---
title: Définir un type de package NuGet
description: Décrit les types de packages pour indiquer l’utilisation prévue d’un package.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843491"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="45629-103">Définir un type de package NuGet</span><span class="sxs-lookup"><span data-stu-id="45629-103">Set a NuGet package type</span></span>

<span data-ttu-id="45629-104">Avec NuGet 3.5+, les packages peuvent être marqués avec un *type de package* spécifique pour indiquer leur usage prévu.</span><span class="sxs-lookup"><span data-stu-id="45629-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="45629-105">Les packages non marqués avec un type, notamment tous les packages créés avec des versions antérieures de NuGet, sont du type `Dependency` par défaut.</span><span class="sxs-lookup"><span data-stu-id="45629-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="45629-106">Les packages de type `Dependency` ajoutent des ressources de build ou d’exécution aux bibliothèques et applications et peuvent être installés dans n’importe quel type de projet (en supposant qu’ils soient compatibles).</span><span class="sxs-lookup"><span data-stu-id="45629-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="45629-107">Les packages de type `DotnetCliTool` sont des extensions de la [CLI dotnet](/dotnet/articles/core/tools/index) et ils sont appelés à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="45629-107">`DotnetCliTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="45629-108">De tels packages peuvent être installés uniquement dans des projets .NET Core et n’ont aucun effet sur les opérations de restauration.</span><span class="sxs-lookup"><span data-stu-id="45629-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="45629-109">Plus d’informations sur ces extensions par projet sont disponibles dans la documentation [Extensibilité de .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="45629-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="45629-110">Les packages de type personnalisé utilisent un identificateur de type arbitraire qui respecte les mêmes règles de format que les ID de package.</span><span class="sxs-lookup"><span data-stu-id="45629-110">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="45629-111">Tous les types autres que `Dependency` et `DotnetCliTool`, en revanche, ne sont pas reconnus par le gestionnaire de package NuGet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45629-111">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="45629-112">Les types de package sont définis dans le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="45629-112">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="45629-113">Il est préférable pour la compatibilité descendante de ne *pas* définir explicitement le type `Dependency` et de plutôt compter sur le fait que NuGet supposera qu’il s’agit de ce type quand aucun type n’est spécifié.</span><span class="sxs-lookup"><span data-stu-id="45629-113">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="45629-114">`.nuspec`: Indique le type de package dans un nœud `packageTypes\packageType` sous l’élément `<metadata>` :</span><span class="sxs-lookup"><span data-stu-id="45629-114">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
