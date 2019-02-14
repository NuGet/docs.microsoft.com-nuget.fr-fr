---
title: Notes de publication NuGet 5.0 preview
description: Notes de publication pour les aperçus de NuGet 5.0, y compris les problèmes connus, les correctifs de bogues, les nouvelles fonctionnalités et les dcr.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247657"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="1e6a6-103">Notes de publication de NuGet 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="1e6a6-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="1e6a6-104">Préversions 5.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="1e6a6-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="1e6a6-105">Le 13 février 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="1e6a6-106">Le 23 janvier 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="1e6a6-107">Résumé : Quelles sont les nouveautés dans NuGet 5.0 Preview 3</span><span class="sxs-lookup"><span data-stu-id="1e6a6-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="1e6a6-108">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="1e6a6-108">Issues fixed in this release</span></span> 

<span data-ttu-id="1e6a6-109">**Bogues :**</span><span class="sxs-lookup"><span data-stu-id="1e6a6-109">**Bugs:**</span></span>

* <span data-ttu-id="1e6a6-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="1e6a6-110">nuget.exe /?</span></span> <span data-ttu-id="1e6a6-111">doit répertorier les versions de msbuild correct - [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="1e6a6-112">NuGet.targets(498,5) : erreur : Impossible de trouver une partie du chemin d’accès « / tmp/NuGetScratch - sur mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="1e6a6-113">restauration énumère inutilement le contenu de toutes les versions de package référencé dans le cache de l’ordinateur - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="1e6a6-114">La détection automatique de MSBuild sélectionne toujours 16.0 après l’installation de VS 2019 affiché un aperçu - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="1e6a6-115">package de liste dotnet sur une solution génère des entrées en double pour le framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="1e6a6-116">Exception « nom de chemin d’accès vide n’est pas légale » lorsque IVsPackageInstaller.InstallPackage appelante sur l’ancien projets et packages dossier n’existent pas.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="1e6a6-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="1e6a6-118">niveau de détail MSBuild/t : Restore minimal doit être plus minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="1e6a6-119">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="1e6a6-119">**DCRs**</span></span>

* <span data-ttu-id="1e6a6-120">Permettre aux auteurs de package définir le comportement transitive de build actifs - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="1e6a6-121">Activer la restauration dans Visual Studio pour réussir si un projet ne fait pas partie de la solution ou n’est pas chargé, mais a été précédemment restauré - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="1e6a6-122">Résumé : Nouveautés de la version 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="1e6a6-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="1e6a6-123">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="1e6a6-123">Issues fixed in this release</span></span>

<span data-ttu-id="1e6a6-124">**Bogues :**</span><span class="sxs-lookup"><span data-stu-id="1e6a6-124">**Bugs:**</span></span>

