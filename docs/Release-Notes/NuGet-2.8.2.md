---
title: Notes de publication NuGet point 2.8.2 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet point 2.8.2, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet point 2.8.2 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f50bd1f0c981ef293a4d2ff425e0dffbdf58036c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="9eda3-104">Notes de mise à jour de NuGet point 2.8.2</span><span class="sxs-lookup"><span data-stu-id="9eda3-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="9eda3-105">[Notes de publication NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Notes de publication](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="9eda3-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="9eda3-106">NuGet point 2.8.2 a été publiée le 22 mai 2014.</span><span class="sxs-lookup"><span data-stu-id="9eda3-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="9eda3-107">Cette version inclus uniquement les modifications apportées à la ligne de commande de nuget.exe, le package NuGet.Server et autres packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="9eda3-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="9eda3-108">La mise en production n’incluait pas une mise à jour de l’extension Visual Studio ou d’une extension WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="9eda3-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="9eda3-109">Mises à jour importantes</span><span class="sxs-lookup"><span data-stu-id="9eda3-109">Notable Updates</span></span>

<span data-ttu-id="9eda3-110">Les mises à jour plus notables se trouvaient dans la ligne de commande de nuget.exe et package NuGet.Server (pour les flux NuGet auto-hébergé).</span><span class="sxs-lookup"><span data-stu-id="9eda3-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="9eda3-111">Correctifs de bogues importants nuget.exe</span><span class="sxs-lookup"><span data-stu-id="9eda3-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="9eda3-112">NuGet.exe Push échoue et effectue une nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="9eda3-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="9eda3-113">Push de NuGet.exe n’envoie pas correctement les informations d’identification de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="9eda3-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="9eda3-114">Push de NuGet.exe ne suivez redirection temporaire</span><span class="sxs-lookup"><span data-stu-id="9eda3-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="9eda3-115">Correctif de bogue NuGet.Server important</span><span class="sxs-lookup"><span data-stu-id="9eda3-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="9eda3-116">Valeur incorrecte de IsAbsoluteLatestVersion retournée par NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="9eda3-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="9eda3-117">Packages mis à jour</span><span class="sxs-lookup"><span data-stu-id="9eda3-117">Packages Updated</span></span>

<span data-ttu-id="9eda3-118">Les nuget.exe de ligne de commande et les correctifs NuGet.Server sont fournis en tant que mises à jour du package NuGet.</span><span class="sxs-lookup"><span data-stu-id="9eda3-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="9eda3-119">Autres packages de mise à jour avec le point 2.8.2 ainsi a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="9eda3-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="9eda3-120">Voici la liste des packages mis à jour :</span><span class="sxs-lookup"><span data-stu-id="9eda3-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="9eda3-121">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="9eda3-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="9eda3-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="9eda3-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="9eda3-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="9eda3-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="9eda3-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="9eda3-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="9eda3-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (le package, pas l’extension)</span><span class="sxs-lookup"><span data-stu-id="9eda3-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="9eda3-126">Toutes les modifications</span><span class="sxs-lookup"><span data-stu-id="9eda3-126">All Changes</span></span>
<span data-ttu-id="9eda3-127">Comportaient 10 problèmes résolus dans la version.</span><span class="sxs-lookup"><span data-stu-id="9eda3-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="9eda3-128">Pour obtenir la liste complète des travaux les éléments corrigés dans NuGet point 2.8.2, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="9eda3-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
