---
title: Notes de publication de NuGet 3,0
description: Notes de publication pour NuGet 3.0.0, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776555"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="8aa9f-103">Notes de publication de NuGet 3,0</span><span class="sxs-lookup"><span data-stu-id="8aa9f-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="8aa9f-104">Notes de publication de [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Notes de publication de NuGet 3,1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="8aa9f-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="8aa9f-105">NuGet 3,0 a été publié le 20 juillet 2015 en tant qu’extension de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="8aa9f-106">Nous avons poussé cette version avec Visual Studio afin que la mise à jour complète de l’expérience 3,0 NuGet soit disponible pour les nouveaux utilisateurs de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="8aa9f-107">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="8aa9f-108">Nous recommandons aux développeurs qui ont accès à la mise à jour de la Galerie Visual Studio d’accéder à la dernière version disponible, car nous publions une mise à jour peu après la publication de Visual Studio 2015 qui contient la prise en charge du développement Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="8aa9f-109">Au total, nous avons clôturé 240 problèmes dans la version 3,0, et vous pouvez consulter la [liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="8aa9f-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="8aa9f-110">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="8aa9f-110">Known Issues</span></span>

<span data-ttu-id="8aa9f-111">Un certain nombre de problèmes connus ont été fournis avec cette version, et tous ces éléments ont été corrigés dans notre version de 3,1 planifiée pour coïncider avec la publication de Windows 10 le 29 juillet.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="8aa9f-112">Vous pouvez mettre à jour votre extension Visual Studio à partir de la Galerie sur ou après cette date pour résoudre ces problèmes connus.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="8aa9f-113">La traduction n’est pas fournie pour l’étiquette « ne plus afficher ce message » dans la fenêtre d’aperçu et l’étiquette « auteurs » dans la fenêtre Description du package.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="8aa9f-114">Lorsque vous travaillez sur un projet à l’aide du contrôle de code source TFS, NuGet ne peut pas présenter l’interface utilisateur du gestionnaire de package si le fichier Nuget.Config est marqué en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="8aa9f-115">**Solution de contournement** Consultez le fichier à partir de TFS.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="8aa9f-116">Le texte de la « barre de redémarrage » jaune dans la fenêtre PowerShell NuGet n’est pas visible lorsque vous utilisez le thème Visual Studio Dark.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="8aa9f-117">**Solution de contournement** Utilisez le thème Visual Studio Light.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="8aa9f-118">Résumé des principaux problèmes résolus</span><span class="sxs-lookup"><span data-stu-id="8aa9f-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="8aa9f-119">Appels fréquents de mise à jour du réseau lors de l’actualisation de la fenêtre du gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="8aa9f-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="8aa9f-120">Défilement différé lors du passage à l’affichage installé dans le gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="8aa9f-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="8aa9f-121">Les appels réseau doivent être exécutés sur un thread d’arrière-plan</span><span class="sxs-lookup"><span data-stu-id="8aa9f-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="8aa9f-122">Ajout de la case à cocher « ne pas afficher la fenêtre d’aperçu »</span><span class="sxs-lookup"><span data-stu-id="8aa9f-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="8aa9f-123">Ajout de la limitation des processus pour réduire l’utilisation du processeur</span><span class="sxs-lookup"><span data-stu-id="8aa9f-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="8aa9f-124">Amélioration de la gestion des références de bibliothèque de classes portables</span><span class="sxs-lookup"><span data-stu-id="8aa9f-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="8aa9f-125">Le service de saisie semi-automatique respecte la casse</span><span class="sxs-lookup"><span data-stu-id="8aa9f-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="8aa9f-126">Mettre à jour pour réintroduire les informations d’identification d’authentification de base</span><span class="sxs-lookup"><span data-stu-id="8aa9f-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="8aa9f-127">Amélioration de la journalisation des erreurs</span><span class="sxs-lookup"><span data-stu-id="8aa9f-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="8aa9f-128">Amélioration des messages d’erreur PowerShell lors de l’appel de Update-Package</span><span class="sxs-lookup"><span data-stu-id="8aa9f-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="8aa9f-129">Correction du lien « en savoir plus sur les options » pour éviter les pannes sur Windows 10</span><span class="sxs-lookup"><span data-stu-id="8aa9f-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="8aa9f-130">Paramètre de case à cocher conserver les préversions</span><span class="sxs-lookup"><span data-stu-id="8aa9f-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="8aa9f-131">Amélioration des performances de collecte grâce à la mise en cache des résultats dans les projets d’une solution</span><span class="sxs-lookup"><span data-stu-id="8aa9f-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="8aa9f-132">Plusieurs packages peuvent être collectés en parallèle</span><span class="sxs-lookup"><span data-stu-id="8aa9f-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="8aa9f-133">Suppression de la commande Install-Package-force</span><span class="sxs-lookup"><span data-stu-id="8aa9f-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="8aa9f-134">Gardez un œil sur [notre blog](http://blog.nuget.org) pour en savoir plus sur la progression et les annonces à mesure que nous nous sommes prêts à fournir un support pour le développement Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8aa9f-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>