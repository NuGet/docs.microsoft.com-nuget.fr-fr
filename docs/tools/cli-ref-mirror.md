---
title: Commande de mise en miroir de CLI de NuGet
description: Référence de la commande de mise en miroir de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550204"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="ebbc7-103">mirror (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ebbc7-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="ebbc7-104">**S’applique à :** publication du package &bullet; **versions prises en charge :** déconseillées dans 3.2 +</span><span class="sxs-lookup"><span data-stu-id="ebbc7-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="ebbc7-105">Reflète un package et ses dépendances à partir des référentiels source spécifiée dans le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="ebbc7-106">Pour activer cette commande pour les versions de NuGet avant 3.2, accédez à [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), sélectionnez la version stable la plus récente, téléchargez `NuGet.ServerExtensions.dll` et `Nuget-Signed.exe` vers votre disque local et le changement de nom `Nuget-Signed.exe` à `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="ebbc7-107">Utilisation</span><span class="sxs-lookup"><span data-stu-id="ebbc7-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="ebbc7-108">où `<packageID>` est le package pour mettre en miroir, ou `<configFilePath>` identifie le `packages.config` fichier qui répertorie les packages à mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="ebbc7-109">Le `<listUrlTarget>` Spécifie le référentiel source, et `<publishUrlTarget>` Spécifie le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="ebbc7-110">Si votre référentiel cible se trouve sur `https://machine/repo` qui est en cours d’exécution [NuGet.Server](../hosting-packages/nuget-server.md), les URL de la liste et push sera `https://machine/repo/nuget` et `https://machine/repo/api/v2/package`, respectivement.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="ebbc7-111">Options</span><span class="sxs-lookup"><span data-stu-id="ebbc7-111">Options</span></span>

| <span data-ttu-id="ebbc7-112">Option</span><span class="sxs-lookup"><span data-stu-id="ebbc7-112">Option</span></span> | <span data-ttu-id="ebbc7-113">Description</span><span class="sxs-lookup"><span data-stu-id="ebbc7-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ebbc7-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="ebbc7-114">ApiKey</span></span> | <span data-ttu-id="ebbc7-115">La clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-115">The API key for the target repository.</span></span> <span data-ttu-id="ebbc7-116">Si absent, celle spécifiée dans le fichier de configuration est utilisée (`%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="ebbc7-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="ebbc7-117">Help</span><span class="sxs-lookup"><span data-stu-id="ebbc7-117">Help</span></span> | <span data-ttu-id="ebbc7-118">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="ebbc7-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="ebbc7-119">NoCache</span></span> | <span data-ttu-id="ebbc7-120">Empêche NuGet d’utiliser les packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="ebbc7-121">Consultez [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ebbc7-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="ebbc7-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="ebbc7-122">Noop</span></span> | <span data-ttu-id="ebbc7-123">Enregistre ce qui aurait fait, mais n’effectue pas les actions ; part du principe de réussite pour les opérations de push.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="ebbc7-124">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="ebbc7-124">PreRelease</span></span> | <span data-ttu-id="ebbc7-125">Inclut les packages de version préliminaire dans l’opération de mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="ebbc7-126">Source</span><span class="sxs-lookup"><span data-stu-id="ebbc7-126">Source</span></span> | <span data-ttu-id="ebbc7-127">Une liste des sources de package pour mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-127">A list of package sources to mirror.</span></span> <span data-ttu-id="ebbc7-128">Si aucune source n’est spécifiées, ceux définis dans le fichier de configuration (voir ApiKey ci-dessus) sont utilisés à la valeur par défaut : nuget.org si aucun n’est spécifié.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="ebbc7-129">Délai d'expiration</span><span class="sxs-lookup"><span data-stu-id="ebbc7-129">Timeout</span></span> | <span data-ttu-id="ebbc7-130">Spécifie le délai d’attente, en secondes, pour envoyer vers un serveur.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="ebbc7-131">La valeur par défaut est 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="ebbc7-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="ebbc7-132">Version</span><span class="sxs-lookup"><span data-stu-id="ebbc7-132">Version</span></span> | <span data-ttu-id="ebbc7-133">La version du package à installer.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-133">The version of the package to install.</span></span> <span data-ttu-id="ebbc7-134">Si non spécifié, la version la plus récente est mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="ebbc7-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="ebbc7-135">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ebbc7-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ebbc7-136">Exemples</span><span class="sxs-lookup"><span data-stu-id="ebbc7-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
