---
title: Notes de publication de NuGet 4.8 RTM
description: Notes de publication de NuGet 4.8.1, avec notamment les problèmes connus, les résolutions de bogues, les fonctionnalités ajoutées et les DCR.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: cf15c4f6a2e3e9f6ce7b6acb2304648041043685
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324823"
---
# <a name="nuget-48-rtm-release-notes"></a>Notes de publication de NuGet 4.8 RTM

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec NuGet 4.8.


Des versions en ligne de commande offrant les mêmes fonctionnalités sont également disponibles :
* NuGet.exe 4.8 - [NuGet.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [SDK .NET Core 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-this-release"></a>Résumé : Nouveautés de cette version
* NuGet.exe prend désormais en charge les noms de fichiers longs sur Windows 10 - [#6937](https://github.com/NuGet/Home/issues/6937)
* Les plug-ins d’authentification sont désormais compatibles avec MsBuild, DotNet.exe, NuGet.exe et Visual Studio, y compris en multiplateforme. La première génération de plug-ins d’authentification n’était pas prise en charge par MsBuild et DotNet.exe. Remarque : Un plug-in d’authentification VSTS est inclus dans les builds Visual Studio 2017 15.9 Preview. [#6486](https://github.com/NuGet/Home/issues/6486)
* Le programme de résolution du SDK MsBuild fait désormais partie de NuGet, et est installé avec les outils NuGet pour Visual Studio. De cette façon, les versions restent toujours synchronisées. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference prend désormais en charge les métadonnées DevelopmentDependency - [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="known-issues"></a>Problèmes connus
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>L’installation des packages signés sur une machine CI ou dans un environnement hors connexion est plus longue que d’habitude

#### <a name="issue"></a>Problème
Si l’ordinateur a un accès limité à Internet (s’il s’agit, par exemple, d’un ordinateur de build dans un scénario CI/CD), l’installation ou la restauration d’un package NuGet signé entraîne un avertissement ([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028)), car les serveurs de révocation ne sont pas accessibles. Il s'agit du comportement attendu. Toutefois, dans certains cas, cela peut avoir des conséquences inattendues, comme un temps d’installation ou de restauration plus long que d’habitude.

#### <a name="workaround"></a>Solution de contournement
Effectuez une mise à jour vers Visual Studio 15.8.4 et NuGet.exe 4.8.1, où nous avons ajouté une variable d’environnement permettant de basculer en mode de vérification de la révocation.
Le fait de définir la variable d’environnement `NUGET_CERT_REVOCATION_MODE` sur `offline` force NuGet à vérifier l’état de révocation du certificat uniquement par rapport à la liste de révocation de certificat mise en cache, et NuGet ne tente pas de contacter les serveurs de révocation. Quand le mode de vérification de révocation est défini sur `offline`, l’avertissement devient un message informatif.

> [!Warning]
> Dans des circonstances normales, il n’est pas recommandé de faire passer hors connexion le mode de vérification de révocation. Si vous le faites, NuGet va ignorer la vérification de révocation en ligne et effectuer une vérification de révocation hors connexion par rapport à la liste de révocation de certificat mise en cache, qui peut être obsolète. Cela signifie que les packages dans lesquels le certificat de signature a été révoqué continuent d’être installés ou restaurés.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>L’option `Migrate packages.config to PackageReference...` n’est pas disponible dans le menu contextuel

#### <a name="issue"></a>Problème

À la première ouverture d’un projet, il peut arriver que NuGet ne s’initialise pas tant qu’aucune opération NuGet n’a été réalisée. Dans ce cas, l’option de migration ne s’affiche pas dans le menu contextuel sur `packages.config` ou `References`.

#### <a name="workaround"></a>Solution de contournement

Effectuez l’une des actions NuGet suivantes :
* Ouvrez l’interface utilisateur du Gestionnaire de package : cliquez avec le bouton droit sur `References` et sélectionnez `Manage NuGet Packages...`.
* Ouvrez la console du Gestionnaire de package : dans `Tools > NuGet Package Manager`, sélectionnez `Package Manager Console`.
* Exécutez la restauration NuGet : cliquez avec le bouton droit sur le nœud de la solution dans l’Explorateur de solutions, puis sélectionnez `Restore NuGet Packages`.
* Générez le projet qui déclenche également la restauration NuGet.

L’option de migration devrait apparaître. Notez qu’elle n’est pas prise en charge et ne s’affiche pas pour les types de projets ASP.NET et C++.
Remarque : Ce problème a été résolu dans Visual Studio 2017 15.9 Preview 3

## <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

### <a name="bugs"></a>Bogues
#### <a name="signing"></a>Signature
* Signature : Installation d’un package signé dans un environnement hors connexion [#7008](https://github.com/NuGet/Home/issues/7008) -- Corrigé dans la version 4.8.1
* Signature : Vérification d’URL incorrecte - [#7174](https://github.com/NuGet/Home/issues/7174)
* Signature : Vérifier l’intégrité du package dans RepositorySignatureVerifier lorsque le package est contresigné par le référentiel - [#6926](https://github.com/NuGet/Home/issues/6926)
* Le message « La vérification de l’intégrité du package a échoué » doit inclure un ID de package (et un code d’erreur) - [#6944](https://github.com/NuGet/Home/issues/6944)
* La vérification des packages signés par le référentiel permet aux packages d’être signés par des certificats différents - [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet - Signature - L’URL d’horodatage ne peut pas être https:// ? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Ne pas utiliser NullRef dans un scénario de compression NuSpec améliore également les options - [#6866](https://github.com/NuGet/Home/issues/6866)
* La mémoire n’est pas valide lors de l’ajout de l’horodatage à la contresignature, dans le cadre de la mise à jour des informations sur les signataires - [#6840](https://github.com/NuGet/Home/issues/6840)
* Signature : Supprimer les exceptions de liste de certificats de confiance - [#6794](https://github.com/NuGet/Home/issues/6794)
* Signature : contentUrl doit être HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)
* Signature :  SignedPackageVerifierSettings.VSClientDefaultPolicy n’est pas utilisé - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Compression
* restore et build ne devraient pas être nécessaires lors de l’utilisation de dotnet.exe pour compresser le fichier nuspec - [#6866](https://github.com/NuGet/Home/issues/6866)
* Autoriser les jetons de remplacement vides dans NuspecProperties - [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask lève l’exception NullReferenceException quand NuspecProperties est spécifié - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Accessibilité
* [Accessibilité] La chaîne « Préversion » située sous le bouton du package est recouverte par la description du package dans l’interface utilisateur de PM - [#4504](https://github.com/NuGet/Home/issues/4504)
* [Accessibilité] La liste déroulante de la source de package et le bouton Paramètres sont tronqués lors de la sélection de « Microsoft Visual Studio Offline Packages » dans l’interface utilisateur PM - [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Console de gestion PowerShell
* `Update-Package` ignore la plage de versions de PackageReference - [#6775](https://github.com/NuGet/Home/issues/6775)
* Le problème `Update-Package -reinstall` s’étend à toute l’application - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` réinstalle tous les packages au lieu d’installer uniquement celui qui est nommé - [#737](https://github.com/NuGet/Home/issues/737)
* Peut être mis à jour vers un package NuGet non listé à partir de la Console du Gestionnaire de package - [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Divers
* Pour corriger `NuGet update self`, NuGet.Commandline nupkg ne doit pas être semver2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)
* Améliorer l’expérience utilisateur en évitant les échecs d’installation NU1107 - [#7107](https://github.com/NuGet/Home/issues/7107)
* La sérialisation de GetAuthenticationCredentialRequest est incorrecte - [#6983](https://github.com/NuGet/Home/issues/6983)
* NuGet Visual Studio AsyncPackage n’est pas chargé lorsqu’il est initialisé en dehors du thread d’interface utilisateur - [#6976](https://github.com/NuGet/Home/issues/6976)
* La restauration signale à tort que project.json est nécessaire - [#6959](https://github.com/NuGet/Home/issues/6959)
* Interface utilisateur du Gestionnaire de package : aperçu des modifications, le bouton OK n’est pas automatiquement utilisable par le clavier - [#6893](https://github.com/NuGet/Home/issues/6893)
* Les RestoreSources sont ignorées pour le projet avec des références p2p - [#6776](https://github.com/NuGet/Home/issues/6776)
* La création d’un projet de test unitaire à l’aide d’un modèle .NET Framework ouvre un ancien modèle de projet avec packages.config - [#6736](https://github.com/NuGet/Home/issues/6736)
* Autoriser la référence de projet à remplacer la dépendance de package - [#6536](https://github.com/NuGet/Home/issues/6536)
* Exposer NoDefaultExcludes dans la tâche MSBuild - [#6450](https://github.com/NuGet/Home/issues/6450)
* Le message d’état « Clear All NuGet Cache(s) » peut être masqué après un redimensionnement de la fenêtre - [#5938](https://github.com/NuGet/Home/issues/5938)


[Liste de tous les problèmes résolus dans cette version](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
