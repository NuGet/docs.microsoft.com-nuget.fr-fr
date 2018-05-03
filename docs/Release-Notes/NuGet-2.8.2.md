---
title: Notes de mise à jour de NuGet point 2.8.2
description: Notes de publication pour NuGet point 2.8.2, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="9c384-103">Notes de mise à jour de NuGet point 2.8.2</span><span class="sxs-lookup"><span data-stu-id="9c384-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="9c384-104">[Notes de publication NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Notes de publication](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="9c384-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="9c384-105">NuGet point 2.8.2 a été publiée le 22 mai 2014.</span><span class="sxs-lookup"><span data-stu-id="9c384-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="9c384-106">Cette version inclus uniquement les modifications apportées à la ligne de commande de nuget.exe, le package NuGet.Server et autres packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="9c384-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="9c384-107">La mise en production n’incluait pas une mise à jour de l’extension Visual Studio ou d’une extension WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="9c384-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="9c384-108">Mises à jour importantes</span><span class="sxs-lookup"><span data-stu-id="9c384-108">Notable Updates</span></span>

<span data-ttu-id="9c384-109">Les mises à jour plus notables se trouvaient dans la ligne de commande de nuget.exe et package NuGet.Server (pour les flux NuGet auto-hébergé).</span><span class="sxs-lookup"><span data-stu-id="9c384-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="9c384-110">Correctifs de bogues importants nuget.exe</span><span class="sxs-lookup"><span data-stu-id="9c384-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="9c384-111">NuGet.exe Push échoue et effectue une nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="9c384-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="9c384-112">Push de NuGet.exe n’envoie pas correctement les informations d’identification de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="9c384-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="9c384-113">Push de NuGet.exe ne suivez redirection temporaire</span><span class="sxs-lookup"><span data-stu-id="9c384-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="9c384-114">Correctif de bogue NuGet.Server important</span><span class="sxs-lookup"><span data-stu-id="9c384-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="9c384-115">Valeur incorrecte de IsAbsoluteLatestVersion retournée par NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="9c384-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="9c384-116">Packages mis à jour</span><span class="sxs-lookup"><span data-stu-id="9c384-116">Packages Updated</span></span>

<span data-ttu-id="9c384-117">Les nuget.exe de ligne de commande et les correctifs NuGet.Server sont fournis en tant que mises à jour du package NuGet.</span><span class="sxs-lookup"><span data-stu-id="9c384-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="9c384-118">Autres packages de mise à jour avec le point 2.8.2 ainsi a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="9c384-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="9c384-119">Voici la liste des packages mis à jour :</span><span class="sxs-lookup"><span data-stu-id="9c384-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="9c384-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="9c384-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="9c384-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="9c384-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="9c384-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="9c384-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="9c384-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="9c384-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="9c384-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (le package, pas l’extension)</span><span class="sxs-lookup"><span data-stu-id="9c384-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="9c384-125">Toutes les modifications</span><span class="sxs-lookup"><span data-stu-id="9c384-125">All Changes</span></span>
<span data-ttu-id="9c384-126">Comportaient 10 problèmes résolus dans la version.</span><span class="sxs-lookup"><span data-stu-id="9c384-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="9c384-127">Pour obtenir la liste complète des travaux les éléments corrigés dans NuGet point 2.8.2, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="9c384-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
