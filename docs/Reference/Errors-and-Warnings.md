---
title: "Restauration des erreurs et avertissements référence NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informations de référence complètes pour les avertissements et erreurs émises à partir de NuGet pendant la restauration de package"
keywords: Erreurs de NuGet, les avertissements de NuGet, les diagnostics
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
ms.openlocfilehash: c7d77af04744888ce8af92d617a2ffc7daef4eb0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="5e777-104">Erreurs et avertissements</span><span class="sxs-lookup"><span data-stu-id="5e777-104">Errors and warnings</span></span>

<span data-ttu-id="5e777-105">Dans NuGet 4.3.0, erreurs et avertissements sont numérotées comme décrit dans cette rubrique et fournissent des informations détaillées pour vous aider à résoudre les problèmes rencontrés.</span><span class="sxs-lookup"><span data-stu-id="5e777-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="5e777-106">Les erreurs et les avertissements répertoriés ici sont uniquement disponibles avec [basée sur les PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) NuGet 4.3.0 et projets.</span><span class="sxs-lookup"><span data-stu-id="5e777-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="5e777-107">NuGet honore également des propriétés MSBuild pour supprimer les avertissements ou les élever à erreurs.</span><span class="sxs-lookup"><span data-stu-id="5e777-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="5e777-108">Pour plus d’informations, consultez [Comment : supprimer les avertissements du compilateur](/visualstudio/ide/how-to-suppress-compiler-warnings) dans la documentation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5e777-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="5e777-109">**Erreurs**</span><span class="sxs-lookup"><span data-stu-id="5e777-109">**Errors**</span></span>

