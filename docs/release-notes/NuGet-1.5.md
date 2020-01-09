---
title: Notes de publication de NuGet 1,5
description: Notes de publication de NuGet 1,5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383347"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="848cb-103">Notes de publication de NuGet 1,5</span><span class="sxs-lookup"><span data-stu-id="848cb-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="848cb-104">[Notes de publication de nuget 1,4](../release-notes/nuget-1.4.md) | [notes de publication de NuGet 1,6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="848cb-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="848cb-105">NuGet 1,5 a été publié le 30 août 2011.</span><span class="sxs-lookup"><span data-stu-id="848cb-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="848cb-106">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="848cb-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="848cb-107">Modèles de projet avec des packages NuGet préinstallés</span><span class="sxs-lookup"><span data-stu-id="848cb-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="848cb-108">Lors de la création d’un nouveau modèle de projet ASP.NET MVC 3, les bibliothèques de scripts jQuery incluses dans le projet y sont placées en installant les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="848cb-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="848cb-109">Le modèle de projet ASP.NET MVC 3 comprend un ensemble de packages NuGet qui sont installés lorsque le modèle de projet est appelé.</span><span class="sxs-lookup"><span data-stu-id="848cb-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="848cb-110">Cette possibilité d’inclure des packages NuGet avec un modèle de projet est maintenant une fonctionnalité de NuGet que _n’importe quel_ modèle de projet peut désormais tirer parti de.</span><span class="sxs-lookup"><span data-stu-id="848cb-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="848cb-111">Pour plus d’informations sur cette fonctionnalité, lisez ce billet [de blog par le développeur de la fonctionnalité](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="848cb-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="848cb-112">Références d’assembly explicites</span><span class="sxs-lookup"><span data-stu-id="848cb-112">Explicit Assembly References</span></span>

<span data-ttu-id="848cb-113">Ajout d’un nouvel élément `<references />` utilisé pour spécifier explicitement les assemblys dans le package à référencer.</span><span class="sxs-lookup"><span data-stu-id="848cb-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="848cb-114">Par exemple, si vous ajoutez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="848cb-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="848cb-115">Ensuite, seuls les `xunit.dll` et `xunit.extensions.dll` seront référencés à partir du sous [-dossier Framework/profil](../reference/nuspec.md#explicit-assembly-references) approprié du dossier `lib`, même s’il existe d’autres assemblys dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="848cb-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="848cb-116">Si cet élément est omis, le comportement habituel s’applique, qui consiste à référencer chaque assembly dans le dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="848cb-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="848cb-117">__À quoi sert cette fonctionnalité ?__</span><span class="sxs-lookup"><span data-stu-id="848cb-117">__What is this feature used for?__</span></span>

<span data-ttu-id="848cb-118">Cette fonctionnalité prend en charge uniquement les assemblys au moment de la conception.</span><span class="sxs-lookup"><span data-stu-id="848cb-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="848cb-119">Par exemple, lors de l’utilisation de contrats de code, les assemblys de contrat doivent être en regard des assemblys de Runtime qu’ils augmentent afin que Visual Studio puisse les trouver, mais les assemblys de contrat ne doivent pas être référencés par le projet et ne doivent pas être copiés dans le dossier `bin`.</span><span class="sxs-lookup"><span data-stu-id="848cb-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="848cb-120">De même, la fonctionnalité peut être utilisée pour les infrastructures de tests unitaires telles que XUnit qui nécessitent que ses assemblys d’outils soient situés à côté des assemblys de Runtime, mais exclus des références de projet.</span><span class="sxs-lookup"><span data-stu-id="848cb-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="848cb-121">Ajout de la possibilité d’exclure des fichiers dans le fichier. NuSpec</span><span class="sxs-lookup"><span data-stu-id="848cb-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="848cb-122">L’élément `<file>` dans un fichier `.nuspec` peut être utilisé pour inclure un fichier spécifique ou un ensemble de fichiers à l’aide d’un caractère générique.</span><span class="sxs-lookup"><span data-stu-id="848cb-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="848cb-123">Lorsque vous utilisez un caractère générique, il n’existe aucun moyen d’exclure un sous-ensemble spécifique des fichiers inclus.</span><span class="sxs-lookup"><span data-stu-id="848cb-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="848cb-124">Supposons, par exemple, que vous souhaitiez tous les fichiers texte d’un dossier, à l’exception d’un dossier spécifique.</span><span class="sxs-lookup"><span data-stu-id="848cb-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="848cb-125">Utilisez des points-virgules pour spécifier plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="848cb-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="848cb-126">Ou utiliser un caractère générique pour exclure un ensemble de fichiers tels que tous les fichiers de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="848cb-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="848cb-127">Suppression de packages à l’aide de la boîte de dialogue invite à supprimer les dépendances</span><span class="sxs-lookup"><span data-stu-id="848cb-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="848cb-128">Lors de la désinstallation d’un package avec des dépendances, NuGet vous invite à supprimer les dépendances d’un package ainsi que le package.</span><span class="sxs-lookup"><span data-stu-id="848cb-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Suppression de packages dépendants](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="848cb-130">amélioration de la commande `Get-Package`</span><span class="sxs-lookup"><span data-stu-id="848cb-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="848cb-131">La commande `Get-Package` prend maintenant en charge un paramètre `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="848cb-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="848cb-132">La commande</span><span class="sxs-lookup"><span data-stu-id="848cb-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="848cb-133">répertorie tous les packages installés dans le projet A.</span><span class="sxs-lookup"><span data-stu-id="848cb-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="848cb-134">Prise en charge des proxies qui requièrent une authentification</span><span class="sxs-lookup"><span data-stu-id="848cb-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="848cb-135">Lorsque vous utilisez NuGet derrière un proxy qui requiert une authentification, NuGet demande des informations d’identification de proxy.</span><span class="sxs-lookup"><span data-stu-id="848cb-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="848cb-136">La saisie des informations d’identification permet à NuGet de se connecter au référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="848cb-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="848cb-137">Prise en charge des dépôts qui requièrent une authentification</span><span class="sxs-lookup"><span data-stu-id="848cb-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="848cb-138">NuGet prend désormais en charge la connexion à des [dépôts privés](../hosting-packages/local-feeds.md) qui requièrent une authentification de base ou NTLM.</span><span class="sxs-lookup"><span data-stu-id="848cb-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="848cb-139">La prise en charge de l’authentification Digest sera ajoutée dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="848cb-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="848cb-140">Améliorations des performances du référentiel nuget.org</span><span class="sxs-lookup"><span data-stu-id="848cb-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="848cb-141">Nous avons apporté plusieurs améliorations de performances à la Galerie de nuget.org pour rendre la liste des packages et accélérer la recherche.</span><span class="sxs-lookup"><span data-stu-id="848cb-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="848cb-142">Filtrage de projet de la boîte de dialogue de solution</span><span class="sxs-lookup"><span data-stu-id="848cb-142">Solution dialog project filtering</span></span>
<span data-ttu-id="848cb-143">Dans la boîte de dialogue de niveau solution, lorsque vous êtes invité à entrer les projets à installer, nous affichons uniquement les projets qui sont compatibles avec le package sélectionné.</span><span class="sxs-lookup"><span data-stu-id="848cb-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="848cb-144">Notes de publication du package</span><span class="sxs-lookup"><span data-stu-id="848cb-144">Package Release Notes</span></span>
<span data-ttu-id="848cb-145">Les packages NuGet incluent désormais la prise en charge des notes de publication.</span><span class="sxs-lookup"><span data-stu-id="848cb-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="848cb-146">Les notes de publication s’affichent uniquement lors de l’affichage des _mises à jour_ d’un package. il est donc inutile de les ajouter à votre première version.</span><span class="sxs-lookup"><span data-stu-id="848cb-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Notes de publication dans l’onglet mises à jour](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="848cb-148">Pour ajouter des notes de publication à un package, utilisez le nouvel élément de métadonnées `<releaseNotes />` dans votre fichier NuSpec.</span><span class="sxs-lookup"><span data-stu-id="848cb-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="848cb-149">amélioration de l’NuSpec & ltfiles/&gt;</span><span class="sxs-lookup"><span data-stu-id="848cb-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="848cb-150">Le fichier `.nuspec` autorise désormais un élément `<files />` vide, ce qui indique à NuGet. exe de ne pas inclure de fichier dans le package.</span><span class="sxs-lookup"><span data-stu-id="848cb-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="848cb-151">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="848cb-151">Bug Fixes</span></span>
<span data-ttu-id="848cb-152">NuGet 1,5 avait un total de 107 éléments de travail corrigés.</span><span class="sxs-lookup"><span data-stu-id="848cb-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="848cb-153">103 de ceux-ci ont été marqués comme des bogues.</span><span class="sxs-lookup"><span data-stu-id="848cb-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="848cb-154">Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 1,5, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="848cb-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="848cb-155">Les correctifs de bogues méritent d’être notés :</span><span class="sxs-lookup"><span data-stu-id="848cb-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="848cb-156">[Problème 1273](http://nuget.codeplex.com/workitem/1273): `packages.config` un plus grand contrôle de version en triant les packages par ordre alphabétique et en supprimant les espaces superflus.</span><span class="sxs-lookup"><span data-stu-id="848cb-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="848cb-157">[Problème 844](http://nuget.codeplex.com/workitem/844): les numéros de version sont désormais normalisés afin que `Install-Package 1.0` fonctionne sur un package avec la version `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="848cb-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="848cb-158">[Problème 1060](http://nuget.codeplex.com/workitem/1060): lors de la création d’un package à l’aide de NuGet. exe, l’indicateur `-Version` remplace l’élément `<version />`.</span><span class="sxs-lookup"><span data-stu-id="848cb-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
