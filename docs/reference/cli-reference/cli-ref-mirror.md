---
title: Commande Mirror CLI NuGet
description: Référence pour la commande NuGet. exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959711"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="2fcdc-103">mirror (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2fcdc-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="2fcdc-104">**S’applique à:** publication &bullet; de packages **versions prises en charge:** déconseillé dans 3.2 +</span><span class="sxs-lookup"><span data-stu-id="2fcdc-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="2fcdc-105">Met en miroir un package et ses dépendances à partir des dépôts source spécifiés vers le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="2fcdc-106">NuGet. ServerExtensions. dll et NuGet-Signed. exe qui prenait déjà en charge cette commande dans NuGet 2. x (en renommant NuGet-Signed. exe en NuGet. exe) ne sont plus disponibles au téléchargement.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="2fcdc-107">Pour utiliser une commande similaire à celle-ci, essayez [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="2fcdc-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="2fcdc-108">Usage</span><span class="sxs-lookup"><span data-stu-id="2fcdc-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="2fcdc-109">où `<packageID>` est le package à mettre en miroir `<configFilePath>` , ou `packages.config` identifie le fichier qui répertorie les packages à mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="2fcdc-110">Spécifie le référentiel source et `<publishUrlTarget>` spécifie le référentiel cible. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="2fcdc-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="2fcdc-111">Si votre dépôt cible `https://machine/repo` se trouve sur qui exécute [NuGet. Server](../../hosting-packages/nuget-server.md), la liste et les URL de `https://machine/repo/nuget` transmission sont et `https://machine/repo/api/v2/package`, respectivement.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="2fcdc-112">Options</span><span class="sxs-lookup"><span data-stu-id="2fcdc-112">Options</span></span>

| <span data-ttu-id="2fcdc-113">Option</span><span class="sxs-lookup"><span data-stu-id="2fcdc-113">Option</span></span> | <span data-ttu-id="2fcdc-114">Description</span><span class="sxs-lookup"><span data-stu-id="2fcdc-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2fcdc-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="2fcdc-115">ApiKey</span></span> | <span data-ttu-id="2fcdc-116">Clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-116">The API key for the target repository.</span></span> <span data-ttu-id="2fcdc-117">S’il n’est pas présent, celui spécifié dans le fichier de configuration`%AppData%\NuGet\NuGet.Config` est utilisé (( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="2fcdc-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="2fcdc-118">Aide</span><span class="sxs-lookup"><span data-stu-id="2fcdc-118">Help</span></span> | <span data-ttu-id="2fcdc-119">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="2fcdc-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="2fcdc-120">NoCache</span></span> | <span data-ttu-id="2fcdc-121">Empêche NuGet d’utiliser les packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="2fcdc-122">Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2fcdc-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="2fcdc-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="2fcdc-123">Noop</span></span> | <span data-ttu-id="2fcdc-124">Journalise ce qui serait fait, mais n’effectue pas les actions. suppose la réussite des opérations push.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="2fcdc-125">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="2fcdc-125">PreRelease</span></span> | <span data-ttu-id="2fcdc-126">Comprend des packages de version préliminaire dans l’opération de mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="2fcdc-127">source</span><span class="sxs-lookup"><span data-stu-id="2fcdc-127">Source</span></span> | <span data-ttu-id="2fcdc-128">Liste des sources de package à mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-128">A list of package sources to mirror.</span></span> <span data-ttu-id="2fcdc-129">Si aucune source n’est spécifiée, celles définies dans le fichier de configuration (voir ApiKey ci-dessus) sont utilisées, par défaut nuget.org si aucune n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="2fcdc-130">Délai</span><span class="sxs-lookup"><span data-stu-id="2fcdc-130">Timeout</span></span> | <span data-ttu-id="2fcdc-131">Spécifie le délai d’attente, en secondes, pour effectuer un push vers un serveur.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="2fcdc-132">La valeur par défaut est 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="2fcdc-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="2fcdc-133">Version</span><span class="sxs-lookup"><span data-stu-id="2fcdc-133">Version</span></span> | <span data-ttu-id="2fcdc-134">Version du package à installer.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-134">The version of the package to install.</span></span> <span data-ttu-id="2fcdc-135">S’il n’est pas spécifié, la version la plus récente est mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="2fcdc-136">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2fcdc-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2fcdc-137">Exemples</span><span class="sxs-lookup"><span data-stu-id="2fcdc-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
