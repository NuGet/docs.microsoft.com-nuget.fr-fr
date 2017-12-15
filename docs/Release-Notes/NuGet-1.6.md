---
title: Notes de publication NuGet 1.6 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ed433790-99bf-4b71-92a8-17314bd49867
description: "Notes de publication pour 1.6 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 1.6 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7824d62cb73c54205175ec742cfc26d1ca3aa741
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="4b81d-104">Notes de version 1.6 de NuGet</span><span class="sxs-lookup"><span data-stu-id="4b81d-104">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="4b81d-105">[Notes de publication NuGet 1.5](../release-notes/nuget-1.5.md) | [Notes de version 1.7 de NuGet](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="4b81d-105">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="4b81d-106">NuGet 1.6 a été publiée le 13 décembre 2011.</span><span class="sxs-lookup"><span data-stu-id="4b81d-106">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="4b81d-107">Problème connu d’Installation</span><span class="sxs-lookup"><span data-stu-id="4b81d-107">Known Installation Issue</span></span>
<span data-ttu-id="4b81d-108">Si vous exécutez Visual Studio 2010 SP1, vous susceptible de rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet, si vous disposez d’une version plus ancienne est installée.</span><span class="sxs-lookup"><span data-stu-id="4b81d-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="4b81d-109">La solution de contournement consiste à simplement désinstaller NuGet et l’installer à partir de la galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b81d-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="4b81d-110">Consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4b81d-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="4b81d-111">Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis il est probable que devez redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="4b81d-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="4b81d-112">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="4b81d-112">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="4b81d-113">Prise en charge pour le contrôle de version sémantique et les versions préliminaires des Packages</span><span class="sxs-lookup"><span data-stu-id="4b81d-113">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="4b81d-114">NuGet 1.6 introduit la prise en charge pour le contrôle de version sémantique (SemVer).</span><span class="sxs-lookup"><span data-stu-id="4b81d-114">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="4b81d-115">Pour plus d’informations sur la façon dont il utilise SemVer, lisez le [documentation du contrôle de version](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="4b81d-115">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="4b81d-116">À l’aide de NuGet sans vérifier dans des Packages (restauration de Package)</span><span class="sxs-lookup"><span data-stu-id="4b81d-116">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="4b81d-117">NuGet 1.6 prend désormais en charge de première classe pour le flux de travail dans le NuGet packages ne sont pas ajoutés au contrôle de code source, mais au lieu de cela sont restaurés au moment de la génération si manquant.</span><span class="sxs-lookup"><span data-stu-id="4b81d-117">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="4b81d-118">Pour plus d’informations, lisez la [à l’aide de NuGet sans validation des packages pour le contrôle de code source](../consume-packages/packages-and-source-control.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="4b81d-118">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="4b81d-119">Modèles d’élément qui installent des Packages NuGet</span><span class="sxs-lookup"><span data-stu-id="4b81d-119">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="4b81d-120">Basé sur le travail pour prendre en charge les package NuGet préinstallé aux modèles de projet Visual Studio, 1.6 de NuGet ajoute également la prise en charge pour les modèles d’élément Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b81d-120">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="4b81d-121">Modèles d’élément peuvent posséder des packages NuGet qui sont installées lorsque le modèle d’invoqué associées.</span><span class="sxs-lookup"><span data-stu-id="4b81d-121">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="4b81d-122">Pour plus d’informations sur la modification d’un modèle de projet/élément pour installer les packages NuGet, consultez le [Packages dans les modèles Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="4b81d-122">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="4b81d-123">Prise en charge de la désactivation des sources de package</span><span class="sxs-lookup"><span data-stu-id="4b81d-123">Support for disabling package sources</span></span>
<span data-ttu-id="4b81d-124">Lorsque plusieurs sources de package sont configurés, NuGet recherchera dans chacun d’eux pour les packages lors de l’installation d’un package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="4b81d-124">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="4b81d-125">Une source de package est arrêté pour une raison quelconque peut gravement ralentissent NuGet.</span><span class="sxs-lookup"><span data-stu-id="4b81d-125">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="4b81d-126">Avant NuGet 1.6, vous pourriez supprimer la source du package, mais vous devez mémoriser les détails lorsque vous souhaitez ajouter de nouveau.</span><span class="sxs-lookup"><span data-stu-id="4b81d-126">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="4b81d-127">NuGet 1.6 permet de désactivation d’une source de package pour le désactiver, mais l’application.</span><span class="sxs-lookup"><span data-stu-id="4b81d-127">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![La désactivation d’un package](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="4b81d-129">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="4b81d-129">Bug Fixes</span></span>
<span data-ttu-id="4b81d-130">NuGet 1.6 comportait 106 fixe des éléments de travail.</span><span class="sxs-lookup"><span data-stu-id="4b81d-130">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="4b81d-131">95 de celles qui ont été classés en tant que bogues et 10 d'entre eux ont des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="4b81d-131">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="4b81d-132">Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.6, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="4b81d-132">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
