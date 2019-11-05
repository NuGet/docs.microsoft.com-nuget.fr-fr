---
title: Préversions dans les packages NuGet
description: Instructions pour la génération de packages en préversion
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610716"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="5e61d-103">Génération de packages en préversion</span><span class="sxs-lookup"><span data-stu-id="5e61d-103">Building pre-release packages</span></span>

<span data-ttu-id="5e61d-104">Chaque fois que vous publiez un package mis à jour avec un nouveau numéro de version, NuGet le considère comme la « dernière version stable », comme indiqué par exemple dans l’interface utilisateur du gestionnaire de package dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="5e61d-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Interface utilisateur du gestionnaire de package montrant la dernière version stable](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="5e61d-106">Une version stable est une version considérée comme suffisamment fiable pour être utilisée en production.</span><span class="sxs-lookup"><span data-stu-id="5e61d-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="5e61d-107">La dernière version stable est également celle qui est installée sous forme de mise à jour de package ou pendant une restauration de package (conformément aux contraintes décrites dans [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="5e61d-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="5e61d-108">Pour prendre en charge le cycle de vie de publication du logiciel, NuGet 1.6 et ultérieur permet de distribuer des packages en préversion, où le numéro de version inclut un suffixe de gestion des versions sémantique comme `-alpha`, `-beta` ou `-rc`.</span><span class="sxs-lookup"><span data-stu-id="5e61d-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="5e61d-109">Pour plus d’informations, consultez [Gestion des versions de package](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="5e61d-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="5e61d-110">Vous pouvez spécifier ces versions en utilisant l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="5e61d-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="5e61d-111">**Si votre projet utilise [`PackageReference`](../consume-packages/package-references-in-project-files.md)**  : incluez le suffixe de version sémantique dans l’élément [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) du fichier `.csproj` :</span><span class="sxs-lookup"><span data-stu-id="5e61d-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="5e61d-112">**Si votre projet utilise un fichier [`packages.config`](../reference/packages-config.md)**  : incluez le suffixe de version sémantique dans l’élément [`version`](../reference/nuspec.md#version) du fichier [`.nuspec`](../reference/nuspec.md) :</span><span class="sxs-lookup"><span data-stu-id="5e61d-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="5e61d-113">Lorsque vous êtes prêt à publier une version stable, supprimez simplement le suffixe et le package est prioritaire sur toutes les préversions.</span><span class="sxs-lookup"><span data-stu-id="5e61d-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="5e61d-114">Là encore, consultez [Gestion des versions de package](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="5e61d-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="5e61d-115">Installation et mise à jour des packages en préversion</span><span class="sxs-lookup"><span data-stu-id="5e61d-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="5e61d-116">Par défaut, NuGet n’inclut pas de préversions dans le cadre de l’utilisation de packages, mais vous pouvez modifier ce comportement comme suit :</span><span class="sxs-lookup"><span data-stu-id="5e61d-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="5e61d-117">**Interface utilisateur du gestionnaire de package dans Visual Studio** : dans l’interface utilisateur **Gérer les packages NuGet**, cochez la case **Inclure la préversion** :</span><span class="sxs-lookup"><span data-stu-id="5e61d-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Case à cocher Inclure la préversion dans Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="5e61d-119">Le fait de cocher ou décocher cette case actualise l’interface utilisateur du gestionnaire de package et la liste des versions disponibles que vous pouvez installer.</span><span class="sxs-lookup"><span data-stu-id="5e61d-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="5e61d-120">**Console du gestionnaire de package** : utilisez le commutateur `-IncludePrerelease` avec les commandes `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` et `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="5e61d-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="5e61d-121">Reportez-vous à [Informations de référence sur PowerShell](../reference/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5e61d-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="5e61d-122">**Interface de ligne de commande NuGet** : utilisez le commutateur `-prerelease` avec les commandes `install`, `update`, `delete` et `mirror`.</span><span class="sxs-lookup"><span data-stu-id="5e61d-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="5e61d-123">Reportez-vous à [Informations de référence sur l’interface de ligne de commande NuGet](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5e61d-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="5e61d-124">Gestion sémantique des versions</span><span class="sxs-lookup"><span data-stu-id="5e61d-124">Semantic versioning</span></span>

<span data-ttu-id="5e61d-125">La [gestion sémantique de version ou convention SemVer](https://semver.org/spec/v1.0.0.html) décrit la manière d’utiliser des chaînes dans les numéros de version pour qu’elles indiquent la signification du code sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="5e61d-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="5e61d-126">Dans cette convention, chaque version se compose de trois parties, `Major.Minor.Patch`, avec la signification suivante :</span><span class="sxs-lookup"><span data-stu-id="5e61d-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="5e61d-127">`Major` : Modifications avec rupture</span><span class="sxs-lookup"><span data-stu-id="5e61d-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="5e61d-128">`Minor` : Nouvelles fonctionnalités, offrant néanmoins une compatibilité descendante</span><span class="sxs-lookup"><span data-stu-id="5e61d-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="5e61d-129">`Patch` : Correctifs de bogues à compatibilité descendante uniquement</span><span class="sxs-lookup"><span data-stu-id="5e61d-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="5e61d-130">Les préversions sont alors signalées par l’ajout d’un trait d’union et d’une chaîne après le numéro du correctif.</span><span class="sxs-lookup"><span data-stu-id="5e61d-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="5e61d-131">Techniquement parlant, vous pouvez utiliser *n’importe quelle* chaîne après le trait d’union pour que NuGet traite le package comme une préversion.</span><span class="sxs-lookup"><span data-stu-id="5e61d-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="5e61d-132">NuGet affiche alors le numéro de version complet dans l’interface utilisateur applicable, en laissant les consommateurs interpréter la signification pour eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="5e61d-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="5e61d-133">En sachant cela, il est généralement judicieux de suivre les conventions de nommage reconnues comme les suivantes :</span><span class="sxs-lookup"><span data-stu-id="5e61d-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="5e61d-134">`-alpha` : version alpha, généralement utilisée pour les travaux en cours et les expérimentations.</span><span class="sxs-lookup"><span data-stu-id="5e61d-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="5e61d-135">`-beta`: version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.</span><span class="sxs-lookup"><span data-stu-id="5e61d-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="5e61d-136">`-rc` : version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.</span><span class="sxs-lookup"><span data-stu-id="5e61d-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="5e61d-137">NuGet 4.3.0+ prend en charge la [gestion sémantique de version 2.0.0](https://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de pré-livraison utilisant la notation à points (par exemple, `1.0.1-build.23`).</span><span class="sxs-lookup"><span data-stu-id="5e61d-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="5e61d-138">La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="5e61d-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="5e61d-139">Dans les versions antérieures de NuGet, vous pouviez utiliser un format similaire à `1.0.1-build23`, mais celui-ci est toujours considéré comme une version de pré-livraison.</span><span class="sxs-lookup"><span data-stu-id="5e61d-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="5e61d-140">Quels que soient les suffixes que vous utilisez, toutefois, NuGet leur donne la priorité dans l’ordre alphabétique inverse :</span><span class="sxs-lookup"><span data-stu-id="5e61d-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="5e61d-141">Comme indiqué, la version sans aucun suffixe est toujours prioritaire par rapport aux préversions.</span><span class="sxs-lookup"><span data-stu-id="5e61d-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="5e61d-142">Les zéros de début ne sont pas nécessaires avec semver2, mais ils le sont avec l’ancien schéma de version.</span><span class="sxs-lookup"><span data-stu-id="5e61d-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="5e61d-143">Si vous utilisez des suffixes numériques avec des balises en version préliminaire susceptibles d’utiliser des nombres à deux chiffres (ou plus), utilisez des zéros non significatifs comme dans beta.01 et beta.05 pour pouvoir les trier correctement quand ces numéros s’allongent.</span><span class="sxs-lookup"><span data-stu-id="5e61d-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="5e61d-144">Cette recommandation s’applique uniquement à l’ancien schéma de version.</span><span class="sxs-lookup"><span data-stu-id="5e61d-144">This recommendation only applies to the old version schema.</span></span>
