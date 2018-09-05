---
title: Notes de version 1.5 de NuGet
description: Notes de publication pour 1.5 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548723"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="c2168-103">Notes de version 1.5 de NuGet</span><span class="sxs-lookup"><span data-stu-id="c2168-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="c2168-104">[Notes de publication de NuGet 1.4](../release-notes/nuget-1.4.md) | [Notes de publication de NuGet 1.6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="c2168-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="c2168-105">NuGet 1.5 a été publiée le 30 août 2011.</span><span class="sxs-lookup"><span data-stu-id="c2168-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="c2168-106">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="c2168-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="c2168-107">Modèles de projet avec les Packages NuGet préinstallés</span><span class="sxs-lookup"><span data-stu-id="c2168-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="c2168-108">Lorsque vous créez un nouveau modèle de projet ASP.NET MVC 3, les bibliothèques de scripts jQuery inclus dans le projet réellement y sont placés en installant les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="c2168-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="c2168-109">Le modèle de projet ASP.NET MVC 3 inclut un ensemble de packages NuGet installés lorsque le modèle de projet est appelé.</span><span class="sxs-lookup"><span data-stu-id="c2168-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="c2168-110">Cette possibilité d’inclure des packages NuGet avec un modèle de projet est maintenant une fonctionnalité de NuGet qui _n’importe quel_ modèle de projet permettre désormais tirer parti de.</span><span class="sxs-lookup"><span data-stu-id="c2168-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="c2168-111">Pour plus d’informations sur cette fonctionnalité, consultez ce [billet de blog par le développeur de la fonctionnalité](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2168-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="c2168-112">Références d’Assembly explicite</span><span class="sxs-lookup"><span data-stu-id="c2168-112">Explicit Assembly References</span></span>

<span data-ttu-id="c2168-113">Ajouté une nouvelle `<references />` élément utilisé pour spécifier explicitement les assemblys dans le package doit être référencé.</span><span class="sxs-lookup"><span data-stu-id="c2168-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="c2168-114">Par exemple, si vous ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="c2168-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="c2168-115">Seuls les `xunit.dll` et `xunit.extensions.dll` sera référencé à partir de la commande appropriée [sous-dossier de framework/profil](../reference/nuspec.md#explicit-assembly-references) de la `lib` dossier même si d’autres assemblys dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="c2168-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="c2168-116">Si cet élément est omis, le comportement habituel s’applique, qui consiste à faire référence à chaque assembly dans le `lib` dossier.</span><span class="sxs-lookup"><span data-stu-id="c2168-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="c2168-117">__Quelle est l’utilité de cette fonctionnalité ?__</span><span class="sxs-lookup"><span data-stu-id="c2168-117">__What is this feature used for?__</span></span>

<span data-ttu-id="c2168-118">Cette fonctionnalité prend en charge les assemblys uniquement au moment du design.</span><span class="sxs-lookup"><span data-stu-id="c2168-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="c2168-119">Par exemple, lorsque vous utilisez des contrats de Code, les assemblys de contrat doivent être en regard des assemblys de runtime qu’ils augmentent afin que Visual Studio puisse les trouver, mais les assemblys de contrat ne doivent pas réellement être référencés par le projet et ne doivent pas être copiés dans le `bin` dossier.</span><span class="sxs-lookup"><span data-stu-id="c2168-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="c2168-120">De même, la fonctionnalité peut être utilisée à pour les infrastructures de tests unitaires comme XUnit nécessitant ses assemblys d’outils située en regard des assemblys par le runtime, mais exclu des références de projet.</span><span class="sxs-lookup"><span data-stu-id="c2168-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="c2168-121">Ajout de la possibilité d’exclure des fichiers dans le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="c2168-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="c2168-122">Le `<file>` élément au sein d’un `.nuspec` fichier peut être utilisé pour inclure un fichier spécifique ou un ensemble de fichiers à l’aide d’un caractère générique.</span><span class="sxs-lookup"><span data-stu-id="c2168-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="c2168-123">Lorsque vous utilisez un caractère générique, il n’existe aucun moyen pour exclure un sous-ensemble spécifique des fichiers inclus.</span><span class="sxs-lookup"><span data-stu-id="c2168-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="c2168-124">Par exemple, supposons que vous voulez tous les fichiers de texte dans un dossier à l’exception d’une valeur spécifique.</span><span class="sxs-lookup"><span data-stu-id="c2168-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="c2168-125">Utilisez des points-virgules pour spécifier plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="c2168-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="c2168-126">Ou utilisez un caractère générique à exclure un ensemble de fichiers tels que tous les fichiers de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="c2168-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="c2168-127">Suppression des packages à l’aide de la boîte de dialogue vous invite à entrer pour supprimer des dépendances</span><span class="sxs-lookup"><span data-stu-id="c2168-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="c2168-128">Lorsque vous désinstallez un package avec des dépendances, NuGet vous invite à entrer, ce qui permet la suppression des dépendances d’un package, ainsi que le package.</span><span class="sxs-lookup"><span data-stu-id="c2168-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Suppression des packages dépendants](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="c2168-130">`Get-Package` amélioration de la commande</span><span class="sxs-lookup"><span data-stu-id="c2168-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="c2168-131">Le `Get-Package` commande prend désormais en charge un `-ProjectName` paramètre.</span><span class="sxs-lookup"><span data-stu-id="c2168-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="c2168-132">Par conséquent, la commande</span><span class="sxs-lookup"><span data-stu-id="c2168-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="c2168-133">Répertorie tous les packages installés dans le projet A.</span><span class="sxs-lookup"><span data-stu-id="c2168-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="c2168-134">Prise en charge des serveurs proxy qui requièrent une authentification</span><span class="sxs-lookup"><span data-stu-id="c2168-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="c2168-135">Lorsque vous utilisez NuGet derrière un proxy qui requiert une authentification, NuGet vous invite désormais des informations d’identification du proxy.</span><span class="sxs-lookup"><span data-stu-id="c2168-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="c2168-136">Entrer les informations d’identification permet de NuGet pour se connecter au référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="c2168-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="c2168-137">Prise en charge pour les dépôts qui requièrent une authentification</span><span class="sxs-lookup"><span data-stu-id="c2168-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="c2168-138">NuGet prend désormais en charge la connexion à [référentiels privés](../hosting-packages/local-feeds.md) nécessitant une authentification de base ou NTLM.</span><span class="sxs-lookup"><span data-stu-id="c2168-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="c2168-139">Prise en charge pour l’authentification Digest figurera dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c2168-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="c2168-140">Améliorations des performances pour le référentiel nuget.org</span><span class="sxs-lookup"><span data-stu-id="c2168-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="c2168-141">Nous avons apporté plusieurs améliorations de performances dans la galerie nuget.org pour rendre le package de liste et de recherche plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="c2168-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="c2168-142">Filtrage de solution boîte de dialogue projet</span><span class="sxs-lookup"><span data-stu-id="c2168-142">Solution dialog project filtering</span></span>
<span data-ttu-id="c2168-143">Dans le niveau de la Solution boîte de dialogue, lors d’une demande pour les projets installer, nous expliquons seulement les projets qui sont compatibles avec le package sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c2168-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="c2168-144">Notes de publication de package</span><span class="sxs-lookup"><span data-stu-id="c2168-144">Package Release Notes</span></span>
<span data-ttu-id="c2168-145">Les packages NuGet incluent désormais la prise en charge des notes de publication.</span><span class="sxs-lookup"><span data-stu-id="c2168-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="c2168-146">Les notes de publication affiche uniquement les lors de l’affichage _mises à jour_ pour un package, par conséquent, il est inutile pour les ajouter à votre première version.</span><span class="sxs-lookup"><span data-stu-id="c2168-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Notes de publication dans l’onglet mises à jour](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="c2168-148">Pour ajouter des notes de publication à un package, utilisez la nouvelle `<releaseNotes />` élément de métadonnées dans votre fichier NuSpec.</span><span class="sxs-lookup"><span data-stu-id="c2168-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="c2168-149">.NuSpec & ltfiles /&gt; amélioration du produit</span><span class="sxs-lookup"><span data-stu-id="c2168-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="c2168-150">Le `.nuspec` fichier permet désormais vide `<files />` élément, ce qui indique à nuget.exe ne pas à inclure n’importe quel fichier dans le package.</span><span class="sxs-lookup"><span data-stu-id="c2168-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c2168-151">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="c2168-151">Bug Fixes</span></span>
<span data-ttu-id="c2168-152">NuGet 1.5 comportait 107 fixe des éléments de travail.</span><span class="sxs-lookup"><span data-stu-id="c2168-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="c2168-153">103 de ceux ont été marquées comme des bogues.</span><span class="sxs-lookup"><span data-stu-id="c2168-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="c2168-154">Pour obtenir une liste complète de travail éléments résolus dans NuGet 1.5, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="c2168-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="c2168-155">Correctifs de bogues à noter :</span><span class="sxs-lookup"><span data-stu-id="c2168-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="c2168-156">[Problème 1273](http://nuget.codeplex.com/workitem/1273): apportées `packages.config` plus convivial en packages de tri par ordre alphabétique et en supprimant les espaces blancs supplémentaires de contrôle de version.</span><span class="sxs-lookup"><span data-stu-id="c2168-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="c2168-157">[Problème 844](http://nuget.codeplex.com/workitem/844): numéros de Version sont désormais normalisées afin que `Install-Package 1.0` fonctionne sur un package avec la version `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="c2168-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="c2168-158">[Problème 1060](http://nuget.codeplex.com/workitem/1060): lors de la création d’un package à l’aide de nuget.exe, le `-Version` indicateur substitue le `<version />` élément.</span><span class="sxs-lookup"><span data-stu-id="c2168-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
