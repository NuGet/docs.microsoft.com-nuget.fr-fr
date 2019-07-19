---
title: Commande Mirror CLI NuGet
description: Référence pour la commande NuGet. exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327666"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="3b4f0-103">mirror (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3b4f0-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="3b4f0-104">**S’applique à:** publication &bullet; de packages **versions prises en charge:** déconseillé dans 3.2 +</span><span class="sxs-lookup"><span data-stu-id="3b4f0-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="3b4f0-105">Met en miroir un package et ses dépendances à partir des dépôts source spécifiés vers le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="3b4f0-106">Pour activer cette commande pour les versions de NuGet antérieures à 3,2 [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), accédez à, sélectionnez la version stable `NuGet.ServerExtensions.dll` la `Nuget-Signed.exe` plus récente, téléchargez et `nuget.exe` sur votre `Nuget-Signed.exe` disque local et renommez-la.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="3b4f0-107">Usage</span><span class="sxs-lookup"><span data-stu-id="3b4f0-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="3b4f0-108">où `<packageID>` est le package à mettre en miroir `<configFilePath>` , ou `packages.config` identifie le fichier qui répertorie les packages à mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="3b4f0-109">Spécifie le référentiel source et `<publishUrlTarget>` spécifie le référentiel cible. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="3b4f0-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="3b4f0-110">Si votre dépôt cible `https://machine/repo` se trouve sur qui exécute [NuGet. Server](../../hosting-packages/nuget-server.md), la liste et les URL de `https://machine/repo/nuget` transmission sont et `https://machine/repo/api/v2/package`, respectivement.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="3b4f0-111">Options</span><span class="sxs-lookup"><span data-stu-id="3b4f0-111">Options</span></span>

| <span data-ttu-id="3b4f0-112">Option</span><span class="sxs-lookup"><span data-stu-id="3b4f0-112">Option</span></span> | <span data-ttu-id="3b4f0-113">Description</span><span class="sxs-lookup"><span data-stu-id="3b4f0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b4f0-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="3b4f0-114">ApiKey</span></span> | <span data-ttu-id="3b4f0-115">Clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-115">The API key for the target repository.</span></span> <span data-ttu-id="3b4f0-116">S’il n’est pas présent, celui spécifié dans le fichier de configuration`%AppData%\NuGet\NuGet.Config` est utilisé (( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="3b4f0-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="3b4f0-117">Aide</span><span class="sxs-lookup"><span data-stu-id="3b4f0-117">Help</span></span> | <span data-ttu-id="3b4f0-118">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="3b4f0-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="3b4f0-119">NoCache</span></span> | <span data-ttu-id="3b4f0-120">Empêche NuGet d’utiliser les packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="3b4f0-121">Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3b4f0-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="3b4f0-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="3b4f0-122">Noop</span></span> | <span data-ttu-id="3b4f0-123">Journalise ce qui serait fait, mais n’effectue pas les actions. suppose la réussite des opérations push.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="3b4f0-124">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="3b4f0-124">PreRelease</span></span> | <span data-ttu-id="3b4f0-125">Comprend des packages de version préliminaire dans l’opération de mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="3b4f0-126">source</span><span class="sxs-lookup"><span data-stu-id="3b4f0-126">Source</span></span> | <span data-ttu-id="3b4f0-127">Liste des sources de package à mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-127">A list of package sources to mirror.</span></span> <span data-ttu-id="3b4f0-128">Si aucune source n’est spécifiée, celles définies dans le fichier de configuration (voir ApiKey ci-dessus) sont utilisées, par défaut nuget.org si aucune n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="3b4f0-129">Délai</span><span class="sxs-lookup"><span data-stu-id="3b4f0-129">Timeout</span></span> | <span data-ttu-id="3b4f0-130">Spécifie le délai d’attente, en secondes, pour effectuer un push vers un serveur.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="3b4f0-131">La valeur par défaut est 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="3b4f0-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="3b4f0-132">Version</span><span class="sxs-lookup"><span data-stu-id="3b4f0-132">Version</span></span> | <span data-ttu-id="3b4f0-133">Version du package à installer.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-133">The version of the package to install.</span></span> <span data-ttu-id="3b4f0-134">S’il n’est pas spécifié, la version la plus récente est mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="3b4f0-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="3b4f0-135">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3b4f0-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3b4f0-136">Exemples</span><span class="sxs-lookup"><span data-stu-id="3b4f0-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
