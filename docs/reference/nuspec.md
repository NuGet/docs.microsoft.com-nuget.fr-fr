---
title: Référence du fichier .nuspec pour NuGet
description: Le fichier .nuspec contient des métadonnées de package utilisées lors de la création d’un package et pour fournir des informations aux consommateurs de packages.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6d190d9fdb26d76fa8e46b7d283c1857cfab26e9
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508034"
---
# <a name="nuspec-reference"></a><span data-ttu-id="a0b8c-103">Informations de référence sur le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="a0b8c-103">.nuspec reference</span></span>

<span data-ttu-id="a0b8c-104">Un fichier `.nuspec` est un manifeste XML qui contient des métadonnées de package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="a0b8c-105">Ce manifeste est utilisé à la fois pour générer le package et pour fournir des informations aux consommateurs.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="a0b8c-106">Le manifeste est toujours inclus dans un package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="a0b8c-107">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-107">In this topic:</span></span>

- [<span data-ttu-id="a0b8c-108">Forme générale et schéma</span><span class="sxs-lookup"><span data-stu-id="a0b8c-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="a0b8c-109">[Jetons de remplacement](#replacement-tokens) (lors d’une utilisation avec un projet Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a0b8c-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="a0b8c-110">Dépendances</span><span class="sxs-lookup"><span data-stu-id="a0b8c-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="a0b8c-111">Références d’assembly explicite</span><span class="sxs-lookup"><span data-stu-id="a0b8c-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="a0b8c-112">Références d’assembly Framework</span><span class="sxs-lookup"><span data-stu-id="a0b8c-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="a0b8c-113">Inclusion des fichiers d’assembly</span><span class="sxs-lookup"><span data-stu-id="a0b8c-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="a0b8c-114">Inclusion des fichiers de contenu</span><span class="sxs-lookup"><span data-stu-id="a0b8c-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="a0b8c-115">Exemples de fichiers nuspec</span><span class="sxs-lookup"><span data-stu-id="a0b8c-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="a0b8c-116">Forme générale et schéma</span><span class="sxs-lookup"><span data-stu-id="a0b8c-116">General form and schema</span></span>

<span data-ttu-id="a0b8c-117">Le fichier de schéma `nuspec.xsd` actuel se trouve dans le [dépôt GitHub NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="a0b8c-118">Dans ce schéma, un fichier `.nuspec` a la forme générale suivante :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="a0b8c-119">Pour obtenir une représentation visuelle claire du schéma, ouvrez le fichier de schéma dans Visual Studio en mode Design et cliquez sur le lien **Explorateur de schémas XML**.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="a0b8c-120">Vous pouvez également ouvrir le fichier en tant que code, cliquer avec le bouton droit dans l’éditeur, puis sélectionner **Show XML Schema Explorer** (Afficher l’Explorateur de schémas XML).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="a0b8c-121">Dans les deux cas, vous obtenez un affichage semblable à celui ci-dessous (quand il est en grande partie développé) :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorateur de schémas Visual Studio avec nuspec.xsd ouvert](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="a0b8c-123">Attributs de métadonnées</span><span class="sxs-lookup"><span data-stu-id="a0b8c-123">Metadata attributes</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="a0b8c-124">Éléments de métadonnées requis</span><span class="sxs-lookup"><span data-stu-id="a0b8c-124">Required metadata elements</span></span>

<span data-ttu-id="a0b8c-125">Bien que les éléments suivants correspondent à la configuration minimale requise pour un package, vous devez envisager d’ajouter les [éléments de métadonnées facultatifs](#optional-metadata-elements) afin d’améliorer l’expérience globale des développeurs avec votre package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-125">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="a0b8c-126">Ces éléments doivent apparaître dans un élément `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-126">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="a0b8c-127">Élément</span><span class="sxs-lookup"><span data-stu-id="a0b8c-127">Element</span></span> | <span data-ttu-id="a0b8c-128">Description</span><span class="sxs-lookup"><span data-stu-id="a0b8c-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-129">**ID**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-129">**id**</span></span> | <span data-ttu-id="a0b8c-130">Identificateur de package ne respectant pas la casse, qui doit être unique dans nuget.org ou dans toute autre galerie susceptible d’héberger le package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-130">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="a0b8c-131">Les ID ne peuvent pas contenir d’espaces ni de caractères qui ne sont pas valides pour une URL et suivent généralement les règles d’espace de noms .NET.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-131">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="a0b8c-132">Pour obtenir des conseils, consultez [Choix d’un identificateur de package unique](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-132">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="a0b8c-133">**version**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-133">**version**</span></span> | <span data-ttu-id="a0b8c-134">Version du package, selon le modèle *version_principale.version_secondaire.version_corrective*.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-134">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="a0b8c-135">Les numéros de version peuvent inclure un suffixe de préversion comme décrit dans [Gestion de versions des packages](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-135">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="a0b8c-136">**description**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-136">**description**</span></span> | <span data-ttu-id="a0b8c-137">Description longue du package pour l’affichage de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-137">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="a0b8c-138">**authors**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-138">**authors**</span></span> | <span data-ttu-id="a0b8c-139">Liste séparée par des virgules des auteurs de packages, qui correspondent aux noms de profil sur nuget.org. Ceux-ci sont affichés dans la galerie NuGet sur nuget.org et servent à croiser les références des packages de mêmes auteurs.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-139">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="a0b8c-140">Éléments de métadonnées facultatifs</span><span class="sxs-lookup"><span data-stu-id="a0b8c-140">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="a0b8c-141">titre</span><span class="sxs-lookup"><span data-stu-id="a0b8c-141">title</span></span>
<span data-ttu-id="a0b8c-142">Titre convivial du package, généralement utilisé dans les affichages de l’interface utilisateur comme sur nuget.org et dans le gestionnaire de package de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-142">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="a0b8c-143">Si non spécifié, l’ID de package est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-143">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="a0b8c-144">owners</span><span class="sxs-lookup"><span data-stu-id="a0b8c-144">owners</span></span>
<span data-ttu-id="a0b8c-145">Liste des créateurs de packages séparés par des virgules, qui utilisent des noms de profil sur nuget.org. Il s’agit souvent de la même liste que dans `authors` et elle est ignorée lors du chargement du package sur nuget.org. Consultez [Gestion des propriétaires de packages sur nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-145">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="a0b8c-146">projectUrl</span><span class="sxs-lookup"><span data-stu-id="a0b8c-146">projectUrl</span></span>
<span data-ttu-id="a0b8c-147">URL de la page d’accueil du package, souvent affichée dans l’interface utilisateur ainsi que sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-147">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="a0b8c-148">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="a0b8c-148">licenseUrl</span></span>
<span data-ttu-id="a0b8c-149">URL de la licence du package, souvent affichée dans l’interface utilisateur ainsi que sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-149">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="iconurl"></a><span data-ttu-id="a0b8c-150">iconUrl</span><span class="sxs-lookup"><span data-stu-id="a0b8c-150">iconUrl</span></span>
<span data-ttu-id="a0b8c-151">URL d’une image 64x64 avec un arrière-plan transparent à utiliser comme icône pour le package dans l’affichage de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-151">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="a0b8c-152">Vérifiez que cet élément contient *l’URL directe de l’image* et non l’URL d’une page web contenant l’image.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-152">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="a0b8c-153">Par exemple, pour utiliser une image à partir de GitHub, utilisez le fichier brut comme URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-153">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="a0b8c-154">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="a0b8c-154">requireLicenseAcceptance</span></span>
<span data-ttu-id="a0b8c-155">Valeur booléenne qui spécifie si le client doit inviter l’utilisateur à accepter la licence du package avant d’installer le package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-155">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="a0b8c-156">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="a0b8c-156">developmentDependency</span></span>
<span data-ttu-id="a0b8c-157">*(2.8+)* Valeur booléenne qui spécifie si le package doit être marqué comme dépendance de développement uniquement, ce qui l’empêche d’être inclus en tant que dépendance dans d’autres packages.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-157">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span>
#### <a name="summary"></a><span data-ttu-id="a0b8c-158">résumé</span><span class="sxs-lookup"><span data-stu-id="a0b8c-158">summary</span></span>
<span data-ttu-id="a0b8c-159">Brève description du package pour l’affichage de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-159">A short description of the package for UI display.</span></span> <span data-ttu-id="a0b8c-160">Si cet élément est omis, une version tronquée de `description` est utilisée.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-160">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="a0b8c-161">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="a0b8c-161">releaseNotes</span></span>
<span data-ttu-id="a0b8c-162">*(1.5+)* Description des changements apportés à cette version du package, souvent utilisée dans l’interface utilisateur, par exemple sous l’onglet **Mises à jour** du Gestionnaire de package Visual Studio à la place de la description du package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-162">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="a0b8c-163">copyright</span><span class="sxs-lookup"><span data-stu-id="a0b8c-163">copyright</span></span>
<span data-ttu-id="a0b8c-164">*(1.5+)* Détails de copyright pour le package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-164">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="a0b8c-165">language</span><span class="sxs-lookup"><span data-stu-id="a0b8c-165">language</span></span>
<span data-ttu-id="a0b8c-166">ID de paramètres régionaux du package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-166">The locale ID for the package.</span></span> <span data-ttu-id="a0b8c-167">Consultez [Création de packages localisés](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-167">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="a0b8c-168">étiquettes</span><span class="sxs-lookup"><span data-stu-id="a0b8c-168">tags</span></span>
<span data-ttu-id="a0b8c-169">Liste de balises et de mots clés délimités par des espaces, qui décrivent le package et permettent de découvrir les packages grâce à des fonctions de recherche et de filtrage.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-169">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="a0b8c-170">pièce remplaçable par</span><span class="sxs-lookup"><span data-stu-id="a0b8c-170">serviceable</span></span> 
<span data-ttu-id="a0b8c-171">*(3.3+)* Uniquement réservé à un usage NuGet interne.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-171">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="a0b8c-172">dépôt</span><span class="sxs-lookup"><span data-stu-id="a0b8c-172">repository</span></span>
<span data-ttu-id="a0b8c-173">Métadonnées du référentiel, composé de quatre attributs facultatifs : *type* et *url* *(4.0 +)*, et *branche* et  *validation* *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-173">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="a0b8c-174">Ces attributs permettent de mapper le fichier .nupkg vers le référentiel qui, générés avec la possibilité d’obtenir aussi détaillée que la branche individuel ou de la validation qui a créé le package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-174">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="a0b8c-175">Ce doit être une url accessible au public qui peut être appelé directement par un logiciel de contrôle de version.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-175">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="a0b8c-176">Il ne doit pas être une page html comme cela est destiné à l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-176">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="a0b8c-177">Pour un lien vers la page de projet, utilisez le `projectUrl` champ, à la place. |</span><span class="sxs-lookup"><span data-stu-id="a0b8c-177">For linking to project page, use the `projectUrl` field, instead.|</span></span>
#### <a name="minclientversion"></a><span data-ttu-id="a0b8c-178">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="a0b8c-178">minClientVersion</span></span>
<span data-ttu-id="a0b8c-179">Spécifie la version minimale du client NuGet qui peut installer ce package, appliquée par nuget.exe et le gestionnaire de package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-179">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="a0b8c-180">Cet attribut est utilisé chaque fois que le package dépend de fonctionnalités spécifiques du fichier `.nuspec` qui ont été ajoutées dans une version particulière du client NuGet.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-180">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="a0b8c-181">Par exemple, un package utilisant l’attribut `developmentDependency` doit spécifier « 2.8 » pour `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-181">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="a0b8c-182">De même, un package utilisant l’élément `contentFiles` (consultez la section suivante) doit affecter à `minClientVersion` la valeur « 3.3 ».</span><span class="sxs-lookup"><span data-stu-id="a0b8c-182">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="a0b8c-183">Notez également que, comme les clients NuGet antérieurs à 2.5 ne reconnaissent pas cet indicateur, ils refusent *toujours* d’installer le package, quel que soit le contenu de `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-183">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="a0b8c-184">Éléments de collection</span><span class="sxs-lookup"><span data-stu-id="a0b8c-184">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="a0b8c-185">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="a0b8c-185">packageTypes</span></span>
<span data-ttu-id="a0b8c-186">*(3.5+)* Collection de zéro ou plusieurs éléments `<packageType>` spécifiant le type du package s’il est différent du package de dépendances classique.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-186">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="a0b8c-187">Chaque élément packageType a des attributs *name* et *version*.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-187">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="a0b8c-188">Consultez [Définition d’un type de package](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-188">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="a0b8c-189">dépendances</span><span class="sxs-lookup"><span data-stu-id="a0b8c-189">dependencies</span></span>
<span data-ttu-id="a0b8c-190">Collection de zéro ou plusieurs éléments `<dependency>` spécifiant les dépendances du package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-190">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="a0b8c-191">Chaque dépendance a des attributs *id*, *version*, *include* (3.x+) et *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-191">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="a0b8c-192">Consultez [Dépendances](#dependencies-element) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-192">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="a0b8c-193">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="a0b8c-193">frameworkAssemblies</span></span>
<span data-ttu-id="a0b8c-194">*(1.2 +)* Collection de zéro ou plusieurs éléments `<frameworkAssembly>` identifiant les références d’assembly .NET Framework nécessaires à ce package, ce qui garantit que les références sont ajoutées à des projets utilisant le package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-194">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="a0b8c-195">Chaque élément frameworkAssembly a des attributs *assemblyName* et *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-195">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="a0b8c-196">Consultez [Références d’assembly Framework](#specifying-framework-assembly-references-gac) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-196">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="a0b8c-197">Références</span><span class="sxs-lookup"><span data-stu-id="a0b8c-197">references</span></span>
<span data-ttu-id="a0b8c-198">*(1.5+)* Collection de zéro ou plusieurs éléments `<reference>` nommant des assemblys dans le dossier `lib` du package qui sont ajoutés en tant que références de projet.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-198">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="a0b8c-199">Chaque référence a un attribut *file*.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-199">Each reference has a *file* attribute.</span></span> <span data-ttu-id="a0b8c-200">`<references>` peut également contenir un élément `<group>` avec un attribut *targetFramework* qui contient à son tour des éléments `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-200">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="a0b8c-201">Si cet élément est omis, toutes les références dans `lib` sont incluses.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-201">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="a0b8c-202">Consultez [Références d’assembly explicite](#specifying-explicit-assembly-references) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-202">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="a0b8c-203">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a0b8c-203">contentFiles</span></span>
<span data-ttu-id="a0b8c-204">*(3.3+)* Collection d’éléments `<files>` qui identifient les fichiers de contenu à inclure dans le projet de consommation.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-204">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="a0b8c-205">Ces fichiers sont spécifiés avec un ensemble d’attributs qui décrivent comment ils doivent être utilisés dans le système de projet.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-205">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="a0b8c-206">Consultez [Inclusion des fichiers d’assembly](#specifying-files-to-include-in-the-package) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-206">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="a0b8c-207">fichiers </span><span class="sxs-lookup"><span data-stu-id="a0b8c-207">files</span></span> 
<span data-ttu-id="a0b8c-208">Le nœud `<package>` peut contenir un nœud `<files>` en tant que frère de `<metadata>` et/ou un enfant `<contentFiles>` sous `<metadata>` pour indiquer l’assembly et les fichiers de contenu à inclure dans le package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-208">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="a0b8c-209">Consultez [Inclusion des fichiers d’assembly](#including-assembly-files) et [Inclusion des fichiers de contenu](#including-content-files) plus loin dans cette rubrique pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-209">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="a0b8c-210">Jetons de remplacement</span><span class="sxs-lookup"><span data-stu-id="a0b8c-210">Replacement tokens</span></span>

<span data-ttu-id="a0b8c-211">Lors de la création d’un package, la [commande `nuget pack`](../tools/cli-ref-pack.md) remplace les jetons séparés par des $ dans le nœud `<metadata>` du fichier `.nuspec` par des valeurs provenant d’un fichier projet ou du commutateur `-properties` de la commande `pack`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-211">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="a0b8c-212">Sur la ligne de commande, vous spécifiez des valeurs de jeton avec `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-212">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="a0b8c-213">Par exemple, vous pouvez utiliser un jeton tel que `$owners$` et `$desc$` dans le fichier `.nuspec` et fournir les valeurs au moment de la compression comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-213">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="a0b8c-214">Pour utiliser les valeurs à partir d’un projet, spécifiez les jetons décrits dans le tableau ci-dessous (AssemblyInfo fait référence au fichier dans `Properties` comme `AssemblyInfo.cs` ou `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-214">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="a0b8c-215">Pour utiliser ces jetons, exécutez `nuget pack` avec le fichier projet et non simplement le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-215">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="a0b8c-216">Par exemple, quand vous utilisez la commande suivante, les jetons `$id$` et `$version$` dans un fichier `.nuspec` sont remplacés par les valeurs `AssemblyName` et `AssemblyVersion` du projet :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-216">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="a0b8c-217">En général, quand vous avez un projet, vous créez le fichier `.nuspec` initialement à l’aide de `nuget spec MyProject.csproj` qui inclut automatiquement certains de ces jetons standard.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-217">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="a0b8c-218">Toutefois, si un projet ne possède pas de valeurs pour les éléments `.nuspec` requis, `nuget pack` échoue.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-218">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="a0b8c-219">De plus, si vous modifiez des valeurs de projet, veillez à regénérer avant de créer le package ; pour effectuer cette opération en toute facilité, utilisez le commutateur `build` de la commande pack.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-219">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="a0b8c-220">À l’exception de `$configuration$`, les valeurs dans le projet sont préférées à celles affectées au même jeton sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-220">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="a0b8c-221">Token</span><span class="sxs-lookup"><span data-stu-id="a0b8c-221">Token</span></span> | <span data-ttu-id="a0b8c-222">Source de valeur</span><span class="sxs-lookup"><span data-stu-id="a0b8c-222">Value source</span></span> | <span data-ttu-id="a0b8c-223">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-223">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="a0b8c-224">**$id$**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-224">**$id$**</span></span> | <span data-ttu-id="a0b8c-225">Fichier projet</span><span class="sxs-lookup"><span data-stu-id="a0b8c-225">Project file</span></span> | <span data-ttu-id="a0b8c-226">AssemblyName (titre) à partir du fichier de projet</span><span class="sxs-lookup"><span data-stu-id="a0b8c-226">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="a0b8c-227">**$version$**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-227">**$version$**</span></span> | <span data-ttu-id="a0b8c-228">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a0b8c-228">AssemblyInfo</span></span> | <span data-ttu-id="a0b8c-229">AssemblyInformationalVersion si présente, sinon AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="a0b8c-229">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="a0b8c-230">**$author$**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-230">**$author$**</span></span> | <span data-ttu-id="a0b8c-231">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a0b8c-231">AssemblyInfo</span></span> | <span data-ttu-id="a0b8c-232">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="a0b8c-232">AssemblyCompany</span></span> |
| <span data-ttu-id="a0b8c-233">**$title$**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-233">**$title$**</span></span> | <span data-ttu-id="a0b8c-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a0b8c-234">AssemblyInfo</span></span> | <span data-ttu-id="a0b8c-235">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="a0b8c-235">AssemblyTitle</span></span> |
| <span data-ttu-id="a0b8c-236">**$description$**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-236">**$description$**</span></span> | <span data-ttu-id="a0b8c-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a0b8c-237">AssemblyInfo</span></span> | <span data-ttu-id="a0b8c-238">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="a0b8c-238">AssemblyDescription</span></span> |
| <span data-ttu-id="a0b8c-239">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-239">**$copyright$**</span></span> | <span data-ttu-id="a0b8c-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a0b8c-240">AssemblyInfo</span></span> | <span data-ttu-id="a0b8c-241">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="a0b8c-241">AssemblyCopyright</span></span> |
| <span data-ttu-id="a0b8c-242">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-242">**$configuration$**</span></span> | <span data-ttu-id="a0b8c-243">DLL d’assembly</span><span class="sxs-lookup"><span data-stu-id="a0b8c-243">Assembly DLL</span></span> | <span data-ttu-id="a0b8c-244">Configuration utilisée pour générer l’assembly, Debug étant la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-244">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="a0b8c-245">Notez que, pour créer un package à l’aide d’une configuration Release, vous utilisez toujours `-properties Configuration=Release` sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-245">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="a0b8c-246">Les jetons peuvent également être utilisés pour résoudre les chemins quand vous incluez des [fichiers d’assembly](#including-assembly-files) et [fichiers de contenu](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-246">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="a0b8c-247">Les jetons ont les mêmes noms que les propriétés MSBuild, ce qui permet de sélectionner les fichiers à inclure en fonction de la configuration de build actuelle.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-247">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="a0b8c-248">Par exemple, si vous utilisez les jetons suivants dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-248">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="a0b8c-249">Et que vous générez un assembly dont `AssemblyName` est `LoggingLibrary` avec la configuration `Release` dans MSBuild, les lignes résultantes dans le fichier `.nuspec` du package sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-249">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="a0b8c-250">Élément de dépendances</span><span class="sxs-lookup"><span data-stu-id="a0b8c-250">Dependencies element</span></span>

<span data-ttu-id="a0b8c-251">L’élément `<dependencies>` dans `<metadata>` contient un nombre quelconque d’éléments `<dependency>` qui identifient d’autres packages dont dépend le package de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-251">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="a0b8c-252">Les attributs pour chaque élément `<dependency>` sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-252">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="a0b8c-253">Attribut</span><span class="sxs-lookup"><span data-stu-id="a0b8c-253">Attribute</span></span> | <span data-ttu-id="a0b8c-254">Description</span><span class="sxs-lookup"><span data-stu-id="a0b8c-254">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="a0b8c-255">(Obligatoire) ID de package de la dépendance, tel que « EntityFramework » et « NUnit », qui est le nom du package nuget.org affiché sur une page de package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-255">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="a0b8c-256">(Obligatoire) Plage de versions acceptables en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-256">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="a0b8c-257">Consultez [Gestion de versions des packages](../reference/package-versioning.md#version-ranges-and-wildcards) pour connaître la syntaxe exacte.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-257">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="a0b8c-258">include</span><span class="sxs-lookup"><span data-stu-id="a0b8c-258">include</span></span> | <span data-ttu-id="a0b8c-259">Liste de balises include/exclude séparées par des virgules (voir ci-dessous) indiquant la dépendance à inclure dans le package final.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-259">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="a0b8c-260">La valeur par défaut est `none`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-260">The default value is `none`.</span></span> |
| <span data-ttu-id="a0b8c-261">exclude</span><span class="sxs-lookup"><span data-stu-id="a0b8c-261">exclude</span></span> | <span data-ttu-id="a0b8c-262">Liste de balises include/exclude séparées par des virgules (voir ci-dessous) indiquant la dépendance à exclure dans le package final.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="a0b8c-263">La valeur par défaut est `all`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-263">The  default value is `all`.</span></span> <span data-ttu-id="a0b8c-264">Les balises spécifiées avec `exclude` sont prioritaires sur celles spécifiées avec `include`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-264">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="a0b8c-265">Par exemple, `include="runtime, compile" exclude="compile"` est identique à `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-265">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="a0b8c-266">Balise include/exclude</span><span class="sxs-lookup"><span data-stu-id="a0b8c-266">Include/Exclude tag</span></span> | <span data-ttu-id="a0b8c-267">Dossiers affectés de la cible</span><span class="sxs-lookup"><span data-stu-id="a0b8c-267">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-268">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a0b8c-268">contentFiles</span></span> | <span data-ttu-id="a0b8c-269">Contenu</span><span class="sxs-lookup"><span data-stu-id="a0b8c-269">Content</span></span> |
| <span data-ttu-id="a0b8c-270">runtime</span><span class="sxs-lookup"><span data-stu-id="a0b8c-270">runtime</span></span> | <span data-ttu-id="a0b8c-271">Runtime, Resources et FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="a0b8c-271">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="a0b8c-272">compile</span><span class="sxs-lookup"><span data-stu-id="a0b8c-272">compile</span></span> | <span data-ttu-id="a0b8c-273">lib</span><span class="sxs-lookup"><span data-stu-id="a0b8c-273">lib</span></span> |
| <span data-ttu-id="a0b8c-274">build</span><span class="sxs-lookup"><span data-stu-id="a0b8c-274">build</span></span> | <span data-ttu-id="a0b8c-275">build (propriétés et cibles MSBuild)</span><span class="sxs-lookup"><span data-stu-id="a0b8c-275">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="a0b8c-276">native</span><span class="sxs-lookup"><span data-stu-id="a0b8c-276">native</span></span> | <span data-ttu-id="a0b8c-277">native</span><span class="sxs-lookup"><span data-stu-id="a0b8c-277">native</span></span> |
| <span data-ttu-id="a0b8c-278">none</span><span class="sxs-lookup"><span data-stu-id="a0b8c-278">none</span></span> | <span data-ttu-id="a0b8c-279">Aucun dossier</span><span class="sxs-lookup"><span data-stu-id="a0b8c-279">No folders</span></span> |
| <span data-ttu-id="a0b8c-280">all</span><span class="sxs-lookup"><span data-stu-id="a0b8c-280">all</span></span> | <span data-ttu-id="a0b8c-281">Tous les dossiers</span><span class="sxs-lookup"><span data-stu-id="a0b8c-281">All folders</span></span> |

<span data-ttu-id="a0b8c-282">Par exemple, les lignes suivantes indiquent les dépendances sur `PackageA` version 1.1.0 ou ultérieure, et `PackageB` version 1.x.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-282">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="a0b8c-283">Les lignes suivantes indiquent les dépendances sur les mêmes packages, mais spécifient d’inclure les dossiers `contentFiles` et `build` de `PackageA` et tous les éléments sauf les dossiers `native` et `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-283">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="a0b8c-284">Remarque : Quand vous créez un fichier `.nuspec` à partir d’un projet avec `nuget spec`, les dépendances qui existent dans le projet sont automatiquement incluses dans le fichier `.nuspec` obtenu.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-284">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="a0b8c-285">Groupes de dépendances</span><span class="sxs-lookup"><span data-stu-id="a0b8c-285">Dependency groups</span></span>

<span data-ttu-id="a0b8c-286">*Version 2.0+*</span><span class="sxs-lookup"><span data-stu-id="a0b8c-286">*Version 2.0+*</span></span>

<span data-ttu-id="a0b8c-287">Comme alternative à une liste plate unique, les dépendances peuvent être spécifiées selon le profil de framework du projet cible avec les éléments `<group>` dans `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-287">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="a0b8c-288">Chaque groupe possède un attribut nommé `targetFramework` et contient zéro ou plusieurs éléments `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-288">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="a0b8c-289">Ces dépendances sont installées ensemble quand la version cible de .NET Framework est compatible avec le profil de framework du projet.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-289">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="a0b8c-290">L’élément `<group>` sans un attribut `targetFramework` est utilisé comme valeur par défaut ou liste de secours de dépendances.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-290">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="a0b8c-291">Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-291">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="a0b8c-292">Le format de groupe ne peut pas être mélangé avec une liste plate.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-292">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="a0b8c-293">L’exemple suivant illustre différentes variantes de l’élément `<group>` :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-293">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="a0b8c-294">Références d’assembly explicite</span><span class="sxs-lookup"><span data-stu-id="a0b8c-294">Explicit assembly references</span></span>

<span data-ttu-id="a0b8c-295">L’élément `<references>` spécifie explicitement les assemblys que le projet cible doit référencer lors de l’utilisation du package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-295">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="a0b8c-296">Quand cet élément est présent, NuGet n’ajoute des références qu’aux assemblys répertoriés ; il n’ajoute de références pour aucun autre assembly dans le dossier `lib` du package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-296">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="a0b8c-297">Par exemple, l’élément `<references>` suivant demande à NuGet d’ajouter des références à `xunit.dll` et `xunit.extensions.dll` uniquement même s’il existe d’autres assemblys dans le package :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-297">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="a0b8c-298">Des références explicites sont généralement utilisées pour les assemblys uniquement au moment du design.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-298">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="a0b8c-299">Quand vous utilisez des [contrats de code](/dotnet/framework/debug-trace-profile/code-contracts), par exemple, les assemblys de contrat doivent être en regard des assemblys de runtime qu’ils augmentent afin que Visual Studio puisse les trouver, mais les assemblys de contrat n’ont pas à être référencés par le projet ni copiés dans le dossier `bin` du projet.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-299">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="a0b8c-300">De même, des références explicites peuvent servir pour les frameworks de tests unitaires, tels que XUnit,dont les assemblys d’outils doivent être situés en regard des assemblys de runtime, mais qui n’ont pas besoin d’être inclus comme références de projet.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-300">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="a0b8c-301">Groupes de référence</span><span class="sxs-lookup"><span data-stu-id="a0b8c-301">Reference groups</span></span>

<span data-ttu-id="a0b8c-302">Comme alternative à une liste plate unique, les références peuvent être spécifiées selon le profil de framework du projet cible avec les éléments `<group>` dans `<references>`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-302">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="a0b8c-303">Chaque groupe possède un attribut nommé `targetFramework` et contient zéro ou plusieurs éléments `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-303">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="a0b8c-304">Ces références sont ajoutées à un projet quand la version cible de .NET Framework est compatible avec le profil de framework du projet.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-304">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="a0b8c-305">L’élément `<group>` sans un attribut `targetFramework` est utilisé comme valeur par défaut ou liste de secours de références.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-305">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="a0b8c-306">Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-306">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="a0b8c-307">Le format de groupe ne peut pas être mélangé avec une liste plate.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-307">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="a0b8c-308">L’exemple suivant illustre différentes variantes de l’élément `<group>` :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-308">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="a0b8c-309">Références d’assembly Framework</span><span class="sxs-lookup"><span data-stu-id="a0b8c-309">Framework assembly references</span></span>

<span data-ttu-id="a0b8c-310">Les assemblys Framework sont ceux qui font partie du .NET Framework et doivent déjà figurer dans le GAC (Global Assembly Cache) pour un ordinateur donné.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-310">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="a0b8c-311">En identifiant ces assemblys dans l’élément `<frameworkAssemblies>`, un package peut garantir que les références requises sont ajoutées à un projet si le projet ne dispose pas déjà de telles références.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-311">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="a0b8c-312">Ces assemblys, bien entendu, ne sont pas directement inclus dans un package.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-312">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="a0b8c-313">L’élément `<frameworkAssemblies>` contient zéro ou plusieurs éléments `<frameworkAssembly>`, chacun d’eux spécifiant les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-313">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="a0b8c-314">Attribut</span><span class="sxs-lookup"><span data-stu-id="a0b8c-314">Attribute</span></span> | <span data-ttu-id="a0b8c-315">Description</span><span class="sxs-lookup"><span data-stu-id="a0b8c-315">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-316">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-316">**assemblyName**</span></span> | <span data-ttu-id="a0b8c-317">(Obligatoire) Nom d’assembly qualifié complet.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-317">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="a0b8c-318">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-318">**targetFramework**</span></span> | <span data-ttu-id="a0b8c-319">(Facultatif) Spécifie la version cible de .NET Framework à laquelle s’applique cette référence.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-319">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="a0b8c-320">Si cet attribut est omis, indique que la référence s’applique à tous les frameworks.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-320">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="a0b8c-321">Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-321">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="a0b8c-322">L’exemple suivant montre une référence à `System.Net` pour toutes les versions cibles de .NET Framework et une référence à `System.ServiceModel` pour .NET Framework 4.0 uniquement :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-322">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="a0b8c-323">Inclusion des fichiers d’assembly</span><span class="sxs-lookup"><span data-stu-id="a0b8c-323">Including assembly files</span></span>

<span data-ttu-id="a0b8c-324">Si vous suivez les conventions décrites dans [Création d’un package](../create-packages/creating-a-package.md), il est inutile de spécifier explicitement une liste de fichiers dans le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-324">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="a0b8c-325">La commande `nuget pack` sélectionne automatiquement les fichiers nécessaires.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-325">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="a0b8c-326">Quand un package est installé dans un projet, NuGet ajoute automatiquement des références d’assembly aux DLL du package, *à l’exclusion* de celles nommées `.resources.dll`, car elles sont supposées être des assemblys satellites localisés.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-326">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="a0b8c-327">C’est pourquoi vous devez éviter d’utiliser `.resources.dll` pour les fichiers qui contiennent du code de package essentiel.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-327">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="a0b8c-328">Pour ignorer ce comportement automatique et contrôler explicitement les fichiers qui sont inclus dans un package, placez un élément `<files>` en tant qu’enfant de `<package>` (et frère de `<metadata>`), identifiant chaque fichier avec un élément `<file>` distinct.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-328">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="a0b8c-329">Exemple :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-329">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="a0b8c-330">Avec NuGet 2.x et versions antérieures, et des projets utilisant `packages.config`, l’élément `<files>` est également utilisé pour inclure les fichiers de contenu non modifiables quand un package est installé.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-330">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="a0b8c-331">Avec NuGet 3.3+ et les projets PackageReference, l’élément `<contentFiles>` est utilisé à la place.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-331">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="a0b8c-332">Consultez [Inclusion des fichiers de contenu](#including-content-files) ci-dessous pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-332">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="a0b8c-333">Attributs des éléments File</span><span class="sxs-lookup"><span data-stu-id="a0b8c-333">File element attributes</span></span>

<span data-ttu-id="a0b8c-334">Chaque élément `<file>` spécifie les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-334">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="a0b8c-335">Attribut</span><span class="sxs-lookup"><span data-stu-id="a0b8c-335">Attribute</span></span> | <span data-ttu-id="a0b8c-336">Description</span><span class="sxs-lookup"><span data-stu-id="a0b8c-336">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-337">**src**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-337">**src**</span></span> | <span data-ttu-id="a0b8c-338">Emplacement du ou des fichiers à inclure, soumis à des exclusions définies par l’attribut `exclude`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-338">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="a0b8c-339">Le chemin est relatif au fichier `.nuspec` sauf si un chemin absolu est spécifié.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-339">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="a0b8c-340">Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-340">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a0b8c-341">**target**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-341">**target**</span></span> | <span data-ttu-id="a0b8c-342">Chemin relatif vers le dossier dans le package où les fichiers sources sont placés, qui doit commencer par `lib`, `content`, `build` ou `tools`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-342">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="a0b8c-343">Consultez [Création d’un fichier .nuspec à partir d’un répertoire de travail basé sur une convention](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-343">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="a0b8c-344">**exclude**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-344">**exclude**</span></span> | <span data-ttu-id="a0b8c-345">Liste de fichiers ou de modèles de fichiers séparés par un point-virgule à exclure de l’emplacement `src`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-345">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="a0b8c-346">Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-346">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="a0b8c-347">Exemples</span><span class="sxs-lookup"><span data-stu-id="a0b8c-347">Examples</span></span>

<span data-ttu-id="a0b8c-348">**Assembly unique**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-348">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="a0b8c-349">**Assembly unique spécifique à une version cible de .NET Framework**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-349">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="a0b8c-350">**Ensemble de DLL avec un caractère générique**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-350">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="a0b8c-351">**DLL de différents frameworks**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-351">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="a0b8c-352">**Exclusion de fichiers**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-352">**Excluding files**</span></span>

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="a0b8c-353">Inclusion des fichiers de contenu</span><span class="sxs-lookup"><span data-stu-id="a0b8c-353">Including content files</span></span>

<span data-ttu-id="a0b8c-354">Les fichiers de contenu sont des fichiers non modifiables qu’un package doit inclure dans un projet.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-354">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="a0b8c-355">Comme ils ne sont pas modifiables, ils ne sont pas destinés à être changés par le projet de consommation.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-355">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="a0b8c-356">Des exemples de fichiers de contenu sont notamment :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-356">Example content files include:</span></span>

- <span data-ttu-id="a0b8c-357">Images incorporées en tant que ressources</span><span class="sxs-lookup"><span data-stu-id="a0b8c-357">Images that are embedded as resources</span></span>
- <span data-ttu-id="a0b8c-358">Fichiers sources qui sont déjà compilés</span><span class="sxs-lookup"><span data-stu-id="a0b8c-358">Source files that are already compiled</span></span>
- <span data-ttu-id="a0b8c-359">Scripts qui doivent être inclus avec la sortie de génération du projet</span><span class="sxs-lookup"><span data-stu-id="a0b8c-359">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="a0b8c-360">Fichiers de configuration pour le package qui doivent être inclus dans le projet, mais ne nécessitent aucune modification spécifique au projet</span><span class="sxs-lookup"><span data-stu-id="a0b8c-360">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="a0b8c-361">Les fichiers de contenu sont inclus dans un package à l’aide de l’élément `<files>`, en spécifiant le dossier `content` dans l’attribut `target`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-361">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="a0b8c-362">Toutefois, ces fichiers sont ignorés quand le package est installé dans un projet utilisant PackageReference, qui utilise à la place l’élément `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-362">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="a0b8c-363">Pour une compatibilité maximale avec les projets de consommation, un package spécifie dans l’idéal les fichiers de contenu dans les deux éléments.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-363">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="a0b8c-364">Utilisation de l’élément files pour les fichiers de contenu</span><span class="sxs-lookup"><span data-stu-id="a0b8c-364">Using the files element for content files</span></span>

<span data-ttu-id="a0b8c-365">Pour les fichiers de contenu, utilisez simplement le même format que pour les fichiers d’assembly, mais spécifiez `content` comme dossier de base dans l’attribut `target` comme indiqué dans les exemples suivants.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-365">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="a0b8c-366">**Fichiers de contenu de base**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-366">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="a0b8c-367">**Fichiers de contenu avec structure de répertoires**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-367">**Content files with directory structure**</span></span>

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

<span data-ttu-id="a0b8c-368">**Fichier de contenu spécifique à une version cible de .NET Framework**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-368">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="a0b8c-369">**Fichier de contenu copié vers un dossier avec un point dans le nom**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-369">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="a0b8c-370">Dans ce cas, NuGet détecte que l’extension dans `target` ne correspond pas à l’extension dans `src` et traite par conséquent cette partie du nom dans `target` en tant que dossier :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-370">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="a0b8c-371">**Fichiers de contenu sans extensions**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-371">**Content files without extensions**</span></span>

<span data-ttu-id="a0b8c-372">Pour inclure les fichiers sans extension, utilisez les caractères génériques `*` ou `**` :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-372">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="a0b8c-373">**Fichiers de contenu avec chemin complet et cible complète**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-373">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="a0b8c-374">Dans ce cas, étant donné que les extensions de fichier de la source et de la cible correspondent, NuGet part du principe que la cible est un nom de fichier et non un dossier :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-374">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="a0b8c-375">**Modification du nom d’un fichier de contenu dans le package**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-375">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="a0b8c-376">**Exclusion de fichiers**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-376">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="a0b8c-377">Utilisation de l’élément contentFiles pour les fichiers de contenu</span><span class="sxs-lookup"><span data-stu-id="a0b8c-377">Using the contentFiles element for content files</span></span>

<span data-ttu-id="a0b8c-378">*NuGet 4.0 + avec PackageReference*</span><span class="sxs-lookup"><span data-stu-id="a0b8c-378">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="a0b8c-379">Par défaut, un package place le contenu dans un dossier `contentFiles` (voir ci-dessous) et `nuget pack` a mis tous les fichiers dans ce dossier à l’aide des attributs par défaut.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-379">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="a0b8c-380">Dans ce cas, il n’est pas du tout nécessaire d’inclure un nœud `contentFiles` dans le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-380">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="a0b8c-381">Pour contrôler les fichiers qui sont inclus, l’élément `<contentFiles>` spécifie une collection d’éléments `<files>` qui identifient exactement les fichiers à ajouter.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-381">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="a0b8c-382">Ces fichiers sont spécifiés avec un ensemble d’attributs qui décrivent comment ils doivent être utilisés dans le système de projet :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-382">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="a0b8c-383">Attribut</span><span class="sxs-lookup"><span data-stu-id="a0b8c-383">Attribute</span></span> | <span data-ttu-id="a0b8c-384">Description</span><span class="sxs-lookup"><span data-stu-id="a0b8c-384">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-385">**include**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-385">**include**</span></span> | <span data-ttu-id="a0b8c-386">(Obligatoire) Emplacement du ou des fichiers à inclure, soumis à des exclusions définies par l’attribut `exclude`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-386">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="a0b8c-387">Le chemin est relatif au fichier `.nuspec` sauf si un chemin absolu est spécifié.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-387">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="a0b8c-388">Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-388">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a0b8c-389">**exclude**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-389">**exclude**</span></span> | <span data-ttu-id="a0b8c-390">Liste de fichiers ou de modèles de fichiers séparés par un point-virgule à exclure de l’emplacement `src`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-390">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="a0b8c-391">Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a0b8c-392">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-392">**buildAction**</span></span> | <span data-ttu-id="a0b8c-393">Action de génération à affecter à l’élément de contenu pour MSBuild, comme `Content`, `None`, `Embedded Resource`, `Compile`, etc. La valeur par défaut est `Compile`.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-393">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="a0b8c-394">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-394">**copyToOutput**</span></span> | <span data-ttu-id="a0b8c-395">Valeur booléenne indiquant s’il faut copier des éléments de contenu à la build (ou publiez) dossier de sortie.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-395">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="a0b8c-396">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-396">The default is false.</span></span> |
| <span data-ttu-id="a0b8c-397">**flatten**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-397">**flatten**</span></span> | <span data-ttu-id="a0b8c-398">Valeur booléenne indiquant s’il faut copier des éléments de contenu dans un dossier unique dans la sortie de génération (true) ou conserver la structure de dossiers dans le package (false).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-398">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="a0b8c-399">Cet indicateur fonctionne uniquement lorsque l’indicateur copyToOutput est défini sur true.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-399">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="a0b8c-400">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-400">The default is false.</span></span> |

<span data-ttu-id="a0b8c-401">Lors de l’installation d’un package, NuGet applique les éléments enfants de `<contentFiles>` de haut en bas.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-401">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="a0b8c-402">Si plusieurs entrées correspondent au même fichier, toutes les entrées sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-402">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="a0b8c-403">L’entrée supérieure remplace les entrées inférieures s’il existe un conflit pour le même attribut.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-403">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="a0b8c-404">Structure de dossiers de package</span><span class="sxs-lookup"><span data-stu-id="a0b8c-404">Package folder structure</span></span>

<span data-ttu-id="a0b8c-405">Le projet de package doit structurer le contenu à l’aide du modèle suivant :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-405">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="a0b8c-406">`codeLanguages` peut être `cs`, `vb`, `fs`, `any`, ou l’équivalent en minuscules d’un élément `$(ProjectLanguage)` donné.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-406">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="a0b8c-407">`TxM` est n’importe quel moniker du Framework cible légal pris en charge par NuGet (consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="a0b8c-407">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="a0b8c-408">Toute structure de dossiers peut être ajoutée à la fin de cette syntaxe.</span><span class="sxs-lookup"><span data-stu-id="a0b8c-408">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="a0b8c-409">Exemple :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-409">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="a0b8c-410">Les dossiers vides peuvent utiliser `.` pour choisir de ne pas fournir de contenu pour certaines combinaisons de langage et TxM, par exemple :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-410">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="a0b8c-411">Exemple de section contentFiles</span><span class="sxs-lookup"><span data-stu-id="a0b8c-411">Example contentFiles section</span></span>

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="a0b8c-412">Exemples de fichiers nuspec</span><span class="sxs-lookup"><span data-stu-id="a0b8c-412">Example nuspec files</span></span>

<span data-ttu-id="a0b8c-413">**Fichier `.nuspec` simple qui ne spécifie pas de dépendances ni de fichiers**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-413">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="a0b8c-414">**Fichier `.nuspec` avec des dépendances**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-414">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="a0b8c-415">**Fichier `.nuspec` avec des fichiers**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-415">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="a0b8c-416">**Fichier `.nuspec` avec des assemblys Framework**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-416">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="a0b8c-417">Dans cet exemple, les éléments suivants sont installés pour les cibles de projets spécifiques :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-417">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="a0b8c-418">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="a0b8c-418">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="a0b8c-419">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="a0b8c-419">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="a0b8c-420">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="a0b8c-420">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="a0b8c-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="a0b8c-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="a0b8c-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="a0b8c-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
