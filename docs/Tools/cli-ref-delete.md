---
title: Commande delete de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informations de référence pour la commande de suppression de nuget.exe"
keywords: "supprimer la référence de NuGet, supprimer la commande de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b5d53b83cdccaa8e284b844786b0ec27e7afb63a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="5e21d-104">supprimer la commande (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5e21d-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="5e21d-105">**S’applique à :** la publication du package &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="5e21d-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5e21d-106">Supprime ou unlists un package à partir d’une source de package.</span><span class="sxs-lookup"><span data-stu-id="5e21d-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="5e21d-107">Pour nuget.org, la commande de suppression [unlists le package](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="5e21d-107">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5e21d-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="5e21d-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="5e21d-109">où `<packageID>` et `<packageVersion>` identifier le package exact pour supprimer ou retirer de la liste.</span><span class="sxs-lookup"><span data-stu-id="5e21d-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="5e21d-110">Le comportement exact dépend de la source.</span><span class="sxs-lookup"><span data-stu-id="5e21d-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="5e21d-111">Pour des dossiers locaux, par exemple, la suppression du package ; pour nuget.org le package n’est pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="5e21d-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="5e21d-112">Options</span><span class="sxs-lookup"><span data-stu-id="5e21d-112">Options</span></span>

| <span data-ttu-id="5e21d-113">Option</span><span class="sxs-lookup"><span data-stu-id="5e21d-113">Option</span></span> | <span data-ttu-id="5e21d-114">Description</span><span class="sxs-lookup"><span data-stu-id="5e21d-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5e21d-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="5e21d-115">ApiKey</span></span> | <span data-ttu-id="5e21d-116">La clé d’API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="5e21d-116">The API key for the target repository.</span></span> <span data-ttu-id="5e21d-117">Sinon, l’élément spécifié dans le fichier de configuration est utilisé.</span><span class="sxs-lookup"><span data-stu-id="5e21d-117">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="5e21d-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5e21d-118">ConfigFile</span></span> | <span data-ttu-id="5e21d-119">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="5e21d-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5e21d-120">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="5e21d-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5e21d-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5e21d-121">ForceEnglishOutput</span></span> | <span data-ttu-id="5e21d-122">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="5e21d-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5e21d-123">Help</span><span class="sxs-lookup"><span data-stu-id="5e21d-123">Help</span></span> | <span data-ttu-id="5e21d-124">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="5e21d-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="5e21d-125">Non interactif</span><span class="sxs-lookup"><span data-stu-id="5e21d-125">NonInteractive</span></span> | <span data-ttu-id="5e21d-126">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="5e21d-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5e21d-127">Source</span><span class="sxs-lookup"><span data-stu-id="5e21d-127">Source</span></span> | <span data-ttu-id="5e21d-128">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="5e21d-128">Specifies the server URL.</span></span> <span data-ttu-id="5e21d-129">L’URL de nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="5e21d-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="5e21d-130">Pour les flux privés, remplacez le nom d’hôte, par exemple, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="5e21d-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="5e21d-131">Commentaires</span><span class="sxs-lookup"><span data-stu-id="5e21d-131">Verbosity</span></span> | <span data-ttu-id="5e21d-132">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="5e21d-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5e21d-133">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5e21d-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5e21d-134">Exemples</span><span class="sxs-lookup"><span data-stu-id="5e21d-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
