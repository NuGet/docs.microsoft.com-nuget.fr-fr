---
title: NuGet CLI sources commande | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Commande des sources de référence pour le nuget.exe"
keywords: "NuGet sources de référence, des sources de commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="b6f26-104">commande de sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b6f26-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="b6f26-105">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="b6f26-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b6f26-106">Gère la liste des sources de `%AppData%\NuGet\NuGet.Config` ou le fichier de configuration spécifié.</span><span class="sxs-lookup"><span data-stu-id="b6f26-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="b6f26-107">Notez que l’URL source nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="b6f26-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="b6f26-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="b6f26-108">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="b6f26-109">où `<operation>` est un des *liste, ajouter, supprimer, activer, désactiver,* ou *mise à jour*, `<name>` est le nom de la source, et `<source>` est l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="b6f26-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="b6f26-110">Options</span><span class="sxs-lookup"><span data-stu-id="b6f26-110">Options</span></span>

| <span data-ttu-id="b6f26-111">Option</span><span class="sxs-lookup"><span data-stu-id="b6f26-111">Option</span></span> | <span data-ttu-id="b6f26-112">Description</span><span class="sxs-lookup"><span data-stu-id="b6f26-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b6f26-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b6f26-113">ConfigFile</span></span> | <span data-ttu-id="b6f26-114">*(2.5 +)*  NuGet le fichier de configuration à appliquer.</span><span class="sxs-lookup"><span data-stu-id="b6f26-114">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="b6f26-115">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="b6f26-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="b6f26-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b6f26-116">ForceEnglishOutput</span></span> | <span data-ttu-id="b6f26-117">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="b6f26-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b6f26-118">Format</span><span class="sxs-lookup"><span data-stu-id="b6f26-118">Format</span></span> | <span data-ttu-id="b6f26-119">S’applique à la `list` action et peut être `Detailed` (la valeur par défaut) ou `Short`.</span><span class="sxs-lookup"><span data-stu-id="b6f26-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="b6f26-120">Help</span><span class="sxs-lookup"><span data-stu-id="b6f26-120">Help</span></span> | <span data-ttu-id="b6f26-121">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="b6f26-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="b6f26-122">Non interactif</span><span class="sxs-lookup"><span data-stu-id="b6f26-122">NonInteractive</span></span> | <span data-ttu-id="b6f26-123">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="b6f26-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b6f26-124">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="b6f26-124">Password</span></span> | <span data-ttu-id="b6f26-125">Spécifie le mot de passe pour s’authentifier auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="b6f26-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="b6f26-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="b6f26-126">StorePasswordInClearText</span></span> | <span data-ttu-id="b6f26-127">Indique que le mot de passe en texte non chiffré au lieu du comportement par défaut de stockage sous forme chiffrée.</span><span class="sxs-lookup"><span data-stu-id="b6f26-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="b6f26-128">UserName</span><span class="sxs-lookup"><span data-stu-id="b6f26-128">UserName</span></span> | <span data-ttu-id="b6f26-129">Spécifie le nom d’utilisateur pour l’authentification avec la source.</span><span class="sxs-lookup"><span data-stu-id="b6f26-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="b6f26-130">Commentaires</span><span class="sxs-lookup"><span data-stu-id="b6f26-130">Verbosity</span></span> | <span data-ttu-id="b6f26-131">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="b6f26-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="b6f26-132">Assurez-vous d’ajouter un mot de passe des sources dans le même contexte utilisateur comme le nuget.exe sera ensuite utilisé pour accéder à la source du package.</span><span class="sxs-lookup"><span data-stu-id="b6f26-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="b6f26-133">Le mot de passe est stockée chiffrées dans le fichier de configuration et peut être déchiffrée uniquement dans le même contexte utilisateur car il a été chiffré.</span><span class="sxs-lookup"><span data-stu-id="b6f26-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="b6f26-134">Par exemple lorsque vous utilisez un serveur de builds pour restaurer les packages NuGet que le mot de passe doit être chiffré avec le même utilisateur Windows sous lequel s’exécute la tâche de serveur de build.</span><span class="sxs-lookup"><span data-stu-id="b6f26-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="b6f26-135">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b6f26-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b6f26-136">Exemples</span><span class="sxs-lookup"><span data-stu-id="b6f26-136">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
