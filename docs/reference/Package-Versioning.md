---
title: Référence de Version de Package NuGet
description: Détails exacts sur la spécification des numéros de version et de plages pour d’autres packages qui dépend d’un package NuGet, et comment les dépendances sont installées.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: d1da26b55c2c273c15c9c16891bf44abffd160a5
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/22/2018
---
# <a name="package-versioning"></a><span data-ttu-id="45a67-103">Contrôle de version des packages</span><span class="sxs-lookup"><span data-stu-id="45a67-103">Package versioning</span></span>

<span data-ttu-id="45a67-104">Un package spécifique est toujours appelée à l’aide de son identificateur de package et un numéro de version exact.</span><span class="sxs-lookup"><span data-stu-id="45a67-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="45a67-105">Par exemple, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sur nuget.org a plusieurs dizaines des packages spécifiques disponibles, allant de version *4.1.10311* vers la version *6.1.3* (la dernière stable version) et les diverses versions préliminaires telles que *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="45a67-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="45a67-106">Lorsque vous créez un package, vous assignez un numéro de version spécifique avec un suffixe facultatif en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="45a67-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="45a67-107">En revanche, lors de l’utilisation de packages, vous pouvez spécifier un numéro de version exacte ou d’une plage de versions acceptables.</span><span class="sxs-lookup"><span data-stu-id="45a67-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="45a67-108">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="45a67-108">In this topic:</span></span>

