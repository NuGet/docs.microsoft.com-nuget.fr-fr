---
title: Recherche et sélection de packages NuGet
description: Explique comment rechercher et sélectionner les packages NuGet les mieux adaptés à votre projet, et fournit des informations détaillées sur la syntaxe de recherche NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 9f427005251bc2bf7a8a79285e39b4bd49062dbf
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428855"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Recherche et sélection des packages NuGet pour votre projet

Lorsque vous démarrez un projet .NET, ou chaque fois que votre application ou votre service a un problème d’ordre fonctionnel, vous pouvez gagner du temps et vous éviter des problèmes en utilisant des packages NuGet existants qui répondent à vos besoins. Ces packages peuvent provenir de la collection publique de [nuget.org](https://www.nuget.org/packages/), ou d’une source privée fournie par votre organisation ou par un tiers.

## <a name="finding-packages"></a>Recherche de packages

Lorsque vous accédez au site nuget.org ou que vous ouvrez l’interface utilisateur du gestionnaire de package dans Visual Studio, vous voyez une liste de packages, dans laquelle ces derniers sont triés par nombre total de téléchargements. Vous voyez ainsi immédiatement les packages qui sont les plus utilisés dans les millions de projets .NET existants. Il est donc très probable que vous trouviez des packages utiles pour vos projets, parmi ceux répertoriés dans les premières pages de la liste.

![Affichage par défaut de nuget.org/packages montrant les packages les plus populaires](media/Finding-01-Popularity.png)

Notez l’option **Inclure la préversion** dans le coin supérieur droit de la page. Lorsque cette option est sélectionnée, nuget.org affiche toutes les versions des packages, y compris la version bêta et autres premières versions. Pour afficher uniquement les versions stables publiées, décochez la case.

Pour des besoins spécifiques, la recherche par mot-clé (dans le Gestionnaire de package de Visual Studio ou sur un portail comme nuget.org) constitue l’approche la plus courante pour trouver un package adapté. Par exemple, si vous effectuez une recherche sur « json », vous obtenez la liste de tous les packages NuGet qui sont marqués avec ce mot clé, et qui ont donc un lien avec le format de données JSON.

![Résultats de recherche pour « json » sur nuget.org](media/Finding-02-SearchResults.png)

Vous pouvez également effectuer une recherche à l’aide de l’ID du package, si vous le connaissez. Consultez [Syntaxe de recherche](#search-syntax) ci-dessous.

Pour l’instant, les résultats de la recherche sont triés uniquement par pertinence. Il est donc conseillé de regarder au moins les quelques premières pages de résultats pour trouver les packages qui répondent le mieux à vos besoins, ou d’affiner vos termes de recherche pour obtenir des résultats plus précis.

### <a name="does-the-package-support-my-projects-target-framework"></a>Le package prend-il en charge la version cible de .NET Framework de mon projet ?

NuGet n’installe un package dans un projet que si les frameworks pris en charge par ce package comprennent la version cible de .NET Framework du projet Si le package n’est pas compatible, NuGet affiche un message d’erreur.

Certains packages répertorient les frameworks qu’ils prennent en charge directement dans la galerie nuget.org. Toutefois, étant donné que ces données ne sont pas obligatoires, de nombreux packages n’incluent pas cette liste. Actuellement, il n’existe aucun moyen de rechercher sur nuget.org les packages qui prennent en charge une version cible de .NET Framework précise (la fonctionnalité est envisagée, voir [Problème NuGet 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Heureusement, il existe d’autres moyens de déterminer les frameworks pris en charge :

1. Essayez d’installer un package dans un projet à l’aide de la commande [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md), dans la console du gestionnaire de package NuGet. Si le package est incompatible, cette commande affiche les frameworks qui sont pris en charge par le package.

1. Téléchargez le package sur nuget.org, en cliquant sur le lien **Manual download** (Téléchargement manuel) situé sous **Info**. Remplacez l’extension `.nupkg` par `.zip`, puis ouvrez le fichier pour examiner le contenu de son dossier `lib`. Vous voyez les sous-dossiers de chacun des frameworks pris en charge, où chaque sous-dossier est nommé avec un moniker de version cible de .NET Framework (TFM, consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md)). Si vous ne voyez aucun sous-dossier sous `lib`, mais seulement une DLL, essayez d’installer le package dans votre projet pour voir s’il est compatible.

## <a name="pre-release-packages"></a>Packages de préversion

De nombreux auteurs de packages sortent des préversions et des versions bêta, dans le but de recevoir les commentaires des utilisateurs et d’apporter d’éventuelles améliorations.

Par défaut, nuget.org affiche les packages de préversion dans les résultats de recherche. Pour rechercher uniquement les versions stables, décochez l’option **Inclure la préversion** située dans le coin supérieur droit de la page.

![Case à cocher Inclure la préversion sur nuget.org](media/Finding-06-include-prerelease.png)

Par défaut, NuGet n’inclut pas les préversions dans Visual Studio, lorsque les outils de l’interface CLI dotnet et NuGet sont utilisés. Pour modifier ce comportement, effectuez les opérations suivantes :

- **Interface utilisateur du gestionnaire de package dans Visual Studio** : dans l’interface utilisateur **Gérer les packages NuGet**, cochez la case **Inclure la préversion**. Le fait de cocher ou décocher cette case actualise l’interface utilisateur du gestionnaire de package et la liste des versions disponibles que vous pouvez installer.

    ![Case à cocher Inclure la préversion dans Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Console du gestionnaire de package** : utilisez le commutateur `-IncludePrerelease` avec les commandes `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` et `Update-Package`. Reportez-vous à [Informations de référence sur PowerShell](../reference/powershell-reference.md).

- **Interface CLI nuget.exe** : utilisez le commutateur `-prerelease` avec les commandes `install`, `update`, `delete` et `mirror`. Reportez-vous à [Informations de référence sur l’interface de ligne de commande NuGet](../reference/nuget-exe-cli-reference.md).

- **Interface CLI dotnet.exe** : spécifiez la préversion exacte à l’aide de l’argument `-v`. Consultez la [référence dotnet Ajouter un package](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Packages C++ natifs

NuGet prend en charge les packages C++ natifs qui peuvent être utilisés dans les projets C++ dans Visual Studio. Cela active la commande de menu contextuel **Gérer les packages NuGet** dans les projets, introduit une version cible de .NET Framework `native` et fournit une intégration MSBuild.

Pour rechercher des packages natifs sur [nuget.org](https://www.nuget.org/packages), utilisez `tag:native`. Ces packages fournissent en général des fichiers `.targets` et `.props`, que NuGet importe automatiquement lorsque le package est ajouté à un projet.

## <a name="evaluating-packages"></a>Évaluation de packages

La meilleure façon d’évaluer l’utilité d’un package consiste à le télécharger et à l’essayer dans votre code (tous les packages présents sur nuget.org font d’ailleurs l’objet d’analyses antivirus régulières). Après tout, au départ, les packages les plus populaires ne sont utilisés que par une poignée de développeurs, et vous pourriez faire partie de ces utilisateurs précoces !

En même temps, utiliser un package NuGet signifie créer une dépendance à celui-ci. Vous devez donc être sûr qu’il est fiable et robuste. Étant donné que l’installation et le test direct d’un package sont des processus relativement longs, il est conseillé de lire les informations fournies dans la page du package pour en savoir plus sur ses qualités :

- *Downloads statistics* (Statistiques de téléchargement) : dans la page du package sur nuget.org, la section **Statistics** (Statistiques) indique le nombre total de téléchargements, les téléchargements de la version la plus récente, et le nombre moyen de téléchargements par jour. Un nombre élevé signifie que de nombreux développeurs dépendent de ce package, et donc que celui-ci a fait ses preuves.

    ![Statistiques de téléchargement dans la page du package](media/Finding-03-Downloads.png)

- *Utilisation de GitHub*: sur la page package, la section **utilisation de GitHub** répertorie les dépôts GitHub publics qui dépendent de ce package et qui ont un grand nombre d’étoiles sur GitHub. Le nombre d’étoiles d’un dépôt GitHub indique généralement le degré d’actualité du référentiel avec les utilisateurs GitHub (d’autres étoiles signifient généralement plus populaires). Visitez [la page de prise en main de GitHub](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars) pour plus d’informations sur les étoiles et le système de classement des référentiels de github.

    ![Utilisation de GitHub](media/GitHub-Usage.png)

    > [!Note]
    > La section utilisation du GitHub d’un package est générée automatiquement, périodiquement, sans examen humain des dépôts individuels, et uniquement à des fins d’information afin de vous montrer les dépôts GitHub qui dépendent du package et qui sont populaires avec GitHub utilisateurs.

- *Version history* (Historique des versions) : dans la page du package, regardez sous **Info** pour connaître la date de la mise à jour la plus récente et consulter l’historique des versions (**Version History**). Un package bien géré doit comprendre des mises à jour récentes et un historique des versions très fourni. Les packages négligés comprennent peu de mises à jour et, souvent, n’ont pas été mis à jour depuis un certain temps.

    ![Historique des versions dans la page du package](media/Finding-04-VersionHistory.png)

- *Installations récentes*: sur la page package sous **statistiques**, sélectionnez **afficher les statistiques complètes**. La page des statistiques complètes affiche le package installé au cours des six dernières semaines par numéro de version. Généralement, les packages très utilisés par les autres développeurs constituent un bon choix.

- *Support* : sur la page du package, sous **Info**, sélectionnez **Project Site** (Site du projet), le cas échéant, pour afficher les options de support proposées par l’auteur. Un projet avec un site dédié est généralement mieux pris en charge.

- *Developer history* (Historique des développeurs) : dans la page du package, sous **Owners** (Propriétaires), sélectionnez un propriétaire pour voir les autres packages qu’il a publiés. Les développeurs qui ont publié plusieurs packages sont davantage susceptibles de continuer la prise en charge de leur package.

- *Open source contributions* (Contributions open source) : de nombreux packages sont conservés dans des référentiels open source, ce qui permet aux développeurs qui en dépendent de contribuer directement aux correctifs de bogues et à l’amélioration des fonctionnalités. L’historique des contributions d’un package donné est également un bon indicateur du nombre de développeurs activement impliqués.

- *Interview the owners* (Interroger les propriétaires) : les nouveaux développeurs peuvent eux aussi produire des packages de grande qualité. Il est donc bon de leur permettre d’apporter quelque chose de nouveau à l’écosystème NuGet. Vous pouvez alors contacter directement les développeurs du package via l’option **Contact Owners** (Contacter les propriétaires) sous **Info**, dans la page du package. Ils seront très probablement contents de collaborer avec vous et de répondre à vos besoins !

- *Reserved Package ID Prefixes* (Préfixes d’ID de packages réservés) : de nombreux propriétaires de packages ont demandé et reçu un [préfixe d’ID de package réservé](../nuget-org/id-prefix-reservation.md). Quand vous voyez la coche à côté d’un ID de package sur [nuget.org](https://www.nuget.org/) ou dans Visual Studio, cela signifie que le propriétaire du package a répondu à nos [critères](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) pour la réservation d’ID de préfixe. Cela signifie que le propriétaire du package est clair quant à l’identification de lui-même et de son package.

> [!Note]
> Gardez toujours à l’esprit les termes du contrat de licence d’un package, que vous pouvez consulter en sélectionnant les **informations de licence** sur la page de liste d’un package sur NuGet.org. Si un package ne spécifie pas les termes du contrat de licence, contactez le propriétaire du package directement à l’aide du lien **contacter les propriétaires** sur la page du package. Microsoft ne vous accorde pas de licences de droits de propriété intellectuelle pour le compte de fournisseurs de packages tiers et n’est pas responsable des informations fournies par des tiers.

## <a name="license-url-deprecation"></a>Dépréciation d’URL de licence
Avec le passage de [licenseUrl](../reference/nuspec.md#licenseurl) vers [licence](../reference/nuspec.md#license), des clients et flux NuGet risquent de ne pas pouvoir accéder aux informations de licence dans certains cas. Pour maintenir une compatibilité descendante, l’URL de la licence pointe vers ce document, qui explique comment récupérer les informations de licence dans ces situations.

Si vous cliquez sur l’URL de la licence pour un package qui vous avez amené sur cette page, cela signifie que le package contient un fichier de licence et
* Vous êtes connecté à un flux qui ne sait pas encore comment interpréter et afficher les nouvelles informations de licence pour le client **OU**
* Vous utilisez un client qui ne sait pas encore comment interpréter et lire les nouvelles informations de licence potentiellement fournies par le flux **OU**
* Une combinaison de ces deux cas

Voici comment vous pouvez lire les informations contenues dans le fichier de licence à l’intérieur du package :
1. Téléchargez le package NuGet et décompressez son contenu dans un dossier.
1. Ouvrez le fichier `.nuspec` situé à la racine de ce dossier.
1. Il devrait contenir une balise de type `<license type="file">license\license.txt</license>`. Cela implique que le fichier de licence est nommé `license.txt` et se trouve à l’intérieur d’un dossier `license` également à la racine de ce dossier.
1. Accédez au dossier `license` et ouvrez le fichier `license.txt`.

Pour découvrir l’équivalent MSBuild à la définition de la licence dans le `.nuspec`, consultez [Packing a license expression or a license file](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file) (Compression d’une expression de licence ou d’un fichier de licence).

## <a name="search-syntax"></a>Syntaxe de recherche

La recherche de packages NuGet fonctionne de la même manière sur nuget.org, dans l’interface CLI de NuGet et dans l’extension du gestionnaire de package NuGet de Visual Studio. En règle générale, la recherche s’appuie sur les mots clés et les descriptions des packages.

- **Filtrage** : vous pouvez appliquer un terme de recherche à une propriété spécifique à l’aide de la syntaxe `<property>:<term>`, où `<property>` (non sensible à la casse) peut être `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary` ou `owner`. Vous pouvez rechercher plusieurs propriétés en même temps. Les recherches sur la propriété `id` sont des correspondances de sous-chaînes, tandis que `packageid` et `owner` utilisent une correspondance exacte qui ne respecte pas la casse. Exemples :

```
PackageId:jquery             # Match the package ID in an exact, case-insensitive manner

owner:microsoft              # Match the owner in an exact, case-insensitive manner

id:NuGet.Core                # Match any part of the ID property
Id:"Nuget.Core"
ID:jQuery
id:jquery id:ui              # Search for multiple terms in the ID
id:jquery tags:validation    # Search multiple properties

invalid:jquery ui            # Unsupported properties are ignored, so this
                             # is the same as searching on ui
```
