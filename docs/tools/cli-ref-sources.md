---
title: NuGet CLI sources de commande
description: Référence pour nuget.exe sources de commande
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610624"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="1e024-103">sources (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1e024-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="1e024-104">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="1e024-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1e024-105">Gère la liste des sources situées dans le fichier de configuration d’étendue utilisateur ou un fichier de configuration spécifié.</span><span class="sxs-lookup"><span data-stu-id="1e024-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="1e024-106">Le fichier de configuration d’étendue utilisateur se trouve à `%appdata%\NuGet\NuGet.Config` (Windows) et `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1e024-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="1e024-107">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="1e024-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="1e024-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="1e024-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="1e024-109">où `<operation>` est un des *liste, ajouter, supprimer, activer, désactiver,* ou *mise à jour*, `<name>` est le nom de la source, et `<source>` est l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="1e024-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="1e024-110">Vous pouvez utiliser qu’une seule source à la fois.</span><span class="sxs-lookup"><span data-stu-id="1e024-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="1e024-111">Options</span><span class="sxs-lookup"><span data-stu-id="1e024-111">Options</span></span>

| <span data-ttu-id="1e024-112">Option</span><span class="sxs-lookup"><span data-stu-id="1e024-112">Option</span></span> | <span data-ttu-id="1e024-113">Description</span><span class="sxs-lookup"><span data-stu-id="1e024-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e024-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1e024-114">ConfigFile</span></span> | <span data-ttu-id="1e024-115">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="1e024-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1e024-116">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="1e024-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1e024-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1e024-117">ForceEnglishOutput</span></span> | <span data-ttu-id="1e024-118">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="1e024-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1e024-119">Format</span><span class="sxs-lookup"><span data-stu-id="1e024-119">Format</span></span> | <span data-ttu-id="1e024-120">S’applique à la `list` action et peut être `Detailed` (la valeur par défaut) ou `Short`.</span><span class="sxs-lookup"><span data-stu-id="1e024-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="1e024-121">Help</span><span class="sxs-lookup"><span data-stu-id="1e024-121">Help</span></span> | <span data-ttu-id="1e024-122">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="1e024-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="1e024-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1e024-123">NonInteractive</span></span> | <span data-ttu-id="1e024-124">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="1e024-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1e024-125">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="1e024-125">Password</span></span> | <span data-ttu-id="1e024-126">Spécifie le mot de passe pour l’authentification auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="1e024-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="1e024-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="1e024-127">StorePasswordInClearText</span></span> | <span data-ttu-id="1e024-128">Indique que le mot de passe en texte non chiffré au lieu du comportement par défaut de stockage sous une forme chiffrée.</span><span class="sxs-lookup"><span data-stu-id="1e024-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="1e024-129">UserName</span><span class="sxs-lookup"><span data-stu-id="1e024-129">UserName</span></span> | <span data-ttu-id="1e024-130">Spécifie le nom d’utilisateur pour l’authentification auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="1e024-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="1e024-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1e024-131">Verbosity</span></span> | <span data-ttu-id="1e024-132">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="1e024-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="1e024-133">Veillez à ajouter le mot de passe des sources dans le même contexte utilisateur comme nuget.exe est utilisée ultérieurement pour accéder à la source du package.</span><span class="sxs-lookup"><span data-stu-id="1e024-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="1e024-134">Le mot de passe sera stocké chiffré dans le fichier de configuration et peut uniquement être déchiffré dans le même contexte utilisateur, car il a été chiffré.</span><span class="sxs-lookup"><span data-stu-id="1e024-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="1e024-135">Ainsi, par exemple lorsque vous utilisez un serveur de builds pour restaurer les packages NuGet que le mot de passe doit être chiffré avec le même utilisateur Windows sous lequel s’exécute la tâche de serveur de build.</span><span class="sxs-lookup"><span data-stu-id="1e024-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="1e024-136">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1e024-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1e024-137">Exemples</span><span class="sxs-lookup"><span data-stu-id="1e024-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
