---
title: Commande config de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informations de référence pour la commande config de nuget.exe"
keywords: "référence de configuration NuGet, commande config"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7cf7c06000904a617752567ed7612c0c48042db9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="2082b-104">commande de configuration (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2082b-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="2082b-105">**S’applique à :** tous les &bullet; **versions prises en charge**: tous les</span><span class="sxs-lookup"><span data-stu-id="2082b-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="2082b-106">Obtient ou définit les valeurs de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="2082b-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="2082b-107">Pour l’utilisation supplémentaire, consultez [configuration de comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="2082b-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="2082b-108">Pour plus d’informations sur les noms de clés autorisées, reportez-vous à la [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="2082b-108">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="2082b-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="2082b-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="2082b-110">où `<name>` et `<value>` spécifier une paire clé-valeur à définir dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="2082b-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="2082b-111">Vous pouvez spécifier autant de paires comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="2082b-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="2082b-112">Pour supprimer une valeur, spécifiez le nom et le `=` signe mais aucune valeur.</span><span class="sxs-lookup"><span data-stu-id="2082b-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="2082b-113">Pour les noms de clé autorisées, consultez la [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="2082b-113">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="2082b-114">Dans NuGet 3.4 + `<value>` peut utiliser [variables d’environnement](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="2082b-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="2082b-115">Options</span><span class="sxs-lookup"><span data-stu-id="2082b-115">Options</span></span>

| <span data-ttu-id="2082b-116">Option</span><span class="sxs-lookup"><span data-stu-id="2082b-116">Option</span></span> | <span data-ttu-id="2082b-117">Description</span><span class="sxs-lookup"><span data-stu-id="2082b-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2082b-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="2082b-118">AsPath</span></span> | <span data-ttu-id="2082b-119">Renvoie la valeur de la configuration comme un chemin d’accès, ignorées lorsque `-Set` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2082b-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="2082b-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2082b-120">ConfigFile</span></span> | <span data-ttu-id="2082b-121">Le fichier de configuration NuGet à modifier.</span><span class="sxs-lookup"><span data-stu-id="2082b-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="2082b-122">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2082b-122">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2082b-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2082b-123">ForceEnglishOutput</span></span> | <span data-ttu-id="2082b-124">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="2082b-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2082b-125">Help</span><span class="sxs-lookup"><span data-stu-id="2082b-125">Help</span></span> | <span data-ttu-id="2082b-126">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="2082b-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="2082b-127">Non interactif</span><span class="sxs-lookup"><span data-stu-id="2082b-127">NonInteractive</span></span> | <span data-ttu-id="2082b-128">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="2082b-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2082b-129">Commentaires</span><span class="sxs-lookup"><span data-stu-id="2082b-129">Verbosity</span></span> | <span data-ttu-id="2082b-130">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="2082b-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2082b-131">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2082b-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="2082b-132">Exemples</span><span class="sxs-lookup"><span data-stu-id="2082b-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
