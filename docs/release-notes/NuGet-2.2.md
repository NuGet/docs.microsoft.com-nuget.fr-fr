---
title: Notes de publication de NuGet 2,2
description: Notes de publication de NuGet 2,2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780429"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="fe255-103">Notes de publication de NuGet 2,2</span><span class="sxs-lookup"><span data-stu-id="fe255-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="fe255-104">Notes de publication de [NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Notes de publication de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="fe255-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="fe255-105">NuGet 2,2 a été publié le 12 décembre 2012.</span><span class="sxs-lookup"><span data-stu-id="fe255-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="fe255-106">Lancement rapide Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe255-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="fe255-107">L’une des nouvelles fonctionnalités qui ont été ajoutées dans Visual Studio 2012 était la [boîte de dialogue lancement rapide](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="fe255-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="fe255-108">NuGet 2,2 étend cette boîte de dialogue, ce qui lui permet d’initialiser la boîte de dialogue du gestionnaire de package avec les termes de recherche entrés dans le lancement rapide.</span><span class="sxs-lookup"><span data-stu-id="fe255-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="fe255-109">Par exemple, l’entrée de « jQuery » dans le lancement rapide comprend désormais une option dans les résultats pour rechercher les packages NuGet correspondant à « jQuery ».</span><span class="sxs-lookup"><span data-stu-id="fe255-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet dans Visual Studio lancement rapide](./media/quick-launch.png)

<span data-ttu-id="fe255-111">Si cette option est sélectionnée, l’expérience de recherche du gestionnaire de package NuGet standard est lancée pour le terme « jQuery ».</span><span class="sxs-lookup"><span data-stu-id="fe255-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Boîte de dialogue du gestionnaire de package NuGet préremplie](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="fe255-113">Spécifier le dossier entier pour le contenu du package</span><span class="sxs-lookup"><span data-stu-id="fe255-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="fe255-114">NuGet 2,2 vous permet désormais de spécifier un dossier entier dans l' `<file>` élément du `.nuspec` fichier pour inclure tout le contenu de ce dossier.</span><span class="sxs-lookup"><span data-stu-id="fe255-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="fe255-115">Par exemple, le code suivant entraîne l’ajout de tous les scripts du dossier scripts du package au dossier contents\scripts lorsque le package est installé dans un projet.</span><span class="sxs-lookup"><span data-stu-id="fe255-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="fe255-116">**Mise à jour 6/24/16 : les dossiers vides dans le dossier « contenu » sont ignorés lors de l’installation du package.**</span><span class="sxs-lookup"><span data-stu-id="fe255-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="fe255-117">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="fe255-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="fe255-118">L’installation du package échoue pour les projets F # lors de l’utilisation de la console du gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="fe255-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="fe255-119">Lorsque vous tentez d’installer un package NuGet dans un projet F # à l’aide de la console du gestionnaire de package, une exception InvalidOperationException est levée.</span><span class="sxs-lookup"><span data-stu-id="fe255-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="fe255-120">Nous travaillons activement avec l’équipe F # pour résoudre le problème, mais dans le même temps, la solution consiste à installer des packages NuGet dans des projets F # via la boîte de dialogue du gestionnaire de package de NuGet plutôt que la console.</span><span class="sxs-lookup"><span data-stu-id="fe255-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="fe255-121">Des [informations supplémentaires sont disponibles sur CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="fe255-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="fe255-122">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="fe255-122">Bug Fixes</span></span>
<span data-ttu-id="fe255-123">NuGet 2,2 comprend de nombreux correctifs de bogues.</span><span class="sxs-lookup"><span data-stu-id="fe255-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="fe255-124">Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2,2, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="fe255-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
