---
title: Notes de publication de NuGet 5,3
description: Notes de publication de NuGet 5,3, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: ca71c5b9ef546f3ea92e55763d5059466ac3a930
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813752"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="8cfb8-103">Notes de publication de NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="8cfb8-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="8cfb8-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="8cfb8-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="8cfb8-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="8cfb8-105">NuGet version</span></span> | <span data-ttu-id="8cfb8-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8cfb8-106">Available in Visual Studio version</span></span>| <span data-ttu-id="8cfb8-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="8cfb8-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="8cfb8-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="8cfb8-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="8cfb8-109">Visual Studio 2019 version 16,3</span><span class="sxs-lookup"><span data-stu-id="8cfb8-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="8cfb8-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="8cfb8-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="8cfb8-111">**5.3.1**</span><span class="sxs-lookup"><span data-stu-id="8cfb8-111">**5.3.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="8cfb8-112">Version 16.3.6 de Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="8cfb8-112">Visual Studio 2019 version 16.3.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="8cfb8-113">Version future : 3.0.101</span><span class="sxs-lookup"><span data-stu-id="8cfb8-113">Future version: 3.0.101</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<span data-ttu-id="8cfb8-114"><sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="8cfb8-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="8cfb8-115">Résumé : nouveautés de 5,3</span><span class="sxs-lookup"><span data-stu-id="8cfb8-115">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="8cfb8-116">[L’icône de package peut être incorporée dans le package](../reference/msbuild-targets.md#packing-an-icon-image-file), au lieu d’avoir besoin d’une URL externe.</span><span class="sxs-lookup"><span data-stu-id="8cfb8-116">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="8cfb8-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="8cfb8-118">Sécurité améliorée avec suivi et mise en application SHA pour packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-118">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="8cfb8-119">Activer la désapprobation des packages NuGet obsolètes/hérités [#2867](https://github.com/NuGet/Home/issues/2867) | billet de [blog](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](../nuget-org/deprecate-packages.md)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-119">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](../nuget-org/deprecate-packages.md)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="8cfb8-120">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="8cfb8-120">Issues fixed in this release</span></span>

<span data-ttu-id="8cfb8-121">**Bogues**</span><span class="sxs-lookup"><span data-stu-id="8cfb8-121">**Bugs**</span></span>

* <span data-ttu-id="8cfb8-122">Les packages NuGet produits avec le kit de développement logiciel (SDK) 3.0.100-preview9 ne peuvent pas être utilisés par les utilisateurs du SDK 2,2... en fonction de votre fuseau horaire [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-122">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="8cfb8-123">Guillemets « les caractères non conformes dans le chemin d’accès sont à l’origine de l’erreur «caractères illégaux dans le chemin » dans `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-123">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="8cfb8-124">VS : les assemblys sont entièrement Ngen-Ed non partiellement Ngen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-124">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="8cfb8-125">Réduire l’utilisation de la mémoire (se désabonner des événements)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-125">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="8cfb8-126">Le message « Error_UnableToFindProjectInfo » n’est pas correct par programmation- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-126">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="8cfb8-127">Améliorations apportées à NU1403-valider tous les packages, inclure les valeurs SHA attendues/réelles- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-127">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="8cfb8-128">Énumération multiple dans `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-128">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="8cfb8-129">Restauration de la modification « public-> Internal » dans PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-129">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="8cfb8-130">IVsPackageSourceProvider. GetSources (...) a un comportement d’exception mal défini- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-130">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="8cfb8-131">Rendre publique le constructeur PluginManager- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-131">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="8cfb8-132">Mesures permettant de suivre la fréquence d’actualisation de l’interface utilisateur PM- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-132">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="8cfb8-133">Réduire le nombre d’actualisations de l’interface utilisateur lors de l’installation par le biais de l’interface utilisateur du gestionnaire de package- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-133">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="8cfb8-134">Télémétrie : les valeurs DateTime utilisent des formats spécifiques à la culture- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-134">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="8cfb8-135">Réduire les actualisations de l’interface utilisateur sous l’onglet Parcourir de l’interface utilisateur du gestionnaire de package #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-135">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="8cfb8-136">[Échec du test] Le message « Impossible d’analyser le fichier de configuration » s’affiche à deux reprises [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-136">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="8cfb8-137">Déclencher une erreur NU5037 avec une bonne page de documentation qui explique les correctifs du client (le fichier NuSpec requis est manquant dans le package)- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-137">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="8cfb8-138">La restauration en mode verrouillé échoue quand le RuntimeIdentifier d’un projet est modifié- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-138">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="8cfb8-139">Rendre les paramètres lus dans VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-139">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="8cfb8-140">La régression dans `Nuget sources add` provoque l’impossibilité d’inclure le caractère «  : », la valeur hexadécimale 0x3A, dans un nom «erreurs- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-140">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="8cfb8-141">Fournisseurs d’informations d’identification du plug-in NuGet-masquer la fenêtre de processus- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-141">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="8cfb8-142">L’application de PackagePathResolver est un chemin d’accès absolu- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-142">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="8cfb8-143">Réduire les actualisations de l’interface utilisateur dans les onglets installer et mettre à jour de l’interface utilisateur du gestionnaire de package- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-143">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="8cfb8-144">**DCR :**</span><span class="sxs-lookup"><span data-stu-id="8cfb8-144">**DCR:**</span></span>

* <span data-ttu-id="8cfb8-145">Mettre à jour les frameworks Xamarin pour les mapper à netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-145">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="8cfb8-146">Activer la copie du contenu de la « fenêtre d’aperçu » du gestionnaire de package pour l’installation/la mise à jour- [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-146">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="8cfb8-147">Activer la restauration sur les fichiers. proj- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-147">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="8cfb8-148">Introduisez des `NUGET_NETFX_PLUGIN_PATHS` et des `NUGET_NETCORE_PLUGIN_PATHS` pour prendre en charge la configuration des deux en même temps [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-148">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="8cfb8-149">Activer plusieurs versions pour un PackageDownload via l’attribut de version- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-149">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="8cfb8-150">Options Add-SolutionDirectory et-PackageDirectory à NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-150">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="8cfb8-151">**[Liste de tous les problèmes résolus dans cette version-5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="8cfb8-151">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>

## <a name="summary-whats-new-in-531"></a><span data-ttu-id="8cfb8-152">Résumé : nouveautés de la procédure 5.3.1</span><span class="sxs-lookup"><span data-stu-id="8cfb8-152">Summary: What's New in 5.3.1</span></span>

* <span data-ttu-id="8cfb8-153">Plug-in : une tâche a été annulée-ne laissez pas les annulations affecter l’instanciation du plug-in- [#8648](https://github.com/NuGet/Home/issues/8648)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-153">Plugin: A task was canceled - don't let cancellations affect plugin instantiation - [#8648](https://github.com/NuGet/Home/issues/8648)</span></span>

* <span data-ttu-id="8cfb8-154">La tâche de restauration ne peut pas être exécutée deux fois en toute sécurité dans un même processus (lorsque des fournisseurs d’informations d’identification sont utilisés)- [#8688](https://github.com/NuGet/Home/issues/8688)</span><span class="sxs-lookup"><span data-stu-id="8cfb8-154">Restore Task cannot be safely run twice in one process (when Credential providers are used) - [#8688](https://github.com/NuGet/Home/issues/8688)</span></span>
