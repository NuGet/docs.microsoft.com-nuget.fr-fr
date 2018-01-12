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
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Prise en charge de NuGet pour le système de projets Visual Studio

Pour prendre en charge des types de projets tiers dans Visual Studio, NuGet 3.x+ prend en charge le [Système de projets commun (CPS, Common Project System)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), tandis que NuGet 3.2+ prend aussi en charge les systèmes de projets non-CPS.

Pour s’intégrer à NuGet, un système de projets doit publier sa propre prise en charge de toutes les fonctionnalités des projets décrites dans cette rubrique.


> [!NOTE]
> Ne déclarez pas des fonctionnalités que votre projet n’a pas en réalité, de façon à permettre l’installation correcte des packages dans votre projet. De nombreuses fonctionnalités de Visual Studio et d’autres extensions dépendent des fonctionnalités du projet, en plus du client NuGet. Publier des fonctionnalités dont votre projet ne dispose pas en réalité peut provoquer le dysfonctionnement de ces composants et une dégradation de l’expérience de vos utilisateurs.

## <a name="advertise-project-capabilities"></a>Publier les fonctionnalités d’un projet

Le client NuGet détermine les packages qui sont compatibles avec votre type de projet en fonction des [fonctionnalités du projet](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), comme décrit dans le tableau suivant.


|Fonctionnalité|Description|
|----------------|-----------|
|AssemblyReferences|Indique que le projet prend en charge les références d’assembly (ceci est différent de WinRTReferences)|
|DeclaredSourceItems|Indique que le projet est un projet MSBuild classique (non DNX) dans la mesure où il déclare des éléments sources dans le projet lui-même (et non pas dans un fichier `project.json` qui suppose que tous les fichiers du dossier font partie d’une compilation).|
|UserSourceItems|Indique que l’utilisateur est autorisé à ajouter des fichiers arbitraires à son projet.|

Pour les systèmes de projets basés sur CPS, les détails d’implémentation des fonctionnalités des projets décrites dans le reste de cette section ont été écrits pour vous. Consultez [Déclaration des fonctionnalités de projet dans les projets CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implémentation de VsProjectCapabilitiesPresenceChecker

La classe `VsProjectCapabilitiesPresenceChecker` doit implémenter l’interface `IVsBooleanSymbolPresenceChecker`, qui est définie comme suit :

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


Voici un exemple d’implémentation de cette interface :
    
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

N’oubliez pas d’ajouter/supprimer des fonctionnalités dans l’ensemble `ActualProjectCapabilities`, en fonction de ce que votre système de projets prend réellement en charge. Pour obtenir des descriptions complètes, consultez la [documentation sur les fonctionnalités des projets](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).

## <a name="responding-to-queries"></a>Réponse à des requêtes

Un projet déclare cette fonctionnalité en prenant en charge la propriété `VSHPROPID_ProjectCapabilitiesChecker` via `IVsHierarchy::GetProperty`. Elle doit retourner une instance de `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, qui est défini dans l’assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`. Référencez cet assembly en installant le [package NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Par exemple, vous pouvez ajouter l’instruction `case` suivante à l’instruction `switch` de votre méthode `IVsHierarchy::GetProperty` :

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Prise en charge de DTE

NuGet pilote le système de projets pour ajouter des références, des éléments de contenu et des importations MSBuild en appelant [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), qui est l’interface d’automatisation du plus haut niveau de Visual Studio. DTE est un ensemble d’interfaces COM que vous pouvez déjà implémenter.

Si votre type de projet est basé sur CPS, DTE est implémenté pour vous.
