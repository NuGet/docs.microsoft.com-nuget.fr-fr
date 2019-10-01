---
title: Notes de publication de NuGet 5,3
description: Notes de publication de NuGet 5,3, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 683ee7d1bef30d0a7414ec1694a9735d79b2ab45
ms.sourcegitcommit: c529f5944868a0692ca8550b716a73e05df0ccbf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71687889"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="73579-103">Notes de publication de NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="73579-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="73579-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="73579-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="73579-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="73579-105">NuGet version</span></span> | <span data-ttu-id="73579-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73579-106">Available in Visual Studio version</span></span>| <span data-ttu-id="73579-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="73579-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="73579-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="73579-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="73579-109">Visual Studio 2019 version 16,3</span><span class="sxs-lookup"><span data-stu-id="73579-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="73579-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="73579-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="73579-111"><sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="73579-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="73579-112">Résumé : Nouveautés de 5,3</span><span class="sxs-lookup"><span data-stu-id="73579-112">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="73579-113">[L’icône de package peut être incorporée dans le package](../reference/msbuild-targets.md#packing-an-icon-image-file), au lieu d’avoir besoin d’une URL externe.</span><span class="sxs-lookup"><span data-stu-id="73579-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="73579-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="73579-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="73579-115">Sécurité améliorée avec suivi et mise en application SHA pour packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="73579-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="73579-116">Activer la désapprobation des packages NuGet obsolètes/hérités [#2867](https://github.com/NuGet/Home/issues/2867)billet de[blog](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) |   | [docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span><span class="sxs-lookup"><span data-stu-id="73579-116">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="73579-117">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="73579-117">Issues fixed in this release</span></span>

<span data-ttu-id="73579-118">**Bogues**</span><span class="sxs-lookup"><span data-stu-id="73579-118">**Bugs**</span></span>

* <span data-ttu-id="73579-119">Les packages NuGet produits avec le kit de développement logiciel (SDK) 3.0.100-preview9 ne peuvent pas être utilisés par les utilisateurs du SDK 2,2... en fonction de votre fuseau horaire [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="73579-119">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="73579-120">Guillemets dans le chemin d’accès, la cause de l’erreur « `nuget restore` caractères illégaux dans le chemin d’accès » dans [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="73579-120">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="73579-121">VS : les assemblys sont entièrement Ngen-Ed non partiellement Ngen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="73579-121">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="73579-122">Réduire l’utilisation de la mémoire (se désabonner des événements)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="73579-122">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="73579-123">Le message « Error_UnableToFindProjectInfo » n’est pas correct par programmation- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="73579-123">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="73579-124">Améliorations apportées à NU1403-valider tous les packages, inclure les valeurs SHA attendues/réelles- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="73579-124">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="73579-125">Énumération multiple `NuGetPackageManager.PreviewUpdatePackagesAsync`dans  -  [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="73579-125">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="73579-126">Restauration de la modification « public-> Internal » dans PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="73579-126">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="73579-127">IVsPackageSourceProvider. GetSources (...) a un comportement d’exception mal défini- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="73579-127">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="73579-128">Rendre publique le constructeur PluginManager- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="73579-128">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="73579-129">Mesures permettant de suivre la fréquence d’actualisation de l’interface utilisateur PM- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="73579-129">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="73579-130">Réduire le nombre d’actualisations de l’interface utilisateur lors de l’installation par le biais de l’interface utilisateur du gestionnaire de package- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="73579-130">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="73579-131">Télémétrie : les valeurs DateTime utilisent des formats spécifiques à la culture- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="73579-131">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="73579-132">Réduire les actualisations de l’interface utilisateur sous l’onglet Parcourir de l’interface utilisateur du gestionnaire de package #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="73579-132">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="73579-133">[Échec du test] Le message « Impossible d’analyser le fichier de configuration » s’affiche à deux reprises [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="73579-133">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="73579-134">Déclencher une erreur NU5037 avec une bonne page de documentation qui explique les correctifs du client (le fichier NuSpec requis est manquant dans le package)- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="73579-134">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="73579-135">La restauration en mode verrouillé échoue quand le RuntimeIdentifier d’un projet est modifié- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="73579-135">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="73579-136">Rendre les paramètres lus dans VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="73579-136">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="73579-137">La régression `Nuget sources add` dans amène le caractère «  : », la valeur hexadécimale 0x3A, ne peut pas être inclus dans un nom «Errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="73579-137">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="73579-138">Fournisseurs d’informations d’identification du plug-in NuGet-masquer la fenêtre de processus- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="73579-138">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="73579-139">L’application de PackagePathResolver est un chemin d’accès absolu- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="73579-139">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="73579-140">Réduire les actualisations de l’interface utilisateur dans les onglets installer et mettre à jour de l’interface utilisateur du gestionnaire de package- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="73579-140">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="73579-141">**DCR :**</span><span class="sxs-lookup"><span data-stu-id="73579-141">**DCR:**</span></span>

* <span data-ttu-id="73579-142">Mettre à jour les frameworks Xamarin pour les mapper à netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="73579-142">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="73579-143">Activer la copie du contenu de la « fenêtre d’aperçu » du gestionnaire de package pour l’installation/la mise à jour- [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="73579-143">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="73579-144">Activer la restauration sur les fichiers. proj- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="73579-144">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="73579-145">Introduire `NUGET_NETFX_PLUGIN_PATHS` et`NUGET_NETCORE_PLUGIN_PATHS` pour prendre en charge la configuration des deux en même temps [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="73579-145">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="73579-146">Activer plusieurs versions pour un PackageDownload via l’attribut de version- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="73579-146">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="73579-147">Options Add-SolutionDirectory et-PackageDirectory à NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="73579-147">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="73579-148">**[Liste de tous les problèmes résolus dans cette version-5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="73579-148">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
