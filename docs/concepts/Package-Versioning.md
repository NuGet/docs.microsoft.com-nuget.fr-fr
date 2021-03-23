---
title: Référence de version de package NuGet
description: Détails exacts sur la spécification des numéros de version et des plages pour les autres packages dont dépend un package NuGet, et comment les dépendances sont installées.
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 77b96e83f8fc7afd391537d16120d037585dd379
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859198"
---
# <a name="package-versioning"></a><span data-ttu-id="9e99b-103">Contrôle de version des packages</span><span class="sxs-lookup"><span data-stu-id="9e99b-103">Package versioning</span></span>

<span data-ttu-id="9e99b-104">Un package spécifique est toujours référencé à l'aide de son identificateur de package et d'un numéro de version exact.</span><span class="sxs-lookup"><span data-stu-id="9e99b-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="9e99b-105">Par exemple, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sur nuget.org propose plusieurs dizaines de packages spécifiques disponibles, allant de la version *4.1.10311* à la version *6.1.3*. (la dernière version stable) et une variété de préversions comme *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="9e99b-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="9e99b-106">Lors de la création d'un package, vous attribuez un numéro de version spécifique avec un suffixe de texte de préversion optionnel.</span><span class="sxs-lookup"><span data-stu-id="9e99b-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="9e99b-107">En revanche, lorsque vous consommez des packages, vous pouvez spécifier un numéro de version exact ou une plage de versions acceptables.</span><span class="sxs-lookup"><span data-stu-id="9e99b-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="9e99b-108">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="9e99b-108">In this topic:</span></span>

