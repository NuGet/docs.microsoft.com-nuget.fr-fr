---
title: Commande de mise en miroir de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande de mise en miroir de nuget.exe"
keywords: "référence de mise en miroir de NuGet, les commandes de mise en miroir"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff5f1c1a915943e8a2eb9c6d6ab09a850968371
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="cc3e6-104">commande de mise en miroir (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cc3e6-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="cc3e6-105">**S’applique à :** la publication du package &bullet; **versions prises en charge :** déconseillée dans 3.2 +</span><span class="sxs-lookup"><span data-stu-id="cc3e6-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="cc3e6-106">Reflète un package et ses dépendances à partir des référentiels source spécifiée dans le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="cc3e6-107">Pour activer cette commande pour les versions de NuGet avant 3.2, accédez à [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), sélectionnez la dernière version stable, téléchargez `NuGet.ServerExtensions.dll` et `Nuget-Signed.exe` à votre disque local et le changement de nom `Nuget-Signed.exe` à `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="cc3e6-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="cc3e6-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="cc3e6-109">où `<packageID>` est le package pour mettre en miroir, ou `<configFilePath>` identifie les `packages.config` fichier qui répertorie les packages à mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="cc3e6-110">Le `<listUrlTarget>` Spécifie le référentiel de code source, et `<publishUrlTarget>` Spécifie le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="cc3e6-111">Si votre référentiel cible se trouve sur `https://machine/repo` qui est en cours d’exécution [NuGet.Server](../hosting-packages/NuGet-Server.md), les URL de liste et push sera `https://machine/repo/nuget` et `https://machine/repo/api/v2/package`, respectivement.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/NuGet-Server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="cc3e6-112">Options</span><span class="sxs-lookup"><span data-stu-id="cc3e6-112">Options</span></span>

| <span data-ttu-id="cc3e6-113">Option</span><span class="sxs-lookup"><span data-stu-id="cc3e6-113">Option</span></span> | <span data-ttu-id="cc3e6-114">Description</span><span class="sxs-lookup"><span data-stu-id="cc3e6-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc3e6-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="cc3e6-115">ApiKey</span></span> | <span data-ttu-id="cc3e6-116">La clé d’API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-116">The API key for the target repository.</span></span> <span data-ttu-id="cc3e6-117">Si absent, celui spécifié dans *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="cc3e6-118">Help</span><span class="sxs-lookup"><span data-stu-id="cc3e6-118">Help</span></span> | <span data-ttu-id="cc3e6-119">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="cc3e6-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="cc3e6-120">NoCache</span></span> | <span data-ttu-id="cc3e6-121">NuGet empêche l’utilisation de packages de caches de l’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="cc3e6-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="cc3e6-122">Noop</span></span> | <span data-ttu-id="cc3e6-123">Journaux seront effectuées, mais n’effectue pas les actions. suppose la réussite des opérations de push.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="cc3e6-124">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="cc3e6-124">PreRelease</span></span> | <span data-ttu-id="cc3e6-125">Inclut les versions préliminaires des packages dans l’opération de mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="cc3e6-126">Source</span><span class="sxs-lookup"><span data-stu-id="cc3e6-126">Source</span></span> | <span data-ttu-id="cc3e6-127">Liste des sources de package pour mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-127">A list of package sources to mirror.</span></span> <span data-ttu-id="cc3e6-128">Si aucune source n’est spécifiées, ceux définis dans *%AppData%\NuGet\NuGet.Config* sont utilisés, la valeur par défaut : nuget.org si aucune n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="cc3e6-129">Délai d'expiration</span><span class="sxs-lookup"><span data-stu-id="cc3e6-129">Timeout</span></span> | <span data-ttu-id="cc3e6-130">Spécifie le délai d’attente, en secondes, en exécutant un push sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="cc3e6-131">La valeur par défaut est 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="cc3e6-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="cc3e6-132">Version</span><span class="sxs-lookup"><span data-stu-id="cc3e6-132">Version</span></span> | <span data-ttu-id="cc3e6-133">La version du package à installer.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-133">The version of the package to install.</span></span> <span data-ttu-id="cc3e6-134">Si non spécifié, la version la plus récente est mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="cc3e6-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="cc3e6-135">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cc3e6-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cc3e6-136">Exemples</span><span class="sxs-lookup"><span data-stu-id="cc3e6-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
