---
title: Notes de publication de NuGet 4.0 RC | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/17/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication de NuGet 4.0 RC, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR."
keywords: "notes de publication de NuGet 4.0 RC, correctifs de bogues, problèmes connus, fonctionnalités ajoutées, DCR"
ms.reviewer:
- kraigb
ms.openlocfilehash: 9156f75edc9cf72cbb1d122f01d8a071ed56a124
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-40-rc-release-notes"></a>Notes de publication de la version NuGet 4.0 RC

[Notes de publication de NuGet 3.5 RTM](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC pour Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) ajoute la prise en charge des scénarios .NET Core, répond aux principaux commentaires des clients et améliore les performances dans de nombreux scénarios. Cette version offre plusieurs améliorations telles que la prise en charge de PackageReference, des commandes NuGet comme cibles MSBuild, la restauration des packages en arrière-plan, et bien plus encore.

## <a name="bug-fixes"></a>Correctifs de bogues

- Changements de comportement dans `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)

- Échec de la restauration de nuget.exe sur les ordinateurs VS « 15 » uniquement - [#3834](https://github.com/NuGet/Home/issues/3834)

- Un nouveau projet de fichier .NETCore doit bloquer la build pendant la restauration - [#3780](https://github.com/NuGet/Home/issues/3780)

- Impossible de restaurer une application web ASP.NET Core migrée de VS2015 vers VS « 15 ». - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Échec de test] Le package « jQuery Validation » ne peut pas être désinstallé par l’interface utilisateur du Gestionnaire de package - [#3755](https://github.com/NuGet/Home/issues/3755)

- Quand un package est installé dans un fichier `project.json` UWP, les projets parents doivent également être restaurés - [#3731](https://github.com/NuGet/Home/issues/3731)

- Modifiez les cibles NuGet pour enregistrer dans le journal les sources de package avec un niveau de détail élevé plutôt que normal - [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet pack3 doit inclure la documentation XML par défaut - [#3698](https://github.com/NuGet/Home/issues/3698)

- La mise à jour par lots échoue à partir de l’interface utilisateur quand la source sans le package est en premier que et Tout est sélectionné comme source - [#3696](https://github.com/NuGet/Home/issues/3696)

- La commande Nuget pack n’inclut pas tous les fichiers - [#3678](https://github.com/NuGet/Home/issues/3678)

- Problème d’insuffisance de mémoire - [#3661](https://github.com/NuGet/Home/issues/3661)

- La section ProjectFileDependencyGroups du fichier de ressources doit utiliser des noms de bibliothèques pour les projets - [#3611](https://github.com/NuGet/Home/issues/3611)

- « dotnet restore » et sous-répertoires récursifs - [#3517](https://github.com/NuGet/Home/issues/3517)

- Les échecs Restore3 sont enregistrés en tant qu’avertissements plutôt qu’en tant qu’erreurs - [#3503](https://github.com/NuGet/Home/issues/3503)

- Problème TFS : « [fichier] introuvable dans votre espace de travail, ou vous n’êtes pas autorisé à y accéder » - [#2805](https://github.com/NuGet/Home/issues/2805)

- Le fait de taper « nuget <packagename>» dans la zone de recherche de lancement rapide de Visual Studio conserve le préfixe « nuget » - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException : Élément racine non reconnu dans le composant Core Properties. Ligne 2, position 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` avec &lt; ou &gt; placé dans une séquence d’échappement dans des champs de texte n’est plus généré - [#2651](https://github.com/NuGet/Home/issues/2651)

- La suppression nuget.exe n’invite pas à fournir d’informations d’identification (elle est en mode non interactif) - [#2626](https://github.com/NuGet/Home/issues/2626)

- La suppression nuget.exe fournit un avertissement concernant la Clé API pour les sources locales, alors que cela n’est pas justifié - [#2625](https://github.com/NuGet/Home/issues/2625)

- Expérience d’erreur médiocre lors de l’installation de package -pre EF - [#2566](https://github.com/NuGet/Home/issues/2566)

- Visual Studio s’est arrêté de manière anormale après un changement de sélection dans le Gestionnaire de package - [#2551](https://github.com/NuGet/Home/issues/2551)

- La restauration dotnet effectue des recherches d’ID respectant la casse sur des dépôts locaux à liste plate quand des versions flottantes sont utilisées - [#2516](https://github.com/NuGet/Home/issues/2516)

- La suppression nuget.exe est rompue pour le flux V2 - [#2509](https://github.com/NuGet/Home/issues/2509)

- Le délai d’attente de push de nuget.exe a besoin d’un meilleur message d’erreur - [#2503](https://github.com/NuGet/Home/issues/2503)

- La restauration d’outil sans importations correctes échoue de manière silencieuse. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet vous invite à entrer des informations d’identification quand il y a un flux privé, même lors de l’installation à partir de nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)

- Un package ApplicationInsights 2.0 est répertorié alors qu’il n’existe pas encore - [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay dans la branche 5 de Visual Studio « 15 » Preview - [#3500](https://github.com/NuGet/Home/issues/3500)

- Le premier événement OnBuild est ignoré pour la restauration lors de la génération pour UWP - [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 rompt l’installation d’EntityFramework ? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Ajouter la source à la journalisation détaillée (à prendre en compte pour 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Paramètre NoCache non respecté dans la version 3.4+ du client nuget - [#3074](https://github.com/NuGet/Home/issues/3074)

- Quand le chargement d’un fournisseur d’informations d’identification dans Visual Studio échoue, ne rompez pas NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Fonctionnalités

- Configurer CI pour exécuter x86 - [#3868](https://github.com/NuGet/Home/issues/3868)

- Restauration automatique 3/3 : interface utilisateur non bloquante - [#3658](https://github.com/NuGet/Home/issues/3658)

- Restauration automatique 2/3 : restauration en arrière-plan sur nomination - [#3657](https://github.com/NuGet/Home/issues/3657)

- Restaurer les références de projet pour qu’elles correspondent au comportement de build (récursivité) - [#3615](https://github.com/NuGet/Home/issues/3615)

- Prise en charge de DPL dans Visual Studio « 15 » - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- Déplacement du fichier de paramètres vers Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)

- Les cibles et les propriétés de restauration générées ont besoin d’une prise en charge de la participation au ciblage croisé - [#3496](https://github.com/NuGet/Home/issues/3496)

- Prise en charge de la restauration NuGet pour PackageTargetFallback (fonctionnalité Importations) - [#3494](https://github.com/NuGet/Home/issues/3494)

- Implémentation de ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 pour un RID - [#3465](https://github.com/NuGet/Home/issues/3465)

- Prise en charge de l’ajout/suppression/mise à jour de PackageRefs dans l’interface utilisateur de NuGet - [#3457](https://github.com/NuGet/Home/issues/3457)

- Restauration automatique 1/3 : Implémentation de l’API de nomination par le biais de la mise en cache des informations de restauration de projet - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] Tâches et cibles de restauration NuGet - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] Activation de la restauration au niveau de la solution dans MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)

- Prise en charge de l’extensibilité publique du fournisseur d’informations d’identification dans Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)

- Restauration nuget récursive - [#2533](https://github.com/NuGet/Home/issues/2533)

- Impossible de charger Microsoft.TeamFoundation.Client sur dev15. Nécessité de mettre à jour Microsoft.TeamFoundation.Client vers la version 15.0 pour Visual Studio « 15 » Preview - [#2392](https://github.com/NuGet/Home/issues/2392)

- Impossible d’installer un package C++ dans un projet UWP C++ dans Visual Studio « 15 » Preview - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg doit prendre en charge le dossier \buildCrossTargeting\ et importer `.targets` / `.props` pour le « ciblage croisé » de l’étendue MSBuild. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Conception de ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)

- Correction de l’interface utilisateur de NuGet pour prendre en charge la restauration avec PackageReferences dans `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)

- Ajout du bouton Effacer le cache aux paramètres du Gestionnaire de package VS - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCR

- La restauration de solution doit être bloquée pendant la restauration automatique. - [#3797](https://github.com/NuGet/Home/issues/3797)

- L’installation de NetCore à partir de l’interface utilisateur du Gestionnaire de Package NuGet effectue une installation sur chaque TFM, au lieu de ceux pris en charge par le package - [#3721](https://github.com/NuGet/Home/issues/3721)

- L’API de nominateur de restauration doit aussi prendre en charge DotNetCliToolsReferences. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Marquer notre vsix Visual Studio « 15 » en tant que systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)

- Migrer du référencement de MS.VS.Services.Client vers MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) doit être respecté au niveau du projet par la restauration - [#3618](https://github.com/NuGet/Home/issues/3618)

- La restauration dans un projet avec TargetFramework unique ne doit pas conditionner les propriétés - [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet restore3 foo.csproj doit suivre les dépendances projectref et les restaurer aussi. Comme la build. - [#3577](https://github.com/NuGet/Home/issues/3577)

- Dépendances « type » : « plateforme » représentées en tant que « type » : « package » dans le fichier de verrouillage - [#2695](https://github.com/NuGet/Home/issues/2695)

- Le mode détaillé NuGet.exe doit afficher l’URL de téléchargement - [#2629](https://github.com/NuGet/Home/issues/2629)

- Déplacer NuGet xplat vers Microsoft.NetCore.App et netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push - Il devrait être possible de remplacer le serveur de symboles lors d’une opération Push à partir de la ligne de commande - [#2348](https://github.com/NuGet/Home/issues/2348)

- Consolider le code pour la recherche du chemin de packages global - [#2296](https://github.com/NuGet/Home/issues/2296)

- Il faut un meilleur nom que suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)

- Déterminer le nom de la dépendance `project.json` à utiliser pour les projets MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)

- Ajout de la prise en charge de SemVer 2.0.0 à NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- Autoriser la disponibilité de la dépendance transitive NuPkgs avec `.targets` dans MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)

- La restauration NuGet à partir de la ligne de commande est beaucoup plus lente que VS - [#3330](https://github.com/NuGet/Home/issues/3330)

- Faire en sorte que la comparaison de version et d’ID de package respecte la casse - [#2522](https://github.com/NuGet/Home/issues/2522)

- L’option NoCache ne fonctionne pas pour la restauration/installation basée sur `packages.config` (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)

- Les ressources FindPackageByIdResource ont besoin d’un enregistreur d’événements et d’un contexte de cache par défaut - [#1357](https://github.com/NuGet/Home/issues/1357)