- <span data-ttu-id="9e99b-109">[Principes de base d’une version](#version-basics), y compris les suffixes de préversion.</span><span class="sxs-lookup"><span data-stu-id="9e99b-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="9e99b-110">Plages de versions</span><span class="sxs-lookup"><span data-stu-id="9e99b-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="9e99b-111">Numéros de version normalisés</span><span class="sxs-lookup"><span data-stu-id="9e99b-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="9e99b-112">Principes de base d’une version</span><span class="sxs-lookup"><span data-stu-id="9e99b-112">Version basics</span></span>

<span data-ttu-id="9e99b-113">Un numéro de version spécifique se présente sous la forme *Major.Minor.Patch[-Suffix]*, où les composants ont la signification suivante :</span><span class="sxs-lookup"><span data-stu-id="9e99b-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="9e99b-114">*Majeure*: modifications avec rupture</span><span class="sxs-lookup"><span data-stu-id="9e99b-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="9e99b-115">*Mineure*: nouvelles fonctionnalités, mais à compatibilité descendante</span><span class="sxs-lookup"><span data-stu-id="9e99b-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="9e99b-116">*Patch*: correctifs de bogues à compatibilité descendante uniquement</span><span class="sxs-lookup"><span data-stu-id="9e99b-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="9e99b-117">*-Suffix* (optionnel) : un trait d'union suivi d'une chaîne de caractères indiquant une version préversion (suivant la convention [Semantic Versioning ou SemVer 1.0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="9e99b-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="9e99b-118">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="9e99b-118">**Examples:**</span></span>

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="9e99b-119">nuget.org rejette tout upload de package sans numéro de version exact.</span><span class="sxs-lookup"><span data-stu-id="9e99b-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="9e99b-120">La version doit être spécifiée dans le fichier `.nuspec` ou fichier projet utilisé pour créer le package.</span><span class="sxs-lookup"><span data-stu-id="9e99b-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="9e99b-121">Préversions</span><span class="sxs-lookup"><span data-stu-id="9e99b-121">Pre-release versions</span></span>

<span data-ttu-id="9e99b-122">Techniquement parlant, les créateurs de packages peuvent utiliser n'importe quelle chaîne de caractères comme suffixe pour désigner une préversion car NuGet traite une telle version comme une préversion et ne fait aucune autre interprétation.</span><span class="sxs-lookup"><span data-stu-id="9e99b-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="9e99b-123">En d'autres termes, NuGet affiche la chaîne de caractères de la version complète, quelle que soit l'interface utilisateur concernée, laissant au consommateur le soin d'interpréter la signification du suffixe.</span><span class="sxs-lookup"><span data-stu-id="9e99b-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="9e99b-124">Cela dit, les développeurs de packages adoptent généralement des conventions d’affectation de noms reconnues :</span><span class="sxs-lookup"><span data-stu-id="9e99b-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="9e99b-125">`-alpha`: Version alpha, généralement utilisée pour les travaux en cours et l’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="9e99b-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="9e99b-126">`-beta`: version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.</span><span class="sxs-lookup"><span data-stu-id="9e99b-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="9e99b-127">`-rc` : version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.</span><span class="sxs-lookup"><span data-stu-id="9e99b-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="9e99b-128">NuGet 4.3.0+ prend en charge [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de préversion utilisant la notation à points (par exemple, *1.0.1-build.23*).</span><span class="sxs-lookup"><span data-stu-id="9e99b-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="9e99b-129">La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="9e99b-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="9e99b-130">Vous pouvez utiliser un format comme *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="9e99b-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="9e99b-131">Lorsque vous résolvez des références de packages et que plusieurs versions de packages ne diffèrent que par le suffixe, NuGet choisit d'abord une version sans suffixe, puis applique la priorité aux préversions dans l'ordre alphabétique inverse.</span><span class="sxs-lookup"><span data-stu-id="9e99b-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="9e99b-132">Par exemple, les versions suivantes seraient choisies dans l'ordre exact indiqué :</span><span class="sxs-lookup"><span data-stu-id="9e99b-132">For example, the following versions would be chosen in the exact order shown:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a><span data-ttu-id="9e99b-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="9e99b-134">Avec NuGet 4.3.0+ et Visual Studio 2017 version 15.3+, NuGet prend en charge [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="9e99b-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="9e99b-135">Certaines sémantiques de SemVer 2.0.0 ne sont pas prises en charge dans les clients plus anciens.</span><span class="sxs-lookup"><span data-stu-id="9e99b-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="9e99b-136">NuGet considère une version de package comme spécifique à SemVer 2.0.0 si l'un des énoncés suivants est vrai :</span><span class="sxs-lookup"><span data-stu-id="9e99b-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="9e99b-137">L'étiquette de préversion est séparée par des points, par exemple, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="9e99b-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="9e99b-138">La version contient des métadonnées de build, par exemple, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="9e99b-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="9e99b-139">Pour nuget.org, un package est défini comme un package SemVer 2.0.0 si l'un des énoncés suivants est vrai :</span><span class="sxs-lookup"><span data-stu-id="9e99b-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="9e99b-140">La propre version du package est conforme à SemVer 2.0.0 mais pas à SemVer 1.0.0, comme défini ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9e99b-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="9e99b-141">Toutes les plages de versions des dépendances du package ont une version minimale ou maximale conforme à SemVer 2.0.0 mais non conforme à SemVer 1.0.0, définie ci-dessus ; par exemple, *[1.0.0-alpha.1, )*.</span><span class="sxs-lookup"><span data-stu-id="9e99b-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="9e99b-142">Si vous uploadez un package spécifique à SemVer 2.0.0 sur nuget.org, le package est invisible pour les anciens clients et disponible uniquement pour les clients NuGet suivants :</span><span class="sxs-lookup"><span data-stu-id="9e99b-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="9e99b-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="9e99b-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="9e99b-144">Visual Studio 2017 15.3+</span><span class="sxs-lookup"><span data-stu-id="9e99b-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="9e99b-145">Visual Studio 2015 with [NuGet VSIX 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="9e99b-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="9e99b-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="9e99b-146">dotnet</span></span>
  - <span data-ttu-id="9e99b-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="9e99b-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="9e99b-148">Clients tiers :</span><span class="sxs-lookup"><span data-stu-id="9e99b-148">Third-party clients:</span></span>

- <span data-ttu-id="9e99b-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="9e99b-149">JetBrains Rider</span></span>
- <span data-ttu-id="9e99b-150">Paket version 5.0+</span><span class="sxs-lookup"><span data-stu-id="9e99b-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="9e99b-151">Plages de versions</span><span class="sxs-lookup"><span data-stu-id="9e99b-151">Version ranges</span></span>

<span data-ttu-id="9e99b-152">Lorsque NuGet fait référence à des dépendances de packages, il prend en charge l'utilisation de la notation d'intervalle pour spécifier les plages de versions, résumées comme suit :</span><span class="sxs-lookup"><span data-stu-id="9e99b-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="9e99b-153">Notation</span><span class="sxs-lookup"><span data-stu-id="9e99b-153">Notation</span></span> | <span data-ttu-id="9e99b-154">Règle appliquée</span><span class="sxs-lookup"><span data-stu-id="9e99b-154">Applied rule</span></span> | <span data-ttu-id="9e99b-155">Description</span><span class="sxs-lookup"><span data-stu-id="9e99b-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="9e99b-156">1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-156">1.0</span></span> | <span data-ttu-id="9e99b-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-157">x ≥ 1.0</span></span> | <span data-ttu-id="9e99b-158">Version minimale, inclusive</span><span class="sxs-lookup"><span data-stu-id="9e99b-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="9e99b-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="9e99b-159">(1.0,)</span></span> | <span data-ttu-id="9e99b-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-160">x > 1.0</span></span> | <span data-ttu-id="9e99b-161">Version minimale, exclusive</span><span class="sxs-lookup"><span data-stu-id="9e99b-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="9e99b-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="9e99b-162">[1.0]</span></span> | <span data-ttu-id="9e99b-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-163">x == 1.0</span></span> | <span data-ttu-id="9e99b-164">Correspondance exacte des versions</span><span class="sxs-lookup"><span data-stu-id="9e99b-164">Exact version match</span></span> |
| <span data-ttu-id="9e99b-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="9e99b-165">(,1.0]</span></span> | <span data-ttu-id="9e99b-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-166">x ≤ 1.0</span></span> | <span data-ttu-id="9e99b-167">Version maximale, inclusive</span><span class="sxs-lookup"><span data-stu-id="9e99b-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="9e99b-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="9e99b-168">(,1.0)</span></span> | <span data-ttu-id="9e99b-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-169">x < 1.0</span></span> | <span data-ttu-id="9e99b-170">Version maximale, exclusive</span><span class="sxs-lookup"><span data-stu-id="9e99b-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="9e99b-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="9e99b-171">[1.0,2.0]</span></span> | <span data-ttu-id="9e99b-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="9e99b-173">Plage exacte, inclusive</span><span class="sxs-lookup"><span data-stu-id="9e99b-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="9e99b-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="9e99b-174">(1.0,2.0)</span></span> | <span data-ttu-id="9e99b-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="9e99b-176">Plage exacte, exclusive</span><span class="sxs-lookup"><span data-stu-id="9e99b-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="9e99b-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="9e99b-177">[1.0,2.0)</span></span> | <span data-ttu-id="9e99b-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="9e99b-179">Version maximum exclusive et minimum inclusive mixte</span><span class="sxs-lookup"><span data-stu-id="9e99b-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="9e99b-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="9e99b-180">(1.0)</span></span>    | <span data-ttu-id="9e99b-181">non valide</span><span class="sxs-lookup"><span data-stu-id="9e99b-181">invalid</span></span> | <span data-ttu-id="9e99b-182">non valide</span><span class="sxs-lookup"><span data-stu-id="9e99b-182">invalid</span></span> |

<span data-ttu-id="9e99b-183">Lors de l’utilisation du format PackageReference, NuGet prend également en charge l’utilisation d’une notation flottante, \* , pour les parties de suffixe majeure, mineure, de correctif et de préversion du nombre.</span><span class="sxs-lookup"><span data-stu-id="9e99b-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="9e99b-184">Les versions flottantes ne sont pas prises en charge avec le `packages.config` format.</span><span class="sxs-lookup"><span data-stu-id="9e99b-184">Floating versions are not supported with the `packages.config` format.</span></span> <span data-ttu-id="9e99b-185">Quand une version flottante est spécifiée, la règle doit être résolue en la version existante la plus élevée qui correspond à la description de la version.</span><span class="sxs-lookup"><span data-stu-id="9e99b-185">When a floating version is specified, the rule is to resolve to the highest existent version that matches the version description.</span></span> <span data-ttu-id="9e99b-186">Vous trouverez ci-dessous des exemples de versions flottantes et de résolution.</span><span class="sxs-lookup"><span data-stu-id="9e99b-186">Examples of floating versions and the resolutions are below.</span></span>

> [!Note]
> <span data-ttu-id="9e99b-187">Les plages de versions dans PackageReference incluent des préversions.</span><span class="sxs-lookup"><span data-stu-id="9e99b-187">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="9e99b-188">De par leur conception, les versions flottantes ne résolvent pas les préversions à moins que vous ne l’ayez décidé.</span><span class="sxs-lookup"><span data-stu-id="9e99b-188">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="9e99b-189">Pour connaître l'état de la demande de fonctionnalité associée, voir le [problème 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="9e99b-189">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="9e99b-190">Exemples</span><span class="sxs-lookup"><span data-stu-id="9e99b-190">Examples</span></span>

<span data-ttu-id="9e99b-191">Spécifiez toujours une version ou une plage de versions pour les dépendances de packages dans les fichiers projet, les fichiers `packages.config` et les fichiers `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="9e99b-191">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="9e99b-192">Sans version ou plage de versions, NuGet 2.8.x (et versions antérieures) choisit la dernière version de package disponible lors de la résolution d'une dépendance, tandis que NuGet 3.x (et versions ultérieures) sélectionne la version de package la plus basse.</span><span class="sxs-lookup"><span data-stu-id="9e99b-192">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="9e99b-193">La spécification d'une version ou d'une plage de versions permet de lever ce doute.</span><span class="sxs-lookup"><span data-stu-id="9e99b-193">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="9e99b-194">Références dans les fichiers projet (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="9e99b-194">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a><span data-ttu-id="9e99b-195">Résolutions de version flottante</span><span class="sxs-lookup"><span data-stu-id="9e99b-195">Floating version resolutions</span></span> 

| <span data-ttu-id="9e99b-196">Version</span><span class="sxs-lookup"><span data-stu-id="9e99b-196">Version</span></span> | <span data-ttu-id="9e99b-197">Versions présentes sur le serveur</span><span class="sxs-lookup"><span data-stu-id="9e99b-197">Versions present on server</span></span> | <span data-ttu-id="9e99b-198">Résolution</span><span class="sxs-lookup"><span data-stu-id="9e99b-198">Resolution</span></span> | <span data-ttu-id="9e99b-199">Motif</span><span class="sxs-lookup"><span data-stu-id="9e99b-199">Reason</span></span> | <span data-ttu-id="9e99b-200">Notes</span><span class="sxs-lookup"><span data-stu-id="9e99b-200">Notes</span></span> |
|----------|--------------|-------------|-------------|-------------|
| * | <span data-ttu-id="9e99b-201">1.1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-201">1.1.0</span></span> <br> <span data-ttu-id="9e99b-202">1.1.1</span><span class="sxs-lookup"><span data-stu-id="9e99b-202">1.1.1</span></span> <br> <span data-ttu-id="9e99b-203">1.2.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-203">1.2.0</span></span> <br> <span data-ttu-id="9e99b-204">1.3.0-alpha</span><span class="sxs-lookup"><span data-stu-id="9e99b-204">1.3.0-alpha</span></span>  | <span data-ttu-id="9e99b-205">1.2.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-205">1.2.0</span></span> | <span data-ttu-id="9e99b-206">Version stable la plus élevée.</span><span class="sxs-lookup"><span data-stu-id="9e99b-206">The highest stable version.</span></span> |
| <span data-ttu-id="9e99b-207">1.1.\*</span><span class="sxs-lookup"><span data-stu-id="9e99b-207">1.1.\*</span></span> | <span data-ttu-id="9e99b-208">1.1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-208">1.1.0</span></span> <br> <span data-ttu-id="9e99b-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="9e99b-209">1.1.1</span></span> <br> <span data-ttu-id="9e99b-210">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="9e99b-210">1.1.2-alpha</span></span> <br> <span data-ttu-id="9e99b-211">1.2.0-alpha</span><span class="sxs-lookup"><span data-stu-id="9e99b-211">1.2.0-alpha</span></span> | <span data-ttu-id="9e99b-212">1.1.1</span><span class="sxs-lookup"><span data-stu-id="9e99b-212">1.1.1</span></span> | <span data-ttu-id="9e99b-213">Version stable la plus élevée qui respecte le modèle spécifié.</span><span class="sxs-lookup"><span data-stu-id="9e99b-213">The highest stable version that respects the specified pattern.</span></span>|
| <span data-ttu-id="9e99b-214">\* - \*</span><span class="sxs-lookup"><span data-stu-id="9e99b-214">\* - \*</span></span> | <span data-ttu-id="9e99b-215">1.1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-215">1.1.0</span></span> <br> <span data-ttu-id="9e99b-216">1.1.1</span><span class="sxs-lookup"><span data-stu-id="9e99b-216">1.1.1</span></span> <br> <span data-ttu-id="9e99b-217">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="9e99b-217">1.1.2-alpha</span></span> <br> <span data-ttu-id="9e99b-218">1.3.0-bêta</span><span class="sxs-lookup"><span data-stu-id="9e99b-218">1.3.0-beta</span></span>  | <span data-ttu-id="9e99b-219">1.3.0-bêta</span><span class="sxs-lookup"><span data-stu-id="9e99b-219">1.3.0-beta</span></span> | <span data-ttu-id="9e99b-220">La version la plus élevée, y compris les versions non stables.</span><span class="sxs-lookup"><span data-stu-id="9e99b-220">The highest version including the not stable versions.</span></span> | <span data-ttu-id="9e99b-221">Disponible dans Visual Studio version 16,6, NuGet version 5,6, kit SDK .NET Core version 3.1.300</span><span class="sxs-lookup"><span data-stu-id="9e99b-221">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |
| <span data-ttu-id="9e99b-222">1,1. *-*</span><span class="sxs-lookup"><span data-stu-id="9e99b-222">1.1.\* - \*</span></span> | <span data-ttu-id="9e99b-223">1.1.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-223">1.1.0</span></span> <br> <span data-ttu-id="9e99b-224">1.1.1</span><span class="sxs-lookup"><span data-stu-id="9e99b-224">1.1.1</span></span> <br> <span data-ttu-id="9e99b-225">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="9e99b-225">1.1.2-alpha</span></span> <br> <span data-ttu-id="9e99b-226">1.1.2-bêta</span><span class="sxs-lookup"><span data-stu-id="9e99b-226">1.1.2-beta</span></span> <br> <span data-ttu-id="9e99b-227">1.3.0-bêta</span><span class="sxs-lookup"><span data-stu-id="9e99b-227">1.3.0-beta</span></span>  | <span data-ttu-id="9e99b-228">1.1.2-bêta</span><span class="sxs-lookup"><span data-stu-id="9e99b-228">1.1.2-beta</span></span> | <span data-ttu-id="9e99b-229">Version la plus élevée respectant le modèle et incluant les versions non stables.</span><span class="sxs-lookup"><span data-stu-id="9e99b-229">The highest version respecting the pattern and including the not stable versions.</span></span> | <span data-ttu-id="9e99b-230">Disponible dans Visual Studio version 16,6, NuGet version 5,6, kit SDK .NET Core version 3.1.300</span><span class="sxs-lookup"><span data-stu-id="9e99b-230">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |

<span data-ttu-id="9e99b-231">**Références dans `packages.config` :**</span><span class="sxs-lookup"><span data-stu-id="9e99b-231">**References in `packages.config`:**</span></span>

<span data-ttu-id="9e99b-232">dans `packages.config`, chaque dépendance est répertoriée avec un attribut `version` exact utilisé lors de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="9e99b-232">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="9e99b-233">L'attribut `allowedVersions` n'est utilisé que pendant les opérations de mise à jour afin de limiter les versions avec lesquelles le package peut être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="9e99b-233">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="9e99b-234">**Références dans les fichiers `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="9e99b-234">**References in `.nuspec` files**</span></span>

<span data-ttu-id="9e99b-235">L'attribut `version` d'un élément `<dependency>` décrit les versions de plage acceptables pour une dépendance.</span><span class="sxs-lookup"><span data-stu-id="9e99b-235">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="9e99b-236">Numéros de version normalisés</span><span class="sxs-lookup"><span data-stu-id="9e99b-236">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="9e99b-237">Il s’agit d’un changement important pour NuGet 3.4 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="9e99b-237">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="9e99b-238">Lorsque vous obtenez des packages à partir d'un référentiel pendant l'installation, la réinstallation ou la restauration, NuGet 3.4+ traite les numéros de version comme suit :</span><span class="sxs-lookup"><span data-stu-id="9e99b-238">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="9e99b-239">Les zéros non significatifs sont supprimés des numéros de version :</span><span class="sxs-lookup"><span data-stu-id="9e99b-239">Leading zeroes are removed from version numbers:</span></span>

  <span data-ttu-id="9e99b-240">1,00 est traité comme 1,0 1.01.1 est traité comme 1.1.1 1.00.0.1 est traité comme 1.0.0.1</span><span class="sxs-lookup"><span data-stu-id="9e99b-240">1.00 is treated as 1.0 1.01.1 is treated as 1.1.1 1.00.0.1 is treated as 1.0.0.1</span></span>

- <span data-ttu-id="9e99b-241">Un zéro dans la quatrième partie du numéro de version sera omis</span><span class="sxs-lookup"><span data-stu-id="9e99b-241">A zero in the fourth part of the version number will be omitted</span></span>

  <span data-ttu-id="9e99b-242">1.0.0.0 est traité comme 1.0.0 1.0.01.0 est traité comme 1.0.1</span><span class="sxs-lookup"><span data-stu-id="9e99b-242">1.0.0.0 is treated as 1.0.0 1.0.01.0 is treated as 1.0.1</span></span>

- <span data-ttu-id="9e99b-243">Suppression des métadonnées de build SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="9e99b-243">SemVer 2.0.0 build metadata is removed</span></span>

  <span data-ttu-id="9e99b-244">1.0.7 + r3456 est traité comme 1.0.7</span><span class="sxs-lookup"><span data-stu-id="9e99b-244">1.0.7+r3456 is treated as 1.0.7</span></span>

<span data-ttu-id="9e99b-245">Les opérations `pack` et `restore` normalisent les versions lorsque cela est possible.</span><span class="sxs-lookup"><span data-stu-id="9e99b-245">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="9e99b-246">Pour les packages déjà construits, cette normalisation n'affecte pas les numéros de version dans les packages eux-mêmes ; elle affecte uniquement la façon dont NuGet mappe les versions lors de la résolution des dépendances.</span><span class="sxs-lookup"><span data-stu-id="9e99b-246">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="9e99b-247">Cependant, les dépôts de packages NuGet doivent traiter ces valeurs de la même manière que NuGet pour éviter la duplication des versions de packages.</span><span class="sxs-lookup"><span data-stu-id="9e99b-247">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="9e99b-248">Ainsi, un référentiel qui contient la version *1.0* d'un package ne doit pas également héberger la version *1.0.0* comme un package séparé et différent.</span><span class="sxs-lookup"><span data-stu-id="9e99b-248">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>

## <a name="where-nugetversion-diverges-from-semantic-versioning"></a><span data-ttu-id="9e99b-249">Où NuGetVersion divergent du contrôle de version sémantique</span><span class="sxs-lookup"><span data-stu-id="9e99b-249">Where NuGetVersion diverges from Semantic Versioning</span></span>

<span data-ttu-id="9e99b-250">Si vous souhaitez utiliser les versions de package NuGet par programmation, il est fortement recommandé d’utiliser [le package NuGet. Versioning](https://www.nuget.org/packages/NuGet.Versioning).</span><span class="sxs-lookup"><span data-stu-id="9e99b-250">If you want to programatically use NuGet package versions, it is strongly recommended to use [the package NuGet.Versioning](https://www.nuget.org/packages/NuGet.Versioning).</span></span> <span data-ttu-id="9e99b-251">La méthode statique `NuGetVersion.Parse(string)` peut être utilisée pour analyser les chaînes de version et `VersionComparer` peut être utilisée pour trier des `NuGetVersion` instances.</span><span class="sxs-lookup"><span data-stu-id="9e99b-251">The static method `NuGetVersion.Parse(string)` can be used to parse the version strings, and `VersionComparer` can be used to sort `NuGetVersion` instances.</span></span>

<span data-ttu-id="9e99b-252">Si vous implémentez la fonctionnalité NuGet dans un langage qui ne s’exécute pas sur .NET, voici la liste connue des différences entre `NuGetVersion` et le contrôle de version sémantique, et les raisons pour lesquelles une bibliothèque de contrôle de version sémantique existante peut ne pas fonctionner pour les packages déjà publiés sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="9e99b-252">If you are implementing NuGet functionality in a language that does not run on .NET, here are the known list of differences between `NuGetVersion` and Semantic Versioning, and the reasons why an existing Semantic Versioning library might not work for packages already published on nuget.org.</span></span>

1. <span data-ttu-id="9e99b-253">`NuGetVersion` prend en charge un quatrième segment `Revision` de version,, pour être compatible avec, ou un sur-ensemble de [`System.Version`](/dotnet/api/system.version) .</span><span class="sxs-lookup"><span data-stu-id="9e99b-253">`NuGetVersion` supports a 4th version segment, `Revision`, to be compatible with, or a superset of, [`System.Version`](/dotnet/api/system.version).</span></span> <span data-ttu-id="9e99b-254">Par conséquent, à l’exclusion de la version préliminaire et des étiquettes de métadonnées, une chaîne de version est `Major.Minor.Patch.Revision` .</span><span class="sxs-lookup"><span data-stu-id="9e99b-254">Therefore, excluding prerelease and metadata labels, a version string is `Major.Minor.Patch.Revision`.</span></span> <span data-ttu-id="9e99b-255">En fonction de la normalisation de la version décrite ci-dessus, si `Revision` est égal à zéro, il est omis de la chaîne de version normalisée.</span><span class="sxs-lookup"><span data-stu-id="9e99b-255">As per version normalization described above, if `Revision` is zero, it is omit from the normalized version string.</span></span>
2. <span data-ttu-id="9e99b-256">`NuGetVersion` seul le segment principal doit être défini.</span><span class="sxs-lookup"><span data-stu-id="9e99b-256">`NuGetVersion` only requires the major segment to be defined.</span></span> <span data-ttu-id="9e99b-257">Tous les autres sont facultatifs et sont équivalents à zéro.</span><span class="sxs-lookup"><span data-stu-id="9e99b-257">All others are optional, and are equivalent to zero.</span></span> <span data-ttu-id="9e99b-258">Cela signifie que `1` , `1.0` , `1.0.0` et `1.0.0.0` sont tous acceptés et égaux.</span><span class="sxs-lookup"><span data-stu-id="9e99b-258">This means that `1`, `1.0`, `1.0.0`, and `1.0.0.0` are all accepted and equal.</span></span>
3. <span data-ttu-id="9e99b-259">`NuGetVersion` utilise les comparaisons de chaînes case insenstive pour les composants en préversion.</span><span class="sxs-lookup"><span data-stu-id="9e99b-259">`NuGetVersion` uses case insenstive string comparisons for pre-release components.</span></span> <span data-ttu-id="9e99b-260">Cela signifie que `1.0.0-alpha` et `1.0.0-Alpha` sont égaux.</span><span class="sxs-lookup"><span data-stu-id="9e99b-260">This means that `1.0.0-alpha` and `1.0.0-Alpha` are equal.</span></span>
