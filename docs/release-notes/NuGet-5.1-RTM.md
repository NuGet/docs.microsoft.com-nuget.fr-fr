---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975833"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="4ecaf-101">Notes de publication NuGet 5.1</span><span class="sxs-lookup"><span data-stu-id="4ecaf-101">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="4ecaf-102">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="4ecaf-102">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="4ecaf-103">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="4ecaf-103">NuGet version</span></span> | <span data-ttu-id="4ecaf-104">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ecaf-104">Available in Visual Studio version</span></span>| <span data-ttu-id="4ecaf-105">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="4ecaf-105">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="4ecaf-106">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="4ecaf-106">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="4ecaf-107">Visual Studio 2019 version 16.1</span><span class="sxs-lookup"><span data-stu-id="4ecaf-107">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="4ecaf-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="4ecaf-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="4ecaf-109"><sup>1</sup>installées avec Visual Studio 2019 par charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="4ecaf-109"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="4ecaf-110"><sup>2</sup>disponible en tant qu’option installation avec Visual Studio 2019 avec la charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="4ecaf-110"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="4ecaf-111">Résumé : Quelles sont les nouveautés dans 5.1</span><span class="sxs-lookup"><span data-stu-id="4ecaf-111">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="4ecaf-112">Prise en charge pour ignorer un push de package s’il existe déjà pour permettre une meilleure intégration avec les flux de travail CI/CD - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-112">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="4ecaf-113">Visual Studio fournit désormais un lien pratique vers la page du package de la galerie nuget.org - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-113">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="4ecaf-114">Prise en charge de nouvelles ressources .NET Core 3.0 comme [Pack de ciblage](https://github.com/dotnet/cli/issues/10006) et [Packs de Runtime](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-114">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="4ecaf-115">La prise en charge de NuGet pack et restore pour FrameworkReferences activer les références de package de ciblage et exécution - [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-115">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="4ecaf-116">Prise en charge « télécharger uniquement » package scénario avec PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-116">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="4ecaf-117">À l’aide du graphique Exlcude runtime et les packs à partir des résultats de recherche et de restauration de ciblage PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-117">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="4ecaf-118">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="4ecaf-118">Issues fixed in this release</span></span>

<span data-ttu-id="4ecaf-119">**Bogues**</span><span class="sxs-lookup"><span data-stu-id="4ecaf-119">**Bugs**</span></span>

* <span data-ttu-id="4ecaf-120">Plug-ins : détails de l’exception perdu lors de la création de plug-in - [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-120">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="4ecaf-121">Plage de PackageReference avec une limite inférieure exclusive ne fonctionne pas si la limite inférieure est présente sur une des sources.</span><span class="sxs-lookup"><span data-stu-id="4ecaf-121">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="4ecaf-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="4ecaf-123">Améliorer IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-123">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="4ecaf-124">Fichier de verrouillage - fichier de verrouillage régénérer lors de changements dans le graphique de projet - les packages [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-124">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="4ecaf-125">ProjectSystem bogue : Les Packages NuGet obtention automatique supprimé - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-125">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="4ecaf-126">Ajouter une cible pour retourner le FrameworkReference similaires aux CollectPackageDownloads et CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-126">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="4ecaf-127">Cache HTTP :  RepositoryResources ressource n’est pas mis en cache d’une manière avec version - [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-127">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="4ecaf-128">Journalisation : pile des appels d’exception ne sont pas signalés avec des commentaires détaillés - [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-128">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="4ecaf-129">Modifiez toutes les URL de Docs de NuGet afin d’utiliser le protocole HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-129">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="4ecaf-130">Améliorer le message d’avertissement NU3024 - [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-130">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="4ecaf-131">fichier de verrouillage ne pas mis à jour lorsque packagereference supprimé - [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-131">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="4ecaf-132">Améliorer la gestion de cas d’erreur lors de la validation d’un élément licenseurl et licence dans nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-132">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="4ecaf-133">PM UI - un clic droit sur l’en-tête d’onglet et en cliquant sur « Ouvrir l’emplacement du fichier » entraîne l’erreur - [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-133">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="4ecaf-134">Plug-ins : consigner les lors de la sortie du processus de plug-in - [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-134">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="4ecaf-135">Plug-ins : taux de collision élevé dans les valeurs de date/heure de journalisation - [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-135">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="4ecaf-136">Manifest.ReadFrom échoue sur n’importe quel fichier nuspec avec LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-136">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="4ecaf-137">RestoreLockedMode : NU1004 inattendu lorsque ProjectReference fait référence à un projet avec AssemblyName personnalisé - [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-137">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="4ecaf-138">Meilleur message d’erreur lorsque le démarrage de plug-in échoue avec une exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-138">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="4ecaf-139">Lorsque vous effectuez une restauration NoOp, éviter \*. écriture dgspec.json dans le répertoire obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-139">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="4ecaf-140">GeneratePathProperty = trues ne peut pas générer la propriété sur le non-respect de la casse - [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-140">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="4ecaf-141">Paramètres : caractère non conforme dans le chemin source du package peut se bloquer VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-141">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="4ecaf-142">Si le fichier de verrouillage est supprimé, restauration ne génère pas de fichier de verrouillage sur NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-142">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="4ecaf-143">URL de licence et les causes de licence lire erreur avec des métadonnées - [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-143">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="4ecaf-144">Exceptions non gérées dans V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-144">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="4ecaf-145">NuGet.exe retourne le code de sortie zéro pour les arguments non valides - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-145">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="4ecaf-146">Mettre à jour des erreurs et des documents de l’avertissement pour refléter des scénarios connexes signatures - [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-146">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="4ecaf-147">Fichier de ressources doit utiliser des chemins d’accès relatifs pour activer le déplacement de projets plus facilement - [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-147">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="4ecaf-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="4ecaf-148">**DCRs**</span></span>

* <span data-ttu-id="4ecaf-149">Plug-ins : activer la journalisation des diagnostics - [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-149">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="4ecaf-150">Mappage de Tizen 6 Vérifiez à la version 2.1 de NetStandard - [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="4ecaf-150">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="4ecaf-151">**[Liste de tous les problèmes résolus dans cette version - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="4ecaf-151">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
