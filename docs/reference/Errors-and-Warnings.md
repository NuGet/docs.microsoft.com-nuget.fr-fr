---
title: NuGet erreurs et avertissements référence
description: Informations de référence complètes pour les avertissements et erreurs émises à partir de NuGet lors de diverses opérations de NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
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
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 748c2746a61886617e2eefe3e6c4a2e2a5b9d4d3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/22/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="43ba7-103">Erreurs et avertissements</span><span class="sxs-lookup"><span data-stu-id="43ba7-103">Errors and warnings</span></span>

<span data-ttu-id="43ba7-104">Dans NuGet 4.3.0+, les erreurs et avertissements sont numérotées comme décrit dans cette rubrique et fournissent des informations détaillées pour vous aider à résoudre les problèmes rencontrés.</span><span class="sxs-lookup"><span data-stu-id="43ba7-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="43ba7-105">Les erreurs et les avertissements répertoriés ici sont uniquement disponibles avec [basée sur les PackageReference](../consume-packages/package-references-in-project-files.md) projets et 4.3.0+ de NuGet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="43ba7-106">NuGet honore également des propriétés MSBuild pour supprimer les avertissements ou les élever à erreurs.</span><span class="sxs-lookup"><span data-stu-id="43ba7-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="43ba7-107">Pour plus d’informations, consultez [Comment : supprimer les avertissements du compilateur](/visualstudio/ide/how-to-suppress-compiler-warnings) dans la documentation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43ba7-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="43ba7-108">**erreurs**</span><span class="sxs-lookup"><span data-stu-id="43ba7-108">**Errors**</span></span>

