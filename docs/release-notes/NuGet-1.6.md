---
title: Notes de publication de NuGet 1,6
description: Notes de publication de NuGet 1,6, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384135"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="73ab2-103">Notes de publication de NuGet 1,6</span><span class="sxs-lookup"><span data-stu-id="73ab2-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="73ab2-104">[Notes de publication de nuget 1,5](../release-notes/nuget-1.5.md) | [notes de publication de NuGet 1,7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="73ab2-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="73ab2-105">NuGet 1,6 a été publié le 13 décembre 2011.</span><span class="sxs-lookup"><span data-stu-id="73ab2-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="73ab2-106">Problème d’installation connu</span><span class="sxs-lookup"><span data-stu-id="73ab2-106">Known Installation Issue</span></span>
<span data-ttu-id="73ab2-107">Si vous exécutez VS 2010 SP1, vous pouvez rencontrer une erreur d’installation lors de la tentative de mise à niveau de NuGet si une version antérieure est installée.</span><span class="sxs-lookup"><span data-stu-id="73ab2-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="73ab2-108">La solution consiste à désinstaller simplement NuGet, puis à l’installer à partir de la Galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73ab2-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="73ab2-109">Pour plus d'informations, voir <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="73ab2-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="73ab2-110">Remarque : si Visual Studio ne vous permet pas de désinstaller l’extension (le bouton désinstaller est désactivé), vous devrez probablement redémarrer Visual Studio à l’aide de « exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="73ab2-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="73ab2-111">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="73ab2-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="73ab2-112">Prise en charge du contrôle de version sémantique et des packages de préversion</span><span class="sxs-lookup"><span data-stu-id="73ab2-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="73ab2-113">NuGet 1,6 introduit la prise en charge de la gestion sémantique des versions (SemVer).</span><span class="sxs-lookup"><span data-stu-id="73ab2-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="73ab2-114">Pour plus d’informations sur l’utilisation de SemVer, consultez la documentation sur le contrôle de [version](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="73ab2-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="73ab2-115">Utilisation de NuGet sans archiver les packages (restauration des packages)</span><span class="sxs-lookup"><span data-stu-id="73ab2-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="73ab2-116">NuGet 1,6 dispose désormais de la prise en charge de première classe pour le flux de travail dans lequel les packages NuGet ne sont pas ajoutés au contrôle de code source, mais ils sont restaurés au moment de la génération s’ils sont manquants.</span><span class="sxs-lookup"><span data-stu-id="73ab2-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="73ab2-117">Pour plus d’informations, consultez la rubrique [utilisation de NuGet sans validation des packages dans le contrôle de code source](../consume-packages/packages-and-source-control.md) .</span><span class="sxs-lookup"><span data-stu-id="73ab2-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="73ab2-118">Modèles d’élément qui installent des packages NuGet</span><span class="sxs-lookup"><span data-stu-id="73ab2-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="73ab2-119">En s’appuyant sur le travail pour prendre en charge le package NuGet préinstallé dans les modèles de projet Visual Studio, NuGet 1,6 ajoute également la prise en charge des modèles d’élément Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73ab2-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="73ab2-120">Les modèles d’élément peuvent avoir des packages NuGet associés qui sont installés lors de l’appel du modèle.</span><span class="sxs-lookup"><span data-stu-id="73ab2-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="73ab2-121">Pour plus d’informations sur la modification d’un modèle de projet/d’élément en vue d’installer des packages NuGet, consultez la rubrique [packages dans les modèles Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="73ab2-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="73ab2-122">Prise en charge de la désactivation des sources de packages</span><span class="sxs-lookup"><span data-stu-id="73ab2-122">Support for disabling package sources</span></span>
<span data-ttu-id="73ab2-123">Lorsque plusieurs sources de package sont configurées, NuGet les recherche pour les packages lors de l’installation d’un package et de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="73ab2-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="73ab2-124">Une source de package déverrouillée pour une raison quelconque peut gravement ralentir NuGet.</span><span class="sxs-lookup"><span data-stu-id="73ab2-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="73ab2-125">Avant NuGet 1,6, vous pouviez supprimer la source du package, mais vous devez vous souvenir des détails relatifs au moment où vous souhaitez l’ajouter de nouveau dans.</span><span class="sxs-lookup"><span data-stu-id="73ab2-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="73ab2-126">NuGet 1,6 permet de désélectionner une source de package pour la désactiver, tout en la conservant.</span><span class="sxs-lookup"><span data-stu-id="73ab2-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Désactivation d’un package](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="73ab2-128">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="73ab2-128">Bug Fixes</span></span>
<span data-ttu-id="73ab2-129">NuGet 1,6 avait un total de 106 éléments de travail corrigés.</span><span class="sxs-lookup"><span data-stu-id="73ab2-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="73ab2-130">95 de celles-ci ont été classées comme des bogues et 10 de ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="73ab2-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="73ab2-131">Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 1,6, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="73ab2-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
