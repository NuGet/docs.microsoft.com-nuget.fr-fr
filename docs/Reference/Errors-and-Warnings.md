---
title: "Restauration des erreurs et avertissements référence NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Informations de référence complètes pour les avertissements et erreurs émises à partir de NuGet pendant la restauration de package"
keywords: Erreurs de NuGet, les avertissements de NuGet, les diagnostics
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
ms.openlocfilehash: 9e22b63636980ce64017c950148d9005bf9c2fb1
ms.sourcegitcommit: ed01eaeef9bf488c36556b97247ca440384c0242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a>Erreurs et avertissements

Dans NuGet 4.3.0, erreurs et avertissements sont numérotées comme décrit dans cette rubrique et fournissent des informations détaillées pour vous aider à résoudre les problèmes rencontrés. 

Les erreurs et les avertissements répertoriés ici sont uniquement disponibles avec [basée sur les PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) NuGet 4.3.0 et projets. NuGet honore également des propriétés MSBuild pour supprimer les avertissements ou les élever à erreurs. Pour plus d’informations, consultez [Comment : supprimer les avertissements du compilateur](/visualstudio/ide/how-to-suppress-compiler-warnings) dans la documentation de Visual Studio.

**Erreurs**

| Regrouper | Numéros d’erreur |
| --- | --- |
| [Erreurs d’entrée non valides](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Erreurs de package et de projet manquants](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (précédemment NU1607) [NU1108](#nu1108) (précédemment NU1606) |
| [Erreurs de compatibilité](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**Avertissements**

| Regrouper | Numéros d’avertissement |
| --- | --- |
| [Avertissements d’entrée non valides](#invalid-input-warnings) | [NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503) |
| [Avertissements de version de package inattendue](#unexpected-package-version-warnings) | [NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605) |
| [Avertissements de conflit de programme de résolution](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [Avertissements de secours de package](#package-fallback-warnings) | [NU1701](#nu1701) |
| [Flux d’avertissements](#feed-warnings) | [NU1801](#nu1801) |
| [Avertissements et erreurs internes de NuGet](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |

## <a name="invalid-input-errors"></a>Erreurs d’entrée non valides

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problème** | Le projet ne contient pas une ou plusieurs infrastructures. |
| **Causes courantes** | Le projet ne contient pas un `TargetFramework` ou `TargetFrameworks` propriété. |
| **Exemple de message** | *Le projet projA ne spécifie pas les versions .NET Framework cible dans c:\tmp\projA.csproj* |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problème** | Combinaison non valide d’entrées avec un mot clé clair. |
| **Causes courantes** | CLEAR ne peut pas être combiné avec d’autres entrées. |
| **Exemple de message** | *« CLAIR » ne peut pas être utilisé conjointement avec d’autres valeurs* |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problème** | `PackageTargetFallback`et `AssetTargetFallback` fournir un comportement différent pour la sélection des ressources et ne peut pas être utilisées ensemble. |
| **Causes courantes** | Les deux `PackageTargetFallback` et `AssetTargetFallback` existent dans le projet. |
| **Exemple de message** | *PackageTargetFallback et AssetTargetFallback ne peuvent pas être utilisées ensemble. Supprimez les références de PackageTargetFallback(deprecated) à partir de l’environnement de projet.* |

## <a name="missing-package-and-project-errors"></a>Erreurs de package et de projet manquants

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problème** | Un groupe de dépendances ne pas être résolu. Il s’agit d’un problème générique pour les types qui ne sont pas des packages ou des projets. |
| **Causes courantes** | Le projet contient une dépendance sur un élément qui n’existe pas. |
| **Exemple de message** | *Impossible de résoudre System.Missing pour net45* |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problème** | Impossible de trouver le package sur des sources. |
| **Causes courantes** | La source du package approprié est manquante ou l’identificateur de package est incorrect. |
| **Exemple de message** | *Impossible de trouver le package System.Missing. Aucun package n’existe avec cet id de source (s) : dotnet cœur, roslyn-dotnet, nuget.org* |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problème** | L’identificateur du package est trouvé, mais une version dans la plage de dépendance spécifié est introuvable sur une des sources. |
| **Causes courantes** | La source du package approprié est manquante ou la plage de dépendance est incorrecte. La plage peut être spécifiée par un package et non à l’utilisateur. L’utilisateur peut être amené à basculer vers une version disponible si ce package est référencé directement par le projet. |
| **Exemple de message** | *Impossible de trouver le package NuGet.Versioning avec la version (> = 9.0.1)<br/> -30 de trouvé ou les versions dans nuget.org [plus proche de la version : 4.0.0]<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -trouvé le 9 versions dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032]<br/> -trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet* |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problème** | Aucune version stable ont été trouvées dans la plage de dépendance. Versions préliminaires ont été trouvées, mais ne sont pas autorisées. |
| **Causes courantes** | Le projet spécifié une version stable pour la plage de dépendance. Les utilisateurs doivent modifier la plage de versions pour inclure les versions préliminaires. |
| **Exemple de message** | *Impossible de trouver un package stable NuGet.Versioning avec la version (> = 3.0.0)<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -versions 9 de trouvé dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032] <br/> -Trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet* |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problème** | Un ProjectReference pointe vers un fichier qui n’existe pas. |
| **Causes courantes** | Il manque le fichier projet à partir du disque ou la référence est incorrecte. |
| **Exemple de message** | *Référence de projet n’existe pas de 'c:\a.csproj'. Vérifiez que la référence de projet est valide et que le fichier projet existe.* |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problème** | Le fichier de projet existe mais aucune information de restauration a été fournie pour celui-ci. |
| **Causes courantes** | Dans Visual Studio, cela peut signifier que le projet est déchargé. À partir de la ligne de commande, cela peut signifier que le fichier est endommagé ou qu’il ne contient pas personnalisé après la cible d’importations nécessaire pour la restauration lire le projet. |
| **Exemple de message** | *Impossible de lire les informations de projet pour 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.* |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problème** | Contraintes de dépendances ne peut pas être résolus. |
| **Causes courantes** | Les packages contiennent la dépendance sur les versions exactes d’un package au lieu de plages ouvertes. |
| **Exemple de message** | *Impossible de satisfaire les requêtes en conflit pour {id} : {chemin d’accès de conflit} Framework : {graphique cible}* |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a>NU1107 (précédemment NU1607)

| | |
| --- | --- |
| **Problème** | Impossible de résoudre les contraintes de dépendances entre les packages. |
| **Causes courantes** | Les packages avec des contraintes de dépendance sur les versions exactes ne permettent pas d’autres packages d’augmenter la version, si nécessaire. |
| **Exemple de message** | *Conflit de version détecté pour NuGet.Versioning. Référencer le package directement à partir du projet pour résoudre ce problème.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (précédemment NU1606)

| | |
| --- | --- |
| **Problème** | Une dépendance circulaire a été détectée. |
| **Causes courantes** | Un package a été créé correctement. |
| **Exemple de message** | *Cycle détecté : A -> B -> A* |

## <a name="compatibility-errors"></a>Erreurs de compatibilité

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problème** | Un projet de dépendance ne contient pas une infrastructure compatible avec le projet actuel. |
| **Causes courantes** | La version du projet cible est une version supérieure à celle du projet de consommation. |
| **Exemple de message** | *Projet WAN n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Project prend en charge WAN :<br/> -netstandard1.6 (. NETStandard, Version = version 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = version 1.0)* |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problème** | Un package de dépendance ne contient pas toutes les ressources compatibles avec le projet. |
| **Causes courantes** | Le package ne prend pas en charge la version du projet cible. |
| **Exemple de message** | *Package System.ComponentModel.EventBasedAsync 4.0.11 n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Package prend en charge System.ComponentModel.EventBasedAsync 4.0.11 :<br/> -monoandroid10 (MonoAndroid, Version = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (. NETFramework, Version = v4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. NETStandard, Version = v1.0)<br/> -portable-net45 + 8 + wp8 + wpa81 (. NETPortable, Version = v0.0, profil = Profile259)<br/> -win8 (Windows, Version = v8.0)<br/> -wp8 (WindowsPhone, Version = v8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v8.1)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problème** | Le package ne prend pas en charge du projet `RuntimeIdentifier`. |
| **Causes courantes** | Le package ne prend pas en charge en cours `RuntimeIdentifier`. Modifier la `RuntimeIdentifier` valeurs utilisées dans le projet si nécessaire. |
| **Exemple de message** | *System.Example 1.0.0 fournit un assembly de référence de la compilation pour.dll sur net461, mais il n’existe aucun assembly au moment de l’exécution compatible.* |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problème** | Le package requiert des fonctionnalités ou des structures non prises en charge par la version installée de NuGet. |
| **Causes courantes** | Mettre à niveau NuGet pour résoudre le problème. |
| **Exemple de message** | *Le package 'NuGet.Versioning' nécessite '5.0.0' version du client de NuGet ou version ultérieure, mais la version NuGet actuelle est '4.3.0'. Pour mettre à niveau NuGet, accédez à http://docs.nuget.org/consume/installing-nuget.* |

## <a name="invalid-input-warnings"></a>Avertissements d’entrée non valides

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problème** | La restauration du projet tente de fonctionner sur n’a été trouvé. |
| **Causes courantes** | Le projet est manquant. |
| **Exemple de message** | *Le dossier 'c:\projects\a' ne contient pas de projet à restaurer.* |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problème** | `RuntimeSupports`contient un profil non valide. |
| **Causes courantes** | Le profil prend en charge est introuvable dans un `runtime.json` fichier issues des packages de dépendance actuel. |
| **Exemple de message** | *Profil de compatibilité inconnu : aaa* |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problème** | Un projet de dépendance n’importe pas les cibles de restauration de NuGet. Cela revient à NU1105 mais ici le projet est ignoré et ignorés au lieu de provoquer l’échec de restauration tous. Dans les solutions complexes il existe souvent des autres types de projets qui n’acceptent pas de restauration. |
| **Causes courantes** | Cela peut se produire pour les projets qui n’importent pas de propriétés/cibles communes qui importer automatiquement la restauration. Si le projet n’a pas besoin d’être restauré ce message peut être ignoré. |
| **Exemple de message** | *Ignorer la restauration de projet 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.* |

## <a name="unexpected-package-version-warnings"></a>Avertissements de version de package inattendue

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problème** | Une dépendance directe a été agrandir à une version plus élevée que le projet spécifié. |
| **Causes courantes** | Un autre package de dépendance requis d’une version ultérieure et augmenté le package. |
| **Exemple de message** | *Dépendance spécifiée était NuGet.Versioning (> = 3.5.0), mais se terminait avec NuGet.Versioning 4.0.0.* |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problème** | Une dépendance de package est manquant dans une limite inférieure. Cela n’autorise pas la restauration rechercher la *meilleure correspondance*. Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée. Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur. |
| **Causes courantes** | Il s’agit généralement d’un erreur de création de package. |
| **Exemple de message** | *NuGet.Packaging 4.0.0 ne fournit pas une limite inférieure inclusive de dépendance NuGet.Versioning (3.5.0 >). Une meilleure correspondance approximative de 3.6.0 a été résolue.* |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problème** | Une dépendance de package spécifié une version qui est introuvable. Une version ultérieure a été utilisée à la place, ce qui diffère du package qui a été créé par rapport à.<br/><br/>Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*. Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée. Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur. |
| **Causes courantes** | Les sources de package ne contiennent pas de la version attendue limite inférieure. Si le package attendu n’a pas été lancé. Cela peut être un erreur de création de package. |
| **Exemple de message** | NuGet.Packaging 4.0.0 dépend NuGet.Versioning (> = 4.0.0) mais 4.0.0 n’a pas été trouvé. Une meilleure correspondance approximative de 5.0.0 a été résolue. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problème** | Une dépendance de projet ne définit pas une limite inférieure.<br/><br/>Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*. Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée. Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur. |
| **Causes courantes** | Du projet *PackageReference* *Version* attribut doit être mis à jour pour inclure une limite inférieure. |
| **Exemple de message** | *Projet dépendance NuGet.Versioning (< = 9.0.0) doe ne contient pas une limite inférieure inclusive. Inclure une limite inférieure dans la version de dépendance pour garantir des résultats de la restauration de cohérence.* |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problème** | Un package de dépendance spécifié une contrainte de version sur une version supérieure d’un package au restauration finalement réduite. |
| **Causes courantes** | Wins le plus proche lors de la résolution des packages. Un package plus proche dans le graphique peut avoir substitution un package distant. |
| **Exemple de message** | *Détecté vers une version antérieure du package : NuGet.Versioning de 4.0.0 vers la version 3.5.0. Référencer le package directement à partir du projet pour sélectionner une autre version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |

## <a name="resolver-conflict-warnings"></a>Avertissements de conflit de programme de résolution

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problème** | Un package de résolution est supérieur à ce qui permet à une contrainte de dépendance. Dans certains cas, cela est intentionnel et l’avertissement peut être supprimé. |
| **Causes courantes** | Un package référencé directement par un projet remplacera les contraintes de dépendance à partir d’autres packages.   |
| **Exemple de message** | *Version du package détectés en dehors de la contrainte de dépendance : x 1.0.0 requiert y (= 1.0.0), mais la version y 2.0.0 a été résolue.* |

## <a name="package-fallback-warnings"></a>Avertissements de secours de package

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problème** | *PackageTargetFallback/AssetTargetFallback* a été utilisé pour sélectionner des éléments multimédias à partir d’un package. Il s’agit d’un avertissement pour informer l’utilisateur que les ressources ne peuvent pas être de 100 % compatible. |
| **Causes courantes** | Le package ne prend pas en charge l’infrastructure du projet. |
| **Exemple de message** | *Package 'NuGet.Versioning' a été restauré à l’aide de « portable-net45 + win8 » à la place le framework cible du projet 'netstandard1.5'. Ce package ne peut pas être entièrement compatible avec votre projet.* |

## <a name="feed-warnings"></a>Flux d’avertissements

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problème** | Une erreur s’est produite lors de la lecture du flux lorsque `IgnoreFailedSources` est définie sur true, le convertir en un avertissement non fatale. Il peut contenir n’importe quel message et générique. |
| **Causes courantes** | La source n’est pas valide. |
| **Exemple de message** | N/A |

## <a name="nuget-internal-errors-and-warnings"></a>Avertissements et erreurs internes de NuGet

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problème** | Une erreur interne non spécifique à partir de NuGet. |
| **Causes courantes** | Vérifiez les journaux pour plus d’informations |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problème** | Avertissement interne non spécifique de NuGet. |
| **Causes courantes** | Vérifiez les journaux pour plus d’informations |
