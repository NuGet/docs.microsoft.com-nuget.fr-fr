---
title: Notes de version 1.6 de NuGet
description: Notes de publication pour 1.6 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549010"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="ca34a-103">Notes de version 1.6 de NuGet</span><span class="sxs-lookup"><span data-stu-id="ca34a-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="ca34a-104">[Notes de publication de NuGet 1.5](../release-notes/nuget-1.5.md) | [Notes de publication de NuGet 1.7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="ca34a-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="ca34a-105">1.6 de NuGet a été publiée le 13 décembre 2011.</span><span class="sxs-lookup"><span data-stu-id="ca34a-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ca34a-106">Problème d’Installation connus</span><span class="sxs-lookup"><span data-stu-id="ca34a-106">Known Installation Issue</span></span>
<span data-ttu-id="ca34a-107">Si vous exécutez Visual Studio 2010 SP1, vous pouvez rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet si vous avez une version antérieure est installée.</span><span class="sxs-lookup"><span data-stu-id="ca34a-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ca34a-108">La solution de contournement consiste à désinstaller simplement NuGet, puis l’installer à partir de la galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca34a-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ca34a-109">Pour plus d’informations, consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="ca34a-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="ca34a-110">Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis vous avez probablement besoin de redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="ca34a-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="ca34a-111">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="ca34a-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="ca34a-112">Prise en charge pour le contrôle de version sémantique et les Packages de version préliminaire</span><span class="sxs-lookup"><span data-stu-id="ca34a-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="ca34a-113">1.6 de NuGet prend désormais en charge pour la gestion sémantique de version (SemVer).</span><span class="sxs-lookup"><span data-stu-id="ca34a-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="ca34a-114">Pour plus d’informations sur la façon dont il utilise SemVer, lisez le [documentation sur le contrôle de version](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ca34a-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="ca34a-115">À l’aide de NuGet sans vérifier dans des Packages (restauration de Package)</span><span class="sxs-lookup"><span data-stu-id="ca34a-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="ca34a-116">1.6 de NuGet prend désormais en charge de première classe pour le flux de travail dans le NuGet packages ne sont pas ajoutés au contrôle de code source, mais au lieu de cela sont restaurés au moment de la génération s’il est manquant.</span><span class="sxs-lookup"><span data-stu-id="ca34a-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="ca34a-117">Pour plus d’informations, consultez le [à l’aide de NuGet sans validation des packages pour le contrôle de code source](../consume-packages/packages-and-source-control.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="ca34a-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="ca34a-118">Modèles d’élément qui installer les Packages NuGet</span><span class="sxs-lookup"><span data-stu-id="ca34a-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="ca34a-119">S’appuyant sur le travail pour prendre en charge les packages NuGet préinstallés les modèles de projet Visual Studio, NuGet 1.6 ajoute également la prise en charge pour les modèles d’élément Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca34a-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="ca34a-120">Modèles d’élément peuvent avoir des packages NuGet qui sont installés lorsque le modèle dans appelé associées.</span><span class="sxs-lookup"><span data-stu-id="ca34a-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="ca34a-121">Pour plus d’informations sur la modification d’un modèle de projet/élément pour installer les packages NuGet, lisez le [Packages dans les modèles Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="ca34a-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="ca34a-122">Prise en charge de la désactivation des sources de package</span><span class="sxs-lookup"><span data-stu-id="ca34a-122">Support for disabling package sources</span></span>
<span data-ttu-id="ca34a-123">Lorsque plusieurs sources de package sont configurées, NuGet recherche dans chacun d’eux pour les packages lors de l’installation d’un package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="ca34a-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="ca34a-124">Une source de package est arrêté pour une raison quelconque peut sérieusement ralentir NuGet.</span><span class="sxs-lookup"><span data-stu-id="ca34a-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="ca34a-125">Avant NuGet 1.6, vous pouvez supprimer la source du package, mais vous devez ensuite n’oubliez pas les détails du moment où vous souhaitez pour l’ajouter de nouveau.</span><span class="sxs-lookup"><span data-stu-id="ca34a-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="ca34a-126">NuGet 1.6 permet une source de package pour le désactiver, mais gardez-le décochant l’option.</span><span class="sxs-lookup"><span data-stu-id="ca34a-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![La désactivation d’un package](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="ca34a-128">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="ca34a-128">Bug Fixes</span></span>
<span data-ttu-id="ca34a-129">NuGet 1.6 avait un total de 106 fixe des éléments de travail.</span><span class="sxs-lookup"><span data-stu-id="ca34a-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="ca34a-130">95 de ceux qui ont été classés comme des bogues et 10 de ces étaient des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="ca34a-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="ca34a-131">Pour obtenir une liste complète de travail éléments résolus dans NuGet 1.6, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="ca34a-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
