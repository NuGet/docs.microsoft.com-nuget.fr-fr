---
title: NuGet CLI sources commande | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Commande des sources de référence pour le nuget.exe"
keywords: "NuGet sources de référence, des sources de commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c1cd909c0c35d52f0269d267367669df46f9db55
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="594b4-104">commande de sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="594b4-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="594b4-105">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="594b4-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="594b4-106">Gère la liste des sources de `%AppData%\NuGet\NuGet.Config` ou le fichier de configuration spécifié.</span><span class="sxs-lookup"><span data-stu-id="594b4-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="594b4-107">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="594b4-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="594b4-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="594b4-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="594b4-109">où `<operation>` est un des *liste, ajouter, supprimer, activer, désactiver,* ou *mise à jour*, `<name>` est le nom de la source, et `<source>` est l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="594b4-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="594b4-110">Options</span><span class="sxs-lookup"><span data-stu-id="594b4-110">Options</span></span>

| <span data-ttu-id="594b4-111">Option</span><span class="sxs-lookup"><span data-stu-id="594b4-111">Option</span></span> | <span data-ttu-id="594b4-112">Description</span><span class="sxs-lookup"><span data-stu-id="594b4-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="594b4-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="594b4-113">ConfigFile</span></span> | <span data-ttu-id="594b4-114">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="594b4-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="594b4-115">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="594b4-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="594b4-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="594b4-116">ForceEnglishOutput</span></span> | <span data-ttu-id="594b4-117">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="594b4-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="594b4-118">Format</span><span class="sxs-lookup"><span data-stu-id="594b4-118">Format</span></span> | <span data-ttu-id="594b4-119">S’applique à la `list` action et peut être `Detailed` (la valeur par défaut) ou `Short`.</span><span class="sxs-lookup"><span data-stu-id="594b4-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="594b4-120">Help</span><span class="sxs-lookup"><span data-stu-id="594b4-120">Help</span></span> | <span data-ttu-id="594b4-121">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="594b4-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="594b4-122">Non interactif</span><span class="sxs-lookup"><span data-stu-id="594b4-122">NonInteractive</span></span> | <span data-ttu-id="594b4-123">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="594b4-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="594b4-124">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="594b4-124">Password</span></span> | <span data-ttu-id="594b4-125">Spécifie le mot de passe pour s’authentifier auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="594b4-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="594b4-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="594b4-126">StorePasswordInClearText</span></span> | <span data-ttu-id="594b4-127">Indique que le mot de passe en texte non chiffré au lieu du comportement par défaut de stockage sous forme chiffrée.</span><span class="sxs-lookup"><span data-stu-id="594b4-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="594b4-128">UserName</span><span class="sxs-lookup"><span data-stu-id="594b4-128">UserName</span></span> | <span data-ttu-id="594b4-129">Spécifie le nom d’utilisateur pour l’authentification avec la source.</span><span class="sxs-lookup"><span data-stu-id="594b4-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="594b4-130">Commentaires</span><span class="sxs-lookup"><span data-stu-id="594b4-130">Verbosity</span></span> | <span data-ttu-id="594b4-131">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="594b4-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="594b4-132">Assurez-vous d’ajouter un mot de passe des sources dans le même contexte utilisateur comme le nuget.exe sera ensuite utilisé pour accéder à la source du package.</span><span class="sxs-lookup"><span data-stu-id="594b4-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="594b4-133">Le mot de passe est stockée chiffrées dans le fichier de configuration et peut être déchiffrée uniquement dans le même contexte utilisateur car il a été chiffré.</span><span class="sxs-lookup"><span data-stu-id="594b4-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="594b4-134">Par exemple lorsque vous utilisez un serveur de builds pour restaurer les packages NuGet que le mot de passe doit être chiffré avec le même utilisateur Windows sous lequel s’exécute la tâche de serveur de build.</span><span class="sxs-lookup"><span data-stu-id="594b4-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="594b4-135">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="594b4-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="594b4-136">Exemples</span><span class="sxs-lookup"><span data-stu-id="594b4-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
