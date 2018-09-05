---
title: Notes de publication NuGet 3.1
description: Notes de publication pour 3.1 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545345"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="3aa37-103">Notes de publication NuGet 3.1</span><span class="sxs-lookup"><span data-stu-id="3aa37-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="3aa37-104">[Notes de publication de NuGet 3.0](../release-notes/nuget-3.0.0.md) | [Notes de publication de NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="3aa37-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="3aa37-105">NuGet 3.1 a été publiée le 27 juillet 2015 comme extension groupée dans le SDK de plateforme Windows universelle pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3aa37-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="3aa37-106">Nous avons envoyé cette version avec le SDK de plateforme Windows afin que l’expérience de développement Windows peut tirer parti du travail NuGet multiplateforme qui a déjà été démarré.</span><span class="sxs-lookup"><span data-stu-id="3aa37-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="3aa37-107">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3aa37-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="3aa37-108">Nous recommandons aux développeurs qui ont accès à la mise à jour de la galerie Visual Studio à la version la plus récente est disponible, car nous publions toujours les mises à jour avec les correctifs de bogues et de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3aa37-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="3aa37-109">Extension NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3aa37-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="3aa37-110">Problèmes et les fonctionnalités dans cette version sont marquées sur GitHub avec le [« 3.1 RTM UWP transitive prise en charge » jalon](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) au total, nous avons fermé 67 problèmes dans la version 3.1.</span><span class="sxs-lookup"><span data-stu-id="3aa37-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="3aa37-111">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="3aa37-111">New Features</span></span>

* <span data-ttu-id="3aa37-112">`project.json` prise en charge pour la prise en charge Windows UWP et ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="3aa37-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="3aa37-113">Installation de package transitives</span><span class="sxs-lookup"><span data-stu-id="3aa37-113">Transitive package installation</span></span>

<span data-ttu-id="3aa37-114">Description et la définition de ces fonctionnalités peuvent être trouvées ailleurs dans la documentation.</span><span class="sxs-lookup"><span data-stu-id="3aa37-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="3aa37-115">Déconseillé</span><span class="sxs-lookup"><span data-stu-id="3aa37-115">Deprecated</span></span>

<span data-ttu-id="3aa37-116">Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 :</span><span class="sxs-lookup"><span data-stu-id="3aa37-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="3aa37-117">Packages au niveau de la solution ne peuvent plus être installés</span><span class="sxs-lookup"><span data-stu-id="3aa37-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="3aa37-118">Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 et les projets qui utilisent le `project.json` spécification</span><span class="sxs-lookup"><span data-stu-id="3aa37-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="3aa37-119">`install.ps1` et `uninstall.ps1` -ces scripts seront ignorés pendant l’installation du package, la restauration, mettre à jour et désinstaller</span><span class="sxs-lookup"><span data-stu-id="3aa37-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="3aa37-120">Transformations de configuration va être ignorées</span><span class="sxs-lookup"><span data-stu-id="3aa37-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="3aa37-121">Contenu est exécuté, mais pas copié dans un projet.</span><span class="sxs-lookup"><span data-stu-id="3aa37-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="3aa37-122">L’équipe travaille pour ré-implémenter cette fonctionnalité, suivez la discussion et avancer à : [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="3aa37-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="3aa37-123">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="3aa37-123">Known Issues</span></span>

<span data-ttu-id="3aa37-124">Il existe un nombre de problèmes connus fournies par cette version.</span><span class="sxs-lookup"><span data-stu-id="3aa37-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="3aa37-125">Installation de la version 3.1 avec le SDK Windows 10 rétrograde n’importe quelle version de l’extension NuGet qui a été précédemment installée</span><span class="sxs-lookup"><span data-stu-id="3aa37-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="3aa37-126">NuGet en ligne de commande</span><span class="sxs-lookup"><span data-stu-id="3aa37-126">NuGet Command-line</span></span>

<span data-ttu-id="3aa37-127">L’exécutable de ligne de commande NuGet a été mis à jour et déplacé vers un nouvel emplacement distribuable de sorte que les versions historiques de nuget.exe peuvent continuer à être mis à disposition.</span><span class="sxs-lookup"><span data-stu-id="3aa37-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="3aa37-128">Vous pouvez télécharger la version 3.1 bêta de nuget.exe pour Windows à : [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="3aa37-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="3aa37-129">Le nouvel emplacement distribuable réside sur l’hôte dist.nuget.org, avec une structure de dossiers qui suit ce modèle :</span><span class="sxs-lookup"><span data-stu-id="3aa37-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="3aa37-130">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="3aa37-130">New Features</span></span>

* <span data-ttu-id="3aa37-131">NuGet.exe peut restaurer et installer des packages dans les projets qui utilisent un `project.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="3aa37-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="3aa37-132">NuGet.exe peut se connecter à et utiliser le protocole v3 de NuGet à : [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="3aa37-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="3aa37-133">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="3aa37-133">Known Issues</span></span> ##

1.    <span data-ttu-id="3aa37-134">Impossible d’exécuter pack par rapport à un `project.json` fichier - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="3aa37-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="3aa37-135">N’est pas pris en charge sur Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="3aa37-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="3aa37-136">N’est pas localisé - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="3aa37-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="3aa37-137">N’est pas signé, à l’instar existant http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="3aa37-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
