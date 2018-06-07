---
title: Référence de PowerShell NuGet ajouter-BindingRedirect.
description: Référence de commande Add-BindingRedirect PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817621"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="9f13c-103">Add-BindingRedirect (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9f13c-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9f13c-104">*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="9f13c-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="9f13c-105">Examine tous les assemblys du chemin de sortie pour un projet et ajoute des redirections de liaison au fichier de configuration web ou application en cas de besoin.</span><span class="sxs-lookup"><span data-stu-id="9f13c-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="9f13c-106">Cette commande est exécutée automatiquement lors de l’installation d’un package.</span><span class="sxs-lookup"><span data-stu-id="9f13c-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="9f13c-107">Pour plus d’informations sur la liaison des redirections et pourquoi ils sont utilisés, consultez [redirection des Versions d’Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .NET.</span><span class="sxs-lookup"><span data-stu-id="9f13c-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="9f13c-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9f13c-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="9f13c-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9f13c-109">Parameters</span></span>

| <span data-ttu-id="9f13c-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="9f13c-110">Parameter</span></span> | <span data-ttu-id="9f13c-111">Description</span><span class="sxs-lookup"><span data-stu-id="9f13c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9f13c-112">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="9f13c-112">ProjectName</span></span> | <span data-ttu-id="9f13c-113">(Obligatoire) Le projet auquel vous souhaitez ajouter des redirections de liaison.</span><span class="sxs-lookup"><span data-stu-id="9f13c-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="9f13c-114">Le commutateur - NomProjet lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="9f13c-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="9f13c-115">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="9f13c-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9f13c-116">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="9f13c-116">Common Parameters</span></span>

<span data-ttu-id="9f13c-117">`Add-BindingRedirect` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9f13c-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9f13c-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="9f13c-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```