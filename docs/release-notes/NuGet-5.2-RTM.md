---
title: Notes de publication de NuGet 5,2 RTM
description: Notes de publication de NuGet 5,2, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776206"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="d8021-103">Notes de publication de NuGet 5,2</span><span class="sxs-lookup"><span data-stu-id="d8021-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="d8021-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="d8021-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d8021-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="d8021-105">NuGet version</span></span> | <span data-ttu-id="d8021-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8021-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d8021-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d8021-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d8021-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="d8021-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d8021-109">Visual Studio 2019 version 16,2</span><span class="sxs-lookup"><span data-stu-id="d8021-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d8021-110">[2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d8021-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="d8021-111"><sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="d8021-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="d8021-112"><sup>2</sup> Disponible en tant qu’installation facultative avec Visual Studio 2019 avec la charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="d8021-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="d8021-113">Résumé : nouveautés de 5,2</span><span class="sxs-lookup"><span data-stu-id="d8021-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="d8021-114">Correction d’un bogue critique qui provoquait occasionnellement des échecs d’opération NuGet en raison de problèmes de chemin sur Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="d8021-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="d8021-115">Amélioration de la réactivité de l’interface utilisateur lors de l’exploration des packages à l’aide de l’interface utilisateur du gestionnaire de package NuGet dans Visual Studio, particulièrement pour les sources lentes- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="d8021-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="d8021-116">Tonnes de correctifs de fiabilité pour le fichier de verrouillage ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) et le plug-in d’authentification ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210)[, #8198,](https://github.com/NuGet/Home/issues/8198)[#7845](https://github.com/NuGet/Home/issues/7845))</span><span class="sxs-lookup"><span data-stu-id="d8021-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d8021-117">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="d8021-117">Issues fixed in this release</span></span>

<span data-ttu-id="d8021-118">**Bogues**</span><span class="sxs-lookup"><span data-stu-id="d8021-118">**Bugs**</span></span>

* <span data-ttu-id="d8021-119">Perf : console du gestionnaire de package : mise à jour différée de l’interface utilisateur « projet par défaut », valeur sélectionnée de la liste modifiable- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="d8021-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="d8021-120">Performances : améliorations des performances dans l’interface utilisateur PM- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="d8021-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="d8021-121">Perf : délai d’attente de l’interface utilisateur lors de la lecture du projet par défaut dans PMC- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="d8021-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="d8021-122">Perf : [vsfeedback] l’onglet de mise à jour NuGet se fige pour une source de package locale- [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="d8021-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="d8021-123">Plug-ins : NuGet attend le délai d’expiration de la négociation complète si le plug-in ne parvient pas à démarrer ou à se terminer [#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="d8021-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="d8021-124">Plug-ins : améliorer la diagnostic de l’échec de lancement du plug-in- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="d8021-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="d8021-125">Plug-ins : problème avec nuget.exe découverte de plug-ins intégrés- [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="d8021-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="d8021-126">Plug-ins : le fichier cache n’est jamais en lecture [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="d8021-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="d8021-127">Plug-ins : « une tâche a été annulée. »</span><span class="sxs-lookup"><span data-stu-id="d8021-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="d8021-128">erreurs avec le plug-in d’authentification lors de la restauration- [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="d8021-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="d8021-129">Cache de plug-ins non détectable par intermittence sur les plateformes Linux- [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="d8021-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="d8021-130">LockFile : avec ATF, le NU1004 est faux en raison d’une vérification de l’égalité de la version cible du .NET Framework incorrecte- [#8187](https://github.com/NuGet/Home/issues/8187)</span><span class="sxs-lookup"><span data-stu-id="d8021-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="d8021-131">LockFile : indicateur de restauration'--Locked-Mode’non respecté si le fichier de verrouillage est vide ou incorrect [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="d8021-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="d8021-132">LockFile : pas de projets en minuscules avec des noms d’assemblys personnalisés dans les packages verrouiller les fichiers- [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="d8021-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="d8021-133">LockFile : mettre la référence du projet en minuscules dans le fichier de verrouillage- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="d8021-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="d8021-134">Restauration : l’installation d’un package avec signature falsifiée entraîne l’échec de plusieurs tentatives d’installation (avec une sortie répétée)- [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="d8021-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="d8021-135">VS : les options utilisateur de solution ne sont pas désérialisées après la mise à jour NuGet- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="d8021-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="d8021-136">dotnet-List-package dans un projet UnitTest retourne une erreur : [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="d8021-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="d8021-137">Créer un groupe de packages NuGet pour le programme d’installation de VS-correction de certains problèmes d’installation VSIX- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="d8021-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="d8021-138">GeneratePackageOnBuild ne doit pas définir nobuild.</span><span class="sxs-lookup"><span data-stu-id="d8021-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="d8021-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="d8021-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="d8021-140">La nouvelle option « -SymbolPackageFormat snupkg » génère une erreur lorsque le fichier. NuSpec contient un élément de référence d’assembly explicite- [#7638](https://github.com/NuGet/Home/issues/7638)</span><span class="sxs-lookup"><span data-stu-id="d8021-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="d8021-141">NuGet. targets (498, 5) : erreur : impossible de trouver une partie du chemin d’accès'/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="d8021-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="d8021-142">**DCR :**</span><span class="sxs-lookup"><span data-stu-id="d8021-142">**DCR:**</span></span>

* <span data-ttu-id="d8021-143">Ajoutez une propriété MSBuild qui indique que PackageDownload est pris en charge- [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="d8021-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="d8021-144">FrameworkReference supprimer le workflow de dépendance via FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="d8021-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="d8021-145">Mécanisme permettant de fournir des runtime.jsà l’extérieur d’un package- [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="d8021-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="d8021-146">**[Liste de tous les problèmes résolus dans cette version-5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="d8021-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


