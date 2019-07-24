---
title: Commande de configuration de l’interface CLI NuGet
description: Référence pour la commande de configuration de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433316"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="0cb21-103">commande config (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="0cb21-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="0cb21-104">**S’applique à:** toutes les &bullet; **versions prises en charge**: toutes</span><span class="sxs-lookup"><span data-stu-id="0cb21-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="0cb21-105">Obtient ou définit les valeurs de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="0cb21-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="0cb21-106">Pour une utilisation supplémentaire, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="0cb21-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="0cb21-107">Pour plus d’informations sur les noms de clé autorisés, reportez-vous à la [Référence du fichier de configuration NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="0cb21-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0cb21-108">Usage</span><span class="sxs-lookup"><span data-stu-id="0cb21-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="0cb21-109">où `<name>` et`<value>` spécifient une paire clé-valeur à définir dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="0cb21-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="0cb21-110">Vous pouvez spécifier autant de paires que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="0cb21-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="0cb21-111">Pour supprimer une valeur, spécifiez le nom et `=` le signe, mais aucune valeur.</span><span class="sxs-lookup"><span data-stu-id="0cb21-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="0cb21-112">Pour les noms de clé autorisés, consultez la [Référence du fichier de configuration NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="0cb21-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="0cb21-113">Dans NuGet 3.4 +, `<value>` peut utiliser des [variables d’environnement](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="0cb21-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="0cb21-114">Options</span><span class="sxs-lookup"><span data-stu-id="0cb21-114">Options</span></span>

| <span data-ttu-id="0cb21-115">Option</span><span class="sxs-lookup"><span data-stu-id="0cb21-115">Option</span></span> | <span data-ttu-id="0cb21-116">Description</span><span class="sxs-lookup"><span data-stu-id="0cb21-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0cb21-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="0cb21-117">AsPath</span></span> | <span data-ttu-id="0cb21-118">Retourne la valeur de configuration sous la forme d’un `-Set` chemin d’accès, ignoré lorsque est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0cb21-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="0cb21-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0cb21-119">ConfigFile</span></span> | <span data-ttu-id="0cb21-120">Fichier de configuration NuGet à modifier.</span><span class="sxs-lookup"><span data-stu-id="0cb21-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="0cb21-121">S’il n’est pas spécifié, le fichier par`%AppData%\NuGet\NuGet.Config` défaut est utilisé ( `~/.config/NuGet/NuGet.Config` Windows) ou (Mac/ `~/.nuget/NuGet/NuGet.Config` Linux) ou (varie selon la distribution du système d’exploitation).</span><span class="sxs-lookup"><span data-stu-id="0cb21-121">If not specified, the default file is used -`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.config/NuGet/NuGet.Config`  (Mac/Linux) or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution).</span></span>|
| <span data-ttu-id="0cb21-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0cb21-122">ForceEnglishOutput</span></span> | <span data-ttu-id="0cb21-123">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="0cb21-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0cb21-124">Help</span><span class="sxs-lookup"><span data-stu-id="0cb21-124">Help</span></span> | <span data-ttu-id="0cb21-125">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="0cb21-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="0cb21-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0cb21-126">NonInteractive</span></span> | <span data-ttu-id="0cb21-127">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0cb21-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0cb21-128">Commentaires</span><span class="sxs-lookup"><span data-stu-id="0cb21-128">Verbosity</span></span> | <span data-ttu-id="0cb21-129">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="0cb21-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0cb21-130">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0cb21-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="0cb21-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="0cb21-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```