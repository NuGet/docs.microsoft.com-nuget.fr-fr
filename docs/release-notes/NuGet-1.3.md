---
title: Notes de publication de NuGet 1,3
description: Notes de publication de NuGet 1,3, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777123"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="4f0d4-103">Notes de publication de NuGet 1,3</span><span class="sxs-lookup"><span data-stu-id="4f0d4-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="4f0d4-104">Notes de publication de [NuGet 1,2](../release-notes/nuget-1.2.md)  |  [Notes de publication de NuGet 1,4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="4f0d4-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="4f0d4-105">NuGet 1,3 a été publié le 25 avril 2011.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="4f0d4-106">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="4f0d4-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="4f0d4-107">Création de packages rationalisée avec intégration de serveur de symboles</span><span class="sxs-lookup"><span data-stu-id="4f0d4-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="4f0d4-108">L’équipe NuGet a fait ses partenariats avec les personnes de [SymbolSource.org](http://www.symbolsource.org/) pour offrir un moyen simple de publier vos sources et vos PDB avec votre package.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="4f0d4-109">Cela permet aux consommateurs de votre package d’effectuer un pas à pas détaillé dans la source de votre package dans le débogueur.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="4f0d4-110">Pour plus d’informations, consultez [création et publication d’un package de symboles](../create-packages/symbol-packages.md) le moyen le plus simple de publier des packages NuGet avec des sources.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="4f0d4-111">Vous pouvez également regarder une démonstration en direct de cette fonctionnalité dans le cadre de la Conférence NuGet en profondeur sur MIX11.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="4f0d4-112">Cette fonctionnalité est entièrement démontrée à partir de 20 minutes de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="4f0d4-113">`Open-PackagePage` Command</span><span class="sxs-lookup"><span data-stu-id="4f0d4-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="4f0d4-114">Cette commande permet d’accéder facilement à la page de projet d’un package à partir de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="4f0d4-115">Il fournit également des options pour ouvrir l’URL de licence et la page signaler un abus pour le package.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="4f0d4-116">La syntaxe de la commande est la suivante :</span><span class="sxs-lookup"><span data-stu-id="4f0d4-116">The syntax for the command is:</span></span>

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

<span data-ttu-id="4f0d4-117">L' `-PassThru` option est utilisée pour retourner la valeur de l’URL spécifiée.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="4f0d4-118">Exemples :</span><span class="sxs-lookup"><span data-stu-id="4f0d4-118">Examples:</span></span>

```
PM> Open-PackagePage Ninject
```

<span data-ttu-id="4f0d4-119">Ouvre un navigateur à l’URL du projet spécifiée dans le package Ninject.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -License
```

<span data-ttu-id="4f0d4-120">Ouvre un navigateur à l’URL de licence spécifiée dans le package Ninject.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -ReportAbuse
```

<span data-ttu-id="4f0d4-121">Ouvre un navigateur à l’URL de la source de package actuelle utilisée pour signaler un abus pour le package spécifié.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

<span data-ttu-id="4f0d4-122">Affecte l’URL de licence à la variable, $url, sans ouvrir l’URL dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="4f0d4-123">Optimisation des performances</span><span class="sxs-lookup"><span data-stu-id="4f0d4-123">Performance Improvements</span></span>

<span data-ttu-id="4f0d4-124">NuGet 1,3 introduit de nombreuses améliorations en matière de performances.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="4f0d4-125">NuGet 1,3 évite de télécharger plusieurs fois la même version d’un package en incluant un cache par utilisateur local.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="4f0d4-126">Le cache est accessible et effacé via la boîte de dialogue des paramètres du gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="4f0d4-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Boîte de dialogue Options NuGet avec les paramètres du cache du package](./media/nuget-options.png)

<span data-ttu-id="4f0d4-128">D’autres améliorations de performances incluent l’ajout de la prise en charge de la compression HTTP et l’amélioration de la vitesse d’installation du package dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="4f0d4-129">Visual Studio et nuget.exe utilisent la même liste de sources de packages</span><span class="sxs-lookup"><span data-stu-id="4f0d4-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="4f0d4-130">Avant NuGet 1,3, la liste des sources de packages utilisées par nuget.exe et la Add-In de Visual Studio NuGet n’étaient pas stockées au même endroit.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="4f0d4-131">NuGet 1,3 utilise désormais la même liste aux deux emplacements.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="4f0d4-132">La liste est stockée dans `NuGet.Config` le dossier AppData et stockée dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="4f0d4-133">nuget.exe ignore les fichiers et dossiers qui commencent par « . » par défaut</span><span class="sxs-lookup"><span data-stu-id="4f0d4-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="4f0d4-134">Pour que NuGet fonctionne correctement avec les systèmes de contrôle de code source tels que Subversion et mercurial, nuget.exe ignore les dossiers et les fichiers qui commencent par le caractère « . » lors de la création de packages.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="4f0d4-135">Vous pouvez le remplacer à l’aide de deux nouveaux indicateurs :</span><span class="sxs-lookup"><span data-stu-id="4f0d4-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="4f0d4-136">__-NoDefaultExcludes__ est utilisé pour remplacer ce paramètre et inclure tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="4f0d4-137">__-Exclude__ est utilisé pour ajouter d’autres fichiers/dossiers à exclure à l’aide d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="4f0d4-138">Par exemple, pour exclure tous les fichiers avec l’extension de fichier « . bak »</span><span class="sxs-lookup"><span data-stu-id="4f0d4-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="4f0d4-139">_Remarque : le modèle n’est pas récursif par défaut._</span><span class="sxs-lookup"><span data-stu-id="4f0d4-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="4f0d4-140">Prise en charge des projets WiX et de .NET micro Framework</span><span class="sxs-lookup"><span data-stu-id="4f0d4-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="4f0d4-141">Grâce aux contributions de la Communauté, NuGet prend en charge les types de projets WiX, ainsi que le .NET micro Framework.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4f0d4-142">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="4f0d4-142">Bug Fixes</span></span>

<span data-ttu-id="4f0d4-143">Pour obtenir la liste complète des correctifs de bogues, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="4f0d4-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="4f0d4-144">Correction des bogues à noter</span><span class="sxs-lookup"><span data-stu-id="4f0d4-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="4f0d4-145">Les packages avec des fichiers sources fonctionnent dans les deux sites Web et dans les projets d’application Web.</span><span class="sxs-lookup"><span data-stu-id="4f0d4-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="4f0d4-146">Pour les sites Web, les fichiers sources sont copiés dans le `App_Code` dossier</span><span class="sxs-lookup"><span data-stu-id="4f0d4-146">For Websites, source files are copied into the `App_Code` folder</span></span>
