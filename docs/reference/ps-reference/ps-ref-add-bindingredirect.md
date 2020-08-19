---
title: NuGet Add-BindingRedirect PowerShell Reference
description: Référence pour la commande PowerShell Add-BindingRedirect dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623121"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="a2062-103">Add-BindingRedirect (console du gestionnaire de package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a2062-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a2062-104">*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="a2062-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a2062-105">Examine tous les assemblys dans le chemin de sortie d’un projet et ajoute des redirections de liaison au fichier de configuration d’application ou Web, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a2062-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="a2062-106">Cette commande est exécutée automatiquement lors de l’installation d’un package.</span><span class="sxs-lookup"><span data-stu-id="a2062-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="a2062-107">Cela s’applique uniquement aux scénarios utilisant un fichier packages.config.</span><span class="sxs-lookup"><span data-stu-id="a2062-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="a2062-108">Pour plus d’informations, consultez informations de référence sur les [fichiers NuGet packages.config](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="a2062-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="a2062-109">Pour plus d’informations sur les redirections de liaison et la raison pour laquelle elles sont utilisées, consultez [redirection des versions d’assemblys](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .net.</span><span class="sxs-lookup"><span data-stu-id="a2062-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="a2062-110">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a2062-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a2062-111">Paramètres</span><span class="sxs-lookup"><span data-stu-id="a2062-111">Parameters</span></span>

| <span data-ttu-id="a2062-112">Paramètre</span><span class="sxs-lookup"><span data-stu-id="a2062-112">Parameter</span></span> | <span data-ttu-id="a2062-113">Description</span><span class="sxs-lookup"><span data-stu-id="a2062-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a2062-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="a2062-114">ProjectName</span></span> | <span data-ttu-id="a2062-115">Souhaitée Projet auquel ajouter des redirections de liaison.</span><span class="sxs-lookup"><span data-stu-id="a2062-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="a2062-116">Le commutateur-ProjectName lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="a2062-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="a2062-117">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="a2062-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a2062-118">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="a2062-118">Common Parameters</span></span>

<span data-ttu-id="a2062-119">`Add-BindingRedirect` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a2062-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a2062-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="a2062-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
