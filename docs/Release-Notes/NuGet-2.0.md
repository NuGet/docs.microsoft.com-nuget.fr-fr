---
title: Notes de publication NuGet 2.0 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de version de NuGet 2.0, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 2.0, les correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eaa3c8db1cce72ff93671a1df63698748cdfab70
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="cc295-104">Notes de publication NuGet 2.0</span><span class="sxs-lookup"><span data-stu-id="cc295-104">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="cc295-105">[Notes de publication NuGet 1.8](../release-notes/nuget-1.8.md) | [Notes de version 2.1 de NuGet](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="cc295-105">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="cc295-106">NuGet 2.0 a été publiée le 19 juin 2012.</span><span class="sxs-lookup"><span data-stu-id="cc295-106">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="cc295-107">Problème connu d’Installation</span><span class="sxs-lookup"><span data-stu-id="cc295-107">Known Installation Issue</span></span>
<span data-ttu-id="cc295-108">Si vous exécutez Visual Studio 2010 SP1, vous susceptible de rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet, si vous disposez d’une version plus ancienne est installée.</span><span class="sxs-lookup"><span data-stu-id="cc295-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="cc295-109">La solution de contournement consiste à simplement désinstaller NuGet et l’installer à partir de la galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc295-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="cc295-110">Consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) pour plus d’informations, ou [atteindre directement le correctif logiciel Visual Studio](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="cc295-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="cc295-111">Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis il est probable que devez redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="cc295-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="cc295-112">Autorisation de restauration de package est désormais active</span><span class="sxs-lookup"><span data-stu-id="cc295-112">Package restore consent is now active</span></span>

<span data-ttu-id="cc295-113">Comme décrit dans cette [publier sur le consentement de restauration de package](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0, vous devez désormais consentement donné pour permettre la restauration de package pour vous connecter et télécharger les packages.</span><span class="sxs-lookup"><span data-stu-id="cc295-113">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="cc295-114">Veuillez vous assurer que vous avez fourni le consentement via la boîte de dialogue package manager configuration ou de la variable d’environnement EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="cc295-114">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="cc295-115">Dépendances de groupe par l’infrastructure cible</span><span class="sxs-lookup"><span data-stu-id="cc295-115">Group dependencies by target frameworks</span></span>

<span data-ttu-id="cc295-116">Depuis la version 2.0, package de dépendances peuvent varier en fonction du profil de framework du projet cible.</span><span class="sxs-lookup"><span data-stu-id="cc295-116">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="cc295-117">Pour cela, à l’aide d’une mise à jour `.nuspec` schéma.</span><span class="sxs-lookup"><span data-stu-id="cc295-117">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="cc295-118">Le `<dependencies>` élément peut désormais contenir un ensemble de `<group>` éléments.</span><span class="sxs-lookup"><span data-stu-id="cc295-118">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="cc295-119">Chaque groupe contient zéro ou plusieurs `<dependency>` éléments et un `targetFramework` attribut.</span><span class="sxs-lookup"><span data-stu-id="cc295-119">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="cc295-120">Toutes les dépendances à l’intérieur d’un groupe sont installées ensemble si le framework cible est compatible avec le profil de framework du projet cible.</span><span class="sxs-lookup"><span data-stu-id="cc295-120">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="cc295-121">Exemple :</span><span class="sxs-lookup"><span data-stu-id="cc295-121">For example:</span></span>

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

<span data-ttu-id="cc295-122">Notez qu’un groupe peut contenir **zéro** dépendances.</span><span class="sxs-lookup"><span data-stu-id="cc295-122">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="cc295-123">Dans l’exemple ci-dessus, si le package est installé dans un projet qui cible Silverlight 3.0 ou version ultérieure, aucune dépendance ne sera installé.</span><span class="sxs-lookup"><span data-stu-id="cc295-123">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="cc295-124">Si le package est installé dans un projet qui cible le .NET 4.0 ou version ultérieure, deux dépendances, jQuery et WebActivator, seront installés.</span><span class="sxs-lookup"><span data-stu-id="cc295-124">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="cc295-125">Si le package est installé dans un projet qui cible une version antérieure de ces 2 infrastructures ou toute autre infrastructure, RouteMagic 1.1.0 sera installé.</span><span class="sxs-lookup"><span data-stu-id="cc295-125">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="cc295-126">Il n’existe aucun héritage entre les groupes.</span><span class="sxs-lookup"><span data-stu-id="cc295-126">There is no inheritance between groups.</span></span> <span data-ttu-id="cc295-127">Si le framework cible d’un projet correspond à la `targetFramework` attribut d’un groupe, seuls les dépendances au sein de ce groupe sera installé.</span><span class="sxs-lookup"><span data-stu-id="cc295-127">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="cc295-128">Un package peut spécifier les dépendances de package dans deux formats : l’ancien format de liste plate de `<dependency>` éléments ou les groupes.</span><span class="sxs-lookup"><span data-stu-id="cc295-128">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="cc295-129">Si le `<group>` format est utilisé, le package ne peut pas être installé dans les versions antérieures à 2.0 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc295-129">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="cc295-130">Notez que la combinaison des deux formats n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="cc295-130">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="cc295-131">Par exemple, l’extrait suivant est **non valide** et sont rejetées par NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc295-131">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="cc295-132">Regroupement des fichiers de contenu et des scripts PowerShell par le framework cible</span><span class="sxs-lookup"><span data-stu-id="cc295-132">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="cc295-133">En plus des références d’assembly, les fichiers de contenu et des scripts PowerShell peuvent également être regroupés par le framework cible.</span><span class="sxs-lookup"><span data-stu-id="cc295-133">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="cc295-134">La même structure de dossier se trouve dans le `lib` dossier pour la spécification du framework cible peut désormais être appliqué dans la même façon à la `content` et `tools` dossiers.</span><span class="sxs-lookup"><span data-stu-id="cc295-134">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="cc295-135">Exemple :</span><span class="sxs-lookup"><span data-stu-id="cc295-135">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="cc295-136">**Remarque**: car `init.ps1` est exécutée au niveau de la solution et est dépendant sur n’importe quel projet individuel, il doit être placé directement sous le `tools` dossier.</span><span class="sxs-lookup"><span data-stu-id="cc295-136">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="cc295-137">Si placé dans un dossier spécifique de l’infrastructure, il sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="cc295-137">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="cc295-138">En outre, une nouvelle fonctionnalité de NuGet 2.0 est que le dossier d’une infrastructure peut être *vide*, dans ce cas, NuGet n’ajoute pas les références d’assembly, ajoutez les fichiers de contenu ou exécuter des scripts PowerShell pour la version du framework particulier.</span><span class="sxs-lookup"><span data-stu-id="cc295-138">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="cc295-139">Dans l’exemple ci-dessus, le dossier `content\net40` est vide.</span><span class="sxs-lookup"><span data-stu-id="cc295-139">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="cc295-140">Performances de saisie semi-automatique tab améliorée</span><span class="sxs-lookup"><span data-stu-id="cc295-140">Improved tab completion performance</span></span>
<span data-ttu-id="cc295-141">La fonctionnalité de saisie semi-automatique d’onglet dans la Console du Gestionnaire de Package NuGet a été mis à jour pour améliorer considérablement les performances.</span><span class="sxs-lookup"><span data-stu-id="cc295-141">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="cc295-142">Il y a beaucoup moins retard de l’heure de que la touche tab est enfoncée jusqu'à ce que la liste déroulante de suggestions s’affiche.</span><span class="sxs-lookup"><span data-stu-id="cc295-142">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="cc295-143">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="cc295-143">Bug Fixes</span></span>
<span data-ttu-id="cc295-144">NuGet 2.0 comprend plusieurs correctifs de bogues en mettant l’accent sur les performances et de consentement de restauration de package.</span><span class="sxs-lookup"><span data-stu-id="cc295-144">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="cc295-145">Pour obtenir la liste complète de travail éléments fixes dans NuGet 2.0, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="cc295-145">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
