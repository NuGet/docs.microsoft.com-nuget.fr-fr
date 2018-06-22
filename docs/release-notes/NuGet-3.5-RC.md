---
title: 3.5 Notes de publication RC
description: Notes de publication pour RC 3.5 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d620a8b8d97f9a52cb2bc93a91eb393130a42898
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2018
ms.locfileid: "32044777"
---
# <a name="nuget-35-rc-release-notes"></a>Notes de version RC de NuGet 3.5

[Notes de version 3.5 à la bêta 2 de NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM de Notes de publication](../release-notes/nuget-3.5-RTM.md)

version 3.5 met l’accent sur l’amélioration de la qualité et les performances des clients NuGet. En outre, nous vous avons envoyé certaines fonctionnalités comme la prise en charge de [dossiers secours](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) prise en charge dans `.nuspec` et bien plus encore.

[Liste des problèmes](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Correctifs de bogues

* Installation/restauration d’un package échoue avec « Package contient plusieurs `.nuspec` fichiers. » - [#3231](https://github.com/NuGet/Home/issues/3231)

* pack de NuGet ajoute force `.tt` fichiers au dossier de contenu quelle - [#3203](https://github.com/NuGet/Home/issues/3203)

* NuGet pack csproj (avec `project.json`) se bloque si aucun packOptions et le propriétaire du fichier JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* pack de NuGet pour `project.json` ignore les balises packOptions comme résumé, les auteurs, les propriétaires, etc. - [#3161](https://github.com/NuGet/Home/issues/3161)

* pack de NuGet ignore les dépendances dans la sortie `.nuspec` pour `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Mise à jour de plusieurs packages avec restauration laisse le projet dans un état interrompu - [#3139](https://github.com/NuGet/Home/issues/3139)

* Les fichiers associés ne sont pas ajoutés pour les projets de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Ne peut pas empaqueter bibliothèque ciblant .net Standard correctement - [#3108](https://github.com/NuGet/Home/issues/3108)

* Fichier -> Nouveau projet -> Échec de projet de bibliothèque de classes (Portable) dans VS2015 et Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Erreur de nuGet - 1.0.0-* n’est pas une chaîne de version valide - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ne parvient pas à l’affichage mais works d’Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Erreur lors de la « Install-Package jquery.validation » sur dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Lorsque installé Visual Studio 2015 update 3 sur un VS par NuGet version 3.5.0 erreur - [#3053](https://github.com/NuGet/Home/issues/3053)

* Interface utilisateur du Gestionnaire de package : n’affiche pas nouvelle version après mise à jour d’un package- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey sur la ligne de commande de suppression n’est pas en lecture/envoyé dans 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Chaîne incorrect : version finale d’un package ne doit pas avoir sur une dépendance de version préliminaire. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Création de get de projet de bibliothèque de classes portables (net46 et windows 10) NullRef exception. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Mise à jour de NuGet doit fournir de message d’information lorsqu’une version plus récente est restreinte par la contrainte d’allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Plug-in d’informations d’identification s’est arrêté avec l’erreur -1 / erreur téléchargement du package lors de l’utilisation de fournisseurs d’informations d’identification avec plusieurs sources - [#2885](https://github.com/NuGet/Home/issues/2885)

* pack de NuGet - dépendance de package manquant de Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)

* Bogue dans ExecuteSynchronizedCore sur Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* Visual Studio ne prend pas en charge les variables d’environnement dans repositoryPath (nuget.exe fait) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Résoudre les problèmes d’accessibilité - [#2745](https://github.com/NuGet/Home/issues/2745)

* Les infrastructures portables avec des profils de trait d’union sont rejetées. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Gestionnaire de package NuGet doit indiquer clairement que liste d’options dans les packages de détail ne s’applique pas aux `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Échec de la mise à jour de NuGet 3.3.0 avec ' une contrainte supplémentaire... défini dans packages.config empêche cette opération. » - [#1816](https://github.com/NuGet/Home/issues/1816)

* L’installation du package à partir d’une source locale qui n’existe pas lève un message erroné - [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtre de « Mise à niveau disponibles » affiche les mises à niveau qui violent la contrainte de version - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Amélioration des performances

* Performances : Améliorer les ContentModel framework cible analyse - [#3162](https://github.com/NuGet/Home/issues/3162)

* Performances : Éviter la lecture `runtime.json` fichiers pour les restaurations qui n’ont pas d’identificateurs RID [#3150](https://github.com/NuGet/Home/issues/3150). Sur les ordinateurs de l’élément de configuration, restauration d’un exemple de Qu'application Web ASP.NET réduite plus de 15 secondes à 3 secondes.

* Performances : Temps de chargement Package Manager Console init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956). Temps nécessaire pour ouvrir PackageManagerConsole améliorées dans certains cas de 132s à 10 s.

* Résoudre les problèmes de performances ReSharper de mise à jour de NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): sur un exemple de projet, temps nécessaire pour installer des packages réduite de 140s à 68s.

## <a name="dcrs"></a>DCR

* NuGet a besoin informer les utilisateurs que la mise à niveau/installation dans un tfm dotnet basé PCL peut entraîner des problèmes - [#3138](https://github.com/NuGet/Home/issues/3138)

* Avertir l’installation/mise à niveau incorrect pour le projet avec tfm = « dotnet » - [#3137](https://github.com/NuGet/Home/issues/3137)

* Ajouter la prise en charge netcoreapp11 et netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Imprimer le contenu d’en-tête NuGet-avertissement dans la console de nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Attribut de AssemblyMetadata tirent parti de `.nuspec` jeton remplacements - [#2851](https://github.com/NuGet/Home/issues/2851)

* Supprimez la propriété verrouillée le fichier de verrouillage - [#2379](https://github.com/NuGet/Home/issues/2379)

* Packages de symboles ne doivent pas déjà utilisés dans l’installation ou mettre à jour #2807

## <a name="features"></a>Fonctionnalités

* Prise en charge des dossiers de package de secours - [#2899](https://github.com/NuGet/Home/issues/2899)

* Concevoir et implémenter une notion de type de package pour prendre en charge les packages de l’outil - [#2476](https://github.com/NuGet/Home/issues/2476)

* Pour obtenir le chemin d’accès au dossier packages global - [#2403](https://github.com/NuGet/Home/issues/2403)

* Prise en charge - mettre à jour les packages natifs [#1291](https://github.com/NuGet/Home/issues/1291)
