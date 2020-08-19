---
title: Commande de configuration de l’interface CLI NuGet
description: Référence pour la commande nuget.exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622874"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="30b06-103">commande config (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="30b06-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="30b06-104">**S’applique à :** toutes les &bullet; **versions prises en charge**: toutes</span><span class="sxs-lookup"><span data-stu-id="30b06-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="30b06-105">Obtient ou définit les valeurs de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="30b06-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="30b06-106">Pour une utilisation supplémentaire, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="30b06-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="30b06-107">Pour plus d’informations sur les noms de clé autorisés, reportez-vous à la [Référence du fichier de configuration NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="30b06-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="30b06-108">Usage</span><span class="sxs-lookup"><span data-stu-id="30b06-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="30b06-109">où `<name>` et `<value>` spécifient une paire clé-valeur à définir dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="30b06-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="30b06-110">Vous pouvez spécifier autant de paires que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="30b06-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="30b06-111">Pour supprimer une valeur, spécifiez le nom et le `=` signe, mais aucune valeur.</span><span class="sxs-lookup"><span data-stu-id="30b06-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="30b06-112">Pour les noms de clé autorisés, consultez la [Référence du fichier de configuration NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="30b06-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="30b06-113">Dans NuGet 3.4 +, `<value>` peut utiliser des [variables d’environnement](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="30b06-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="30b06-114">Options</span><span class="sxs-lookup"><span data-stu-id="30b06-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="30b06-115">Retourne la valeur de configuration sous la forme d’un chemin d’accès, ignoré lorsque `-Set` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="30b06-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="30b06-116">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="30b06-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="30b06-117">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="30b06-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="30b06-118">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="30b06-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="30b06-119">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="30b06-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="30b06-120">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="30b06-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="30b06-121">Une sur plus de paires clé-valeur à définir dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="30b06-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="30b06-122">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="30b06-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="30b06-123">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="30b06-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="30b06-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="30b06-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
