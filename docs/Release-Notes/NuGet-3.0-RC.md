---
title: Notes de version de NuGet 3.0 RC | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de version de NuGet 3.0 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 3.0 RC, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="610ca-104">Notes de version de NuGet 3.0 RC</span><span class="sxs-lookup"><span data-stu-id="610ca-104">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="610ca-105">[Notes de mise à jour de NuGet 3.0 bêta](../release-notes/nuget-3.0-beta.md) | [notes de mise à jour de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="610ca-105">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="610ca-106">NuGet 3.0 RC le 29 avril 2015 a été publiée avec la version de Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="610ca-106">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="610ca-107">Cette version comporte un nombre de résolutions de bogues importantes, des améliorations de performances et des mises à jour pour prendre en charge les infrastructures de nouveau.</span><span class="sxs-lookup"><span data-stu-id="610ca-107">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="610ca-108">Il est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="610ca-108">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="610ca-109">Se concentrer sur les performances</span><span class="sxs-lookup"><span data-stu-id="610ca-109">Continued Focus on Performance</span></span>

<span data-ttu-id="610ca-110">Stabilité et performances des requêtes de NuGet continuent de représenter une rubrique à chaud qui se concentre sur.</span><span class="sxs-lookup"><span data-stu-id="610ca-110">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="610ca-111">Avec cette version, vous devez commencer à voir les opérations de recherche très rapide dans le site Web et NuGet UI.</span><span class="sxs-lookup"><span data-stu-id="610ca-111">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="610ca-112">Nous surveillons le service et la façon dont vous utilisez le service afin que nous puissions continuer à paramétrer ces opérations.</span><span class="sxs-lookup"><span data-stu-id="610ca-112">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="610ca-113">Résolu des problèmes significatifs</span><span class="sxs-lookup"><span data-stu-id="610ca-113">Significant Issues Resolved</span></span>

<span data-ttu-id="610ca-114">Afin de stabiliser les clients NuGet, nous avons plusieurs problèmes résolus dans le cadre de cette version.</span><span class="sxs-lookup"><span data-stu-id="610ca-114">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="610ca-115">Voici juste une courte liste de certains des problèmes plus importants résolus :</span><span class="sxs-lookup"><span data-stu-id="610ca-115">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="610ca-116">Dans le cadre de la modification du nom de l’infrastructure de K pour ASP.NET 5, monikers d’infrastructure ont été mis à jour pour gérer dnx et dnxcore [lien](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="610ca-116">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="610ca-117">Ajouté la documentation d’aide à partir des liens dans l’interface utilisateur de Visual Studio [lien](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="610ca-117">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="610ca-118">Une meilleure gestion des références complexes dans `.nuspec` avec références délimitée par des virgules de framework [lien](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="610ca-118">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="610ca-119">Fixe la prise en charge pour les cultures japonais [lien](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="610ca-119">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="610ca-120">Client mis à jour pour autoriser les projets ASP.NET 5 à utiliser les nouveaux points de terminaison v3 [lien](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="610ca-120">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="610ca-121">Dossier de packages de mise à jour pour une meilleure handle avec contrôle de code source [lien](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="610ca-121">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="610ca-122">Fixe la prise en charge pour les packages de satellites [lien](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="610ca-122">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="610ca-123">Correction de la prise en charge pour les fichiers de contenu spécifiques à l’infrastructure [lien](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="610ca-123">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="610ca-124">Révision de présence de GitHub</span><span class="sxs-lookup"><span data-stu-id="610ca-124">GitHub presence overhaul</span></span>

<span data-ttu-id="610ca-125">Nous avons apporté des modifications à notre [de source de référentiels de code sur GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="610ca-125">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="610ca-126">Si vous rencontrez des problèmes avec le client NuGet Visual Studio, les commandes Powershell ou la ligne de commande exécutable vous pouvez connecter ces problèmes et surveiller leur progression sur notre [liste de problèmes de référentiel GitHub accueil](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="610ca-126">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="610ca-127">Nous surveillons problèmes pour la galerie dans notre [GitHub NuGetGallery référentiel](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="610ca-127">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="610ca-128">Tenez-vous informé</span><span class="sxs-lookup"><span data-stu-id="610ca-128">Stay Tuned</span></span>

<span data-ttu-id="610ca-129">Veuillez garder un œil sur [notre blog](http://blog.nuget.org) pour plus d’avancement et les annonces de NuGet 3.0 !</span><span class="sxs-lookup"><span data-stu-id="610ca-129">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>