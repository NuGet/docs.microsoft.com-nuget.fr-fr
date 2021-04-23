---
title: Notes de publication de NuGet 5,0 RTM
description: Notes de publication de NuGet 5,0, y compris les problèmes connus, les correctifs de bogues, les nouvelles fonctionnalités et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901744"
---
# <a name="nuget-50-release-notes"></a>Notes de publication de NuGet 5,0

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio| Disponible dans les SDK .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Version 16.0.4 de Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core 

<sup>2</sup> Disponible en tant qu’installation facultative avec Visual Studio 2019 avec la charge de travail .NET Core

## <a name="summary-whats-new-in-50"></a>Résumé : nouveautés de 5,0

* Prise en charge de la restauration de [solutions filtrées](/visualstudio/ide/filtered-solutions) dans Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` le dossier active les packages pour les cibles/props de collaboration transitant vers le projet hôte- [#6091](https://github.com/NuGet/Home/issues/6091)
* Meilleure prise en charge des scénarios PackageReference dans les API NuGet IV- [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` est déconseillé- [#7928](https://github.com/NuGet/Home/issues/7928)
* Le plug-in de fournisseur d’informations d’identification de la génération 1 a été remplacé par la [génération 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) et sera bientôt déconseillé- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Bogues**

* Lorsque vous procédez à une restauration NoOp, évitez * .dgspec.jsen écriture dans le répertoire obj- [#7854](https://github.com/NuGet/Home/issues/7854)

* Les autorisations sur les fichiers créés à l’intérieur de ~/.NuGet sont trop ouvertes- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` ne fonctionne pas avec les sources qui ont besoin de l’authentification [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet. VisualStudio. IVsPackageInstaller-l’appel de sur un projet sans références de package utilise toujours packages.config, même si la valeur par défaut est PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC : Update-Package réinstallation échoue (« impossible de trouver le package ») sur les packages dérépertoriés. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Ajouter un avis de tiers dans nos référentiel et VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet. VisualStudio. IVsPackageInstaller. InstallPackage doit installer la dernière version si aucune version n’est spécifiée- [#7493](https://github.com/NuGet/Home/issues/7493)

* --prise en charge interactive de dotnet NuGet Push- [#7519](https://github.com/NuGet/Home/issues/7519)

* Lors de la restauration avec le fichier de verrou, l’avertissement NU1603 ne doit pas être déclenché. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet ne doit pas imprimer le chemin d’accès au projet pendant la restauration avec une journalisation minimale- [#7647](https://github.com/NuGet/Home/issues/7647)

* --prise en charge interactive de dotnet Remove package- [#7727](https://github.com/NuGet/Home/issues/7727)

* Rajoutez NuGet. Packaging. Core avec TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache a besoin d’un chemin plus bref pour fonctionner correctement [#7770](https://github.com/NuGet/Home/issues/7770)

* Préférer le chemin d’accès pour la découverte MSBuild si l’utilisateur n’a pas demandé de version spécifique de MSBuild [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` doit répertorier les versions MSBuild correctes- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet. targets (498, 5) : erreur : impossible de trouver une partie du chemin d’accès'/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)

* Restore énumère inutilement le contenu de toutes les versions du package référencé dans le cache de l’ordinateur- [#7639](https://github.com/NuGet/Home/issues/7639)

* La détection automatique MSBuild sélectionne toujours 16,0 après l’installation de VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)

* le package de liste dotnet sur une solution génère des entrées en double pour le Framework- [#7607](https://github.com/NuGet/Home/issues/7607)

* L’exception « le nom de chemin d’accès vide n’est pas légal » lors de l’appel de IVsPackageInstaller. InstallPackage sur les anciens projets et les packages n’existe pas. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t : Restore le niveau de détail minimal doit être plus minimal- [#4695](https://github.com/NuGet/Home/issues/4695)

* L’interface utilisateur NuGet de VS 16 contient des onglets illisibles en raison de problèmes de couleur- [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet. Core & NuGet. clients License.txt clarification- [#7629](https://github.com/NuGet/Home/issues/7629)

* Restore énumère inutilement le dossier de package global en tentant de déterminer le type- [#7596](https://github.com/NuGet/Home/issues/7596)

* Les erreurs de la mise en application du verrouillage du fichier doivent s’afficher dans Liste d’erreurs fenêtre [#7429](https://github.com/NuGet/Home/issues/7429)

* Résoudre les problèmes de NuGet.Configfiguration- [#7326](https://github.com/NuGet/Home/issues/7326)

* Adapter à MSBuild mise à jour de son emplacement d’installation- [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet. Build. Tasks. Pack doit être une dépendance de développement- [#7249](https://github.com/NuGet/Home/issues/7249)

* Ajouter un point d’extension de Pack pour inclure des symboles de débogage- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` doit conserver la plage des versions de dépendances dans le nupkg créé (même si la version flottante est utilisée)- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` échoue sur la source authentifiée lorsque la configuration au niveau de l’utilisateur a également la source- [#7209](https://github.com/NuGet/Home/issues/7209)

* Le Pack ne doit pas restreindre l’ensemble de BuildActions pour les fichiers de contenu- [#7155](https://github.com/NuGet/Home/issues/7155)

* Si vous utilisez un ProjectReference qui nécessite que AssetTargetFallback aboutisse, doit avertir. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Blocage dû à des problèmes de thread lors de l’appel à CPS (CommonProjectSystem)- [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` n’utilise pas les informations d’identification de la configuration globale pour une source spécifiée dans la configuration locale- [#6935](https://github.com/NuGet/Home/issues/6935)

* Problèmes de Threading avec MEF appelé sur les chemins de code Async- [#6771](https://github.com/NuGet/Home/issues/6771)

* Signature : une erreur a été signalée deux fois et sans [#6455](https://github.com/NuGet/Home/issues/6455) de pile d’appels

* L’installation d’un package signé avec un certificat de signature non approuvé doit indiquer une erreur : [#6318](https://github.com/NuGet/Home/issues/6318)

* La restauration NuGet n’est pas correctement NoOps quand 2 projets partagent le répertoire obj- [#6114](https://github.com/NuGet/Home/issues/6114)

* Impossible d’utiliser PAT avec `dotnet restore` sur Linux avec des packages à partir d’un flux authentifié- [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore échoue en raison d’un flux de l’ordinateur désactivé- [#5410](https://github.com/NuGet/Home/issues/5410)

**DCR**

* Avertir de la prochaine suppression de « dotnet Pack project.jssur »- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Ajouter un avertissement de désapprobation pour le plug-in d’informations d’identification Gen1- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Signature : activé référentiel pour exiger la vérification du client de chaque package en tant que référentiel signé--via la ressource RepositorySignatures/5.0.0- [#7759](https://github.com/NuGet/Home/issues/7759)

* limiter le nombre de requêtes http par source via NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet doit cibler Net472 (pour faciliter le nettoyage de la build 16,0 du VSIX)- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC : supprimer la commande OpenPackagePage- [#7384](https://github.com/NuGet/Home/issues/7384)

* Faire correspondre NetCoreApp 3,0 à netstandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)

* Ajout de la prise en charge de netstandard 2.0 aux packages NuGet. *- [#6516](https://github.com/NuGet/Home/issues/6516)

* Autoriser les auteurs de package à définir le comportement transitif des ressources de build- [#6091](https://github.com/NuGet/Home/issues/6091)

* Prise en charge de la fonctionnalité de filtre de solution VS 2019. Prend également en charge le projet qui n’est pas dans la solution, ou les projets déchargés. Vous devez restaurer la solution complète (via l’interface CLI ou VS) en premier [#5820](https://github.com/NuGet/Home/issues/5820)

* Assemblys NuGet 5,0 pour exiger .NET 4.7.2 (via TFM change)- [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData à partir de NuGet. l’empaquetage doit être un type public. Mettez à jour les métadonnées de licence ingérées à partir de spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Supprimer les API de paramètres obsolètes- [#7294](https://github.com/NuGet/Home/issues/7294)

* Contourner les délais d’attente de restauration sur les systèmes avec 1 processeur- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet préfère l’authentification NTLM, même s’il existe des informations d’identification dans NuGet.config option-Add config pour filtrer les types d’authentification des informations d’identification- [#5286](https://github.com/NuGet/Home/issues/5286)

* Activer EmbedInteropTypes pour PackageReference (fonctionnalité de Packages.Config correspondante)- [#2365](https://github.com/NuGet/Home/issues/2365)

**[Liste de tous les problèmes résolus dans cette version-5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Résumé : nouveautés de 5.0.2

* Sécurité (lors de l’exécution via dotnet.exe ou mono.exe)-le dossier obj doit être créé avec les autorisations appropriées [#7908](https://github.com/NuGet/Home/issues/7908)

* nuget.exe restauration sur mono/MacOS échoue avec des nuget.config personnalisées et `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Problèmes connus

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Les packages dans FallbackFolders ont été installés de façon personnalisée par le kit SDK .NET Core et la validation de la signature échoue. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problème
Si vous utilisez dotnet.exe 2.x pour restaurer un projet qui cible netcoreapp 1.x et netcoreapp 2.x, le dossier de secours est traité comme un flux de fichier. Cela signifie que, lors de la restauration, NuGet sélectionnera le package dans le dossier de secours et essaiera de l’installer dans le dossier de packages globaux, et la validation de signature habituelle échouera.<br>
#### <a name="workaround"></a>Solution de contournement
Désactivez l’utilisation du dossier de secours en affectant à la valeur `RestoreAdditionalProjectSources` Nothing :

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Utilisez cette fonction avec précaution, car les packages qui seraient restaurés à partir du dossier de secours seront maintenant téléchargés à partir de NuGet.org.