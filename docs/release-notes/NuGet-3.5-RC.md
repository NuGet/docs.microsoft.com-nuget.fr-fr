---
title: Notes de publication de 3,5 RC
description: Notes de publication de NuGet 3,5 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780204"
---
# <a name="nuget-35-rc-release-notes"></a>Notes de publication de NuGet 3,5 RC

Notes de publication [de NuGet 3,5-bêta2](../release-notes/nuget-3.5-Beta2.md)  |  [Notes de publication de NuGet 3,5-RTM](../release-notes/nuget-3.5-RTM.md)

la version 3,5 est axée sur l’amélioration de la qualité et des performances des clients NuGet. En outre, nous avons fourni quelques fonctionnalités telles que la prise en charge des [dossiers de secours](https://github.com/NuGet/Home/issues/2899), la prise en charge de [PackageType](https://github.com/NuGet/Home/issues/2476) dans `.nuspec` et bien plus encore.

[Liste des problèmes](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Résolutions de bogues

* L’installation/la restauration d’un package échoue avec « le package contient plusieurs `.nuspec` fichiers ». - [#3231](https://github.com/NuGet/Home/issues/3231)

* le Pack NuGet ajoute `.tt` de force aux fichiers dans le dossier de contenu, quelle que soit la [#3203](https://github.com/NuGet/Home/issues/3203)

* NuGet Pack csproj (avec `project.json` ) se bloque s’il n’existe aucun packOptions et propriétaire dans le fichier JSON- [#3180](https://github.com/NuGet/Home/issues/3180)

* le Pack NuGet pour `project.json` ignore les balises packOptions comme Summary, Authors, Owners, etc. [#3161](https://github.com/NuGet/Home/issues/3161)

* le Pack NuGet ignore les dépendances dans la sortie `.nuspec` pour `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* La mise à jour de plusieurs packages avec la restauration laisse le projet dans un État rompu, [#3139](https://github.com/NuGet/Home/issues/3139)

* Les ContentFiles sous n’importe lequel ne sont pas ajoutés pour les projets netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)

* Impossible de regrouper correctement la bibliothèque .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)

* Fichier > nouveau projet de bibliothèque de classes de > (portable) échoue dans VS2015 et Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Erreur NuGet-1.0.0-* n’est pas une chaîne de version valide- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ne parvient pas à s’afficher mais Install-Package Works [#3068](https://github.com/NuGet/Home/issues/3068)

* Erreur lorsque « Install-Package jQuery. validation » sur dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* Lors de l’installation de VS 2015 Update 3 sur un VS qui utilise une erreur NuGet version 3.5.0 se produit- [#3053](https://github.com/NuGet/Home/issues/3053)

* Interface utilisateur du gestionnaire de package : n’affiche pas la nouvelle version après la mise à jour d’un package- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey sur la ligne de commande de suppression n’est pas en lecture/envoi dans 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Chaîne incorrecte : une version stable d’un package ne doit pas avoir une dépendance de préversion. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Création d’une exception de NullRef de projet PCL (net46 et Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* La mise à jour NuGet doit fournir un message informatif quand une version supérieure est limitée par la contrainte allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)

* [#2885](https://github.com/NuGet/Home/issues/2885) le plug-in des informations d’identification s’est arrêté avec l’erreur 1/erreur lors du téléchargement du package lors de l’utilisation de fournisseurs d’informations d’identification avec plusieurs sources

* Pack NuGet-Newtonsoft.Jsmanquant sur la dépendance du package- [#2876](https://github.com/NuGet/Home/issues/2876)

* Bogue dans ExecuteSynchronizedCore sur Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)

* VS ne prend pas en charge les variables d’environnement dans repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* Résoudre les problèmes d’accessibilité- [#2745](https://github.com/NuGet/Home/issues/2745)

* Les infrastructures portables avec des profils avec trait d’Union sont rejetées. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Le gestionnaire de package NuGet doit faire en sorte qu’il soit clair que les options Lister les détails des packages ne s’appliquent pas à `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* La mise à jour NuGet 3.3.0 échoue avec «une contrainte supplémentaire... défini dans packages.config empêche cette opération.» - [#1816](https://github.com/NuGet/Home/issues/1816)

* L’installation d’un package à partir d’une source locale qui n’existe pas lève une fausse [#1674](https://github.com/NuGet/Home/issues/1674) de messages

* Le filtre « mettre à niveau une mise à jour » affiche des mises à niveau qui violent la contrainte de version- [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Optimisation des performances

* Performances : améliorer l’analyse du Framework cible ContentModel- [#3162](https://github.com/NuGet/Home/issues/3162)

* Performances : Évitez `runtime.json` de lire des fichiers pour les restaurations qui n’ont pas de rid [#3150](https://github.com/NuGet/Home/issues/3150). Sur les machines CI, la restauration d’un exemple d’application Web ASP.NET est réduite de plus de 15 secondes à 3 secondes.

* Performances : la console du gestionnaire de package init.ps1 temps de chargement [#2956](https://github.com/NuGet/Home/issues/2956). La durée d’ouverture de PackageManagerConsole a été améliorée dans certains cas, de 132s à 10s.

* Résolvez les problèmes de performances resharpers dans NuGet Update- [#3044](https://github.com/NuGet/Home/issues/3044): sur un exemple de projet, temps nécessaire pour installer les packages réduits de 140s à 68s.

## <a name="dcrs"></a>DCR

* NuGet doit permettre aux utilisateurs de savoir que la mise à niveau/installation dans un PCL basé sur dotnet TFM peut provoquer des problèmes [#3138](https://github.com/NuGet/Home/issues/3138)

* Signaler une installation/mise à niveau incorrecte pour le projet w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Ajouter la prise en charge de netcoreapp11 et netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)

* Imprimer le contenu de l’en-tête NuGet-Warning sur la console dans nuget.exe [#2934](https://github.com/NuGet/Home/issues/2934)

* Tirer parti de l’attribut AssemblyMetadata pour les `.nuspec` remplacements de jetons- [#2851](https://github.com/NuGet/Home/issues/2851)

* Supprimez la propriété locked du fichier de verrouillage- [#2379](https://github.com/NuGet/Home/issues/2379)

* Les packages de symboles ne doivent jamais être utilisés dans l’installation ou la mise à jour #2807

## <a name="features"></a>Fonctionnalités

* Prise en charge des dossiers de package de secours- [#2899](https://github.com/NuGet/Home/issues/2899)

* Concevez et implémentez une notion de type de package pour prendre en charge les packages d’outils- [#2476](https://github.com/NuGet/Home/issues/2476)

* API permettant d’accéder au dossier des packages globaux- [#2403](https://github.com/NuGet/Home/issues/2403)

* Prise en charge des mises à jour des packages natifs- [#1291](https://github.com/NuGet/Home/issues/1291)
