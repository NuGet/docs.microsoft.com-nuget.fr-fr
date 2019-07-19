---
title: Commande de suppression de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe Delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327836"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="acb97-103">Delete, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="acb97-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="acb97-104">**S’applique à:** publication &bullet; de packages **versions prises en charge:** tout</span><span class="sxs-lookup"><span data-stu-id="acb97-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="acb97-105">Supprime ou déliste un package d’une source de package.</span><span class="sxs-lookup"><span data-stu-id="acb97-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="acb97-106">Pour nuget.org, la commande delete [déliste le package](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="acb97-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="acb97-107">Usage</span><span class="sxs-lookup"><span data-stu-id="acb97-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="acb97-108">où `<packageID>` et`<packageVersion>` identifient le package exact à supprimer ou à supprimer de la liste.</span><span class="sxs-lookup"><span data-stu-id="acb97-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="acb97-109">Le comportement exact dépend de la source.</span><span class="sxs-lookup"><span data-stu-id="acb97-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="acb97-110">Pour les dossiers locaux, par exemple, le package est supprimé; pour nuget.org, le package n’est pas répertorié.</span><span class="sxs-lookup"><span data-stu-id="acb97-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="acb97-111">Options</span><span class="sxs-lookup"><span data-stu-id="acb97-111">Options</span></span>

| <span data-ttu-id="acb97-112">Option</span><span class="sxs-lookup"><span data-stu-id="acb97-112">Option</span></span> | <span data-ttu-id="acb97-113">Description</span><span class="sxs-lookup"><span data-stu-id="acb97-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="acb97-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="acb97-114">ApiKey</span></span> | <span data-ttu-id="acb97-115">Clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="acb97-115">The API key for the target repository.</span></span> <span data-ttu-id="acb97-116">S’il n’est pas présent, celui spécifié dans le fichier de configuration est utilisé.</span><span class="sxs-lookup"><span data-stu-id="acb97-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="acb97-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="acb97-117">ConfigFile</span></span> | <span data-ttu-id="acb97-118">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="acb97-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="acb97-119">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="acb97-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="acb97-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="acb97-120">ForceEnglishOutput</span></span> | <span data-ttu-id="acb97-121">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="acb97-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="acb97-122">Help</span><span class="sxs-lookup"><span data-stu-id="acb97-122">Help</span></span> | <span data-ttu-id="acb97-123">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="acb97-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="acb97-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="acb97-124">NonInteractive</span></span> | <span data-ttu-id="acb97-125">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="acb97-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="acb97-126">source</span><span class="sxs-lookup"><span data-stu-id="acb97-126">Source</span></span> | <span data-ttu-id="acb97-127">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="acb97-127">Specifies the server URL.</span></span> <span data-ttu-id="acb97-128">L’URL de nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="acb97-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="acb97-129">Pour les flux privés, remplacez le nom d’hôte, par exemple, *% hostname%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="acb97-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="acb97-130">Commentaires</span><span class="sxs-lookup"><span data-stu-id="acb97-130">Verbosity</span></span> | <span data-ttu-id="acb97-131">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="acb97-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="acb97-132">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="acb97-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="acb97-133">Exemples</span><span class="sxs-lookup"><span data-stu-id="acb97-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
