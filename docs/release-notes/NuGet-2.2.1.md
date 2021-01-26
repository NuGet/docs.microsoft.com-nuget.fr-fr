---
title: Notes de publication de NuGet 2.2.1
description: Notes de publication pour NuGet 2.2.1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776806"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="06ed8-103">Notes de publication de NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="06ed8-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="06ed8-104">Notes de publication de [NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Notes de publication de NuGet 2,5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="06ed8-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="06ed8-105">NuGet 2.2.1 a été publié le 15 février 2013.</span><span class="sxs-lookup"><span data-stu-id="06ed8-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="06ed8-106">Le numéro de version de l’extension VS est 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="06ed8-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="06ed8-107">Actualisation de la localisation</span><span class="sxs-lookup"><span data-stu-id="06ed8-107">Localization Refresh</span></span>
<span data-ttu-id="06ed8-108">Lorsque NuGet est fourni avec Visual Studio 2012, il a été entièrement localisé en anglais + 13 autres langages.</span><span class="sxs-lookup"><span data-stu-id="06ed8-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="06ed8-109">Depuis, NuGet 2,1 et 2,2 ont été expédiés, mais la localisation n’a pas été actualisée.</span><span class="sxs-lookup"><span data-stu-id="06ed8-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="06ed8-110">La version 2.2.1 de NuGet actualise notre localisation.</span><span class="sxs-lookup"><span data-stu-id="06ed8-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="06ed8-111">L’interface utilisateur et la console PowerShell de NuGet sont localisées dans les langues suivantes :</span><span class="sxs-lookup"><span data-stu-id="06ed8-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="06ed8-112">Chinois (simplifié)</span><span class="sxs-lookup"><span data-stu-id="06ed8-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="06ed8-113">Chinois (traditionnel)</span><span class="sxs-lookup"><span data-stu-id="06ed8-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="06ed8-114">Tchèque</span><span class="sxs-lookup"><span data-stu-id="06ed8-114">Czech</span></span>
1. <span data-ttu-id="06ed8-115">Anglais</span><span class="sxs-lookup"><span data-stu-id="06ed8-115">English</span></span>
1. <span data-ttu-id="06ed8-116">Français</span><span class="sxs-lookup"><span data-stu-id="06ed8-116">French</span></span>
1. <span data-ttu-id="06ed8-117">Allemand</span><span class="sxs-lookup"><span data-stu-id="06ed8-117">German</span></span>
1. <span data-ttu-id="06ed8-118">Italien</span><span class="sxs-lookup"><span data-stu-id="06ed8-118">Italian</span></span>
1. <span data-ttu-id="06ed8-119">Japonais</span><span class="sxs-lookup"><span data-stu-id="06ed8-119">Japanese</span></span>
1. <span data-ttu-id="06ed8-120">Coréen</span><span class="sxs-lookup"><span data-stu-id="06ed8-120">Korean</span></span>
1. <span data-ttu-id="06ed8-121">Polonais</span><span class="sxs-lookup"><span data-stu-id="06ed8-121">Polish</span></span>
1. <span data-ttu-id="06ed8-122">Portugais (Brésil)</span><span class="sxs-lookup"><span data-stu-id="06ed8-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="06ed8-123">Russe</span><span class="sxs-lookup"><span data-stu-id="06ed8-123">Russian</span></span>
1. <span data-ttu-id="06ed8-124">Espagnol</span><span class="sxs-lookup"><span data-stu-id="06ed8-124">Spanish</span></span>
1. <span data-ttu-id="06ed8-125">Turc</span><span class="sxs-lookup"><span data-stu-id="06ed8-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="06ed8-126">Les modèles Visual Studio prennent en charge plusieurs référentiels de packages préinstallés</span><span class="sxs-lookup"><span data-stu-id="06ed8-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="06ed8-127">Si vous produisez des modèles Visual Studio, vous pouvez utiliser NuGet pour [préinstaller les packages](../visual-studio-extensibility/visual-studio-templates.md) dans le cadre du modèle.</span><span class="sxs-lookup"><span data-stu-id="06ed8-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="06ed8-128">Jusqu’à présent, cette fonctionnalité avait une limitation que tous les packages devaient provenir de la même source.</span><span class="sxs-lookup"><span data-stu-id="06ed8-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="06ed8-129">Toutefois, avec NuGet 2.2.1, vous pouvez avoir des packages installés à partir de plusieurs référentiels (dans le modèle, un VSIX ou un dossier sur le disque défini dans le registre).</span><span class="sxs-lookup"><span data-stu-id="06ed8-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="06ed8-130">Le scénario principal de cette fonctionnalité est le modèle de projet ASP.NET personnalisé.</span><span class="sxs-lookup"><span data-stu-id="06ed8-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="06ed8-131">Les modèles ASP.NET intégrés utilisent des packages préinstallés, en extrayant des packages à partir du disque local.</span><span class="sxs-lookup"><span data-stu-id="06ed8-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="06ed8-132">Vous pouvez maintenant créer un modèle de projet ASP.NET personnalisé qui utilise les packages existants installés par ASP.NET, mais ajouter des packages NuGet supplémentaires à votre modèle.</span><span class="sxs-lookup"><span data-stu-id="06ed8-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="06ed8-133">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="06ed8-133">Bug Fixes</span></span>
<span data-ttu-id="06ed8-134">NuGet 2.2.1 comprend quelques correctifs de bogues ciblés.</span><span class="sxs-lookup"><span data-stu-id="06ed8-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="06ed8-135">Pour obtenir la liste des éléments de travail corrigés dans NuGet 2.2.1, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="06ed8-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="06ed8-136">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="06ed8-136">Known Issues</span></span>

<span data-ttu-id="06ed8-137">Si vous étendez des modèles de projet ASP.NET, tous les référentiels de packages préinstallés doivent utiliser la même valeur pour l' `isPreunzipped` attribut.</span><span class="sxs-lookup"><span data-stu-id="06ed8-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
