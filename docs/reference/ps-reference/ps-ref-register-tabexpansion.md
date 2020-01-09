---
title: Registre NuGet-référence PowerShell TabExpansion
description: Référence pour la commande PowerShell Register-TabExpansion dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384452"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="813ab-103">Register-TabExpansion (console du gestionnaire de package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="813ab-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="813ab-104">*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="813ab-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="813ab-105">Inscrit un expansion de tabulation pour les paramètres de la commande spécifiée, de telle sorte que lorsque la touche Tab est utilisée lors de l’entrée dans une commande, les valeurs développées apparaissent en tant qu’options disponibles pour le paramètre en question.</span><span class="sxs-lookup"><span data-stu-id="813ab-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="813ab-106">Toutes les expansions précédentes de la commande sont remplacées.</span><span class="sxs-lookup"><span data-stu-id="813ab-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="813ab-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="813ab-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="813ab-108">Parameters</span><span class="sxs-lookup"><span data-stu-id="813ab-108">Parameters</span></span>

| <span data-ttu-id="813ab-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="813ab-109">Parameter</span></span> | <span data-ttu-id="813ab-110">Description</span><span class="sxs-lookup"><span data-stu-id="813ab-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="813ab-111">Name</span><span class="sxs-lookup"><span data-stu-id="813ab-111">Name</span></span> | <span data-ttu-id="813ab-112">Souhaitée Commande dans laquelle enregistrer les expansions.</span><span class="sxs-lookup"><span data-stu-id="813ab-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="813ab-113">Le commutateur-Name lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="813ab-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="813ab-114">Définition</span><span class="sxs-lookup"><span data-stu-id="813ab-114">Definition</span></span> | <span data-ttu-id="813ab-115">Souhaitée Objet décrivant l’argument dans la syntaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` où `<parameter>` est le nom du paramètre à modifier et chaque `<value>` fournit une expansion spécifique.</span><span class="sxs-lookup"><span data-stu-id="813ab-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="813ab-116">Les guillemets simples et doubles sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="813ab-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="813ab-117">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="813ab-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="813ab-118">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="813ab-118">Common Parameters</span></span>

<span data-ttu-id="813ab-119">`Register-TabExpansion` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="813ab-119">`Register-TabExpansion` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="813ab-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="813ab-120">Examples</span></span>

<span data-ttu-id="813ab-121">Prenons l’exemple d’une solution qui contient trois projets : EventManager, Utilities et SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="813ab-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="813ab-122">Le développeur utilise fréquemment la commande `Update-Package` à différents moments avec chacun de ces projets.</span><span class="sxs-lookup"><span data-stu-id="813ab-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="813ab-123">Elle cherche à ce que la commande `Update-Package` fournissent des expansions de saisie semi-automatique pour l’argument `-ProjectName`, de sorte qu’elle n’a pas besoin de taper un nom de projet à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="813ab-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="813ab-124">La commande suivante inscrit ces trois noms de projet en tant qu’expansion pour le paramètre `-ProjectName` :</span><span class="sxs-lookup"><span data-stu-id="813ab-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="813ab-125">Le développeur peut ensuite taper `Update-Package -ProjectName `, appuyer sur la touche Tab et voir les expansions proposées en tant qu’options de saisie semi-automatique :</span><span class="sxs-lookup"><span data-stu-id="813ab-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Exemple d’utilisation de Register-TabExpansion](media/Register-TabExpansion-Example.png)
