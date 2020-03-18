---
title: Référence de version de package NuGet
description: Détails exacts sur la spécification des numéros de version et des plages pour les autres packages dont dépend un package NuGet, et comment les dépendances sont installées.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 912c0d015e2f499bc7386483bc6c35ecd765d3d4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428834"
---
# <a name="package-versioning"></a><span data-ttu-id="99170-103">Contrôle de version des packages</span><span class="sxs-lookup"><span data-stu-id="99170-103">Package versioning</span></span>

<span data-ttu-id="99170-104">Un package spécifique est toujours référencé à l'aide de son identificateur de package et d'un numéro de version exact.</span><span class="sxs-lookup"><span data-stu-id="99170-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="99170-105">Par exemple, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sur nuget.org propose plusieurs dizaines de packages spécifiques disponibles, allant de la version *4.1.10311* à la version *6.1.3*. (la dernière version stable) et une variété de préversions comme *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="99170-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="99170-106">Lors de la création d'un package, vous attribuez un numéro de version spécifique avec un suffixe de texte de préversion optionnel.</span><span class="sxs-lookup"><span data-stu-id="99170-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="99170-107">En revanche, lorsque vous consommez des packages, vous pouvez spécifier un numéro de version exact ou une plage de versions acceptables.</span><span class="sxs-lookup"><span data-stu-id="99170-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="99170-108">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="99170-108">In this topic:</span></span>

