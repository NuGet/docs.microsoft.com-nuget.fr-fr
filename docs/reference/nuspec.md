---
title: Référence du fichier .nuspec pour NuGet
description: Le fichier .nuspec contient des métadonnées de package utilisées lors de la création d’un package et pour fournir des informations aux consommateurs de packages.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: e4c57c0580fe9018703291c08d60e559f95183dc
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426206"
---
# <a name="nuspec-reference"></a><span data-ttu-id="d181e-103">Informations de référence sur le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="d181e-103">.nuspec reference</span></span>

<span data-ttu-id="d181e-104">Un fichier `.nuspec` est un manifeste XML qui contient des métadonnées de package.</span><span class="sxs-lookup"><span data-stu-id="d181e-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="d181e-105">Ce manifeste est utilisé à la fois pour générer le package et pour fournir des informations aux consommateurs.</span><span class="sxs-lookup"><span data-stu-id="d181e-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="d181e-106">Le manifeste est toujours inclus dans un package.</span><span class="sxs-lookup"><span data-stu-id="d181e-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="d181e-107">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="d181e-107">In this topic:</span></span>

- [<span data-ttu-id="d181e-108">Forme générale et schéma</span><span class="sxs-lookup"><span data-stu-id="d181e-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="d181e-109">[Jetons de remplacement](#replacement-tokens) (lors d’une utilisation avec un projet Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d181e-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="d181e-110">Dépendances</span><span class="sxs-lookup"><span data-stu-id="d181e-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="d181e-111">Références d’assembly explicite</span><span class="sxs-lookup"><span data-stu-id="d181e-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="d181e-112">Références d’assembly Framework</span><span class="sxs-lookup"><span data-stu-id="d181e-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="d181e-113">Inclusion des fichiers d’assembly</span><span class="sxs-lookup"><span data-stu-id="d181e-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="d181e-114">Inclusion des fichiers de contenu</span><span class="sxs-lookup"><span data-stu-id="d181e-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="d181e-115">Exemples de fichiers nuspec</span><span class="sxs-lookup"><span data-stu-id="d181e-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="d181e-116">Compatibilité des types de projet</span><span class="sxs-lookup"><span data-stu-id="d181e-116">Project type compatibility</span></span>

- <span data-ttu-id="d181e-117">Utilisez `.nuspec` avec `nuget.exe pack` pour non-SDK-style des projets qui utilisent `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d181e-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="d181e-118">Un `.nuspec` fichier n’est pas nécessaire pour créer des packages pour les projets de style SDK (.NET Core et .NET Standard des projets qui utilisent le [attribut SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="d181e-118">A `.nuspec` file is not required to create packages for SDK-style projects (.NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="d181e-119">(Notez qu’un `.nuspec` est généré lorsque vous créez le package.)</span><span class="sxs-lookup"><span data-stu-id="d181e-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="d181e-120">Si vous créez un package à l’aide `dotnet.exe pack` ou `msbuild pack target`, il est recommandé que vous [inclure toutes les propriétés](../reference/msbuild-targets.md#pack-target) qui ne figurent généralement dans le `.nuspec` à la place de fichiers dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="d181e-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="d181e-121">Toutefois, vous pouvez choisir à la place de [utiliser un `.nuspec` fichier de pack à l’aide de `dotnet.exe` ou `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="d181e-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="d181e-122">Pour les projets migrés à partir de `packages.config` à [PackageReference](../consume-packages/package-references-in-project-files.md), un `.nuspec` fichier n’est pas nécessaire pour créer le package.</span><span class="sxs-lookup"><span data-stu-id="d181e-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="d181e-123">Au lieu de cela, utilisez [pack msbuild](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="d181e-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="d181e-124">Forme générale et schéma</span><span class="sxs-lookup"><span data-stu-id="d181e-124">General form and schema</span></span>

<span data-ttu-id="d181e-125">Le fichier de schéma `nuspec.xsd` actuel se trouve dans le [dépôt GitHub NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="d181e-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="d181e-126">Dans ce schéma, un fichier `.nuspec` a la forme générale suivante :</span><span class="sxs-lookup"><span data-stu-id="d181e-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="d181e-127">Pour obtenir une représentation visuelle claire du schéma, ouvrez le fichier de schéma dans Visual Studio en mode Design et cliquez sur le lien **Explorateur de schémas XML**.</span><span class="sxs-lookup"><span data-stu-id="d181e-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="d181e-128">Vous pouvez également ouvrir le fichier en tant que code, cliquer avec le bouton droit dans l’éditeur, puis sélectionner **Show XML Schema Explorer** (Afficher l’Explorateur de schémas XML).</span><span class="sxs-lookup"><span data-stu-id="d181e-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="d181e-129">Dans les deux cas, vous obtenez un affichage semblable à celui ci-dessous (quand il est en grande partie développé) :</span><span class="sxs-lookup"><span data-stu-id="d181e-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorateur de schémas Visual Studio avec nuspec.xsd ouvert](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="d181e-131">Éléments de métadonnées requis</span><span class="sxs-lookup"><span data-stu-id="d181e-131">Required metadata elements</span></span>

<span data-ttu-id="d181e-132">Bien que les éléments suivants correspondent à la configuration minimale requise pour un package, vous devez envisager d’ajouter les [éléments de métadonnées facultatifs](#optional-metadata-elements) afin d’améliorer l’expérience globale des développeurs avec votre package.</span><span class="sxs-lookup"><span data-stu-id="d181e-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="d181e-133">Ces éléments doivent apparaître dans un élément `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="d181e-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="d181e-134">ID</span><span class="sxs-lookup"><span data-stu-id="d181e-134">id</span></span> 
<span data-ttu-id="d181e-135">Identificateur de package ne respectant pas la casse, qui doit être unique dans nuget.org ou dans toute autre galerie susceptible d’héberger le package.</span><span class="sxs-lookup"><span data-stu-id="d181e-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="d181e-136">Les ID ne peuvent pas contenir d’espaces ni de caractères qui ne sont pas valides pour une URL et suivent généralement les règles d’espace de noms .NET.</span><span class="sxs-lookup"><span data-stu-id="d181e-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="d181e-137">Pour obtenir des conseils, consultez [Choix d’un identificateur de package unique](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="d181e-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="d181e-138">version</span><span class="sxs-lookup"><span data-stu-id="d181e-138">version</span></span>
<span data-ttu-id="d181e-139">Version du package, selon le modèle *version_principale.version_secondaire.version_corrective*.</span><span class="sxs-lookup"><span data-stu-id="d181e-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="d181e-140">Les numéros de version peuvent inclure un suffixe de préversion comme décrit dans [Gestion de versions des packages](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="d181e-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="d181e-141">Description</span><span class="sxs-lookup"><span data-stu-id="d181e-141">description</span></span>
<span data-ttu-id="d181e-142">Description longue du package pour l’affichage de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d181e-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="d181e-143">authors</span><span class="sxs-lookup"><span data-stu-id="d181e-143">authors</span></span>
<span data-ttu-id="d181e-144">Liste séparée par des virgules des auteurs de packages, qui correspondent aux noms de profil sur nuget.org. Ceux-ci sont affichés dans la galerie NuGet sur nuget.org et servent à croiser les références des packages de mêmes auteurs.</span><span class="sxs-lookup"><span data-stu-id="d181e-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="d181e-145">Éléments de métadonnées facultatifs</span><span class="sxs-lookup"><span data-stu-id="d181e-145">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="d181e-146">titre</span><span class="sxs-lookup"><span data-stu-id="d181e-146">title</span></span>
<span data-ttu-id="d181e-147">Titre convivial du package, généralement utilisé dans les affichages de l’interface utilisateur comme sur nuget.org et dans le gestionnaire de package de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d181e-147">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="d181e-148">Si non spécifié, l’ID de package est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d181e-148">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="d181e-149">owners</span><span class="sxs-lookup"><span data-stu-id="d181e-149">owners</span></span>
<span data-ttu-id="d181e-150">Liste des créateurs de packages séparés par des virgules, qui utilisent des noms de profil sur nuget.org. Il s’agit souvent de la même liste que dans `authors` et elle est ignorée lors du chargement du package sur nuget.org. Consultez [Gestion des propriétaires de packages sur nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="d181e-150">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="d181e-151">projectUrl</span><span class="sxs-lookup"><span data-stu-id="d181e-151">projectUrl</span></span>
<span data-ttu-id="d181e-152">URL de la page d’accueil du package, souvent affichée dans l’interface utilisateur ainsi que sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d181e-152">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="d181e-153">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="d181e-153">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="d181e-154">licenseUrl est déconseillé.</span><span class="sxs-lookup"><span data-stu-id="d181e-154">licenseUrl is being deprecated.</span></span> <span data-ttu-id="d181e-155">Utilisez à la place des licences.</span><span class="sxs-lookup"><span data-stu-id="d181e-155">Use license instead.</span></span>

<span data-ttu-id="d181e-156">URL de la licence du package, souvent affichée dans l’interface utilisateur ainsi que sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d181e-156">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="license"></a><span data-ttu-id="d181e-157">licence</span><span class="sxs-lookup"><span data-stu-id="d181e-157">license</span></span>
<span data-ttu-id="d181e-158">Expression de licence SPDX ou chemin d’accès à un fichier de licence dans le package, souvent affiché dans l’interface utilisateur, ainsi que sur nuget.org. Si vous activez votre licence du package sous une licence courants tels que BSD-2-Clause ou MIT, utilisez l’identificateur de licence SPDX associé.</span><span class="sxs-lookup"><span data-stu-id="d181e-158">An SPDX license expression or path to a license file within the package, often shown in UI displays as well as nuget.org. If you’re licensing the package under a common license such as BSD-2-Clause or MIT, use the associated SPDX license identifier.</span></span><br><span data-ttu-id="d181e-159">Par exemple :`<license type="expression">MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="d181e-159">For example: `<license type="expression">MIT</license>`</span></span>

<span data-ttu-id="d181e-160">Voici la liste complète des [identificateurs de licence SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="d181e-160">Here is the complete list of [SPDX license identifiers](https://spdx.org/licenses/).</span></span> <span data-ttu-id="d181e-161">NuGet.org n’accepte que les licences approuvées OSI et FSF avec une expression de type licence.</span><span class="sxs-lookup"><span data-stu-id="d181e-161">NuGet.org accepts only OSI or FSF approved licenses when using license type expression.</span></span>

<span data-ttu-id="d181e-162">Si votre package est concédé sous licence selon plusieurs licences courantes, vous pouvez spécifier une licence composite à l’aide de la [SPDX version 2.0 de la syntaxe expression](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="d181e-162">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span><br><span data-ttu-id="d181e-163">Par exemple :`<license type="expression">BSD-2-Clause OR MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="d181e-163">For example: `<license type="expression">BSD-2-Clause OR MIT</license>`</span></span>

<span data-ttu-id="d181e-164">Si vous utilisez une licence qui n’a pas été attribuée à un identificateur SPDX, ou il s’agit d’une licence personnalisée, vous pouvez empaqueter un fichier (uniquement `.txt` ou `.md`) avec le texte de la licence.</span><span class="sxs-lookup"><span data-stu-id="d181e-164">If you are using a license that hasn’t been assigned an SPDX identifier, or it is a custom license, you can package a file (only `.txt` or `.md`) with the license text.</span></span> <span data-ttu-id="d181e-165">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d181e-165">For example:</span></span>
```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="d181e-166">Pour l’équivalent MSBuild, examinons [une expression de licence ou d’un fichier de licence de livraison](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="d181e-166">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="d181e-167">La syntaxe exacte des expressions de licence de NuGet est décrite ci-dessous dans [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="d181e-167">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="d181e-168">iconUrl</span><span class="sxs-lookup"><span data-stu-id="d181e-168">iconUrl</span></span>
<span data-ttu-id="d181e-169">URL d’une image 64x64 avec un arrière-plan transparent à utiliser comme icône pour le package dans l’affichage de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d181e-169">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="d181e-170">Vérifiez que cet élément contient *l’URL directe de l’image* et non l’URL d’une page web contenant l’image.</span><span class="sxs-lookup"><span data-stu-id="d181e-170">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="d181e-171">Par exemple, pour utiliser une image à partir de GitHub, utilisez le fichier brut comme URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="d181e-171">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="d181e-172">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d181e-172">requireLicenseAcceptance</span></span>
<span data-ttu-id="d181e-173">Valeur booléenne qui spécifie si le client doit inviter l’utilisateur à accepter la licence du package avant d’installer le package.</span><span class="sxs-lookup"><span data-stu-id="d181e-173">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="d181e-174">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="d181e-174">developmentDependency</span></span>
<span data-ttu-id="d181e-175">*(2.8+)* Valeur booléenne qui spécifie si le package doit être marqué comme dépendance de développement uniquement, ce qui l’empêche d’être inclus en tant que dépendance dans d’autres packages.</span><span class="sxs-lookup"><span data-stu-id="d181e-175">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="d181e-176">Avec PackageReference (NuGet 4.8 +), cet indicateur signifie également qu’il exclut les ressources de compilation à partir de la compilation.</span><span class="sxs-lookup"><span data-stu-id="d181e-176">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="d181e-177">Consultez [prise en charge de DevelopmentDependency pour PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="d181e-177">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>
#### <a name="summary"></a><span data-ttu-id="d181e-178">résumé</span><span class="sxs-lookup"><span data-stu-id="d181e-178">summary</span></span>
<span data-ttu-id="d181e-179">Brève description du package pour l’affichage de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d181e-179">A short description of the package for UI display.</span></span> <span data-ttu-id="d181e-180">Si cet élément est omis, une version tronquée de `description` est utilisée.</span><span class="sxs-lookup"><span data-stu-id="d181e-180">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="d181e-181">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="d181e-181">releaseNotes</span></span>
<span data-ttu-id="d181e-182">*(1.5+)* Description des changements apportés à cette version du package, souvent utilisée dans l’interface utilisateur, par exemple sous l’onglet **Mises à jour** du Gestionnaire de package Visual Studio à la place de la description du package.</span><span class="sxs-lookup"><span data-stu-id="d181e-182">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="d181e-183">copyright</span><span class="sxs-lookup"><span data-stu-id="d181e-183">copyright</span></span>
<span data-ttu-id="d181e-184">*(1.5+)* Détails de copyright pour le package.</span><span class="sxs-lookup"><span data-stu-id="d181e-184">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="d181e-185">language</span><span class="sxs-lookup"><span data-stu-id="d181e-185">language</span></span>
<span data-ttu-id="d181e-186">ID de paramètres régionaux du package.</span><span class="sxs-lookup"><span data-stu-id="d181e-186">The locale ID for the package.</span></span> <span data-ttu-id="d181e-187">Consultez [Création de packages localisés](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d181e-187">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="d181e-188">étiquettes</span><span class="sxs-lookup"><span data-stu-id="d181e-188">tags</span></span>
<span data-ttu-id="d181e-189">Liste de balises et de mots clés délimités par des espaces, qui décrivent le package et permettent de découvrir les packages grâce à des fonctions de recherche et de filtrage.</span><span class="sxs-lookup"><span data-stu-id="d181e-189">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="d181e-190">pièce remplaçable par</span><span class="sxs-lookup"><span data-stu-id="d181e-190">serviceable</span></span> 
<span data-ttu-id="d181e-191">*(3.3+)* Uniquement réservé à un usage NuGet interne.</span><span class="sxs-lookup"><span data-stu-id="d181e-191">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="d181e-192">dépôt</span><span class="sxs-lookup"><span data-stu-id="d181e-192">repository</span></span>
<span data-ttu-id="d181e-193">Métadonnées du référentiel, composé de quatre attributs facultatifs : *type* et *url* *(4.0 +)* , et *branche* et  *validation* *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="d181e-193">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="d181e-194">Ces attributs permettent de mapper le fichier .nupkg vers le référentiel qui, générés avec la possibilité d’obtenir aussi détaillée que la branche individuel ou de la validation qui a créé le package.</span><span class="sxs-lookup"><span data-stu-id="d181e-194">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="d181e-195">Ce doit être une url accessible au public qui peut être appelé directement par un logiciel de contrôle de version.</span><span class="sxs-lookup"><span data-stu-id="d181e-195">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="d181e-196">Il ne doit pas être une page html comme cela est destiné à l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d181e-196">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="d181e-197">Pour un lien vers la page de projet, utilisez le `projectUrl` champ, à la place.</span><span class="sxs-lookup"><span data-stu-id="d181e-197">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="d181e-198">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="d181e-198">minClientVersion</span></span>
<span data-ttu-id="d181e-199">Spécifie la version minimale du client NuGet qui peut installer ce package, appliquée par nuget.exe et le gestionnaire de package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d181e-199">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="d181e-200">Cet attribut est utilisé chaque fois que le package dépend de fonctionnalités spécifiques du fichier `.nuspec` qui ont été ajoutées dans une version particulière du client NuGet.</span><span class="sxs-lookup"><span data-stu-id="d181e-200">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="d181e-201">Par exemple, un package utilisant l’attribut `developmentDependency` doit spécifier « 2.8 » pour `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="d181e-201">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="d181e-202">De même, un package utilisant l’élément `contentFiles` (consultez la section suivante) doit affecter à `minClientVersion` la valeur « 3.3 ».</span><span class="sxs-lookup"><span data-stu-id="d181e-202">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="d181e-203">Notez également que, comme les clients NuGet antérieurs à 2.5 ne reconnaissent pas cet indicateur, ils refusent *toujours* d’installer le package, quel que soit le contenu de `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="d181e-203">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="d181e-204">Éléments de collection</span><span class="sxs-lookup"><span data-stu-id="d181e-204">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="d181e-205">packageTypes</span><span class="sxs-lookup"><span data-stu-id="d181e-205">packageTypes</span></span>
<span data-ttu-id="d181e-206">*(3.5+)* Collection de zéro ou plusieurs éléments `<packageType>` spécifiant le type du package s’il est différent du package de dépendances classique.</span><span class="sxs-lookup"><span data-stu-id="d181e-206">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="d181e-207">Chaque élément packageType a des attributs *name* et *version*.</span><span class="sxs-lookup"><span data-stu-id="d181e-207">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="d181e-208">Consultez [Définition d’un type de package](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="d181e-208">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="d181e-209">dépendances</span><span class="sxs-lookup"><span data-stu-id="d181e-209">dependencies</span></span>
<span data-ttu-id="d181e-210">Collection de zéro ou plusieurs éléments `<dependency>` spécifiant les dépendances du package.</span><span class="sxs-lookup"><span data-stu-id="d181e-210">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="d181e-211">Chaque dépendance a des attributs *id*, *version*, *include* (3.x+) et *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="d181e-211">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="d181e-212">Consultez [Dépendances](#dependencies-element) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d181e-212">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="d181e-213">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d181e-213">frameworkAssemblies</span></span>
<span data-ttu-id="d181e-214">*(1.2 +)* Collection de zéro ou plusieurs éléments `<frameworkAssembly>` identifiant les références d’assembly .NET Framework nécessaires à ce package, ce qui garantit que les références sont ajoutées à des projets utilisant le package.</span><span class="sxs-lookup"><span data-stu-id="d181e-214">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="d181e-215">Chaque élément frameworkAssembly a des attributs *assemblyName* et *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="d181e-215">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="d181e-216">Consultez [Références d’assembly Framework](#specifying-framework-assembly-references-gac) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d181e-216">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="d181e-217">Références</span><span class="sxs-lookup"><span data-stu-id="d181e-217">references</span></span>
<span data-ttu-id="d181e-218">*(1.5+)* Collection de zéro ou plusieurs éléments `<reference>` nommant des assemblys dans le dossier `lib` du package qui sont ajoutés en tant que références de projet.</span><span class="sxs-lookup"><span data-stu-id="d181e-218">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="d181e-219">Chaque référence a un attribut *file*.</span><span class="sxs-lookup"><span data-stu-id="d181e-219">Each reference has a *file* attribute.</span></span> <span data-ttu-id="d181e-220">`<references>` peut également contenir un élément `<group>` avec un attribut *targetFramework* qui contient à son tour des éléments `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="d181e-220">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="d181e-221">Si cet élément est omis, toutes les références dans `lib` sont incluses.</span><span class="sxs-lookup"><span data-stu-id="d181e-221">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="d181e-222">Consultez [Références d’assembly explicite](#specifying-explicit-assembly-references) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d181e-222">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="d181e-223">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d181e-223">contentFiles</span></span>
<span data-ttu-id="d181e-224">*(3.3+)* Collection d’éléments `<files>` qui identifient les fichiers de contenu à inclure dans le projet de consommation.</span><span class="sxs-lookup"><span data-stu-id="d181e-224">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="d181e-225">Ces fichiers sont spécifiés avec un ensemble d’attributs qui décrivent comment ils doivent être utilisés dans le système de projet.</span><span class="sxs-lookup"><span data-stu-id="d181e-225">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="d181e-226">Consultez [Inclusion des fichiers d’assembly](#specifying-files-to-include-in-the-package) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d181e-226">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="d181e-227">fichiers</span><span class="sxs-lookup"><span data-stu-id="d181e-227">files</span></span> 
<span data-ttu-id="d181e-228">Le `<package>` nœud peut contenir un `<files>` nœud en tant que frère à `<metadata>`et un `<contentFiles>` enfant sous `<metadata>`, pour spécifier les fichiers d’assembly et le contenu à inclure dans le package.</span><span class="sxs-lookup"><span data-stu-id="d181e-228">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="d181e-229">Consultez [Inclusion des fichiers d’assembly](#including-assembly-files) et [Inclusion des fichiers de contenu](#including-content-files) plus loin dans cette rubrique pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d181e-229">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="d181e-230">Jetons de remplacement</span><span class="sxs-lookup"><span data-stu-id="d181e-230">Replacement tokens</span></span>

<span data-ttu-id="d181e-231">Lors de la création d’un package, la [commande `nuget pack`](../tools/cli-ref-pack.md) remplace les jetons séparés par des $ dans le nœud `<metadata>` du fichier `.nuspec` par des valeurs provenant d’un fichier projet ou du commutateur `-properties` de la commande `pack`.</span><span class="sxs-lookup"><span data-stu-id="d181e-231">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="d181e-232">Sur la ligne de commande, vous spécifiez des valeurs de jeton avec `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="d181e-232">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="d181e-233">Par exemple, vous pouvez utiliser un jeton tel que `$owners$` et `$desc$` dans le fichier `.nuspec` et fournir les valeurs au moment de la compression comme suit :</span><span class="sxs-lookup"><span data-stu-id="d181e-233">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="d181e-234">Pour utiliser les valeurs à partir d’un projet, spécifiez les jetons décrits dans le tableau ci-dessous (AssemblyInfo fait référence au fichier dans `Properties` comme `AssemblyInfo.cs` ou `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="d181e-234">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="d181e-235">Pour utiliser ces jetons, exécutez `nuget pack` avec le fichier projet et non simplement le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d181e-235">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="d181e-236">Par exemple, quand vous utilisez la commande suivante, les jetons `$id$` et `$version$` dans un fichier `.nuspec` sont remplacés par les valeurs `AssemblyName` et `AssemblyVersion` du projet :</span><span class="sxs-lookup"><span data-stu-id="d181e-236">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="d181e-237">En général, quand vous avez un projet, vous créez le fichier `.nuspec` initialement à l’aide de `nuget spec MyProject.csproj` qui inclut automatiquement certains de ces jetons standard.</span><span class="sxs-lookup"><span data-stu-id="d181e-237">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="d181e-238">Toutefois, si un projet ne possède pas de valeurs pour les éléments `.nuspec` requis, `nuget pack` échoue.</span><span class="sxs-lookup"><span data-stu-id="d181e-238">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="d181e-239">De plus, si vous modifiez des valeurs de projet, veillez à regénérer avant de créer le package ; pour effectuer cette opération en toute facilité, utilisez le commutateur `build` de la commande pack.</span><span class="sxs-lookup"><span data-stu-id="d181e-239">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="d181e-240">À l’exception de `$configuration$`, les valeurs dans le projet sont préférées à celles affectées au même jeton sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d181e-240">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="d181e-241">Token</span><span class="sxs-lookup"><span data-stu-id="d181e-241">Token</span></span> | <span data-ttu-id="d181e-242">Source de valeur</span><span class="sxs-lookup"><span data-stu-id="d181e-242">Value source</span></span> | <span data-ttu-id="d181e-243">Value</span><span class="sxs-lookup"><span data-stu-id="d181e-243">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="d181e-244">**$id$**</span><span class="sxs-lookup"><span data-stu-id="d181e-244">**$id$**</span></span> | <span data-ttu-id="d181e-245">Fichier projet</span><span class="sxs-lookup"><span data-stu-id="d181e-245">Project file</span></span> | <span data-ttu-id="d181e-246">AssemblyName (titre) à partir du fichier de projet</span><span class="sxs-lookup"><span data-stu-id="d181e-246">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="d181e-247">**$version$**</span><span class="sxs-lookup"><span data-stu-id="d181e-247">**$version$**</span></span> | <span data-ttu-id="d181e-248">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d181e-248">AssemblyInfo</span></span> | <span data-ttu-id="d181e-249">AssemblyInformationalVersion si présente, sinon AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="d181e-249">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="d181e-250">**$author$**</span><span class="sxs-lookup"><span data-stu-id="d181e-250">**$author$**</span></span> | <span data-ttu-id="d181e-251">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d181e-251">AssemblyInfo</span></span> | <span data-ttu-id="d181e-252">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="d181e-252">AssemblyCompany</span></span> |
| <span data-ttu-id="d181e-253">**$title$**</span><span class="sxs-lookup"><span data-stu-id="d181e-253">**$title$**</span></span> | <span data-ttu-id="d181e-254">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d181e-254">AssemblyInfo</span></span> | <span data-ttu-id="d181e-255">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="d181e-255">AssemblyTitle</span></span> |
| <span data-ttu-id="d181e-256">**$description$**</span><span class="sxs-lookup"><span data-stu-id="d181e-256">**$description$**</span></span> | <span data-ttu-id="d181e-257">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d181e-257">AssemblyInfo</span></span> | <span data-ttu-id="d181e-258">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="d181e-258">AssemblyDescription</span></span> |
| <span data-ttu-id="d181e-259">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="d181e-259">**$copyright$**</span></span> | <span data-ttu-id="d181e-260">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d181e-260">AssemblyInfo</span></span> | <span data-ttu-id="d181e-261">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="d181e-261">AssemblyCopyright</span></span> |
| <span data-ttu-id="d181e-262">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="d181e-262">**$configuration$**</span></span> | <span data-ttu-id="d181e-263">DLL d’assembly</span><span class="sxs-lookup"><span data-stu-id="d181e-263">Assembly DLL</span></span> | <span data-ttu-id="d181e-264">Configuration utilisée pour générer l’assembly, Debug étant la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="d181e-264">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="d181e-265">Notez que, pour créer un package à l’aide d’une configuration Release, vous utilisez toujours `-properties Configuration=Release` sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d181e-265">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="d181e-266">Les jetons peuvent également être utilisés pour résoudre les chemins quand vous incluez des [fichiers d’assembly](#including-assembly-files) et [fichiers de contenu](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="d181e-266">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="d181e-267">Les jetons ont les mêmes noms que les propriétés MSBuild, ce qui permet de sélectionner les fichiers à inclure en fonction de la configuration de build actuelle.</span><span class="sxs-lookup"><span data-stu-id="d181e-267">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="d181e-268">Par exemple, si vous utilisez les jetons suivants dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="d181e-268">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="d181e-269">Et que vous générez un assembly dont `AssemblyName` est `LoggingLibrary` avec la configuration `Release` dans MSBuild, les lignes résultantes dans le fichier `.nuspec` du package sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d181e-269">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="d181e-270">Élément de dépendances</span><span class="sxs-lookup"><span data-stu-id="d181e-270">Dependencies element</span></span>

<span data-ttu-id="d181e-271">L’élément `<dependencies>` dans `<metadata>` contient un nombre quelconque d’éléments `<dependency>` qui identifient d’autres packages dont dépend le package de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="d181e-271">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="d181e-272">Les attributs pour chaque élément `<dependency>` sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="d181e-272">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="d181e-273">Attribut</span><span class="sxs-lookup"><span data-stu-id="d181e-273">Attribute</span></span> | <span data-ttu-id="d181e-274">Description</span><span class="sxs-lookup"><span data-stu-id="d181e-274">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="d181e-275">(Obligatoire) ID de package de la dépendance, tel que « EntityFramework » et « NUnit », qui est le nom du package nuget.org affiché sur une page de package.</span><span class="sxs-lookup"><span data-stu-id="d181e-275">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="d181e-276">(Obligatoire) Plage de versions acceptables en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="d181e-276">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="d181e-277">Consultez [Gestion de versions des packages](../reference/package-versioning.md#version-ranges-and-wildcards) pour connaître la syntaxe exacte.</span><span class="sxs-lookup"><span data-stu-id="d181e-277">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="d181e-278">include</span><span class="sxs-lookup"><span data-stu-id="d181e-278">include</span></span> | <span data-ttu-id="d181e-279">Liste de balises include/exclude séparées par des virgules (voir ci-dessous) indiquant la dépendance à inclure dans le package final.</span><span class="sxs-lookup"><span data-stu-id="d181e-279">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="d181e-280">La valeur par défaut est `all`.</span><span class="sxs-lookup"><span data-stu-id="d181e-280">The default value is `all`.</span></span> |
| <span data-ttu-id="d181e-281">exclude</span><span class="sxs-lookup"><span data-stu-id="d181e-281">exclude</span></span> | <span data-ttu-id="d181e-282">Liste de balises include/exclude séparées par des virgules (voir ci-dessous) indiquant la dépendance à exclure dans le package final.</span><span class="sxs-lookup"><span data-stu-id="d181e-282">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="d181e-283">La valeur par défaut est `build,analyzers` qui peut être remplacé.</span><span class="sxs-lookup"><span data-stu-id="d181e-283">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="d181e-284">Mais `content/ ContentFiles` sont également implicitement exclus dans le package final qui ne peut pas être remplacé.</span><span class="sxs-lookup"><span data-stu-id="d181e-284">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="d181e-285">Les balises spécifiées avec `exclude` sont prioritaires sur celles spécifiées avec `include`.</span><span class="sxs-lookup"><span data-stu-id="d181e-285">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="d181e-286">Par exemple, `include="runtime, compile" exclude="compile"` est identique à `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="d181e-286">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="d181e-287">Balise include/exclude</span><span class="sxs-lookup"><span data-stu-id="d181e-287">Include/Exclude tag</span></span> | <span data-ttu-id="d181e-288">Dossiers affectés de la cible</span><span class="sxs-lookup"><span data-stu-id="d181e-288">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="d181e-289">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d181e-289">contentFiles</span></span> | <span data-ttu-id="d181e-290">Contenu</span><span class="sxs-lookup"><span data-stu-id="d181e-290">Content</span></span> |
| <span data-ttu-id="d181e-291">runtime</span><span class="sxs-lookup"><span data-stu-id="d181e-291">runtime</span></span> | <span data-ttu-id="d181e-292">Runtime, Resources et FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d181e-292">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="d181e-293">compile</span><span class="sxs-lookup"><span data-stu-id="d181e-293">compile</span></span> | <span data-ttu-id="d181e-294">lib</span><span class="sxs-lookup"><span data-stu-id="d181e-294">lib</span></span> |
| <span data-ttu-id="d181e-295">build</span><span class="sxs-lookup"><span data-stu-id="d181e-295">build</span></span> | <span data-ttu-id="d181e-296">build (propriétés et cibles MSBuild)</span><span class="sxs-lookup"><span data-stu-id="d181e-296">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="d181e-297">native</span><span class="sxs-lookup"><span data-stu-id="d181e-297">native</span></span> | <span data-ttu-id="d181e-298">native</span><span class="sxs-lookup"><span data-stu-id="d181e-298">native</span></span> |
| <span data-ttu-id="d181e-299">none</span><span class="sxs-lookup"><span data-stu-id="d181e-299">none</span></span> | <span data-ttu-id="d181e-300">Aucun dossier</span><span class="sxs-lookup"><span data-stu-id="d181e-300">No folders</span></span> |
| <span data-ttu-id="d181e-301">all</span><span class="sxs-lookup"><span data-stu-id="d181e-301">all</span></span> | <span data-ttu-id="d181e-302">Tous les dossiers</span><span class="sxs-lookup"><span data-stu-id="d181e-302">All folders</span></span> |

<span data-ttu-id="d181e-303">Par exemple, les lignes suivantes indiquent les dépendances sur `PackageA` version 1.1.0 ou ultérieure, et `PackageB` version 1.x.</span><span class="sxs-lookup"><span data-stu-id="d181e-303">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="d181e-304">Les lignes suivantes indiquent les dépendances sur les mêmes packages, mais spécifient d’inclure les dossiers `contentFiles` et `build` de `PackageA` et tous les éléments sauf les dossiers `native` et `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="d181e-304">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="d181e-305">Remarque : Lorsque vous créez un `.nuspec` à partir d’un projet `nuget spec`, dépendances qui existent dans le projet sont automatiquement incluses dans résultant `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="d181e-305">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="d181e-306">Groupes de dépendances</span><span class="sxs-lookup"><span data-stu-id="d181e-306">Dependency groups</span></span>

<span data-ttu-id="d181e-307">*Version 2.0+*</span><span class="sxs-lookup"><span data-stu-id="d181e-307">*Version 2.0+*</span></span>

<span data-ttu-id="d181e-308">Comme alternative à une liste plate unique, les dépendances peuvent être spécifiées selon le profil de framework du projet cible avec les éléments `<group>` dans `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="d181e-308">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="d181e-309">Chaque groupe possède un attribut nommé `targetFramework` et contient zéro ou plusieurs éléments `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="d181e-309">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="d181e-310">Ces dépendances sont installées ensemble quand la version cible de .NET Framework est compatible avec le profil de framework du projet.</span><span class="sxs-lookup"><span data-stu-id="d181e-310">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d181e-311">L’élément `<group>` sans un attribut `targetFramework` est utilisé comme valeur par défaut ou liste de secours de dépendances.</span><span class="sxs-lookup"><span data-stu-id="d181e-311">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="d181e-312">Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts.</span><span class="sxs-lookup"><span data-stu-id="d181e-312">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d181e-313">Le format de groupe ne peut pas être mélangé avec une liste plate.</span><span class="sxs-lookup"><span data-stu-id="d181e-313">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d181e-314">L’exemple suivant illustre différentes variantes de l’élément `<group>` :</span><span class="sxs-lookup"><span data-stu-id="d181e-314">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="d181e-315">Références d’assembly explicite</span><span class="sxs-lookup"><span data-stu-id="d181e-315">Explicit assembly references</span></span>

<span data-ttu-id="d181e-316">Le `<references>` élément est utilisé par les projets à l’aide de `packages.config` pour spécifier explicitement les assemblys que le projet cible doit référencer lors de l’utilisation du package.</span><span class="sxs-lookup"><span data-stu-id="d181e-316">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="d181e-317">Des références explicites sont généralement utilisées pour les assemblys uniquement au moment du design.</span><span class="sxs-lookup"><span data-stu-id="d181e-317">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="d181e-318">Pour plus d’informations, consultez la page sur [en sélectionnant les assemblys référencés par les projets](../create-packages/select-assemblies-referenced-by-projects.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d181e-318">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="d181e-319">Par exemple, l’élément `<references>` suivant demande à NuGet d’ajouter des références à `xunit.dll` et `xunit.extensions.dll` uniquement même s’il existe d’autres assemblys dans le package :</span><span class="sxs-lookup"><span data-stu-id="d181e-319">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="d181e-320">Groupes de référence</span><span class="sxs-lookup"><span data-stu-id="d181e-320">Reference groups</span></span>

<span data-ttu-id="d181e-321">Comme alternative à une liste plate unique, les références peuvent être spécifiées selon le profil de framework du projet cible avec les éléments `<group>` dans `<references>`.</span><span class="sxs-lookup"><span data-stu-id="d181e-321">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="d181e-322">Chaque groupe possède un attribut nommé `targetFramework` et contient zéro ou plusieurs éléments `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="d181e-322">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="d181e-323">Ces références sont ajoutées à un projet quand la version cible de .NET Framework est compatible avec le profil de framework du projet.</span><span class="sxs-lookup"><span data-stu-id="d181e-323">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d181e-324">L’élément `<group>` sans un attribut `targetFramework` est utilisé comme valeur par défaut ou liste de secours de références.</span><span class="sxs-lookup"><span data-stu-id="d181e-324">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="d181e-325">Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts.</span><span class="sxs-lookup"><span data-stu-id="d181e-325">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d181e-326">Le format de groupe ne peut pas être mélangé avec une liste plate.</span><span class="sxs-lookup"><span data-stu-id="d181e-326">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d181e-327">L’exemple suivant illustre différentes variantes de l’élément `<group>` :</span><span class="sxs-lookup"><span data-stu-id="d181e-327">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="d181e-328">Références d’assembly Framework</span><span class="sxs-lookup"><span data-stu-id="d181e-328">Framework assembly references</span></span>

<span data-ttu-id="d181e-329">Les assemblys Framework sont ceux qui font partie du .NET Framework et doivent déjà figurer dans le GAC (Global Assembly Cache) pour un ordinateur donné.</span><span class="sxs-lookup"><span data-stu-id="d181e-329">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="d181e-330">En identifiant ces assemblys dans l’élément `<frameworkAssemblies>`, un package peut garantir que les références requises sont ajoutées à un projet si le projet ne dispose pas déjà de telles références.</span><span class="sxs-lookup"><span data-stu-id="d181e-330">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="d181e-331">Ces assemblys, bien entendu, ne sont pas directement inclus dans un package.</span><span class="sxs-lookup"><span data-stu-id="d181e-331">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="d181e-332">L’élément `<frameworkAssemblies>` contient zéro ou plusieurs éléments `<frameworkAssembly>`, chacun d’eux spécifiant les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="d181e-332">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="d181e-333">Attribut</span><span class="sxs-lookup"><span data-stu-id="d181e-333">Attribute</span></span> | <span data-ttu-id="d181e-334">Description</span><span class="sxs-lookup"><span data-stu-id="d181e-334">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d181e-335">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="d181e-335">**assemblyName**</span></span> | <span data-ttu-id="d181e-336">(Obligatoire) Nom d’assembly qualifié complet.</span><span class="sxs-lookup"><span data-stu-id="d181e-336">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="d181e-337">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="d181e-337">**targetFramework**</span></span> | <span data-ttu-id="d181e-338">(Facultatif) Spécifie la version cible de .NET Framework à laquelle s’applique cette référence.</span><span class="sxs-lookup"><span data-stu-id="d181e-338">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="d181e-339">Si cet attribut est omis, indique que la référence s’applique à tous les frameworks.</span><span class="sxs-lookup"><span data-stu-id="d181e-339">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="d181e-340">Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts.</span><span class="sxs-lookup"><span data-stu-id="d181e-340">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="d181e-341">L’exemple suivant montre une référence à `System.Net` pour toutes les versions cibles de .NET Framework et une référence à `System.ServiceModel` pour .NET Framework 4.0 uniquement :</span><span class="sxs-lookup"><span data-stu-id="d181e-341">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="d181e-342">Inclusion des fichiers d’assembly</span><span class="sxs-lookup"><span data-stu-id="d181e-342">Including assembly files</span></span>

<span data-ttu-id="d181e-343">Si vous suivez les conventions décrites dans [Création d’un package](../create-packages/creating-a-package.md), il est inutile de spécifier explicitement une liste de fichiers dans le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d181e-343">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="d181e-344">La commande `nuget pack` sélectionne automatiquement les fichiers nécessaires.</span><span class="sxs-lookup"><span data-stu-id="d181e-344">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="d181e-345">Quand un package est installé dans un projet, NuGet ajoute automatiquement des références d’assembly aux DLL du package, *à l’exclusion* de celles nommées `.resources.dll`, car elles sont supposées être des assemblys satellites localisés.</span><span class="sxs-lookup"><span data-stu-id="d181e-345">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="d181e-346">C’est pourquoi vous devez éviter d’utiliser `.resources.dll` pour les fichiers qui contiennent du code de package essentiel.</span><span class="sxs-lookup"><span data-stu-id="d181e-346">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="d181e-347">Pour ignorer ce comportement automatique et contrôler explicitement les fichiers qui sont inclus dans un package, placez un élément `<files>` en tant qu’enfant de `<package>` (et frère de `<metadata>`), identifiant chaque fichier avec un élément `<file>` distinct.</span><span class="sxs-lookup"><span data-stu-id="d181e-347">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="d181e-348">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d181e-348">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="d181e-349">Avec NuGet 2.x et versions antérieures, et des projets utilisant `packages.config`, l’élément `<files>` est également utilisé pour inclure les fichiers de contenu non modifiables quand un package est installé.</span><span class="sxs-lookup"><span data-stu-id="d181e-349">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="d181e-350">Avec NuGet 3.3+ et les projets PackageReference, l’élément `<contentFiles>` est utilisé à la place.</span><span class="sxs-lookup"><span data-stu-id="d181e-350">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="d181e-351">Consultez [Inclusion des fichiers de contenu](#including-content-files) ci-dessous pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d181e-351">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="d181e-352">Attributs des éléments File</span><span class="sxs-lookup"><span data-stu-id="d181e-352">File element attributes</span></span>

<span data-ttu-id="d181e-353">Chaque élément `<file>` spécifie les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="d181e-353">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="d181e-354">Attribut</span><span class="sxs-lookup"><span data-stu-id="d181e-354">Attribute</span></span> | <span data-ttu-id="d181e-355">Description</span><span class="sxs-lookup"><span data-stu-id="d181e-355">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d181e-356">**src**</span><span class="sxs-lookup"><span data-stu-id="d181e-356">**src**</span></span> | <span data-ttu-id="d181e-357">Emplacement du ou des fichiers à inclure, soumis à des exclusions définies par l’attribut `exclude`.</span><span class="sxs-lookup"><span data-stu-id="d181e-357">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d181e-358">Le chemin est relatif au fichier `.nuspec` sauf si un chemin absolu est spécifié.</span><span class="sxs-lookup"><span data-stu-id="d181e-358">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d181e-359">Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive.</span><span class="sxs-lookup"><span data-stu-id="d181e-359">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d181e-360">**target**</span><span class="sxs-lookup"><span data-stu-id="d181e-360">**target**</span></span> | <span data-ttu-id="d181e-361">Chemin relatif vers le dossier dans le package où les fichiers sources sont placés, qui doit commencer par `lib`, `content`, `build` ou `tools`.</span><span class="sxs-lookup"><span data-stu-id="d181e-361">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="d181e-362">Consultez [Création d’un fichier .nuspec à partir d’un répertoire de travail basé sur une convention](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="d181e-362">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="d181e-363">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d181e-363">**exclude**</span></span> | <span data-ttu-id="d181e-364">Liste de fichiers ou de modèles de fichiers séparés par un point-virgule à exclure de l’emplacement `src`.</span><span class="sxs-lookup"><span data-stu-id="d181e-364">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d181e-365">Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive.</span><span class="sxs-lookup"><span data-stu-id="d181e-365">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="d181e-366">Exemples</span><span class="sxs-lookup"><span data-stu-id="d181e-366">Examples</span></span>

<span data-ttu-id="d181e-367">**Assembly unique**</span><span class="sxs-lookup"><span data-stu-id="d181e-367">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="d181e-368">**Assembly unique spécifique à une version cible de .NET Framework**</span><span class="sxs-lookup"><span data-stu-id="d181e-368">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="d181e-369">**Ensemble de DLL avec un caractère générique**</span><span class="sxs-lookup"><span data-stu-id="d181e-369">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="d181e-370">**DLL de différents frameworks**</span><span class="sxs-lookup"><span data-stu-id="d181e-370">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="d181e-371">**Exclusion de fichiers**</span><span class="sxs-lookup"><span data-stu-id="d181e-371">**Excluding files**</span></span>

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="d181e-372">Inclusion des fichiers de contenu</span><span class="sxs-lookup"><span data-stu-id="d181e-372">Including content files</span></span>

<span data-ttu-id="d181e-373">Les fichiers de contenu sont des fichiers non modifiables qu’un package doit inclure dans un projet.</span><span class="sxs-lookup"><span data-stu-id="d181e-373">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="d181e-374">Comme ils ne sont pas modifiables, ils ne sont pas destinés à être changés par le projet de consommation.</span><span class="sxs-lookup"><span data-stu-id="d181e-374">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="d181e-375">Des exemples de fichiers de contenu sont notamment :</span><span class="sxs-lookup"><span data-stu-id="d181e-375">Example content files include:</span></span>

- <span data-ttu-id="d181e-376">Images incorporées en tant que ressources</span><span class="sxs-lookup"><span data-stu-id="d181e-376">Images that are embedded as resources</span></span>
- <span data-ttu-id="d181e-377">Fichiers sources qui sont déjà compilés</span><span class="sxs-lookup"><span data-stu-id="d181e-377">Source files that are already compiled</span></span>
- <span data-ttu-id="d181e-378">Scripts qui doivent être inclus avec la sortie de génération du projet</span><span class="sxs-lookup"><span data-stu-id="d181e-378">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="d181e-379">Fichiers de configuration pour le package qui doivent être inclus dans le projet, mais ne nécessitent aucune modification spécifique au projet</span><span class="sxs-lookup"><span data-stu-id="d181e-379">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="d181e-380">Les fichiers de contenu sont inclus dans un package à l’aide de l’élément `<files>`, en spécifiant le dossier `content` dans l’attribut `target`.</span><span class="sxs-lookup"><span data-stu-id="d181e-380">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="d181e-381">Toutefois, ces fichiers sont ignorés quand le package est installé dans un projet utilisant PackageReference, qui utilise à la place l’élément `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="d181e-381">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="d181e-382">Pour une compatibilité maximale avec les projets de consommation, un package spécifie dans l’idéal les fichiers de contenu dans les deux éléments.</span><span class="sxs-lookup"><span data-stu-id="d181e-382">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="d181e-383">Utilisation de l’élément files pour les fichiers de contenu</span><span class="sxs-lookup"><span data-stu-id="d181e-383">Using the files element for content files</span></span>

<span data-ttu-id="d181e-384">Pour les fichiers de contenu, utilisez simplement le même format que pour les fichiers d’assembly, mais spécifiez `content` comme dossier de base dans l’attribut `target` comme indiqué dans les exemples suivants.</span><span class="sxs-lookup"><span data-stu-id="d181e-384">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="d181e-385">**Fichiers de contenu de base**</span><span class="sxs-lookup"><span data-stu-id="d181e-385">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="d181e-386">**Fichiers de contenu avec structure de répertoires**</span><span class="sxs-lookup"><span data-stu-id="d181e-386">**Content files with directory structure**</span></span>

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

<span data-ttu-id="d181e-387">**Fichier de contenu spécifique à une version cible de .NET Framework**</span><span class="sxs-lookup"><span data-stu-id="d181e-387">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="d181e-388">**Fichier de contenu copié vers un dossier avec un point dans le nom**</span><span class="sxs-lookup"><span data-stu-id="d181e-388">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="d181e-389">Dans ce cas, NuGet détecte que l’extension dans `target` ne correspond pas à l’extension dans `src` et traite par conséquent cette partie du nom dans `target` en tant que dossier :</span><span class="sxs-lookup"><span data-stu-id="d181e-389">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="d181e-390">**Fichiers de contenu sans extensions**</span><span class="sxs-lookup"><span data-stu-id="d181e-390">**Content files without extensions**</span></span>

<span data-ttu-id="d181e-391">Pour inclure les fichiers sans extension, utilisez les caractères génériques `*` ou `**` :</span><span class="sxs-lookup"><span data-stu-id="d181e-391">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="d181e-392">**Fichiers de contenu avec chemin complet et cible complète**</span><span class="sxs-lookup"><span data-stu-id="d181e-392">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="d181e-393">Dans ce cas, étant donné que les extensions de fichier de la source et de la cible correspondent, NuGet part du principe que la cible est un nom de fichier et non un dossier :</span><span class="sxs-lookup"><span data-stu-id="d181e-393">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="d181e-394">**Modification du nom d’un fichier de contenu dans le package**</span><span class="sxs-lookup"><span data-stu-id="d181e-394">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="d181e-395">**Exclusion de fichiers**</span><span class="sxs-lookup"><span data-stu-id="d181e-395">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="d181e-396">Utilisation de l’élément contentFiles pour les fichiers de contenu</span><span class="sxs-lookup"><span data-stu-id="d181e-396">Using the contentFiles element for content files</span></span>

<span data-ttu-id="d181e-397">*NuGet 4.0 + avec PackageReference*</span><span class="sxs-lookup"><span data-stu-id="d181e-397">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="d181e-398">Par défaut, un package place le contenu dans un dossier `contentFiles` (voir ci-dessous) et `nuget pack` a mis tous les fichiers dans ce dossier à l’aide des attributs par défaut.</span><span class="sxs-lookup"><span data-stu-id="d181e-398">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="d181e-399">Dans ce cas, il n’est pas du tout nécessaire d’inclure un nœud `contentFiles` dans le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d181e-399">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="d181e-400">Pour contrôler les fichiers qui sont inclus, l’élément `<contentFiles>` spécifie une collection d’éléments `<files>` qui identifient exactement les fichiers à ajouter.</span><span class="sxs-lookup"><span data-stu-id="d181e-400">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="d181e-401">Ces fichiers sont spécifiés avec un ensemble d’attributs qui décrivent comment ils doivent être utilisés dans le système de projet :</span><span class="sxs-lookup"><span data-stu-id="d181e-401">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="d181e-402">Attribut</span><span class="sxs-lookup"><span data-stu-id="d181e-402">Attribute</span></span> | <span data-ttu-id="d181e-403">Description</span><span class="sxs-lookup"><span data-stu-id="d181e-403">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d181e-404">**include**</span><span class="sxs-lookup"><span data-stu-id="d181e-404">**include**</span></span> | <span data-ttu-id="d181e-405">(Obligatoire) Emplacement du ou des fichiers à inclure, soumis à des exclusions définies par l’attribut `exclude`.</span><span class="sxs-lookup"><span data-stu-id="d181e-405">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d181e-406">Le chemin est relatif au fichier `.nuspec` sauf si un chemin absolu est spécifié.</span><span class="sxs-lookup"><span data-stu-id="d181e-406">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d181e-407">Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive.</span><span class="sxs-lookup"><span data-stu-id="d181e-407">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d181e-408">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d181e-408">**exclude**</span></span> | <span data-ttu-id="d181e-409">Liste de fichiers ou de modèles de fichiers séparés par un point-virgule à exclure de l’emplacement `src`.</span><span class="sxs-lookup"><span data-stu-id="d181e-409">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d181e-410">Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive.</span><span class="sxs-lookup"><span data-stu-id="d181e-410">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d181e-411">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="d181e-411">**buildAction**</span></span> | <span data-ttu-id="d181e-412">Action de génération à affecter à l’élément de contenu pour MSBuild, comme `Content`, `None`, `Embedded Resource`, `Compile`, etc. La valeur par défaut est `Compile`.</span><span class="sxs-lookup"><span data-stu-id="d181e-412">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="d181e-413">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="d181e-413">**copyToOutput**</span></span> | <span data-ttu-id="d181e-414">Valeur booléenne indiquant s’il faut copier des éléments de contenu à la build (ou publiez) dossier de sortie.</span><span class="sxs-lookup"><span data-stu-id="d181e-414">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="d181e-415">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="d181e-415">The default is false.</span></span> |
| <span data-ttu-id="d181e-416">**flatten**</span><span class="sxs-lookup"><span data-stu-id="d181e-416">**flatten**</span></span> | <span data-ttu-id="d181e-417">Valeur booléenne indiquant s’il faut copier des éléments de contenu dans un dossier unique dans la sortie de génération (true) ou conserver la structure de dossiers dans le package (false).</span><span class="sxs-lookup"><span data-stu-id="d181e-417">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="d181e-418">Cet indicateur fonctionne uniquement lorsque l’indicateur copyToOutput est défini sur true.</span><span class="sxs-lookup"><span data-stu-id="d181e-418">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="d181e-419">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="d181e-419">The default is false.</span></span> |

<span data-ttu-id="d181e-420">Lors de l’installation d’un package, NuGet applique les éléments enfants de `<contentFiles>` de haut en bas.</span><span class="sxs-lookup"><span data-stu-id="d181e-420">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="d181e-421">Si plusieurs entrées correspondent au même fichier, toutes les entrées sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="d181e-421">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="d181e-422">L’entrée supérieure remplace les entrées inférieures s’il existe un conflit pour le même attribut.</span><span class="sxs-lookup"><span data-stu-id="d181e-422">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="d181e-423">Structure de dossiers de package</span><span class="sxs-lookup"><span data-stu-id="d181e-423">Package folder structure</span></span>

<span data-ttu-id="d181e-424">Le projet de package doit structurer le contenu à l’aide du modèle suivant :</span><span class="sxs-lookup"><span data-stu-id="d181e-424">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="d181e-425">`codeLanguages` peut être `cs`, `vb`, `fs`, `any`, ou l’équivalent en minuscules d’un élément `$(ProjectLanguage)` donné.</span><span class="sxs-lookup"><span data-stu-id="d181e-425">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="d181e-426">`TxM` est n’importe quel moniker du Framework cible légal pris en charge par NuGet (consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="d181e-426">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="d181e-427">Toute structure de dossiers peut être ajoutée à la fin de cette syntaxe.</span><span class="sxs-lookup"><span data-stu-id="d181e-427">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="d181e-428">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d181e-428">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="d181e-429">Les dossiers vides peuvent utiliser `.` pour choisir de ne pas fournir de contenu pour certaines combinaisons de langage et TxM, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d181e-429">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="d181e-430">Exemple de section contentFiles</span><span class="sxs-lookup"><span data-stu-id="d181e-430">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="d181e-431">Exemples de fichiers nuspec</span><span class="sxs-lookup"><span data-stu-id="d181e-431">Example nuspec files</span></span>

<span data-ttu-id="d181e-432">**Fichier `.nuspec` simple qui ne spécifie pas de dépendances ni de fichiers**</span><span class="sxs-lookup"><span data-stu-id="d181e-432">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="d181e-433">**Fichier `.nuspec` avec des dépendances**</span><span class="sxs-lookup"><span data-stu-id="d181e-433">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="d181e-434">**Fichier `.nuspec` avec des fichiers**</span><span class="sxs-lookup"><span data-stu-id="d181e-434">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="d181e-435">**Fichier `.nuspec` avec des assemblys Framework**</span><span class="sxs-lookup"><span data-stu-id="d181e-435">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="d181e-436">Dans cet exemple, les éléments suivants sont installés pour les cibles de projets spécifiques :</span><span class="sxs-lookup"><span data-stu-id="d181e-436">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="d181e-437">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d181e-437">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="d181e-438">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d181e-438">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="d181e-439">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="d181e-439">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="d181e-440">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="d181e-440">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
