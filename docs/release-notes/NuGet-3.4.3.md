---
title: Notes de publication de NuGet 3.4.3
description: Notes de publication pour NuGet 3.4.3 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549163"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="ab08c-103">Notes de publication de NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="ab08c-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="ab08c-104">[Notes de publication de NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [Notes de publication de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="ab08c-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="ab08c-105">NuGet 3.4.3 a été publiée le 22 avril 2016 pour résoudre plusieurs problèmes qui ont été identifiées dans les versions 3.4 et ultérieures.</span><span class="sxs-lookup"><span data-stu-id="ab08c-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="ab08c-106">Vous pouvez télécharger l’extension VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="ab08c-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ab08c-107">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="ab08c-107">Updates and Improvements</span></span>

* <span data-ttu-id="ab08c-108">Une meilleure fiabilité de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ab08c-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="ab08c-109">Nous avons résolu certains problèmes dans NuGet qui ont provoqué des incidents dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ab08c-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="ab08c-110">Correctifs</span><span class="sxs-lookup"><span data-stu-id="ab08c-110">Fixes</span></span>

* <span data-ttu-id="ab08c-111">Correction des problèmes d’autorisation avec nuget privé protégé par mot de passe des flux.</span><span class="sxs-lookup"><span data-stu-id="ab08c-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="ab08c-112">Correction d’un problème autour de l’impossibilité de se restaurer à partir de PCL `project.json` avec des runtimes spécifiés.</span><span class="sxs-lookup"><span data-stu-id="ab08c-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="ab08c-113">Certains clients étaient en cours d’exécution sur les défaillances intermittentes lors de l’installation des packages.</span><span class="sxs-lookup"><span data-stu-id="ab08c-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="ab08c-114">Ce problème a maintenant été résolu dans cette version.</span><span class="sxs-lookup"><span data-stu-id="ab08c-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="ab08c-115">Correction d’un problème qui provoquait des échecs de restauration en C / c++ / CLI des projets avec `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ab08c-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="ab08c-116">Certains packages (par ex. ModernHttpClient) où n’est pas décompressé correctement lorsque vous utilisez nuget dans mono.</span><span class="sxs-lookup"><span data-stu-id="ab08c-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="ab08c-117">Ce problème a maintenant été résolu dans cette version.</span><span class="sxs-lookup"><span data-stu-id="ab08c-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="ab08c-118">Pour obtenir la liste complète des correctifs et améliorations dans cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="ab08c-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>