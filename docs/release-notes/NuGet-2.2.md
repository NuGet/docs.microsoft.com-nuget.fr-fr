---
title: Notes de publication NuGet 2.2
description: Notes de publication pour 2.2 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545990"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="9e8ef-103">Notes de publication NuGet 2.2</span><span class="sxs-lookup"><span data-stu-id="9e8ef-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="9e8ef-104">[Notes de publication de NuGet 2.1](../release-notes/nuget-2.1.md) | [Notes de publication de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="9e8ef-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="9e8ef-105">2.2 de NuGet a été publiée le 12 décembre 2012.</span><span class="sxs-lookup"><span data-stu-id="9e8ef-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="9e8ef-106">Lancement rapide Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e8ef-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="9e8ef-107">Une des nouvelles fonctionnalités qui a été ajoutée dans Visual Studio 2012 a été le [boîte de dialogue Lancement rapide](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="9e8ef-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="9e8ef-108">NuGet 2.2 étend cette boîte de dialogue, ce qui lui permet d’initialiser la boîte de dialogue de gestionnaire de package avec les termes de recherche entrés dans le lancement rapide.</span><span class="sxs-lookup"><span data-stu-id="9e8ef-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="9e8ef-109">Par exemple, saisissez « jquery » dans Lancement rapide maintenant inclut une option dans les résultats de recherche de packages NuGet correspondant à 'jquery'.</span><span class="sxs-lookup"><span data-stu-id="9e8ef-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet dans Lancement rapide de Visual Studio](./media/quick-launch.png)

<span data-ttu-id="9e8ef-111">Cette option lancera standard NuGet package manager fonctions de recherche pour le terme « jquery ».</span><span class="sxs-lookup"><span data-stu-id="9e8ef-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Boîte de dialogue Gestionnaire de Package NuGet préremplie](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="9e8ef-113">Spécifiez la totalité du dossier pour le contenu du Package</span><span class="sxs-lookup"><span data-stu-id="9e8ef-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="9e8ef-114">2.2 de NuGet vous permet désormais de spécifier un dossier entier dans le `<file>` élément de la `.nuspec` fichier à inclure tout le contenu de ce dossier.</span><span class="sxs-lookup"><span data-stu-id="9e8ef-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="9e8ef-115">Par exemple, les éléments suivants provoquent tous les scripts dans le dossier de scripts du package à ajouter au dossier contents\scripts lorsque le package est installé dans un projet.</span><span class="sxs-lookup"><span data-stu-id="9e8ef-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="9e8ef-116">**Mettre à jour du 24/6/16 : les dossiers vides dans le dossier « contenu » sont ignorés lors de l’installation du package.**</span><span class="sxs-lookup"><span data-stu-id="9e8ef-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="9e8ef-117">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="9e8ef-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="9e8ef-118">Installation du package échoue pour les projets F # lors de l’utilisation de la console du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="9e8ef-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="9e8ef-119">Lorsque vous tentez d’installer un package NuGet dans un projet F # à l’aide de la console du Gestionnaire de package, une exception InvalidOperationException est levée.</span><span class="sxs-lookup"><span data-stu-id="9e8ef-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="9e8ef-120">Nous travaillons activement avec l’équipe F # pour résoudre le problème, mais en attendant, la solution de contournement consiste à installer des packages NuGet dans des projets F # via la boîte de dialogue Gestionnaire de package de NuGet au lieu de la console.</span><span class="sxs-lookup"><span data-stu-id="9e8ef-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="9e8ef-121">[Plus d’informations sont disponibles sur CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="9e8ef-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="9e8ef-122">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="9e8ef-122">Bug Fixes</span></span>
<span data-ttu-id="9e8ef-123">NuGet 2.2 inclut plusieurs correctifs de bogues.</span><span class="sxs-lookup"><span data-stu-id="9e8ef-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="9e8ef-124">Pour obtenir une liste complète de travail éléments résolus dans NuGet 2.2, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="9e8ef-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
