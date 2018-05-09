---
title: Commande de suppression de NuGet CLI
description: Informations de référence pour la commande de suppression de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="f46e5-103">supprimer la commande (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f46e5-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="f46e5-104">**S’applique à :** la publication du package &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="f46e5-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f46e5-105">Supprime ou unlists un package à partir d’une source de package.</span><span class="sxs-lookup"><span data-stu-id="f46e5-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="f46e5-106">Pour nuget.org, la commande de suppression [unlists le package](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f46e5-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f46e5-107">Utilisation</span><span class="sxs-lookup"><span data-stu-id="f46e5-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="f46e5-108">où `<packageID>` et `<packageVersion>` identifier le package exact pour supprimer ou retirer de la liste.</span><span class="sxs-lookup"><span data-stu-id="f46e5-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="f46e5-109">Le comportement exact dépend de la source.</span><span class="sxs-lookup"><span data-stu-id="f46e5-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="f46e5-110">Pour des dossiers locaux, par exemple, la suppression du package ; pour nuget.org le package n’est pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="f46e5-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="f46e5-111">Options</span><span class="sxs-lookup"><span data-stu-id="f46e5-111">Options</span></span>

| <span data-ttu-id="f46e5-112">Option</span><span class="sxs-lookup"><span data-stu-id="f46e5-112">Option</span></span> | <span data-ttu-id="f46e5-113">Description</span><span class="sxs-lookup"><span data-stu-id="f46e5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f46e5-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="f46e5-114">ApiKey</span></span> | <span data-ttu-id="f46e5-115">La clé d’API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="f46e5-115">The API key for the target repository.</span></span> <span data-ttu-id="f46e5-116">Sinon, l’élément spécifié dans le fichier de configuration est utilisé.</span><span class="sxs-lookup"><span data-stu-id="f46e5-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="f46e5-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f46e5-117">ConfigFile</span></span> | <span data-ttu-id="f46e5-118">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="f46e5-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f46e5-119">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="f46e5-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f46e5-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f46e5-120">ForceEnglishOutput</span></span> | <span data-ttu-id="f46e5-121">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="f46e5-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f46e5-122">Help</span><span class="sxs-lookup"><span data-stu-id="f46e5-122">Help</span></span> | <span data-ttu-id="f46e5-123">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="f46e5-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="f46e5-124">Non interactif</span><span class="sxs-lookup"><span data-stu-id="f46e5-124">NonInteractive</span></span> | <span data-ttu-id="f46e5-125">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="f46e5-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f46e5-126">Source</span><span class="sxs-lookup"><span data-stu-id="f46e5-126">Source</span></span> | <span data-ttu-id="f46e5-127">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="f46e5-127">Specifies the server URL.</span></span> <span data-ttu-id="f46e5-128">L’URL de nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="f46e5-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="f46e5-129">Pour les flux privés, remplacez le nom d’hôte, par exemple, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="f46e5-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="f46e5-130">Commentaires</span><span class="sxs-lookup"><span data-stu-id="f46e5-130">Verbosity</span></span> | <span data-ttu-id="f46e5-131">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="f46e5-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f46e5-132">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f46e5-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f46e5-133">Exemples</span><span class="sxs-lookup"><span data-stu-id="f46e5-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
