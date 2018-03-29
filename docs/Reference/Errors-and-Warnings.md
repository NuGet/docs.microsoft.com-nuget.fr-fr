---
title: NuGet erreurs et avertissements référence | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informations de référence complètes pour les avertissements et erreurs émises à partir de NuGet lors de diverses opérations de NuGet.
keywords: Erreurs de NuGet, les avertissements de NuGet, les diagnostics
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
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
ms.openlocfilehash: 020e31dc8646c43b86bcee555f1772e8b1db7761
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="e2da1-104">Erreurs et avertissements</span><span class="sxs-lookup"><span data-stu-id="e2da1-104">Errors and warnings</span></span>

<span data-ttu-id="e2da1-105">Dans NuGet 4.3.0+, les erreurs et avertissements sont numérotées comme décrit dans cette rubrique et fournissent des informations détaillées pour vous aider à résoudre les problèmes rencontrés.</span><span class="sxs-lookup"><span data-stu-id="e2da1-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="e2da1-106">Les erreurs et les avertissements répertoriés ici sont uniquement disponibles avec [basée sur les PackageReference](../consume-packages/package-references-in-project-files.md) projets et 4.3.0+ de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="e2da1-107">NuGet honore également des propriétés MSBuild pour supprimer les avertissements ou les élever à erreurs.</span><span class="sxs-lookup"><span data-stu-id="e2da1-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="e2da1-108">Pour plus d’informations, consultez [Comment : supprimer les avertissements du compilateur](/visualstudio/ide/how-to-suppress-compiler-warnings) dans la documentation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2da1-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="e2da1-109">**erreurs**</span><span class="sxs-lookup"><span data-stu-id="e2da1-109">**Errors**</span></span>

