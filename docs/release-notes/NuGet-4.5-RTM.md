---
title: Notes de publication de NuGet 4.5 RTM
description: Notes de publication pour NuGet 4.5 RTM, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432502"
---
# <a name="nuget-45-release-notes"></a><span data-ttu-id="89913-103">Notes de publication de NuGet 4.5</span><span class="sxs-lookup"><span data-stu-id="89913-103">NuGet 4.5 Release Notes</span></span>

<span data-ttu-id="89913-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="89913-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-450"></a><span data-ttu-id="89913-105">Résumé : Nouveautés de la version 4.5.0</span><span class="sxs-lookup"><span data-stu-id="89913-105">Summary: What's New in 4.5.0</span></span>

## <a name="summary-whats-new-in-452"></a><span data-ttu-id="89913-106">Résumé : Nouveautés de la version 4.5.2</span><span class="sxs-lookup"><span data-stu-id="89913-106">Summary: What's New in 4.5.2</span></span>

* <span data-ttu-id="89913-107">Correctif de sécurité : Les autorisations sur les fichiers créés dans ~/.nuget sont trop ouvertes [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="89913-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-453"></a><span data-ttu-id="89913-108">Résumé : Nouveautés de la version 4.5.3</span><span class="sxs-lookup"><span data-stu-id="89913-108">Summary: What's New in 4.5.3</span></span>

* <span data-ttu-id="89913-109">Correctif de sécurité : Les fichiers dans les NUPKG peuvent avoir un chemin relatif au-dessus du répertoire NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="89913-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="89913-110">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="89913-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="89913-111">Problèmes liés à .NET Standard 2.0 avec .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="89913-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="89913-112">.NET Standard et ses outils ont été conçus de façon à ce que les projets qui ciblent le .NET Framework 4.6.1 puissent consommer les projets et les packages NuGet ciblant .NET Standard 2.0 ou antérieur.</span><span class="sxs-lookup"><span data-stu-id="89913-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="89913-113">[Ce document](https://github.com/dotnet/standard/issues/481) récapitule les problèmes liés à ce scénario et propose des solutions de contournement que vous pouvez déployer avec les outils actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="89913-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="89913-114">Impossible d’afficher, d’ajouter ou de mettre à jour DotNetCLITools à l’aide du Gestionnaire de package NuGet</span><span class="sxs-lookup"><span data-stu-id="89913-114">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="89913-115">Problème</span><span class="sxs-lookup"><span data-stu-id="89913-115">Issue</span></span>

<span data-ttu-id="89913-116">Le Gestionnaire de package NuGet ne s’affiche pas et n’autorise pas l’ajout/mise à jour de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="89913-116">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="89913-117">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="89913-117">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="89913-118">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="89913-118">Workaround</span></span>

<span data-ttu-id="89913-119">Vous devez modifier manuellement DotNetCLIToolReferences dans votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="89913-119">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="89913-120">Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes</span><span class="sxs-lookup"><span data-stu-id="89913-120">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="89913-121">Problème</span><span class="sxs-lookup"><span data-stu-id="89913-121">Issue</span></span>

<span data-ttu-id="89913-122">Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89913-122">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="89913-123">Cela se produit quand vous utilisez PackageReferences comme format de gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="89913-123">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="89913-124">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="89913-124">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="89913-125">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="89913-125">Workaround</span></span>

<span data-ttu-id="89913-126">Effectuez une restauration manuelle.</span><span class="sxs-lookup"><span data-stu-id="89913-126">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="89913-127">Un package dans un projet .NET Core qui contient un assembly avec une signature non valide peut déclencher une boucle de restauration infinie</span><span class="sxs-lookup"><span data-stu-id="89913-127">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="89913-128">Problème</span><span class="sxs-lookup"><span data-stu-id="89913-128">Issue</span></span>

<span data-ttu-id="89913-129">Parfois, quand vous utilisez un package qui contient un assembly avec une signature non valide ou quand la version du package est définie avec le symbole « DateTime », la restauration automatique du package s’exécute dans une boucle infinie ([dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)).</span><span class="sxs-lookup"><span data-stu-id="89913-129">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="89913-130">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="89913-130">Workaround</span></span>

<span data-ttu-id="89913-131">Il n’existe aucune solution de contournement pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="89913-131">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="89913-132">Problèmes résolus dans NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="89913-132">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="89913-133">Pour plus d’informations sur les problèmes résolus dans NuGet 4.4 RTM, consultez les [Notes de publication de NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md).</span><span class="sxs-lookup"><span data-stu-id="89913-133">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="89913-134">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="89913-134">Features</span></span>

- <span data-ttu-id="89913-135">Désactiver l’envoi (push) automatique du package de symboles - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="89913-135">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="89913-136">Bogues</span><span class="sxs-lookup"><span data-stu-id="89913-136">Bugs</span></span>

- <span data-ttu-id="89913-137">[Régression] dans 15.5p1 : Portable0.0 est ignoré - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="89913-137">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="89913-138">Les ressources des packages sont manquantes après restauration - [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="89913-138">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="89913-139">Les fournisseurs d’informations d’identification de plug-in ne fonctionnent pas avec les URI contenant des espaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="89913-139">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="89913-140">Si la restauration de package a échoué, l’erreur devrait s’imprimer en sortie, même si le niveau de détail minimal est activé - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="89913-140">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="89913-141">dotnet</span><span class="sxs-lookup"><span data-stu-id="89913-141">dotnet</span></span>
  - <span data-ttu-id="89913-142">dotnetcore restore au niveau de la solution ne suit pas ProjectReference avec ReferenceOutputAssembly false provoquant des échecs de génération aléatoires - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="89913-142">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="89913-143">La saisie semi-automatique dans PMC fonctionne correctement avec les méthodes d’objet - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="89913-143">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="89913-144">La restauration de nuget.exe échoue avec l’ensemble d’outils de Visual Studio 2015 - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="89913-144">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="89913-145">Performances - l’instanciation de pmc est coûteuse dans vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="89913-145">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="89913-146">Lenteur d’obtention des informations de dépendances en cas de lenteur de la connexion - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="89913-146">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="89913-147">uninstall-package w/ -RemoveDependencies échoue si plusieurs packages partagent une dépendance commune - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="89913-147">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="89913-148">Finalisation de NuGet.Core.nupkg pour la publication - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="89913-148">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="89913-149">Le pack NuGet résout un ID de dépendance à partir du nom de répertoire quand -IncludeProjectReferences est utilisé pour csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="89913-149">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="89913-150">L’initialiseur de type pour « NuGet.ProxyCache » a levé une exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="89913-150">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="89913-151">Problème de performances de nuget restore avec kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="89913-151">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="89913-152">L’interface utilisateur du client n’affiche ni erreur ni avertissement quand la recherche est en avance par rapport aux objets blob d’inscription - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="89913-152">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="89913-153">Get-Packages -Updates génère une requête incorrecte - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="89913-153">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="89913-154">Liens vers les problèmes GitHub corrigés dans RTM 4.5</span><span class="sxs-lookup"><span data-stu-id="89913-154">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="89913-155">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="89913-155">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
