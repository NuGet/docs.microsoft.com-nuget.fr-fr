---
title: Prise en charge de NuGet pour le système de projets Visual Studio
description: Intégration de NuGet dans le système de projets Visual Studio pour les types de projets tiers.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 7af330f88b47352666933598719d9c8f8cb66a78
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779412"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="d8a79-103">Prise en charge de NuGet pour le système de projets Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8a79-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="d8a79-104">Pour prendre en charge des types de projets tiers dans Visual Studio, NuGet 3.x+ prend en charge le [Système de projets commun (CPS, Common Project System)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), tandis que NuGet 3.2+ prend aussi en charge les systèmes de projets non-CPS.</span><span class="sxs-lookup"><span data-stu-id="d8a79-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="d8a79-105">Pour s’intégrer à NuGet, un système de projets doit publier sa propre prise en charge de toutes les fonctionnalités des projets décrites dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="d8a79-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="d8a79-106">Ne déclarez pas des fonctionnalités que votre projet ne possède pas en réalité, de façon à permettre l’installation correcte des packages dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="d8a79-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="d8a79-107">De nombreuses fonctionnalités de Visual Studio et d’autres extensions dépendent des fonctionnalités du projet, en plus du client NuGet.</span><span class="sxs-lookup"><span data-stu-id="d8a79-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="d8a79-108">Publier des fonctionnalités dont votre projet ne dispose pas en réalité peut provoquer le dysfonctionnement de ces composants et une dégradation de l’expérience de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d8a79-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="d8a79-109">Publier les fonctionnalités d’un projet</span><span class="sxs-lookup"><span data-stu-id="d8a79-109">Advertise project capabilities</span></span>

<span data-ttu-id="d8a79-110">Le client NuGet détermine les packages qui sont compatibles avec votre type de projet en fonction des [fonctionnalités du projet](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), comme décrit dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="d8a79-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="d8a79-111">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="d8a79-111">Capability</span></span> | <span data-ttu-id="d8a79-112">Description</span><span class="sxs-lookup"><span data-stu-id="d8a79-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d8a79-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="d8a79-113">AssemblyReferences</span></span> | <span data-ttu-id="d8a79-114">Indique que le projet prend en charge les références d’assembly (à distinguer de WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="d8a79-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="d8a79-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="d8a79-115">DeclaredSourceItems</span></span> | <span data-ttu-id="d8a79-116">Indique que le projet est un projet MSBuild classique (non DNX) dans la mesure où il déclare des éléments sources dans le projet lui-même.</span><span class="sxs-lookup"><span data-stu-id="d8a79-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="d8a79-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="d8a79-117">UserSourceItems</span></span>|<span data-ttu-id="d8a79-118">Indique que l’utilisateur est autorisé à ajouter des fichiers arbitraires à son projet.</span><span class="sxs-lookup"><span data-stu-id="d8a79-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="d8a79-119">Pour les systèmes de projets basés sur CPS, les détails d’implémentation des fonctionnalités des projets décrites dans le reste de cette section ont été écrits pour vous.</span><span class="sxs-lookup"><span data-stu-id="d8a79-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="d8a79-120">Consultez [Déclaration des fonctionnalités de projet dans les projets CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="d8a79-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="d8a79-121">Implémentation de VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="d8a79-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="d8a79-122">La classe `VsProjectCapabilitiesPresenceChecker` doit implémenter l’interface `IVsBooleanSymbolPresenceChecker`, qui est définie comme suit :</span><span class="sxs-lookup"><span data-stu-id="d8a79-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

<span data-ttu-id="d8a79-123">Voici un exemple d’implémentation de cette interface :</span><span class="sxs-lookup"><span data-stu-id="d8a79-123">A sample implementation of this interface would then be:</span></span>

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="d8a79-124">N’oubliez pas d’ajouter/supprimer des fonctionnalités dans l’ensemble `ActualProjectCapabilities`, en fonction de ce que votre système de projets prend réellement en charge.</span><span class="sxs-lookup"><span data-stu-id="d8a79-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="d8a79-125">Pour obtenir des descriptions complètes, consultez la [documentation sur les fonctionnalités des projets](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="d8a79-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="d8a79-126">Réponse à des requêtes</span><span class="sxs-lookup"><span data-stu-id="d8a79-126">Responding to queries</span></span>

<span data-ttu-id="d8a79-127">Un projet déclare cette fonctionnalité en prenant en charge la propriété `VSHPROPID_ProjectCapabilitiesChecker` via `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="d8a79-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="d8a79-128">Elle doit retourner une instance de `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, qui est défini dans l’assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`.</span><span class="sxs-lookup"><span data-stu-id="d8a79-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="d8a79-129">Référencez cet assembly en installant [son package NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="d8a79-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="d8a79-130">Par exemple, vous pouvez ajouter l’instruction `case` suivante à l’instruction `switch` de votre méthode `IVsHierarchy::GetProperty` :</span><span class="sxs-lookup"><span data-stu-id="d8a79-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="d8a79-131">Prise en charge de DTE</span><span class="sxs-lookup"><span data-stu-id="d8a79-131">DTE Support</span></span>

<span data-ttu-id="d8a79-132">NuGet pilote le système de projets pour ajouter des références, des éléments de contenu et des importations MSBuild en appelant [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), qui est l’interface d’automatisation du plus haut niveau de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8a79-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="d8a79-133">DTE est un ensemble d’interfaces COM que vous pouvez déjà implémenter.</span><span class="sxs-lookup"><span data-stu-id="d8a79-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="d8a79-134">Si votre type de projet est basé sur CPS, DTE est implémenté pour vous.</span><span class="sxs-lookup"><span data-stu-id="d8a79-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
