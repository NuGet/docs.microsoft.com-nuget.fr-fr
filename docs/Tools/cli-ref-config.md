---
title: Commande config de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Informations de référence pour la commande config de nuget.exe"
keywords: "référence de configuration NuGet, commande config"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f49751d9747687177e3b6c1890ee9d2919be8d0e
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="2200e-104">commande de configuration (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2200e-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="2200e-105">**S’applique à :** tous les &bullet; **versions prises en charge**: tous les</span><span class="sxs-lookup"><span data-stu-id="2200e-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="2200e-106">Obtient ou définit les valeurs de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="2200e-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="2200e-107">Pour l’utilisation supplémentaire, consultez [configuration de comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="2200e-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="2200e-108">Pour plus d’informations sur les noms de clés autorisées, reportez-vous à la [référence du fichier de configuration NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="2200e-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="2200e-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="2200e-109">Usage</span></span>

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="2200e-110">où `<name>` et `<value>` spécifier une paire clé-valeur à définir dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="2200e-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="2200e-111">Vous pouvez spécifier autant de paires comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="2200e-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="2200e-112">Pour supprimer une valeur, spécifiez le nom et le `=` signe mais aucune valeur.</span><span class="sxs-lookup"><span data-stu-id="2200e-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="2200e-113">Pour les noms de clé autorisées, consultez la [référence du fichier de configuration NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="2200e-113">For allowable key names, see the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

<span data-ttu-id="2200e-114">Dans NuGet 3.4 + `<value>` peut utiliser [variables d’environnement](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="2200e-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="2200e-115">Options</span><span class="sxs-lookup"><span data-stu-id="2200e-115">Options</span></span>

| <span data-ttu-id="2200e-116">Option</span><span class="sxs-lookup"><span data-stu-id="2200e-116">Option</span></span> | <span data-ttu-id="2200e-117">Description</span><span class="sxs-lookup"><span data-stu-id="2200e-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2200e-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="2200e-118">AsPath</span></span> | <span data-ttu-id="2200e-119">Renvoie la valeur de la configuration comme un chemin d’accès, ignorées lorsque `-Set` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2200e-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="2200e-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2200e-120">ConfigFile</span></span> | <span data-ttu-id="2200e-121">*(2.5 +)*  NuGet le fichier de configuration à modifier.</span><span class="sxs-lookup"><span data-stu-id="2200e-121">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="2200e-122">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2200e-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="2200e-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2200e-123">ForceEnglishOutput</span></span> | <span data-ttu-id="2200e-124">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="2200e-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2200e-125">Help</span><span class="sxs-lookup"><span data-stu-id="2200e-125">Help</span></span> | <span data-ttu-id="2200e-126">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="2200e-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="2200e-127">Non interactif</span><span class="sxs-lookup"><span data-stu-id="2200e-127">NonInteractive</span></span> | <span data-ttu-id="2200e-128">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="2200e-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2200e-129">Commentaires</span><span class="sxs-lookup"><span data-stu-id="2200e-129">Verbosity</span></span> | <span data-ttu-id="2200e-130">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="2200e-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="2200e-131">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2200e-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="2200e-132">Exemples</span><span class="sxs-lookup"><span data-stu-id="2200e-132">Examples</span></span>

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
