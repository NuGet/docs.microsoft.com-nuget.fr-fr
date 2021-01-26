---
title: Notes de publication de NuGet 4.9 RTM
description: Notes de publication de NuGet 4.9, avec notamment les problèmes connus, les résolutions de bogues, les nouvelles fonctionnalités et les DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 429218fa4968d572ef187ef1dbfacac8a3bde2b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780145"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="d39cd-103">Notes de publication NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="d39cd-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="d39cd-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="d39cd-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d39cd-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="d39cd-105">NuGet version</span></span> | <span data-ttu-id="d39cd-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d39cd-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d39cd-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d39cd-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d39cd-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="d39cd-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d39cd-109">Version 15.9.0 de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d39cd-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="d39cd-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="d39cd-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="d39cd-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="d39cd-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="d39cd-112">n/a</span><span class="sxs-lookup"><span data-stu-id="d39cd-112">n/a</span></span> | <span data-ttu-id="d39cd-113">n/a</span><span class="sxs-lookup"><span data-stu-id="d39cd-113">n/a</span></span> |
| [<span data-ttu-id="d39cd-114">**4.9.2 indique**</span><span class="sxs-lookup"><span data-stu-id="d39cd-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="d39cd-115">Version 15.9.4 de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d39cd-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="d39cd-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="d39cd-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="d39cd-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="d39cd-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="d39cd-118">Version 15.9.6 de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d39cd-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="d39cd-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="d39cd-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="d39cd-120">Récapitulatif : Nouveautés de la version 4.9.0</span><span class="sxs-lookup"><span data-stu-id="d39cd-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="d39cd-121">Signature : activez ClientPolicies pour exiger l’utilisation d’un ensemble d’auteurs et de référentiels approuvés listés dans NuGet.Config [#6961](https://github.com/NuGet/Home/issues/6961), billet de [blog](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="d39cd-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="d39cd-122">Création de fichiers « .snupkg » qui contiennent les symboles dans un pack ; push amélioré pour comprendre le protocole nuget afin d’accepter les fichiers snupkg pour le serveur de symboles - [#6878](https://github.com/NuGet/Home/issues/6878), [billet de blog](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="d39cd-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="d39cd-123">Plug-in d’informations d’identification NuGet V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="d39cd-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="d39cd-124">Licence de packages NuGet autonomes - [#4628](https://github.com/NuGet/Home/issues/4628), [annonce](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="d39cd-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="d39cd-125">Possibilité d’activer les métadonnées « GeneratePathProperty » sur un objet PackageReference pour générer une propriété MSBuild par pack dans le répertoire Foo.Bar\1.0\" - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="d39cd-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="d39cd-126">Meilleure réussite des clients avec les opérations NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="d39cd-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="d39cd-127">Activer les restaurations de packages reproductibles à l’aide d’un fichier de verrouillage - [#5602](https://github.com/NuGet/Home/issues/5602), [annonce](https://github.com/NuGet/Announcements/issues/28), [billet de blog](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="d39cd-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d39cd-128">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="d39cd-128">Issues fixed in this release</span></span>

* <span data-ttu-id="d39cd-129">Les avertissements convertis en erreurs (via WarnAsErrors) déclenchés par PackageExtraction ne doivent jamais quitter le package extrait - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="d39cd-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="d39cd-130">Les packages mal signés ne doivent pas finir dans le dossier des packages globaux - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="d39cd-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="d39cd-131">La génération de la redirection de liaison ne doit pas ignorer les assemblys de façade - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="d39cd-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="d39cd-132">L’opération VersionRange Equals ne compare pas plages flottante - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="d39cd-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="d39cd-133">Restauration : régression des performances à l’aide de la nouvelle pile .NET Core 2.1 HTTP - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="d39cd-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="d39cd-134">La mise à jour d’un package ne doit pas modifier la propriété PrivateAssets d’un objet PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="d39cd-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="d39cd-135">Signature : la signature doit échouer si un package contient trop d’entrées (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="d39cd-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="d39cd-136">Le chemin de code « dotnet nuget push » doit prendre en charge le nouveau fournisseur d’informations d’identification - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="d39cd-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="d39cd-137">Prise en charge des plug-ins d’exécution avec la culture dite indifférente (comme dans docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="d39cd-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="d39cd-138">« nuget sources add » ne doit pas supprimer les informations d’identification de NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="d39cd-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="d39cd-139">L’installation d’un objet devDependency PackageReference doit utiliser par défaut excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="d39cd-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="d39cd-140">Correction de l’option migrator afin qu’elle s’affiche pour tous les projets et affiche une erreur si le projet est incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="d39cd-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="d39cd-141">« dotnet add package » doit valider la restauration effectuée dans le fichier de ressources - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="d39cd-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="d39cd-142">Signature : amélioration des messages d’erreur associés à la signature - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="d39cd-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="d39cd-143">[Échec de test] [zh-TW] La chaîne « Package Manager Console » n’est pas localisée sur la Console du Gestionnaire de package - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="d39cd-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="d39cd-144">Le message d’erreur « Unable to find project information » (Impossible de trouver des informations sur le projet) doit être un peu plus spécifique dans VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="d39cd-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="d39cd-145">Message d’erreur inutile lorsque vous utilisez incorrectement une balise de version nuspec d’un pack nuget - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="d39cd-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="d39cd-146">DCR - signature : prise en charge du protocole NuGet : ressource RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="d39cd-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="d39cd-147">DCR - Le fichier .nupkg.metadata sera créé au cours de l’extraction du package - contient « content-hash » - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="d39cd-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="d39cd-148">DCR - ignorer la vérification authenticode des plug-ins lors de l’exécution sur Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="d39cd-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="d39cd-149">Liste de tous les problèmes résolus dans cette version 4.9.0</span><span class="sxs-lookup"><span data-stu-id="d39cd-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="d39cd-150">Récapitulatif : Nouveautés de la version 4.9.1</span><span class="sxs-lookup"><span data-stu-id="d39cd-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="d39cd-151">Ajout de la prise en charge de la lecture d’une écriture dans le fichier nuget.config via une nouvelle commande trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="d39cd-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d39cd-152">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="d39cd-152">Issues fixed in this release</span></span>

* <span data-ttu-id="d39cd-153">Correction de la génération de lien de licence - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="d39cd-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="d39cd-154">Régression des codes d’erreur pour la validation des signatures- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="d39cd-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="d39cd-155">Le package NuGet.Build.Tasks.Pack ne contient pas d’informations de licence - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="d39cd-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="d39cd-156">Liste de tous les problèmes résolus dans cette version 4.9.1</span><span class="sxs-lookup"><span data-stu-id="d39cd-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="d39cd-157">Résumé : nouveautés de 4.9.2 indique</span><span class="sxs-lookup"><span data-stu-id="d39cd-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d39cd-158">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="d39cd-158">Issues fixed in this release</span></span>

* <span data-ttu-id="d39cd-159">La restauration VS/dotnet.exe/nuget.exe/msbuild.exe n’utilise pas les informations d’identification lorsque le nom de la source contient un blanc - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="d39cd-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="d39cd-160">Problèmes d’accessibilité LicenseAcceptanceWindow et LicenseFileWindow - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="d39cd-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="d39cd-161">Correction de FormatException dans DateTime.Parse à partir de DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="d39cd-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="d39cd-162">Liste de tous les problèmes résolus dans cette version 4.9.2</span><span class="sxs-lookup"><span data-stu-id="d39cd-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="d39cd-163">Résumé : nouveautés de 4.9.3</span><span class="sxs-lookup"><span data-stu-id="d39cd-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d39cd-164">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="d39cd-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="d39cd-165">Problèmes « Restaurations de packages reproductibles à l’aide d’un fichier de verrouillage »</span><span class="sxs-lookup"><span data-stu-id="d39cd-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="d39cd-166">Le mode verrouillé ne fonctionne pas car le hachage est mal calculé pour les packages précédemment mis en cache - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="d39cd-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="d39cd-167">La restauration correspond à une version différente de celle définie dans le fichier `packages.lock.json` - [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="d39cd-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="d39cd-168">'--locked-mode / RestoreLockedMode' entraîne des problèmes de restauration parasites quand des ProjectReferences sont impliqués - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="d39cd-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="d39cd-169">Le programme de résolution du kit MSBuild SDK tente de valider SHA pour un package de SDK en échec de restauration lors de l’utilisation de packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="d39cd-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="d39cd-170">Problèmes « Verrouiller vos dépendances à l’aide de stratégies d’approbation configurables »</span><span class="sxs-lookup"><span data-stu-id="d39cd-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="d39cd-171">dotnet.exe ne doit pas évaluer de signataires approuvés quand les packages signés ne sont pas pris en charge - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="d39cd-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="d39cd-172">L’ordre des trustedSigners dans le fichier config affecte l’évaluation des approbations - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="d39cd-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="d39cd-173">Impossible d’implémenter ISettings [provoqué par la refactorisation des API de paramètres pour prendre en charge la fonctionnalité de stratégies d’approbation] - [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="d39cd-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="d39cd-174">Problèmes « Expérience de débogage améliorée »</span><span class="sxs-lookup"><span data-stu-id="d39cd-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="d39cd-175">Impossible de publier le package de symboles pour l’outil global .NET Core - [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="d39cd-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="d39cd-176">Problèmes « Packages NuGet autonomes - Licence »</span><span class="sxs-lookup"><span data-stu-id="d39cd-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="d39cd-177">Erreur de création de package de symboles .snupkg lors de l’utilisation du fichier de licence incorporé - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="d39cd-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="d39cd-178">Liste de tous les problèmes résolus dans cette version 4.9.3</span><span class="sxs-lookup"><span data-stu-id="d39cd-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="d39cd-179">Résumé : nouveautés de 4.9.4</span><span class="sxs-lookup"><span data-stu-id="d39cd-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="d39cd-180">Correctif de sécurité : les autorisations sur les fichiers créés à l’intérieur de ~/.NuGet sont trop ouvertes [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="d39cd-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="d39cd-181">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="d39cd-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="d39cd-182">dotnet nuget push --interactive génère une erreur sur Mac.</span><span class="sxs-lookup"><span data-stu-id="d39cd-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="d39cd-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="d39cd-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="d39cd-184">Problème</span><span class="sxs-lookup"><span data-stu-id="d39cd-184">Issue</span></span>
<span data-ttu-id="d39cd-185">L’argument `--interactive` n’est pas transféré par l’interface CLI dotnet et génère l’erreur `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="d39cd-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="d39cd-186">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="d39cd-186">Workaround</span></span>
<span data-ttu-id="d39cd-187">Exécutez une autre commande dotnet avec l’option interactive, par exemple `dotnet restore --interactive` et identifiez-vous.</span><span class="sxs-lookup"><span data-stu-id="d39cd-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="d39cd-188">L’authentification peut-être mise en cache par le fournisseur des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="d39cd-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="d39cd-189">Exécutez ensuite `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="d39cd-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="d39cd-190">Les packages dans FallbackFolders ont été installés de façon personnalisée par le kit SDK .NET Core et la validation de la signature échoue.</span><span class="sxs-lookup"><span data-stu-id="d39cd-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="d39cd-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="d39cd-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="d39cd-192">Problème</span><span class="sxs-lookup"><span data-stu-id="d39cd-192">Issue</span></span>
<span data-ttu-id="d39cd-193">Si vous utilisez dotnet.exe 2.x pour restaurer un projet qui cible netcoreapp 1.x et netcoreapp 2.x, le dossier de secours est traité comme un flux de fichier.</span><span class="sxs-lookup"><span data-stu-id="d39cd-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="d39cd-194">Cela signifie que, lors de la restauration, NuGet sélectionnera le package dans le dossier de secours et essaiera de l’installer dans le dossier de packages globaux, et la validation de signature habituelle échouera.</span><span class="sxs-lookup"><span data-stu-id="d39cd-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="d39cd-195">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="d39cd-195">Workaround</span></span>
<span data-ttu-id="d39cd-196">Désactivez l’utilisation du dossier de secours en n’attribuant aucune valeur au paramètre `RestoreAdditionalProjectSources`.</span><span class="sxs-lookup"><span data-stu-id="d39cd-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="d39cd-197">`<RestoreAdditionalProjectSources/>` Utilisez cette option avec précaution car cela entraînera le téléchargement d’un grand nombre de packages à partir de NuGet.org, qui sinon auraient été restaurés à partir du dossier de secours.</span><span class="sxs-lookup"><span data-stu-id="d39cd-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
