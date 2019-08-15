---
title: Référence de version du package NuGet
description: Des détails précis sur la spécification des numéros de version et des plages pour d’autres packages dont dépend un package NuGet et sur la façon dont les dépendances sont installées.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019994"
---
# <a name="package-versioning"></a><span data-ttu-id="a2309-103">Contrôle de version des packages</span><span class="sxs-lookup"><span data-stu-id="a2309-103">Package versioning</span></span>

<span data-ttu-id="a2309-104">Un package spécifique est toujours référencé à l’aide de son identificateur de package et d’un numéro de version exact.</span><span class="sxs-lookup"><span data-stu-id="a2309-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="a2309-105">Par exemple, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sur NuGet.org dispose de plusieurs douzaines de packages spécifiques disponibles, allant de la version *4.1.10311* à la version *6.1.3* (la dernière version stable) et à une variété de versions préliminaires comme *6.2.0-beta1* .</span><span class="sxs-lookup"><span data-stu-id="a2309-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="a2309-106">Lorsque vous créez un package, vous affectez un numéro de version spécifique avec un suffixe de texte en préversion facultatif.</span><span class="sxs-lookup"><span data-stu-id="a2309-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="a2309-107">En revanche, lors de l’utilisation de packages, vous pouvez spécifier un numéro de version exact ou une plage de versions acceptables.</span><span class="sxs-lookup"><span data-stu-id="a2309-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="a2309-108">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="a2309-108">In this topic:</span></span>