| <span data-ttu-id="e2da1-110">Regrouper</span><span class="sxs-lookup"><span data-stu-id="e2da1-110">Group</span></span> | <span data-ttu-id="e2da1-111">Numéros d’erreur</span><span class="sxs-lookup"><span data-stu-id="e2da1-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="e2da1-112">Erreurs d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="e2da1-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="e2da1-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="e2da1-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="e2da1-114">Erreurs de package et de projet manquants</span><span class="sxs-lookup"><span data-stu-id="e2da1-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="e2da1-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (précédemment NU1607) [NU1108](#nu1108) (précédemment NU1606)</span><span class="sxs-lookup"><span data-stu-id="e2da1-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="e2da1-116">Erreurs de compatibilité</span><span class="sxs-lookup"><span data-stu-id="e2da1-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="e2da1-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="e2da1-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="e2da1-118">**Avertissements**</span><span class="sxs-lookup"><span data-stu-id="e2da1-118">**Warnings**</span></span>

| <span data-ttu-id="e2da1-119">Regrouper</span><span class="sxs-lookup"><span data-stu-id="e2da1-119">Group</span></span> | <span data-ttu-id="e2da1-120">Numéros d’avertissement</span><span class="sxs-lookup"><span data-stu-id="e2da1-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="e2da1-121">Avertissements d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="e2da1-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="e2da1-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="e2da1-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="e2da1-123">Avertissements de version de package inattendue</span><span class="sxs-lookup"><span data-stu-id="e2da1-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="e2da1-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="e2da1-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="e2da1-125">Avertissements de conflit de programme de résolution</span><span class="sxs-lookup"><span data-stu-id="e2da1-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="e2da1-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="e2da1-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="e2da1-127">Avertissements de secours de package</span><span class="sxs-lookup"><span data-stu-id="e2da1-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="e2da1-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="e2da1-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="e2da1-129">Flux d’avertissements</span><span class="sxs-lookup"><span data-stu-id="e2da1-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="e2da1-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="e2da1-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="e2da1-131">Avertissements et erreurs internes de NuGet</span><span class="sxs-lookup"><span data-stu-id="e2da1-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="e2da1-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="e2da1-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="e2da1-133">Packages signés (création et la vérification)</span><span class="sxs-lookup"><span data-stu-id="e2da1-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="e2da1-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="e2da1-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="e2da1-135">Erreurs d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="e2da1-135">Invalid input errors</span></span>

<span data-ttu-id="e2da1-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="e2da1-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="e2da1-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="e2da1-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-138">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-138">**Issue**</span></span> | <span data-ttu-id="e2da1-139">Le projet ne contient pas une ou plusieurs infrastructures.</span><span class="sxs-lookup"><span data-stu-id="e2da1-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="e2da1-140">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-140">**Example message**</span></span> | <span data-ttu-id="e2da1-141">*Le projet projA ne spécifie pas les versions .NET Framework cible dans c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="e2da1-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="e2da1-142">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-142">**Solution**</span></span> | <span data-ttu-id="e2da1-143">Ajouter un `TargetFramework` ou `TargetFrameworks` propriété au fichier projet spécifié.</span><span class="sxs-lookup"><span data-stu-id="e2da1-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="e2da1-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="e2da1-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-145">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-145">**Issue**</span></span> | <span data-ttu-id="e2da1-146">Combinaison non valide d’entrées avec un mot clé clair.</span><span class="sxs-lookup"><span data-stu-id="e2da1-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="e2da1-147">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-147">**Example message**</span></span> | <span data-ttu-id="e2da1-148">*« CLAIR » ne peut pas être utilisé conjointement avec d’autres valeurs*</span><span class="sxs-lookup"><span data-stu-id="e2da1-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="e2da1-149">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-149">**Solution**</span></span> | <span data-ttu-id="e2da1-150">Utilisez en lui-même et omettre toutes les autres entrées.</span><span class="sxs-lookup"><span data-stu-id="e2da1-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="e2da1-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="e2da1-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-152">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-152">**Issue**</span></span> | <span data-ttu-id="e2da1-153">`PackageTargetFallback` et `AssetTargetFallback` fournir un comportement différent pour la sélection des ressources et ne peut pas être utilisées ensemble.</span><span class="sxs-lookup"><span data-stu-id="e2da1-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="e2da1-154">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-154">**Example message**</span></span> | <span data-ttu-id="e2da1-155">*PackageTargetFallback et AssetTargetFallback ne peuvent pas être utilisées ensemble. Supprimez les références de PackageTargetFallback(deprecated) à partir de l’environnement de projet.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="e2da1-156">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-156">**Solution**</span></span> | <span data-ttu-id="e2da1-157">Supprimer déconseillées `PackageTargetFallback` élément à partir du projet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="e2da1-158">Erreurs de package et de projet manquants</span><span class="sxs-lookup"><span data-stu-id="e2da1-158">Missing package and project errors</span></span>

<span data-ttu-id="e2da1-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="e2da1-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="e2da1-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="e2da1-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-161">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-161">**Issue**</span></span> | <span data-ttu-id="e2da1-162">Un groupe de dépendances ne pas être résolu.</span><span class="sxs-lookup"><span data-stu-id="e2da1-162">A dependency group not be resolved.</span></span> <span data-ttu-id="e2da1-163">Il s’agit d’un problème générique pour les types qui ne sont pas des packages ou des projets.</span><span class="sxs-lookup"><span data-stu-id="e2da1-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="e2da1-164">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-164">**Example message**</span></span> | <span data-ttu-id="e2da1-165">*Impossible de résoudre System.Missing pour net45*</span><span class="sxs-lookup"><span data-stu-id="e2da1-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="e2da1-166">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-166">**Solution**</span></span> | <span data-ttu-id="e2da1-167">Ouvrez le fichier projet et examinez la liste de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="e2da1-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="e2da1-168">Vérifiez que chaque dépendance existe sur les sources de package que vous utilisez, et que le package prend en charge la version du projet cible.</span><span class="sxs-lookup"><span data-stu-id="e2da1-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="e2da1-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="e2da1-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-170">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-170">**Issue**</span></span> | <span data-ttu-id="e2da1-171">Impossible de trouver le package sur des sources.</span><span class="sxs-lookup"><span data-stu-id="e2da1-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="e2da1-172">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-172">**Example message**</span></span> | <span data-ttu-id="e2da1-173">*Impossible de trouver le package System.Missing. Aucun package n’existe avec cet id de source (s) : dotnet cœur, roslyn-dotnet, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="e2da1-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="e2da1-174">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-174">**Solution**</span></span> | <span data-ttu-id="e2da1-175">Examinez les dépendances du projet dans Visual Studio afin de vous assurer que vous utilisez le nombre d’identificateur et la version de package approprié.</span><span class="sxs-lookup"><span data-stu-id="e2da1-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="e2da1-176">Assurez-vous également que le [configuration NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifie les sources de package votre s’attendre à être à l’aide.</span><span class="sxs-lookup"><span data-stu-id="e2da1-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="e2da1-177">Si vous utilisez des packages qui ont [sémantique le contrôle de version 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), assurez-vous que vous utilisez le [V3 de flux de](https://api.nuget.org/v3/index.json) dans le [configuration NuGet](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e2da1-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="e2da1-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="e2da1-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-179">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-179">**Issue**</span></span> | <span data-ttu-id="e2da1-180">L’identificateur du package est trouvé, mais une version dans la plage de dépendance spécifié est introuvable sur une des sources.</span><span class="sxs-lookup"><span data-stu-id="e2da1-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="e2da1-181">La plage peut être spécifiée par un package et non à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e2da1-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="e2da1-182">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-182">**Example message**</span></span> | <span data-ttu-id="e2da1-183">*Impossible de trouver le package NuGet.Versioning avec la version (> = 9.0.1)<br/> -30 de trouvé ou les versions dans nuget.org [plus proche de la version : 4.0.0]<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -trouvé le 9 versions dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032]<br/> -trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet*</span><span class="sxs-lookup"><span data-stu-id="e2da1-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="e2da1-184">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-184">**Solution**</span></span> | <span data-ttu-id="e2da1-185">Modifiez le fichier projet pour corriger la version du package.</span><span class="sxs-lookup"><span data-stu-id="e2da1-185">Edit the project file to correct the package version.</span></span> <span data-ttu-id="e2da1-186">Assurez-vous également que le [configuration NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifie les sources de package votre s’attendre à être à l’aide.</span><span class="sxs-lookup"><span data-stu-id="e2da1-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="e2da1-187">Vous devrez peut-être modifier la version requeted si ce package est référencé directement par le projet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="e2da1-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="e2da1-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-189">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-189">**Issue**</span></span> | <span data-ttu-id="e2da1-190">Le projet spécifié une version stable pour la plage de dépendance, mais aucune version stable a été trouvée dans cette plage.</span><span class="sxs-lookup"><span data-stu-id="e2da1-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="e2da1-191">Versions préliminaires ont été trouvées, mais ne sont pas autorisées.</span><span class="sxs-lookup"><span data-stu-id="e2da1-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="e2da1-192">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-192">**Example message**</span></span> | <span data-ttu-id="e2da1-193">*Impossible de trouver un package stable NuGet.Versioning avec la version (> = 3.0.0)<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -versions 9 de trouvé dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032] <br/> -Trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet*</span><span class="sxs-lookup"><span data-stu-id="e2da1-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="e2da1-194">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-194">**Solution**</span></span> |  <span data-ttu-id="e2da1-195">Modifier la plage de version dans le fichier projet pour inclure les versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="e2da1-195">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="e2da1-196">Consultez [contrôle de version de Package](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e2da1-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="e2da1-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="e2da1-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-198">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-198">**Issue**</span></span> | <span data-ttu-id="e2da1-199">Un ProjectReference pointe vers un fichier qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="e2da1-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="e2da1-200">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-200">**Example message**</span></span> | <span data-ttu-id="e2da1-201">*Référence de projet n’existe pas de 'c:\a.csproj'. Vérifiez que la référence de projet est valide et que le fichier projet existe.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="e2da1-202">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-202">**Solution**</span></span> | <span data-ttu-id="e2da1-203">Modifiez le fichier projet pour corriger le chemin d’accès du projet référencé ou pour supprimer la référence totalement si elle n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e2da1-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="e2da1-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="e2da1-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-205">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-205">**Issue**</span></span> | <span data-ttu-id="e2da1-206">Le fichier de projet existe mais aucune information de restauration a été fournie pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e2da1-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="e2da1-207">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-207">**Example message**</span></span> | <span data-ttu-id="e2da1-208">*Impossible de lire les informations de projet pour 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="e2da1-209">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-209">**Solution**</span></span> | <span data-ttu-id="e2da1-210">Dans Visual Studio, l’erreur peut signifier que le projet est déchargé, dans les cas de recharger le projet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="e2da1-211">À partir de la ligne de commande, cela peut signifier que le fichier est endommagé ou qu’il ne contient pas personnalisé « après les importations » cible nécessaire pour la restauration lire le projet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="e2da1-212">Vérifiez que le fichier projet est valide et qu’il contient une cible « après les importations ».</span><span class="sxs-lookup"><span data-stu-id="e2da1-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="e2da1-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="e2da1-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-214">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-214">**Issue**</span></span> | <span data-ttu-id="e2da1-215">Contraintes de dépendances ne peut pas être résolus.</span><span class="sxs-lookup"><span data-stu-id="e2da1-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="e2da1-216">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-216">**Example message**</span></span> | <span data-ttu-id="e2da1-217">*Impossible de satisfaire les requêtes en conflit pour {id} : {chemin d’accès de conflit} Framework : {graphique cible}*</span><span class="sxs-lookup"><span data-stu-id="e2da1-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="e2da1-218">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-218">**Solution**</span></span> | <span data-ttu-id="e2da1-219">Modifiez le fichier projet pour spécifier les plages plus flexible pour la dépendance plutôt qu’une version exacte.</span><span class="sxs-lookup"><span data-stu-id="e2da1-219">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="e2da1-220">NU1107 (précédemment NU1607)</span><span class="sxs-lookup"><span data-stu-id="e2da1-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-221">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-221">**Issue**</span></span> | <span data-ttu-id="e2da1-222">Impossible de résoudre les contraintes de dépendances entre les packages.</span><span class="sxs-lookup"><span data-stu-id="e2da1-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="e2da1-223">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-223">**Example message**</span></span> | <span data-ttu-id="e2da1-224">*Conflit de version détecté pour NuGet.Versioning. Référencer le package directement à partir du projet pour résoudre ce problème.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="e2da1-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="e2da1-225">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-225">**Solution**</span></span> | <span data-ttu-id="e2da1-226">Les packages avec des contraintes de dépendance sur les versions exactes ne permettent pas d’autres packages d’augmenter la version, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e2da1-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="e2da1-227">Ajoutez une référence au projet directement (dans le fichier projet) avec la version exacte requise.</span><span class="sxs-lookup"><span data-stu-id="e2da1-227">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="e2da1-228">NU1108 (précédemment NU1606)</span><span class="sxs-lookup"><span data-stu-id="e2da1-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-229">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-229">**Issue**</span></span> | <span data-ttu-id="e2da1-230">Une dépendance circulaire a été détectée.</span><span class="sxs-lookup"><span data-stu-id="e2da1-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="e2da1-231">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-231">**Example message**</span></span> | <span data-ttu-id="e2da1-232">*Cycle détecté : A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="e2da1-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="e2da1-233">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-233">**Solution**</span></span> | <span data-ttu-id="e2da1-234">Le package a été créé correctement ; Contactez le propriétaire du package pour corriger le bogue.</span><span class="sxs-lookup"><span data-stu-id="e2da1-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="e2da1-235">Erreurs de compatibilité</span><span class="sxs-lookup"><span data-stu-id="e2da1-235">Compatibility errors</span></span>

<span data-ttu-id="e2da1-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="e2da1-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="e2da1-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="e2da1-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-238">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-238">**Issue**</span></span> | <span data-ttu-id="e2da1-239">Un projet de dépendance ne contient pas une infrastructure compatible avec le projet actuel.</span><span class="sxs-lookup"><span data-stu-id="e2da1-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="e2da1-240">En règle générale, la version du projet cible est une version supérieure à celle du projet de consommation.</span><span class="sxs-lookup"><span data-stu-id="e2da1-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="e2da1-241">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-241">**Example message**</span></span> | <span data-ttu-id="e2da1-242">*Projet WAN n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Project prend en charge WAN :<br/> -netstandard1.6 (. NETStandard, Version = version 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = version 1.0)*</span><span class="sxs-lookup"><span data-stu-id="e2da1-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="e2da1-243">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-243">**Solution**</span></span> | <span data-ttu-id="e2da1-244">Modifier le framework du projet cible à une version inférieure ou égale à celle du projet de consommation.</span><span class="sxs-lookup"><span data-stu-id="e2da1-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="e2da1-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="e2da1-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-246">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-246">**Issue**</span></span> | <span data-ttu-id="e2da1-247">Un package de dépendance ne contient pas toutes les ressources compatibles avec le projet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="e2da1-248">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-248">**Example message**</span></span> | <span data-ttu-id="e2da1-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Package prend en charge System.ComponentModel.EventBasedAsync 4.0.11 :<br/> -monoandroid10 (MonoAndroid, Version = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (. NETFramework, Version = v4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. NETStandard, Version = v1.0)<br/> -portable-net45 + 8 + wp8 + wpa81 (. NETPortable, Version = v0.0, profil = Profile259)<br/> -win8 (Windows, Version = v8.0)<br/> -wp8 (WindowsPhone, Version = v8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v8.1)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="e2da1-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="e2da1-250">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-250">**Solution**</span></span> | <span data-ttu-id="e2da1-251">Modifier le framework du projet cible qui prend en charge par le package.</span><span class="sxs-lookup"><span data-stu-id="e2da1-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="e2da1-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="e2da1-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-253">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-253">**Issue**</span></span> | <span data-ttu-id="e2da1-254">Le package ne prend pas en charge du projet `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="e2da1-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="e2da1-255">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-255">**Example message**</span></span> | <span data-ttu-id="e2da1-256">*System.Example 1.0.0 fournit un assembly de référence de la compilation pour.dll sur net461, mais il n’existe aucun assembly au moment de l’exécution compatible.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="e2da1-257">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-257">**Solution**</span></span> | <span data-ttu-id="e2da1-258">Modifier la `RuntimeIdentifier` valeurs utilisées dans le projet en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="e2da1-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="e2da1-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="e2da1-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-260">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-260">**Issue**</span></span> | <span data-ttu-id="e2da1-261">Le package requiert des fonctionnalités ou des structures non prises en charge par la version installée de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="e2da1-262">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-262">**Example message**</span></span> | <span data-ttu-id="e2da1-263">*Le package 'NuGet.Versioning' nécessite '5.0.0' version du client de NuGet ou version ultérieure, mais la version NuGet actuelle est '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="e2da1-264">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-264">**Solution**</span></span> | <span data-ttu-id="e2da1-265">Installez une version plus récente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="e2da1-266">Consultez [outils clients de l’installation de NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="e2da1-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="e2da1-267">Avertissements d’entrée non valides</span><span class="sxs-lookup"><span data-stu-id="e2da1-267">Invalid input warnings</span></span>

<span data-ttu-id="e2da1-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="e2da1-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="e2da1-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="e2da1-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-270">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-270">**Issue**</span></span> | <span data-ttu-id="e2da1-271">La restauration du projet tente de fonctionner sur n’a été trouvé.</span><span class="sxs-lookup"><span data-stu-id="e2da1-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="e2da1-272">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-272">**Example message**</span></span> | <span data-ttu-id="e2da1-273">*Le dossier 'c:\projects\a' ne contient pas de projet à restaurer.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="e2da1-274">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-274">**Solution**</span></span> | <span data-ttu-id="e2da1-275">Exécutez nuget restore dans un dossier qui contient un projet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="e2da1-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="e2da1-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-277">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-277">**Issue**</span></span> | <span data-ttu-id="e2da1-278">`RuntimeSupports` contient un profil non valide.</span><span class="sxs-lookup"><span data-stu-id="e2da1-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="e2da1-279">En règle générale, le profil prend en charge est introuvable dans un `runtime.json` fichier issues des packages de dépendance actuel.</span><span class="sxs-lookup"><span data-stu-id="e2da1-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="e2da1-280">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-280">**Example message**</span></span> | <span data-ttu-id="e2da1-281">*Profil de compatibilité inconnu : aaa*</span><span class="sxs-lookup"><span data-stu-id="e2da1-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="e2da1-282">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-282">**Solution**</span></span> | <span data-ttu-id="e2da1-283">Vérifier la `RuntimeSupports` valeur dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="e2da1-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="e2da1-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-285">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-285">**Issue**</span></span> | <span data-ttu-id="e2da1-286">Un projet de dépendance n’importe pas les cibles de restauration de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="e2da1-287">Cela revient à NU1105 mais ici le projet est ignoré et ignorés au lieu de provoquer l’échec de restauration tous.</span><span class="sxs-lookup"><span data-stu-id="e2da1-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="e2da1-288">Dans les solutions complexes il existe souvent des autres types de projets qui n’acceptent pas de restauration.</span><span class="sxs-lookup"><span data-stu-id="e2da1-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="e2da1-289">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-289">**Example message**</span></span> | <span data-ttu-id="e2da1-290">*Ignorer la restauration de projet 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="e2da1-291">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-291">**Solution**</span></span> | <span data-ttu-id="e2da1-292">Cela peut se produire pour les projets qui n’importent pas de propriétés/cibles communes qui importer automatiquement la restauration.</span><span class="sxs-lookup"><span data-stu-id="e2da1-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="e2da1-293">Si le projet n’a pas besoin d’être restauré ce message peut être ignoré.</span><span class="sxs-lookup"><span data-stu-id="e2da1-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="e2da1-294">Dans le cas contraire, modifiez le projet affecté pour ajouter des cibles pour la restauration.</span><span class="sxs-lookup"><span data-stu-id="e2da1-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="e2da1-295">Avertissements de version de package inattendue</span><span class="sxs-lookup"><span data-stu-id="e2da1-295">Unexpected package version warnings</span></span>

<span data-ttu-id="e2da1-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="e2da1-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="e2da1-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="e2da1-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-298">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-298">**Issue**</span></span> | <span data-ttu-id="e2da1-299">Une dépendance directe a été agrandir à une version plus élevée que le projet spécifié.</span><span class="sxs-lookup"><span data-stu-id="e2da1-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="e2da1-300">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-300">**Example message**</span></span> | <span data-ttu-id="e2da1-301">*Dépendance spécifiée était NuGet.Versioning (> = 3.5.0), mais se terminait avec NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="e2da1-302">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-302">**Solution**</span></span> | <span data-ttu-id="e2da1-303">Mettre à jour la dépendance dans le projet à une version appropriée.</span><span class="sxs-lookup"><span data-stu-id="e2da1-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="e2da1-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="e2da1-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-305">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-305">**Issue**</span></span> | <span data-ttu-id="e2da1-306">Une dépendance de package est manquant dans une limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="e2da1-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="e2da1-307">Cela n’autorise pas la restauration rechercher la *meilleure correspondance*.</span><span class="sxs-lookup"><span data-stu-id="e2da1-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="e2da1-308">Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="e2da1-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="e2da1-309">Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e2da1-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="e2da1-310">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-310">**Example message**</span></span> | <span data-ttu-id="e2da1-311">*NuGet.Packaging 4.0.0 ne fournit pas une limite inférieure inclusive de dépendance NuGet.Versioning (3.5.0 >). Une meilleure correspondance approximative de 3.6.0 a été résolue.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="e2da1-312">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-312">**Solution**</span></span> | <span data-ttu-id="e2da1-313">Il s’agit généralement d’un erreur de création de package.</span><span class="sxs-lookup"><span data-stu-id="e2da1-313">This is usually a package authoring error.</span></span> <span data-ttu-id="e2da1-314">Contactez l’auteur du package pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="e2da1-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="e2da1-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="e2da1-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-316">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-316">**Issue**</span></span> | <span data-ttu-id="e2da1-317">Une dépendance de package spécifié une version qui est introuvable.</span><span class="sxs-lookup"><span data-stu-id="e2da1-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="e2da1-318">En règle générale, les sources de package ne contiennent pas de la version attendue limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="e2da1-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="e2da1-319">Une version ultérieure a été utilisée à la place, ce qui diffère du package qui a été créé par rapport à.</span><span class="sxs-lookup"><span data-stu-id="e2da1-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="e2da1-320">Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*.</span><span class="sxs-lookup"><span data-stu-id="e2da1-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="e2da1-321">Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="e2da1-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="e2da1-322">Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e2da1-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="e2da1-323">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-323">**Example message**</span></span> | <span data-ttu-id="e2da1-324">NuGet.Packaging 4.0.0 dépend NuGet.Versioning (> = 4.0.0) mais 4.0.0 n’a pas été trouvé.</span><span class="sxs-lookup"><span data-stu-id="e2da1-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="e2da1-325">Une meilleure correspondance approximative de 5.0.0 a été résolue.</span><span class="sxs-lookup"><span data-stu-id="e2da1-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="e2da1-326">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-326">**Solution**</span></span> | <span data-ttu-id="e2da1-327">Si le package attendu n’a pas été lancé. Cela peut être un erreur de création de package.</span><span class="sxs-lookup"><span data-stu-id="e2da1-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="e2da1-328">Contactez l’auteur du package pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="e2da1-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="e2da1-329">Si le package a été lancé, puis vérifiez qu’il est disponible sur les sources de package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="e2da1-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="e2da1-330">Si vous utilisez une source privée, vous devrez peut-être mettre à jour le package sur ce flux.</span><span class="sxs-lookup"><span data-stu-id="e2da1-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="e2da1-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="e2da1-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-332">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-332">**Issue**</span></span> | <span data-ttu-id="e2da1-333">Une dépendance de projet ne définit pas une limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="e2da1-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="e2da1-334">Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*.</span><span class="sxs-lookup"><span data-stu-id="e2da1-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="e2da1-335">Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="e2da1-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="e2da1-336">Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e2da1-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="e2da1-337">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-337">**Example message**</span></span> | <span data-ttu-id="e2da1-338">*Projet dépendance NuGet.Versioning (< = 9.0.0) doe ne contient pas une limite inférieure inclusive. Inclure une limite inférieure dans la version de dépendance pour garantir des résultats de la restauration de cohérence.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="e2da1-339">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-339">**Solution**</span></span> | <span data-ttu-id="e2da1-340">Mettre à jour du projet `PackageReference` `Version` attribut à inclure une limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="e2da1-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="e2da1-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="e2da1-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-342">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-342">**Issue**</span></span> | <span data-ttu-id="e2da1-343">Un package de dépendance spécifié une contrainte de version sur une version supérieure d’un package au restauration finalement réduite.</span><span class="sxs-lookup"><span data-stu-id="e2da1-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="e2da1-344">Autrement dit, en raison de la « plus proche wins » règle lors de la résolution des packages, un package plus proche dans le graphique peut avoir substitution un package distant.</span><span class="sxs-lookup"><span data-stu-id="e2da1-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="e2da1-345">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-345">**Example message**</span></span> | <span data-ttu-id="e2da1-346">*Détecté vers une version antérieure du package : NuGet.Versioning de 4.0.0 vers la version 3.5.0. Référencer le package directement à partir du projet pour sélectionner une autre version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="e2da1-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="e2da1-347">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-347">**Solution**</span></span> | <span data-ttu-id="e2da1-348">Ajoutez une référence directe au projet pour la version la plus récente du package que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="e2da1-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="e2da1-349">Avertissements de conflit de programme de résolution</span><span class="sxs-lookup"><span data-stu-id="e2da1-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="e2da1-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="e2da1-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-351">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-351">**Issue**</span></span> | <span data-ttu-id="e2da1-352">Un package résolu est supérieur à ce qui permet à une contrainte de dépendance.</span><span class="sxs-lookup"><span data-stu-id="e2da1-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="e2da1-353">Cela signifie qu’un package référencé directement par un projet substitue les contraintes de dépendance à partir d’autres packages.</span><span class="sxs-lookup"><span data-stu-id="e2da1-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="e2da1-354">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-354">**Example message**</span></span> | <span data-ttu-id="e2da1-355">*Version du package détectés en dehors de la contrainte de dépendance : x 1.0.0 requiert y (= 1.0.0), mais la version y 2.0.0 a été résolue.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="e2da1-356">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-356">**Solution**</span></span> | <span data-ttu-id="e2da1-357">Dans certains cas, cela est intentionnel et l’avertissement peut être supprimé.</span><span class="sxs-lookup"><span data-stu-id="e2da1-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="e2da1-358">Dans le cas contraire, modifiez la référence du projet au package d’élargir ses contraintes de version.</span><span class="sxs-lookup"><span data-stu-id="e2da1-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="e2da1-359">Avertissements de secours de package</span><span class="sxs-lookup"><span data-stu-id="e2da1-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="e2da1-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="e2da1-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-361">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-361">**Issue**</span></span> | <span data-ttu-id="e2da1-362">`PackageTargetFallback` / `AssetTargetFallback` a été utilisé pour sélectionner des éléments multimédias à partir d’un package.</span><span class="sxs-lookup"><span data-stu-id="e2da1-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="e2da1-363">L’avertissement permettre aux utilisateurs de savoir que les ressources ne peuvent pas être de 100 % compatible.</span><span class="sxs-lookup"><span data-stu-id="e2da1-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="e2da1-364">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-364">**Example message**</span></span> | <span data-ttu-id="e2da1-365">*Package 'NuGet.Versioning' a été restauré à l’aide de « portable-net45 + win8 » à la place le framework cible du projet 'netstandard1.5'. Ce package ne peut pas être entièrement compatible avec votre projet.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="e2da1-366">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-366">**Solution**</span></span> | <span data-ttu-id="e2da1-367">Modifier le framework du projet cible qui prend en charge par le package.</span><span class="sxs-lookup"><span data-stu-id="e2da1-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="e2da1-368">Flux d’avertissements</span><span class="sxs-lookup"><span data-stu-id="e2da1-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="e2da1-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="e2da1-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-370">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-370">**Issue**</span></span> | <span data-ttu-id="e2da1-371">Une erreur s’est produite lors de la lecture du flux lorsque `IgnoreFailedSources` est définie sur true, le convertir en un avertissement non fatale.</span><span class="sxs-lookup"><span data-stu-id="e2da1-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="e2da1-372">Il peut contenir n’importe quel message et générique.</span><span class="sxs-lookup"><span data-stu-id="e2da1-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="e2da1-373">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-373">**Example message**</span></span> | <span data-ttu-id="e2da1-374">N/A</span><span class="sxs-lookup"><span data-stu-id="e2da1-374">n/a</span></span> |
| <span data-ttu-id="e2da1-375">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-375">**Solution**</span></span> | <span data-ttu-id="e2da1-376">Modifier votre configuration pour spécifier les sources valides.</span><span class="sxs-lookup"><span data-stu-id="e2da1-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="e2da1-377">Avertissements et erreurs internes de NuGet</span><span class="sxs-lookup"><span data-stu-id="e2da1-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="e2da1-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="e2da1-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="e2da1-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="e2da1-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-380">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-380">**Issue**</span></span> | <span data-ttu-id="e2da1-381">Une erreur interne non spécifique à partir de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="e2da1-382">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-382">**Solution**</span></span> | <span data-ttu-id="e2da1-383">Vérifiez les journaux pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="e2da1-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="e2da1-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="e2da1-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-385">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-385">**Issue**</span></span> | <span data-ttu-id="e2da1-386">Avertissement interne non spécifique de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="e2da1-387">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-387">**Solution**</span></span> | <span data-ttu-id="e2da1-388">Vérifiez les journaux pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="e2da1-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="e2da1-389">Packages signés (création et la vérification)</span><span class="sxs-lookup"><span data-stu-id="e2da1-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="e2da1-390">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="e2da1-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="e2da1-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="e2da1-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="e2da1-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="e2da1-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-393">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-393">**Issue**</span></span> | <span data-ttu-id="e2da1-394">Une erreur non spécifique associée à la signature du package et signé la vérification du package.</span><span class="sxs-lookup"><span data-stu-id="e2da1-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="e2da1-395">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-395">**Solution**</span></span> | <span data-ttu-id="e2da1-396">Vérifiez les journaux pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e2da1-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="e2da1-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="e2da1-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-398">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-398">**Issue**</span></span> | <span data-ttu-id="e2da1-399">Arguments non valides à un le [sign la commande](../tools/cli-ref-sign.md) ou le [Vérifiez la commande](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="e2da1-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="e2da1-400">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-400">**Solution**</span></span> | <span data-ttu-id="e2da1-401">Vérifiez et corrigez les arguments fournis.</span><span class="sxs-lookup"><span data-stu-id="e2da1-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="e2da1-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="e2da1-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-403">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-403">**Issue**</span></span> | <span data-ttu-id="e2da1-404">Le `-Timestamper` option n’a pas été spécifiée avec la [commande de connexion nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="e2da1-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="e2da1-405">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-405">**Example message**</span></span> | <span data-ttu-id="e2da1-406">*Le '-Timestamper' option n’a pas été fournie. Le package signé ne sera pas horodaté.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="e2da1-407">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-407">**Solution**</span></span> | <span data-ttu-id="e2da1-408">Spécifiez le `-Timestamper` option avec `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="e2da1-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="e2da1-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="e2da1-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-410">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-410">**Issue**</span></span> | <span data-ttu-id="e2da1-411">Un package non signé a été fourni pour le [nuget Vérifiez la commande](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="e2da1-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="e2da1-412">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-412">**Solution**</span></span> | <span data-ttu-id="e2da1-413">Exécutez `nuget verify` avec un package signé.</span><span class="sxs-lookup"><span data-stu-id="e2da1-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="e2da1-414">Consultez [signer un package](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="e2da1-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="e2da1-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="e2da1-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-416">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-416">**Issue**</span></span> | <span data-ttu-id="e2da1-417">Échec de la vérification d’intégrité de package, ce qui signifie que qu’un package signé a été falsifié depuis en cours de signature.</span><span class="sxs-lookup"><span data-stu-id="e2da1-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="e2da1-418">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-418">**Solution**</span></span> | <span data-ttu-id="e2da1-419">Analyser votre ordinateur avec un logiciel antivirus.</span><span class="sxs-lookup"><span data-stu-id="e2da1-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="e2da1-420">Puis supprimez le package à partir de l’ordinateur, réinstallez-le et recommencez l’opération.</span><span class="sxs-lookup"><span data-stu-id="e2da1-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="e2da1-421">Si le problème persiste, contactez le propriétaire de la source du package et le package.</span><span class="sxs-lookup"><span data-stu-id="e2da1-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="e2da1-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="e2da1-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-423">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-423">**Issue**</span></span> | <span data-ttu-id="e2da1-424">Échec de la génération de chaîne de certificat pour la signature principale.</span><span class="sxs-lookup"><span data-stu-id="e2da1-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="e2da1-425">Le certificat de signature principal n’est pas fiable, révoqué, ou les informations de révocation du certificat ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="e2da1-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="e2da1-426">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-426">**Example message**</span></span> | <span data-ttu-id="e2da1-427">*Avertissement : NU3018 : la fonction de révocation n’a pas pu vérifier la révocation du certificat.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="e2da1-428">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-428">**Solution**</span></span> | <span data-ttu-id="e2da1-429">Utiliser un certificat approuvé et valide.</span><span class="sxs-lookup"><span data-stu-id="e2da1-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="e2da1-430">Vérifiez la connectivité internet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="e2da1-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="e2da1-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e2da1-432">**Problème**</span><span class="sxs-lookup"><span data-stu-id="e2da1-432">**Issue**</span></span> | <span data-ttu-id="e2da1-433">Échec de la génération de la chaîne certificat pour la signature d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="e2da1-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="e2da1-434">Le certificat de signature d’horodatage n’est pas fiable, révoqué, ou les informations de révocation du certificat ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="e2da1-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="e2da1-435">**Exemple de message**</span><span class="sxs-lookup"><span data-stu-id="e2da1-435">**Example message**</span></span> | <span data-ttu-id="e2da1-436">*Avertissement : NU3028 : la fonction de révocation n’a pas pu vérifier la révocation du certificat.*</span><span class="sxs-lookup"><span data-stu-id="e2da1-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="e2da1-437">**Solution**</span><span class="sxs-lookup"><span data-stu-id="e2da1-437">**Solution**</span></span> | <span data-ttu-id="e2da1-438">Utiliser un certificat approuvé et valide.</span><span class="sxs-lookup"><span data-stu-id="e2da1-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="e2da1-439">Vérifiez la connectivité internet.</span><span class="sxs-lookup"><span data-stu-id="e2da1-439">Check internet connectivity.</span></span> |
