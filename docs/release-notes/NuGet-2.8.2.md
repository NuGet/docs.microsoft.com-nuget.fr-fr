---
title: Notes de publication de NuGet 2.8.2
description: Notes de publication pour NuGet 2.8.2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780370"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="3e227-103">Notes de publication de NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="3e227-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="3e227-104">Notes de publication de [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Notes de publication de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="3e227-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="3e227-105">NuGet 2.8.2 a été publié le 22 mai 2014.</span><span class="sxs-lookup"><span data-stu-id="3e227-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="3e227-106">Cette version inclut uniquement les modifications apportées à la ligne de commande nuget.exe, au package NuGet. Server et à d’autres packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e227-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="3e227-107">La version n’a pas inclus une extension Visual Studio ou une extension WebMatrix mise à jour.</span><span class="sxs-lookup"><span data-stu-id="3e227-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="3e227-108">Mises à jour notables</span><span class="sxs-lookup"><span data-stu-id="3e227-108">Notable Updates</span></span>

<span data-ttu-id="3e227-109">Les mises à jour les plus notable se trouvaient dans la nuget.exe ligne de commande et le package NuGet. Server (pour les flux NuGet auto-hébergés).</span><span class="sxs-lookup"><span data-stu-id="3e227-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="3e227-110">nuget.exe importantes correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="3e227-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="3e227-111">nuget.exe opération Push échoue et tente à nouvel essai</span><span class="sxs-lookup"><span data-stu-id="3e227-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="3e227-112">nuget.exe Push n’envoie pas correctement les informations d’identification d’authentification de base</span><span class="sxs-lookup"><span data-stu-id="3e227-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="3e227-113">nuget.exe Push ne suivra pas la redirection temporaire</span><span class="sxs-lookup"><span data-stu-id="3e227-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="3e227-114">Important correctif de bogue NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="3e227-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="3e227-115">Valeur incorrecte de IsAbsoluteLatestVersion retournée par NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="3e227-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="3e227-116">Packages mis à jour</span><span class="sxs-lookup"><span data-stu-id="3e227-116">Packages Updated</span></span>

<span data-ttu-id="3e227-117">Les correctifs de ligne de commande nuget.exe et NuGet. Server sont fournis en tant que mises à jour de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e227-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="3e227-118">D’autres packages ont également été mis à jour avec 2.8.2.</span><span class="sxs-lookup"><span data-stu-id="3e227-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="3e227-119">Voici la liste des packages mis à jour :</span><span class="sxs-lookup"><span data-stu-id="3e227-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="3e227-120">NuGet. Core</span><span class="sxs-lookup"><span data-stu-id="3e227-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="3e227-121">NuGet. CommandLine</span><span class="sxs-lookup"><span data-stu-id="3e227-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="3e227-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="3e227-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="3e227-123">NuGet. Build</span><span class="sxs-lookup"><span data-stu-id="3e227-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="3e227-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (le package, pas l’extension)</span><span class="sxs-lookup"><span data-stu-id="3e227-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="3e227-125">Toutes les modifications</span><span class="sxs-lookup"><span data-stu-id="3e227-125">All Changes</span></span>
<span data-ttu-id="3e227-126">10 problèmes ont été résolus dans la version.</span><span class="sxs-lookup"><span data-stu-id="3e227-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="3e227-127">Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2.8.2, consultez le [suivi des problèmes NuGet pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="3e227-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
