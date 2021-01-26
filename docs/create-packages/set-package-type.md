---
title: Définir un type de package NuGet
description: Décrit les types de packages pour indiquer l’utilisation prévue d’un package.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774369"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="85868-103">Définir un type de package NuGet</span><span class="sxs-lookup"><span data-stu-id="85868-103">Set a NuGet package type</span></span>

<span data-ttu-id="85868-104">Avec NuGet 3.5+, les packages peuvent être marqués avec un *type de package* spécifique pour indiquer leur usage prévu.</span><span class="sxs-lookup"><span data-stu-id="85868-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="85868-105">Les packages non marqués avec un type, notamment tous les packages créés avec des versions antérieures de NuGet, sont du type `Dependency` par défaut.</span><span class="sxs-lookup"><span data-stu-id="85868-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="85868-106">Les packages de type `Dependency` ajoutent des ressources de build ou d’exécution aux bibliothèques et applications et peuvent être installés dans n’importe quel type de projet (en supposant qu’ils soient compatibles).</span><span class="sxs-lookup"><span data-stu-id="85868-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="85868-107">Les packages de type `DotnetTool` sont des extensions de la [CLI dotnet](/dotnet/articles/core/tools/index) et ils sont appelés à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="85868-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="85868-108">De tels packages peuvent être installés uniquement dans des projets .NET Core et n’ont aucun effet sur les opérations de restauration.</span><span class="sxs-lookup"><span data-stu-id="85868-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="85868-109">Plus d’informations sur ces extensions par projet sont disponibles dans la documentation [Extensibilité de .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="85868-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="85868-110">`Template` les packages de type fournissent des [modèles personnalisés](/dotnet/core/tools/custom-templates) qui peuvent être utilisés pour créer des fichiers ou des projets comme une application, un service, un outil ou une bibliothèque de classes.</span><span class="sxs-lookup"><span data-stu-id="85868-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="85868-111">Les packages de type personnalisé utilisent un identificateur de type arbitraire qui respecte les mêmes règles de format que les ID de package.</span><span class="sxs-lookup"><span data-stu-id="85868-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="85868-112">Tous les types autres que `Dependency` et `DotnetTool`, en revanche, ne sont pas reconnus par le gestionnaire de package NuGet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85868-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="85868-113">Les types de package sont définis dans le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="85868-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="85868-114">Il est préférable pour la compatibilité descendante de ne *pas* définir explicitement le type `Dependency` et de plutôt compter sur le fait que NuGet supposera qu’il s’agit de ce type quand aucun type n’est spécifié.</span><span class="sxs-lookup"><span data-stu-id="85868-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="85868-115">`.nuspec` : indique le type de package dans un nœud `packageTypes\packageType` sous l’élément `<metadata>` :</span><span class="sxs-lookup"><span data-stu-id="85868-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
