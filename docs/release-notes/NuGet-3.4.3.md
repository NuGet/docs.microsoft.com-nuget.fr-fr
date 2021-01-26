---
title: Notes de publication de NuGet 3.4.3
description: Notes de publication pour NuGet 3.4.3, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776468"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="6ff87-103">Notes de publication de NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="6ff87-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="6ff87-104">Notes de publication de [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Notes de publication de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="6ff87-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="6ff87-105">NuGet 3.4.3 a été publié le 22 avril 2016 pour résoudre plusieurs problèmes identifiés dans le 3,4 et dans les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="6ff87-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="6ff87-106">Vous pouvez télécharger les versions VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="6ff87-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="6ff87-107">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="6ff87-107">Updates and Improvements</span></span>

* <span data-ttu-id="6ff87-108">Amélioration de la fiabilité de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6ff87-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="6ff87-109">Nous avons résolu certains problèmes dans NuGet qui provoquaient des blocages dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6ff87-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="6ff87-110">Correctifs</span><span class="sxs-lookup"><span data-stu-id="6ff87-110">Fixes</span></span>

* <span data-ttu-id="6ff87-111">Correction de certains problèmes d’autorisation avec les flux NuGet privés protégés par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="6ff87-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="6ff87-112">Résolution d’un problème lié à l’impossibilité de restaurer les bibliothèques de classes portable à partir de `project.json` avec des runtimes spécifiés.</span><span class="sxs-lookup"><span data-stu-id="6ff87-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="6ff87-113">Certains clients étaient confrontés à des défaillances intermittentes lors de l’installation des packages.</span><span class="sxs-lookup"><span data-stu-id="6ff87-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="6ff87-114">Ce problème a été résolu dans cette version.</span><span class="sxs-lookup"><span data-stu-id="6ff87-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="6ff87-115">Correction d’un problème qui provoquait des échecs de restauration dans les projets C++/CLI avec `project.json` .</span><span class="sxs-lookup"><span data-stu-id="6ff87-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="6ff87-116">Certains packages (par exemple, ModernHttpClient) où ne sont pas décompressés correctement lorsque vous utilisez NuGet en mono.</span><span class="sxs-lookup"><span data-stu-id="6ff87-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="6ff87-117">Ce problème a été résolu dans cette version.</span><span class="sxs-lookup"><span data-stu-id="6ff87-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="6ff87-118">Pour obtenir la liste complète des correctifs et améliorations de cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="6ff87-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>