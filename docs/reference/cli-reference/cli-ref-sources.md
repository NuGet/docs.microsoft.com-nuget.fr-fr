---
title: Commande de sources de l’interface CLI NuGet
description: Référence pour la commande nuget.exe sources
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780010"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="e4438-103">commande sources (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="e4438-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="e4438-104">**S’applique à : consommation de** packages, publication &bullet; des **versions prises en charge :** toutes</span><span class="sxs-lookup"><span data-stu-id="e4438-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e4438-105">Gère la liste des sources situées dans le fichier de configuration de l’étendue de l’utilisateur ou dans un fichier de configuration spécifié.</span><span class="sxs-lookup"><span data-stu-id="e4438-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="e4438-106">Le fichier de configuration de l’étendue de l’utilisateur se trouve à l’emplacement `%appdata%\NuGet\NuGet.Config` (Windows) et `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="e4438-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="e4438-107">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="e4438-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="e4438-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="e4438-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="e4438-109">où `<operation>` est l’une des *listes, ajouter, supprimer, activer, désactiver* ou *mettre à jour*, `<name>` est le nom de la source et `<source>` est l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="e4438-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="e4438-110">Vous ne pouvez utiliser qu’une seule source à la fois.</span><span class="sxs-lookup"><span data-stu-id="e4438-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="e4438-111">Options</span><span class="sxs-lookup"><span data-stu-id="e4438-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="e4438-112">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="e4438-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e4438-113">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="e4438-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="e4438-114">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="e4438-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="e4438-115">S’applique à l' `list` action et peut avoir `Detailed` la valeur (valeur par défaut) ou `Short` .</span><span class="sxs-lookup"><span data-stu-id="e4438-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="e4438-116">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="e4438-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="e4438-117">Nom de la source.</span><span class="sxs-lookup"><span data-stu-id="e4438-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="e4438-118">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e4438-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="e4438-119">Spécifie le mot de passe pour l’authentification auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="e4438-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="e4438-120">Chemin d’accès à la source du ou des packages.</span><span class="sxs-lookup"><span data-stu-id="e4438-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="e4438-121">Indique de stocker le mot de passe dans du texte non chiffré au lieu du comportement par défaut du stockage d’un formulaire chiffré.</span><span class="sxs-lookup"><span data-stu-id="e4438-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="e4438-122">Spécifie le nom d’utilisateur pour l’authentification auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="e4438-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="e4438-123">Liste séparée par des virgules des types d’authentification valides pour cette source.</span><span class="sxs-lookup"><span data-stu-id="e4438-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="e4438-124">Par défaut, tous les types d’authentification sont valides.</span><span class="sxs-lookup"><span data-stu-id="e4438-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="e4438-125">Exemple : `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="e4438-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="e4438-126">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="e4438-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="e4438-127">Veillez à ajouter le mot de passe des sources dans le même contexte utilisateur, car le nuget.exe est utilisé ultérieurement pour accéder à la source du package.</span><span class="sxs-lookup"><span data-stu-id="e4438-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="e4438-128">Le mot de passe est stocké de manière chiffrée dans le fichier de configuration et ne peut être déchiffré que dans le même contexte utilisateur que celui dans lequel il a été chiffré.</span><span class="sxs-lookup"><span data-stu-id="e4438-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="e4438-129">Par exemple, lorsque vous utilisez un serveur de builds pour restaurer des packages NuGet, le mot de passe doit être chiffré avec le même utilisateur Windows sous lequel la tâche de serveur de builds s’exécutera.</span><span class="sxs-lookup"><span data-stu-id="e4438-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="e4438-130">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e4438-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e4438-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="e4438-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
