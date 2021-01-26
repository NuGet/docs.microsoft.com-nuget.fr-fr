---
title: Notes de publication de NuGet 2.8.6
description: Notes de publication pour NuGet 2.8.6, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776699"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="388f0-103">Notes de publication de NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="388f0-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="388f0-104">Notes de publication de [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Notes de publication de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="388f0-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="388f0-105">NuGet 2.8.6 a été publié le 20 juillet 2015 en tant que mise à jour mineure de notre extension 2.8.5, avec des correctifs et des améliorations ciblés pour prendre en charge les packages qui peuvent être fournis avec la prise en charge du modèle de développement UWP Windows 10.</span><span class="sxs-lookup"><span data-stu-id="388f0-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="388f0-106">Cette version de l’extension du gestionnaire de package NuGet prend en charge Visual Studio 2013 uniquement.</span><span class="sxs-lookup"><span data-stu-id="388f0-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="388f0-107">Dans cette version, la boîte de dialogue du gestionnaire de package NuGet a été ajoutée pour :</span><span class="sxs-lookup"><span data-stu-id="388f0-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="388f0-108">A introduit le moniker de Framework cible UAP pour prendre en charge le développement d’applications Windows 10.</span><span class="sxs-lookup"><span data-stu-id="388f0-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="388f0-109">Points de terminaison du protocole NuGet version 3</span><span class="sxs-lookup"><span data-stu-id="388f0-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="388f0-110">Prise en charge de [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) attribut protocolVersion sur les sources de référentiel.</span><span class="sxs-lookup"><span data-stu-id="388f0-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="388f0-111">La valeur par défaut est « 2 »</span><span class="sxs-lookup"><span data-stu-id="388f0-111">Default value is "2"</span></span>
* <span data-ttu-id="388f0-112">Revenir au référentiel distant si une version de package requise n’est pas disponible dans le cache local</span><span class="sxs-lookup"><span data-stu-id="388f0-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>