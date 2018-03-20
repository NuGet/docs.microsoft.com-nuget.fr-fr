---
title: "Préversions dans les packages NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Instructions pour la génération de packages en préversion"
keywords: "gestion de versions, gestion des versions de package NuGet, préversions NuGet, packages NuGet en préversion, préversions de packages, versions de package RC, versions de package bêta, gestion de versions sémantique NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 03f744a96841a8c49d9f1dde89620b85de968d6f
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2018
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="1973b-104">Génération de packages en préversion</span><span class="sxs-lookup"><span data-stu-id="1973b-104">Building pre-release packages</span></span>

<span data-ttu-id="1973b-105">Chaque fois que vous publiez un package mis à jour avec un nouveau numéro de version, NuGet le considère comme la « dernière version stable », comme indiqué par exemple dans l’interface utilisateur du gestionnaire de package dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="1973b-105">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Interface utilisateur du gestionnaire de package montrant la dernière version stable](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="1973b-107">Une version stable est une version considérée comme suffisamment fiable pour être utilisée en production.</span><span class="sxs-lookup"><span data-stu-id="1973b-107">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="1973b-108">La dernière version stable est également celle qui est installée sous forme de mise à jour de package ou pendant une restauration de package (conformément aux contraintes décrites dans [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="1973b-108">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="1973b-109">Pour prendre en charge le cycle de vie de publication du logiciel, NuGet 1.6 et ultérieur permet de distribuer des packages en préversion, où le numéro de version inclut un suffixe de gestion des versions sémantique comme `-alpha`, `-beta` ou `-rc`.</span><span class="sxs-lookup"><span data-stu-id="1973b-109">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="1973b-110">Pour plus d’informations, consultez [Gestion des versions de package](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="1973b-110">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="1973b-111">Vous pouvez spécifier ces versions de deux manières :</span><span class="sxs-lookup"><span data-stu-id="1973b-111">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="1973b-112">Fichier `.nuspec` : incluez le suffixe de version sémantique dans l’élément `version` :</span><span class="sxs-lookup"><span data-stu-id="1973b-112">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="1973b-113">Attributs d’assembly : lors de la création d’un package à partir d’un projet Visual Studio (`.csproj` ou `.vbproj`), utilisez `AssemblyInformationalVersionAttribute` pour spécifier la version :</span><span class="sxs-lookup"><span data-stu-id="1973b-113">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="1973b-114">NuGet sélectionne cette valeur au lieu de celle spécifiée dans l’attribut `AssemblyVersion`, qui ne prend pas en charge la gestion de versions sémantique.</span><span class="sxs-lookup"><span data-stu-id="1973b-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="1973b-115">Lorsque vous êtes prêt à publier une version stable, supprimez simplement le suffixe et le package est prioritaire sur toutes les préversions.</span><span class="sxs-lookup"><span data-stu-id="1973b-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="1973b-116">Là encore, consultez [Gestion des versions de package](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="1973b-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="1973b-117">Installation et mise à jour des packages en préversion</span><span class="sxs-lookup"><span data-stu-id="1973b-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="1973b-118">Par défaut, NuGet n’inclut pas de préversions dans le cadre de l’utilisation de packages, mais vous pouvez modifier ce comportement comme suit :</span><span class="sxs-lookup"><span data-stu-id="1973b-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="1973b-119">**Interface utilisateur du gestionnaire de package dans Visual Studio** : dans l’interface utilisateur **Gérer les packages NuGet**, cochez la case **Inclure la préversion** :</span><span class="sxs-lookup"><span data-stu-id="1973b-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Case à cocher Inclure la préversion dans Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="1973b-121">Le fait de cocher ou décocher cette case actualise l’interface utilisateur du gestionnaire de package et la liste des versions disponibles que vous pouvez installer.</span><span class="sxs-lookup"><span data-stu-id="1973b-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="1973b-122">**Console du gestionnaire de package** : utilisez le commutateur `-IncludePrerelease` avec les commandes `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` et `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="1973b-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="1973b-123">Reportez-vous à [Informations de référence sur PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1973b-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="1973b-124">**Interface de ligne de commande NuGet** : utilisez le commutateur `-prerelease` avec les commandes `install`, `update`, `delete` et `mirror`.</span><span class="sxs-lookup"><span data-stu-id="1973b-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="1973b-125">Reportez-vous à [Informations de référence sur l’interface de ligne de commande NuGet](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1973b-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="1973b-126">Gestion sémantique des versions</span><span class="sxs-lookup"><span data-stu-id="1973b-126">Semantic versioning</span></span>

<span data-ttu-id="1973b-127">La [gestion sémantique des versions ou convention SemVer](http://semver.org/spec/v1.0.0.html) décrit la manière d’utiliser des chaînes dans les numéros de version pour qu’elles indiquent la signification du code sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="1973b-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="1973b-128">Dans cette convention, chaque version se compose de trois parties, `Major.Minor.Patch`, avec la signification suivante :</span><span class="sxs-lookup"><span data-stu-id="1973b-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="1973b-129">`Major` : Modifications avec rupture</span><span class="sxs-lookup"><span data-stu-id="1973b-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="1973b-130">`Minor` : Nouvelles fonctionnalités, offrant néanmoins une compatibilité descendante</span><span class="sxs-lookup"><span data-stu-id="1973b-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="1973b-131">`Patch` : Correctifs de bogues à compatibilité descendante uniquement</span><span class="sxs-lookup"><span data-stu-id="1973b-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="1973b-132">Les préversions sont alors signalées par l’ajout d’un trait d’union et d’une chaîne après le numéro du correctif.</span><span class="sxs-lookup"><span data-stu-id="1973b-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="1973b-133">Techniquement parlant, vous pouvez utiliser *n’importe quelle* chaîne après le trait d’union pour que NuGet traite le package comme une préversion.</span><span class="sxs-lookup"><span data-stu-id="1973b-133">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="1973b-134">NuGet affiche alors le numéro de version complet dans l’interface utilisateur applicable, en laissant les consommateurs interpréter la signification pour eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="1973b-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="1973b-135">En sachant cela, il est généralement judicieux de suivre les conventions de nommage reconnues comme les suivantes :</span><span class="sxs-lookup"><span data-stu-id="1973b-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="1973b-136">`-alpha` : version alpha, généralement utilisée pour les travaux en cours et les expérimentations.</span><span class="sxs-lookup"><span data-stu-id="1973b-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="1973b-137">`-beta`: version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.</span><span class="sxs-lookup"><span data-stu-id="1973b-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="1973b-138">`-rc` : version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.</span><span class="sxs-lookup"><span data-stu-id="1973b-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="1973b-139">NuGet 4.3.0+ prend en charge la [gestion sémantique de version 2.0.0](http://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de pré-livraison utilisant la notation à points (par exemple, `1.0.1-build.23`).</span><span class="sxs-lookup"><span data-stu-id="1973b-139">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="1973b-140">La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="1973b-140">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="1973b-141">Dans les versions antérieures de NuGet, vous pouviez utiliser un format similaire à `1.0.1-build23`, mais celui-ci est toujours considéré comme une version de pré-livraison.</span><span class="sxs-lookup"><span data-stu-id="1973b-141">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="1973b-142">Quels que soient les suffixes que vous utilisez, toutefois, NuGet leur donne la priorité dans l’ordre alphabétique inverse :</span><span class="sxs-lookup"><span data-stu-id="1973b-142">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="1973b-143">Comme indiqué, la version sans aucun suffixe est toujours prioritaire par rapport aux préversions.</span><span class="sxs-lookup"><span data-stu-id="1973b-143">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="1973b-144">Notez également que si vous utilisez des suffixes numériques avec des balises en préversion susceptibles d’utiliser des nombres à deux chiffres (ou plus), utilisez des zéros non significatifs comme dans beta01 et beta05 pour pouvoir les trier correctement quand ces numéros s’allongent.</span><span class="sxs-lookup"><span data-stu-id="1973b-144">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
