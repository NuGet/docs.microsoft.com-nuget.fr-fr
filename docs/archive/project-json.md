---
title: "Informations de référence sur le fichier project.json pour NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/27/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Dans certains types de projets, project.json gère la liste des packages NuGet utilisés dans le projet."
keywords: "project.json NuGet, références de package NuGet, dépendances NuGet, project.lock.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2e2c521b18dd67e49942cc20eafef0be7f91573a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="projectjson-reference"></a><span data-ttu-id="3d32e-104">Documentation de référence sur project.json</span><span class="sxs-lookup"><span data-stu-id="3d32e-104">project.json reference</span></span>

<span data-ttu-id="3d32e-105">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="3d32e-105">*NuGet 3.x+*</span></span>

<span data-ttu-id="3d32e-106">Le fichier `project.json` gère une liste de packages utilisés dans un projet, appelée format de référence de package.</span><span class="sxs-lookup"><span data-stu-id="3d32e-106">The `project.json` file maintains a list of packages used in a project, known as a package reference format.</span></span> <span data-ttu-id="3d32e-107">Il remplace `packages.config` mais est à son tour remplacé par [PackageReference](../consume-packages/package-references-in-project-files.md) avec NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="3d32e-107">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="3d32e-108">Le fichier [`project.lock.json`](#projectlockjson) (décrit ci-dessous) est également utilisé dans les projets employant `project.json`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-108">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="3d32e-109">`project.json` présente la structure de base suivante, où chacun des quatre objets de niveau supérieur peut avoir un nombre quelconque d’objets enfants :</span><span class="sxs-lookup"><span data-stu-id="3d32e-109">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="3d32e-110">Dépendances</span><span class="sxs-lookup"><span data-stu-id="3d32e-110">Dependencies</span></span>

<span data-ttu-id="3d32e-111">Répertorie les dépendances de package NuGet de votre projet sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="3d32e-111">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="3d32e-112">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3d32e-112">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="3d32e-113">La section `dependencies` est l’emplacement où la boîte de dialogue Gestionnaire de package NuGet ajoute des dépendances de package à votre projet.</span><span class="sxs-lookup"><span data-stu-id="3d32e-113">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="3d32e-114">L’ID du package correspond à l’ID du package sur nuget.org, identique à l’ID utilisé dans la console du Gestionnaire de package : `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-114">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="3d32e-115">Lors de la restauration de packages, la contrainte de version `"5.0.0"` implique `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-115">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="3d32e-116">Autrement dit, si 5.0.0 n’est pas disponible sur le serveur mais que 5.0.1 l’est, NuGet installe 5.0.1 et vous informe de la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="3d32e-116">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="3d32e-117">NuGet récupère sinon la version la plus ancienne possible sur le serveur correspondant à la contrainte.</span><span class="sxs-lookup"><span data-stu-id="3d32e-117">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="3d32e-118">Consultez [Résolution des dépendances](../consume-packages/dependency-resolution.md) pour plus d’informations sur les règles de résolution.</span><span class="sxs-lookup"><span data-stu-id="3d32e-118">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="3d32e-119">Gestion des ressources de dépendance</span><span class="sxs-lookup"><span data-stu-id="3d32e-119">Managing dependency assets</span></span>

<span data-ttu-id="3d32e-120">Les ressources des dépendances qui sont transférées dans le projet de niveau supérieur sont contrôlées en spécifiant un ensemble de balises séparées par des virgules dans les propriétés `include` et `exclude` de la référence de dépendance.</span><span class="sxs-lookup"><span data-stu-id="3d32e-120">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="3d32e-121">Les balises sont répertoriées dans le tableau ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3d32e-121">The tags are listed the table below:</span></span>

| <span data-ttu-id="3d32e-122">Balise include/exclude</span><span class="sxs-lookup"><span data-stu-id="3d32e-122">Include/Exclude tag</span></span> | <span data-ttu-id="3d32e-123">Dossiers affectés de la cible</span><span class="sxs-lookup"><span data-stu-id="3d32e-123">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="3d32e-124">contentFiles</span><span class="sxs-lookup"><span data-stu-id="3d32e-124">contentFiles</span></span> | <span data-ttu-id="3d32e-125">Contenu</span><span class="sxs-lookup"><span data-stu-id="3d32e-125">Content</span></span>  |
| <span data-ttu-id="3d32e-126">runtime</span><span class="sxs-lookup"><span data-stu-id="3d32e-126">runtime</span></span> | <span data-ttu-id="3d32e-127">Runtime, Resources et FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="3d32e-127">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="3d32e-128">compile</span><span class="sxs-lookup"><span data-stu-id="3d32e-128">compile</span></span> | <span data-ttu-id="3d32e-129">lib</span><span class="sxs-lookup"><span data-stu-id="3d32e-129">lib</span></span> |
| <span data-ttu-id="3d32e-130">build</span><span class="sxs-lookup"><span data-stu-id="3d32e-130">build</span></span> | <span data-ttu-id="3d32e-131">build (propriétés et cibles MSBuild)</span><span class="sxs-lookup"><span data-stu-id="3d32e-131">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="3d32e-132">natifs</span><span class="sxs-lookup"><span data-stu-id="3d32e-132">native</span></span> | <span data-ttu-id="3d32e-133">natifs</span><span class="sxs-lookup"><span data-stu-id="3d32e-133">native</span></span> |
| <span data-ttu-id="3d32e-134">aucun</span><span class="sxs-lookup"><span data-stu-id="3d32e-134">none</span></span> | <span data-ttu-id="3d32e-135">Aucun dossier</span><span class="sxs-lookup"><span data-stu-id="3d32e-135">No folders</span></span> |
| <span data-ttu-id="3d32e-136">toutes les</span><span class="sxs-lookup"><span data-stu-id="3d32e-136">all</span></span> | <span data-ttu-id="3d32e-137">Tous les dossiers</span><span class="sxs-lookup"><span data-stu-id="3d32e-137">All folders</span></span> |

<span data-ttu-id="3d32e-138">Les balises spécifiées avec `exclude` sont prioritaires sur celles spécifiées avec `include`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-138">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="3d32e-139">Par exemple, `include="runtime, compile" exclude="compile"` est identique à `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-139">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="3d32e-140">Par exemple, pour inclure les dossiers `build` et `native` d’une dépendance, utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3d32e-140">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="3d32e-141">Pour exclure les dossiers `content` et `build` d’une dépendance, utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3d32e-141">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="3d32e-142">Frameworks</span><span class="sxs-lookup"><span data-stu-id="3d32e-142">Frameworks</span></span>

<span data-ttu-id="3d32e-143">Répertorie les frameworks sur lesquels le projet est exécuté, comme `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-143">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="3d32e-144">Une seule entrée est autorisée dans la section `frameworks`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-144">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="3d32e-145">(Les fichiers `project.json` pour les projets ASP.NET qui sont générés avec une chaîne d’outils DNX dépréciée, ce qui permet plusieurs cibles, représentent une exception.)</span><span class="sxs-lookup"><span data-stu-id="3d32e-145">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX toolchain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="3d32e-146">Runtimes</span><span class="sxs-lookup"><span data-stu-id="3d32e-146">Runtimes</span></span>

<span data-ttu-id="3d32e-147">Répertorie les systèmes d’exploitation et les architectures sur lesquels votre application est exécutée, comme `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-147">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="3d32e-148">Un package contenant une bibliothèque de classes portable qui peut s’exécuter sur n’importe quel runtime n’a pas besoin d’en spécifier un.</span><span class="sxs-lookup"><span data-stu-id="3d32e-148">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="3d32e-149">Cela doit également être vrai pour toutes les dépendances, sinon vous devez spécifier les runtimes.</span><span class="sxs-lookup"><span data-stu-id="3d32e-149">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="3d32e-150">Prises en charge</span><span class="sxs-lookup"><span data-stu-id="3d32e-150">Supports</span></span>

<span data-ttu-id="3d32e-151">Définit un ensemble de vérifications pour les dépendances de package.</span><span class="sxs-lookup"><span data-stu-id="3d32e-151">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="3d32e-152">Vous pouvez définir l’emplacement d’exécution prévu pour la bibliothèque de classes portable ou l’application.</span><span class="sxs-lookup"><span data-stu-id="3d32e-152">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="3d32e-153">Les définitions ne sont pas restrictives, comme votre code peut être en mesure de s’exécuter à un autre emplacement.</span><span class="sxs-lookup"><span data-stu-id="3d32e-153">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="3d32e-154">Toutefois, la spécification de ces vérifications permet à NuGet de contrôler que toutes les dépendances sont satisfaites sur les monikers du Framework cible répertoriés.</span><span class="sxs-lookup"><span data-stu-id="3d32e-154">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="3d32e-155">`net46.app`, `uwp.10.0.app`, entre autres, en sont des exemples de valeurs.</span><span class="sxs-lookup"><span data-stu-id="3d32e-155">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="3d32e-156">Cette section doit être renseignée automatiquement quand vous sélectionnez une entrée dans la boîte de dialogue des cibles de bibliothèque de classes portable.</span><span class="sxs-lookup"><span data-stu-id="3d32e-156">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="3d32e-157">Importations</span><span class="sxs-lookup"><span data-stu-id="3d32e-157">Imports</span></span>

<span data-ttu-id="3d32e-158">Les importations sont conçues pour permettre aux packages qui utilisent le moniker du Framework cible `dotnet` de fonctionner avec les packages qui ne déclarent pas de moniker du Framework cible dotnet.</span><span class="sxs-lookup"><span data-stu-id="3d32e-158">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="3d32e-159">Si votre projet utilise le moniker du Framework cible `dotnet`, tous les packages dont vous dépendez doivent également avoir un moniker du Framework cible `dotnet`, sauf si vous ajoutez le code suivant à votre fichier `project.json` afin de permettre à des plateformes autres que `dotnet` d’être compatibles avec `dotnet` :</span><span class="sxs-lookup"><span data-stu-id="3d32e-159">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="3d32e-160">Si vous utilisez le moniker du Framework cible `dotnet`, le système de projet de bibliothèque de classes portable ajoute l’instruction `imports` appropriée selon les cibles prises en charge.</span><span class="sxs-lookup"><span data-stu-id="3d32e-160">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="3d32e-161">Différences par rapport à des applications portables et des projets web</span><span class="sxs-lookup"><span data-stu-id="3d32e-161">Differences from portable apps and web projects</span></span>

<span data-ttu-id="3d32e-162">Le fichier `project.json` utilisé par NuGet est un sous-ensemble des éléments se trouvant dans les projets ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3d32e-162">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="3d32e-163">Dans ASP.NET Core, `project.json` est utilisé pour les métadonnées de projet, les informations de compilation et les dépendances.</span><span class="sxs-lookup"><span data-stu-id="3d32e-163">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="3d32e-164">Quand ils sont utilisés dans d’autres systèmes de projet, ces trois éléments sont répartis en fichiers distincts et `project.json` contient moins d’informations.</span><span class="sxs-lookup"><span data-stu-id="3d32e-164">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="3d32e-165">Les différences notables sont notamment les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3d32e-165">Notable differences include:</span></span>

- <span data-ttu-id="3d32e-166">Il ne peut exister qu’un framework dans la section `frameworks`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-166">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="3d32e-167">Le fichier ne peut pas contenir de dépendances, d’options de compilation ni d’autres éléments que vous voyez dans les fichiers `project.json` DNX.</span><span class="sxs-lookup"><span data-stu-id="3d32e-167">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="3d32e-168">Étant donné qu’il ne peut exister qu’un seul framework, il est inutile d’entrer des dépendances spécifiques au framework.</span><span class="sxs-lookup"><span data-stu-id="3d32e-168">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="3d32e-169">La compilation étant gérée par MSBuild, les options de compilation et les définitions du préprocesseur, entre autres, font toutes partie du fichier projet MSBuild et non de `project.json`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-169">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="3d32e-170">Dans NuGet 3+, les développeurs ne sont pas censés modifier manuellement le fichier `project.json`, car l’interface utilisateur du Gestionnaire de package dans Visual Studio manipule le contenu.</span><span class="sxs-lookup"><span data-stu-id="3d32e-170">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="3d32e-171">Ceci dit, vous pouvez certainement modifier le fichier, mais vous devez générer le projet pour démarrer une restauration de package ou appeler la restauration d’une autre façon.</span><span class="sxs-lookup"><span data-stu-id="3d32e-171">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="3d32e-172">Consultez [Restauration de packages](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="3d32e-172">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="3d32e-173">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="3d32e-173">project.lock.json</span></span>

<span data-ttu-id="3d32e-174">Le fichier `project.lock.json` est généré au cours de la restauration des packages NuGet dans les projets qui utilisent `project.json`.</span><span class="sxs-lookup"><span data-stu-id="3d32e-174">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="3d32e-175">Il contient un instantané de toutes les informations qui sont générées quand NuGet parcourt le graphique des packages et inclut la version, le contenu et les dépendances de tous les packages dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="3d32e-175">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="3d32e-176">Le système de génération l’utilise pour choisir les packages à partir d’un emplacement global qui sont pertinents lors de la génération du projet au lieu de dépendre d’un dossier de packages local dans le projet lui-même.</span><span class="sxs-lookup"><span data-stu-id="3d32e-176">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="3d32e-177">Les performances de génération sont ainsi plus rapides, car il est nécessaire d’accéder en lecture seule à `project.lock.json` et non à de nombreux fichiers `.nuspec` séparés.</span><span class="sxs-lookup"><span data-stu-id="3d32e-177">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="3d32e-178">`project.lock.json` étant généré automatiquement lors de la restauration de package, il peut être omis du contrôle de code source en l’ajoutant aux fichiers `.gitignore` et `.tfignore` (consultez [Packages et contrôle de code source](../consume-packages/packages-and-source-control.md)).</span><span class="sxs-lookup"><span data-stu-id="3d32e-178">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="3d32e-179">Toutefois, si vous l’incluez dans le contrôle de code source, l’historique des modifications affiche les modifications dans les dépendances résolues au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="3d32e-179">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
