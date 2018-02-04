---
title: Notes de publication NuGet 1.3 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour 1.3 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 1.3 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="0a7c0-104">Notes de version 1.3 de NuGet</span><span class="sxs-lookup"><span data-stu-id="0a7c0-104">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="0a7c0-105">[Notes de publication NuGet 1.2](../release-notes/nuget-1.2.md) | [NuGet 1.4 Notes de publication](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="0a7c0-105">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="0a7c0-106">NuGet 1.3 a été publiée le 25 avril 2011.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-106">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="0a7c0-107">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="0a7c0-107">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="0a7c0-108">Création simplifiée d’un Package avec l’intégration du serveur de symboles</span><span class="sxs-lookup"><span data-stu-id="0a7c0-108">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="0a7c0-109">L’équipe NuGet en partenariat avec le personnel à [SymbolSource.org](http://www.symbolsource.org/) pour offrir un moyen simple de la publication de vos sources et les du PDB en même temps que votre package.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-109">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="0a7c0-110">Cela permet aux consommateurs de votre package de pas à pas détaillé de la source de votre package dans le débogueur.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-110">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="0a7c0-111">Pour plus d’informations, consultez [création et la publication d’un Package de symbole](../create-packages/symbol-packages.md) la méthode simple pour publier des packages NuGet avec des sources.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-111">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="0a7c0-112">Vous pouvez également regarder une démonstration en direct de cette fonctionnalité dans le cadre de NuGet en profondeur parler à Mix11.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-112">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="0a7c0-113">Cette fonctionnalité est pleinement démontrée en commençant à la marque de 20 minutes de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-113">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="0a7c0-114">`Open-PackagePage`Commande</span><span class="sxs-lookup"><span data-stu-id="0a7c0-114">`Open-PackagePage` Command</span></span>

<span data-ttu-id="0a7c0-115">Cette commande facilite l’accès à la page de projet pour un package à partir de la console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-115">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="0a7c0-116">Il fournit également des options pour ouvrir l’URL de licence et la page du rapport abus pour le package.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-116">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="0a7c0-117">La syntaxe de la commande est :</span><span class="sxs-lookup"><span data-stu-id="0a7c0-117">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="0a7c0-118">Le `-PassThru` option est utilisée pour retourner la valeur de l’URL spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-118">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="0a7c0-119">Exemples :</span><span class="sxs-lookup"><span data-stu-id="0a7c0-119">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="0a7c0-120">Ouvre un navigateur vers l’URL de projet spécifiée dans le package Ninject.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-120">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="0a7c0-121">Ouvre un navigateur vers l’URL de licence spécifiée dans le package Ninject.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-121">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="0a7c0-122">Ouvre un navigateur vers l’URL de la source du package actuel utilisée pour signaler un abus pour le package spécifié.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-122">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="0a7c0-123">Assigne l’URL de licence à la variable $url sans ouvrir l’URL dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-123">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="0a7c0-124">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="0a7c0-124">Performance Improvements</span></span>

<span data-ttu-id="0a7c0-125">NuGet 1.3 introduit de nombreuses améliorations des performances.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-125">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="0a7c0-126">NuGet 1.3 évite de téléchargement de la même version d’un package plusieurs fois en incluant un cache de l’utilisateur local.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-126">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="0a7c0-127">Le cache sont accessibles et désactivé via la boîte de dialogue Paramètres du Gestionnaire de Package :</span><span class="sxs-lookup"><span data-stu-id="0a7c0-127">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Boîte de dialogue Options NuGet avec les paramètres de Cache de Package](./media/nuget-options.png)

<span data-ttu-id="0a7c0-129">Autres améliorations des performances incluent la prise en charge de la compression HTTP et améliore la vitesse d’installation de package dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-129">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="0a7c0-130">Visual Studio et nuget.exe utilise la même liste de sources de package</span><span class="sxs-lookup"><span data-stu-id="0a7c0-130">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="0a7c0-131">Avant de NuGet 1.3, la liste des sources de package utilisé par nuget.exe et le complément NuGet Visual Studio n’étaient pas stockés au même endroit.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-131">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="0a7c0-132">NuGet 1.3 utilise désormais la même liste dans les deux emplacements.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-132">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="0a7c0-133">La liste est stockée dans `NuGet.Config` et stockés dans le dossier AppData.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-133">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="0a7c0-134">NuGet.exe ignore les fichiers et dossiers qui commencent par «. » par défaut</span><span class="sxs-lookup"><span data-stu-id="0a7c0-134">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="0a7c0-135">Pour fonctionner avec les systèmes de contrôle de code source ces Mercurial et la sous-version NuGet, nuget.exe ignore les dossiers et fichiers qui commencent par le '.' caractère lors de la création de packages.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-135">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="0a7c0-136">Cela peut être substituée à l’aide de deux nouveaux indicateurs :</span><span class="sxs-lookup"><span data-stu-id="0a7c0-136">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="0a7c0-137">__-NoDefaultExcludes__ est utilisée pour remplacer ce paramètre et d’inclure tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-137">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="0a7c0-138">__-Exclure__ est utilisé pour ajouter d’autres fichiers/dossiers à exclure à l’aide d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-138">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="0a7c0-139">Par exemple, pour exclure tous les fichiers avec l’extension de fichier '.bak'</span><span class="sxs-lookup"><span data-stu-id="0a7c0-139">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="0a7c0-140">_Remarque : le modèle n’est pas récursive par défaut._</span><span class="sxs-lookup"><span data-stu-id="0a7c0-140">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="0a7c0-141">Prise en charge des projets WiX et Micro .NET Framework</span><span class="sxs-lookup"><span data-stu-id="0a7c0-141">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="0a7c0-142">Grâce aux contributions de la Communauté, NuGet prend en charge les types de projets WiX, ainsi que le Micro de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-142">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="0a7c0-143">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="0a7c0-143">Bug Fixes</span></span>

<span data-ttu-id="0a7c0-144">Pour obtenir une liste complète des correctifs de bogues, veuillez consulter le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="0a7c0-144">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="0a7c0-145">Correctifs de bogues à noter</span><span class="sxs-lookup"><span data-stu-id="0a7c0-145">Bug fixes worth noting</span></span>

* <span data-ttu-id="0a7c0-146">Les packages avec les fichiers sources fonctionnent dans les deux sites Web et projets d’Application Web.</span><span class="sxs-lookup"><span data-stu-id="0a7c0-146">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="0a7c0-147">Pour les sites Web, les fichiers sources sont copiés dans le `App_Code` dossier</span><span class="sxs-lookup"><span data-stu-id="0a7c0-147">For Websites, source files are copied into the `App_Code` folder</span></span>
