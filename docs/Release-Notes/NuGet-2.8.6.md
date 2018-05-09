---
title: Notes de mise à jour de NuGet 2.8.6
description: Notes de publication pour NuGet 2.8.6, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="891b6-103">Notes de mise à jour de NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="891b6-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="891b6-104">[Notes de publication NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Notes de publication](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="891b6-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="891b6-105">NuGet 2.8.6 a été publiée le 20 juillet 2015 comme une mise à jour mineure notre 2.8.5 VSIX avec certains ciblés correctifs et améliorations pour prendre en charge les packages qui peuvent être livrés avec prise en charge pour le modèle de développement Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="891b6-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="891b6-106">Cette version de l’extension de gestionnaire de package NuGet fournit la prise en charge de Visual Studio 2013 uniquement.</span><span class="sxs-lookup"><span data-stu-id="891b6-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="891b6-107">Dans cette version, la boîte de dialogue Gestionnaire de Package NuGet comportait prend désormais en charge :</span><span class="sxs-lookup"><span data-stu-id="891b6-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="891b6-108">A introduit le Moniker du Framework cible UAP pour prendre en charge le développement d’applications Windows 10.</span><span class="sxs-lookup"><span data-stu-id="891b6-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="891b6-109">Points de terminaison NuGet protocol version 3</span><span class="sxs-lookup"><span data-stu-id="891b6-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="891b6-110">Prise en charge de [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) attribut protocolVersion sur des sources de référentiel.</span><span class="sxs-lookup"><span data-stu-id="891b6-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="891b6-111">Valeur par défaut est « 2 »</span><span class="sxs-lookup"><span data-stu-id="891b6-111">Default value is "2"</span></span>
* <span data-ttu-id="891b6-112">Retour à l’espace de stockage à distance, si une version de package nécessaire n’est pas disponible dans le cache local</span><span class="sxs-lookup"><span data-stu-id="891b6-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>