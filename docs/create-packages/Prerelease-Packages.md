---
title: Préversions dans les packages NuGet
description: Instructions pour la génération de packages en préversion
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 150fc61e51fe10622fe6b369b60dfc61a9ac916f
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432450"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="6940e-103">Génération de packages en préversion</span><span class="sxs-lookup"><span data-stu-id="6940e-103">Building pre-release packages</span></span>

<span data-ttu-id="6940e-104">Chaque fois que vous publiez un package mis à jour avec un nouveau numéro de version, NuGet le considère comme la « dernière version stable », comme indiqué par exemple dans l’interface utilisateur du gestionnaire de package dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="6940e-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Interface utilisateur du gestionnaire de package montrant la dernière version stable](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="6940e-106">Une version stable est une version considérée comme suffisamment fiable pour être utilisée en production.</span><span class="sxs-lookup"><span data-stu-id="6940e-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="6940e-107">La dernière version stable est également celle qui est installée sous forme de mise à jour de package ou pendant une restauration de package (conformément aux contraintes décrites dans [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="6940e-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="6940e-108">Pour prendre en charge le cycle de vie de publication du logiciel, NuGet 1.6 et ultérieur permet de distribuer des packages en préversion, où le numéro de version inclut un suffixe de gestion des versions sémantique comme `-alpha`, `-beta` ou `-rc`.</span><span class="sxs-lookup"><span data-stu-id="6940e-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="6940e-109">Pour plus d’informations, consultez [Gestion des versions de package](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="6940e-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="6940e-110">Vous pouvez spécifier ces versions de deux manières :</span><span class="sxs-lookup"><span data-stu-id="6940e-110">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="6940e-111">Fichier `.nuspec` : incluez le suffixe de version sémantique dans l’élément `version` :</span><span class="sxs-lookup"><span data-stu-id="6940e-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="6940e-112">Attributs d’assembly : lors de la création d’un package à partir d’un projet Visual Studio (`.csproj` ou `.vbproj`), utilisez `AssemblyInformationalVersionAttribute` pour spécifier la version :</span><span class="sxs-lookup"><span data-stu-id="6940e-112">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="6940e-113">NuGet sélectionne cette valeur au lieu de celle spécifiée dans l’attribut `AssemblyVersion`, qui ne prend pas en charge la gestion de versions sémantique.</span><span class="sxs-lookup"><span data-stu-id="6940e-113">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="6940e-114">Lorsque vous êtes prêt à publier une version stable, supprimez simplement le suffixe et le package est prioritaire sur toutes les préversions.</span><span class="sxs-lookup"><span data-stu-id="6940e-114">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="6940e-115">Là encore, consultez [Gestion des versions de package](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="6940e-115">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="6940e-116">Installation et mise à jour des packages en préversion</span><span class="sxs-lookup"><span data-stu-id="6940e-116">Installing and updating pre-release packages</span></span>

<span data-ttu-id="6940e-117">Par défaut, NuGet n’inclut pas de préversions dans le cadre de l’utilisation de packages, mais vous pouvez modifier ce comportement comme suit :</span><span class="sxs-lookup"><span data-stu-id="6940e-117">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="6940e-118">**Interface utilisateur du Gestionnaire de package dans Visual Studio** : dans l’interface utilisateur **Gérer les packages NuGet**, cochez la case **Inclure la préversion** :</span><span class="sxs-lookup"><span data-stu-id="6940e-118">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Case à cocher Inclure la préversion dans Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="6940e-120">Le fait de cocher ou décocher cette case actualise l’interface utilisateur du gestionnaire de package et la liste des versions disponibles que vous pouvez installer.</span><span class="sxs-lookup"><span data-stu-id="6940e-120">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="6940e-121">**Console du Gestionnaire de package** : utilisez le commutateur `-IncludePrerelease` avec les commandes `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` et `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="6940e-121">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="6940e-122">Reportez-vous à [Informations de référence sur PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="6940e-122">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="6940e-123">**Interface de ligne de commande NuGet** : utilisez le commutateur `-prerelease` avec les commandes `install`, `update`, `delete` et `mirror`.</span><span class="sxs-lookup"><span data-stu-id="6940e-123">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="6940e-124">Reportez-vous à [Informations de référence sur l’interface de ligne de commande NuGet](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="6940e-124">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="6940e-125">Gestion sémantique des versions</span><span class="sxs-lookup"><span data-stu-id="6940e-125">Semantic versioning</span></span>

<span data-ttu-id="6940e-126">La [gestion sémantique de version ou convention SemVer](http://semver.org/spec/v1.0.0.html) décrit la manière d’utiliser des chaînes dans les numéros de version pour qu’elles indiquent la signification du code sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="6940e-126">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="6940e-127">Dans cette convention, chaque version se compose de trois parties, `Major.Minor.Patch`, avec la signification suivante :</span><span class="sxs-lookup"><span data-stu-id="6940e-127">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="6940e-128">`Major`: Modifications avec rupture</span><span class="sxs-lookup"><span data-stu-id="6940e-128">`Major`: Breaking changes</span></span>
- <span data-ttu-id="6940e-129">`Minor`: Nouvelles fonctionnalités, offrant néanmoins une compatibilité descendante</span><span class="sxs-lookup"><span data-stu-id="6940e-129">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="6940e-130">`Patch`: Correctifs de bogues à compatibilité descendante uniquement</span><span class="sxs-lookup"><span data-stu-id="6940e-130">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="6940e-131">Les préversions sont alors signalées par l’ajout d’un trait d’union et d’une chaîne après le numéro du correctif.</span><span class="sxs-lookup"><span data-stu-id="6940e-131">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="6940e-132">Techniquement parlant, vous pouvez utiliser *n’importe quelle* chaîne après le trait d’union pour que NuGet traite le package comme une préversion.</span><span class="sxs-lookup"><span data-stu-id="6940e-132">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="6940e-133">NuGet affiche alors le numéro de version complet dans l’interface utilisateur applicable, en laissant les consommateurs interpréter la signification pour eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="6940e-133">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="6940e-134">En sachant cela, il est généralement judicieux de suivre les conventions de nommage reconnues comme les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6940e-134">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="6940e-135">`-alpha`: Version alpha, généralement utilisée pour les travaux en cours et les expérimentations</span><span class="sxs-lookup"><span data-stu-id="6940e-135">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="6940e-136">`-beta`: Version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.</span><span class="sxs-lookup"><span data-stu-id="6940e-136">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="6940e-137">`-rc`: Version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.</span><span class="sxs-lookup"><span data-stu-id="6940e-137">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="6940e-138">NuGet 4.3.0+ prend en charge la [gestion sémantique de version 2.0.0](http://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de pré-livraison utilisant la notation à points (par exemple, `1.0.1-build.23`).</span><span class="sxs-lookup"><span data-stu-id="6940e-138">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="6940e-139">La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="6940e-139">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="6940e-140">Dans les versions antérieures de NuGet, vous pouviez utiliser un format similaire à `1.0.1-build23`, mais celui-ci est toujours considéré comme une version de pré-livraison.</span><span class="sxs-lookup"><span data-stu-id="6940e-140">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="6940e-141">Quels que soient les suffixes que vous utilisez, toutefois, NuGet leur donne la priorité dans l’ordre alphabétique inverse :</span><span class="sxs-lookup"><span data-stu-id="6940e-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="6940e-142">Comme indiqué, la version sans aucun suffixe est toujours prioritaire par rapport aux préversions.</span><span class="sxs-lookup"><span data-stu-id="6940e-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="6940e-143">Notez également que si vous utilisez des suffixes numériques avec des balises en préversion susceptibles d’utiliser des nombres à deux chiffres (ou plus), utilisez des zéros non significatifs comme dans beta01 et beta05 pour pouvoir les trier correctement quand ces numéros s’allongent.</span><span class="sxs-lookup"><span data-stu-id="6940e-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
