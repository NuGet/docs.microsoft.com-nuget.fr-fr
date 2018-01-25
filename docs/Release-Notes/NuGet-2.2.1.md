---
title: Notes de publication NuGet 2.2.1 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet 2.2.1, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 2.2.1 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="615fa-104">Notes de version 2.2.1 de NuGet</span><span class="sxs-lookup"><span data-stu-id="615fa-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="615fa-105">[Notes de publication NuGet 2.2](../release-notes/nuget-2.2.md) | [NuGet 2.5 Notes de publication](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="615fa-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="615fa-106">NuGet 2.2.1 a été publiée le 15 février 2013.</span><span class="sxs-lookup"><span data-stu-id="615fa-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="615fa-107">Le numéro de version Extension VS est 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="615fa-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="615fa-108">Actualisation de la localisation</span><span class="sxs-lookup"><span data-stu-id="615fa-108">Localization Refresh</span></span>
<span data-ttu-id="615fa-109">Lors de l’expédition NuGet dans le cadre de Visual Studio 2012, elle a été entièrement localisée en anglais + 13 autres langues.</span><span class="sxs-lookup"><span data-stu-id="615fa-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="615fa-110">Depuis, NuGet 2.1 et 2.2 ont été expédiés mais la localisation n’avait pas été actualisée.</span><span class="sxs-lookup"><span data-stu-id="615fa-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="615fa-111">La version NuGet 2.2.1 actualise la localisation.</span><span class="sxs-lookup"><span data-stu-id="615fa-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="615fa-112">Interface utilisateur et la PowerShell Console de NuGet sont traduits dans les langues suivantes :</span><span class="sxs-lookup"><span data-stu-id="615fa-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="615fa-113">Chinois (simplifié)</span><span class="sxs-lookup"><span data-stu-id="615fa-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="615fa-114">Chinois (traditionnel)</span><span class="sxs-lookup"><span data-stu-id="615fa-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="615fa-115">Tchèque</span><span class="sxs-lookup"><span data-stu-id="615fa-115">Czech</span></span>
1. <span data-ttu-id="615fa-116">Anglais</span><span class="sxs-lookup"><span data-stu-id="615fa-116">English</span></span>
1. <span data-ttu-id="615fa-117">Français</span><span class="sxs-lookup"><span data-stu-id="615fa-117">French</span></span>
1. <span data-ttu-id="615fa-118">Allemand</span><span class="sxs-lookup"><span data-stu-id="615fa-118">German</span></span>
1. <span data-ttu-id="615fa-119">Italien</span><span class="sxs-lookup"><span data-stu-id="615fa-119">Italian</span></span>
1. <span data-ttu-id="615fa-120">Japonais</span><span class="sxs-lookup"><span data-stu-id="615fa-120">Japanese</span></span>
1. <span data-ttu-id="615fa-121">Coréen</span><span class="sxs-lookup"><span data-stu-id="615fa-121">Korean</span></span>
1. <span data-ttu-id="615fa-122">Polonais</span><span class="sxs-lookup"><span data-stu-id="615fa-122">Polish</span></span>
1. <span data-ttu-id="615fa-123">Portugais (Brésil)</span><span class="sxs-lookup"><span data-stu-id="615fa-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="615fa-124">Russe</span><span class="sxs-lookup"><span data-stu-id="615fa-124">Russian</span></span>
1. <span data-ttu-id="615fa-125">Espagnol</span><span class="sxs-lookup"><span data-stu-id="615fa-125">Spanish</span></span>
1. <span data-ttu-id="615fa-126">Turc</span><span class="sxs-lookup"><span data-stu-id="615fa-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="615fa-127">Modèles Visual Studio prend en charge plusieurs référentiels Package préinstallé</span><span class="sxs-lookup"><span data-stu-id="615fa-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="615fa-128">Si vous produisez des modèles Visual Studio, vous pouvez utiliser NuGet pour [préinstaller les packages](../visual-studio-extensibility/visual-studio-templates.md) en tant que partie du modèle.</span><span class="sxs-lookup"><span data-stu-id="615fa-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="615fa-129">Jusqu'à présent, cette fonctionnalité avait une limitation que tous les packages doivent provenir de la même source.</span><span class="sxs-lookup"><span data-stu-id="615fa-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="615fa-130">Avec NuGet 2.2.1, vous pouvez avoir des packages installés à partir de plusieurs référentiels (dans le modèle, une extension VSIX ou un dossier sur le disque défini dans le Registre).</span><span class="sxs-lookup"><span data-stu-id="615fa-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="615fa-131">Le scénario principal de cette fonctionnalité est des modèles de projet ASP.NET personnalisés.</span><span class="sxs-lookup"><span data-stu-id="615fa-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="615fa-132">Les modèles ASP.NET intégrés utilisent les packages préinstallés, extraction de packages à partir du disque local.</span><span class="sxs-lookup"><span data-stu-id="615fa-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="615fa-133">Vous pouvez maintenant créer un modèle de projet ASP.NET personnalisé qui utilise les packages existants installés par ASP.NET et ajouter des packages NuGet supplémentaires dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="615fa-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="615fa-134">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="615fa-134">Bug Fixes</span></span>
<span data-ttu-id="615fa-135">NuGet 2.2.1 comprend plusieurs correctifs de bogues ciblés.</span><span class="sxs-lookup"><span data-stu-id="615fa-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="615fa-136">Pour obtenir la liste de travail éléments fixes dans NuGet 2.2.1, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="615fa-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="615fa-137">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="615fa-137">Known Issues</span></span>

<span data-ttu-id="615fa-138">Si vous étendez des modèles de projet ASP.NET, tous les référentiels préinstallé package doivent utiliser la même valeur pour le `isPreunzipped` attribut.</span><span class="sxs-lookup"><span data-stu-id="615fa-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
