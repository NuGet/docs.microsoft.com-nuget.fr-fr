---
title: Notes de publication de NuGet 2.8.2
description: Notes de publication pour NuGet 2.8.2 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551146"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="2aaeb-103">Notes de publication de NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="2aaeb-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="2aaeb-104">[Notes de publication de NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [Notes de publication de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="2aaeb-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="2aaeb-105">NuGet 2.8.2 a été publiée le 22 mai 2014.</span><span class="sxs-lookup"><span data-stu-id="2aaeb-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="2aaeb-106">Cette version inclus uniquement les modifications apportées à la ligne de commande de nuget.exe, le package NuGet.Server et autres packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="2aaeb-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="2aaeb-107">La version n’inclure pas une extension est mise à jour Visual Studio ou WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="2aaeb-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="2aaeb-108">Mises à jour notables</span><span class="sxs-lookup"><span data-stu-id="2aaeb-108">Notable Updates</span></span>

<span data-ttu-id="2aaeb-109">Les mises à jour les plus importants se trouvant dans la ligne de commande de nuget.exe et le package NuGet.Server (pour les flux NuGet auto-hébergé).</span><span class="sxs-lookup"><span data-stu-id="2aaeb-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="2aaeb-110">Correctifs de bogues importants nuget.exe</span><span class="sxs-lookup"><span data-stu-id="2aaeb-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="2aaeb-111">NuGet.exe Push échoue et effectue une nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="2aaeb-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="2aaeb-112">Push de NuGet.exe n’envoie pas correctement les informations d’identification de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="2aaeb-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="2aaeb-113">Push de NuGet.exe ne suivez redirection temporaire</span><span class="sxs-lookup"><span data-stu-id="2aaeb-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="2aaeb-114">Correctif de bogue important NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="2aaeb-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="2aaeb-115">Valeur incorrecte de IsAbsoluteLatestVersion retournée par le NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="2aaeb-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="2aaeb-116">Packages mis à jour</span><span class="sxs-lookup"><span data-stu-id="2aaeb-116">Packages Updated</span></span>

<span data-ttu-id="2aaeb-117">Les correctifs de le NuGet.Server nuget.exe de ligne de commande sont fournis en tant que mises à jour de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="2aaeb-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="2aaeb-118">Autres packages de mise à jour avec la version 2.8.2 ainsi se sont produites.</span><span class="sxs-lookup"><span data-stu-id="2aaeb-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="2aaeb-119">Voici la liste des packages mis à jour :</span><span class="sxs-lookup"><span data-stu-id="2aaeb-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="2aaeb-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="2aaeb-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="2aaeb-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="2aaeb-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="2aaeb-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="2aaeb-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="2aaeb-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="2aaeb-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="2aaeb-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (le package, pas l’extension)</span><span class="sxs-lookup"><span data-stu-id="2aaeb-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="2aaeb-125">Toutes les modifications</span><span class="sxs-lookup"><span data-stu-id="2aaeb-125">All Changes</span></span>
<span data-ttu-id="2aaeb-126">Portaient les 10 problèmes résolus dans la version.</span><span class="sxs-lookup"><span data-stu-id="2aaeb-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="2aaeb-127">Pour obtenir la liste complète des travaux éléments résolus dans NuGet 2.8.2, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="2aaeb-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