- <span data-ttu-id="45a67-109">[Principes de base version](#version-basics) , y compris les suffixes de la version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="45a67-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="45a67-110">Les caractères génériques et les plages de versions</span><span class="sxs-lookup"><span data-stu-id="45a67-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="45a67-111">Numéros de version normalisée</span><span class="sxs-lookup"><span data-stu-id="45a67-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="45a67-112">Principes fondamentaux de version</span><span class="sxs-lookup"><span data-stu-id="45a67-112">Version basics</span></span>

<span data-ttu-id="45a67-113">Un numéro de version est au format *majeure.mineure.correctif [-suffixe]*, où les composants ont les significations suivantes :</span><span class="sxs-lookup"><span data-stu-id="45a67-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="45a67-114">*Principaux*: modifications avec rupture</span><span class="sxs-lookup"><span data-stu-id="45a67-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="45a67-115">*Secondaire*: nouvelles fonctionnalités, mais offre une compatibilité descendante</span><span class="sxs-lookup"><span data-stu-id="45a67-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="45a67-116">*Correctif*: offre une compatibilité descendante correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="45a67-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="45a67-117">*-Suffixe* (facultatif) : un trait d’union suivi d’une chaîne qui dénote une version préliminaire (suivant la [convention de contrôle de version sémantique ou SemVer 1.0](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="45a67-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="45a67-118">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="45a67-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="45a67-119">NuGet.org rejette tout le téléchargement du package qui ne dispose pas d’un numéro de version exact.</span><span class="sxs-lookup"><span data-stu-id="45a67-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="45a67-120">La version doit être spécifiée dans le `.nuspec` ou le fichier de projet utilisé pour créer le package.</span><span class="sxs-lookup"><span data-stu-id="45a67-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="45a67-121">Versions préliminaires</span><span class="sxs-lookup"><span data-stu-id="45a67-121">Pre-release versions</span></span>

<span data-ttu-id="45a67-122">Techniquement parlant, créateurs de package peuvent utiliser n’importe quelle chaîne comme suffixe pour désigner une version préliminaire, NuGet traite n’importe quelle version de ce type en tant que version préliminaire et rend les autres sans interprétation.</span><span class="sxs-lookup"><span data-stu-id="45a67-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="45a67-123">Autrement dit, affiche NuGet la version complète de chaîne dans l’interface utilisateur est impliquée, laissant toute interprétation de, autrement dit le suffixe au consommateur.</span><span class="sxs-lookup"><span data-stu-id="45a67-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="45a67-124">Ceci dit, les développeurs de packages suivent les conventions d’affectation de noms reconnues :</span><span class="sxs-lookup"><span data-stu-id="45a67-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="45a67-125">`-alpha`: Version alpha, généralement utilisée pour les travaux en cours et d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="45a67-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="45a67-126">`-beta`: version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.</span><span class="sxs-lookup"><span data-stu-id="45a67-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="45a67-127">`-rc` : version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.</span><span class="sxs-lookup"><span data-stu-id="45a67-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="45a67-128">Prend en charge de NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de version préliminaire avec la notation à points, comme dans *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="45a67-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="45a67-129">La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="45a67-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="45a67-130">Vous pouvez utiliser un formulaire comme *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="45a67-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="45a67-131">Lors de la résolution des références de package et de plusieurs versions de package diffèrent uniquement par le suffixe, NuGet choisit une version sans suffixe tout d’abord, puis applique la priorité pour la version préliminaire dans l’ordre alphabétique inverse.</span><span class="sxs-lookup"><span data-stu-id="45a67-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="45a67-132">Par exemple, les versions suivantes sont choisies en respectant l’ordre indiqué :</span><span class="sxs-lookup"><span data-stu-id="45a67-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="45a67-133">Contrôle de version sémantique 2.0.0</span><span class="sxs-lookup"><span data-stu-id="45a67-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="45a67-134">Avec NuGet 4.3.0+ et Visual Studio 2017 version 15.3 +, NuGet prend en charge [contrôle de version sémantique 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="45a67-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="45a67-135">Certaines sémantiques de SemVer v2.0.0 ne sont pas pris en charge de clients plus anciens.</span><span class="sxs-lookup"><span data-stu-id="45a67-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="45a67-136">NuGet considère qu’une version de package à être v2.0.0 SemVer spécifiques si une des affirmations suivantes est vraie :</span><span class="sxs-lookup"><span data-stu-id="45a67-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="45a67-137">L’étiquette de la version préliminaire est séparée par un point, par exemple, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="45a67-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="45a67-138">La version a des métadonnées de la génération, par exemple, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="45a67-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="45a67-139">Pour nuget.org, un package est défini en tant que package v2.0.0 SemVer si une des affirmations suivantes est vraie :</span><span class="sxs-lookup"><span data-stu-id="45a67-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="45a67-140">La version du package est v2.0.0 SemVer conforme, mais pas les v1.0.0 SemVer conforme, tel qu’indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="45a67-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="45a67-141">Une des plages de versions de dépendance du package dont la version minimale ou maximale est v2.0.0 SemVer conforme, mais pas les v1.0.0 SemVer conforme, définis ci-dessus ; par exemple, *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="45a67-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="45a67-142">Si vous téléchargez un package de v2.0.0 spécifiques SemVer nuget.org, le package est invisible pour les clients plus anciens et disponible aux clients NuGet uniquement suivants :</span><span class="sxs-lookup"><span data-stu-id="45a67-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="45a67-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="45a67-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="45a67-144">Visual Studio 2017 version 15.3 +</span><span class="sxs-lookup"><span data-stu-id="45a67-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="45a67-145">Visual Studio 2015 avec [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="45a67-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="45a67-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="45a67-146">dotnet</span></span>
  - <span data-ttu-id="45a67-147">dotnetcore.exe (Kit de développement .NET 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="45a67-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="45a67-148">Les clients tiers :</span><span class="sxs-lookup"><span data-stu-id="45a67-148">Third-party clients:</span></span>

- <span data-ttu-id="45a67-149">JetBrains avenant</span><span class="sxs-lookup"><span data-stu-id="45a67-149">JetBrains Rider</span></span>
- <span data-ttu-id="45a67-150">Paket version 5.0 +</span><span class="sxs-lookup"><span data-stu-id="45a67-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="45a67-151">Les caractères génériques et les plages de versions</span><span class="sxs-lookup"><span data-stu-id="45a67-151">Version ranges and wildcards</span></span>

<span data-ttu-id="45a67-152">Lorsque vous faites référence aux dépendances de package, NuGet prend en charge à l’aide de la notation de l’intervalle pour la spécification de plages de versions, résumées comme suit :</span><span class="sxs-lookup"><span data-stu-id="45a67-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="45a67-153">Notation</span><span class="sxs-lookup"><span data-stu-id="45a67-153">Notation</span></span> | <span data-ttu-id="45a67-154">Règle appliquée</span><span class="sxs-lookup"><span data-stu-id="45a67-154">Applied rule</span></span> | <span data-ttu-id="45a67-155">Description</span><span class="sxs-lookup"><span data-stu-id="45a67-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="45a67-156">1.0</span><span class="sxs-lookup"><span data-stu-id="45a67-156">1.0</span></span> | <span data-ttu-id="45a67-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="45a67-157">x ≥ 1.0</span></span> | <span data-ttu-id="45a67-158">Version minimale, inclusive</span><span class="sxs-lookup"><span data-stu-id="45a67-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="45a67-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="45a67-159">(1.0,)</span></span> | <span data-ttu-id="45a67-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="45a67-160">x > 1.0</span></span> | <span data-ttu-id="45a67-161">Version minimale, exclusive</span><span class="sxs-lookup"><span data-stu-id="45a67-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="45a67-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="45a67-162">[1.0]</span></span> | <span data-ttu-id="45a67-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="45a67-163">x == 1.0</span></span> | <span data-ttu-id="45a67-164">Correspondance exacte</span><span class="sxs-lookup"><span data-stu-id="45a67-164">Exact version match</span></span> |
| <span data-ttu-id="45a67-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="45a67-165">(,1.0]</span></span> | <span data-ttu-id="45a67-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="45a67-166">x ≤ 1.0</span></span> | <span data-ttu-id="45a67-167">Version maximale, inclusive</span><span class="sxs-lookup"><span data-stu-id="45a67-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="45a67-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="45a67-168">(,1.0)</span></span> | <span data-ttu-id="45a67-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="45a67-169">x < 1.0</span></span> | <span data-ttu-id="45a67-170">Version maximale, exclusive</span><span class="sxs-lookup"><span data-stu-id="45a67-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="45a67-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="45a67-171">[1.0,2.0]</span></span> | <span data-ttu-id="45a67-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="45a67-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="45a67-173">Plage exacte, inclusif</span><span class="sxs-lookup"><span data-stu-id="45a67-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="45a67-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="45a67-174">(1.0,2.0)</span></span> | <span data-ttu-id="45a67-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="45a67-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="45a67-176">Plage exacte, exclusif</span><span class="sxs-lookup"><span data-stu-id="45a67-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="45a67-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="45a67-177">[1.0,2.0)</span></span> | <span data-ttu-id="45a67-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="45a67-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="45a67-179">Inclusive minimum et exclusive maximale version mixte</span><span class="sxs-lookup"><span data-stu-id="45a67-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="45a67-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="45a67-180">(1.0)</span></span>    | <span data-ttu-id="45a67-181">non valide</span><span class="sxs-lookup"><span data-stu-id="45a67-181">invalid</span></span> | <span data-ttu-id="45a67-182">non valide</span><span class="sxs-lookup"><span data-stu-id="45a67-182">invalid</span></span> |

<span data-ttu-id="45a67-183">Lorsque vous utilisez le format PackageReference, NuGet prend également en charge à l’aide d’une notation de caractère générique, \*, pour majeure, mineure, Patch et parties de suffixe de la version préliminaire du nombre.</span><span class="sxs-lookup"><span data-stu-id="45a67-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="45a67-184">Les caractères génériques ne sont pas pris en charge avec les `packages.config` format.</span><span class="sxs-lookup"><span data-stu-id="45a67-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="45a67-185">Versions antérieures ne sont pas incluses lors de la résolution des plages de versions.</span><span class="sxs-lookup"><span data-stu-id="45a67-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="45a67-186">Versions préliminaires *sont* inclus lorsque vous utilisez un caractère générique (\*).</span><span class="sxs-lookup"><span data-stu-id="45a67-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="45a67-187">La plage de versions *[1.0,2.0]*, par exemple, n’inclut pas 2.0 bêta, mais les génériques _2.0-\*_ est.</span><span class="sxs-lookup"><span data-stu-id="45a67-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="45a67-188">Consultez [émettre 912](https://github.com/NuGet/Home/issues/912) pour obtenir des informations sur les caractères génériques de la version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="45a67-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="45a67-189">Exemples</span><span class="sxs-lookup"><span data-stu-id="45a67-189">Examples</span></span>

<span data-ttu-id="45a67-190">Spécifiez toujours une version ou une plage de versions pour les dépendances de package dans les fichiers de projet, `packages.config` fichiers, et `.nuspec` fichiers.</span><span class="sxs-lookup"><span data-stu-id="45a67-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="45a67-191">Sans une version ou d’une plage de versions, NuGet 2.8.x et précédemment choisit la dernière version de package disponibles lors de la résolution d’une dépendance, tandis que NuGet 3.x et choisit ensuite d’utiliser la version du package le plus bas.</span><span class="sxs-lookup"><span data-stu-id="45a67-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="45a67-192">Spécification d’une version ou plage permet d’éviter cette incertitude.</span><span class="sxs-lookup"><span data-stu-id="45a67-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="45a67-193">Références dans les fichiers de projet (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="45a67-193">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="45a67-194">**Références de `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="45a67-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="45a67-195">Dans `packages.config`, chaque dépendance est répertorié avec un exacte `version` attribut qui est utilisé lors de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="45a67-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="45a67-196">Le `allowedVersions` attribut est utilisé uniquement pendant les opérations de mise à jour pour limiter les versions à laquelle le package peut être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="45a67-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="45a67-197">**Références de `.nuspec` fichiers**</span><span class="sxs-lookup"><span data-stu-id="45a67-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="45a67-198">Le `version` d’attribut dans un `<dependency>` élément décrit les versions de plage qui sont acceptables pour une dépendance.</span><span class="sxs-lookup"><span data-stu-id="45a67-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="45a67-199">Numéros de version normalisée</span><span class="sxs-lookup"><span data-stu-id="45a67-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="45a67-200">Il s’agit d’une modification avec rupture pour NuGet 3.4 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="45a67-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="45a67-201">Lors de l’obtention de packages à partir d’un référentiel pendant l’installation, réinstallez ou restaurer les opérations, NuGet 3.4 + traite les numéros de version comme suit :</span><span class="sxs-lookup"><span data-stu-id="45a67-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="45a67-202">Les zéros non significatifs sont supprimés de numéros de version :</span><span class="sxs-lookup"><span data-stu-id="45a67-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="45a67-203">Un zéro dans la quatrième partie du numéro de version sera omis</span><span class="sxs-lookup"><span data-stu-id="45a67-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="45a67-204">Cette normalisation n’affecte pas les numéros de version dans les packages eux-mêmes ; elle affecte uniquement comment NuGet correspond aux versions lors de la résolution des dépendances.</span><span class="sxs-lookup"><span data-stu-id="45a67-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="45a67-205">Toutefois, les dépôts de package NuGet doivent traiter ces valeurs dans la même façon que NuGet pour éviter la duplication de version de package.</span><span class="sxs-lookup"><span data-stu-id="45a67-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="45a67-206">Par conséquent, un référentiel qui contient la version *1.0* d’un package ne doivent pas également héberger version *1.0.0* en tant que package distinct et différent.</span><span class="sxs-lookup"><span data-stu-id="45a67-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