* <span data-ttu-id="1e6a6-125">Visual Studio de 16.0 NuGet UI comporte des onglets illisibles en raison de problèmes de couleur - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="1e6a6-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="1e6a6-127">Restauration énumère inutilement le dossier de package global dans la tentative de déterminer le type - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="1e6a6-128">Erreurs de mise en œuvre du fichier de verrouillage doivent apparaître dans la fenêtre liste d’erreurs - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="1e6a6-129">Résoudre les problèmes de NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="1e6a6-130">S’adapter à la mise à jour de MSBuild il s’agit de l’emplacement d’installation.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="1e6a6-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="1e6a6-132">NuGet.Build.Tasks.Pack doit être une dépendance de développement - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="1e6a6-133">Ajouter le point d’extension pack pour inclure des symboles - de débogage [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="1e6a6-134">dotnet pack doit conserver la plage de versions de dépendance dans le package NuGet créé.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="1e6a6-135">(même si une version flottante est utilisée) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="1e6a6-136">restauration de dotnet échoue sur une source authentifiée lors de la configuration de niveau de l’utilisateur a également source - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="1e6a6-137">Pack ne doit pas restreindre l’ensemble des BuildActions pour les fichiers de contenu - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="1e6a6-138">À l’aide d’un projectreference nécessitant AssetTargetFallback réussisse, doit émettre un avertissement.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="1e6a6-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="1e6a6-140">Blocage en raison de problèmes liés aux threads lors de l’appel dans le CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="1e6a6-141">dotnet ajouter le package ne sont pas utiliser les informations d’identification à partir de la configuration globale pour une source spécifiée dans la configuration locale - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="1e6a6-142">Problèmes de thread avec MEF qui est appelée sur les chemins de code asynchrone - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="1e6a6-143">Signature : erreur signalée à deux reprises et sans la pile des appels - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="1e6a6-144">Installation d’un package signé avec un certificat de signature non approuvé doit afficher l’erreur - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="1e6a6-145">La restauration NuGet incorrectement commandes NOOP lorsque 2 projets partagent répertoire obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="1e6a6-146">Impossible d’utiliser PAT avec restauration dotnet sur Linux avec des packages à partir de flux authentifié - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="1e6a6-147">restauration de dotnet échoue en raison de la machine désactivé large flux - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="1e6a6-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="1e6a6-148">**DCRs**</span></span>

* <span data-ttu-id="1e6a6-149">Assemblys de NuGet 5.0 nécessitent .NET 4.7.2 (via la modification du moniker du Framework cible) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="1e6a6-150">NuGetLicenseData de NuGet.Packaging doit être un type public.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="1e6a6-151">Mettre à jour les métadonnées de licence reçues à partir de spdx.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="1e6a6-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="1e6a6-153">Supprimer les paramètres des API obsolètes - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="1e6a6-154">Délais d’attente de restauration de solution de contournement sur les systèmes avec 1 processeur - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="1e6a6-155">NuGet préfère l’authentification NTLM, même s’il existe des informations d’identification dans NuGet.config : ajouter l’option de configuration pour filtrer les types d’authentification pour les informations d’identification - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="1e6a6-156">Activer EmbedInteropTypes pour PackageReference (fonctionnalité Packages.Config de correspondance) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="1e6a6-157">Liste de tous les problèmes corrigés dans cette version 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="1e6a6-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="1e6a6-158">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="1e6a6-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="1e6a6-159">dotnet nuget push --interactive génère une erreur sur Mac.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="1e6a6-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="1e6a6-161">**Problème** le `--interactive` argument n’est pas transféré par l’interface cli dotnet et génère l’erreur `error: Missing value for option 'interactive'` 
 **solution de contournement** exécuter toute autre commande dotnet avec l’option interactive comme `dotnet restore --interactive` et s’authentifier.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="1e6a6-162">L’authentification peut-être mise en cache par le fournisseur des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="1e6a6-163">Exécutez ensuite `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="1e6a6-164">Les packages dans FallbackFolders ont été installés de façon personnalisée par le kit SDK .NET Core et la validation de la signature échoue.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="1e6a6-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="1e6a6-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="1e6a6-166">**Problème** lors de l’utilisation de dotnet.exe 2.x pour restaurer un projet qui netcoreapp cible multiples 1.x et netcoreapp 2.x, le dossier de secours est traité comme un flux de fichier.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="1e6a6-167">Cela signifie que, lors de la restauration, NuGet sélectionnera le package dans le dossier de secours et essaiera de l’installer dans le dossier de packages globaux, et la validation de signature habituelle échouera.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="1e6a6-168">**Solution de contournement** désactiver l’utilisation du dossier de secours en définissant le `RestoreAdditionalProjectSources` avec la valeur nothing.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="1e6a6-169">`<RestoreAdditionalProjectSources/>` Utilisez cette option avec précaution car cela entraînera le téléchargement d’un grand nombre de packages à partir de NuGet.org, qui sinon auraient été restaurés à partir du dossier de secours.</span><span class="sxs-lookup"><span data-stu-id="1e6a6-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