| <span data-ttu-id="43ba7-109">Regrouper</span><span class="sxs-lookup"><span data-stu-id="43ba7-109">Group</span></span> | <span data-ttu-id="43ba7-110">Numéros d’erreur</span><span class="sxs-lookup"><span data-stu-id="43ba7-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="43ba7-111">Erreurs d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="43ba7-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="43ba7-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="43ba7-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="43ba7-113">Erreurs de package et de projet manquants</span><span class="sxs-lookup"><span data-stu-id="43ba7-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="43ba7-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (précédemment NU1607) [NU1108](#nu1108) (précédemment NU1606)</span><span class="sxs-lookup"><span data-stu-id="43ba7-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="43ba7-115">Erreurs de compatibilité</span><span class="sxs-lookup"><span data-stu-id="43ba7-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="43ba7-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="43ba7-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="43ba7-117">**Avertissements**</span><span class="sxs-lookup"><span data-stu-id="43ba7-117">**Warnings**</span></span>

| <span data-ttu-id="43ba7-118">Regrouper</span><span class="sxs-lookup"><span data-stu-id="43ba7-118">Group</span></span> | <span data-ttu-id="43ba7-119">Numéros d’avertissement</span><span class="sxs-lookup"><span data-stu-id="43ba7-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="43ba7-120">Avertissements d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="43ba7-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="43ba7-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="43ba7-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="43ba7-122">Avertissements de version de package inattendue</span><span class="sxs-lookup"><span data-stu-id="43ba7-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="43ba7-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="43ba7-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="43ba7-124">Avertissements de conflit de programme de résolution</span><span class="sxs-lookup"><span data-stu-id="43ba7-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="43ba7-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="43ba7-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="43ba7-126">Avertissements de secours de package</span><span class="sxs-lookup"><span data-stu-id="43ba7-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="43ba7-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="43ba7-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="43ba7-128">Flux d’avertissements</span><span class="sxs-lookup"><span data-stu-id="43ba7-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="43ba7-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="43ba7-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="43ba7-130">Avertissements et erreurs internes de NuGet</span><span class="sxs-lookup"><span data-stu-id="43ba7-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="43ba7-131">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="43ba7-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="43ba7-132">Packages signés (création et la vérification)</span><span class="sxs-lookup"><span data-stu-id="43ba7-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="43ba7-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="43ba7-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="43ba7-134">Erreurs d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="43ba7-134">Invalid input errors</span></span>

<span data-ttu-id="43ba7-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="43ba7-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="43ba7-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="43ba7-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-137">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-137">**Issue**</span></span> | <span data-ttu-id="43ba7-138">Le projet ne contient pas une ou plusieurs infrastructures.</span><span class="sxs-lookup"><span data-stu-id="43ba7-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="43ba7-139">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-139">**Example message**</span></span> | <span data-ttu-id="43ba7-140">*Le projet projA ne spécifie pas les versions .NET Framework cible dans c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="43ba7-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="43ba7-141">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-141">**Solution**</span></span> | <span data-ttu-id="43ba7-142">Ajouter un `TargetFramework` ou `TargetFrameworks` propriété au fichier projet spécifié.</span><span class="sxs-lookup"><span data-stu-id="43ba7-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="43ba7-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="43ba7-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-144">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-144">**Issue**</span></span> | <span data-ttu-id="43ba7-145">Combinaison non valide d’entrées avec un mot clé clair.</span><span class="sxs-lookup"><span data-stu-id="43ba7-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="43ba7-146">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-146">**Example message**</span></span> | <span data-ttu-id="43ba7-147">*« CLAIR » ne peut pas être utilisé conjointement avec d’autres valeurs*</span><span class="sxs-lookup"><span data-stu-id="43ba7-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="43ba7-148">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-148">**Solution**</span></span> | <span data-ttu-id="43ba7-149">Utilisez en lui-même et omettre toutes les autres entrées.</span><span class="sxs-lookup"><span data-stu-id="43ba7-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="43ba7-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="43ba7-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-151">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-151">**Issue**</span></span> | <span data-ttu-id="43ba7-152">`PackageTargetFallback` et `AssetTargetFallback` fournir un comportement différent pour la sélection des ressources et ne peut pas être utilisées ensemble.</span><span class="sxs-lookup"><span data-stu-id="43ba7-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="43ba7-153">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-153">**Example message**</span></span> | <span data-ttu-id="43ba7-154">*PackageTargetFallback et AssetTargetFallback ne peuvent pas être utilisées ensemble. Supprimez les références de PackageTargetFallback(deprecated) à partir de l’environnement de projet.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="43ba7-155">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-155">**Solution**</span></span> | <span data-ttu-id="43ba7-156">Supprimer déconseillées `PackageTargetFallback` élément à partir du projet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="43ba7-157">Erreurs de package et de projet manquants</span><span class="sxs-lookup"><span data-stu-id="43ba7-157">Missing package and project errors</span></span>

<span data-ttu-id="43ba7-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="43ba7-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="43ba7-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="43ba7-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-160">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-160">**Issue**</span></span> | <span data-ttu-id="43ba7-161">Un groupe de dépendances ne pas être résolu.</span><span class="sxs-lookup"><span data-stu-id="43ba7-161">A dependency group not be resolved.</span></span> <span data-ttu-id="43ba7-162">Il s’agit d’un problème générique pour les types qui ne sont pas des packages ou des projets.</span><span class="sxs-lookup"><span data-stu-id="43ba7-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="43ba7-163">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-163">**Example message**</span></span> | <span data-ttu-id="43ba7-164">*Impossible de résoudre System.Missing pour net45*</span><span class="sxs-lookup"><span data-stu-id="43ba7-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="43ba7-165">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-165">**Solution**</span></span> | <span data-ttu-id="43ba7-166">Ouvrez le fichier projet et examinez la liste de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="43ba7-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="43ba7-167">Vérifiez que chaque dépendance existe sur les sources de package que vous utilisez, et que le package prend en charge la version du projet cible.</span><span class="sxs-lookup"><span data-stu-id="43ba7-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="43ba7-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="43ba7-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-169">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-169">**Issue**</span></span> | <span data-ttu-id="43ba7-170">Impossible de trouver le package sur des sources.</span><span class="sxs-lookup"><span data-stu-id="43ba7-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="43ba7-171">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-171">**Example message**</span></span> | <span data-ttu-id="43ba7-172">*Impossible de trouver le package System.Missing. Aucun package n’existe avec cet id de source (s) : dotnet cœur, roslyn-dotnet, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="43ba7-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="43ba7-173">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-173">**Solution**</span></span> | <span data-ttu-id="43ba7-174">Examinez les dépendances du projet dans Visual Studio afin de vous assurer que vous utilisez le nombre d’identificateur et la version de package approprié.</span><span class="sxs-lookup"><span data-stu-id="43ba7-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="43ba7-175">Assurez-vous également que le [configuration NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifie les sources de package votre s’attendre à être à l’aide.</span><span class="sxs-lookup"><span data-stu-id="43ba7-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="43ba7-176">Si vous utilisez des packages qui ont [sémantique le contrôle de version 2.0.0](../reference/package-versioning.md#semantic-versioning-200), assurez-vous que vous utilisez la version 3 de flux, `https://api.nuget.org/v3/index.json`, dans le [configuration NuGet](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="43ba7-176">If you use packages that have [Semantic Versioning 2.0.0](../reference/package-versioning.md#semantic-versioning-200), please make sure that you are using the V3 feed, `https://api.nuget.org/v3/index.json`, in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="43ba7-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="43ba7-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-178">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-178">**Issue**</span></span> | <span data-ttu-id="43ba7-179">L’identificateur du package est trouvé, mais une version dans la plage de dépendance spécifié est introuvable sur une des sources.</span><span class="sxs-lookup"><span data-stu-id="43ba7-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="43ba7-180">La plage peut être spécifiée par un package et non à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="43ba7-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="43ba7-181">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-181">**Example message**</span></span> | <span data-ttu-id="43ba7-182">*Impossible de trouver le package NuGet.Versioning avec la version (> = 9.0.1)<br/> -30 de trouvé ou les versions dans nuget.org [plus proche de la version : 4.0.0]<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -trouvé le 9 versions dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032]<br/> -trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet*</span><span class="sxs-lookup"><span data-stu-id="43ba7-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="43ba7-183">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-183">**Solution**</span></span> | <span data-ttu-id="43ba7-184">Modifiez le fichier projet pour corriger la version du package.</span><span class="sxs-lookup"><span data-stu-id="43ba7-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="43ba7-185">Assurez-vous également que le [configuration NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifie les sources de package votre s’attendre à être à l’aide.</span><span class="sxs-lookup"><span data-stu-id="43ba7-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="43ba7-186">Vous devrez peut-être modifier la version requeted si ce package est référencé directement par le projet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="43ba7-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="43ba7-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-188">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-188">**Issue**</span></span> | <span data-ttu-id="43ba7-189">Le projet spécifié une version stable pour la plage de dépendance, mais aucune version stable a été trouvée dans cette plage.</span><span class="sxs-lookup"><span data-stu-id="43ba7-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="43ba7-190">Versions préliminaires ont été trouvées, mais ne sont pas autorisées.</span><span class="sxs-lookup"><span data-stu-id="43ba7-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="43ba7-191">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-191">**Example message**</span></span> | <span data-ttu-id="43ba7-192">*Impossible de trouver un package stable NuGet.Versioning avec la version (> = 3.0.0)<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -versions 9 de trouvé dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032] <br/> -Trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet*</span><span class="sxs-lookup"><span data-stu-id="43ba7-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="43ba7-193">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-193">**Solution**</span></span> |  <span data-ttu-id="43ba7-194">Modifier la plage de version dans le fichier projet pour inclure les versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="43ba7-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="43ba7-195">Consultez [contrôle de version de Package](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="43ba7-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="43ba7-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="43ba7-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-197">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-197">**Issue**</span></span> | <span data-ttu-id="43ba7-198">Un ProjectReference pointe vers un fichier qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="43ba7-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="43ba7-199">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-199">**Example message**</span></span> | <span data-ttu-id="43ba7-200">*Référence de projet n’existe pas de 'c:\a.csproj'. Vérifiez que la référence de projet est valide et que le fichier projet existe.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="43ba7-201">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-201">**Solution**</span></span> | <span data-ttu-id="43ba7-202">Modifiez le fichier projet pour corriger le chemin d’accès du projet référencé ou pour supprimer la référence totalement si elle n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="43ba7-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="43ba7-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="43ba7-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-204">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-204">**Issue**</span></span> | <span data-ttu-id="43ba7-205">Le fichier de projet existe mais aucune information de restauration a été fournie pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="43ba7-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="43ba7-206">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-206">**Example message**</span></span> | <span data-ttu-id="43ba7-207">*Impossible de lire les informations de projet pour 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="43ba7-208">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-208">**Solution**</span></span> | <span data-ttu-id="43ba7-209">Dans Visual Studio, l’erreur peut signifier que le projet est déchargé, dans les cas de recharger le projet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="43ba7-210">À partir de la ligne de commande, cela peut signifier que le fichier est endommagé ou qu’il ne contient pas personnalisé « après les importations » cible nécessaire pour la restauration lire le projet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="43ba7-211">Vérifiez que le fichier projet est valide et qu’il contient une cible « après les importations ».</span><span class="sxs-lookup"><span data-stu-id="43ba7-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="43ba7-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="43ba7-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-213">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-213">**Issue**</span></span> | <span data-ttu-id="43ba7-214">Contraintes de dépendances ne peut pas être résolus.</span><span class="sxs-lookup"><span data-stu-id="43ba7-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="43ba7-215">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-215">**Example message**</span></span> | <span data-ttu-id="43ba7-216">*Impossible de satisfaire les requêtes en conflit pour {id} : {chemin d’accès de conflit} Framework : {graphique cible}*</span><span class="sxs-lookup"><span data-stu-id="43ba7-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="43ba7-217">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-217">**Solution**</span></span> | <span data-ttu-id="43ba7-218">Modifiez le fichier projet pour spécifier les plages plus flexible pour la dépendance plutôt qu’une version exacte.</span><span class="sxs-lookup"><span data-stu-id="43ba7-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="43ba7-219">NU1107 (précédemment NU1607)</span><span class="sxs-lookup"><span data-stu-id="43ba7-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-220">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-220">**Issue**</span></span> | <span data-ttu-id="43ba7-221">Impossible de résoudre les contraintes de dépendances entre les packages.</span><span class="sxs-lookup"><span data-stu-id="43ba7-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="43ba7-222">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-222">**Example message**</span></span> | <span data-ttu-id="43ba7-223">*Conflit de version détecté pour NuGet.Versioning. Référencer le package directement à partir du projet pour résoudre ce problème.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="43ba7-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="43ba7-224">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-224">**Solution**</span></span> | <span data-ttu-id="43ba7-225">Les packages avec des contraintes de dépendance sur les versions exactes ne permettent pas d’autres packages d’augmenter la version, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="43ba7-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="43ba7-226">Ajoutez une référence au projet directement (dans le fichier projet) avec la version exacte requise.</span><span class="sxs-lookup"><span data-stu-id="43ba7-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="43ba7-227">NU1108 (précédemment NU1606)</span><span class="sxs-lookup"><span data-stu-id="43ba7-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-228">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-228">**Issue**</span></span> | <span data-ttu-id="43ba7-229">Une dépendance circulaire a été détectée.</span><span class="sxs-lookup"><span data-stu-id="43ba7-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="43ba7-230">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-230">**Example message**</span></span> | <span data-ttu-id="43ba7-231">*Cycle détecté : A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="43ba7-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="43ba7-232">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-232">**Solution**</span></span> | <span data-ttu-id="43ba7-233">Le package a été créé correctement ; Contactez le propriétaire du package pour corriger le bogue.</span><span class="sxs-lookup"><span data-stu-id="43ba7-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="43ba7-234">Erreurs de compatibilité</span><span class="sxs-lookup"><span data-stu-id="43ba7-234">Compatibility errors</span></span>

<span data-ttu-id="43ba7-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="43ba7-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="43ba7-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="43ba7-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-237">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-237">**Issue**</span></span> | <span data-ttu-id="43ba7-238">Un projet de dépendance ne contient pas une infrastructure compatible avec le projet actuel.</span><span class="sxs-lookup"><span data-stu-id="43ba7-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="43ba7-239">En règle générale, la version du projet cible est une version supérieure à celle du projet de consommation.</span><span class="sxs-lookup"><span data-stu-id="43ba7-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="43ba7-240">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-240">**Example message**</span></span> | <span data-ttu-id="43ba7-241">*Projet WAN n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Project prend en charge WAN :<br/> -netstandard1.6 (. NETStandard, Version = version 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = version 1.0)*</span><span class="sxs-lookup"><span data-stu-id="43ba7-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="43ba7-242">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-242">**Solution**</span></span> | <span data-ttu-id="43ba7-243">Modifier le framework du projet cible à une version inférieure ou égale à celle du projet de consommation.</span><span class="sxs-lookup"><span data-stu-id="43ba7-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="43ba7-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="43ba7-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-245">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-245">**Issue**</span></span> | <span data-ttu-id="43ba7-246">Un package de dépendance ne contient pas toutes les ressources compatibles avec le projet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="43ba7-247">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-247">**Example message**</span></span> | <span data-ttu-id="43ba7-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Package prend en charge System.ComponentModel.EventBasedAsync 4.0.11 :<br/> -monoandroid10 (MonoAndroid, Version = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (. NETFramework, Version = v4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. NETStandard, Version = v1.0)<br/> -portable-net45 + 8 + wp8 + wpa81 (. NETPortable, Version = v0.0, profil = Profile259)<br/> -win8 (Windows, Version = v8.0)<br/> -wp8 (WindowsPhone, Version = v8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v8.1)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="43ba7-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="43ba7-249">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-249">**Solution**</span></span> | <span data-ttu-id="43ba7-250">Modifier le framework du projet cible qui prend en charge par le package.</span><span class="sxs-lookup"><span data-stu-id="43ba7-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="43ba7-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="43ba7-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-252">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-252">**Issue**</span></span> | <span data-ttu-id="43ba7-253">Le package ne prend pas en charge du projet `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="43ba7-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="43ba7-254">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-254">**Example message**</span></span> | <span data-ttu-id="43ba7-255">*System.Example 1.0.0 fournit un assembly de référence de la compilation pour.dll sur net461, mais il n’existe aucun assembly au moment de l’exécution compatible.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="43ba7-256">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-256">**Solution**</span></span> | <span data-ttu-id="43ba7-257">Modifier la `RuntimeIdentifier` valeurs utilisées dans le projet en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="43ba7-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="43ba7-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="43ba7-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-259">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-259">**Issue**</span></span> | <span data-ttu-id="43ba7-260">Le package requiert des fonctionnalités ou des structures non prises en charge par la version installée de NuGet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="43ba7-261">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-261">**Example message**</span></span> | <span data-ttu-id="43ba7-262">*Le package 'NuGet.Versioning' nécessite '5.0.0' version du client de NuGet ou version ultérieure, mais la version NuGet actuelle est '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="43ba7-263">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-263">**Solution**</span></span> | <span data-ttu-id="43ba7-264">Installez une version plus récente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="43ba7-265">Consultez [outils clients de l’installation de NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="43ba7-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="43ba7-266">Avertissements d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="43ba7-266">Invalid input warnings</span></span>

<span data-ttu-id="43ba7-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="43ba7-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="43ba7-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="43ba7-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-269">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-269">**Issue**</span></span> | <span data-ttu-id="43ba7-270">La restauration du projet tente de fonctionner sur n’a été trouvé.</span><span class="sxs-lookup"><span data-stu-id="43ba7-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="43ba7-271">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-271">**Example message**</span></span> | <span data-ttu-id="43ba7-272">*Le dossier 'c:\projects\a' ne contient pas de projet à restaurer.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="43ba7-273">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-273">**Solution**</span></span> | <span data-ttu-id="43ba7-274">Exécutez nuget restore dans un dossier qui contient un projet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="43ba7-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="43ba7-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-276">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-276">**Issue**</span></span> | <span data-ttu-id="43ba7-277">`RuntimeSupports` contient un profil non valide.</span><span class="sxs-lookup"><span data-stu-id="43ba7-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="43ba7-278">En règle générale, le profil prend en charge est introuvable dans un `runtime.json` fichier issues des packages de dépendance actuel.</span><span class="sxs-lookup"><span data-stu-id="43ba7-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="43ba7-279">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-279">**Example message**</span></span> | <span data-ttu-id="43ba7-280">*Profil de compatibilité inconnu : aaa*</span><span class="sxs-lookup"><span data-stu-id="43ba7-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="43ba7-281">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-281">**Solution**</span></span> | <span data-ttu-id="43ba7-282">Vérifier la `RuntimeSupports` valeur dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="43ba7-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="43ba7-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-284">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-284">**Issue**</span></span> | <span data-ttu-id="43ba7-285">Un projet de dépendance n’importe pas les cibles de restauration de NuGet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="43ba7-286">Cela revient à NU1105 mais ici le projet est ignoré et ignorés au lieu de provoquer l’échec de restauration tous.</span><span class="sxs-lookup"><span data-stu-id="43ba7-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="43ba7-287">Dans les solutions complexes il existe souvent des autres types de projets qui n’acceptent pas de restauration.</span><span class="sxs-lookup"><span data-stu-id="43ba7-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="43ba7-288">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-288">**Example message**</span></span> | <span data-ttu-id="43ba7-289">*Ignorer la restauration de projet 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="43ba7-290">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-290">**Solution**</span></span> | <span data-ttu-id="43ba7-291">Cela peut se produire pour les projets qui n’importent pas de propriétés/cibles communes qui importer automatiquement la restauration.</span><span class="sxs-lookup"><span data-stu-id="43ba7-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="43ba7-292">Si le projet n’a pas besoin d’être restauré ce message peut être ignoré.</span><span class="sxs-lookup"><span data-stu-id="43ba7-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="43ba7-293">Dans le cas contraire, modifiez le projet affecté pour ajouter des cibles pour la restauration.</span><span class="sxs-lookup"><span data-stu-id="43ba7-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="43ba7-294">Avertissements de version de package inattendue</span><span class="sxs-lookup"><span data-stu-id="43ba7-294">Unexpected package version warnings</span></span>

<span data-ttu-id="43ba7-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="43ba7-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="43ba7-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="43ba7-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-297">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-297">**Issue**</span></span> | <span data-ttu-id="43ba7-298">Une dépendance directe a été agrandir à une version plus élevée que le projet spécifié.</span><span class="sxs-lookup"><span data-stu-id="43ba7-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="43ba7-299">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-299">**Example message**</span></span> | <span data-ttu-id="43ba7-300">*Dépendance spécifiée était NuGet.Versioning (> = 3.5.0), mais se terminait avec NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="43ba7-301">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-301">**Solution**</span></span> | <span data-ttu-id="43ba7-302">Mettre à jour la dépendance dans le projet à une version appropriée.</span><span class="sxs-lookup"><span data-stu-id="43ba7-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="43ba7-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="43ba7-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-304">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-304">**Issue**</span></span> | <span data-ttu-id="43ba7-305">Une dépendance de package est manquant dans une limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="43ba7-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="43ba7-306">Cela n’autorise pas la restauration rechercher la *meilleure correspondance*.</span><span class="sxs-lookup"><span data-stu-id="43ba7-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="43ba7-307">Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="43ba7-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="43ba7-308">Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur.</span><span class="sxs-lookup"><span data-stu-id="43ba7-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="43ba7-309">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-309">**Example message**</span></span> | <span data-ttu-id="43ba7-310">*NuGet.Packaging 4.0.0 ne fournit pas une limite inférieure inclusive de dépendance NuGet.Versioning (3.5.0 >). Une meilleure correspondance approximative de 3.6.0 a été résolue.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="43ba7-311">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-311">**Solution**</span></span> | <span data-ttu-id="43ba7-312">Il s’agit généralement d’un erreur de création de package.</span><span class="sxs-lookup"><span data-stu-id="43ba7-312">This is usually a package authoring error.</span></span> <span data-ttu-id="43ba7-313">Contactez l’auteur du package pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="43ba7-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="43ba7-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="43ba7-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-315">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-315">**Issue**</span></span> | <span data-ttu-id="43ba7-316">Une dépendance de package spécifié une version qui est introuvable.</span><span class="sxs-lookup"><span data-stu-id="43ba7-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="43ba7-317">En règle générale, les sources de package ne contiennent pas de la version attendue limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="43ba7-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="43ba7-318">Une version ultérieure a été utilisée à la place, ce qui diffère du package qui a été créé par rapport à.</span><span class="sxs-lookup"><span data-stu-id="43ba7-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="43ba7-319">Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*.</span><span class="sxs-lookup"><span data-stu-id="43ba7-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="43ba7-320">Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="43ba7-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="43ba7-321">Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur.</span><span class="sxs-lookup"><span data-stu-id="43ba7-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="43ba7-322">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-322">**Example message**</span></span> | <span data-ttu-id="43ba7-323">NuGet.Packaging 4.0.0 dépend NuGet.Versioning (> = 4.0.0) mais 4.0.0 n’a pas été trouvé.</span><span class="sxs-lookup"><span data-stu-id="43ba7-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="43ba7-324">Une meilleure correspondance approximative de 5.0.0 a été résolue.</span><span class="sxs-lookup"><span data-stu-id="43ba7-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="43ba7-325">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-325">**Solution**</span></span> | <span data-ttu-id="43ba7-326">Si le package attendu n’a pas été lancé. Cela peut être un erreur de création de package.</span><span class="sxs-lookup"><span data-stu-id="43ba7-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="43ba7-327">Contactez l’auteur du package pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="43ba7-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="43ba7-328">Si le package a été lancé, puis vérifiez qu’il est disponible sur les sources de package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="43ba7-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="43ba7-329">Si vous utilisez une source privée, vous devrez peut-être mettre à jour le package sur ce flux.</span><span class="sxs-lookup"><span data-stu-id="43ba7-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="43ba7-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="43ba7-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-331">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-331">**Issue**</span></span> | <span data-ttu-id="43ba7-332">Une dépendance de projet ne définit pas une limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="43ba7-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="43ba7-333">Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*.</span><span class="sxs-lookup"><span data-stu-id="43ba7-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="43ba7-334">Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="43ba7-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="43ba7-335">Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur.</span><span class="sxs-lookup"><span data-stu-id="43ba7-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="43ba7-336">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-336">**Example message**</span></span> | <span data-ttu-id="43ba7-337">*Projet dépendance NuGet.Versioning (< = 9.0.0) doe ne contient pas une limite inférieure inclusive. Inclure une limite inférieure dans la version de dépendance pour garantir des résultats de la restauration de cohérence.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="43ba7-338">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-338">**Solution**</span></span> | <span data-ttu-id="43ba7-339">Mettre à jour du projet `PackageReference` `Version` attribut à inclure une limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="43ba7-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="43ba7-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="43ba7-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-341">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-341">**Issue**</span></span> | <span data-ttu-id="43ba7-342">Un package de dépendance spécifié une contrainte de version sur une version supérieure d’un package au restauration finalement réduite.</span><span class="sxs-lookup"><span data-stu-id="43ba7-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="43ba7-343">Autrement dit, en raison de la « plus proche wins » règle lors de la résolution des packages, un package plus proche dans le graphique peut avoir substitution un package distant.</span><span class="sxs-lookup"><span data-stu-id="43ba7-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="43ba7-344">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-344">**Example message**</span></span> | <span data-ttu-id="43ba7-345">*Détecté vers une version antérieure du package : NuGet.Versioning de 4.0.0 vers la version 3.5.0. Référencer le package directement à partir du projet pour sélectionner une autre version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="43ba7-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="43ba7-346">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-346">**Solution**</span></span> | <span data-ttu-id="43ba7-347">Ajoutez une référence directe au projet pour la version la plus récente du package que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="43ba7-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="43ba7-348">Avertissements de conflit de programme de résolution</span><span class="sxs-lookup"><span data-stu-id="43ba7-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="43ba7-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="43ba7-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-350">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-350">**Issue**</span></span> | <span data-ttu-id="43ba7-351">Un package résolu est supérieur à ce qui permet à une contrainte de dépendance.</span><span class="sxs-lookup"><span data-stu-id="43ba7-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="43ba7-352">Cela signifie qu’un package référencé directement par un projet substitue les contraintes de dépendance à partir d’autres packages.</span><span class="sxs-lookup"><span data-stu-id="43ba7-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="43ba7-353">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-353">**Example message**</span></span> | <span data-ttu-id="43ba7-354">*Version du package détectés en dehors de la contrainte de dépendance : x 1.0.0 requiert y (= 1.0.0), mais la version y 2.0.0 a été résolue.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="43ba7-355">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-355">**Solution**</span></span> | <span data-ttu-id="43ba7-356">Dans certains cas, cela est intentionnel et l’avertissement peut être supprimé.</span><span class="sxs-lookup"><span data-stu-id="43ba7-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="43ba7-357">Dans le cas contraire, modifiez la référence du projet au package d’élargir ses contraintes de version.</span><span class="sxs-lookup"><span data-stu-id="43ba7-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="43ba7-358">Avertissements de secours de package</span><span class="sxs-lookup"><span data-stu-id="43ba7-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="43ba7-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="43ba7-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-360">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-360">**Issue**</span></span> | <span data-ttu-id="43ba7-361">`PackageTargetFallback` / `AssetTargetFallback` a été utilisé pour sélectionner des éléments multimédias à partir d’un package.</span><span class="sxs-lookup"><span data-stu-id="43ba7-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="43ba7-362">L’avertissement permettre aux utilisateurs de savoir que les ressources ne peuvent pas être de 100 % compatible.</span><span class="sxs-lookup"><span data-stu-id="43ba7-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="43ba7-363">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-363">**Example message**</span></span> | <span data-ttu-id="43ba7-364">*Package 'NuGet.Versioning' a été restauré à l’aide de « portable-net45 + win8 » à la place le framework cible du projet 'netstandard1.5'. Ce package ne peut pas être entièrement compatible avec votre projet.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="43ba7-365">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-365">**Solution**</span></span> | <span data-ttu-id="43ba7-366">Modifier le framework du projet cible qui prend en charge par le package.</span><span class="sxs-lookup"><span data-stu-id="43ba7-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="43ba7-367">Flux d’avertissements</span><span class="sxs-lookup"><span data-stu-id="43ba7-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="43ba7-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="43ba7-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-369">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-369">**Issue**</span></span> | <span data-ttu-id="43ba7-370">Une erreur s’est produite lors de la lecture du flux lorsque `IgnoreFailedSources` est définie sur true, le convertir en un avertissement non fatale.</span><span class="sxs-lookup"><span data-stu-id="43ba7-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="43ba7-371">Il peut contenir n’importe quel message et générique.</span><span class="sxs-lookup"><span data-stu-id="43ba7-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="43ba7-372">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-372">**Example message**</span></span> | <span data-ttu-id="43ba7-373">N/A</span><span class="sxs-lookup"><span data-stu-id="43ba7-373">n/a</span></span> |
| <span data-ttu-id="43ba7-374">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-374">**Solution**</span></span> | <span data-ttu-id="43ba7-375">Modifier votre configuration pour spécifier les sources valides.</span><span class="sxs-lookup"><span data-stu-id="43ba7-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="43ba7-376">Avertissements et erreurs internes de NuGet</span><span class="sxs-lookup"><span data-stu-id="43ba7-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="43ba7-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="43ba7-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="43ba7-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="43ba7-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-379">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-379">**Issue**</span></span> | <span data-ttu-id="43ba7-380">Une erreur interne non spécifique à partir de NuGet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="43ba7-381">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-381">**Solution**</span></span> | <span data-ttu-id="43ba7-382">Vérifiez les journaux pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="43ba7-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="43ba7-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="43ba7-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-384">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-384">**Issue**</span></span> | <span data-ttu-id="43ba7-385">Avertissement interne non spécifique de NuGet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="43ba7-386">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-386">**Solution**</span></span> | <span data-ttu-id="43ba7-387">Vérifiez les journaux pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="43ba7-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="43ba7-388">Packages signés (création et la vérification)</span><span class="sxs-lookup"><span data-stu-id="43ba7-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="43ba7-389">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="43ba7-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="43ba7-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="43ba7-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="43ba7-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="43ba7-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-392">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-392">**Issue**</span></span> | <span data-ttu-id="43ba7-393">Une erreur non spécifique associée à la signature du package et signé la vérification du package.</span><span class="sxs-lookup"><span data-stu-id="43ba7-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="43ba7-394">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-394">**Solution**</span></span> | <span data-ttu-id="43ba7-395">Vérifiez les journaux pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="43ba7-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="43ba7-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="43ba7-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-397">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-397">**Issue**</span></span> | <span data-ttu-id="43ba7-398">Arguments non valides à un le [sign la commande](../tools/cli-ref-sign.md) ou le [Vérifiez la commande](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="43ba7-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="43ba7-399">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-399">**Solution**</span></span> | <span data-ttu-id="43ba7-400">Vérifiez et corrigez les arguments fournis.</span><span class="sxs-lookup"><span data-stu-id="43ba7-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="43ba7-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="43ba7-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-402">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-402">**Issue**</span></span> | <span data-ttu-id="43ba7-403">Le `-Timestamper` option n’a pas été spécifiée avec la [commande de connexion nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="43ba7-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="43ba7-404">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-404">**Example message**</span></span> | <span data-ttu-id="43ba7-405">*Le '-Timestamper' option n’a pas été fournie. Le package signé ne sera pas horodaté.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="43ba7-406">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-406">**Solution**</span></span> | <span data-ttu-id="43ba7-407">Spécifiez le `-Timestamper` option avec `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="43ba7-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="43ba7-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="43ba7-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-409">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-409">**Issue**</span></span> | <span data-ttu-id="43ba7-410">Un package non signé a été fourni pour le [nuget Vérifiez la commande](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="43ba7-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="43ba7-411">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-411">**Solution**</span></span> | <span data-ttu-id="43ba7-412">Exécutez `nuget verify` avec un package signé.</span><span class="sxs-lookup"><span data-stu-id="43ba7-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="43ba7-413">Consultez [signer un package](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="43ba7-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="43ba7-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="43ba7-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-415">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-415">**Issue**</span></span> | <span data-ttu-id="43ba7-416">Échec de la vérification d’intégrité de package, ce qui signifie que qu’un package signé a été falsifié depuis en cours de signature.</span><span class="sxs-lookup"><span data-stu-id="43ba7-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="43ba7-417">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-417">**Solution**</span></span> | <span data-ttu-id="43ba7-418">Analyser votre ordinateur avec un logiciel antivirus.</span><span class="sxs-lookup"><span data-stu-id="43ba7-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="43ba7-419">Puis supprimez le package à partir de l’ordinateur, réinstallez-le et recommencez l’opération.</span><span class="sxs-lookup"><span data-stu-id="43ba7-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="43ba7-420">Si le problème persiste, contactez le propriétaire de la source du package et le package.</span><span class="sxs-lookup"><span data-stu-id="43ba7-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="43ba7-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="43ba7-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-422">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-422">**Issue**</span></span> | <span data-ttu-id="43ba7-423">Échec de la génération de chaîne de certificat pour la signature principale.</span><span class="sxs-lookup"><span data-stu-id="43ba7-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="43ba7-424">Le certificat de signature principal n’est pas fiable, révoqué, ou les informations de révocation du certificat ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="43ba7-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="43ba7-425">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-425">**Example message**</span></span> | <span data-ttu-id="43ba7-426">*Avertissement : NU3018 : la fonction de révocation n’a pas pu vérifier la révocation du certificat.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="43ba7-427">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-427">**Solution**</span></span> | <span data-ttu-id="43ba7-428">Utiliser un certificat approuvé et valide.</span><span class="sxs-lookup"><span data-stu-id="43ba7-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="43ba7-429">Vérifiez la connectivité internet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="43ba7-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="43ba7-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43ba7-431">**Problème**</span><span class="sxs-lookup"><span data-stu-id="43ba7-431">**Issue**</span></span> | <span data-ttu-id="43ba7-432">Échec de la génération de la chaîne certificat pour la signature d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="43ba7-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="43ba7-433">Le certificat de signature d’horodatage n’est pas fiable, révoqué, ou les informations de révocation du certificat ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="43ba7-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="43ba7-434">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="43ba7-434">**Example message**</span></span> | <span data-ttu-id="43ba7-435">*Avertissement : NU3028 : la fonction de révocation n’a pas pu vérifier la révocation du certificat.*</span><span class="sxs-lookup"><span data-stu-id="43ba7-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="43ba7-436">**Solution**</span><span class="sxs-lookup"><span data-stu-id="43ba7-436">**Solution**</span></span> | <span data-ttu-id="43ba7-437">Utiliser un certificat approuvé et valide.</span><span class="sxs-lookup"><span data-stu-id="43ba7-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="43ba7-438">Vérifiez la connectivité internet.</span><span class="sxs-lookup"><span data-stu-id="43ba7-438">Check internet connectivity.</span></span> |
