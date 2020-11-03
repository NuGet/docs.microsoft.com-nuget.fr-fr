---
title: Informations de référence sur PowerShell Add-BindingRedirect de NuGet
description: Référence pour Add-BindingRedirect commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 382ba9b179428c70e3eb16db86a363e095207d61
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237255"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="61ce4-103">Add-BindingRedirect (console du gestionnaire de package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="61ce4-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="61ce4-104">*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="61ce4-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="61ce4-105">Examine tous les assemblys dans le chemin de sortie d’un projet et ajoute des redirections de liaison au fichier de configuration d’application ou Web, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="61ce4-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="61ce4-106">Cette commande est exécutée automatiquement lors de l’installation d’un package.</span><span class="sxs-lookup"><span data-stu-id="61ce4-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="61ce4-107">Cela s’applique uniquement aux scénarios utilisant un fichier packages.config.</span><span class="sxs-lookup"><span data-stu-id="61ce4-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="61ce4-108">Pour plus d’informations, consultez informations de référence sur les [fichiers NuGet packages.config](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="61ce4-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="61ce4-109">Pour plus d’informations sur les redirections de liaison et la raison pour laquelle elles sont utilisées, consultez [redirection des versions d’assemblys](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .net.</span><span class="sxs-lookup"><span data-stu-id="61ce4-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="61ce4-110">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="61ce4-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="61ce4-111">Paramètres</span><span class="sxs-lookup"><span data-stu-id="61ce4-111">Parameters</span></span>

| <span data-ttu-id="61ce4-112">Paramètre</span><span class="sxs-lookup"><span data-stu-id="61ce4-112">Parameter</span></span> | <span data-ttu-id="61ce4-113">Description</span><span class="sxs-lookup"><span data-stu-id="61ce4-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61ce4-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="61ce4-114">ProjectName</span></span> | <span data-ttu-id="61ce4-115">Souhaitée Projet auquel ajouter des redirections de liaison.</span><span class="sxs-lookup"><span data-stu-id="61ce4-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="61ce4-116">Le commutateur-ProjectName lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ce4-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="61ce4-117">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="61ce4-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="61ce4-118">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="61ce4-118">Common Parameters</span></span>

<span data-ttu-id="61ce4-119">`Add-BindingRedirect` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="61ce4-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="61ce4-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="61ce4-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```