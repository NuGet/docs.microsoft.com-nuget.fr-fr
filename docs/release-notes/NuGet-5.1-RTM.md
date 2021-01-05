---
title: Notes de publication de NuGet 5,1 RTM
description: Notes de publication de NuGet 5,1, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699865"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="8c393-103">Notes de publication de NuGet 5,1</span><span class="sxs-lookup"><span data-stu-id="8c393-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="8c393-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="8c393-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="8c393-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="8c393-105">NuGet version</span></span> | <span data-ttu-id="8c393-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8c393-106">Available in Visual Studio version</span></span>| <span data-ttu-id="8c393-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="8c393-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="8c393-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="8c393-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="8c393-109">Visual Studio 2019 version 16,1</span><span class="sxs-lookup"><span data-stu-id="8c393-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="8c393-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="8c393-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="8c393-111"><sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="8c393-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="8c393-112"><sup>2</sup> Disponible en tant qu’installation facultative avec Visual Studio 2019 avec la charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="8c393-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="8c393-113">Résumé : nouveautés de 5,1</span><span class="sxs-lookup"><span data-stu-id="8c393-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="8c393-114">Prise en charge pour ignorer un push de package s’il existe déjà pour permettre une meilleure intégration avec les flux de travail CI/CD- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="8c393-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="8c393-115">Visual Studio fournit maintenant un lien pratique vers la page de la Galerie nuget.org du package- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="8c393-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="8c393-116">Prise en charge des nouvelles ressources .NET Core 3,0, telles que le [ciblage de packs](https://github.com/dotnet/cli/issues/10006) et les [packs d’exécution](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="8c393-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="8c393-117">Prise en charge du Pack et de la restauration NuGet pour FrameworkReferences pour activer le ciblage et les références de package d’exécution- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="8c393-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="8c393-118">Prise en charge du scénario de package « Télécharger uniquement » avec PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="8c393-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="8c393-119">Exclure le runtime et les packs de ciblage des résultats de la recherche & Restore Graph à l’aide de PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="8c393-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="8c393-120">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="8c393-120">Issues fixed in this release</span></span>

<span data-ttu-id="8c393-121">**Bogues**</span><span class="sxs-lookup"><span data-stu-id="8c393-121">**Bugs**</span></span>

* <span data-ttu-id="8c393-122">Plug-ins : détails de l’exception perdus pendant la création du plug-in- [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="8c393-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="8c393-123">La plage PackageReference avec limite inférieure exclusive ne fonctionne pas si la limite inférieure est présente dans l’une des sources.</span><span class="sxs-lookup"><span data-stu-id="8c393-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="8c393-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="8c393-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="8c393-125">Améliorer les messages IsPackableFalseError- [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="8c393-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="8c393-126">Packages verrouiller les fichiers-régénérer le fichier de verrouillage lorsque le graphique du projet change- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="8c393-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="8c393-127">Bogue ProjectSystem : packages NuGet en cours de suppression automatique- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="8c393-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="8c393-128">Ajoutez une cible pour retourner le FrameworkReference similaire à CollectPackageDownloads et CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="8c393-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="8c393-129">Cache HTTP : la ressource RepositoryResources n’est pas mise en cache dans une méthode avec version [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="8c393-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="8c393-130">Journalisation : les piles d’exception ne sont pas signalés avec un niveau de détail détaillé- [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="8c393-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="8c393-131">Modifiez toutes les URL des documents NuGet pour utiliser le protocole HTTPs- [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="8c393-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="8c393-132">Améliorer le message d’avertissement NU3024- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="8c393-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="8c393-133">verrouillage du fichier qui n’est pas mis à jour quand packagereference a été supprimé- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="8c393-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="8c393-134">Améliorer la gestion des cas d’erreur lors de la validation de licenseUrl et de l’élément de licence dans NuSpec- [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="8c393-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="8c393-135">Interface utilisateur PM-cliquer avec le bouton droit sur l’en-tête de l’onglet et cliquer sur « Ouvrir l’emplacement du fichier » génère une erreur- [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="8c393-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="8c393-136">Plug-ins : journal lorsque le processus de plug-in se termine- [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="8c393-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="8c393-137">Plug-ins : taux de collision élevé dans la journalisation des valeurs DateTime- [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="8c393-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="8c393-138">Manifest. ReadFrom échoue sur n’importe quel NuSpec avec LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="8c393-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="8c393-139">RestoreLockedMode : NU1004 inattendu quand ProjectReference fait référence à un projet avec un [#7889](https://github.com/NuGet/Home/issues/7889) AssemblyName personnalisé</span><span class="sxs-lookup"><span data-stu-id="8c393-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="8c393-140">Meilleur message d’erreur lorsque le démarrage du plug-in échoue avec une exception- [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="8c393-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="8c393-141">Lorsque vous procédez à une restauration NoOp, évitez \* .dgspec.jsen écriture dans le répertoire obj- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="8c393-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="8c393-142">GeneratePathProperty = true ne parvient pas à générer la propriété en cas d’incompatibilité de cas- [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="8c393-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="8c393-143">Paramètres : un caractère non conforme dans le chemin source du package peut se bloquer et [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="8c393-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="8c393-144">Si le fichier de verrouillage est supprimé, la restauration ne génère pas de fichier de verrouillage sur NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="8c393-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="8c393-145">L’URL et la licence de la licence provoquent une erreur de lecture avec les métadonnées- [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="8c393-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="8c393-146">Exceptions non gérées dans V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="8c393-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="8c393-147">nuget.exe retourne le code de sortie zéro pour les arguments non valides- [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="8c393-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="8c393-148">Mettre à jour les erreurs et les documents d’avertissement pour refléter les scénarios liés à la signature- [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="8c393-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="8c393-149">Le fichier de ressources doit utiliser des chemins d’accès relatifs pour faciliter le déplacement des projets [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="8c393-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="8c393-150">**DCR**</span><span class="sxs-lookup"><span data-stu-id="8c393-150">**DCRs**</span></span>

* <span data-ttu-id="8c393-151">Plug-ins : activer la journalisation des diagnostics- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="8c393-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="8c393-152">Faire correspondre Tizen 6 à netstandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="8c393-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="8c393-153">**[Liste de tous les problèmes résolus dans cette version-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="8c393-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
