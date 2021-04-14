---
title: Résolution des problèmes de packages installés
description: Recherche de la source de package utilisée pour les packages individuels
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387570"
---
# <a name="troubleshooting-installed-packages"></a>Résolution des problèmes de packages installés

Il peut arriver que vous souhaitiez valider la source à partir de laquelle un package spécifique a été installé. Voici quelques méthodes que vous pouvez vérifier.

> [!Note]
> Certaines sources de package prennent en charge un concept connu sous le nom de sources amont. Par exemple, [Azure artifacts sources amont](/azure/devops/artifacts/concepts/upstream-sources). Les clients NuGet ne savent pas si un package provient d’une source amont. Par conséquent, toute journalisation de la source du package répertorie la source configurée, et non la source amont.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>`.nupkg.metadata` fichier dans le dossier des packages globaux

Lorsqu’un package est extrait dans le dossier *Global-packages* , un fichier `.nupkg.metadata` est écrit. Depuis NuGet 5.9.0, NuGet ajoute la source du package. Voir ci-dessous pour mapper des versions NuGet à Visual Studio ou à des versions du kit de développement logiciel (SDK) .NET. Par exemple :

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> Si votre dossier *Global-packages* contient des packages extraits avant la mise à niveau vers une version plus récente des outils avec NuGet 5.9.0, le fichier sera la `.nupkg.metadata` version 1 et ne contiendra pas la source du package. Vous pouvez [effacer votre dossier *Global-packages*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) pour vous assurer que tous les packages contiendront la source du package.

> [!Tip]
> NuGet écrit le `.nupkg.metadata` fichier dans le dossier *Global-packages* uniquement. Les projets `packages.config` qui utilisent utilisent un dossier de packages de solution, qui ne crée pas de `.nupkg.metadata` fichier.

## <a name="installed-package-log-message"></a>Message du journal des packages installés

Depuis NuGet 5.9.0, NuGet génère la source du package dans le message de restauration informant qu’un package a été installé. Par exemple :

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> Ce message est généré à un niveau de détail normal/informatif. Visual Studio et l' `dotnet` interface CLI ont par défaut un niveau de détail minimal. ce message n’est donc pas visible par défaut. Les `msbuild` `nuget` Outils CLI et ont par défaut un niveau de détail normal. ce message sera donc visible par défaut.

## <a name="http-log-message"></a>Message du journal HTTP

Lorsqu’un package n’est pas disponible localement, que ce soit dans le dossier *Global-packages* , dans un dossier de secours ou dans une source de fichier local, NuGet le télécharge à partir de n’importe quelle source de package configurée sur http. Les requêtes et les réponses HTTP sont journalisées au niveau de détail normal, et vous ne devriez voir qu’une seule demande et réponse par version de package. Par exemple :

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

Si les fichiers ont été téléchargés récemment, ils peuvent être récupérés à partir du *Cache http* de NuGet

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

Le format d’URL peut être différent pour différentes implémentations de serveur HTTP NuGet et s’il implémente NuGet v2 ou le protocole HTTP v3.

Si `nuget.config` vous avez défini plusieurs sources http, vous verrez plusieurs demandes dans le fichier de chaque package `index.json` , une pour chaque source. Mais il n’y aura qu’un seul `nupkg` téléchargement pour chaque version du package.

## <a name="package-signature-log-message"></a>Message du journal de signature du package

Si le package téléchargé est signé, NuGet validera la signature et enregistrera le message suivant en détail :

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

Ce message indique si le package a été téléchargé à partir d’une source de package HTTP, ou s’il a été copié à partir d’une source de package locale. Il ne sera pas généré si le package est déjà disponible dans le dossier *Global-packages* ou dans un dossier de secours.

> [!Important]
> En raison de la [Suppression de l’approbation de VeriSign ca](https://github.com/dotnet/announcements/issues/180) NuGet, la vérification des packages signés est désactivée sur certaines plateformes, dans certaines versions de NuGet et du kit de développement logiciel (SDK) .net. Par conséquent, les mêmes Packages peuvent avoir des `PackageSignatureVerificationLog` journaux, ou ces journaux peuvent être manquants, en fonction de la plateforme sur laquelle vous exécutez la restauration et de la version de .net ou de NuGet que vous utilisez.

## <a name="nuget-version-map"></a>Mappage de version NuGet

Les versions suivantes de NuGet présentent des modifications importantes concernant la journalisation de la source du package :

|Version de NuGet|Version de Visual Studio|Version du SDK .NET|
|---|---|---|
|5.9.0 NuGet|16.9.0 Visual Studio 2019|KIT DE DÉVELOPPEMENT LOGICIEL (SDK) .NET 5 5.0.200|
