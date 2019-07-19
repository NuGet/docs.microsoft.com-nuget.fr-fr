---
title: NuGet Add-BindingRedirect PowerShell Reference
description: Référence pour la commande PowerShell Add-BindingRedirect dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b1e88d32deb3ff34833ef22a9cbb8cad3f0d4354
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327456"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="d1257-103">Add-BindingRedirect (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d1257-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d1257-104">*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="d1257-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d1257-105">Examine tous les assemblys dans le chemin de sortie d’un projet et ajoute des redirections de liaison au fichier de configuration d’application ou Web, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d1257-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="d1257-106">Cette commande est exécutée automatiquement lors de l’installation d’un package.</span><span class="sxs-lookup"><span data-stu-id="d1257-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="d1257-107">Pour plus d’informations sur les redirections de liaison et la raison pour laquelle elles sont utilisées, consultez redirection des [versions d’assemblys](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .net.</span><span class="sxs-lookup"><span data-stu-id="d1257-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="d1257-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d1257-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d1257-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d1257-109">Parameters</span></span>

| <span data-ttu-id="d1257-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d1257-110">Parameter</span></span> | <span data-ttu-id="d1257-111">Description</span><span class="sxs-lookup"><span data-stu-id="d1257-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1257-112">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="d1257-112">ProjectName</span></span> | <span data-ttu-id="d1257-113">Souhaitée Projet auquel ajouter des redirections de liaison.</span><span class="sxs-lookup"><span data-stu-id="d1257-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="d1257-114">Le commutateur-ProjectName lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="d1257-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="d1257-115">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="d1257-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d1257-116">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="d1257-116">Common Parameters</span></span>

<span data-ttu-id="d1257-117">`Add-BindingRedirect`prend en charge les [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216)suivants: Débogage, action d’erreur, ErrorVariable, mise en mémoire tampon, dévariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d1257-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d1257-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="d1257-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```