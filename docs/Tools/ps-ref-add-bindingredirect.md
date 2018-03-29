---
title: Référence de PowerShell NuGet ajouter-BindingRedirect | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Référence de commande Add-BindingRedirect PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
keywords: NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Add-BindingRedirect
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 2a337bd61295f436b49c56c1680d07ccc6a8c403
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="a54b4-104">Ajouter-BindingRedirect (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a54b4-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a54b4-105">*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="a54b4-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a54b4-106">Examine tous les assemblys du chemin de sortie pour un projet et ajoute des redirections de liaison au fichier de configuration web ou application en cas de besoin.</span><span class="sxs-lookup"><span data-stu-id="a54b4-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="a54b4-107">Cette commande est exécutée automatiquement lors de l’installation d’un package.</span><span class="sxs-lookup"><span data-stu-id="a54b4-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="a54b4-108">Pour plus d’informations sur la liaison des redirections et pourquoi ils sont utilisés, consultez [redirection des Versions d’Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .NET.</span><span class="sxs-lookup"><span data-stu-id="a54b4-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="a54b4-109">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a54b4-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a54b4-110">Paramètres</span><span class="sxs-lookup"><span data-stu-id="a54b4-110">Parameters</span></span>

| <span data-ttu-id="a54b4-111">Paramètre</span><span class="sxs-lookup"><span data-stu-id="a54b4-111">Parameter</span></span> | <span data-ttu-id="a54b4-112">Description</span><span class="sxs-lookup"><span data-stu-id="a54b4-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a54b4-113">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="a54b4-113">ProjectName</span></span> | <span data-ttu-id="a54b4-114">(Obligatoire) Le projet auquel vous souhaitez ajouter des redirections de liaison.</span><span class="sxs-lookup"><span data-stu-id="a54b4-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="a54b4-115">Le commutateur - NomProjet lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="a54b4-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="a54b4-116">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="a54b4-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a54b4-117">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="a54b4-117">Common Parameters</span></span>

<span data-ttu-id="a54b4-118">`Add-BindingRedirect` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a54b4-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a54b4-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="a54b4-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```