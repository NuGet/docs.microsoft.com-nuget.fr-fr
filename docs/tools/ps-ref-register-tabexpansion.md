---
title: Référence de PowerShell NuGet Register-TabExpansion
description: Référence de commande Register-TabExpansion PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 02f6d4ecd246b7ce5425cf56ade10789cf03113c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="37b6e-103">Register-TabExpansion (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="37b6e-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="37b6e-104">*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="37b6e-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="37b6e-105">Inscrit une tabulation pour les paramètres de la commande spécifiée, telle que lorsque l’onglet est utilisé lorsque vous entrez une commande, les valeurs de développé s’affichent en tant que les options disponibles pour le paramètre en question.</span><span class="sxs-lookup"><span data-stu-id="37b6e-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="37b6e-106">Les expansions précédentes de la commande sont remplacées.</span><span class="sxs-lookup"><span data-stu-id="37b6e-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="37b6e-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="37b6e-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="37b6e-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="37b6e-108">Parameters</span></span>

| <span data-ttu-id="37b6e-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="37b6e-109">Parameter</span></span> | <span data-ttu-id="37b6e-110">Description</span><span class="sxs-lookup"><span data-stu-id="37b6e-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="37b6e-111">Name</span><span class="sxs-lookup"><span data-stu-id="37b6e-111">Name</span></span> | <span data-ttu-id="37b6e-112">(Obligatoire) La commande pour laquelle inscrire les expansions.</span><span class="sxs-lookup"><span data-stu-id="37b6e-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="37b6e-113">-Nom de commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="37b6e-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="37b6e-114">Définition</span><span class="sxs-lookup"><span data-stu-id="37b6e-114">Definition</span></span> | <span data-ttu-id="37b6e-115">(Obligatoire) Un objet qui décrit l’argument dans la syntaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` où `<parameter>` est le nom de paramètre à modifier et à chaque `<value>` fournit une extension spécifique.</span><span class="sxs-lookup"><span data-stu-id="37b6e-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="37b6e-116">Les guillemets simples et doubles sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="37b6e-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="37b6e-117">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="37b6e-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="37b6e-118">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="37b6e-118">Common Parameters</span></span>

<span data-ttu-id="37b6e-119">`Register-TabExpansion` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="37b6e-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="37b6e-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="37b6e-120">Examples</span></span>

<span data-ttu-id="37b6e-121">Adoptez une solution qui contient trois noms de projets Gestionnaire d’événements, des utilitaires et SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="37b6e-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="37b6e-122">Le développeur utilise fréquemment la `Update-Package` commande à différents moments avec chacun de ces projets.</span><span class="sxs-lookup"><span data-stu-id="37b6e-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="37b6e-123">Elle trouve utile d’avoir le `Update-Package` commande fournissent des extensions de la saisie semi-automatique pour le `-ProjectName` argument afin qu’elle n’a pas besoin de taper un nom de projet chaque fois.</span><span class="sxs-lookup"><span data-stu-id="37b6e-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="37b6e-124">La commande suivante, enregistre ensuite, ces noms de trois projet comme une extension pour le `-ProjectName` paramètre :</span><span class="sxs-lookup"><span data-stu-id="37b6e-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="37b6e-125">Le développeur peut puis tapez `Update-Package -ProjectName `, appuyez sur Tab et consultez les expansions proposées comme options de saisie semi-automatique :</span><span class="sxs-lookup"><span data-stu-id="37b6e-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Exemple d’utilisation de TabExpansion de Registre](media/Register-TabExpansion-Example.png)
