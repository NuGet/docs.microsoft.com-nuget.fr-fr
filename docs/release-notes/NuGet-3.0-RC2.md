---
title: Notes de publication de NuGet 3.0 RC2
description: Notes de publication pour NuGet 3.0 RC2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545819"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="8d569-103">Notes de publication de NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="8d569-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="8d569-104">[Notes de version RC de NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [Notes de publication de NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="8d569-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="8d569-105">NuGet 3.0 RC2 a été publiée le 3 juin 2015 en tant qu’une version intermédiaire à partir de la galerie d’extensions Visual Studio 2015 et [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="8d569-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="8d569-106">Cette version comporte un nombre importants de correctifs de bogues et améliorations des performances que nous avons pensé étaient importantes de mise à jour avant la version de Visual Studio 2015 terminée.</span><span class="sxs-lookup"><span data-stu-id="8d569-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="8d569-107">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8d569-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="8d569-108">Au total, nous avons fermé 158 problèmes dans cette version, et vous pouvez consulter le [la liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="8d569-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="8d569-109">Résumé des principaux problèmes résolus</span><span class="sxs-lookup"><span data-stu-id="8d569-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="8d569-110">Mise à jour fréquentes réseau appelle au moment de l’actualisation de la fenêtre du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="8d569-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="8d569-111">Retardé défilement lors de la modification à installé vue dans le Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="8d569-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="8d569-112">Les appels réseau doivent être exécutés sur un thread d’arrière-plan</span><span class="sxs-lookup"><span data-stu-id="8d569-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="8d569-113">Case à cocher « Ne pas afficher la fenêtre d’aperçu » ajouté</span><span class="sxs-lookup"><span data-stu-id="8d569-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="8d569-114">Ajout de limitation pour réduire l’utilisation du processeur de processus</span><span class="sxs-lookup"><span data-stu-id="8d569-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="8d569-115">Gestion des références de bibliothèque de classes portable améliorés</span><span class="sxs-lookup"><span data-stu-id="8d569-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="8d569-116">Service de la saisie semi-automatique a été respecte la casse</span><span class="sxs-lookup"><span data-stu-id="8d569-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="8d569-117">Mise à jour de réintroduire les informations d’identification de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="8d569-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="8d569-118">Journalisation des erreurs améliorée</span><span class="sxs-lookup"><span data-stu-id="8d569-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="8d569-119">Messages d’erreur powershell améliorée lors de l’appel de Package de mise à jour</span><span class="sxs-lookup"><span data-stu-id="8d569-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="8d569-120">Téléchargez ce [mettre à jour à l’extension NuGet](https://nuget.codeplex.com/releases/view/615507) à partir de Codeplex et gardez un œil [notre blog](http://blog.nuget.org) pour plus de progression et de publicités pour NuGet 3.0 !</span><span class="sxs-lookup"><span data-stu-id="8d569-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>