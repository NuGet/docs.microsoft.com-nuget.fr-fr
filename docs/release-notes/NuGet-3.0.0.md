---
title: Notes de publication NuGet 3.0
description: Notes de publication pour NuGet 3.0.0 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551861"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="ffd80-103">Notes de publication NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="ffd80-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="ffd80-104">[Notes de publication de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [Notes de publication de NuGet 3.1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="ffd80-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="ffd80-105">NuGet 3.0 a été publiée le 20 juillet 2015 comme extension de bundle dans Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ffd80-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="ffd80-106">Nous avons introduit pour fournir cette version avec Visual Studio afin que l’expérience de NuGet 3.0 mise à jour complète serait disponible pour les nouveaux utilisateurs de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ffd80-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="ffd80-107">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ffd80-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="ffd80-108">Nous recommandons aux développeurs qui ont accès à la mise à jour de la galerie Visual Studio à la version la plus récente est disponible, car nous publions une mise à jour peu après la publication de Visual Studio 2015 qui contient la prise en charge pour le développement de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ffd80-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="ffd80-109">Au total, nous avons fermé 240 problèmes dans la version 3.0, et vous pouvez consulter le [la liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="ffd80-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="ffd80-110">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="ffd80-110">Known Issues</span></span>

<span data-ttu-id="ffd80-111">Il existe un nombre de problèmes connus fournies par cette version, et tous ces éléments sont fixes dans notre version 3.1 planifiées pour coïncider avec la version de Windows 10 sur 29 juillet.</span><span class="sxs-lookup"><span data-stu-id="ffd80-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="ffd80-112">Vous êtes en mesure de mettre à jour votre extension de Visual Studio à partir de la galerie sur ou après cette date pour résoudre ces problèmes connus.</span><span class="sxs-lookup"><span data-stu-id="ffd80-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="ffd80-113">Traduction n’est pas fournie pour l’étiquette « Ne plus afficher ce » sur la fenêtre d’aperçu et de l’étiquette « Auteurs » dans la fenêtre de la description du package.</span><span class="sxs-lookup"><span data-stu-id="ffd80-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="ffd80-114">Lorsque vous travaillez sur un projet à l’aide de TFS contrôle de source, NuGet ne peut pas présenter le Gestionnaire de package interface utilisateur si le fichier Nuget.Config est marqué comme étant en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="ffd80-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="ffd80-115">**Solution de contournement** extraire le fichier à partir de TFS.</span><span class="sxs-lookup"><span data-stu-id="ffd80-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="ffd80-116">Texte dans la « barre de redémarrage » dans la fenêtre Powershell de NuGet jaune n’est pas visible lorsque vous utilisez le thème foncé Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ffd80-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="ffd80-117">**Solution de contournement** utiliser le thème clair de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ffd80-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="ffd80-118">Résumé des principaux problèmes résolus</span><span class="sxs-lookup"><span data-stu-id="ffd80-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="ffd80-119">Mise à jour fréquentes réseau appelle au moment de l’actualisation de la fenêtre du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="ffd80-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="ffd80-120">Retardé défilement lors de la modification à installé vue dans le Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="ffd80-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="ffd80-121">Les appels réseau doivent être exécutés sur un thread d’arrière-plan</span><span class="sxs-lookup"><span data-stu-id="ffd80-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="ffd80-122">Case à cocher « Ne pas afficher la fenêtre d’aperçu » ajouté</span><span class="sxs-lookup"><span data-stu-id="ffd80-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="ffd80-123">Ajout de limitation pour réduire l’utilisation du processeur de processus</span><span class="sxs-lookup"><span data-stu-id="ffd80-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="ffd80-124">Gestion des références de bibliothèque de classes portable améliorés</span><span class="sxs-lookup"><span data-stu-id="ffd80-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="ffd80-125">Service de la saisie semi-automatique a été respecte la casse</span><span class="sxs-lookup"><span data-stu-id="ffd80-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="ffd80-126">Mise à jour de réintroduire les informations d’identification de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="ffd80-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="ffd80-127">Journalisation des erreurs améliorée</span><span class="sxs-lookup"><span data-stu-id="ffd80-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="ffd80-128">Messages d’erreur powershell améliorée lors de l’appel de Package de mise à jour</span><span class="sxs-lookup"><span data-stu-id="ffd80-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="ffd80-129">Fixe le lien « En savoir plus sur les Options » pour éviter un blocage sur Windows 10</span><span class="sxs-lookup"><span data-stu-id="ffd80-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="ffd80-130">N’oubliez pas de paramètre de la case à cocher de la version préliminaire</span><span class="sxs-lookup"><span data-stu-id="ffd80-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="ffd80-131">Performances améliorées de regroupement en mettant en cache les résultats sur plusieurs projets dans une solution</span><span class="sxs-lookup"><span data-stu-id="ffd80-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="ffd80-132">Plusieurs Packages peuvent être regroupés en parallèle</span><span class="sxs-lookup"><span data-stu-id="ffd80-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="ffd80-133">Supprimer le package d’installation-forcer la commande</span><span class="sxs-lookup"><span data-stu-id="ffd80-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="ffd80-134">Veuillez garder un œil sur [notre blog](http://blog.nuget.org) pour plus de progression et de publicités que nous préparons fournir la prise en charge pour le développement de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ffd80-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>