---
title: "Prise en charge de NuGet pour le système de projets Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 9d7fa7f6-82ed-4df6-9734-f43a3d8e3b98
description: "Intégration de NuGet dans le système de projets Visual Studio pour les types de projets tiers."
keywords: "NuGet dans Visual Studio, types de projets personnalisés, projets Visual Studio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c8cad46f18578bec41bd9280985e42972a9b3c1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="f4401-104">Prise en charge de NuGet pour le système de projets Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4401-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="f4401-105">Pour prendre en charge des types de projets tiers dans Visual Studio, NuGet 3.x+ prend en charge le [Système de projets commun (CPS, Common Project System)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), tandis que NuGet 3.2+ prend aussi en charge les systèmes de projets non-CPS.</span><span class="sxs-lookup"><span data-stu-id="f4401-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="f4401-106">Pour s’intégrer à NuGet, un système de projets doit publier sa propre prise en charge de toutes les fonctionnalités des projets décrites dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="f4401-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>


> [!NOTE]
> <span data-ttu-id="f4401-107">Ne déclarez pas des fonctionnalités que votre projet n’a pas en réalité, de façon à permettre l’installation correcte des packages dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="f4401-107">Do not declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="f4401-108">De nombreuses fonctionnalités de Visual Studio et d’autres extensions dépendent des fonctionnalités du projet, en plus du client NuGet.</span><span class="sxs-lookup"><span data-stu-id="f4401-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="f4401-109">Publier des fonctionnalités dont votre projet ne dispose pas en réalité peut provoquer le dysfonctionnement de ces composants et une dégradation de l’expérience de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f4401-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="f4401-110">Publier les fonctionnalités d’un projet</span><span class="sxs-lookup"><span data-stu-id="f4401-110">Advertise project capabilities</span></span>

<span data-ttu-id="f4401-111">Le client NuGet détermine les packages qui sont compatibles avec votre type de projet en fonction des [fonctionnalités du projet](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), comme décrit dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="f4401-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>


|<span data-ttu-id="f4401-112">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="f4401-112">Capability</span></span>|<span data-ttu-id="f4401-113">Description</span><span class="sxs-lookup"><span data-stu-id="f4401-113">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="f4401-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="f4401-114">AssemblyReferences</span></span>|<span data-ttu-id="f4401-115">Indique que le projet prend en charge les références d’assembly (ceci est différent de WinRTReferences)</span><span class="sxs-lookup"><span data-stu-id="f4401-115">Indicates that the project supports assembly references (distinct from WinRTReferences)</span></span>|
|<span data-ttu-id="f4401-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="f4401-116">DeclaredSourceItems</span></span>|<span data-ttu-id="f4401-117">Indique que le projet est un projet MSBuild classique (non DNX) dans la mesure où il déclare des éléments sources dans le projet lui-même (et non pas dans un fichier `project.json` qui suppose que tous les fichiers du dossier font partie d’une compilation).</span><span class="sxs-lookup"><span data-stu-id="f4401-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself (rather than a `project.json` file that assumes all files in the folder are part of a compilation).</span></span>|
|<span data-ttu-id="f4401-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="f4401-118">UserSourceItems</span></span>|<span data-ttu-id="f4401-119">Indique que l’utilisateur est autorisé à ajouter des fichiers arbitraires à son projet.</span><span class="sxs-lookup"><span data-stu-id="f4401-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span>|

<span data-ttu-id="f4401-120">Pour les systèmes de projets basés sur CPS, les détails d’implémentation des fonctionnalités des projets décrites dans le reste de cette section ont été écrits pour vous.</span><span class="sxs-lookup"><span data-stu-id="f4401-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="f4401-121">Consultez [Déclaration des fonctionnalités de projet dans les projets CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="f4401-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="f4401-122">Implémentation de VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="f4401-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="f4401-123">La classe `VsProjectCapabilitiesPresenceChecker` doit implémenter l’interface `IVsBooleanSymbolPresenceChecker`, qui est définie comme suit :</span><span class="sxs-lookup"><span data-stu-id="f4401-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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


<span data-ttu-id="f4401-124">Voici un exemple d’implémentation de cette interface :</span><span class="sxs-lookup"><span data-stu-id="f4401-124">A sample implementation of this interface would then be:</span></span>
    
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

<span data-ttu-id="f4401-125">N’oubliez pas d’ajouter/supprimer des fonctionnalités dans l’ensemble `ActualProjectCapabilities`, en fonction de ce que votre système de projets prend réellement en charge.</span><span class="sxs-lookup"><span data-stu-id="f4401-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="f4401-126">Pour obtenir des descriptions complètes, consultez la [documentation sur les fonctionnalités des projets](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="f4401-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="f4401-127">Réponse à des requêtes</span><span class="sxs-lookup"><span data-stu-id="f4401-127">Responding to queries</span></span>

<span data-ttu-id="f4401-128">Un projet déclare cette fonctionnalité en prenant en charge la propriété `VSHPROPID_ProjectCapabilitiesChecker` via `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="f4401-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="f4401-129">Elle doit retourner une instance de `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, qui est défini dans l’assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`.</span><span class="sxs-lookup"><span data-stu-id="f4401-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="f4401-130">Référencez cet assembly en installant le [package NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="f4401-130">Reference this assembly by installing the [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="f4401-131">Par exemple, vous pouvez ajouter l’instruction `case` suivante à l’instruction `switch` de votre méthode `IVsHierarchy::GetProperty` :</span><span class="sxs-lookup"><span data-stu-id="f4401-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="f4401-132">Prise en charge de DTE</span><span class="sxs-lookup"><span data-stu-id="f4401-132">DTE Support</span></span>

<span data-ttu-id="f4401-133">NuGet pilote le système de projets pour ajouter des références, des éléments de contenu et des importations MSBuild en appelant [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), qui est l’interface d’automatisation du plus haut niveau de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f4401-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="f4401-134">DTE est un ensemble d’interfaces COM que vous pouvez déjà implémenter.</span><span class="sxs-lookup"><span data-stu-id="f4401-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="f4401-135">Si votre type de projet est basé sur CPS, DTE est implémenté pour vous.</span><span class="sxs-lookup"><span data-stu-id="f4401-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
