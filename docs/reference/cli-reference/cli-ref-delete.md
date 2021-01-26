---
title: Commande de suppression de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Delete
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775948"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="ece37-103">Delete, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="ece37-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="ece37-104">**S’applique à : publication de** packages &bullet; **versions prises en charge :** tout</span><span class="sxs-lookup"><span data-stu-id="ece37-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ece37-105">Supprime ou déliste un package d’une source de package.</span><span class="sxs-lookup"><span data-stu-id="ece37-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="ece37-106">Pour nuget.org, la commande delete [déliste le package](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ece37-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ece37-107">Utilisation</span><span class="sxs-lookup"><span data-stu-id="ece37-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="ece37-108">où `<packageID>` et `<packageVersion>` identifient le package exact à supprimer ou à supprimer de la liste.</span><span class="sxs-lookup"><span data-stu-id="ece37-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="ece37-109">Le comportement exact dépend de la source.</span><span class="sxs-lookup"><span data-stu-id="ece37-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="ece37-110">Pour les dossiers locaux, par exemple, le package est supprimé ; pour nuget.org, le package n’est pas répertorié.</span><span class="sxs-lookup"><span data-stu-id="ece37-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="ece37-111">Options</span><span class="sxs-lookup"><span data-stu-id="ece37-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="ece37-112">Clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="ece37-112">The API key for the target repository.</span></span> <span data-ttu-id="ece37-113">S’il n’est pas présent, celui spécifié dans le fichier de configuration est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ece37-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ece37-114">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="ece37-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ece37-115">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ece37-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ece37-116">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="ece37-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ece37-117">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="ece37-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ece37-118">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ece37-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="ece37-119">Ne pas demander lorsque vous supprimez.</span><span class="sxs-lookup"><span data-stu-id="ece37-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="ece37-120">**`-NoServiceEndpoint`** N’ajoute pas « API/v2/packages » à l’URL source.</span><span class="sxs-lookup"><span data-stu-id="ece37-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="ece37-121">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="ece37-121">Specifies the server URL.</span></span> <span data-ttu-id="ece37-122">L’URL de nuget.org est `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="ece37-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="ece37-123">Pour les flux privés, remplacez le nom d’hôte, par exemple, *% hostname%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="ece37-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ece37-124">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="ece37-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="ece37-125">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ece37-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ece37-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="ece37-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
