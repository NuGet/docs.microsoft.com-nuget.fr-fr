---
title: Référence de PowerShell NuGet ajouter-BindingRedirect
description: Référence de commande Add-BindingRedirect PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551655"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="f48f7-103">Add-BindingRedirect (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f48f7-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f48f7-104">*Disponible uniquement dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="f48f7-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f48f7-105">Examine tous les assemblys dans le chemin de sortie pour un projet et ajoute des redirections de liaison au fichier de configuration web ou application lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f48f7-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="f48f7-106">Cette commande est exécutée automatiquement quand vous installez un package.</span><span class="sxs-lookup"><span data-stu-id="f48f7-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="f48f7-107">Pour plus d’informations sur la liaison des redirections et pourquoi ils sont utilisés, consultez [redirection des Versions d’Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .NET.</span><span class="sxs-lookup"><span data-stu-id="f48f7-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="f48f7-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f48f7-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f48f7-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f48f7-109">Parameters</span></span>

| <span data-ttu-id="f48f7-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f48f7-110">Parameter</span></span> | <span data-ttu-id="f48f7-111">Description</span><span class="sxs-lookup"><span data-stu-id="f48f7-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f48f7-112">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="f48f7-112">ProjectName</span></span> | <span data-ttu-id="f48f7-113">(Obligatoire) Le projet auquel ajouter des redirections de liaison.</span><span class="sxs-lookup"><span data-stu-id="f48f7-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="f48f7-114">Le commutateur - NomProjet proprement dit est facultatif.</span><span class="sxs-lookup"><span data-stu-id="f48f7-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="f48f7-115">Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.</span><span class="sxs-lookup"><span data-stu-id="f48f7-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f48f7-116">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="f48f7-116">Common Parameters</span></span>

<span data-ttu-id="f48f7-117">`Add-BindingRedirect` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f48f7-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f48f7-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="f48f7-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```