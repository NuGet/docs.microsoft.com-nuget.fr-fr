---
title: Rechercher à l’aide d’une requête tous les packages publiés sur nuget.org
description: À l’aide de l’API NuGet, vous pouvez rechercher au moyen d’une requête tous les packages publiés sur nuget.org et rester à jour au fil du temps.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498235"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Rechercher à l’aide d’une requête tous les packages publiés sur nuget.org

Un modèle de requête courant sur l’API OData V2 héritée consistait à énumérer tous les packages publiés sur nuget.org, classés par date d’installation. Les scénarios nécessitant ce type de requête sur nuget.org sont très variés :

- Réplication complète de nuget.org
- Détection de la disponibilité de nouvelles versions de packages
- Recherche de packages dépendant de votre package

Pour effectuer cette opération, il fallait généralement trier l’entité de package OData par un horodatage et parcourir le jeu de résultats massif au moyen d’une pagination à l’aide des paramètres `skip` et `top` (taille de page). Malheureusement, cette approche présente certains inconvénients :

- Possibilité d’absence de packages, les requêtes étant exécutées sur des données dont l’ordre est souvent modifié
- Lenteur du temps de réponse aux requêtes, celles-ci n’étant pas optimisées (les requêtes les plus optimisées sont celles qui prennent en charge un scénario principal pour le client NuGet officiel)
- Utilisation d’une API dépréciée et non documentée, ce qui compromet la prise en charge future de ces requêtes
- Impossibilité de relire l’historique dans l’ordre exact de son déroulement

Pour cette raison, vous pouvez suivre le guide ci-après pour résoudre les scénarios cités plus haut d’une manière plus fiable et évolutive.

## <a name="overview"></a>Vue d’ensemble

Ce guide repose sur une ressource de [l’API NuGet](../../api/overview.md) appelée **catalogue**. Le catalogue est une API annexe uniquement qui permet à l’appelant de voir une histoire complète des paquets ajoutés, modifiés et supprimés de nuget.org. Si vous êtes intéressé par tout ou même un sous-ensemble de paquets publiés à nuget.org, le catalogue est un excellent moyen de rester à jour avec l’ensemble des paquets actuellement disponibles au fil du temps.

Ce guide est conçu comme une procédure générale, mais si vous êtes intéressé par des détails précis du catalogue, consultez le [document de référence sur l’API](../../api/catalog-resource.md).