- <span data-ttu-id="a2309-109">[Notions de base](#version-basics) sur les versions, y compris les suffixes de préversion.</span><span class="sxs-lookup"><span data-stu-id="a2309-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="a2309-110">Plages de versions et caractères génériques</span><span class="sxs-lookup"><span data-stu-id="a2309-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="a2309-111">Numéros de version normalisés</span><span class="sxs-lookup"><span data-stu-id="a2309-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="a2309-112">Notions de base sur les versions</span><span class="sxs-lookup"><span data-stu-id="a2309-112">Version basics</span></span>

<span data-ttu-id="a2309-113">Un numéro de version spécifique se présente sous la forme *major. minor. patch [-suffixe]* , où les composants ont les significations suivantes:</span><span class="sxs-lookup"><span data-stu-id="a2309-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="a2309-114">*Principal*: Modifications avec rupture</span><span class="sxs-lookup"><span data-stu-id="a2309-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="a2309-115">*Mineure*: Nouvelles fonctionnalités, offrant néanmoins une compatibilité descendante</span><span class="sxs-lookup"><span data-stu-id="a2309-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="a2309-116">*Correctif*: Correctifs de bogues à compatibilité descendante uniquement</span><span class="sxs-lookup"><span data-stu-id="a2309-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="a2309-117">*-Suffixe* (facultatif): trait d’Union suivi d’une chaîne désignant une préversion (selon le contrôle de [version sémantique ou la Convention SemVer 1,0](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="a2309-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="a2309-118">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="a2309-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="a2309-119">nuget.org rejette tout téléchargement de package qui ne dispose pas d’un numéro de version exact.</span><span class="sxs-lookup"><span data-stu-id="a2309-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="a2309-120">La version doit être spécifiée dans le `.nuspec` fichier projet ou utilisé pour créer le package.</span><span class="sxs-lookup"><span data-stu-id="a2309-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="a2309-121">Versions préliminaires</span><span class="sxs-lookup"><span data-stu-id="a2309-121">Pre-release versions</span></span>

<span data-ttu-id="a2309-122">Techniquement parlant, les créateurs de packages peuvent utiliser n’importe quelle chaîne comme suffixe pour désigner une préversion, car NuGet traite une telle version comme une version préliminaire et n’effectue aucune autre interprétation.</span><span class="sxs-lookup"><span data-stu-id="a2309-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="a2309-123">Autrement dit, NuGet affiche la chaîne de version complète dans n’importe quelle interface utilisateur, en laissant toute interprétation de la signification du suffixe au consommateur.</span><span class="sxs-lookup"><span data-stu-id="a2309-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="a2309-124">Cela dit, les développeurs de packages suivent généralement les conventions de nommage reconnues:</span><span class="sxs-lookup"><span data-stu-id="a2309-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="a2309-125">`-alpha`: Version alpha, généralement utilisée pour les travaux en cours et l’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="a2309-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="a2309-126">`-beta`: Version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.</span><span class="sxs-lookup"><span data-stu-id="a2309-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="a2309-127">`-rc`: Version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.</span><span class="sxs-lookup"><span data-stu-id="a2309-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="a2309-128">NuGet 4.3.0 + prend en charge [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de préversion avec la notation par points, comme dans la version *1.0.1-Build. 23*.</span><span class="sxs-lookup"><span data-stu-id="a2309-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="a2309-129">La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="a2309-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="a2309-130">Vous pouvez utiliser un formulaire comme *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="a2309-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="a2309-131">Lors de la résolution des références de package et que plusieurs versions de package diffèrent uniquement par le suffixe, NuGet choisit une version sans suffixe en premier, puis applique la précédence aux versions préliminaires dans l’ordre alphabétique inversé.</span><span class="sxs-lookup"><span data-stu-id="a2309-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="a2309-132">Par exemple, les versions suivantes sont choisies dans l’ordre exact indiqué:</span><span class="sxs-lookup"><span data-stu-id="a2309-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="a2309-133">Contrôle de version de sémantique 2.0.0</span><span class="sxs-lookup"><span data-stu-id="a2309-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="a2309-134">Avec NuGet 4.3.0 + et Visual Studio 2017 version 15.3 +, NuGet prend en charge le contrôle de [version sémantique 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="a2309-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="a2309-135">Certaines sémantiques de SemVer v 2.0.0 ne sont pas prises en charge dans les clients plus anciens.</span><span class="sxs-lookup"><span data-stu-id="a2309-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="a2309-136">NuGet considère qu’une version de package est spécifique à SemVer v 2.0.0 si l’une des affirmations suivantes est vraie:</span><span class="sxs-lookup"><span data-stu-id="a2309-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="a2309-137">L’étiquette de préversion est séparée par des points, par exemple, *1.0.0-alpha. 1*</span><span class="sxs-lookup"><span data-stu-id="a2309-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="a2309-138">La version comporte des métadonnées de build, par exemple, *1.0.0 + githash*</span><span class="sxs-lookup"><span data-stu-id="a2309-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="a2309-139">Pour nuget.org, un package est défini en tant que package SemVer v 2.0.0 si l’une des affirmations suivantes est vraie:</span><span class="sxs-lookup"><span data-stu-id="a2309-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="a2309-140">La version du package est conforme à SemVer v 2.0.0, mais pas à SemVer v 1.0.0 conforme, comme défini ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a2309-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="a2309-141">Les plages de versions de dépendance du package ont une version minimale ou maximale qui est conforme à SemVer v 2.0.0, mais pas à SemVer v 1.0.0 conforme, définie ci-dessus. par exemple, *[1.0.0-alpha. 1,)* .</span><span class="sxs-lookup"><span data-stu-id="a2309-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="a2309-142">Si vous chargez un package spécifique à SemVer v 2.0.0 sur nuget.org, le package est invisible pour les clients plus anciens et n’est disponible que pour les clients NuGet suivants:</span><span class="sxs-lookup"><span data-stu-id="a2309-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="a2309-143">NuGet 4.3.0 +</span><span class="sxs-lookup"><span data-stu-id="a2309-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="a2309-144">Visual Studio 2017 version 15.3 +</span><span class="sxs-lookup"><span data-stu-id="a2309-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="a2309-145">Visual Studio 2015 avec [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="a2309-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="a2309-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="a2309-146">dotnet</span></span>
  - <span data-ttu-id="a2309-147">dotnetcore. exe (kit de développement logiciel (SDK) .NET 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="a2309-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="a2309-148">Clients tiers:</span><span class="sxs-lookup"><span data-stu-id="a2309-148">Third-party clients:</span></span>

- <span data-ttu-id="a2309-149">Avenant JetBrains</span><span class="sxs-lookup"><span data-stu-id="a2309-149">JetBrains Rider</span></span>
- <span data-ttu-id="a2309-150">Paket version 5.0 +</span><span class="sxs-lookup"><span data-stu-id="a2309-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="a2309-151">Plages de versions et caractères génériques</span><span class="sxs-lookup"><span data-stu-id="a2309-151">Version ranges and wildcards</span></span>

<span data-ttu-id="a2309-152">Lorsque vous faites référence à des dépendances de package, NuGet prend en charge l’utilisation de la notation d’intervalle pour spécifier les plages de versions, résumée comme suit:</span><span class="sxs-lookup"><span data-stu-id="a2309-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="a2309-153">Notation</span><span class="sxs-lookup"><span data-stu-id="a2309-153">Notation</span></span> | <span data-ttu-id="a2309-154">Règle appliquée</span><span class="sxs-lookup"><span data-stu-id="a2309-154">Applied rule</span></span> | <span data-ttu-id="a2309-155">Description</span><span class="sxs-lookup"><span data-stu-id="a2309-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="a2309-156">1.0</span><span class="sxs-lookup"><span data-stu-id="a2309-156">1.0</span></span> | <span data-ttu-id="a2309-157">x ≥ 1,0</span><span class="sxs-lookup"><span data-stu-id="a2309-157">x ≥ 1.0</span></span> | <span data-ttu-id="a2309-158">Version minimale, incluse</span><span class="sxs-lookup"><span data-stu-id="a2309-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="a2309-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="a2309-159">(1.0,)</span></span> | <span data-ttu-id="a2309-160">x > 1,0</span><span class="sxs-lookup"><span data-stu-id="a2309-160">x > 1.0</span></span> | <span data-ttu-id="a2309-161">Version minimale, exclusive</span><span class="sxs-lookup"><span data-stu-id="a2309-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="a2309-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="a2309-162">[1.0]</span></span> | <span data-ttu-id="a2309-163">x = = 1,0</span><span class="sxs-lookup"><span data-stu-id="a2309-163">x == 1.0</span></span> | <span data-ttu-id="a2309-164">Correspondance de version exacte</span><span class="sxs-lookup"><span data-stu-id="a2309-164">Exact version match</span></span> |
| <span data-ttu-id="a2309-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="a2309-165">(,1.0]</span></span> | <span data-ttu-id="a2309-166">x ≤ 1,0</span><span class="sxs-lookup"><span data-stu-id="a2309-166">x ≤ 1.0</span></span> | <span data-ttu-id="a2309-167">Version maximale, inclusive</span><span class="sxs-lookup"><span data-stu-id="a2309-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="a2309-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="a2309-168">(,1.0)</span></span> | <span data-ttu-id="a2309-169">x < 1,0</span><span class="sxs-lookup"><span data-stu-id="a2309-169">x < 1.0</span></span> | <span data-ttu-id="a2309-170">Version maximale, exclusive</span><span class="sxs-lookup"><span data-stu-id="a2309-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="a2309-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="a2309-171">[1.0,2.0]</span></span> | <span data-ttu-id="a2309-172">1,0 ≤ x ≤ 2,0</span><span class="sxs-lookup"><span data-stu-id="a2309-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="a2309-173">Plage exacte, inclusive</span><span class="sxs-lookup"><span data-stu-id="a2309-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="a2309-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="a2309-174">(1.0,2.0)</span></span> | <span data-ttu-id="a2309-175">1,0 < x < 2,0</span><span class="sxs-lookup"><span data-stu-id="a2309-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="a2309-176">Plage exacte, exclusive</span><span class="sxs-lookup"><span data-stu-id="a2309-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="a2309-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="a2309-177">[1.0,2.0)</span></span> | <span data-ttu-id="a2309-178">1,0 ≤ x < 2,0</span><span class="sxs-lookup"><span data-stu-id="a2309-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="a2309-179">Version maximale et minimale inclusive mixte</span><span class="sxs-lookup"><span data-stu-id="a2309-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="a2309-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="a2309-180">(1.0)</span></span>    | <span data-ttu-id="a2309-181">non valide</span><span class="sxs-lookup"><span data-stu-id="a2309-181">invalid</span></span> | <span data-ttu-id="a2309-182">non valide</span><span class="sxs-lookup"><span data-stu-id="a2309-182">invalid</span></span> |

<span data-ttu-id="a2309-183">Lors de l’utilisation du format PackageReference, NuGet prend également en charge l' \*utilisation d’une notation générique,, pour les parties de suffixe majeure, mineure, de correctif et de préversion du nombre.</span><span class="sxs-lookup"><span data-stu-id="a2309-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="a2309-184">Les caractères génériques ne sont pas pris `packages.config` en charge avec le format.</span><span class="sxs-lookup"><span data-stu-id="a2309-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="a2309-185">Les plages de versions dans PackageReference incluent des versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="a2309-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="a2309-186">Par défaut, les versions flottantes ne résolvent pas les versions préliminaires sauf si elles sont activées.</span><span class="sxs-lookup"><span data-stu-id="a2309-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="a2309-187">Pour connaître l’état de la demande de fonctionnalité associée, consultez le [problème 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="a2309-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="a2309-188">Exemples</span><span class="sxs-lookup"><span data-stu-id="a2309-188">Examples</span></span>

<span data-ttu-id="a2309-189">Spécifiez toujours une version ou une plage de versions pour les dépendances `packages.config` de package dans `.nuspec` les fichiers projet, les fichiers et les fichiers.</span><span class="sxs-lookup"><span data-stu-id="a2309-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="a2309-190">Sans une version ou une plage de versions, NuGet 2.8. x et les versions antérieures sélectionnent la dernière version disponible du package lors de la résolution d’une dépendance, tandis que NuGet 3. x et versions ultérieures sélectionnent la version de package la plus basse.</span><span class="sxs-lookup"><span data-stu-id="a2309-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="a2309-191">La spécification d’une version ou d’une plage de versions évite cette incertitude.</span><span class="sxs-lookup"><span data-stu-id="a2309-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="a2309-192">Références dans les fichiers projet (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="a2309-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="a2309-193">**Références dans `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="a2309-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="a2309-194">Dans `packages.config`, chaque dépendance est indiquée avec un attribut `version` exact qui est utilisé lors de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="a2309-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="a2309-195">L' `allowedVersions` attribut est utilisé uniquement pendant les opérations de mise à jour pour limiter les versions vers lesquelles le package peut être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="a2309-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="a2309-196">**Références dans `.nuspec` les fichiers**</span><span class="sxs-lookup"><span data-stu-id="a2309-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="a2309-197">L' `version` attribut d’un `<dependency>` élément décrit les versions de plage acceptables pour une dépendance.</span><span class="sxs-lookup"><span data-stu-id="a2309-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="a2309-198">Numéros de version normalisés</span><span class="sxs-lookup"><span data-stu-id="a2309-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="a2309-199">Il s’agit d’une modification avec rupture pour NuGet 3,4 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="a2309-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="a2309-200">Lors de l’obtention de packages à partir d’un référentiel pendant les opérations d’installation, de réinstallation ou de restauration, NuGet 3.4 + traite les numéros de version comme suit:</span><span class="sxs-lookup"><span data-stu-id="a2309-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="a2309-201">Les zéros non significatifs sont supprimés des numéros de version:</span><span class="sxs-lookup"><span data-stu-id="a2309-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="a2309-202">Un zéro dans la quatrième partie du numéro de version sera omis</span><span class="sxs-lookup"><span data-stu-id="a2309-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="a2309-203">`pack`et `restore` les opérations normalisent les versions chaque fois que cela est possible.</span><span class="sxs-lookup"><span data-stu-id="a2309-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="a2309-204">Pour les packages déjà générés, cette normalisation n’affecte pas les numéros de version dans les packages eux-mêmes. elle affecte uniquement la manière dont NuGet correspond aux versions lors de la résolution des dépendances.</span><span class="sxs-lookup"><span data-stu-id="a2309-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="a2309-205">Toutefois, les dépôts de packages NuGet doivent traiter ces valeurs de la même façon que NuGet pour empêcher la duplication de version de package.</span><span class="sxs-lookup"><span data-stu-id="a2309-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="a2309-206">Par conséquent, un référentiel qui contient la version *1,0* d’un package ne doit pas héberger également la version *1.0.0* comme un package distinct et différent.</span><span class="sxs-lookup"><span data-stu-id="a2309-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
