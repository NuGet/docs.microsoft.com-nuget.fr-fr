---
title: Référence de PowerShell NuGet ajouter-BindingRedirect.
description: Référence de commande Add-BindingRedirect PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="27281-103">Ajouter-BindingRedirect (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="27281-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="27281-104">*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="27281-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="27281-105">Examine tous les assemblys du chemin de sortie pour un projet et ajoute des redirections de liaison au fichier de configuration web ou application en cas de besoin.</span><span class="sxs-lookup"><span data-stu-id="27281-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="27281-106">Cette commande est exécutée automatiquement lors de l’installation d’un package.</span><span class="sxs-lookup"><span data-stu-id="27281-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="27281-107">Pour plus d’informations sur la liaison des redirections et pourquoi ils sont utilisés, consultez [redirection des Versions d’Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .NET.</span><span class="sxs-lookup"><span data-stu-id="27281-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="27281-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="27281-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="27281-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="27281-109">Parameters</span></span>

| <span data-ttu-id="27281-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="27281-110">Parameter</span></span> | <span data-ttu-id="27281-111">Description</span><span class="sxs-lookup"><span data-stu-id="27281-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27281-112">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="27281-112">ProjectName</span></span> | <span data-ttu-id="27281-113">(Obligatoire) Le projet auquel vous souhaitez ajouter des redirections de liaison.</span><span class="sxs-lookup"><span data-stu-id="27281-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="27281-114">Le commutateur - NomProjet lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="27281-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="27281-115">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="27281-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="27281-116">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="27281-116">Common Parameters</span></span>

<span data-ttu-id="27281-117">`Add-BindingRedirect` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="27281-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="27281-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="27281-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```