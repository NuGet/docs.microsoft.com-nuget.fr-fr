---
title: Notes de publication NuGet 3.1 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour 3.1 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 3.1 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="effda-104">Notes de version 3.1 de NuGet</span><span class="sxs-lookup"><span data-stu-id="effda-104">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="effda-105">[Notes de version de NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Notes de publication](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="effda-105">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="effda-106">NuGet 3.1 a été publié le 27 juillet 2015 comme extension fournie dans le SDK de plateforme Windows universelle pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="effda-106">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="effda-107">Nous avons fourni cette version avec le SDK de plateforme Windows afin que l’expérience de développement Windows pourrait tirer parti du travail inter-plateformes NuGet qui a déjà été démarré.</span><span class="sxs-lookup"><span data-stu-id="effda-107">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="effda-108">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="effda-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="effda-109">Nous vous recommandons des développeurs qui ont accès à la mise à jour de la galerie Visual Studio à la version la plus récente est disponible, comme nous publions toujours les mises à jour avec les correctifs de bogues et de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="effda-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="effda-110">Extension NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="effda-110">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="effda-111">Les problèmes et les fonctionnalités dans cette version sont marquées sur GitHub avec la [« 3.1 RTM UWP transitive prise en charge » jalon](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) au total, nous avons fermé 67 problèmes dans la version 3.1.</span><span class="sxs-lookup"><span data-stu-id="effda-111">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="effda-112">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="effda-112">New Features</span></span>

* <span data-ttu-id="effda-113">`project.json`prise en charge pour la prise en charge Windows universelle et ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="effda-113">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="effda-114">Installation du package transitive</span><span class="sxs-lookup"><span data-stu-id="effda-114">Transitive package installation</span></span>

<span data-ttu-id="effda-115">Description et la définition de ces fonctionnalités peuvent être trouvées ailleurs dans la documentation.</span><span class="sxs-lookup"><span data-stu-id="effda-115">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="effda-116">Déconseillé</span><span class="sxs-lookup"><span data-stu-id="effda-116">Deprecated</span></span>

<span data-ttu-id="effda-117">Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 :</span><span class="sxs-lookup"><span data-stu-id="effda-117">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="effda-118">Packages au niveau de la solution ne peuvent plus être installées</span><span class="sxs-lookup"><span data-stu-id="effda-118">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="effda-119">Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 et les projets qui utilisent la `project.json` spécification</span><span class="sxs-lookup"><span data-stu-id="effda-119">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="effda-120">`install.ps1`et `uninstall.ps1` -ces scripts seront ignorés lors de l’installation du package, la restauration, mettre à jour et désinstaller</span><span class="sxs-lookup"><span data-stu-id="effda-120">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="effda-121">Transformations de configuration seront ignorées.</span><span class="sxs-lookup"><span data-stu-id="effda-121">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="effda-122">Le contenu sera effectué, mais pas copié dans un projet.</span><span class="sxs-lookup"><span data-stu-id="effda-122">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="effda-123">L’équipe travaille pour ré-implémenter cette fonctionnalité, suivez la discussion et au niveau de progression : [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="effda-123">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="effda-124">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="effda-124">Known Issues</span></span>

<span data-ttu-id="effda-125">A un nombre de problèmes connus fourni avec cette version.</span><span class="sxs-lookup"><span data-stu-id="effda-125">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="effda-126">Installation de la version 3.1 avec le SDK Windows 10 rétrograde n’importe quelle version de l’extension NuGet qui a déjà été installée</span><span class="sxs-lookup"><span data-stu-id="effda-126">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="effda-127">NuGet de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="effda-127">NuGet Command-line</span></span>

<span data-ttu-id="effda-128">L’exécutable de ligne de commande NuGet a été mis à jour et déplacé vers un nouvel emplacement distribuable afin que les versions historiques de nuget.exe peuvent continuer à disposition.</span><span class="sxs-lookup"><span data-stu-id="effda-128">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="effda-129">Vous pouvez télécharger la version 3.1 bêta de nuget.exe pour Windows à : [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="effda-129">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="effda-130">Le nouvel emplacement distribuable réside sur l’hôte dist.nuget.org, avec une structure de dossiers qui suit ce modèle :</span><span class="sxs-lookup"><span data-stu-id="effda-130">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="effda-131">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="effda-131">New Features</span></span>

* <span data-ttu-id="effda-132">NuGet.exe peut restaurer et installer des packages dans les projets qui utilisent un `project.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="effda-132">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="effda-133">NuGet.exe peuvent se connecter à et utiliser le protocole de v3 NuGet au : [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="effda-133">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="effda-134">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="effda-134">Known Issues</span></span> ##

1.    <span data-ttu-id="effda-135">Impossible d’exécuter le pack par rapport à un `project.json` fichier - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="effda-135">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="effda-136">N’est pas pris en charge sur Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="effda-136">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="effda-137">N’est pas localisée - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="effda-137">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="effda-138">N’est pas signé, tout comme le http://nuget.org/nuget.exe existant - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="effda-138">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