- <span data-ttu-id="99170-109">[Principes de base d’une version](#version-basics), y compris les suffixes de préversion.</span><span class="sxs-lookup"><span data-stu-id="99170-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="99170-110">Plages de versions</span><span class="sxs-lookup"><span data-stu-id="99170-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="99170-111">Numéros de version normalisés</span><span class="sxs-lookup"><span data-stu-id="99170-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="99170-112">Principes de base d’une version</span><span class="sxs-lookup"><span data-stu-id="99170-112">Version basics</span></span>

<span data-ttu-id="99170-113">Un numéro de version spécifique se présente sous la forme *Major.Minor.Patch[-Suffix]* , où les composants ont la signification suivante :</span><span class="sxs-lookup"><span data-stu-id="99170-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="99170-114">*Majeure*: modifications avec rupture</span><span class="sxs-lookup"><span data-stu-id="99170-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="99170-115">*Mineure*: nouvelles fonctionnalités, mais à compatibilité descendante</span><span class="sxs-lookup"><span data-stu-id="99170-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="99170-116">*Patch*: correctifs de bogues à compatibilité descendante uniquement</span><span class="sxs-lookup"><span data-stu-id="99170-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="99170-117">*-Suffix* (optionnel) : un trait d'union suivi d'une chaîne de caractères indiquant une version préversion (suivant la convention [Semantic Versioning ou SemVer 1.0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="99170-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="99170-118">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="99170-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="99170-119">nuget.org rejette tout upload de package sans numéro de version exact.</span><span class="sxs-lookup"><span data-stu-id="99170-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="99170-120">La version doit être spécifiée dans le fichier `.nuspec` ou fichier projet utilisé pour créer le package.</span><span class="sxs-lookup"><span data-stu-id="99170-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="99170-121">Préversions</span><span class="sxs-lookup"><span data-stu-id="99170-121">Pre-release versions</span></span>

<span data-ttu-id="99170-122">Techniquement parlant, les créateurs de packages peuvent utiliser n'importe quelle chaîne de caractères comme suffixe pour désigner une préversion car NuGet traite une telle version comme une préversion et ne fait aucune autre interprétation.</span><span class="sxs-lookup"><span data-stu-id="99170-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="99170-123">En d'autres termes, NuGet affiche la chaîne de caractères de la version complète, quelle que soit l'interface utilisateur concernée, laissant au consommateur le soin d'interpréter la signification du suffixe.</span><span class="sxs-lookup"><span data-stu-id="99170-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="99170-124">Cela dit, les développeurs de packages adoptent généralement des conventions d’affectation de noms reconnues :</span><span class="sxs-lookup"><span data-stu-id="99170-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="99170-125">`-alpha`: version alpha, généralement utilisée pour les travaux en cours et l’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="99170-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="99170-126">`-beta`: version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.</span><span class="sxs-lookup"><span data-stu-id="99170-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="99170-127">`-rc` : version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.</span><span class="sxs-lookup"><span data-stu-id="99170-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="99170-128">NuGet 4.3.0+ prend en charge [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de préversion utilisant la notation à points (par exemple, *1.0.1-build.23*).</span><span class="sxs-lookup"><span data-stu-id="99170-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="99170-129">La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="99170-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="99170-130">Vous pouvez utiliser un format comme *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="99170-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="99170-131">Lorsque vous résolvez des références de packages et que plusieurs versions de packages ne diffèrent que par le suffixe, NuGet choisit d'abord une version sans suffixe, puis applique la priorité aux préversions dans l'ordre alphabétique inverse.</span><span class="sxs-lookup"><span data-stu-id="99170-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="99170-132">Par exemple, les versions suivantes seraient choisies dans l'ordre exact indiqué :</span><span class="sxs-lookup"><span data-stu-id="99170-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="99170-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="99170-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="99170-134">Avec NuGet 4.3.0+ et Visual Studio 2017 version 15.3+, NuGet prend en charge [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="99170-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="99170-135">Certaines sémantiques de SemVer 2.0.0 ne sont pas prises en charge dans les clients plus anciens.</span><span class="sxs-lookup"><span data-stu-id="99170-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="99170-136">NuGet considère une version de package comme spécifique à SemVer 2.0.0 si l'un des énoncés suivants est vrai :</span><span class="sxs-lookup"><span data-stu-id="99170-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="99170-137">L'étiquette de préversion est séparée par des points, par exemple, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="99170-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="99170-138">La version contient des métadonnées de build, par exemple, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="99170-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="99170-139">Pour nuget.org, un package est défini comme un package SemVer 2.0.0 si l'un des énoncés suivants est vrai :</span><span class="sxs-lookup"><span data-stu-id="99170-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="99170-140">La propre version du package est conforme à SemVer 2.0.0 mais pas à SemVer 1.0.0, comme défini ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="99170-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="99170-141">Toutes les plages de versions des dépendances du package ont une version minimale ou maximale conforme à SemVer 2.0.0 mais non conforme à SemVer 1.0.0, définie ci-dessus ; par exemple, *[1.0.0-alpha.1, )* .</span><span class="sxs-lookup"><span data-stu-id="99170-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="99170-142">Si vous uploadez un package spécifique à SemVer 2.0.0 sur nuget.org, le package est invisible pour les anciens clients et disponible uniquement pour les clients NuGet suivants :</span><span class="sxs-lookup"><span data-stu-id="99170-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="99170-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="99170-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="99170-144">Visual Studio 2017 15.3+</span><span class="sxs-lookup"><span data-stu-id="99170-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="99170-145">Visual Studio 2015 with [NuGet VSIX 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="99170-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="99170-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="99170-146">dotnet</span></span>
  - <span data-ttu-id="99170-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="99170-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="99170-148">Clients tiers :</span><span class="sxs-lookup"><span data-stu-id="99170-148">Third-party clients:</span></span>

- <span data-ttu-id="99170-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="99170-149">JetBrains Rider</span></span>
- <span data-ttu-id="99170-150">Paket version 5.0+</span><span class="sxs-lookup"><span data-stu-id="99170-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="99170-151">Plages de versions</span><span class="sxs-lookup"><span data-stu-id="99170-151">Version ranges</span></span>

<span data-ttu-id="99170-152">Lorsque NuGet fait référence à des dépendances de packages, il prend en charge l'utilisation de la notation d'intervalle pour spécifier les plages de versions, résumées comme suit :</span><span class="sxs-lookup"><span data-stu-id="99170-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="99170-153">Notation</span><span class="sxs-lookup"><span data-stu-id="99170-153">Notation</span></span> | <span data-ttu-id="99170-154">Règle appliquée</span><span class="sxs-lookup"><span data-stu-id="99170-154">Applied rule</span></span> | <span data-ttu-id="99170-155">Description</span><span class="sxs-lookup"><span data-stu-id="99170-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="99170-156">1.0</span><span class="sxs-lookup"><span data-stu-id="99170-156">1.0</span></span> | <span data-ttu-id="99170-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="99170-157">x ≥ 1.0</span></span> | <span data-ttu-id="99170-158">Version minimale, inclusive</span><span class="sxs-lookup"><span data-stu-id="99170-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="99170-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="99170-159">(1.0,)</span></span> | <span data-ttu-id="99170-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="99170-160">x > 1.0</span></span> | <span data-ttu-id="99170-161">Version minimale, exclusive</span><span class="sxs-lookup"><span data-stu-id="99170-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="99170-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="99170-162">[1.0]</span></span> | <span data-ttu-id="99170-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="99170-163">x == 1.0</span></span> | <span data-ttu-id="99170-164">Correspondance exacte des versions</span><span class="sxs-lookup"><span data-stu-id="99170-164">Exact version match</span></span> |
| <span data-ttu-id="99170-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="99170-165">(,1.0]</span></span> | <span data-ttu-id="99170-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="99170-166">x ≤ 1.0</span></span> | <span data-ttu-id="99170-167">Version maximale, inclusive</span><span class="sxs-lookup"><span data-stu-id="99170-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="99170-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="99170-168">(,1.0)</span></span> | <span data-ttu-id="99170-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="99170-169">x < 1.0</span></span> | <span data-ttu-id="99170-170">Version maximale, exclusive</span><span class="sxs-lookup"><span data-stu-id="99170-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="99170-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="99170-171">[1.0,2.0]</span></span> | <span data-ttu-id="99170-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="99170-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="99170-173">Plage exacte, inclusive</span><span class="sxs-lookup"><span data-stu-id="99170-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="99170-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="99170-174">(1.0,2.0)</span></span> | <span data-ttu-id="99170-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="99170-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="99170-176">Plage exacte, exclusive</span><span class="sxs-lookup"><span data-stu-id="99170-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="99170-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="99170-177">[1.0,2.0)</span></span> | <span data-ttu-id="99170-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="99170-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="99170-179">Version maximum exclusive et minimum inclusive mixte</span><span class="sxs-lookup"><span data-stu-id="99170-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="99170-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="99170-180">(1.0)</span></span>    | <span data-ttu-id="99170-181">non valide</span><span class="sxs-lookup"><span data-stu-id="99170-181">invalid</span></span> | <span data-ttu-id="99170-182">non valide</span><span class="sxs-lookup"><span data-stu-id="99170-182">invalid</span></span> |

<span data-ttu-id="99170-183">Lorsque vous utilisez le format PackageReference, NuGet prend également en charge l’utilisation d’une notation flottante, \*, pour les parties majeures, mineures, correctives et de suffixe de préversion du nombre.</span><span class="sxs-lookup"><span data-stu-id="99170-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="99170-184">Les versions flottantes ne sont pas prises en charge avec le format `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="99170-184">Floating versions are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="99170-185">Les plages de versions dans PackageReference incluent des préversions.</span><span class="sxs-lookup"><span data-stu-id="99170-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="99170-186">De par leur conception, les versions flottantes ne résolvent pas les préversions à moins que vous ne l’ayez décidé.</span><span class="sxs-lookup"><span data-stu-id="99170-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="99170-187">Pour connaître l'état de la demande de fonctionnalité associée, voir le [problème 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="99170-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="99170-188">Exemples</span><span class="sxs-lookup"><span data-stu-id="99170-188">Examples</span></span>

<span data-ttu-id="99170-189">Spécifiez toujours une version ou une plage de versions pour les dépendances de packages dans les fichiers projet, les fichiers `packages.config` et les fichiers `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="99170-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="99170-190">Sans version ou plage de versions, NuGet 2.8.x (et versions antérieures) choisit la dernière version de package disponible lors de la résolution d'une dépendance, tandis que NuGet 3.x (et versions ultérieures) sélectionne la version de package la plus basse.</span><span class="sxs-lookup"><span data-stu-id="99170-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="99170-191">La spécification d'une version ou d'une plage de versions permet de lever ce doute.</span><span class="sxs-lookup"><span data-stu-id="99170-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="99170-192">Références dans les fichiers projet (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="99170-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="99170-193">**Références dans `packages.config` :**</span><span class="sxs-lookup"><span data-stu-id="99170-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="99170-194">dans `packages.config`, chaque dépendance est répertoriée avec un attribut `version` exact utilisé lors de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="99170-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="99170-195">L'attribut `allowedVersions` n'est utilisé que pendant les opérations de mise à jour afin de limiter les versions avec lesquelles le package peut être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="99170-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="99170-196">**Références dans les fichiers `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="99170-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="99170-197">L'attribut `version` d'un élément `<dependency>` décrit les versions de plage acceptables pour une dépendance.</span><span class="sxs-lookup"><span data-stu-id="99170-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="99170-198">Numéros de version normalisés</span><span class="sxs-lookup"><span data-stu-id="99170-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="99170-199">Il s’agit d’un changement important pour NuGet 3.4 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="99170-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="99170-200">Lorsque vous obtenez des packages à partir d'un référentiel pendant l'installation, la réinstallation ou la restauration, NuGet 3.4+ traite les numéros de version comme suit :</span><span class="sxs-lookup"><span data-stu-id="99170-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="99170-201">Les zéros non significatifs sont supprimés des numéros de version :</span><span class="sxs-lookup"><span data-stu-id="99170-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="99170-202">Un zéro dans la quatrième partie du numéro de version sera omis</span><span class="sxs-lookup"><span data-stu-id="99170-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="99170-203">Les opérations `pack` et `restore` normalisent les versions lorsque cela est possible.</span><span class="sxs-lookup"><span data-stu-id="99170-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="99170-204">Pour les packages déjà construits, cette normalisation n'affecte pas les numéros de version dans les packages eux-mêmes ; elle affecte uniquement la façon dont NuGet mappe les versions lors de la résolution des dépendances.</span><span class="sxs-lookup"><span data-stu-id="99170-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="99170-205">Cependant, les dépôts de packages NuGet doivent traiter ces valeurs de la même manière que NuGet pour éviter la duplication des versions de packages.</span><span class="sxs-lookup"><span data-stu-id="99170-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="99170-206">Ainsi, un référentiel qui contient la version *1.0* d'un package ne doit pas également héberger la version *1.0.0* comme un package séparé et différent.</span><span class="sxs-lookup"><span data-stu-id="99170-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
