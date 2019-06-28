---
title: Commande de config NuGet CLI
description: Référence pour la commande config de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426077"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="80e84-103">commande config (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="80e84-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="80e84-104">**S’applique à :** tous les &bullet; **versions prises en charge**: tous les</span><span class="sxs-lookup"><span data-stu-id="80e84-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="80e84-105">Obtient ou définit les valeurs de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="80e84-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="80e84-106">Pour une utilisation supplémentaire, consultez [les configurations courantes NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="80e84-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="80e84-107">Pour plus d’informations sur les noms de clés autorisées, reportez-vous à la [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="80e84-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="80e84-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="80e84-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="80e84-109">où `<name>` et `<value>` spécifier une paire clé-valeur à définir dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="80e84-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="80e84-110">Vous pouvez spécifier autant de paires comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="80e84-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="80e84-111">Pour supprimer une valeur, spécifiez le nom et le `=` connexion, mais aucune valeur.</span><span class="sxs-lookup"><span data-stu-id="80e84-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="80e84-112">Pour les noms de clés autorisées, consultez le [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="80e84-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="80e84-113">Dans NuGet 3.4 + `<value>` peut utiliser [variables d’environnement](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="80e84-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="80e84-114">Options</span><span class="sxs-lookup"><span data-stu-id="80e84-114">Options</span></span>

| <span data-ttu-id="80e84-115">Option</span><span class="sxs-lookup"><span data-stu-id="80e84-115">Option</span></span> | <span data-ttu-id="80e84-116">Description</span><span class="sxs-lookup"><span data-stu-id="80e84-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80e84-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="80e84-117">AsPath</span></span> | <span data-ttu-id="80e84-118">Renvoie la valeur de la configuration comme un chemin d’accès, ignorées lorsque `-Set` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="80e84-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="80e84-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="80e84-119">ConfigFile</span></span> | <span data-ttu-id="80e84-120">Le fichier de configuration de NuGet à modifier.</span><span class="sxs-lookup"><span data-stu-id="80e84-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="80e84-121">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="80e84-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="80e84-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="80e84-122">ForceEnglishOutput</span></span> | <span data-ttu-id="80e84-123">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="80e84-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="80e84-124">Help</span><span class="sxs-lookup"><span data-stu-id="80e84-124">Help</span></span> | <span data-ttu-id="80e84-125">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="80e84-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="80e84-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="80e84-126">NonInteractive</span></span> | <span data-ttu-id="80e84-127">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="80e84-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="80e84-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="80e84-128">Verbosity</span></span> | <span data-ttu-id="80e84-129">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="80e84-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="80e84-130">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="80e84-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="80e84-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="80e84-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
