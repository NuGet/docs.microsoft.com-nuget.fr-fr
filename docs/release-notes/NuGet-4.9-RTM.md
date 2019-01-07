---
title: Notes de publication de NuGet 4.9 RTM
description: Notes de publication de NuGet 4.9, avec notamment les problèmes connus, les résolutions de bogues, les nouvelles fonctionnalités et les DCR.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735134"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="7643a-103">Notes de publication NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="7643a-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="7643a-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="7643a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="7643a-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="7643a-105">NuGet version</span></span> | <span data-ttu-id="7643a-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7643a-106">Available in Visual Studio version</span></span>| <span data-ttu-id="7643a-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="7643a-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| <span data-ttu-id="7643a-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="7643a-108">**4.9.0**</span></span> | <span data-ttu-id="7643a-109">Visual Studio 2017 version 15.9.0</span><span class="sxs-lookup"><span data-stu-id="7643a-109">Visual Studio 2017 version 15.9.0</span></span> | <span data-ttu-id="7643a-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="7643a-110">2.1.500, 2.2.100</span></span> |
| <span data-ttu-id="7643a-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="7643a-111">**4.9.1**</span></span> | <span data-ttu-id="7643a-112">N/A</span><span class="sxs-lookup"><span data-stu-id="7643a-112">n/a</span></span> | <span data-ttu-id="7643a-113">N/A</span><span class="sxs-lookup"><span data-stu-id="7643a-113">n/a</span></span> |
| [<span data-ttu-id="7643a-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="7643a-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="7643a-115">Visual Studio 2017 version 15.9.4</span><span class="sxs-lookup"><span data-stu-id="7643a-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="7643a-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="7643a-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a><span data-ttu-id="7643a-117">Résumé : Nouveautés de la version 4.9.0</span><span class="sxs-lookup"><span data-stu-id="7643a-117">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="7643a-118">Signature : configure ClientPolicies pour exiger l’utilisation d’un groupe d’auteurs et de référentiels de confiance répertoriés dans NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [billet de blog](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="7643a-118">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="7643a-119">Création de fichiers « .snupkg » qui contiennent les symboles dans un pack ; push amélioré pour comprendre le protocole nuget afin d’accepter les fichiers snupkg pour le serveur de symboles - [#6878](https://github.com/NuGet/Home/issues/6878), [billet de blog](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="7643a-119">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="7643a-120">Plug-in d’informations d’identification NuGet V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="7643a-120">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="7643a-121">Licence de packages NuGet autonomes - [#4628](https://github.com/NuGet/Home/issues/4628), [annonce](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="7643a-121">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="7643a-122">Possibilité d’activer les métadonnées « GeneratePathProperty » sur un objet PackageReference pour générer une propriété MSBuild par pack dans le répertoire Foo.Bar\1.0\" - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="7643a-122">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="7643a-123">Meilleure réussite des clients avec les opérations NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="7643a-123">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7643a-124">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="7643a-124">Issues fixed in this release</span></span>

* <span data-ttu-id="7643a-125">Les avertissements convertis en erreurs (via WarnAsErrors) déclenchés par PackageExtraction ne doivent jamais quitter le package extrait - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="7643a-125">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="7643a-126">Les packages mal signés ne doivent pas finir dans le dossier des packages globaux - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="7643a-126">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="7643a-127">La génération de la redirection de liaison ne doit pas ignorer les assemblys de façade - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="7643a-127">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="7643a-128">L’opération VersionRange Equals ne compare pas plages flottante - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="7643a-128">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="7643a-129">Restauration : régression des performances à l’aide de la nouvelle pile .NET Core 2.1 HTTP - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="7643a-129">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="7643a-130">La mise à jour d’un package ne doit pas modifier la propriété PrivateAssets d’un objet PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="7643a-130">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="7643a-131">Signature : la signature doit échouer si un package contient trop d’entrées (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="7643a-131">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="7643a-132">Le chemin de code « dotnet nuget push » doit prendre en charge le nouveau fournisseur d’informations d’identification - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="7643a-132">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="7643a-133">Prise en charge des plug-ins d’exécution avec la culture dite indifférente (comme dans docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="7643a-133">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="7643a-134">« nuget sources add » ne doit pas supprimer les informations d’identification de NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="7643a-134">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="7643a-135">L’installation d’un objet devDependency PackageReference doit utiliser par défaut excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="7643a-135">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="7643a-136">Correction de l’option migrator afin qu’elle s’affiche pour tous les projets et affiche une erreur si le projet est incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="7643a-136">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="7643a-137">« dotnet add package » doit valider la restauration effectuée dans le fichier de ressources - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="7643a-137">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="7643a-138">Signature : amélioration des messages d’erreur associés à la signature - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="7643a-138">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="7643a-139">[Échec de test] [zh-TW] La chaîne « Package Manager Console » n’est pas localisée sur la Console du Gestionnaire de package - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="7643a-139">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="7643a-140">Le message d’erreur « Unable to find project information » (Impossible de trouver des informations sur le projet) doit être un peu plus spécifique dans VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="7643a-140">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="7643a-141">Message d’erreur inutile lorsque vous utilisez incorrectement une balise de version nuspec d’un pack nuget - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="7643a-141">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="7643a-142">DCR - signature : prise en charge du protocole NuGet : ressource RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="7643a-142">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="7643a-143">DCR - Le fichier .nupkg.metadata sera créé au cours de l’extraction du package - contient « content-hash » - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="7643a-143">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="7643a-144">DCR - ignorer la vérification authenticode des plug-ins lors de l’exécution sur Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="7643a-144">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="7643a-145">Liste de tous les problèmes résolus dans cette version 4.9.0</span><span class="sxs-lookup"><span data-stu-id="7643a-145">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="7643a-146">Résumé : Nouveautés de la version 4.9.1</span><span class="sxs-lookup"><span data-stu-id="7643a-146">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="7643a-147">Ajout de la prise en charge de la lecture d’une écriture dans le fichier nuget.config via une nouvelle commande trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="7643a-147">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7643a-148">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="7643a-148">Issues fixed in this release</span></span>

* <span data-ttu-id="7643a-149">Correction de la génération de lien de licence - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="7643a-149">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="7643a-150">Régression des codes d’erreur pour la validation des signatures- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="7643a-150">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="7643a-151">Le package NuGet.Build.Tasks.Pack ne contient pas d’informations de licence - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="7643a-151">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="7643a-152">Liste de tous les problèmes résolus dans cette version 4.9.1</span><span class="sxs-lookup"><span data-stu-id="7643a-152">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="7643a-153">Résumé : Nouveautés de la version 4.9.2</span><span class="sxs-lookup"><span data-stu-id="7643a-153">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7643a-154">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="7643a-154">Issues fixed in this release</span></span>

* <span data-ttu-id="7643a-155">La restauration VS/dotnet.exe/nuget.exe/msbuild.exe n’utilise pas les informations d’identification lorsque le nom de la source contient un blanc - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="7643a-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="7643a-156">Problèmes d’accessibilité LicenseAcceptanceWindow et LicenseFileWindow - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="7643a-156">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="7643a-157">Correction de FormatException dans DateTime.Parse à partir de DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="7643a-157">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="7643a-158">Liste de tous les problèmes résolus dans cette version 4.9.2</span><span class="sxs-lookup"><span data-stu-id="7643a-158">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a><span data-ttu-id="7643a-159">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="7643a-159">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="7643a-160">dotnet nuget push --interactive génère une erreur sur Mac.</span><span class="sxs-lookup"><span data-stu-id="7643a-160">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="7643a-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="7643a-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="7643a-162">Problème</span><span class="sxs-lookup"><span data-stu-id="7643a-162">Issue</span></span>
<span data-ttu-id="7643a-163">L’argument `--interactive` n’est pas transféré par l’interface CLI dotnet et génère l’erreur `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="7643a-163">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="7643a-164">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="7643a-164">Workaround</span></span>
<span data-ttu-id="7643a-165">Exécutez une autre commande dotnet avec l’option interactive, par exemple `dotnet restore --interactive` et identifiez-vous.</span><span class="sxs-lookup"><span data-stu-id="7643a-165">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="7643a-166">L’authentification peut-être mise en cache par le fournisseur des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7643a-166">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="7643a-167">Exécutez ensuite `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="7643a-167">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="7643a-168">Les packages dans FallbackFolders ont été installés de façon personnalisée par le kit SDK .NET Core et la validation de la signature échoue.</span><span class="sxs-lookup"><span data-stu-id="7643a-168">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="7643a-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="7643a-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="7643a-170">Problème</span><span class="sxs-lookup"><span data-stu-id="7643a-170">Issue</span></span>
<span data-ttu-id="7643a-171">Si vous utilisez dotnet.exe 2.x pour restaurer un projet qui cible netcoreapp 1.x et netcoreapp 2.x, le dossier de secours est traité comme un flux de fichier.</span><span class="sxs-lookup"><span data-stu-id="7643a-171">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="7643a-172">Cela signifie que, lors de la restauration, NuGet sélectionnera le package dans le dossier de secours et essaiera de l’installer dans le dossier de packages globaux, et la validation de signature habituelle échouera.</span><span class="sxs-lookup"><span data-stu-id="7643a-172">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="7643a-173">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="7643a-173">Workaround</span></span>
<span data-ttu-id="7643a-174">Désactivez l’utilisation du dossier de secours en n’attribuant aucune valeur au paramètre `RestoreAdditionalProjectSources`.</span><span class="sxs-lookup"><span data-stu-id="7643a-174">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="7643a-175">`<RestoreAdditionalProjectSources/>` Utilisez cette option avec précaution car cela entraînera le téléchargement d’un grand nombre de packages à partir de NuGet.org, qui sinon auraient été restaurés à partir du dossier de secours.</span><span class="sxs-lookup"><span data-stu-id="7643a-175">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
