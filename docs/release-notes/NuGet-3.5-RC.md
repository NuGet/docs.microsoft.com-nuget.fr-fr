---
title: 3.5 Notes de publication RC
description: Notes de publication pour NuGet 3.5 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548536"
---
# <a name="nuget-35-rc-release-notes"></a>Notes de version RC de NuGet 3.5

[Notes de publication de NuGet 3.5-Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM de Notes de publication](../release-notes/nuget-3.5-RTM.md)

version 3.5 met l’accent sur l’amélioration de qualité et les performances des clients de NuGet. En outre, nous vous avons envoyé quelques fonctionnalités comme la prise en charge de [dossiers de secours](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) prise en charge dans `.nuspec` et bien plus encore.

[Liste des problèmes](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Correctifs de bogues

* Installation/restauration d’un package échoue avec « Package contient plusieurs `.nuspec` fichiers. » - [#3231](https://github.com/NuGet/Home/issues/3231)

* NuGet pack ajoute volontairement `.tt` fichiers au dossier de contenu quelle - [#3203](https://github.com/NuGet/Home/issues/3203)

* NuGet pack csproj (avec `project.json`) se bloque si l’absence de propriétaire dans le fichier JSON - et packOptions [#3180](https://github.com/NuGet/Home/issues/3180)

* pack de NuGet pour `project.json` ignore les balises packOptions comme résumé, les auteurs, les propriétaires, etc. - [#3161](https://github.com/NuGet/Home/issues/3161)

* pack de NuGet ignore les dépendances dans la sortie `.nuspec` pour `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* La mise à jour de plusieurs packages avec restauration laisse le projet dans un état interrompu - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles si l’une ne sont pas ajoutés pour les projets de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Impossible d’empaqueter bibliothèque ciblant .net Standard correctement - [#3108](https://github.com/NuGet/Home/issues/3108)

* Fichier -> Nouveau projet -> échoue de projet de bibliothèque de classes (Portable) dans VS2015 et Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Erreur de NuGet - 1.0.0-* n’est pas une chaîne de version valide - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ne parvient pas à afficher, mais fonctionne de Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Erreur lors de la « Install-Package jquery.validation » sur dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Lorsque installé Visual Studio 2015 update 3 sur un VS qui utilise NuGet version 3.5.0 erreur - [#3053](https://github.com/NuGet/Home/issues/3053)

* Interface utilisateur du Gestionnaire de package : n’affiche pas nouvelle version après la mise à jour un package- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey sur la ligne de commande de suppression n’est pas en lecture/envoyé dans 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Chaîne incorrecte : une version stable d’un package ne doit pas avoir sur une dépendance préliminaire. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Création get de projet de bibliothèque de classes portable (net46 et windows 10) des exceptions nullref pour. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Mise à jour de NuGet doit fournir de message d’information lorsqu’une version supérieure est limitée par la contrainte d’allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Plug-in informations d’identification s’est arrêté avec l’erreur -1 / erreur lors du téléchargement du package lors de l’utilisation de fournisseurs d’informations d’identification avec plusieurs sources - [#2885](https://github.com/NuGet/Home/issues/2885)

* NuGet pack - dépendance de package Newtonsoft.Json manquant - [#2876](https://github.com/NuGet/Home/issues/2876)

* Bogue dans ExecuteSynchronizedCore sur Linux/Mac OS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* Visual Studio ne prend pas en charge les variables d’environnement dans repositoryPath (nuget.exe fait) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Résoudre les problèmes d’accessibilité - [#2745](https://github.com/NuGet/Home/issues/2745)

* Les infrastructures portables avec des profils de trait d’union sont rejetées. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Gestionnaire de package NuGet doit indiquer clairement cette liste d’options dans les packages de détail ne s’applique pas aux `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Mise à jour de NuGet 3.3.0 échoue avec «... une contrainte supplémentaire défini dans packages.config empêche cette opération. » - [#1816](https://github.com/NuGet/Home/issues/1816)

* L’installation du package à partir d’une source locale qui n’existe pas lève un message erroné - [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtre de « Mise à niveau disponibles » affiche les mises à niveau qui violent la contrainte de version - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Amélioration des performances

* Performances : Améliorer les ContentModel target framework d’analyse - [#3162](https://github.com/NuGet/Home/issues/3162)

* Performances : Éviter lecture `runtime.json` fichiers pour les restaurations qui n’ont pas d’identificateurs RID [#3150](https://github.com/NuGet/Home/issues/3150). Sur les ordinateurs de l’élément de configuration, restauration d’un exemple de Qu'application Web ASP.NET est réduite de plus 15 secondes / 3 secondes.

* Performances : Temps de chargement Console du Gestionnaire de Package init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956). Temps nécessaire pour ouvrir PackageManagerConsole améliorées dans certains cas, à partir de 132s, de 10 s.

* Résoudre les problèmes de performances de ReSharper de mise à jour de NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): sur un exemple de projet, temps nécessaire pour installer les packages réduit de 140s à 68s.

## <a name="dcrs"></a>DCR

* NuGet a besoin informer les utilisateurs que la mise à niveau/installation dans un moniker du Framework cible dotnet en bibliothèque de classes portable peut entraîner des problèmes - [#3138](https://github.com/NuGet/Home/issues/3138)

* Avertir l’installation/mise à niveau incorrect pour le projet avec le moniker du Framework cible = « dotnet » - [#3137](https://github.com/NuGet/Home/issues/3137)

* Ajouter une prise en charge netcoreapp11 et netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Imprimer le contenu de l’en-tête dans la console dans nuget.exe - NuGet-avertissement [#2934](https://github.com/NuGet/Home/issues/2934)

* Attribut de AssemblyMetadata tirer parti pour `.nuspec` jeton remplacements - [#2851](https://github.com/NuGet/Home/issues/2851)

* Supprimer la propriété verrouillée le fichier de verrouillage - [#2379](https://github.com/NuGet/Home/issues/2379)

* Packages de symboles ne doivent pas déjà utilisés dans l’installation ou mettre à jour #2807

## <a name="features"></a>Fonctionnalités

* Prise en charge des dossiers de package de secours - [#2899](https://github.com/NuGet/Home/issues/2899)

* Concevez et implémentez une notion de type de package pour prendre en charge les packages de l’outil - [#2476](https://github.com/NuGet/Home/issues/2476)

* API pour obtenir le chemin d’accès au dossier de packages globaux - [#2403](https://github.com/NuGet/Home/issues/2403)

* Prise en charge - mettre à jour les packages natifs [#1291](https://github.com/NuGet/Home/issues/1291)
