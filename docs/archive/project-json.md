---
title: Informations de référence sur le fichier project.json pour NuGet
description: Dans certains types de projets, project.json gère la liste des packages NuGet utilisés dans le projet.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547782"
---
# <a name="projectjson-reference"></a><span data-ttu-id="7a8bd-103">Documentation de référence sur project.json</span><span class="sxs-lookup"><span data-stu-id="7a8bd-103">project.json reference</span></span>

<span data-ttu-id="7a8bd-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="7a8bd-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="7a8bd-105">Le fichier `project.json` gère une liste de packages utilisés dans un projet, appelée format de gestion des packages.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="7a8bd-106">Il remplace `packages.config` mais est à son tour remplacé par [PackageReference](../consume-packages/package-references-in-project-files.md) avec NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="7a8bd-107">Le fichier [`project.lock.json`](#projectlockjson) (décrit ci-dessous) est également utilisé dans les projets employant `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="7a8bd-108">`project.json` présente la structure de base suivante, où chacun des quatre objets de niveau supérieur peut avoir un nombre quelconque d’objets enfants :</span><span class="sxs-lookup"><span data-stu-id="7a8bd-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="7a8bd-109">Dépendances</span><span class="sxs-lookup"><span data-stu-id="7a8bd-109">Dependencies</span></span>

<span data-ttu-id="7a8bd-110">Répertorie les dépendances de package NuGet de votre projet sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="7a8bd-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="7a8bd-111">Exemple :</span><span class="sxs-lookup"><span data-stu-id="7a8bd-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="7a8bd-112">La section `dependencies` est l’emplacement où la boîte de dialogue Gestionnaire de package NuGet ajoute des dépendances de package à votre projet.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="7a8bd-113">L’ID du package correspond à l’ID du package sur nuget.org, identique à l’ID utilisé dans la console du Gestionnaire de package : `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="7a8bd-114">Lors de la restauration de packages, la contrainte de version `"5.0.0"` implique `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="7a8bd-115">Autrement dit, si 5.0.0 n’est pas disponible sur le serveur mais que 5.0.1 l’est, NuGet installe 5.0.1 et vous informe de la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="7a8bd-116">NuGet récupère sinon la version la plus ancienne possible sur le serveur correspondant à la contrainte.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="7a8bd-117">Consultez [Résolution des dépendances](../consume-packages/dependency-resolution.md) pour plus d’informations sur les règles de résolution.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-117">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="7a8bd-118">Gestion des ressources de dépendance</span><span class="sxs-lookup"><span data-stu-id="7a8bd-118">Managing dependency assets</span></span>

<span data-ttu-id="7a8bd-119">Les ressources des dépendances qui sont transférées dans le projet de niveau supérieur sont contrôlées en spécifiant un ensemble de balises séparées par des virgules dans les propriétés `include` et `exclude` de la référence de dépendance.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="7a8bd-120">Les balises sont répertoriées dans le tableau ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7a8bd-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="7a8bd-121">Balise include/exclude</span><span class="sxs-lookup"><span data-stu-id="7a8bd-121">Include/Exclude tag</span></span> | <span data-ttu-id="7a8bd-122">Dossiers affectés de la cible</span><span class="sxs-lookup"><span data-stu-id="7a8bd-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="7a8bd-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7a8bd-123">contentFiles</span></span> | <span data-ttu-id="7a8bd-124">Contenu</span><span class="sxs-lookup"><span data-stu-id="7a8bd-124">Content</span></span>  |
| <span data-ttu-id="7a8bd-125">runtime</span><span class="sxs-lookup"><span data-stu-id="7a8bd-125">runtime</span></span> | <span data-ttu-id="7a8bd-126">Runtime, Resources et FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="7a8bd-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="7a8bd-127">compile</span><span class="sxs-lookup"><span data-stu-id="7a8bd-127">compile</span></span> | <span data-ttu-id="7a8bd-128">lib</span><span class="sxs-lookup"><span data-stu-id="7a8bd-128">lib</span></span> |
| <span data-ttu-id="7a8bd-129">build</span><span class="sxs-lookup"><span data-stu-id="7a8bd-129">build</span></span> | <span data-ttu-id="7a8bd-130">build (propriétés et cibles MSBuild)</span><span class="sxs-lookup"><span data-stu-id="7a8bd-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="7a8bd-131">native</span><span class="sxs-lookup"><span data-stu-id="7a8bd-131">native</span></span> | <span data-ttu-id="7a8bd-132">native</span><span class="sxs-lookup"><span data-stu-id="7a8bd-132">native</span></span> |
| <span data-ttu-id="7a8bd-133">none</span><span class="sxs-lookup"><span data-stu-id="7a8bd-133">none</span></span> | <span data-ttu-id="7a8bd-134">Aucun dossier</span><span class="sxs-lookup"><span data-stu-id="7a8bd-134">No folders</span></span> |
| <span data-ttu-id="7a8bd-135">all</span><span class="sxs-lookup"><span data-stu-id="7a8bd-135">all</span></span> | <span data-ttu-id="7a8bd-136">Tous les dossiers</span><span class="sxs-lookup"><span data-stu-id="7a8bd-136">All folders</span></span> |

<span data-ttu-id="7a8bd-137">Les balises spécifiées avec `exclude` sont prioritaires sur celles spécifiées avec `include`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="7a8bd-138">Par exemple, `include="runtime, compile" exclude="compile"` est identique à `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="7a8bd-139">Par exemple, pour inclure les dossiers `build` et `native` d’une dépendance, utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="7a8bd-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="7a8bd-140">Pour exclure les dossiers `content` et `build` d’une dépendance, utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="7a8bd-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="7a8bd-141">Frameworks</span><span class="sxs-lookup"><span data-stu-id="7a8bd-141">Frameworks</span></span>

<span data-ttu-id="7a8bd-142">Répertorie les frameworks sur lesquels le projet est exécuté, comme `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="7a8bd-143">Une seule entrée est autorisée dans la section `frameworks`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="7a8bd-144">(Les fichiers `project.json` des projets ASP.NET créés avec une chaîne d’outils DNX déconseillée, qui autorise plusieurs cibles, font figure d’exception.)</span><span class="sxs-lookup"><span data-stu-id="7a8bd-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="7a8bd-145">Runtimes</span><span class="sxs-lookup"><span data-stu-id="7a8bd-145">Runtimes</span></span>

<span data-ttu-id="7a8bd-146">Répertorie les systèmes d’exploitation et les architectures sur lesquels votre application est exécutée, comme `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="7a8bd-147">Un package contenant une bibliothèque de classes portable qui peut s’exécuter sur n’importe quel runtime n’a pas besoin d’en spécifier un.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="7a8bd-148">Cela doit également être vrai pour toutes les dépendances, sinon vous devez spécifier les runtimes.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="7a8bd-149">Prises en charge</span><span class="sxs-lookup"><span data-stu-id="7a8bd-149">Supports</span></span>

<span data-ttu-id="7a8bd-150">Définit un ensemble de vérifications pour les dépendances de package.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="7a8bd-151">Vous pouvez définir l’emplacement d’exécution prévu pour la bibliothèque de classes portable ou l’application.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="7a8bd-152">Les définitions ne sont pas restrictives, comme votre code peut être en mesure de s’exécuter à un autre emplacement.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="7a8bd-153">Toutefois, la spécification de ces vérifications permet à NuGet de contrôler que toutes les dépendances sont satisfaites sur les monikers du Framework cible répertoriés.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="7a8bd-154">`net46.app`, `uwp.10.0.app`, entre autres, en sont des exemples de valeurs.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="7a8bd-155">Cette section doit être renseignée automatiquement quand vous sélectionnez une entrée dans la boîte de dialogue des cibles de bibliothèque de classes portable.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="7a8bd-156">Importations</span><span class="sxs-lookup"><span data-stu-id="7a8bd-156">Imports</span></span>

<span data-ttu-id="7a8bd-157">Les importations sont conçues pour permettre aux packages qui utilisent le moniker du Framework cible `dotnet` de fonctionner avec les packages qui ne déclarent pas de moniker du Framework cible dotnet.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="7a8bd-158">Si votre projet utilise le moniker du Framework cible `dotnet`, tous les packages dont vous dépendez doivent également avoir un moniker du Framework cible `dotnet`, sauf si vous ajoutez le code suivant à votre fichier `project.json` afin de permettre à des plateformes autres que `dotnet` d’être compatibles avec `dotnet` :</span><span class="sxs-lookup"><span data-stu-id="7a8bd-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="7a8bd-159">Si vous utilisez le moniker du Framework cible `dotnet`, le système de projet de bibliothèque de classes portable ajoute l’instruction `imports` appropriée selon les cibles prises en charge.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="7a8bd-160">Différences par rapport à des applications portables et des projets web</span><span class="sxs-lookup"><span data-stu-id="7a8bd-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="7a8bd-161">Le fichier `project.json` utilisé par NuGet est un sous-ensemble des éléments se trouvant dans les projets ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="7a8bd-162">Dans ASP.NET Core, `project.json` est utilisé pour les métadonnées de projet, les informations de compilation et les dépendances.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="7a8bd-163">Quand ils sont utilisés dans d’autres systèmes de projet, ces trois éléments sont répartis en fichiers distincts et `project.json` contient moins d’informations.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="7a8bd-164">Les différences notables sont notamment les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7a8bd-164">Notable differences include:</span></span>

- <span data-ttu-id="7a8bd-165">Il ne peut exister qu’un framework dans la section `frameworks`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="7a8bd-166">Le fichier ne peut pas contenir de dépendances, d’options de compilation ni d’autres éléments que vous voyez dans les fichiers `project.json` DNX.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="7a8bd-167">Étant donné qu’il ne peut exister qu’un seul framework, il est inutile d’entrer des dépendances spécifiques au framework.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="7a8bd-168">La compilation étant gérée par MSBuild, les options de compilation et les définitions du préprocesseur, entre autres, font toutes partie du fichier projet MSBuild et non de `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="7a8bd-169">Dans NuGet 3+, les développeurs ne sont pas censés modifier manuellement le fichier `project.json`, car l’interface utilisateur du Gestionnaire de package dans Visual Studio manipule le contenu.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="7a8bd-170">Ceci dit, vous pouvez certainement modifier le fichier, mais vous devez générer le projet pour démarrer une restauration de package ou appeler la restauration d’une autre façon.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="7a8bd-171">Consultez [Restauration de packages](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7a8bd-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="7a8bd-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="7a8bd-172">project.lock.json</span></span>

<span data-ttu-id="7a8bd-173">Le fichier `project.lock.json` est généré au cours de la restauration des packages NuGet dans les projets qui utilisent `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="7a8bd-174">Il contient un instantané de toutes les informations qui sont générées quand NuGet parcourt le graphique des packages et inclut la version, le contenu et les dépendances de tous les packages dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="7a8bd-175">Le système de génération l’utilise pour choisir les packages à partir d’un emplacement global qui sont pertinents lors de la génération du projet au lieu de dépendre d’un dossier de packages local dans le projet lui-même.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="7a8bd-176">Les performances de génération sont ainsi plus rapides, car il est nécessaire d’accéder en lecture seule à `project.lock.json` et non à de nombreux fichiers `.nuspec` séparés.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="7a8bd-177">`project.lock.json` étant généré automatiquement lors de la restauration de package, il peut être omis du contrôle de code source en l’ajoutant aux fichiers `.gitignore` et `.tfignore` (consultez [Packages et contrôle de code source](../consume-packages/packages-and-source-control.md)).</span><span class="sxs-lookup"><span data-stu-id="7a8bd-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="7a8bd-178">Toutefois, si vous l’incluez dans le contrôle de code source, l’historique des modifications affiche les modifications dans les dépendances résolues au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="7a8bd-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
