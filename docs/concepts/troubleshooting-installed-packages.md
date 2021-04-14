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
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="6f0a6-103">Résolution des problèmes de packages installés</span><span class="sxs-lookup"><span data-stu-id="6f0a6-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="6f0a6-104">Il peut arriver que vous souhaitiez valider la source à partir de laquelle un package spécifique a été installé.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="6f0a6-105">Voici quelques méthodes que vous pouvez vérifier.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="6f0a6-106">Certaines sources de package prennent en charge un concept connu sous le nom de sources amont.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="6f0a6-107">Par exemple, [Azure artifacts sources amont](/azure/devops/artifacts/concepts/upstream-sources).</span><span class="sxs-lookup"><span data-stu-id="6f0a6-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="6f0a6-108">Les clients NuGet ne savent pas si un package provient d’une source amont.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="6f0a6-109">Par conséquent, toute journalisation de la source du package répertorie la source configurée, et non la source amont.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="6f0a6-110">`.nupkg.metadata` fichier dans le dossier des packages globaux</span><span class="sxs-lookup"><span data-stu-id="6f0a6-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="6f0a6-111">Lorsqu’un package est extrait dans le dossier *Global-packages* , un fichier `.nupkg.metadata` est écrit.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="6f0a6-112">Depuis NuGet 5.9.0, NuGet ajoute la source du package.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="6f0a6-113">Voir ci-dessous pour mapper des versions NuGet à Visual Studio ou à des versions du kit de développement logiciel (SDK) .NET.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="6f0a6-114">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6f0a6-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="6f0a6-115">Si votre dossier *Global-packages* contient des packages extraits avant la mise à niveau vers une version plus récente des outils avec NuGet 5.9.0, le fichier sera la `.nupkg.metadata` version 1 et ne contiendra pas la source du package.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="6f0a6-116">Vous pouvez [effacer votre dossier *Global-packages*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) pour vous assurer que tous les packages contiendront la source du package.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="6f0a6-117">NuGet écrit le `.nupkg.metadata` fichier dans le dossier *Global-packages* uniquement.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="6f0a6-118">Les projets `packages.config` qui utilisent utilisent un dossier de packages de solution, qui ne crée pas de `.nupkg.metadata` fichier.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="6f0a6-119">Message du journal des packages installés</span><span class="sxs-lookup"><span data-stu-id="6f0a6-119">Installed package log message</span></span>

<span data-ttu-id="6f0a6-120">Depuis NuGet 5.9.0, NuGet génère la source du package dans le message de restauration informant qu’un package a été installé.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="6f0a6-121">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6f0a6-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="6f0a6-122">Ce message est généré à un niveau de détail normal/informatif.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="6f0a6-123">Visual Studio et l' `dotnet` interface CLI ont par défaut un niveau de détail minimal. ce message n’est donc pas visible par défaut.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="6f0a6-124">Les `msbuild` `nuget` Outils CLI et ont par défaut un niveau de détail normal. ce message sera donc visible par défaut.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="6f0a6-125">Message du journal HTTP</span><span class="sxs-lookup"><span data-stu-id="6f0a6-125">HTTP log message</span></span>

<span data-ttu-id="6f0a6-126">Lorsqu’un package n’est pas disponible localement, que ce soit dans le dossier *Global-packages* , dans un dossier de secours ou dans une source de fichier local, NuGet le télécharge à partir de n’importe quelle source de package configurée sur http.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="6f0a6-127">Les requêtes et les réponses HTTP sont journalisées au niveau de détail normal, et vous ne devriez voir qu’une seule demande et réponse par version de package.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="6f0a6-128">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6f0a6-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="6f0a6-129">Si les fichiers ont été téléchargés récemment, ils peuvent être récupérés à partir du *Cache http* de NuGet</span><span class="sxs-lookup"><span data-stu-id="6f0a6-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="6f0a6-130">Le format d’URL peut être différent pour différentes implémentations de serveur HTTP NuGet et s’il implémente NuGet v2 ou le protocole HTTP v3.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="6f0a6-131">Si `nuget.config` vous avez défini plusieurs sources http, vous verrez plusieurs demandes dans le fichier de chaque package `index.json` , une pour chaque source.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="6f0a6-132">Mais il n’y aura qu’un seul `nupkg` téléchargement pour chaque version du package.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="6f0a6-133">Message du journal de signature du package</span><span class="sxs-lookup"><span data-stu-id="6f0a6-133">Package signature log message</span></span>

<span data-ttu-id="6f0a6-134">Si le package téléchargé est signé, NuGet validera la signature et enregistrera le message suivant en détail :</span><span class="sxs-lookup"><span data-stu-id="6f0a6-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="6f0a6-135">Ce message indique si le package a été téléchargé à partir d’une source de package HTTP, ou s’il a été copié à partir d’une source de package locale.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="6f0a6-136">Il ne sera pas généré si le package est déjà disponible dans le dossier *Global-packages* ou dans un dossier de secours.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="6f0a6-137">En raison de la [Suppression de l’approbation de VeriSign ca](https://github.com/dotnet/announcements/issues/180) NuGet, la vérification des packages signés est désactivée sur certaines plateformes, dans certaines versions de NuGet et du kit de développement logiciel (SDK) .net.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="6f0a6-138">Par conséquent, les mêmes Packages peuvent avoir des `PackageSignatureVerificationLog` journaux, ou ces journaux peuvent être manquants, en fonction de la plateforme sur laquelle vous exécutez la restauration et de la version de .net ou de NuGet que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="6f0a6-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="6f0a6-139">Mappage de version NuGet</span><span class="sxs-lookup"><span data-stu-id="6f0a6-139">NuGet Version Map</span></span>

<span data-ttu-id="6f0a6-140">Les versions suivantes de NuGet présentent des modifications importantes concernant la journalisation de la source du package :</span><span class="sxs-lookup"><span data-stu-id="6f0a6-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="6f0a6-141">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="6f0a6-141">NuGet Version</span></span>|<span data-ttu-id="6f0a6-142">Version de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f0a6-142">Visual Studio Version</span></span>|<span data-ttu-id="6f0a6-143">Version du SDK .NET</span><span class="sxs-lookup"><span data-stu-id="6f0a6-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="6f0a6-144">5.9.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="6f0a6-144">NuGet 5.9.0</span></span>|<span data-ttu-id="6f0a6-145">16.9.0 Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="6f0a6-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="6f0a6-146">KIT DE DÉVELOPPEMENT LOGICIEL (SDK) .NET 5 5.0.200</span><span class="sxs-lookup"><span data-stu-id="6f0a6-146">.NET 5 SDK 5.0.200</span></span>|
