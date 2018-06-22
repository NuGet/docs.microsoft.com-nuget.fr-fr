---
title: Notes de publication NuGet 2.0
description: Notes de version de NuGet 2.0, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820795"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="b866b-103">Notes de publication NuGet 2.0</span><span class="sxs-lookup"><span data-stu-id="b866b-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="b866b-104">[Notes de publication NuGet 1.8](../release-notes/nuget-1.8.md) | [Notes de version 2.1 de NuGet](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="b866b-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="b866b-105">NuGet 2.0 a été publiée le 19 juin 2012.</span><span class="sxs-lookup"><span data-stu-id="b866b-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="b866b-106">Problème connu d’Installation</span><span class="sxs-lookup"><span data-stu-id="b866b-106">Known Installation Issue</span></span>
<span data-ttu-id="b866b-107">Si vous exécutez Visual Studio 2010 SP1, vous susceptible de rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet, si vous disposez d’une version plus ancienne est installée.</span><span class="sxs-lookup"><span data-stu-id="b866b-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="b866b-108">La solution de contournement consiste à simplement désinstaller NuGet et l’installer à partir de la galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b866b-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="b866b-109">Consultez [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) pour plus d’informations, ou [atteindre directement le correctif logiciel Visual Studio](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="b866b-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="b866b-110">Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis il est probable que devez redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="b866b-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="b866b-111">Autorisation de restauration de package est désormais active</span><span class="sxs-lookup"><span data-stu-id="b866b-111">Package restore consent is now active</span></span>

<span data-ttu-id="b866b-112">Comme décrit dans cette [publier sur le consentement de restauration de package](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0, vous devez désormais consentement donné pour permettre la restauration de package pour vous connecter et télécharger les packages.</span><span class="sxs-lookup"><span data-stu-id="b866b-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="b866b-113">Veuillez vous assurer que vous avez fourni le consentement via la boîte de dialogue package manager configuration ou de la variable d’environnement EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="b866b-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="b866b-114">Dépendances de groupe par l’infrastructure cible</span><span class="sxs-lookup"><span data-stu-id="b866b-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="b866b-115">Depuis la version 2.0, package de dépendances peuvent varier en fonction du profil de framework du projet cible.</span><span class="sxs-lookup"><span data-stu-id="b866b-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="b866b-116">Pour cela, à l’aide d’une mise à jour `.nuspec` schéma.</span><span class="sxs-lookup"><span data-stu-id="b866b-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="b866b-117">Le `<dependencies>` élément peut désormais contenir un ensemble de `<group>` éléments.</span><span class="sxs-lookup"><span data-stu-id="b866b-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="b866b-118">Chaque groupe contient zéro ou plusieurs `<dependency>` éléments et un `targetFramework` attribut.</span><span class="sxs-lookup"><span data-stu-id="b866b-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="b866b-119">Toutes les dépendances à l’intérieur d’un groupe sont installées ensemble si le framework cible est compatible avec le profil de framework du projet cible.</span><span class="sxs-lookup"><span data-stu-id="b866b-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="b866b-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b866b-120">For example:</span></span>

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

<span data-ttu-id="b866b-121">Notez qu’un groupe peut contenir **zéro** dépendances.</span><span class="sxs-lookup"><span data-stu-id="b866b-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="b866b-122">Dans l’exemple ci-dessus, si le package est installé dans un projet qui cible Silverlight 3.0 ou version ultérieure, aucune dépendance ne sera installé.</span><span class="sxs-lookup"><span data-stu-id="b866b-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="b866b-123">Si le package est installé dans un projet qui cible le .NET 4.0 ou version ultérieure, deux dépendances, jQuery et WebActivator, seront installés.</span><span class="sxs-lookup"><span data-stu-id="b866b-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="b866b-124">Si le package est installé dans un projet qui cible une version antérieure de ces 2 infrastructures ou toute autre infrastructure, RouteMagic 1.1.0 sera installé.</span><span class="sxs-lookup"><span data-stu-id="b866b-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="b866b-125">Il n’existe aucun héritage entre les groupes.</span><span class="sxs-lookup"><span data-stu-id="b866b-125">There is no inheritance between groups.</span></span> <span data-ttu-id="b866b-126">Si le framework cible d’un projet correspond à la `targetFramework` attribut d’un groupe, seuls les dépendances au sein de ce groupe sera installé.</span><span class="sxs-lookup"><span data-stu-id="b866b-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="b866b-127">Un package peut spécifier les dépendances de package dans deux formats : l’ancien format de liste plate de `<dependency>` éléments ou les groupes.</span><span class="sxs-lookup"><span data-stu-id="b866b-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="b866b-128">Si le `<group>` format est utilisé, le package ne peut pas être installé dans les versions antérieures à 2.0 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="b866b-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="b866b-129">Notez que la combinaison des deux formats n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="b866b-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="b866b-130">Par exemple, l’extrait suivant est **non valide** et sont rejetées par NuGet.</span><span class="sxs-lookup"><span data-stu-id="b866b-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="b866b-131">Regroupement des fichiers de contenu et des scripts PowerShell par le framework cible</span><span class="sxs-lookup"><span data-stu-id="b866b-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="b866b-132">En plus des références d’assembly, les fichiers de contenu et des scripts PowerShell peuvent également être regroupés par le framework cible.</span><span class="sxs-lookup"><span data-stu-id="b866b-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="b866b-133">La même structure de dossier se trouve dans le `lib` dossier pour la spécification du framework cible peut désormais être appliqué dans la même façon à la `content` et `tools` dossiers.</span><span class="sxs-lookup"><span data-stu-id="b866b-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="b866b-134">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b866b-134">For example:</span></span>

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

<span data-ttu-id="b866b-135">**Remarque**: car `init.ps1` est exécutée au niveau de la solution et est dépendant sur n’importe quel projet individuel, il doit être placé directement sous le `tools` dossier.</span><span class="sxs-lookup"><span data-stu-id="b866b-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="b866b-136">Si placé dans un dossier spécifique de l’infrastructure, il sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="b866b-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="b866b-137">En outre, une nouvelle fonctionnalité de NuGet 2.0 est que le dossier d’une infrastructure peut être *vide*, dans ce cas, NuGet n’ajoute pas les références d’assembly, ajoutez les fichiers de contenu ou exécuter des scripts PowerShell pour la version du framework particulier.</span><span class="sxs-lookup"><span data-stu-id="b866b-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="b866b-138">Dans l’exemple ci-dessus, le dossier `content\net40` est vide.</span><span class="sxs-lookup"><span data-stu-id="b866b-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="b866b-139">Performances de saisie semi-automatique tab améliorée</span><span class="sxs-lookup"><span data-stu-id="b866b-139">Improved tab completion performance</span></span>
<span data-ttu-id="b866b-140">La fonctionnalité de saisie semi-automatique d’onglet dans la Console du Gestionnaire de Package NuGet a été mis à jour pour améliorer considérablement les performances.</span><span class="sxs-lookup"><span data-stu-id="b866b-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="b866b-141">Il y a beaucoup moins retard de l’heure de que la touche tab est enfoncée jusqu'à ce que la liste déroulante de suggestions s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b866b-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b866b-142">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="b866b-142">Bug Fixes</span></span>
<span data-ttu-id="b866b-143">NuGet 2.0 comprend plusieurs correctifs de bogues en mettant l’accent sur les performances et de consentement de restauration de package.</span><span class="sxs-lookup"><span data-stu-id="b866b-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="b866b-144">Pour obtenir la liste complète de travail éléments fixes dans NuGet 2.0, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b866b-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
