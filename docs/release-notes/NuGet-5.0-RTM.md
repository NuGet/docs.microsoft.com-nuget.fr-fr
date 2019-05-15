---
title: Notes de publication de NuGet 5.0 RTM
description: Notes de publication pour 5.0 NuGet, y compris les problèmes connus, les correctifs de bogues, les nouvelles fonctionnalités et les dcr.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610658"
---
# <a name="nuget-50-release-notes"></a>Notes de publication NuGet 5.0

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio| Disponible dans les SDK .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>installées avec Visual Studio 2019 par charge de travail .NET Core 

<sup>2</sup>disponible en tant qu’option installation avec Visual Studio 2019 avec la charge de travail .NET Core

## <a name="summary-whats-new-in-50"></a>Résumé : Quelles sont les nouveautés dans 5.0

* Prise en charge pour la restauration [filtré solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) dans Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` dossier permet de packages de manière transitive contribuer cibles/propriétés au projet hôte - [#6091](https://github.com/NuGet/Home/issues/6091)
* Meilleure prise en charge pour les scénarios de PackageReference dans NuGet IV API - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` a été déconseillé - [#7928](https://github.com/NuGet/Home/issues/7928)
* Plug-in du fournisseur d’informations d’identification de génération 1 a été remplacée par [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) et sera bientôt dépréciée - [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Bogues**

* Lorsque vous effectuez une restauration NoOp, éviter *. écriture dgspec.json dans le répertoire obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* Autorisations sur les fichiers créés à l’intérieur de ~/.nuget sont trop ouverts - [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` ne fonctionne pas avec les sources nécessitant une authentification - [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller - appel sur un projet avec aucun package fait référence à toujours utilise packages.config, même si la valeur par défaut est définie sur PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC : Package de mise à jour réinstaller échoue (« Impossible de trouver le package ») sur les packages delisted. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Ajouter des avis de tiers dans notre référentiel et le VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage devez installer la version la plus récente lorsque aucune version donnée - [#7493](https://github.com/NuGet/Home/issues/7493)

* --prise en charge interactive pour dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)

* Lors de la restauration avec le fichier de verrouillage, NU1603 avertissement ne doit pas être déclenché. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet ne doit pas imprimer le chemin d’accès pendant la restauration avec une journalisation minimale - [#7647](https://github.com/NuGet/Home/issues/7647)

* --la prise en charge interactive pour dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)

* Ajouter nouveau NuGet.Packaging.Core avec TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache a besoin d’un chemin plus court pour un fonctionnement optimal - [#7770](https://github.com/NuGet/Home/issues/7770)

* Préférez le chemin d’accès pour la découverte de msbuild si l’utilisateur n’a pas demander une version de msbuild spécifiques - [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` doit répertorier les versions de msbuild correct - [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5) : erreur : Impossible de trouver une partie du chemin d’accès « / tmp/NuGetScratch - sur mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* restauration énumère inutilement le contenu de toutes les versions de package référencé dans le cache de l’ordinateur - [#7639](https://github.com/NuGet/Home/issues/7639)

* La détection automatique de MSBuild sélectionne toujours 16.0 après l’installation de VS 2019 affiché un aperçu - [#7621](https://github.com/NuGet/Home/issues/7621)

* package de liste dotnet sur une solution génère des entrées en double pour le framework - [#7607](https://github.com/NuGet/Home/issues/7607)

* Exception « nom de chemin d’accès vide n’est pas légale » lorsque IVsPackageInstaller.InstallPackage appelante sur l’ancien projets et packages dossier n’existent pas. - [#5936](https://github.com/NuGet/Home/issues/5936)

* niveau de détail MSBuild/t : Restore minimal doit être plus minimal - [#4695](https://github.com/NuGet/Home/issues/4695)

* Visual Studio de 16.0 NuGet UI comporte des onglets illisibles en raison de problèmes de couleur - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)

* Restauration énumère inutilement le dossier de package global dans la tentative de déterminer le type - [#7596](https://github.com/NuGet/Home/issues/7596)

* Erreurs de mise en œuvre du fichier de verrouillage doivent apparaître dans la fenêtre liste d’erreurs - [#7429](https://github.com/NuGet/Home/issues/7429)

* Résoudre les problèmes de NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Adapter à MSBuild de la mise à jour son installation emplacement - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack doit être une dépendance de développement - [#7249](https://github.com/NuGet/Home/issues/7249)

* Ajouter le point d’extension pack pour inclure des symboles - de débogage [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` doit conserver la plage de versions de dépendance dans le package NuGet créé (même si une version flottante est utilisée) - [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` ne fonctionne pas pour une source authentifiée lors de la configuration de niveau de l’utilisateur a également source - [#7209](https://github.com/NuGet/Home/issues/7209)

* Pack ne doit pas restreindre l’ensemble des BuildActions pour les fichiers de contenu - [#7155](https://github.com/NuGet/Home/issues/7155)

* À l’aide d’un ProjectReference nécessitant AssetTargetFallback réussisse, doit émettre un avertissement. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Blocage en raison de problèmes liés aux threads lors de l’appel dans le CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` n’utilise pas les informations d’identification à partir de la configuration globale pour une source spécifiée dans la configuration locale - [#6935](https://github.com/NuGet/Home/issues/6935)

* Problèmes liés aux threads grâce à MEF, appelé sur async code chemins d’accès - [#6771](https://github.com/NuGet/Home/issues/6771)

* Signature : erreur signalée à deux reprises et sans la pile des appels - [#6455](https://github.com/NuGet/Home/issues/6455)

* Installation d’un package signé avec un certificat de signature non approuvé doit afficher l’erreur - [#6318](https://github.com/NuGet/Home/issues/6318)

* La restauration NuGet incorrectement commandes NOOP lorsque 2 projets partagent répertoire obj - [#6114](https://github.com/NuGet/Home/issues/6114)

* Impossible d’utiliser PAT avec `dotnet restore` sur Linux avec des packages à partir de flux authentifié - [#5651](https://github.com/NuGet/Home/issues/5651)

* restauration de dotnet échoue en raison de la machine désactivé large flux - [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Avertir de la suppression ultérieure des « project.json du pack dotnet - » [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Ajoute un avertissement de désapprobation pour plug-in des informations d’identification Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Signature : Référentiel est activée pour exiger la vérification du client de chaque package en tant que référentiel signée--via RepositorySignatures/5.0.0 ressource - [#7759](https://github.com/NuGet/Home/issues/7759)

* limiter le nombre de demande http par source via NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet doit cibler Net472 (ce qui permet le nettoyage de la build 16.0 de l’extension VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC : Supprimer la commande de OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)

* Mappage de NetCoreApp 3.0 marque à la version 2.1 de NetStandard - [#7762](https://github.com/NuGet/Home/issues/7762)

* Ajouter la prise en charge netstandard2.0 aux packages de NuGet.* - [#6516](https://github.com/NuGet/Home/issues/6516)

* Permettre aux auteurs de package définir le comportement transitive de build actifs - [#6091](https://github.com/NuGet/Home/issues/6091)

* Prend en charge la fonctionnalité de filtre de Solution VS 2019. Prend également en charge projet pas de solution ou les projets déchargés. Avez besoin de restaurer une solution complète (via l’interface CLI ou VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)

* Assemblys de NuGet 5.0 nécessitent .NET 4.7.2 (via la modification du moniker du Framework cible) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData de NuGet.Packaging doit être un type public. Mettre à jour les métadonnées de licence reçues à partir de spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Supprimer les paramètres des API obsolètes - [#7294](https://github.com/NuGet/Home/issues/7294)

* Délais d’attente de restauration de solution de contournement sur les systèmes avec 1 processeur - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet préfère l’authentification NTLM, même s’il existe des informations d’identification dans NuGet.config : ajouter l’option de configuration pour filtrer les types d’authentification pour les informations d’identification - [#5286](https://github.com/NuGet/Home/issues/5286)

* Activer EmbedInteropTypes pour PackageReference (fonctionnalité Packages.Config de correspondance) - [#2365](https://github.com/NuGet/Home/issues/2365)

**[Liste de tous les problèmes résolus dans cette version - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Résumé : Quelles sont les nouveautés dans 5.0.2

* Sécurité (à l’exécution par le biais de dotnet.exe ou mono.exe) - le dossier obj doit être créé avec les autorisations appropriées [#7908](https://github.com/NuGet/Home/issues/7908)

* restauration de NuGet.exe sur mono/Mac OS échoue avec nuget.config personnalisé et `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Problèmes connus

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Les packages dans FallbackFolders ont été installés de façon personnalisée par le kit SDK .NET Core et la validation de la signature échoue. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problème
Si vous utilisez dotnet.exe 2.x pour restaurer un projet qui cible netcoreapp 1.x et netcoreapp 2.x, le dossier de secours est traité comme un flux de fichier. Cela signifie que, lors de la restauration, NuGet sélectionnera le package dans le dossier de secours et essaiera de l’installer dans le dossier de packages globaux, et la validation de signature habituelle échouera.<br>
#### <a name="workaround"></a>Solution de contournement
Désactiver l’utilisation du dossier de secours en définissant le `RestoreAdditionalProjectSources` Nothing :

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Utilisez-le avec précaution comme des packages seraient restaurés à partir du dossier de secours est maintenant téléchargés à partir de NuGet.org.
