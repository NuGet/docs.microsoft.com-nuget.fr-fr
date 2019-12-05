---
title: Notes de publication de NuGet 5,4
description: Notes de publication de NuGet 5,4, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828407"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="d4fe5-103">Notes de publication de NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="d4fe5-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="d4fe5-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="d4fe5-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d4fe5-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="d4fe5-105">NuGet version</span></span> | <span data-ttu-id="d4fe5-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4fe5-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d4fe5-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d4fe5-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d4fe5-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="d4fe5-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d4fe5-109">Visual Studio 2019 version 16,4</span><span class="sxs-lookup"><span data-stu-id="d4fe5-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d4fe5-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d4fe5-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="d4fe5-111"><sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="d4fe5-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="d4fe5-112">Résumé : nouveautés de 5,4</span><span class="sxs-lookup"><span data-stu-id="d4fe5-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="d4fe5-113">Temps de chargement de solution plus rapide-la surcharge d’exécution du code NuGet pendant la première charge de la solution a été réduite par le biais de NGen partiel pour réduire le coût JIT- [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="d4fe5-114">Nouvelle fonction d’assistance : à partir d’une liste d’ID de package et de versions, récupérez les packages de niveau supérieur probables.</span><span class="sxs-lookup"><span data-stu-id="d4fe5-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="d4fe5-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d4fe5-116">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="d4fe5-116">Issues fixed in this release</span></span>

<span data-ttu-id="d4fe5-117">**Bogues**</span><span class="sxs-lookup"><span data-stu-id="d4fe5-117">**Bugs**</span></span>

* <span data-ttu-id="d4fe5-118">Plug-in : la précision de la journalisation est désactivée sur Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-118">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="d4fe5-119">La suppression d’un plug-in peut parfois lever et faire échouer l’intégralité de l’opération.</span><span class="sxs-lookup"><span data-stu-id="d4fe5-119">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="d4fe5-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="d4fe5-121">Arrêter l’affichage des doublons de version dans la liste des versions autorisées et bloquées dans PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-121">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="d4fe5-122">Le fichier de verrouillage n’est pas généré correctement-l’ordonnancement du Framework ne doit pas avoir d’impact sur la restauration avec lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-122">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="d4fe5-123">La validation LockFile échoue pour les projets avec <RuntimeIdentifiers> défini dans le kit de développement logiciel (SDK) 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-123">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="d4fe5-124">La validation de signature rejettera désormais correctement les signatures avec des horodateurs qui ont 2 valeurs sous le même OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-124">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="d4fe5-125">Mettre à jour la liste de licences- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-125">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="d4fe5-126">**DCR**</span><span class="sxs-lookup"><span data-stu-id="d4fe5-126">**DCRs**</span></span>

* <span data-ttu-id="d4fe5-127">Intégration des fichiers de diagnostic à IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="d4fe5-127">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="d4fe5-128">**[Liste de tous les problèmes résolus dans cette version-5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="d4fe5-128">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
