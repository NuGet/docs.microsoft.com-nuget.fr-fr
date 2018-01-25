---
title: Notes de publication NuGet 1.5 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour la version 1.5 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 1.5 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 261cfbbd262bad28f142b0c3dff8a541641d9fda
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="4033b-104">Notes de version 1.5 de NuGet</span><span class="sxs-lookup"><span data-stu-id="4033b-104">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="4033b-105">[Notes de publication NuGet 1.4](../release-notes/nuget-1.4.md) | [NuGet 1.6 Notes de publication](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="4033b-105">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="4033b-106">NuGet 1.5 a été publiée le 30 août 2011.</span><span class="sxs-lookup"><span data-stu-id="4033b-106">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="4033b-107">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="4033b-107">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="4033b-108">Modèles de projet avec les Packages NuGet préinstallés</span><span class="sxs-lookup"><span data-stu-id="4033b-108">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="4033b-109">Lorsque vous créez un nouveau modèle de projet ASP.NET MVC 3, les bibliothèques de scripts jQuery inclus dans le projet réellement y sont placés en installant les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="4033b-109">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="4033b-110">Le modèle de projet ASP.NET MVC 3 inclut un ensemble de packages NuGet installés lorsque le modèle de projet est appelé.</span><span class="sxs-lookup"><span data-stu-id="4033b-110">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="4033b-111">Cette possibilité d’inclure les packages NuGet avec un modèle de projet est maintenant une fonctionnalité de NuGet qui _tout_ modèle de projet peut désormais tirer parti de.</span><span class="sxs-lookup"><span data-stu-id="4033b-111">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="4033b-112">Pour plus d’informations sur cette fonctionnalité, lire ce [billet de blog par le développeur de la fonctionnalité](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="4033b-112">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="4033b-113">Références d’Assembly explicite</span><span class="sxs-lookup"><span data-stu-id="4033b-113">Explicit Assembly References</span></span>

<span data-ttu-id="4033b-114">Ajouté un nouveau `<references />` élément utilisé pour spécifier explicitement les assemblys dans le package doit être référencé.</span><span class="sxs-lookup"><span data-stu-id="4033b-114">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="4033b-115">Par exemple, si vous ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="4033b-115">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="4033b-116">Alors seulement le `xunit.dll` et `xunit.extensions.dll` sera référencé à partir de la commande appropriée [sous-dossier de profil du framework/](../schema/nuspec.md#explicit-assembly-references) de la `lib` dossier même si d’autres assemblys dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="4033b-116">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../schema/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="4033b-117">Si cet élément est omis, le comportement habituel s’applique, qui consiste à faire référence à chaque assembly dans le `lib` dossier.</span><span class="sxs-lookup"><span data-stu-id="4033b-117">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="4033b-118">__Quelle est l’utilité de cette fonctionnalité ?__</span><span class="sxs-lookup"><span data-stu-id="4033b-118">__What is this feature used for?__</span></span>

<span data-ttu-id="4033b-119">Cette fonctionnalité prend en charge les seuls les assemblys au moment du design.</span><span class="sxs-lookup"><span data-stu-id="4033b-119">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="4033b-120">Par exemple, lors de l’utilisation de contrats de Code, les assemblys de contrat doivent être en regard des assemblys de runtime qui ils augmentent afin que Visual Studio peut trouver les, mais les assemblys de contrat ne doivent pas réellement référencés par le projet et ne doivent pas être copiés dans le `bin` dossier.</span><span class="sxs-lookup"><span data-stu-id="4033b-120">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="4033b-121">De même, la fonctionnalité peut être utilisée pour les infrastructures de tests unitaires telles que XUnit nécessitant ses assemblys d’outils située en regard des assemblys par le runtime, mais exclus des références de projet.</span><span class="sxs-lookup"><span data-stu-id="4033b-121">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="4033b-122">Possibilité d’exclure les fichiers dans le .nuspec</span><span class="sxs-lookup"><span data-stu-id="4033b-122">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="4033b-123">Le `<file>` élément au sein d’un `.nuspec` fichier peut être utilisé pour inclure un fichier spécifique ou un ensemble de fichiers à l’aide d’un caractère générique.</span><span class="sxs-lookup"><span data-stu-id="4033b-123">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="4033b-124">Lorsque vous utilisez un caractère générique, il n’existe aucun moyen pour exclure un sous-ensemble spécifique de fichiers inclus.</span><span class="sxs-lookup"><span data-stu-id="4033b-124">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="4033b-125">Par exemple, supposons que vous souhaitez que tous les fichiers texte dans un dossier à l’exception d’une valeur spécifique.</span><span class="sxs-lookup"><span data-stu-id="4033b-125">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="4033b-126">Utilisez des points-virgules pour spécifier plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="4033b-126">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="4033b-127">Ou utilisez un caractère générique à un ensemble de fichiers tels que tous les fichiers de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="4033b-127">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="4033b-128">Suppression de packages à l’aide de la boîte de dialogue vous invite à entrer pour supprimer les dépendances</span><span class="sxs-lookup"><span data-stu-id="4033b-128">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="4033b-129">Lorsque vous désinstallez un package avec des dépendances, NuGet vous invite à entrer, ce qui permet la suppression des dépendances d’un package, ainsi que le package.</span><span class="sxs-lookup"><span data-stu-id="4033b-129">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Suppression des packages dépendants](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="4033b-131">`Get-Package`amélioration de la commande</span><span class="sxs-lookup"><span data-stu-id="4033b-131">`Get-Package` command improvement</span></span>
<span data-ttu-id="4033b-132">Le `Get-Package` commande prend désormais en charge un `-ProjectName` paramètre.</span><span class="sxs-lookup"><span data-stu-id="4033b-132">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="4033b-133">Par conséquent, la commande</span><span class="sxs-lookup"><span data-stu-id="4033b-133">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="4033b-134">Répertorie tous les packages installés dans le projet A.</span><span class="sxs-lookup"><span data-stu-id="4033b-134">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="4033b-135">Prise en charge des serveurs proxy qui requièrent une authentification</span><span class="sxs-lookup"><span data-stu-id="4033b-135">Support for Proxies that require authentication</span></span>
<span data-ttu-id="4033b-136">Lorsque vous utilisez NuGet derrière un proxy qui nécessite une authentification, NuGet présent à entrer des informations d’identification du proxy.</span><span class="sxs-lookup"><span data-stu-id="4033b-136">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="4033b-137">Entrer les informations d’identification permet de NuGet pour se connecter au référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="4033b-137">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="4033b-138">Prise en charge pour les référentiels qui requièrent une authentification</span><span class="sxs-lookup"><span data-stu-id="4033b-138">Support for Repositories that require authentication</span></span>
<span data-ttu-id="4033b-139">NuGet prend désormais en charge la connexion à [de dépôts privés](../hosting-packages/local-feeds.md) nécessitant une authentification de base ou NTLM.</span><span class="sxs-lookup"><span data-stu-id="4033b-139">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="4033b-140">Prise en charge pour l’authentification Digest sera ajoutée dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4033b-140">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="4033b-141">Améliorations des performances pour le référentiel nuget.org</span><span class="sxs-lookup"><span data-stu-id="4033b-141">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="4033b-142">Nous avons apporté plusieurs améliorations de performances dans la galerie nuget.org pour rendre le package répertorier et de recherche.</span><span class="sxs-lookup"><span data-stu-id="4033b-142">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="4033b-143">Filtrage du projet solution boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="4033b-143">Solution dialog project filtering</span></span>
<span data-ttu-id="4033b-144">Dans le dialogue au niveau Solution, lors de la demande pour les projets installer, nous afficher uniquement les projets qui sont compatibles avec le package sélectionné.</span><span class="sxs-lookup"><span data-stu-id="4033b-144">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="4033b-145">Notes de version de package</span><span class="sxs-lookup"><span data-stu-id="4033b-145">Package Release Notes</span></span>
<span data-ttu-id="4033b-146">Les packages NuGet incluent désormais la prise en charge pour les notes de publication.</span><span class="sxs-lookup"><span data-stu-id="4033b-146">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="4033b-147">Ces notes de publication affiche uniquement les lors de l’affichage _mises à jour_ pour un package, par conséquent, il n’a aucune signification pour les ajouter à votre première version.</span><span class="sxs-lookup"><span data-stu-id="4033b-147">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Notes de publication dans l’onglet mises à jour](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="4033b-149">Pour ajouter des notes de publication à un package, utilisez la nouvelle `<releaseNotes />` élément de métadonnées dans votre fichier NuSpec.</span><span class="sxs-lookup"><span data-stu-id="4033b-149">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="4033b-150">.NuSpec & ltfiles /&gt; amélioration</span><span class="sxs-lookup"><span data-stu-id="4033b-150">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="4033b-151">Le `.nuspec` fichier permet désormais vide `<files />` élément, ce qui indique à nuget.exe ne pas à inclure n’importe quel fichier dans le package.</span><span class="sxs-lookup"><span data-stu-id="4033b-151">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4033b-152">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="4033b-152">Bug Fixes</span></span>
<span data-ttu-id="4033b-153">NuGet 1.5 comportait 107 fixe des éléments de travail.</span><span class="sxs-lookup"><span data-stu-id="4033b-153">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="4033b-154">103 d'entre eux ont été marquées en tant que bogues.</span><span class="sxs-lookup"><span data-stu-id="4033b-154">103 of those were marked as bugs.</span></span>

<span data-ttu-id="4033b-155">Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.5, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="4033b-155">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="4033b-156">Correctifs de bogues à noter :</span><span class="sxs-lookup"><span data-stu-id="4033b-156">Bug fixes worth noting:</span></span>

* <span data-ttu-id="4033b-157">[Problème 1273](http://nuget.codeplex.com/workitem/1273): apportées `packages.config` plus contrôle de version convivial en packages de tri par ordre alphabétique et en supprimant les espaces blancs supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4033b-157">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="4033b-158">[Problème 844](http://nuget.codeplex.com/workitem/844): les numéros de Version sont désormais normalisées afin que `Install-Package 1.0` fonctionne sur un package avec la version `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="4033b-158">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="4033b-159">[Problème 1060](http://nuget.codeplex.com/workitem/1060): lors de la création d’un package à l’aide de nuget.exe, le `-Version` indicateur substitue le `<version />` élément.</span><span class="sxs-lookup"><span data-stu-id="4033b-159">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
