---
title: Commande Mirror CLI NuGet
description: Référence pour la commande nuget.exe Mirror
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779171"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="933fa-103">commande Mirror (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="933fa-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="933fa-104">**S’applique à :** publication de packages &bullet; **versions prises en charge :** déconseillé dans 3.2 +</span><span class="sxs-lookup"><span data-stu-id="933fa-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="933fa-105">Met en miroir un package et ses dépendances à partir des dépôts source spécifiés vers le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="933fa-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="933fa-106">NuGet.ServerExtensions.dll et NuGet-Signed.exe qui prenait déjà en charge cette commande dans NuGet 2. x (en renommant NuGet-Signed.exe en nuget.exe) ne sont plus disponibles au téléchargement.</span><span class="sxs-lookup"><span data-stu-id="933fa-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="933fa-107">Pour utiliser une commande similaire à celle-ci, essayez [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="933fa-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="933fa-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="933fa-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="933fa-109">où `<packageID>` est le package à mettre en miroir, ou `<configFilePath>` identifie le `packages.config` fichier qui répertorie les packages à mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="933fa-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="933fa-110">`<listUrlTarget>`Spécifie le référentiel source et `<publishUrlTarget>` spécifie le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="933fa-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="933fa-111">Si votre dépôt cible se trouve sur `https://machine/repo` qui exécute [NuGet. Server](../../hosting-packages/nuget-server.md), la liste et les URL de transmission sont `https://machine/repo/nuget` et `https://machine/repo/api/v2/package` , respectivement.</span><span class="sxs-lookup"><span data-stu-id="933fa-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="933fa-112">Options</span><span class="sxs-lookup"><span data-stu-id="933fa-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="933fa-113">Clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="933fa-113">The API key for the target repository.</span></span> <span data-ttu-id="933fa-114">S’il n’est pas présent, celui spécifié dans le fichier de configuration est utilisé ( `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="933fa-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="933fa-115">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="933fa-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="933fa-116">Empêche NuGet d’utiliser les packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="933fa-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="933fa-117">Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="933fa-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="933fa-118">Journalise ce qui serait fait, mais n’effectue pas les actions. suppose la réussite des opérations push.</span><span class="sxs-lookup"><span data-stu-id="933fa-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="933fa-119">Comprend des packages de version préliminaire dans l’opération de mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="933fa-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="933fa-120">Liste des sources de package à mettre en miroir.</span><span class="sxs-lookup"><span data-stu-id="933fa-120">A list of package sources to mirror.</span></span> <span data-ttu-id="933fa-121">Si aucune source n’est spécifiée, celles définies dans le fichier de configuration (voir ApiKey ci-dessus) sont utilisées, par défaut nuget.org si aucune n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="933fa-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="933fa-122">Spécifie le délai d’attente, en secondes, pour effectuer un push vers un serveur.</span><span class="sxs-lookup"><span data-stu-id="933fa-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="933fa-123">La valeur par défaut est de 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="933fa-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="933fa-124">Version du package à installer.</span><span class="sxs-lookup"><span data-stu-id="933fa-124">The version of the package to install.</span></span> <span data-ttu-id="933fa-125">S’il n’est pas spécifié, la version la plus récente est mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="933fa-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="933fa-126">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="933fa-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="933fa-127">Exemples</span><span class="sxs-lookup"><span data-stu-id="933fa-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
