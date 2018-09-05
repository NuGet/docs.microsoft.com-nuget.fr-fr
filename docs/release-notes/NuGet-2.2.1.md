---
title: Notes de publication de NuGet 2.2.1
description: Notes de publication pour NuGet 2.2.1 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550696"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="06b48-103">Notes de publication de NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="06b48-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="06b48-104">[Notes de publication de NuGet 2.2](../release-notes/nuget-2.2.md) | [Notes de publication de NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="06b48-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="06b48-105">NuGet 2.2.1 a été publiée le 15 février 2013.</span><span class="sxs-lookup"><span data-stu-id="06b48-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="06b48-106">Le numéro de version d’Extension VS est 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="06b48-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="06b48-107">Actualisation de la localisation</span><span class="sxs-lookup"><span data-stu-id="06b48-107">Localization Refresh</span></span>
<span data-ttu-id="06b48-108">Lorsque NuGet partie intégrante de Visual Studio 2012, elle a été entièrement localisée en anglais + 13 autres langues.</span><span class="sxs-lookup"><span data-stu-id="06b48-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="06b48-109">Depuis lors, NuGet 2.1 et 2.2 ont été renvoyés, mais la localisation n’avait pas été actualisée.</span><span class="sxs-lookup"><span data-stu-id="06b48-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="06b48-110">La version de NuGet 2.2.1 actualise la localisation.</span><span class="sxs-lookup"><span data-stu-id="06b48-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="06b48-111">L’interface utilisateur de NuGet et la PowerShell Console sont traduits dans les langues suivantes :</span><span class="sxs-lookup"><span data-stu-id="06b48-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="06b48-112">Chinois (simplifié)</span><span class="sxs-lookup"><span data-stu-id="06b48-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="06b48-113">Chinois (traditionnel)</span><span class="sxs-lookup"><span data-stu-id="06b48-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="06b48-114">Tchèque</span><span class="sxs-lookup"><span data-stu-id="06b48-114">Czech</span></span>
1. <span data-ttu-id="06b48-115">Anglais</span><span class="sxs-lookup"><span data-stu-id="06b48-115">English</span></span>
1. <span data-ttu-id="06b48-116">Français</span><span class="sxs-lookup"><span data-stu-id="06b48-116">French</span></span>
1. <span data-ttu-id="06b48-117">Allemand</span><span class="sxs-lookup"><span data-stu-id="06b48-117">German</span></span>
1. <span data-ttu-id="06b48-118">Italien</span><span class="sxs-lookup"><span data-stu-id="06b48-118">Italian</span></span>
1. <span data-ttu-id="06b48-119">Japonais</span><span class="sxs-lookup"><span data-stu-id="06b48-119">Japanese</span></span>
1. <span data-ttu-id="06b48-120">Coréen</span><span class="sxs-lookup"><span data-stu-id="06b48-120">Korean</span></span>
1. <span data-ttu-id="06b48-121">Polonais</span><span class="sxs-lookup"><span data-stu-id="06b48-121">Polish</span></span>
1. <span data-ttu-id="06b48-122">Portugais (Brésil)</span><span class="sxs-lookup"><span data-stu-id="06b48-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="06b48-123">Russe</span><span class="sxs-lookup"><span data-stu-id="06b48-123">Russian</span></span>
1. <span data-ttu-id="06b48-124">Espagnol</span><span class="sxs-lookup"><span data-stu-id="06b48-124">Spanish</span></span>
1. <span data-ttu-id="06b48-125">Turc</span><span class="sxs-lookup"><span data-stu-id="06b48-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="06b48-126">Modèles Visual Studio prend en charge plusieurs référentiels de packages préinstallés</span><span class="sxs-lookup"><span data-stu-id="06b48-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="06b48-127">Si vous produisez des modèles Visual Studio, vous pouvez utiliser NuGet pour [préinstaller les packages](../visual-studio-extensibility/visual-studio-templates.md) en tant que partie du modèle.</span><span class="sxs-lookup"><span data-stu-id="06b48-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="06b48-128">Jusqu'à présent, cette fonctionnalité était une limitation que tous les packages nécessaires à venir de la même source.</span><span class="sxs-lookup"><span data-stu-id="06b48-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="06b48-129">Avec NuGet 2.2.1 Cependant, vous pouvez avoir des packages installés à partir de plusieurs référentiels (dans le modèle, une extension VSIX ou dans un dossier sur le disque défini dans le Registre).</span><span class="sxs-lookup"><span data-stu-id="06b48-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="06b48-130">Le scénario principal de cette fonctionnalité est des modèles de projet ASP.NET personnalisés.</span><span class="sxs-lookup"><span data-stu-id="06b48-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="06b48-131">Les modèles d’ASP.NET intégrés utilisent des packages préinstallés, extraction de packages à partir du disque local.</span><span class="sxs-lookup"><span data-stu-id="06b48-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="06b48-132">Vous pouvez maintenant créer un modèle de projet ASP.NET personnalisé qui utilise les packages existants installés par ASP.NET et ajouter les packages NuGet supplémentaires dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="06b48-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="06b48-133">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="06b48-133">Bug Fixes</span></span>
<span data-ttu-id="06b48-134">NuGet 2.2.1 comprend quelques correctifs de bogues ciblés.</span><span class="sxs-lookup"><span data-stu-id="06b48-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="06b48-135">Pour obtenir la liste de travail éléments résolus dans NuGet 2.2.1, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="06b48-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="06b48-136">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="06b48-136">Known Issues</span></span>

<span data-ttu-id="06b48-137">Si vous étendez des modèles de projet ASP.NET, tous les référentiels de packages préinstallés doivent utiliser la même valeur pour le `isPreunzipped` attribut.</span><span class="sxs-lookup"><span data-stu-id="06b48-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
