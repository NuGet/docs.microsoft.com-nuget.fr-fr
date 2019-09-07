---
title: Notes de publication de NuGet 5,3
description: Notes de publication de NuGet 5,3, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774100"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="cb3bf-103">Notes de publication de NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="cb3bf-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="cb3bf-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="cb3bf-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="cb3bf-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="cb3bf-105">NuGet version</span></span> | <span data-ttu-id="cb3bf-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb3bf-106">Available in Visual Studio version</span></span>| <span data-ttu-id="cb3bf-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="cb3bf-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="cb3bf-108">**5.3.0-preview3**</span><span class="sxs-lookup"><span data-stu-id="cb3bf-108">**5.3.0-preview3**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="cb3bf-109">Visual Studio 2019 version 16,3 Preview 3</span><span class="sxs-lookup"><span data-stu-id="cb3bf-109">Visual Studio 2019 version 16.3 Preview 3</span></span>](https://visualstudio.microsoft.com/vs/preview/) | <span data-ttu-id="cb3bf-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="cb3bf-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="cb3bf-111"><sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="cb3bf-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53-preview-3"></a><span data-ttu-id="cb3bf-112">Résumé : Nouveautés de 5,3 Preview 3</span><span class="sxs-lookup"><span data-stu-id="cb3bf-112">Summary: What's New in 5.3 preview 3</span></span>

* <span data-ttu-id="cb3bf-113">[L’icône de package peut être incorporée dans le package](../reference/msbuild-targets.md#packing-an-icon-image-file), au lieu d’avoir besoin d’une URL externe.</span><span class="sxs-lookup"><span data-stu-id="cb3bf-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="cb3bf-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="cb3bf-115">Sécurité améliorée avec suivi et mise en application SHA pour packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="cb3bf-116">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="cb3bf-116">Issues fixed in this release</span></span>

<span data-ttu-id="cb3bf-117">**Bogues**</span><span class="sxs-lookup"><span data-stu-id="cb3bf-117">**Bugs**</span></span>

* <span data-ttu-id="cb3bf-118">VS : les assemblys sont entièrement Ngen-Ed non partiellement Ngen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-118">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="cb3bf-119">Réduire l’utilisation de la mémoire (se désabonner des événements)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-119">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="cb3bf-120">Le message « Error_UnableToFindProjectInfo » n’est pas correct par programmation- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-120">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="cb3bf-121">Améliorations apportées à NU1403-valider tous les packages, inclure les valeurs SHA attendues/réelles- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-121">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="cb3bf-122">Énumération multiple dans NuGetPackageManager. PreviewUpdatePackagesAsync- [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-122">Multiple enumeration in NuGetPackageManager.PreviewUpdatePackagesAsync - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="cb3bf-123">Restauration de la modification « public-> Internal » dans PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-123">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="cb3bf-124">IVsPackageSourceProvider. GetSources (...) a un comportement d’exception mal défini- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-124">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="cb3bf-125">Rendre publique le constructeur PluginManager- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-125">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="cb3bf-126">Mesures permettant de suivre la fréquence d’actualisation de l’interface utilisateur PM- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-126">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="cb3bf-127">Réduire le nombre d’actualisations de l’interface utilisateur lors de l’installation par le biais de l’interface utilisateur du gestionnaire de package- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-127">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="cb3bf-128">Télémétrie : les valeurs DateTime utilisent des formats spécifiques à la culture- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-128">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="cb3bf-129">Réduire les actualisations de l’interface utilisateur sous l’onglet Parcourir de l’interface utilisateur du gestionnaire de package #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-129">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="cb3bf-130">[Échec du test] Le message « Impossible d’analyser le fichier de configuration » s’affiche à deux reprises [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-130">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="cb3bf-131">Déclencher une erreur NU5037 avec une bonne page de documentation qui explique les correctifs du client (le fichier NuSpec requis est manquant dans le package)- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-131">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="cb3bf-132">La restauration en mode verrouillé échoue quand le RuntimeIdentifier d’un projet est modifié- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-132">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="cb3bf-133">Rendre les paramètres lus dans VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-133">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="cb3bf-134">La régression dans « Ajout des sources NuGet » provoque « le caractère « : », la valeur hexadécimale 0x3A, ne peut pas être inclus dans un nom «erreurs- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-134">Regression in 'Nuget sources add' causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="cb3bf-135">Fournisseurs d’informations d’identification du plug-in NuGet-masquer la fenêtre de processus- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-135">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="cb3bf-136">L’application de PackagePathResolver est un chemin d’accès absolu- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-136">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="cb3bf-137">Réduire les actualisations de l’interface utilisateur dans les onglets installer et mettre à jour de l’interface utilisateur du gestionnaire de package- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-137">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="cb3bf-138">**DCR :**</span><span class="sxs-lookup"><span data-stu-id="cb3bf-138">**DCR:**</span></span>

* <span data-ttu-id="cb3bf-139">Mettre à jour les frameworks Xamarin pour les mapper à netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-139">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="cb3bf-140">Activer la copie du contenu de la « fenêtre d’aperçu » du gestionnaire de package pour l’installation/la mise à jour- [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-140">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="cb3bf-141">Activer la restauration sur les fichiers. proj- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-141">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="cb3bf-142">Introduire `NUGET_NETFX_PLUGIN_PATHS` et`NUGET_NETCORE_PLUGIN_PATHS` pour prendre en charge la configuration des deux en même temps [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-142">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="cb3bf-143">Activer plusieurs versions pour un PackageDownload via l’attribut de version- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-143">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="cb3bf-144">Options Add-SolutionDirectory et-PackageDirectory à NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-144">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

* <span data-ttu-id="cb3bf-145">Activer le Pack NuGet pour qu’il soit déterministe- [#6229](https://github.com/NuGet/Home/issues/6229)</span><span class="sxs-lookup"><span data-stu-id="cb3bf-145">Enable NuGet Pack to be deterministic - [#6229](https://github.com/NuGet/Home/issues/6229)</span></span>

<span data-ttu-id="cb3bf-146">**[Liste de tous les problèmes résolus dans cette version-5,3 Preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="cb3bf-146">**[List of all issues fixed in this release - 5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
