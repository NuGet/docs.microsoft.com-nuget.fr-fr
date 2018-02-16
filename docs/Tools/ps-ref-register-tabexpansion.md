---
title: "Référence de PowerShell NuGet Register-TabExpansion | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de commande Register-TabExpansion PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Register-TabExpansion"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e363b8a7fa7e25d24331eb3e4eb87141e6a3b97
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="f3df7-104">Register-TabExpansion (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f3df7-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f3df7-105">*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="f3df7-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f3df7-106">Inscrit une tabulation pour les paramètres de la commande spécifiée, telle que lorsque l’onglet est utilisé lorsque vous entrez une commande, les valeurs de développé s’affichent en tant que les options disponibles pour le paramètre en question.</span><span class="sxs-lookup"><span data-stu-id="f3df7-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="f3df7-107">Les expansions précédentes de la commande sont remplacées.</span><span class="sxs-lookup"><span data-stu-id="f3df7-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="f3df7-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f3df7-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f3df7-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f3df7-109">Parameters</span></span>

| <span data-ttu-id="f3df7-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f3df7-110">Parameter</span></span> | <span data-ttu-id="f3df7-111">Description</span><span class="sxs-lookup"><span data-stu-id="f3df7-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f3df7-112">Name</span><span class="sxs-lookup"><span data-stu-id="f3df7-112">Name</span></span> | <span data-ttu-id="f3df7-113">(Obligatoire) La commande pour laquelle inscrire les expansions.</span><span class="sxs-lookup"><span data-stu-id="f3df7-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="f3df7-114">-Nom de commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="f3df7-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="f3df7-115">Définition</span><span class="sxs-lookup"><span data-stu-id="f3df7-115">Definition</span></span> | <span data-ttu-id="f3df7-116">(Obligatoire) Un objet qui décrit l’argument dans la syntaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` où `<parameter>` est le nom de paramètre à modifier et à chaque `<value>` fournit une extension spécifique.</span><span class="sxs-lookup"><span data-stu-id="f3df7-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="f3df7-117">Les guillemets simples et doubles sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="f3df7-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="f3df7-118">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="f3df7-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f3df7-119">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="f3df7-119">Common Parameters</span></span>

<span data-ttu-id="f3df7-120">`Register-TabExpansion` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f3df7-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f3df7-121">Exemples</span><span class="sxs-lookup"><span data-stu-id="f3df7-121">Examples</span></span>

<span data-ttu-id="f3df7-122">Adoptez une solution qui contient trois noms de projets Gestionnaire d’événements, des utilitaires et SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="f3df7-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="f3df7-123">Le développeur utilise fréquemment la `Update-Package` commande à différents moments avec chacun de ces projets.</span><span class="sxs-lookup"><span data-stu-id="f3df7-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="f3df7-124">Elle trouve utile d’avoir le `Update-Package` commande fournissent des extensions de la saisie semi-automatique pour le `-ProjectName` argument afin qu’elle n’a pas besoin de taper un nom de projet chaque fois.</span><span class="sxs-lookup"><span data-stu-id="f3df7-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="f3df7-125">La commande suivante, enregistre ensuite, ces noms de trois projet comme une extension pour le `-ProjectName` paramètre :</span><span class="sxs-lookup"><span data-stu-id="f3df7-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="f3df7-126">Le développeur peut puis tapez `Update-Package -ProjectName `, appuyez sur Tab et consultez les expansions proposées comme options de saisie semi-automatique :</span><span class="sxs-lookup"><span data-stu-id="f3df7-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Exemple d’utilisation de TabExpansion de Registre](media/Register-TabExpansion-Example.png)
