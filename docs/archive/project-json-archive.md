---
title: "Contenu archivé de project.json NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Éléments divers du contenu de project.json supprimés à d’autres endroits de la documentation NuGet."
keywords: Fichier project.json NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 42a40c6c637839c13effc9e476ac5702a92cfd2a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="e7a87-104">Archive project.json</span><span class="sxs-lookup"><span data-stu-id="e7a87-104">project.json archive</span></span>

<span data-ttu-id="e7a87-105">Le format de référence `project.json`, introduit avec NuGet 3.x, est utilisé pour certains types de projets.</span><span class="sxs-lookup"><span data-stu-id="e7a87-105">The `project.json` reference format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="e7a87-106">Il est déconseillé depuis l’introduction du format PackageReference, suivant lequel les dépendances sont listées directement dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="e7a87-106">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="e7a87-107">Voir aussi :</span><span class="sxs-lookup"><span data-stu-id="e7a87-107">Also see:</span></span>

- [<span data-ttu-id="e7a87-108">Schéma project.json</span><span class="sxs-lookup"><span data-stu-id="e7a87-108">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="e7a87-109">Impact de project.json sur les auteurs de packages</span><span class="sxs-lookup"><span data-stu-id="e7a87-109">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="e7a87-110">project.json et UWP</span><span class="sxs-lookup"><span data-stu-id="e7a87-110">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-reference-format"></a><span data-ttu-id="e7a87-111">Format de référence de project.json</span><span class="sxs-lookup"><span data-stu-id="e7a87-111">project.json reference format</span></span>

<span data-ttu-id="e7a87-112">*À l’origine dans [Restauration de packages](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-112">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="e7a87-113">Dans la liste des formats de référence :</span><span class="sxs-lookup"><span data-stu-id="e7a87-113">In the list of reference formats:</span></span>

- <span data-ttu-id="e7a87-114">[`project.json`](project-json.md) : *(déconseillé)* fichier JSON qui gère la liste des dépendances du projet avec un graphique de packages global dans un fichier associé, `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-114">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="e7a87-115">Ce format est déconseillé ; préférer PackageReference.</span><span class="sxs-lookup"><span data-stu-id="e7a87-115">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="e7a87-116">Restauration NuGet sur Mono</span><span class="sxs-lookup"><span data-stu-id="e7a87-116">nuget restore on Mono</span></span>

<span data-ttu-id="e7a87-117">*À l’origine dans [Installer les outils clients NuGet](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-117">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="e7a87-118">Fonctionne avec `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-118">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="e7a87-119">Restriction des versions de package avec la restauration</span><span class="sxs-lookup"><span data-stu-id="e7a87-119">Constraining package versions with restore</span></span>

<span data-ttu-id="e7a87-120">*À l’origine dans [Restauration de packages](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-120">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="e7a87-121">`project.json` : permet de spécifier une plage de versions directement avec le numéro de version de la dépendance.</span><span class="sxs-lookup"><span data-stu-id="e7a87-121">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="e7a87-122">Exemple :</span><span class="sxs-lookup"><span data-stu-id="e7a87-122">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="e7a87-123">Commandes CLI NuGet</span><span class="sxs-lookup"><span data-stu-id="e7a87-123">NuGet CLI commands</span></span>

- <span data-ttu-id="e7a87-124">`nuget install` ne fonctionne pas avec `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-124">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="e7a87-125">`nuget restore` : avec des projets qui utilisent `project.json`, génère un fichier `project.lock.json` et un fichier `<project>.nuget.props`, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e7a87-125">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="e7a87-126">(Les deux fichiers ne doivent pas obligatoirement figurer dans le contrôle de code source.) L’argument `<projectPath>` peut pointer vers un fichier `project.json` ; il a le même comportement que s’il pointait vers un fichier `packages.config` ou un fichier projet.</span><span class="sxs-lookup"><span data-stu-id="e7a87-126">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="e7a87-127">Dans l’ordre de priorité des dossiers de packages, `%userprofile%\.nuget\packages` est parcouru en premier lorsque `project.json` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="e7a87-127">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="e7a87-128">`nuget update` : sur Mono, cette commande ne fonctionne pas avec les projets qui utilisent `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-128">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="e7a87-129">Résolution des dépendances avec PackageReference</span><span class="sxs-lookup"><span data-stu-id="e7a87-129">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="e7a87-130">*À l’origine dans [Résolution des dépendances](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-130">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="e7a87-131">Le comportement de PackageReference s’applique également à `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-131">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="e7a87-132">La restauration NuGet écrit le graphique de dépendance dans un fichier nommé `project.lock.json` à côté de `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-132">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="e7a87-133">Gestion des ressources de dépendance</span><span class="sxs-lookup"><span data-stu-id="e7a87-133">Managing dependency assets</span></span>

<span data-ttu-id="e7a87-134">*À l’origine dans [Résolution des dépendances](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-134">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="e7a87-135">Le format `project.json` permet de choisir les ressources des dépendances qui seront acheminées dans le projet de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="e7a87-135">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="e7a87-136">Pour plus d’informations, consultez la section [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="e7a87-136">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="e7a87-137">Exclusion de références</span><span class="sxs-lookup"><span data-stu-id="e7a87-137">Excluding references</span></span>

<span data-ttu-id="e7a87-138">*À l’origine dans [Résolution des dépendances](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-138">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="e7a87-139">`project.json` : ajoutez `"exclude" : "all"` dans la dépendance au Package C :</span><span class="sxs-lookup"><span data-stu-id="e7a87-139">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="e7a87-140">Résolution des erreurs de package incompatible</span><span class="sxs-lookup"><span data-stu-id="e7a87-140">Resolving incompatible package errors</span></span>

<span data-ttu-id="e7a87-141">*À l’origine dans [Résolution des dépendances](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-141">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="e7a87-142">Voici un autre moyen de résoudre les erreurs :</span><span class="sxs-lookup"><span data-stu-id="e7a87-142">An added means of resolving errors:</span></span>

- <span data-ttu-id="e7a87-143">**Non recommandé** : lorsque vous collaborez avec l’auteur du package, vous pouvez, comme solution temporaire, faire en sorte que les projets ciblant `netcore`, `netstandard` et `netcoreapp` référencent d’autres frameworks comme étant compatibles. Vous permettez ainsi l’utilisation des packages qui ciblent ces autres frameworks.</span><span class="sxs-lookup"><span data-stu-id="e7a87-143">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="e7a87-144">Consultez [Importations project.json](project-json.md#imports) et [Restauration de cibles MSBuild avec PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="e7a87-144">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="e7a87-145">Cela peut provoquer des comportements inattendus. Par conséquent, il est préférable de résoudre les incompatibilités de package en travaillant à une mise à jour du package avec son auteur.</span><span class="sxs-lookup"><span data-stu-id="e7a87-145">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="e7a87-146">Versions cibles de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e7a87-146">Target frameworks</span></span>

<span data-ttu-id="e7a87-147">*À l’origine dans [Versions cibles de .NET Framework](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-147">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="e7a87-148">[project.json](project-json.md) : le nœud `frameworks` spécifie les versions cibles de .NET Framework avec lesquelles le projet peut être compilé.</span><span class="sxs-lookup"><span data-stu-id="e7a87-148">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="e7a87-149">Créer un package</span><span class="sxs-lookup"><span data-stu-id="e7a87-149">Creating a package</span></span>

<span data-ttu-id="e7a87-150">*À l’origine dans [Créer un package](../create-packages/creating-a-package.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-150">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="e7a87-151">Définition d’un type de package</span><span class="sxs-lookup"><span data-stu-id="e7a87-151">Setting a package type</span></span>

<span data-ttu-id="e7a87-152">Avec .NET Core 1.x, lors de l’installation d’un package DotnetCliTool, Visual Studio le place dans le nœud `project.json` `tools` plutôt que dans le nœud `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-152">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="e7a87-153">Les types de package sont définis dans `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-153">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="e7a87-154">`project.json` : indique le type de package dans un json de propriété `packOptions.packageType` :</span><span class="sxs-lookup"><span data-stu-id="e7a87-154">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="e7a87-155">Ajout de cibles et de propriétés pour MSBuild</span><span class="sxs-lookup"><span data-stu-id="e7a87-155">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="e7a87-156">*À l’origine dans [Créer des packages NuGet .NET Standard avec Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-156">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="e7a87-157">Quand vous utilisez `project.json`, les cibles ne sont pas ajoutées au projet, mais sont accessibles via `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-157">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="e7a87-158">Contrôle de version des packages</span><span class="sxs-lookup"><span data-stu-id="e7a87-158">Package versioning</span></span>

<span data-ttu-id="e7a87-159">*À l’origine dans [Contrôle de version des packages](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-159">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="e7a87-160">Lorsque le format `project.json` est utilisé, NuGet prend également en charge la notation avec le caractère générique \* pour le suffixe du chiffre correspondant aux versions majeure, mineure, corrective et préversion.</span><span class="sxs-lookup"><span data-stu-id="e7a87-160">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="e7a87-161">Informations de référence sur NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="e7a87-161">NuGet.Config reference</span></span>

<span data-ttu-id="e7a87-162">*À l’origine dans [Informations de référence sur NuGet.Config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-162">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="e7a87-163">`globalPackagesFolder` s’applique uniquement à `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-163">`globalPackagesFolder` applies only to `project.json`.</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="e7a87-164">Informations de référence sur nuspec</span><span class="sxs-lookup"><span data-stu-id="e7a87-164">nuspec file reference</span></span>

<span data-ttu-id="e7a87-165">*À l’origine dans [Informations de référence sur nuspec](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="e7a87-166">L’élément `<contentFiles>` est utilisé à la place de `<files>` avec `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="e7a87-167">Contrôle des options du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="e7a87-167">Package manager options control</span></span>

<span data-ttu-id="e7a87-168">*À l’origine dans [Informations de référence sur l’interface utilisateur du Gestionnaire de package](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="e7a87-169">Les projets qui utilisent le format de référence `project.json` présentent uniquement l’option **Afficher la fenêtre d’aperçu**.</span><span class="sxs-lookup"><span data-stu-id="e7a87-169">Projects using `project.json` reference format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="e7a87-170">Modèles Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e7a87-170">Visual Studio Templates</span></span>

<span data-ttu-id="e7a87-171">*À l’origine dans [Packages NuGet dans les modèles Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="e7a87-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="e7a87-172">Meilleures pratiques : les modèles ne comportent pas de fichier `project.json` ; n’incluez aucune référence ni aucun contenu qui serait ajouté lors de l’installation des packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="e7a87-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>