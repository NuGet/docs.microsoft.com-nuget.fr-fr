---
title: Commande de sources de l’interface CLI NuGet
description: Référence pour la commande de sources NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327596"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="ec6f4-103">sources (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ec6f4-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="ec6f4-104">**S’applique à: consommation de** packages &bullet; , publication des **versions prises en charge:** toutes</span><span class="sxs-lookup"><span data-stu-id="ec6f4-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ec6f4-105">Gère la liste des sources situées dans le fichier de configuration de l’étendue de l’utilisateur ou dans un fichier de configuration spécifié.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="ec6f4-106">Le fichier de configuration de l’étendue de `%appdata%\NuGet\NuGet.Config` l’utilisateur se trouve `~/.nuget/NuGet/NuGet.Config` à l’emplacement (Windows) et (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ec6f4-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="ec6f4-107">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="ec6f4-108">Usage</span><span class="sxs-lookup"><span data-stu-id="ec6f4-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="ec6f4-109">où `<operation>` est l’une des *listes, ajouter, supprimer, activer, désactiver* ou *mettre à jour*, `<name>` est le nom de la source `<source>` et est l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="ec6f4-110">Vous ne pouvez utiliser qu’une seule source à la fois.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="ec6f4-111">Options</span><span class="sxs-lookup"><span data-stu-id="ec6f4-111">Options</span></span>

| <span data-ttu-id="ec6f4-112">Option</span><span class="sxs-lookup"><span data-stu-id="ec6f4-112">Option</span></span> | <span data-ttu-id="ec6f4-113">Description</span><span class="sxs-lookup"><span data-stu-id="ec6f4-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec6f4-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ec6f4-114">ConfigFile</span></span> | <span data-ttu-id="ec6f4-115">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ec6f4-116">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ec6f4-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ec6f4-117">ForceEnglishOutput</span></span> | <span data-ttu-id="ec6f4-118">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ec6f4-119">Format</span><span class="sxs-lookup"><span data-stu-id="ec6f4-119">Format</span></span> | <span data-ttu-id="ec6f4-120">S’applique à `list` l’action et peut `Detailed` avoir la valeur (valeur `Short`par défaut) ou.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="ec6f4-121">Aide</span><span class="sxs-lookup"><span data-stu-id="ec6f4-121">Help</span></span> | <span data-ttu-id="ec6f4-122">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="ec6f4-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ec6f4-123">NonInteractive</span></span> | <span data-ttu-id="ec6f4-124">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ec6f4-125">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="ec6f4-125">Password</span></span> | <span data-ttu-id="ec6f4-126">Spécifie le mot de passe pour l’authentification auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="ec6f4-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="ec6f4-127">StorePasswordInClearText</span></span> | <span data-ttu-id="ec6f4-128">Indique de stocker le mot de passe dans du texte non chiffré au lieu du comportement par défaut du stockage d’un formulaire chiffré.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="ec6f4-129">UserName</span><span class="sxs-lookup"><span data-stu-id="ec6f4-129">UserName</span></span> | <span data-ttu-id="ec6f4-130">Spécifie le nom d’utilisateur pour l’authentification auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="ec6f4-131">Commentaires</span><span class="sxs-lookup"><span data-stu-id="ec6f4-131">Verbosity</span></span> | <span data-ttu-id="ec6f4-132">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="ec6f4-133">Veillez à ajouter le mot de passe de la source dans le même contexte utilisateur, car NuGet. exe sera utilisé ultérieurement pour accéder à la source du package.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="ec6f4-134">Le mot de passe est stocké de manière chiffrée dans le fichier de configuration et ne peut être déchiffré que dans le même contexte utilisateur que celui dans lequel il a été chiffré.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="ec6f4-135">Par exemple, lorsque vous utilisez un serveur de builds pour restaurer des packages NuGet, le mot de passe doit être chiffré avec le même utilisateur Windows sous lequel la tâche de serveur de builds s’exécutera.</span><span class="sxs-lookup"><span data-stu-id="ec6f4-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="ec6f4-136">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ec6f4-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ec6f4-137">Exemples</span><span class="sxs-lookup"><span data-stu-id="ec6f4-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
