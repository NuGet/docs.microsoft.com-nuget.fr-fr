---
title: Notes de version 3.1 de NuGet
description: Notes de publication pour 3.1 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="aedac-103">Notes de version 3.1 de NuGet</span><span class="sxs-lookup"><span data-stu-id="aedac-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="aedac-104">[Notes de version de NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Notes de publication](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="aedac-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="aedac-105">NuGet 3.1 a été publié le 27 juillet 2015 comme extension fournie dans le SDK de plateforme Windows universelle pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="aedac-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="aedac-106">Nous avons fourni cette version avec le SDK de plateforme Windows afin que l’expérience de développement Windows pourrait tirer parti du travail inter-plateformes NuGet qui a déjà été démarré.</span><span class="sxs-lookup"><span data-stu-id="aedac-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="aedac-107">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="aedac-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="aedac-108">Nous vous recommandons des développeurs qui ont accès à la mise à jour de la galerie Visual Studio à la version la plus récente est disponible, comme nous publions toujours les mises à jour avec les correctifs de bogues et de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="aedac-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="aedac-109">Extension NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aedac-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="aedac-110">Les problèmes et les fonctionnalités dans cette version sont marquées sur GitHub avec la [« 3.1 RTM UWP transitive prise en charge » jalon](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) au total, nous avons fermé 67 problèmes dans la version 3.1.</span><span class="sxs-lookup"><span data-stu-id="aedac-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="aedac-111">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="aedac-111">New Features</span></span>

* <span data-ttu-id="aedac-112">`project.json` prise en charge pour la prise en charge Windows universelle et ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="aedac-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="aedac-113">Installation du package transitive</span><span class="sxs-lookup"><span data-stu-id="aedac-113">Transitive package installation</span></span>

<span data-ttu-id="aedac-114">Description et la définition de ces fonctionnalités peuvent être trouvées ailleurs dans la documentation.</span><span class="sxs-lookup"><span data-stu-id="aedac-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="aedac-115">Déconseillé</span><span class="sxs-lookup"><span data-stu-id="aedac-115">Deprecated</span></span>

<span data-ttu-id="aedac-116">Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 :</span><span class="sxs-lookup"><span data-stu-id="aedac-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="aedac-117">Packages au niveau de la solution ne peuvent plus être installées</span><span class="sxs-lookup"><span data-stu-id="aedac-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="aedac-118">Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 et les projets qui utilisent la `project.json` spécification</span><span class="sxs-lookup"><span data-stu-id="aedac-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="aedac-119">`install.ps1` et `uninstall.ps1` -ces scripts seront ignorés lors de l’installation du package, la restauration, mettre à jour et désinstaller</span><span class="sxs-lookup"><span data-stu-id="aedac-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="aedac-120">Transformations de configuration seront ignorées.</span><span class="sxs-lookup"><span data-stu-id="aedac-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="aedac-121">Le contenu sera effectué, mais pas copié dans un projet.</span><span class="sxs-lookup"><span data-stu-id="aedac-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="aedac-122">L’équipe travaille pour ré-implémenter cette fonctionnalité, suivez la discussion et au niveau de progression : [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="aedac-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="aedac-123">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="aedac-123">Known Issues</span></span>

<span data-ttu-id="aedac-124">A un nombre de problèmes connus fourni avec cette version.</span><span class="sxs-lookup"><span data-stu-id="aedac-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="aedac-125">Installation de la version 3.1 avec le SDK Windows 10 rétrograde n’importe quelle version de l’extension NuGet qui a déjà été installée</span><span class="sxs-lookup"><span data-stu-id="aedac-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="aedac-126">NuGet de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="aedac-126">NuGet Command-line</span></span>

<span data-ttu-id="aedac-127">L’exécutable de ligne de commande NuGet a été mis à jour et déplacé vers un nouvel emplacement distribuable afin que les versions historiques de nuget.exe peuvent continuer à disposition.</span><span class="sxs-lookup"><span data-stu-id="aedac-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="aedac-128">Vous pouvez télécharger la version 3.1 bêta de nuget.exe pour Windows à : [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="aedac-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="aedac-129">Le nouvel emplacement distribuable réside sur l’hôte dist.nuget.org, avec une structure de dossiers qui suit ce modèle :</span><span class="sxs-lookup"><span data-stu-id="aedac-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="aedac-130">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="aedac-130">New Features</span></span>

* <span data-ttu-id="aedac-131">NuGet.exe peut restaurer et installer des packages dans les projets qui utilisent un `project.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="aedac-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="aedac-132">NuGet.exe peut se connecter à et utiliser le protocole v3 NuGet à : [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="aedac-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="aedac-133">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="aedac-133">Known Issues</span></span> ##

1.    <span data-ttu-id="aedac-134">Impossible d’exécuter le pack par rapport à un `project.json` fichier - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="aedac-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="aedac-135">N’est pas pris en charge sur Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="aedac-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="aedac-136">N’est pas localisée - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="aedac-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="aedac-137">N’est pas signé, tout comme les existantes http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="aedac-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
