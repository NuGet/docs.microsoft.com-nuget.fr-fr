---
title: "Notes de mise à jour de NuGet 3.0 RC2 | Documents Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de version, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR de NuGet 3.0 RC2."
keywords: "Notes de publication NuGet 3.0 RC2, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67299408170ae3c3676c2866bec2945b41ad4184
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="a7243-104">Notes de mise à jour de NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="a7243-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="a7243-105">[Notes de version RC de NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [Notes de version de NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="a7243-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="a7243-106">NuGet 3.0 RC2 3 juin 2015 a été publiée en tant qu’une version intermédiaire à partir de la galerie d’extensions Visual Studio 2015 et [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="a7243-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="a7243-107">Cette version comporte un nombre importants de correctifs de bogues et des améliorations de performances, il nous semble ont été importantes de mise à jour avant la version de Visual Studio 2015 terminée.</span><span class="sxs-lookup"><span data-stu-id="a7243-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="a7243-108">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a7243-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="a7243-109">Au total, nous avons fermé 158 problèmes dans cette version, et vous pouvez passer en revue les [la liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="a7243-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="a7243-110">Résumé des principaux problèmes résolus</span><span class="sxs-lookup"><span data-stu-id="a7243-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="a7243-111">Mise à jour fréquentes réseau appelle au moment de l’actualisation de la fenêtre du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="a7243-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="a7243-112">Retardé de défilement lorsque la modification à installé vue dans le Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="a7243-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="a7243-113">Les appels réseau doivent être exécutés sur un thread d’arrière-plan</span><span class="sxs-lookup"><span data-stu-id="a7243-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="a7243-114">Case à cocher « Ne pas afficher la fenêtre d’aperçu » ajouté</span><span class="sxs-lookup"><span data-stu-id="a7243-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="a7243-115">Processus ajouté la limitation pour réduire l’utilisation du processeur</span><span class="sxs-lookup"><span data-stu-id="a7243-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="a7243-116">Une référence de bibliothèque de classes portable gestion améliorée</span><span class="sxs-lookup"><span data-stu-id="a7243-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="a7243-117">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="a7243-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="a7243-118">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="a7243-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="a7243-119">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="a7243-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="a7243-120">La saisie semi-automatique service a été respectant la casse</span><span class="sxs-lookup"><span data-stu-id="a7243-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="a7243-121">Mise à jour pour rétablir les informations d’identification de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="a7243-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="a7243-122">Journalisation des erreurs améliorées</span><span class="sxs-lookup"><span data-stu-id="a7243-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="a7243-123">Powershell amélioré les messages d’erreur lors de l’appel de Package de mise à jour</span><span class="sxs-lookup"><span data-stu-id="a7243-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="a7243-124">Téléchargez ce [mettre à jour à l’extension NuGet](https://nuget.codeplex.com/releases/view/615507) à partir de Codeplex et gardez un œil [notre blog](http://blog.nuget.org) pour plus d’avancement et les annonces de NuGet 3.0 !</span><span class="sxs-lookup"><span data-stu-id="a7243-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>