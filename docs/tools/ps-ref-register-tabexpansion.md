---
title: Référence de PowerShell NuGet Register-TabExpansion
description: Référence de commande Register-TabExpansion PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842483"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="69a2f-103">Register-TabExpansion (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="69a2f-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="69a2f-104">*Disponible uniquement dans le [Console du Gestionnaire de Package](package-manager-console.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="69a2f-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="69a2f-105">Inscrit une tabulation pour les paramètres de la commande spécifiée, telle que lors de l’onglet est utilisé lorsque vous entrez une commande, les valeurs de développé s’affichent en tant qu’options disponibles pour le paramètre en question.</span><span class="sxs-lookup"><span data-stu-id="69a2f-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="69a2f-106">Les expansions précédentes de la commande sont remplacées.</span><span class="sxs-lookup"><span data-stu-id="69a2f-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="69a2f-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="69a2f-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="69a2f-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="69a2f-108">Parameters</span></span>

| <span data-ttu-id="69a2f-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="69a2f-109">Parameter</span></span> | <span data-ttu-id="69a2f-110">Description</span><span class="sxs-lookup"><span data-stu-id="69a2f-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69a2f-111">Nom</span><span class="sxs-lookup"><span data-stu-id="69a2f-111">Name</span></span> | <span data-ttu-id="69a2f-112">(Obligatoire) La commande pour laquelle inscrire les expansions.</span><span class="sxs-lookup"><span data-stu-id="69a2f-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="69a2f-113">-Nom du commutateur proprement dit est facultatif.</span><span class="sxs-lookup"><span data-stu-id="69a2f-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="69a2f-114">Définition</span><span class="sxs-lookup"><span data-stu-id="69a2f-114">Definition</span></span> | <span data-ttu-id="69a2f-115">(Obligatoire) Objet décrivant l’argument dans la syntaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` où `<parameter>` est le nom du paramètre à modifier et chacun `<value>` fournit une expansion spécifique.</span><span class="sxs-lookup"><span data-stu-id="69a2f-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="69a2f-116">Les guillemets simples et doubles sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="69a2f-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="69a2f-117">Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.</span><span class="sxs-lookup"><span data-stu-id="69a2f-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="69a2f-118">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="69a2f-118">Common Parameters</span></span>

<span data-ttu-id="69a2f-119">`Register-TabExpansion` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="69a2f-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="69a2f-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="69a2f-120">Examples</span></span>

<span data-ttu-id="69a2f-121">Envisagez une solution qui contient trois noms de projets EventManager, d’utilitaires et SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="69a2f-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="69a2f-122">Le développeur utilise fréquemment la `Update-Package` commande à des moments différents avec chacun de ces projets.</span><span class="sxs-lookup"><span data-stu-id="69a2f-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="69a2f-123">Elle estime qu’il est utile de disposer la `Update-Package` commande fournir des expansions de la saisie semi-automatique pour le `-ProjectName` argument afin qu’elle n’a pas besoin de taper un nom de projet chaque fois.</span><span class="sxs-lookup"><span data-stu-id="69a2f-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="69a2f-124">La commande suivante, inscrit ensuite, ces noms de trois projet comme une extension pour le `-ProjectName` paramètre :</span><span class="sxs-lookup"><span data-stu-id="69a2f-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="69a2f-125">Le développeur peut puis tapez `Update-Package -ProjectName `, appuyez sur Tab et consultez les expansions proposées comme options de la saisie semi-automatique :</span><span class="sxs-lookup"><span data-stu-id="69a2f-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Exemple d’utilisation de Register-TabExpansion](media/Register-TabExpansion-Example.png)
