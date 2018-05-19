---
title: Commande config de NuGet CLI
description: Informations de référence pour la commande config de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="8e07a-103">commande de configuration (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8e07a-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="8e07a-104">**S’applique à :** tous les &bullet; **versions prises en charge**: tous les</span><span class="sxs-lookup"><span data-stu-id="8e07a-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="8e07a-105">Obtient ou définit les valeurs de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e07a-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="8e07a-106">Pour l’utilisation supplémentaire, consultez [configuration de comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8e07a-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="8e07a-107">Pour plus d’informations sur les noms de clés autorisées, reportez-vous à la [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="8e07a-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8e07a-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="8e07a-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="8e07a-109">où `<name>` et `<value>` spécifier une paire clé-valeur à définir dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="8e07a-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="8e07a-110">Vous pouvez spécifier autant de paires comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="8e07a-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="8e07a-111">Pour supprimer une valeur, spécifiez le nom et le `=` signe mais aucune valeur.</span><span class="sxs-lookup"><span data-stu-id="8e07a-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="8e07a-112">Pour les noms de clé autorisées, consultez la [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="8e07a-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="8e07a-113">Dans NuGet 3.4 + `<value>` peut utiliser [variables d’environnement](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="8e07a-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="8e07a-114">Options</span><span class="sxs-lookup"><span data-stu-id="8e07a-114">Options</span></span>

| <span data-ttu-id="8e07a-115">Option</span><span class="sxs-lookup"><span data-stu-id="8e07a-115">Option</span></span> | <span data-ttu-id="8e07a-116">Description</span><span class="sxs-lookup"><span data-stu-id="8e07a-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e07a-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="8e07a-117">AsPath</span></span> | <span data-ttu-id="8e07a-118">Renvoie la valeur de la configuration comme un chemin d’accès, ignorées lorsque `-Set` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8e07a-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="8e07a-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8e07a-119">ConfigFile</span></span> | <span data-ttu-id="8e07a-120">Le fichier de configuration NuGet à modifier.</span><span class="sxs-lookup"><span data-stu-id="8e07a-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="8e07a-121">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8e07a-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8e07a-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8e07a-122">ForceEnglishOutput</span></span> | <span data-ttu-id="8e07a-123">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="8e07a-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8e07a-124">Help</span><span class="sxs-lookup"><span data-stu-id="8e07a-124">Help</span></span> | <span data-ttu-id="8e07a-125">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="8e07a-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="8e07a-126">Non interactif</span><span class="sxs-lookup"><span data-stu-id="8e07a-126">NonInteractive</span></span> | <span data-ttu-id="8e07a-127">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="8e07a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8e07a-128">Commentaires</span><span class="sxs-lookup"><span data-stu-id="8e07a-128">Verbosity</span></span> | <span data-ttu-id="8e07a-129">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="8e07a-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8e07a-130">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8e07a-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="8e07a-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="8e07a-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```