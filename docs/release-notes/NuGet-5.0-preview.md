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
# <a name="nuget-50-preview-release-notes"></a>Notes de publication de NuGet 5.0 Preview

## <a name="nuget-50-preview-releases"></a>Préversions 5.0 NuGet

* Le 13 février 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)
* Le 23 janvier 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-3"></a>Résumé : Quelles sont les nouveautés dans NuGet 5.0 Preview 3

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version 

**Bogues :**

* nuget.exe /? doit répertorier les versions de msbuild correct - [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5) : erreur : Impossible de trouver une partie du chemin d’accès « / tmp/NuGetScratch - sur mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* restauration énumère inutilement le contenu de toutes les versions de package référencé dans le cache de l’ordinateur - [#7639](https://github.com/NuGet/Home/issues/7639)

* La détection automatique de MSBuild sélectionne toujours 16.0 après l’installation de VS 2019 affiché un aperçu - [#7621](https://github.com/NuGet/Home/issues/7621)

* package de liste dotnet sur une solution génère des entrées en double pour le framework - [#7607](https://github.com/NuGet/Home/issues/7607)

* Exception « nom de chemin d’accès vide n’est pas légale » lorsque IVsPackageInstaller.InstallPackage appelante sur l’ancien projets et packages dossier n’existent pas. - [#5936](https://github.com/NuGet/Home/issues/5936)

* niveau de détail MSBuild/t : Restore minimal doit être plus minimal - [#4695](https://github.com/NuGet/Home/issues/4695)

**DCRs**

* Permettre aux auteurs de package définir le comportement transitive de build actifs - [#6091](https://github.com/NuGet/Home/issues/6091)

* Activer la restauration dans Visual Studio pour réussir si un projet ne fait pas partie de la solution ou n’est pas chargé, mais a été précédemment restauré - [#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="summary-whats-new-in-50-preview-2"></a>Résumé : Nouveautés de la version 5.0 Preview 2

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Bogues :**

* Visual Studio de 16.0 NuGet UI comporte des onglets illisibles en raison de problèmes de couleur - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)

* Restauration énumère inutilement le dossier de package global dans la tentative de déterminer le type - [#7596](https://github.com/NuGet/Home/issues/7596)

* Erreurs de mise en œuvre du fichier de verrouillage doivent apparaître dans la fenêtre liste d’erreurs - [#7429](https://github.com/NuGet/Home/issues/7429)

* Résoudre les problèmes de NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* S’adapter à la mise à jour de MSBuild il s’agit de l’emplacement d’installation.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack doit être une dépendance de développement - [#7249](https://github.com/NuGet/Home/issues/7249)

* Ajouter le point d’extension pack pour inclure des symboles - de débogage [#7234](https://github.com/NuGet/Home/issues/7234)

* dotnet pack doit conserver la plage de versions de dépendance dans le package NuGet créé. (même si une version flottante est utilisée) - [#7232](https://github.com/NuGet/Home/issues/7232)

* restauration de dotnet échoue sur une source authentifiée lors de la configuration de niveau de l’utilisateur a également source - [#7209](https://github.com/NuGet/Home/issues/7209)

* Pack ne doit pas restreindre l’ensemble des BuildActions pour les fichiers de contenu - [#7155](https://github.com/NuGet/Home/issues/7155)

* À l’aide d’un projectreference nécessitant AssetTargetFallback réussisse, doit émettre un avertissement. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Blocage en raison de problèmes liés aux threads lors de l’appel dans le CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* dotnet ajouter le package ne sont pas utiliser les informations d’identification à partir de la configuration globale pour une source spécifiée dans la configuration locale - [#6935](https://github.com/NuGet/Home/issues/6935)

* Problèmes de thread avec MEF qui est appelée sur les chemins de code asynchrone - [#6771](https://github.com/NuGet/Home/issues/6771)

* Signature : erreur signalée à deux reprises et sans la pile des appels - [#6455](https://github.com/NuGet/Home/issues/6455)

* Installation d’un package signé avec un certificat de signature non approuvé doit afficher l’erreur - [#6318](https://github.com/NuGet/Home/issues/6318)

* La restauration NuGet incorrectement commandes NOOP lorsque 2 projets partagent répertoire obj - [#6114](https://github.com/NuGet/Home/issues/6114)

* Impossible d’utiliser PAT avec restauration dotnet sur Linux avec des packages à partir de flux authentifié - [#5651](https://github.com/NuGet/Home/issues/5651)

* restauration de dotnet échoue en raison de la machine désactivé large flux - [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Assemblys de NuGet 5.0 nécessitent .NET 4.7.2 (via la modification du moniker du Framework cible) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData de NuGet.Packaging doit être un type public. Mettre à jour les métadonnées de licence reçues à partir de spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Supprimer les paramètres des API obsolètes - [#7294](https://github.com/NuGet/Home/issues/7294)

* Délais d’attente de restauration de solution de contournement sur les systèmes avec 1 processeur - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet préfère l’authentification NTLM, même s’il existe des informations d’identification dans NuGet.config : ajouter l’option de configuration pour filtrer les types d’authentification pour les informations d’identification - [#5286](https://github.com/NuGet/Home/issues/5286)

* Activer EmbedInteropTypes pour PackageReference (fonctionnalité Packages.Config de correspondance) - [#2365](https://github.com/NuGet/Home/issues/2365)

[Liste de tous les problèmes corrigés dans cette version 5.0.0-preview2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>Problèmes connus

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive génère une erreur sur Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)
**Problème** le `--interactive` argument n’est pas transféré par l’interface cli dotnet et génère l’erreur `error: Missing value for option 'interactive'` 
 **solution de contournement** exécuter toute autre commande dotnet avec l’option interactive comme `dotnet restore --interactive` et s’authentifier. L’authentification peut-être mise en cache par le fournisseur des informations d’identification. Exécutez ensuite `dotnet nuget push`.

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Les packages dans FallbackFolders ont été installés de façon personnalisée par le kit SDK .NET Core et la validation de la signature échoue. - [#7414](https://github.com/NuGet/Home/issues/7414)
**Problème** lors de l’utilisation de dotnet.exe 2.x pour restaurer un projet qui netcoreapp cible multiples 1.x et netcoreapp 2.x, le dossier de secours est traité comme un flux de fichier. Cela signifie que, lors de la restauration, NuGet sélectionnera le package dans le dossier de secours et essaiera de l’installer dans le dossier de packages globaux, et la validation de signature habituelle échouera.
**Solution de contournement** désactiver l’utilisation du dossier de secours en définissant le `RestoreAdditionalProjectSources` avec la valeur nothing. `<RestoreAdditionalProjectSources/>` Utilisez cette option avec précaution car cela entraînera le téléchargement d’un grand nombre de packages à partir de NuGet.org, qui sinon auraient été restaurés à partir du dossier de secours.
