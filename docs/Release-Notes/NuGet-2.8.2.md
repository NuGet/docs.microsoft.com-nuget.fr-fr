---
title: Notes de publication NuGet point 2.8.2 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "Notes de publication pour NuGet point 2.8.2, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet point 2.8.2 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="09531-104">Notes de mise à jour de NuGet point 2.8.2</span><span class="sxs-lookup"><span data-stu-id="09531-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="09531-105">[Notes de publication NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Notes de publication](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="09531-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="09531-106">NuGet point 2.8.2 a été publiée le 22 mai 2014.</span><span class="sxs-lookup"><span data-stu-id="09531-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="09531-107">Cette version inclus uniquement les modifications apportées à la ligne de commande de nuget.exe, le package NuGet.Server et autres packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="09531-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="09531-108">La mise en production n’incluait pas une mise à jour de l’extension Visual Studio ou d’une extension WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="09531-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="09531-109">Mises à jour importantes</span><span class="sxs-lookup"><span data-stu-id="09531-109">Notable Updates</span></span>

<span data-ttu-id="09531-110">Les mises à jour plus notables se trouvaient dans la ligne de commande de nuget.exe et package NuGet.Server (pour les flux NuGet auto-hébergé).</span><span class="sxs-lookup"><span data-stu-id="09531-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="09531-111">Correctifs de bogues importants nuget.exe</span><span class="sxs-lookup"><span data-stu-id="09531-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="09531-112">NuGet.exe Push échoue et effectue une nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="09531-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="09531-113">Push de NuGet.exe n’envoie pas correctement les informations d’identification de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="09531-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="09531-114">Push de NuGet.exe ne suivez redirection temporaire</span><span class="sxs-lookup"><span data-stu-id="09531-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="09531-115">Correctif de bogue NuGet.Server important</span><span class="sxs-lookup"><span data-stu-id="09531-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="09531-116">Valeur incorrecte de IsAbsoluteLatestVersion retournée par NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="09531-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="09531-117">Packages mis à jour</span><span class="sxs-lookup"><span data-stu-id="09531-117">Packages Updated</span></span>

<span data-ttu-id="09531-118">Les nuget.exe de ligne de commande et les correctifs NuGet.Server sont fournis en tant que mises à jour du package NuGet.</span><span class="sxs-lookup"><span data-stu-id="09531-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="09531-119">Autres packages de mise à jour avec le point 2.8.2 ainsi a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="09531-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="09531-120">Voici la liste des packages mis à jour :</span><span class="sxs-lookup"><span data-stu-id="09531-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="09531-121">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="09531-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="09531-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="09531-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="09531-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="09531-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="09531-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="09531-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="09531-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (le package, pas l’extension)</span><span class="sxs-lookup"><span data-stu-id="09531-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="09531-126">Toutes les modifications</span><span class="sxs-lookup"><span data-stu-id="09531-126">All Changes</span></span>
<span data-ttu-id="09531-127">Comportaient 10 problèmes résolus dans la version.</span><span class="sxs-lookup"><span data-stu-id="09531-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="09531-128">Pour obtenir la liste complète des travaux les éléments corrigés dans NuGet point 2.8.2, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="09531-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
