---
title: Notes de version 1.6 de NuGet
description: Notes de publication pour 1.6 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0345e180893a56302385d27792c4e15ba5d96989
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="af9b5-103">Notes de version 1.6 de NuGet</span><span class="sxs-lookup"><span data-stu-id="af9b5-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="af9b5-104">[Notes de publication NuGet 1.5](../release-notes/nuget-1.5.md) | [Notes de version 1.7 de NuGet](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="af9b5-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="af9b5-105">NuGet 1.6 a été publiée le 13 décembre 2011.</span><span class="sxs-lookup"><span data-stu-id="af9b5-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="af9b5-106">Problème connu d’Installation</span><span class="sxs-lookup"><span data-stu-id="af9b5-106">Known Installation Issue</span></span>
<span data-ttu-id="af9b5-107">Si vous exécutez Visual Studio 2010 SP1, vous susceptible de rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet, si vous disposez d’une version plus ancienne est installée.</span><span class="sxs-lookup"><span data-stu-id="af9b5-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="af9b5-108">La solution de contournement consiste à simplement désinstaller NuGet et l’installer à partir de la galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af9b5-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="af9b5-109">Pour plus d’informations, consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="af9b5-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="af9b5-110">Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis il est probable que devez redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="af9b5-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="af9b5-111">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="af9b5-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="af9b5-112">Prise en charge pour le contrôle de version sémantique et les versions préliminaires des Packages</span><span class="sxs-lookup"><span data-stu-id="af9b5-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="af9b5-113">NuGet 1.6 introduit la prise en charge pour le contrôle de version sémantique (SemVer).</span><span class="sxs-lookup"><span data-stu-id="af9b5-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="af9b5-114">Pour plus d’informations sur la façon dont il utilise SemVer, lisez le [documentation du contrôle de version](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="af9b5-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="af9b5-115">À l’aide de NuGet sans vérifier dans des Packages (restauration de Package)</span><span class="sxs-lookup"><span data-stu-id="af9b5-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="af9b5-116">NuGet 1.6 prend désormais en charge de première classe pour le flux de travail dans le NuGet packages ne sont pas ajoutés au contrôle de code source, mais au lieu de cela sont restaurés au moment de la génération si manquant.</span><span class="sxs-lookup"><span data-stu-id="af9b5-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="af9b5-117">Pour plus d’informations, lisez la [à l’aide de NuGet sans validation des packages pour le contrôle de code source](../consume-packages/packages-and-source-control.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="af9b5-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="af9b5-118">Modèles d’élément qui installent des Packages NuGet</span><span class="sxs-lookup"><span data-stu-id="af9b5-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="af9b5-119">Basé sur le travail pour prendre en charge les package NuGet préinstallé aux modèles de projet Visual Studio, 1.6 de NuGet ajoute également la prise en charge pour les modèles d’élément Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af9b5-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="af9b5-120">Modèles d’élément peuvent posséder des packages NuGet qui sont installées lorsque le modèle d’invoqué associées.</span><span class="sxs-lookup"><span data-stu-id="af9b5-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="af9b5-121">Pour plus d’informations sur la modification d’un modèle de projet/élément pour installer les packages NuGet, consultez le [Packages dans les modèles Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="af9b5-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="af9b5-122">Prise en charge de la désactivation des sources de package</span><span class="sxs-lookup"><span data-stu-id="af9b5-122">Support for disabling package sources</span></span>
<span data-ttu-id="af9b5-123">Lorsque plusieurs sources de package sont configurés, NuGet recherchera dans chacun d’eux pour les packages lors de l’installation d’un package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="af9b5-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="af9b5-124">Une source de package est arrêté pour une raison quelconque peut gravement ralentissent NuGet.</span><span class="sxs-lookup"><span data-stu-id="af9b5-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="af9b5-125">Avant NuGet 1.6, vous pourriez supprimer la source du package, mais vous devez mémoriser les détails lorsque vous souhaitez ajouter de nouveau.</span><span class="sxs-lookup"><span data-stu-id="af9b5-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="af9b5-126">NuGet 1.6 permet de désactivation d’une source de package pour le désactiver, mais l’application.</span><span class="sxs-lookup"><span data-stu-id="af9b5-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![La désactivation d’un package](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="af9b5-128">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="af9b5-128">Bug Fixes</span></span>
<span data-ttu-id="af9b5-129">NuGet 1.6 comportait 106 fixe des éléments de travail.</span><span class="sxs-lookup"><span data-stu-id="af9b5-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="af9b5-130">95 de celles qui ont été classés en tant que bogues et 10 d'entre eux ont des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="af9b5-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="af9b5-131">Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.6, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="af9b5-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