| <span data-ttu-id="5e777-110">Regrouper</span><span class="sxs-lookup"><span data-stu-id="5e777-110">Group</span></span> | <span data-ttu-id="5e777-111">Numéros d’erreur</span><span class="sxs-lookup"><span data-stu-id="5e777-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="5e777-112">Erreurs d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="5e777-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="5e777-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="5e777-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="5e777-114">Erreurs de package et de projet manquants</span><span class="sxs-lookup"><span data-stu-id="5e777-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="5e777-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (précédemment NU1607) [NU1108](#nu1108) (précédemment NU1606)</span><span class="sxs-lookup"><span data-stu-id="5e777-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="5e777-116">Erreurs de compatibilité</span><span class="sxs-lookup"><span data-stu-id="5e777-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="5e777-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="5e777-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="5e777-118">**Avertissements**</span><span class="sxs-lookup"><span data-stu-id="5e777-118">**Warnings**</span></span>

| <span data-ttu-id="5e777-119">Regrouper</span><span class="sxs-lookup"><span data-stu-id="5e777-119">Group</span></span> | <span data-ttu-id="5e777-120">Numéros d’avertissement</span><span class="sxs-lookup"><span data-stu-id="5e777-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="5e777-121">Avertissements d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="5e777-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="5e777-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="5e777-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="5e777-123">Avertissements de version de package inattendue</span><span class="sxs-lookup"><span data-stu-id="5e777-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="5e777-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="5e777-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="5e777-125">Avertissements de conflit de programme de résolution</span><span class="sxs-lookup"><span data-stu-id="5e777-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="5e777-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="5e777-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="5e777-127">Avertissements de secours de package</span><span class="sxs-lookup"><span data-stu-id="5e777-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="5e777-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="5e777-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="5e777-129">Flux d’avertissements</span><span class="sxs-lookup"><span data-stu-id="5e777-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="5e777-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="5e777-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="5e777-131">Avertissements et erreurs internes de NuGet</span><span class="sxs-lookup"><span data-stu-id="5e777-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="5e777-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="5e777-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="5e777-133">Erreurs d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="5e777-133">Invalid input errors</span></span>

<span data-ttu-id="5e777-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="5e777-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="5e777-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="5e777-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-136">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-136">**Issue**</span></span> | <span data-ttu-id="5e777-137">Le projet ne contient pas une ou plusieurs infrastructures.</span><span class="sxs-lookup"><span data-stu-id="5e777-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="5e777-138">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-138">**Common causes**</span></span> | <span data-ttu-id="5e777-139">Le projet ne contient pas un `TargetFramework` ou `TargetFrameworks` propriété.</span><span class="sxs-lookup"><span data-stu-id="5e777-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="5e777-140">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-140">**Example message**</span></span> | <span data-ttu-id="5e777-141">*Le projet projA ne spécifie pas les versions .NET Framework cible dans c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="5e777-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="5e777-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="5e777-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-143">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-143">**Issue**</span></span> | <span data-ttu-id="5e777-144">Combinaison non valide d’entrées avec un mot clé clair.</span><span class="sxs-lookup"><span data-stu-id="5e777-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="5e777-145">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-145">**Common causes**</span></span> | <span data-ttu-id="5e777-146">CLEAR ne peut pas être combiné avec d’autres entrées.</span><span class="sxs-lookup"><span data-stu-id="5e777-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="5e777-147">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-147">**Example message**</span></span> | <span data-ttu-id="5e777-148">*« CLAIR » ne peut pas être utilisé conjointement avec d’autres valeurs*</span><span class="sxs-lookup"><span data-stu-id="5e777-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="5e777-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="5e777-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-150">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-150">**Issue**</span></span> | <span data-ttu-id="5e777-151">`PackageTargetFallback`et `AssetTargetFallback` fournir un comportement différent pour la sélection des ressources et ne peut pas être utilisées ensemble.</span><span class="sxs-lookup"><span data-stu-id="5e777-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="5e777-152">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-152">**Common causes**</span></span> | <span data-ttu-id="5e777-153">Les deux `PackageTargetFallback` et `AssetTargetFallback` existent dans le projet.</span><span class="sxs-lookup"><span data-stu-id="5e777-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="5e777-154">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-154">**Example message**</span></span> | <span data-ttu-id="5e777-155">*PackageTargetFallback et AssetTargetFallback ne peuvent pas être utilisées ensemble. Supprimez les références de PackageTargetFallback(deprecated) à partir de l’environnement de projet.*</span><span class="sxs-lookup"><span data-stu-id="5e777-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="5e777-156">Erreurs de package et de projet manquants</span><span class="sxs-lookup"><span data-stu-id="5e777-156">Missing package and project errors</span></span>

<span data-ttu-id="5e777-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="5e777-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="5e777-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="5e777-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-159">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-159">**Issue**</span></span> | <span data-ttu-id="5e777-160">Un groupe de dépendances ne pas être résolu.</span><span class="sxs-lookup"><span data-stu-id="5e777-160">A dependency group not be resolved.</span></span> <span data-ttu-id="5e777-161">Il s’agit d’un problème générique pour les types qui ne sont pas des packages ou des projets.</span><span class="sxs-lookup"><span data-stu-id="5e777-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="5e777-162">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-162">**Common causes**</span></span> | <span data-ttu-id="5e777-163">Le projet contient une dépendance sur un élément qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="5e777-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="5e777-164">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-164">**Example message**</span></span> | <span data-ttu-id="5e777-165">*Impossible de résoudre System.Missing pour net45*</span><span class="sxs-lookup"><span data-stu-id="5e777-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="5e777-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="5e777-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-167">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-167">**Issue**</span></span> | <span data-ttu-id="5e777-168">Impossible de trouver le package sur des sources.</span><span class="sxs-lookup"><span data-stu-id="5e777-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="5e777-169">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-169">**Common causes**</span></span> | <span data-ttu-id="5e777-170">La source du package approprié est manquante ou l’identificateur de package est incorrect.</span><span class="sxs-lookup"><span data-stu-id="5e777-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="5e777-171">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-171">**Example message**</span></span> | <span data-ttu-id="5e777-172">*Impossible de trouver le package System.Missing. Aucun package n’existe avec cet id de source (s) : dotnet cœur, roslyn-dotnet, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="5e777-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="5e777-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="5e777-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-174">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-174">**Issue**</span></span> | <span data-ttu-id="5e777-175">L’identificateur du package est trouvé, mais une version dans la plage de dépendance spécifié est introuvable sur une des sources.</span><span class="sxs-lookup"><span data-stu-id="5e777-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="5e777-176">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-176">**Common causes**</span></span> | <span data-ttu-id="5e777-177">La source du package approprié est manquante ou la plage de dépendance est incorrecte.</span><span class="sxs-lookup"><span data-stu-id="5e777-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="5e777-178">La plage peut être spécifiée par un package et non à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5e777-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="5e777-179">L’utilisateur peut être amené à basculer vers une version disponible si ce package est référencé directement par le projet.</span><span class="sxs-lookup"><span data-stu-id="5e777-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="5e777-180">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-180">**Example message**</span></span> | <span data-ttu-id="5e777-181">*Impossible de trouver le package NuGet.Versioning avec la version (> = 9.0.1)<br/> -30 de trouvé ou les versions dans nuget.org [plus proche de la version : 4.0.0]<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -trouvé le 9 versions dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032]<br/> -trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet*</span><span class="sxs-lookup"><span data-stu-id="5e777-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="5e777-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="5e777-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-183">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-183">**Issue**</span></span> | <span data-ttu-id="5e777-184">Aucune version stable ont été trouvées dans la plage de dépendance.</span><span class="sxs-lookup"><span data-stu-id="5e777-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="5e777-185">Versions préliminaires ont été trouvées, mais ne sont pas autorisées.</span><span class="sxs-lookup"><span data-stu-id="5e777-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="5e777-186">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-186">**Common causes**</span></span> | <span data-ttu-id="5e777-187">Le projet spécifié une version stable pour la plage de dépendance.</span><span class="sxs-lookup"><span data-stu-id="5e777-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="5e777-188">Les utilisateurs doivent modifier la plage de versions pour inclure les versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="5e777-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="5e777-189">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-189">**Example message**</span></span> | <span data-ttu-id="5e777-190">*Impossible de trouver un package stable NuGet.Versioning avec la version (> = 3.0.0)<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -versions 9 de trouvé dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032] <br/> -Trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet*</span><span class="sxs-lookup"><span data-stu-id="5e777-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="5e777-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="5e777-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-192">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-192">**Issue**</span></span> | <span data-ttu-id="5e777-193">Un ProjectReference pointe vers un fichier qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="5e777-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="5e777-194">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-194">**Common causes**</span></span> | <span data-ttu-id="5e777-195">Il manque le fichier projet à partir du disque ou la référence est incorrecte.</span><span class="sxs-lookup"><span data-stu-id="5e777-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="5e777-196">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-196">**Example message**</span></span> | <span data-ttu-id="5e777-197">*Référence de projet n’existe pas de 'c:\a.csproj'. Vérifiez que la référence de projet est valide et que le fichier projet existe.*</span><span class="sxs-lookup"><span data-stu-id="5e777-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="5e777-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="5e777-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-199">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-199">**Issue**</span></span> | <span data-ttu-id="5e777-200">Le fichier de projet existe mais aucune information de restauration a été fournie pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="5e777-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="5e777-201">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-201">**Common causes**</span></span> | <span data-ttu-id="5e777-202">Dans Visual Studio, cela peut signifier que le projet est déchargé.</span><span class="sxs-lookup"><span data-stu-id="5e777-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="5e777-203">À partir de la ligne de commande, cela peut signifier que le fichier est endommagé ou qu’il ne contient pas personnalisé après la cible d’importations nécessaire pour la restauration lire le projet.</span><span class="sxs-lookup"><span data-stu-id="5e777-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="5e777-204">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-204">**Example message**</span></span> | <span data-ttu-id="5e777-205">*Impossible de lire les informations de projet pour 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.*</span><span class="sxs-lookup"><span data-stu-id="5e777-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="5e777-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="5e777-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-207">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-207">**Issue**</span></span> | <span data-ttu-id="5e777-208">Contraintes de dépendances ne peut pas être résolus.</span><span class="sxs-lookup"><span data-stu-id="5e777-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="5e777-209">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-209">**Common causes**</span></span> | <span data-ttu-id="5e777-210">Les packages contiennent la dépendance sur les versions exactes d’un package au lieu de plages ouvertes.</span><span class="sxs-lookup"><span data-stu-id="5e777-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="5e777-211">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-211">**Example message**</span></span> | <span data-ttu-id="5e777-212">*Impossible de satisfaire les requêtes en conflit pour {id} : {chemin d’accès de conflit} Framework : {graphique cible}*</span><span class="sxs-lookup"><span data-stu-id="5e777-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="5e777-213">NU1107 (précédemment NU1607)</span><span class="sxs-lookup"><span data-stu-id="5e777-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-214">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-214">**Issue**</span></span> | <span data-ttu-id="5e777-215">Impossible de résoudre les contraintes de dépendances entre les packages.</span><span class="sxs-lookup"><span data-stu-id="5e777-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="5e777-216">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-216">**Common causes**</span></span> | <span data-ttu-id="5e777-217">Les packages avec des contraintes de dépendance sur les versions exactes ne permettent pas d’autres packages d’augmenter la version, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5e777-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="5e777-218">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-218">**Example message**</span></span> | <span data-ttu-id="5e777-219">*Conflit de version détecté pour NuGet.Versioning. Référencer le package directement à partir du projet pour résoudre ce problème.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="5e777-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="5e777-220">NU1108 (précédemment NU1606)</span><span class="sxs-lookup"><span data-stu-id="5e777-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-221">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-221">**Issue**</span></span> | <span data-ttu-id="5e777-222">Une dépendance circulaire a été détectée.</span><span class="sxs-lookup"><span data-stu-id="5e777-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="5e777-223">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-223">**Common causes**</span></span> | <span data-ttu-id="5e777-224">Un package a été créé correctement.</span><span class="sxs-lookup"><span data-stu-id="5e777-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="5e777-225">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-225">**Example message**</span></span> | <span data-ttu-id="5e777-226">*Cycle détecté : A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="5e777-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="5e777-227">Erreurs de compatibilité</span><span class="sxs-lookup"><span data-stu-id="5e777-227">Compatibility errors</span></span>

