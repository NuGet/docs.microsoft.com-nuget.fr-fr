---
title: NuGet Add-BindingRedirect PowerShell Reference
description: Référence pour la commande PowerShell Add-BindingRedirect dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384982"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="78e44-103">Add-BindingRedirect (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="78e44-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="78e44-104">*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="78e44-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="78e44-105">Examine tous les assemblys dans le chemin de sortie d’un projet et ajoute des redirections de liaison au fichier de configuration d’application ou Web, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="78e44-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="78e44-106">Cette commande est exécutée automatiquement lors de l’installation d’un package.</span><span class="sxs-lookup"><span data-stu-id="78e44-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="78e44-107">Pour plus d’informations sur les redirections de liaison et la raison pour laquelle elles sont utilisées, consultez [redirection des versions d’assemblys](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .net.</span><span class="sxs-lookup"><span data-stu-id="78e44-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="78e44-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="78e44-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="78e44-109">Parameters</span><span class="sxs-lookup"><span data-stu-id="78e44-109">Parameters</span></span>

| <span data-ttu-id="78e44-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="78e44-110">Parameter</span></span> | <span data-ttu-id="78e44-111">Description</span><span class="sxs-lookup"><span data-stu-id="78e44-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="78e44-112">NomProjet</span><span class="sxs-lookup"><span data-stu-id="78e44-112">ProjectName</span></span> | <span data-ttu-id="78e44-113">Souhaitée Projet auquel ajouter des redirections de liaison.</span><span class="sxs-lookup"><span data-stu-id="78e44-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="78e44-114">Le commutateur-ProjectName lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="78e44-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="78e44-115">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="78e44-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="78e44-116">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="78e44-116">Common Parameters</span></span>

<span data-ttu-id="78e44-117">`Add-BindingRedirect` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="78e44-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="78e44-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="78e44-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```