Les étapes suivantes peuvent être implémentées dans le langage de programmation de votre choix. Si vous souhaitez un exemple complet, jetez un œil à [l’exemple C#](#c-sample-code) mentionné plus bas.

Sinon, suivez le guide ci-dessous pour créer un lecteur de catalogue fiable.

## <a name="initialize-a-cursor"></a>Initialiser un curseur

La première étape de la création d’un lecteur de catalogue fiable consiste à implémenter un curseur. Pour plus d’informations sur la conception d’un curseur de catalogue, consultez le [document de référence sur le catalogue](../../api/catalog-resource.md#cursor). En bref, le curseur est un point dans le temps jusqu’auquel vous avez traité des événements dans le catalogue. Les événements dans le catalogue représentent des publications de package et autres modifications de package. Si vous vous intéressez à tous les packages publiés sur NuGet (depuis le tout début), vous initialisez votre curseur sur un horodatage de « valeur minimale » (par exemple, `DateTime.MinValue` dans .NET). Si seuls vous intéressent les packages publiés à partir de maintenant, vous utilisez l’horodatage actuel comme valeur de curseur initiale.

Dans ce guide, nous allons initialiser notre curseur sur un horodatage remontant à une heure. Pour l’instant, enregistrez simplement l’horodatage en mémoire.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Déterminer l’URL de l’index du catalogue

L’emplacement de chaque ressource (point de terminaison) dans l’API NuGet doit être découvert à l’aide de [l’index de service](../../api/service-index.md). Étant donné que ce guide se concentre sur nuget.org, nous allons utiliser l’index de service de nuget.org.

    GET https://api.nuget.org/v3/index.json

Le document de service est un document JSON contenant toutes les ressources sur nuget.org. Recherchez la ressource `@type` ayant `Catalog/3.0.0`la valeur de propriété de . La valeur de propriété `@id` associée est l’URL de l’index du catalogue. 

## <a name="find-new-catalog-leaves"></a>Rechercher de nouvelles feuilles de catalogue

À l’aide de la valeur de propriété `@id` trouvée à l’étape précédente, téléchargez l’index du catalogue :

    GET https://api.nuget.org/v3/catalog0/index.json

Désérialisez [l’index du catalogue](../../api/catalog-resource.md#catalog-index). Éliminez par filtrage tous les [objets de page de catalogue](../../api/catalog-resource.md#catalog-page-object-in-the-index) pour lesquels `commitTimeStamp` est inférieur ou égal à la valeur actuelle de votre curseur.

Pour chaque page de catalogue restante, téléchargez le document entier à l’aide de la propriété `@id`.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Désérialisez [la page du catalogue](../../api/catalog-resource.md#catalog-page). Éliminez par filtrage tous les [objets de feuille de catalogue](../../api/catalog-resource.md#catalog-item-object-in-a-page) pour lesquels `commitTimeStamp` est inférieur ou égal à la valeur actuelle de votre curseur.

Après avoir téléchargé toutes les pages de catalogue non éliminées par filtrage, vous disposez d’un ensemble d’objets de feuille de catalogue représentant les packages qui ont été publiés, supprimés de la liste, répertoriés ou supprimés entre l’horodatage de votre curseur et maintenant.

## <a name="process-catalog-leaves"></a>Traiter les feuilles du catalogue

À ce stade, vous pouvez effectuer n’importe quel traitement personnalisé sur les éléments du catalogue. Si vous avez uniquement besoin de l’ID et de la version du package, vous pouvez inspecter les propriétés `nuget:id` et `nuget:version` sur les objets d’élément de catalogue trouvés dans les pages. Veillez à examiner la propriété `@type` pour savoir si l’élément de catalogue concerne un package existant ou un package supprimé.

Si vous êtes intéressé par les métadonnées relatives au package (par exemple, la description, les dépendances, la taille du fichier .nupkg, etc.), vous pouvez extraire le [document de feuille du catalogue](../../api/catalog-resource.md#catalog-leaf) à l’aide de la propriété `@id`.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Ce document contient, entre autres, toutes les métadonnées incluses dans la [ressource des métadonnées du package](../../api/registration-base-url-resource.md).

Cette étape est celle où vous implémentez votre logique personnalisée. Les autres étapes de ce guide sont implémentées pratiquement de la même façon, quelle que soit l’opération que vous effectuez avec les feuilles de catalogue.

### <a name="downloading-the-nupkg"></a>Téléchargement du fichier .nupkg

Si vous souhaitez télécharger le fichier .nupkg des packages trouvés dans le catalogue, vous pouvez utiliser la [ressource de contenu de package](../../api/package-base-address-resource.md). Toutefois, notez qu’un court délai s’écoule entre le moment où un package est trouvé dans le catalogue et le moment où il est disponible dans la ressource de contenu du package. Ainsi, si vous rencontrez `404 Not Found` quand vous tentez de télécharger un fichier .nupkg pour un package que vous avez trouvé dans le catalogue, réessayez simplement un peu plus tard. La résolution de ce délai fait l’objet d’un suivi dans le sujet GitHub [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Avancer le curseur

Une fois que vous avez correctement traité les éléments du catalogue, vous devez déterminer la nouvelle valeur de curseur à enregistrer. Pour ce faire, recherchez la valeur `commitTimeStamp` maximale (la plus récente chronologiquement) de tous les éléments de catalogue que vous avez traités. Il s’agit de votre nouvelle valeur du curseur. Enregistrez-la dans un magasin persistant, tel qu’une base de données, le système de fichiers ou le stockage d’objets blob. Quand vous souhaitez obtenir plus d’éléments de catalogue, démarrez simplement à la [première étape](#initialize-a-cursor) en initialisant la valeur de votre curseur à partir de ce magasin persistant.

Si votre application lève une exception ou des erreurs, n’avancez pas le curseur. Avancer le curseur signifie que vous n’avez plus besoin de traiter les éléments de catalogue situés avant le curseur.

Si, pour une raison quelconque, un bogue affecte le traitement des feuilles de catalogue, vous pouvez simplement reculer le curseur dans le temps et autoriser votre code à retraiter les anciens éléments de catalogue.

## <a name="c-sample-code"></a>Exemple de code C#

Le catalogue étant un ensemble de documents JSON disponibles via HTTP, vous pouvez interagir avec lui à l’aide de n’importe quel langage de programmation qui dispose d’un client HTTP et d’un désérialiseur JSON.

Des exemples C# sont disponibles dans le [dépôt NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>SDK du catalogue

Pour consommer le catalogue, le plus simple consiste à utiliser le package du SDK du catalogue .NET (préversion) : [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Ce package est disponible sur le flux `nuget-build` MyGet, pour lequel vous utilisez l’URL source de package NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.

Vous pouvez installer ce package sur un projet compatible avec `netstandard1.3` ou version supérieure (par exemple, .NET Framework 4.6).

Un exemple d’utilisation de ce package est disponible sur GitHub dans le [projet NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

#### <a name="sample-output"></a>Exemple de sortie

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>Exemple minimal

Pour obtenir un exemple avec moins de dépendances qui illustre l’interaction avec le catalogue de façon plus détaillée, consultez [l’exemple de projet CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Le projet cible `netcoreapp2.0` et dépend de [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (pour la résolution de l’index de service) et de [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (pour la désérialisation du JSON).

La logique principale du code est visible dans le [fichier Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

#### <a name="sample-output"></a>Exemple de sortie

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
