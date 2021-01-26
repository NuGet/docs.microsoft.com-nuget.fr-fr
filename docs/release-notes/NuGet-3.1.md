---
title: Notes de publication de NuGet 3,1
description: Notes de publication de NuGet 3,1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776529"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="90687-103">Notes de publication de NuGet 3,1</span><span class="sxs-lookup"><span data-stu-id="90687-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="90687-104">Notes de publication de [NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Notes de publication de NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="90687-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="90687-105">NuGet 3,1 a été publié le 27 juillet 2015 en tant qu’extension groupée du kit de développement logiciel (SDK) plateforme Windows universelle pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="90687-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="90687-106">Nous avons fourni cette version avec le kit de développement logiciel (SDK) de la plate-forme Windows afin que l’expérience de développement Windows puisse tirer parti du travail multiplateforme NuGet précédemment démarré.</span><span class="sxs-lookup"><span data-stu-id="90687-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="90687-107">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="90687-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="90687-108">Nous recommandons aux développeurs qui ont accès à la mise à jour de la Galerie Visual Studio d’accéder à la dernière version disponible, car nous publions toujours des mises à jour avec des correctifs de bogues et de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="90687-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="90687-109">Extension NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90687-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="90687-110">Les problèmes et les fonctionnalités de cette version sont marqués sur GitHub avec le [jalon « 3,1 RTM UWP transitive support »](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  au total, nous avons clos 67 problèmes dans la version 3,1.</span><span class="sxs-lookup"><span data-stu-id="90687-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="90687-111">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="90687-111">New Features</span></span>

* <span data-ttu-id="90687-112">`project.json` prise en charge de la prise en charge de Windows UWP et ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="90687-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="90687-113">Installation du package transitif</span><span class="sxs-lookup"><span data-stu-id="90687-113">Transitive package installation</span></span>

<span data-ttu-id="90687-114">La description et la définition de ces fonctionnalités sont disponibles ailleurs dans la documentation.</span><span class="sxs-lookup"><span data-stu-id="90687-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="90687-115">Déprécié</span><span class="sxs-lookup"><span data-stu-id="90687-115">Deprecated</span></span>

<span data-ttu-id="90687-116">Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 :</span><span class="sxs-lookup"><span data-stu-id="90687-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="90687-117">Les packages au niveau de la solution ne peuvent plus être installés</span><span class="sxs-lookup"><span data-stu-id="90687-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="90687-118">Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 et les projets qui utilisent la `project.json` spécification</span><span class="sxs-lookup"><span data-stu-id="90687-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="90687-119">`install.ps1` et `uninstall.ps1` -ces scripts seront ignorés lors de l’installation, de la restauration, de la mise à jour et de la désinstallation du package</span><span class="sxs-lookup"><span data-stu-id="90687-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="90687-120">Les transformations de configuration seront ignorées</span><span class="sxs-lookup"><span data-stu-id="90687-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="90687-121">Le contenu sera transporté, mais pas copié dans un projet.</span><span class="sxs-lookup"><span data-stu-id="90687-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="90687-122">L’équipe travaille pour réimplémenter cette fonctionnalité, suivre la discussion et la progression à l’adresse suivante : [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="90687-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="90687-123">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="90687-123">Known Issues</span></span>

<span data-ttu-id="90687-124">Un certain nombre de problèmes connus ont été fournis avec cette version.</span><span class="sxs-lookup"><span data-stu-id="90687-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="90687-125">L’installation de la version 3,1 avec le kit de développement logiciel (SDK) Windows 10 rétrograde toute version de l’extension NuGet précédemment installée</span><span class="sxs-lookup"><span data-stu-id="90687-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="90687-126">Ligne de commande NuGet</span><span class="sxs-lookup"><span data-stu-id="90687-126">NuGet Command-line</span></span>

<span data-ttu-id="90687-127">L’exécutable de ligne de commande NuGet a été mis à jour et déplacé vers un nouvel emplacement distribuable afin que les versions historiques de nuget.exe puissent continuer à être mises à disposition.</span><span class="sxs-lookup"><span data-stu-id="90687-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="90687-128">Vous pouvez télécharger la version bêta 3,1 de nuget.exe pour Windows à l’adresse suivante : [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="90687-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="90687-129">Le nouvel emplacement distribuable réside sur l’hôte dist.nuget.org, avec une structure de dossiers qui suit ce modèle :</span><span class="sxs-lookup"><span data-stu-id="90687-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="90687-130">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="90687-130">New Features</span></span>

* <span data-ttu-id="90687-131">nuget.exe pouvez restaurer et installer des packages dans des projets qui utilisent un `project.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="90687-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="90687-132">nuget.exe pouvez vous connecter au protocole NuGet v3 et l’utiliser à l’adresse suivante : [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="90687-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="90687-133">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="90687-133">Known Issues</span></span> ##

1.    <span data-ttu-id="90687-134">Impossible d’exécuter le Pack sur un `project.json` fichier- [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="90687-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="90687-135">N’est pas pris en charge sur mono- [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="90687-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="90687-136">N’est pas localisé- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="90687-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="90687-137">N’est pas signé, comme le http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="90687-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
