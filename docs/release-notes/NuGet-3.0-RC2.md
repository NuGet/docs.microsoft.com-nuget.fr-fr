---
title: Notes de publication de NuGet 3,0 RC2
description: Notes de publication de NuGet 3,0 RC2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780274"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="47fd6-103">Notes de publication de NuGet 3,0 RC2</span><span class="sxs-lookup"><span data-stu-id="47fd6-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="47fd6-104">Notes de publication de [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Notes de publication de NuGet 3,0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="47fd6-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="47fd6-105">NuGet 3,0 RC2 a été publié le 3 juin 2015 en tant que version intermédiaire disponible à partir de la Galerie d’extensions Visual Studio 2015 et de [CodePlex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="47fd6-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="47fd6-106">Cette version comporte un certain nombre de correctifs de bogues et d’améliorations des performances que nous avons pensés à libérer avant la version finale de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="47fd6-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="47fd6-107">Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="47fd6-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="47fd6-108">Au total, nous avons clôturé 158 problèmes dans cette version, et vous pouvez consulter la [liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="47fd6-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="47fd6-109">Résumé des principaux problèmes résolus</span><span class="sxs-lookup"><span data-stu-id="47fd6-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="47fd6-110">Appels fréquents de mise à jour du réseau lors de l’actualisation de la fenêtre du gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="47fd6-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="47fd6-111">Défilement différé lors du passage à l’affichage installé dans le gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="47fd6-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="47fd6-112">Les appels réseau doivent être exécutés sur un thread d’arrière-plan</span><span class="sxs-lookup"><span data-stu-id="47fd6-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="47fd6-113">Ajout de la case à cocher « ne pas afficher la fenêtre d’aperçu »</span><span class="sxs-lookup"><span data-stu-id="47fd6-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="47fd6-114">Ajout de la limitation des processus pour réduire l’utilisation du processeur</span><span class="sxs-lookup"><span data-stu-id="47fd6-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="47fd6-115">Amélioration de la gestion des références de bibliothèque de classes portables</span><span class="sxs-lookup"><span data-stu-id="47fd6-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="47fd6-116">Le service de saisie semi-automatique respecte la casse</span><span class="sxs-lookup"><span data-stu-id="47fd6-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="47fd6-117">Mettre à jour pour réintroduire les informations d’identification d’authentification de base</span><span class="sxs-lookup"><span data-stu-id="47fd6-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="47fd6-118">Amélioration de la journalisation des erreurs</span><span class="sxs-lookup"><span data-stu-id="47fd6-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="47fd6-119">Amélioration des messages d’erreur PowerShell lors de l’appel de Update-Package</span><span class="sxs-lookup"><span data-stu-id="47fd6-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="47fd6-120">Téléchargez cette [mise à jour sur l’extension NuGet](https://nuget.codeplex.com/releases/view/615507) à partir de CodePlex et gardez un œil sur [notre blog](http://blog.nuget.org) pour en savoir plus sur la progression et les annonces de NuGet 3,0 !</span><span class="sxs-lookup"><span data-stu-id="47fd6-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>