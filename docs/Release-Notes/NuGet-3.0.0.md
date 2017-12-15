---
title: Notes de version de NuGet 3.0 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8ad13a67-9348-4f04-8f8b-b8f4a0b2c6df
description: "Notes de publication pour NuGet 3.0.0, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 3.0.0 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 95c4bf92f5eeb676fa6bcc3b7bcbf191efa9cb9e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="0791d-104">Notes de version 3.0 de NuGet</span><span class="sxs-lookup"><span data-stu-id="0791d-104">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="0791d-105">[Notes de mise à jour de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Notes de publication](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="0791d-105">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="0791d-106">NuGet 3.0 a été publiée le 20 juillet 2015 comme extension de regroupement dans Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0791d-106">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="0791d-107">Nous avons envoyé à fournir cette version avec Visual Studio afin que l’expérience de NuGet 3.0 mise à jour terminée, ne serait disponible pour les nouveaux utilisateurs de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0791d-107">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="0791d-108">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0791d-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="0791d-109">Nous vous recommandons des développeurs qui ont accès à la mise à jour de la galerie Visual Studio à la version la plus récente est disponible, comme nous publions une mise à jour peu après la publication de Visual Studio 2015 qui contient la prise en charge pour le développement de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0791d-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="0791d-110">Au total, nous avons fermé 240 problèmes dans la version 3.0, et vous pouvez passer en revue les [la liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="0791d-110">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="0791d-111">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="0791d-111">Known Issues</span></span>

<span data-ttu-id="0791d-112">Un certain nombre de problèmes connus fourni avec cette version, et tous ces éléments ont été corrigés dans notre version 3.1 planifiées pour coïncider avec la version de Windows 10 sur 29 juillet.</span><span class="sxs-lookup"><span data-stu-id="0791d-112">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="0791d-113">Vous ne pourrez pas mettre à jour votre extension de Visual Studio à partir de la galerie sur ou après cette date pour résoudre ces problèmes connus.</span><span class="sxs-lookup"><span data-stu-id="0791d-113">You will be able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="0791d-114">Traduction n’est pas fournie pour l’étiquette « Ne plus afficher cette boîte de dialogue » dans la fenêtre d’aperçu et de l’étiquette « Auteurs » dans la fenêtre de la description du package.</span><span class="sxs-lookup"><span data-stu-id="0791d-114">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="0791d-115">Lorsque vous travaillez sur un projet à l’aide de TFS contrôle de source, NuGet ne peuvent pas présenter le Gestionnaire de package interface utilisateur si le fichier Nuget.Config est marqué comme étant en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="0791d-115">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="0791d-116">**Solution de contournement** à extraire le fichier à partir de TFS.</span><span class="sxs-lookup"><span data-stu-id="0791d-116">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="0791d-117">Texte dans le jaune « redémarrage barre » dans la fenêtre NuGet Powershell n’est pas visible lorsque vous utilisez le thème sombre de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0791d-117">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="0791d-118">**Solution de contournement** utiliser ce thème clair Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0791d-118">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="0791d-119">Résumé des principaux problèmes résolus</span><span class="sxs-lookup"><span data-stu-id="0791d-119">Summary of top issues resolved</span></span>

* [<span data-ttu-id="0791d-120">Mise à jour fréquentes réseau appelle au moment de l’actualisation de la fenêtre du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="0791d-120">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="0791d-121">Retardé de défilement lorsque la modification à installé vue dans le Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="0791d-121">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="0791d-122">Les appels réseau doivent être exécutés sur un thread d’arrière-plan</span><span class="sxs-lookup"><span data-stu-id="0791d-122">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="0791d-123">Case à cocher « Ne pas afficher la fenêtre d’aperçu » ajouté</span><span class="sxs-lookup"><span data-stu-id="0791d-123">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="0791d-124">Processus ajouté la limitation pour réduire l’utilisation du processeur</span><span class="sxs-lookup"><span data-stu-id="0791d-124">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="0791d-125">Une référence de bibliothèque de classes portable gestion améliorée</span><span class="sxs-lookup"><span data-stu-id="0791d-125">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="0791d-126">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="0791d-126">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="0791d-127">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="0791d-127">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="0791d-128">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="0791d-128">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="0791d-129">La saisie semi-automatique service a été respectant la casse</span><span class="sxs-lookup"><span data-stu-id="0791d-129">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="0791d-130">Mise à jour pour rétablir les informations d’identification de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="0791d-130">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="0791d-131">Journalisation des erreurs améliorées</span><span class="sxs-lookup"><span data-stu-id="0791d-131">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="0791d-132">Powershell amélioré les messages d’erreur lors de l’appel de Package de mise à jour</span><span class="sxs-lookup"><span data-stu-id="0791d-132">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="0791d-133">Fixe le lien « En savoir plus sur les Options » pour empêcher le blocage sur Windows 10</span><span class="sxs-lookup"><span data-stu-id="0791d-133">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="0791d-134">N’oubliez pas de paramètre de la case à cocher de la version préliminaire</span><span class="sxs-lookup"><span data-stu-id="0791d-134">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="0791d-135">Performances améliorées de collecte en mettant en cache les résultats pour des projets d’une solution</span><span class="sxs-lookup"><span data-stu-id="0791d-135">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="0791d-136">Plusieurs Packages peuvent être regroupés en parallèle</span><span class="sxs-lookup"><span data-stu-id="0791d-136">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="0791d-137">Supprimer le package d’installation-forcer la commande</span><span class="sxs-lookup"><span data-stu-id="0791d-137">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="0791d-138">Veuillez garder un œil sur [notre blog](http://blog.nuget.org) de progression et des annonces plus que nous se préparer à fournir la prise en charge pour le développement de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0791d-138">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>