<span data-ttu-id="5e777-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="5e777-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="5e777-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="5e777-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-230">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-230">**Issue**</span></span> | <span data-ttu-id="5e777-231">Un projet de dépendance ne contient pas une infrastructure compatible avec le projet actuel.</span><span class="sxs-lookup"><span data-stu-id="5e777-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="5e777-232">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-232">**Common causes**</span></span> | <span data-ttu-id="5e777-233">La version du projet cible est une version supérieure à celle du projet de consommation.</span><span class="sxs-lookup"><span data-stu-id="5e777-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="5e777-234">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-234">**Example message**</span></span> | <span data-ttu-id="5e777-235">*Projet WAN n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Project prend en charge WAN :<br/> -netstandard1.6 (. NETStandard, Version = version 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = version 1.0)*</span><span class="sxs-lookup"><span data-stu-id="5e777-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="5e777-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="5e777-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-237">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-237">**Issue**</span></span> | <span data-ttu-id="5e777-238">Un package de dépendance ne contient pas toutes les ressources compatibles avec le projet.</span><span class="sxs-lookup"><span data-stu-id="5e777-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="5e777-239">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-239">**Common causes**</span></span> | <span data-ttu-id="5e777-240">Le package ne prend pas en charge la version du projet cible.</span><span class="sxs-lookup"><span data-stu-id="5e777-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="5e777-241">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-241">**Example message**</span></span> | <span data-ttu-id="5e777-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Package prend en charge System.ComponentModel.EventBasedAsync 4.0.11 :<br/> -monoandroid10 (MonoAndroid, Version = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (. NETFramework, Version = v4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. NETStandard, Version = v1.0)<br/> -portable-net45 + 8 + wp8 + wpa81 (. NETPortable, Version = v0.0, profil = Profile259)<br/> -win8 (Windows, Version = v8.0)<br/> -wp8 (WindowsPhone, Version = v8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v8.1)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="5e777-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="5e777-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="5e777-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-244">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-244">**Issue**</span></span> | <span data-ttu-id="5e777-245">Le package ne prend pas en charge du projet `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="5e777-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="5e777-246">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-246">**Common causes**</span></span> | <span data-ttu-id="5e777-247">Le package ne prend pas en charge en cours `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="5e777-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="5e777-248">Modifier la `RuntimeIdentifier` valeurs utilisées dans le projet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5e777-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="5e777-249">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-249">**Example message**</span></span> | <span data-ttu-id="5e777-250">*System.Example 1.0.0 fournit un assembly de référence de la compilation pour.dll sur net461, mais il n’existe aucun assembly au moment de l’exécution compatible.*</span><span class="sxs-lookup"><span data-stu-id="5e777-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="5e777-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="5e777-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-252">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-252">**Issue**</span></span> | <span data-ttu-id="5e777-253">Le package requiert des fonctionnalités ou des structures non prises en charge par la version installée de NuGet.</span><span class="sxs-lookup"><span data-stu-id="5e777-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="5e777-254">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-254">**Common causes**</span></span> | <span data-ttu-id="5e777-255">Mettre à niveau NuGet pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="5e777-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="5e777-256">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-256">**Example message**</span></span> | <span data-ttu-id="5e777-257">*Le package 'NuGet.Versioning' nécessite '5.0.0' version du client de NuGet ou version ultérieure, mais la version NuGet actuelle est '4.3.0'. Pour mettre à niveau NuGet, accédez à http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="5e777-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="5e777-258">Avertissements d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="5e777-258">Invalid input warnings</span></span>

<span data-ttu-id="5e777-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="5e777-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="5e777-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="5e777-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-261">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-261">**Issue**</span></span> | <span data-ttu-id="5e777-262">La restauration du projet tente de fonctionner sur n’a été trouvé.</span><span class="sxs-lookup"><span data-stu-id="5e777-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="5e777-263">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-263">**Common causes**</span></span> | <span data-ttu-id="5e777-264">Le projet est manquant.</span><span class="sxs-lookup"><span data-stu-id="5e777-264">The project is missing.</span></span> |
| <span data-ttu-id="5e777-265">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-265">**Example message**</span></span> | <span data-ttu-id="5e777-266">*Le dossier 'c:\projects\a' ne contient pas de projet à restaurer.*</span><span class="sxs-lookup"><span data-stu-id="5e777-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="5e777-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="5e777-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-268">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-268">**Issue**</span></span> | <span data-ttu-id="5e777-269">`RuntimeSupports`contient un profil non valide.</span><span class="sxs-lookup"><span data-stu-id="5e777-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="5e777-270">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-270">**Common causes**</span></span> | <span data-ttu-id="5e777-271">Le profil prend en charge est introuvable dans un `runtime.json` fichier issues des packages de dépendance actuel.</span><span class="sxs-lookup"><span data-stu-id="5e777-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="5e777-272">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-272">**Example message**</span></span> | <span data-ttu-id="5e777-273">*Profil de compatibilité inconnu : aaa*</span><span class="sxs-lookup"><span data-stu-id="5e777-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="5e777-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="5e777-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-275">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-275">**Issue**</span></span> | <span data-ttu-id="5e777-276">Un projet de dépendance n’importe pas les cibles de restauration de NuGet.</span><span class="sxs-lookup"><span data-stu-id="5e777-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="5e777-277">Cela revient à NU1105 mais ici le projet est ignoré et ignorés au lieu de provoquer l’échec de restauration tous.</span><span class="sxs-lookup"><span data-stu-id="5e777-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="5e777-278">Dans les solutions complexes il existe souvent des autres types de projets qui n’acceptent pas de restauration.</span><span class="sxs-lookup"><span data-stu-id="5e777-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="5e777-279">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-279">**Common causes**</span></span> | <span data-ttu-id="5e777-280">Cela peut se produire pour les projets qui n’importent pas de propriétés/cibles communes qui importer automatiquement la restauration.</span><span class="sxs-lookup"><span data-stu-id="5e777-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="5e777-281">Si le projet n’a pas besoin d’être restauré ce message peut être ignoré.</span><span class="sxs-lookup"><span data-stu-id="5e777-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="5e777-282">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-282">**Example message**</span></span> | <span data-ttu-id="5e777-283">*Ignorer la restauration de projet 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.*</span><span class="sxs-lookup"><span data-stu-id="5e777-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="5e777-284">Avertissements de version de package inattendue</span><span class="sxs-lookup"><span data-stu-id="5e777-284">Unexpected package version warnings</span></span>

<span data-ttu-id="5e777-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="5e777-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="5e777-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="5e777-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-287">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-287">**Issue**</span></span> | <span data-ttu-id="5e777-288">Une dépendance directe a été agrandir à une version plus élevée que le projet spécifié.</span><span class="sxs-lookup"><span data-stu-id="5e777-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="5e777-289">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-289">**Common causes**</span></span> | <span data-ttu-id="5e777-290">Un autre package de dépendance requis d’une version ultérieure et augmenté le package.</span><span class="sxs-lookup"><span data-stu-id="5e777-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="5e777-291">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-291">**Example message**</span></span> | <span data-ttu-id="5e777-292">*Dépendance spécifiée était NuGet.Versioning (> = 3.5.0), mais se terminait avec NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="5e777-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="5e777-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="5e777-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-294">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-294">**Issue**</span></span> | <span data-ttu-id="5e777-295">Une dépendance de package est manquant dans une limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="5e777-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="5e777-296">Cela n’autorise pas la restauration rechercher la *meilleure correspondance*.</span><span class="sxs-lookup"><span data-stu-id="5e777-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="5e777-297">Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="5e777-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="5e777-298">Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5e777-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="5e777-299">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-299">**Common causes**</span></span> | <span data-ttu-id="5e777-300">Il s’agit généralement d’un erreur de création de package.</span><span class="sxs-lookup"><span data-stu-id="5e777-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="5e777-301">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-301">**Example message**</span></span> | <span data-ttu-id="5e777-302">*NuGet.Packaging 4.0.0 ne fournit pas une limite inférieure inclusive de dépendance NuGet.Versioning (3.5.0 >). Une meilleure correspondance approximative de 3.6.0 a été résolue.*</span><span class="sxs-lookup"><span data-stu-id="5e777-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="5e777-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="5e777-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-304">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-304">**Issue**</span></span> | <span data-ttu-id="5e777-305">Une dépendance de package spécifié une version qui est introuvable.</span><span class="sxs-lookup"><span data-stu-id="5e777-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="5e777-306">Une version ultérieure a été utilisée à la place, ce qui diffère du package qui a été créé par rapport à.</span><span class="sxs-lookup"><span data-stu-id="5e777-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="5e777-307">Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*.</span><span class="sxs-lookup"><span data-stu-id="5e777-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="5e777-308">Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="5e777-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="5e777-309">Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5e777-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="5e777-310">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-310">**Common causes**</span></span> | <span data-ttu-id="5e777-311">Les sources de package ne contiennent pas de la version attendue limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="5e777-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="5e777-312">Si le package attendu n’a pas été lancé. Cela peut être un erreur de création de package.</span><span class="sxs-lookup"><span data-stu-id="5e777-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="5e777-313">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-313">**Example message**</span></span> | <span data-ttu-id="5e777-314">NuGet.Packaging 4.0.0 dépend NuGet.Versioning (> = 4.0.0) mais 4.0.0 n’a pas été trouvé.</span><span class="sxs-lookup"><span data-stu-id="5e777-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="5e777-315">Une meilleure correspondance approximative de 5.0.0 a été résolue.</span><span class="sxs-lookup"><span data-stu-id="5e777-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="5e777-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="5e777-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-317">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-317">**Issue**</span></span> | <span data-ttu-id="5e777-318">Une dépendance de projet ne définit pas une limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="5e777-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="5e777-319">Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*.</span><span class="sxs-lookup"><span data-stu-id="5e777-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="5e777-320">Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="5e777-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="5e777-321">Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5e777-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="5e777-322">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-322">**Common causes**</span></span> | <span data-ttu-id="5e777-323">Du projet *PackageReference* *Version* attribut doit être mis à jour pour inclure une limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="5e777-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="5e777-324">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-324">**Example message**</span></span> | <span data-ttu-id="5e777-325">*Projet dépendance NuGet.Versioning (< = 9.0.0) doe ne contient pas une limite inférieure inclusive. Inclure une limite inférieure dans la version de dépendance pour garantir des résultats de la restauration de cohérence.*</span><span class="sxs-lookup"><span data-stu-id="5e777-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="5e777-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="5e777-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-327">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-327">**Issue**</span></span> | <span data-ttu-id="5e777-328">Un package de dépendance spécifié une contrainte de version sur une version supérieure d’un package au restauration finalement réduite.</span><span class="sxs-lookup"><span data-stu-id="5e777-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="5e777-329">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-329">**Common causes**</span></span> | <span data-ttu-id="5e777-330">Wins le plus proche lors de la résolution des packages.</span><span class="sxs-lookup"><span data-stu-id="5e777-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="5e777-331">Un package plus proche dans le graphique peut avoir substitution un package distant.</span><span class="sxs-lookup"><span data-stu-id="5e777-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="5e777-332">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-332">**Example message**</span></span> | <span data-ttu-id="5e777-333">*Détecté vers une version antérieure du package : NuGet.Versioning de 4.0.0 vers la version 3.5.0. Référencer le package directement à partir du projet pour sélectionner une autre version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="5e777-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="5e777-334">Avertissements de conflit de programme de résolution</span><span class="sxs-lookup"><span data-stu-id="5e777-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="5e777-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="5e777-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-336">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-336">**Issue**</span></span> | <span data-ttu-id="5e777-337">Un package de résolution est supérieur à ce qui permet à une contrainte de dépendance.</span><span class="sxs-lookup"><span data-stu-id="5e777-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="5e777-338">Dans certains cas, cela est intentionnel et l’avertissement peut être supprimé.</span><span class="sxs-lookup"><span data-stu-id="5e777-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="5e777-339">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-339">**Common causes**</span></span> | <span data-ttu-id="5e777-340">Un package référencé directement par un projet remplacera les contraintes de dépendance à partir d’autres packages.</span><span class="sxs-lookup"><span data-stu-id="5e777-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="5e777-341">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-341">**Example message**</span></span> | <span data-ttu-id="5e777-342">*Version du package détectés en dehors de la contrainte de dépendance : x 1.0.0 requiert y (= 1.0.0), mais la version y 2.0.0 a été résolue.*</span><span class="sxs-lookup"><span data-stu-id="5e777-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="5e777-343">Avertissements de secours de package</span><span class="sxs-lookup"><span data-stu-id="5e777-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="5e777-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="5e777-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-345">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-345">**Issue**</span></span> | <span data-ttu-id="5e777-346">*PackageTargetFallback/AssetTargetFallback* a été utilisé pour sélectionner des éléments multimédias à partir d’un package.</span><span class="sxs-lookup"><span data-stu-id="5e777-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="5e777-347">Il s’agit d’un avertissement pour informer l’utilisateur que les ressources ne peuvent pas être de 100 % compatible.</span><span class="sxs-lookup"><span data-stu-id="5e777-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="5e777-348">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-348">**Common causes**</span></span> | <span data-ttu-id="5e777-349">Le package ne prend pas en charge l’infrastructure du projet.</span><span class="sxs-lookup"><span data-stu-id="5e777-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="5e777-350">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-350">**Example message**</span></span> | <span data-ttu-id="5e777-351">*Package 'NuGet.Versioning' a été restauré à l’aide de « portable-net45 + win8 » à la place le framework cible du projet 'netstandard1.5'. Ce package ne peut pas être entièrement compatible avec votre projet.*</span><span class="sxs-lookup"><span data-stu-id="5e777-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="5e777-352">Flux d’avertissements</span><span class="sxs-lookup"><span data-stu-id="5e777-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="5e777-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="5e777-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-354">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-354">**Issue**</span></span> | <span data-ttu-id="5e777-355">Une erreur s’est produite lors de la lecture du flux lorsque `IgnoreFailedSources` est définie sur true, le convertir en un avertissement non fatale.</span><span class="sxs-lookup"><span data-stu-id="5e777-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="5e777-356">Il peut contenir n’importe quel message et générique.</span><span class="sxs-lookup"><span data-stu-id="5e777-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="5e777-357">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-357">**Common causes**</span></span> | <span data-ttu-id="5e777-358">La source n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="5e777-358">The source is invalid.</span></span> |
| <span data-ttu-id="5e777-359">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="5e777-359">**Example message**</span></span> | <span data-ttu-id="5e777-360">N/A</span><span class="sxs-lookup"><span data-stu-id="5e777-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="5e777-361">Avertissements et erreurs internes de NuGet</span><span class="sxs-lookup"><span data-stu-id="5e777-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="5e777-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="5e777-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="5e777-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="5e777-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-364">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-364">**Issue**</span></span> | <span data-ttu-id="5e777-365">Une erreur interne non spécifique à partir de NuGet.</span><span class="sxs-lookup"><span data-stu-id="5e777-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="5e777-366">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-366">**Common causes**</span></span> | <span data-ttu-id="5e777-367">Vérifiez les journaux pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="5e777-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="5e777-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="5e777-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5e777-369">**Problème**</span><span class="sxs-lookup"><span data-stu-id="5e777-369">**Issue**</span></span> | <span data-ttu-id="5e777-370">Avertissement interne non spécifique de NuGet.</span><span class="sxs-lookup"><span data-stu-id="5e777-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="5e777-371">**Causes courantes**</span><span class="sxs-lookup"><span data-stu-id="5e777-371">**Common causes**</span></span> | <span data-ttu-id="5e777-372">Vérifiez les journaux pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="5e777-372">Check the logs for more information</span></span> |
