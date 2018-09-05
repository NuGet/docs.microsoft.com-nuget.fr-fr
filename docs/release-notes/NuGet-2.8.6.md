---
title: Notes de publication de NuGet 2.8.6
description: Notes de publication pour NuGet 2.8.6, notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546489"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="e6fd9-103">Notes de publication de NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="e6fd9-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="e6fd9-104">[Notes de publication de NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [Notes de publication de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="e6fd9-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="e6fd9-105">NuGet 2.8.6 a été publiée le 20 juillet 2015 en tant qu’une mise à jour mineure pour notre 2.8.5 ciblés de VSIX avec certains correctifs et améliorations pour prendre en charge les packages qui peuvent être livrés avec prise en charge pour le modèle de développement Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="e6fd9-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="e6fd9-106">Cette version de l’extension de gestionnaire de package NuGet fournit la prise en charge de Visual Studio 2013 uniquement.</span><span class="sxs-lookup"><span data-stu-id="e6fd9-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="e6fd9-107">Dans cette version, la boîte de dialogue Gestionnaire de Package NuGet avait prend désormais en charge :</span><span class="sxs-lookup"><span data-stu-id="e6fd9-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="e6fd9-108">A introduit le Moniker du Framework cible UAP pour prendre en charge le développement d’applications Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e6fd9-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="e6fd9-109">Points de terminaison NuGet protocol version 3</span><span class="sxs-lookup"><span data-stu-id="e6fd9-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="e6fd9-110">Prise en charge de [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) attribut protocolVersion sur les sources de référentiel.</span><span class="sxs-lookup"><span data-stu-id="e6fd9-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="e6fd9-111">Valeur par défaut est « 2 »</span><span class="sxs-lookup"><span data-stu-id="e6fd9-111">Default value is "2"</span></span>
* <span data-ttu-id="e6fd9-112">Revenir au référentiel distant si une version de package requis n’est pas disponible dans le cache local</span><span class="sxs-lookup"><span data-stu-id="e6fd9-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>