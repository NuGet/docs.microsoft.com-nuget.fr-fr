---
title: NuGet erreurs et avertissements référence
description: Informations de référence complètes pour les avertissements et erreurs émises à partir de NuGet lors de diverses opérations de NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
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
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 748c2746a61886617e2eefe3e6c4a2e2a5b9d4d3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/22/2018
---
# <a name="errors-and-warnings"></a>Erreurs et avertissements

Dans NuGet 4.3.0+, les erreurs et avertissements sont numérotées comme décrit dans cette rubrique et fournissent des informations détaillées pour vous aider à résoudre les problèmes rencontrés.

Les erreurs et les avertissements répertoriés ici sont uniquement disponibles avec [basée sur les PackageReference](../consume-packages/package-references-in-project-files.md) projets et 4.3.0+ de NuGet. NuGet honore également des propriétés MSBuild pour supprimer les avertissements ou les élever à erreurs. Pour plus d’informations, consultez [Comment : supprimer les avertissements du compilateur](/visualstudio/ide/how-to-suppress-compiler-warnings) dans la documentation de Visual Studio.

**erreurs**

| Regrouper | Numéros d’erreur |
| --- | --- |
| [Erreurs d’entrée non valides](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Erreurs de package et de projet manquants](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (précédemment NU1607) [NU1108](#nu1108) (précédemment NU1606) |
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
| [Packages signés (création et la vérification)](#signed-packages-creation-and-verification)| [NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>Erreurs d’entrée non valides

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problème** | Le projet ne contient pas une ou plusieurs infrastructures. |
| **Exemple de message** | *Le projet projA ne spécifie pas les versions .NET Framework cible dans c:\tmp\projA.csproj* |
| **Solution** | Ajouter un `TargetFramework` ou `TargetFrameworks` propriété au fichier projet spécifié. |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problème** | Combinaison non valide d’entrées avec un mot clé clair. |
| **Exemple de message** | *« CLAIR » ne peut pas être utilisé conjointement avec d’autres valeurs* |
| **Solution** | Utilisez en lui-même et omettre toutes les autres entrées. |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problème** | `PackageTargetFallback` et `AssetTargetFallback` fournir un comportement différent pour la sélection des ressources et ne peut pas être utilisées ensemble. |
| **Exemple de message** | *PackageTargetFallback et AssetTargetFallback ne peuvent pas être utilisées ensemble. Supprimez les références de PackageTargetFallback(deprecated) à partir de l’environnement de projet.* |
| **Solution** | Supprimer déconseillées `PackageTargetFallback` élément à partir du projet. |

## <a name="missing-package-and-project-errors"></a>Erreurs de package et de projet manquants

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problème** | Un groupe de dépendances ne pas être résolu. Il s’agit d’un problème générique pour les types qui ne sont pas des packages ou des projets. |
| **Exemple de message** | *Impossible de résoudre System.Missing pour net45* |
| **Solution** | Ouvrez le fichier projet et examinez la liste de ses dépendances. Vérifiez que chaque dépendance existe sur les sources de package que vous utilisez, et que le package prend en charge la version du projet cible. |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problème** | Impossible de trouver le package sur des sources. |
| **Exemple de message** | *Impossible de trouver le package System.Missing. Aucun package n’existe avec cet id de source (s) : dotnet cœur, roslyn-dotnet, nuget.org* |
| **Solution** | Examinez les dépendances du projet dans Visual Studio afin de vous assurer que vous utilisez le nombre d’identificateur et la version de package approprié. Assurez-vous également que le [configuration NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifie les sources de package votre s’attendre à être à l’aide. Si vous utilisez des packages qui ont [sémantique le contrôle de version 2.0.0](../reference/package-versioning.md#semantic-versioning-200), assurez-vous que vous utilisez la version 3 de flux, `https://api.nuget.org/v3/index.json`, dans le [configuration NuGet](../consume-packages/Configuring-NuGet-Behavior.md). |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problème** | L’identificateur du package est trouvé, mais une version dans la plage de dépendance spécifié est introuvable sur une des sources. La plage peut être spécifiée par un package et non à l’utilisateur. |
| **Exemple de message** | *Impossible de trouver le package NuGet.Versioning avec la version (> = 9.0.1)<br/> -30 de trouvé ou les versions dans nuget.org [plus proche de la version : 4.0.0]<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -trouvé le 9 versions dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032]<br/> -trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet* |
| **Solution** | Modifiez le fichier projet pour corriger la version du package. Assurez-vous également que le [configuration NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifie les sources de package votre s’attendre à être à l’aide. Vous devrez peut-être modifier la version requeted si ce package est référencé directement par le projet. |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problème** | Le projet spécifié une version stable pour la plage de dépendance, mais aucune version stable a été trouvée dans cette plage. Versions préliminaires ont été trouvées, mais ne sont pas autorisées. |
| **Exemple de message** | *Impossible de trouver un package stable NuGet.Versioning avec la version (> = 3.0.0)<br/> -trouvé les 10 ou les versions dans buildtools-dotnet [plus proche de la version : 4.0.0-rc-2129]<br/> -versions 9 de trouvé dans NuGetVolatile [version la plus proche : 3.0.0-beta-00032] <br/> -Trouvé 0 ou les versions dans core-dotnet<br/> -trouvé 0 ou les versions de roslyn-dotnet* |
| **Solution** |  Modifier la plage de version dans le fichier projet pour inclure les versions préliminaires. Consultez [contrôle de version de Package](../reference/Package-Versioning.md). |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problème** | Un ProjectReference pointe vers un fichier qui n’existe pas. |
| **Exemple de message** | *Référence de projet n’existe pas de 'c:\a.csproj'. Vérifiez que la référence de projet est valide et que le fichier projet existe.* |
| **Solution** | Modifiez le fichier projet pour corriger le chemin d’accès du projet référencé ou pour supprimer la référence totalement si elle n’est plus nécessaire. |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problème** | Le fichier de projet existe mais aucune information de restauration a été fournie pour celui-ci. |
| **Exemple de message** | *Impossible de lire les informations de projet pour 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.* |
| **Solution** | Dans Visual Studio, l’erreur peut signifier que le projet est déchargé, dans les cas de recharger le projet. À partir de la ligne de commande, cela peut signifier que le fichier est endommagé ou qu’il ne contient pas personnalisé « après les importations » cible nécessaire pour la restauration lire le projet. Vérifiez que le fichier projet est valide et qu’il contient une cible « après les importations ». |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problème** | Contraintes de dépendances ne peut pas être résolus. |
| **Exemple de message** | *Impossible de satisfaire les requêtes en conflit pour {id} : {chemin d’accès de conflit} Framework : {graphique cible}* |
| **Solution** | Modifiez le fichier projet pour spécifier les plages plus flexible pour la dépendance plutôt qu’une version exacte. |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (précédemment NU1607)

| | |
| --- | --- |
| **Problème** | Impossible de résoudre les contraintes de dépendances entre les packages. |
| **Exemple de message** | *Conflit de version détecté pour NuGet.Versioning. Référencer le package directement à partir du projet pour résoudre ce problème.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |
| **Solution** | Les packages avec des contraintes de dépendance sur les versions exactes ne permettent pas d’autres packages d’augmenter la version, si nécessaire. Ajoutez une référence au projet directement (dans le fichier projet) avec la version exacte requise. |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (précédemment NU1606)

| | |
| --- | --- |
| **Problème** | Une dépendance circulaire a été détectée. |
| **Exemple de message** | *Cycle détecté : A -> B -> A* |
| **Solution** | Le package a été créé correctement ; Contactez le propriétaire du package pour corriger le bogue. |

## <a name="compatibility-errors"></a>Erreurs de compatibilité

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problème** | Un projet de dépendance ne contient pas une infrastructure compatible avec le projet actuel. En règle générale, la version du projet cible est une version supérieure à celle du projet de consommation. |
| **Exemple de message** | *Projet WAN n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Project prend en charge WAN :<br/> -netstandard1.6 (. NETStandard, Version = version 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = version 1.0)* |
| **Solution** | Modifier le framework du projet cible à une version inférieure ou égale à celle du projet de consommation. |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problème** | Un package de dépendance ne contient pas toutes les ressources compatibles avec le projet. |
| **Exemple de message** | *Package System.ComponentModel.EventBasedAsync 4.0.11 n’est pas compatible avec netstandard1.3 (. NETStandard, Version = v1.3). Package prend en charge System.ComponentModel.EventBasedAsync 4.0.11 :<br/> -monoandroid10 (MonoAndroid, Version = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (. NETFramework, Version = v4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. NETStandard, Version = v1.0)<br/> -portable-net45 + 8 + wp8 + wpa81 (. NETPortable, Version = v0.0, profil = Profile259)<br/> -win8 (Windows, Version = v8.0)<br/> -wp8 (WindowsPhone, Version = v8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v8.1)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **Solution** | Modifier le framework du projet cible qui prend en charge par le package. |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problème** | Le package ne prend pas en charge du projet `RuntimeIdentifier`. |
| **Exemple de message** | *System.Example 1.0.0 fournit un assembly de référence de la compilation pour.dll sur net461, mais il n’existe aucun assembly au moment de l’exécution compatible.* |
| **Solution** | Modifier la `RuntimeIdentifier` valeurs utilisées dans le projet en fonction des besoins. |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problème** | Le package requiert des fonctionnalités ou des structures non prises en charge par la version installée de NuGet. |
| **Exemple de message** | *Le package 'NuGet.Versioning' nécessite '5.0.0' version du client de NuGet ou version ultérieure, mais la version NuGet actuelle est '4.3.0'.* |
| **Solution** | Installez une version plus récente de NuGet. Consultez [outils clients de l’installation de NuGet](../install-nuget-client-tools.md). |

## <a name="invalid-input-warnings"></a>Avertissements d’entrée non valides

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problème** | La restauration du projet tente de fonctionner sur n’a été trouvé. |
| **Exemple de message** | *Le dossier 'c:\projects\a' ne contient pas de projet à restaurer.* |
| **Solution** | Exécutez nuget restore dans un dossier qui contient un projet. |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problème** | `RuntimeSupports` contient un profil non valide. En règle générale, le profil prend en charge est introuvable dans un `runtime.json` fichier issues des packages de dépendance actuel.|
| **Exemple de message** | *Profil de compatibilité inconnu : aaa* |
| **Solution** | Vérifier la `RuntimeSupports` valeur dans votre projet. |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problème** | Un projet de dépendance n’importe pas les cibles de restauration de NuGet. Cela revient à NU1105 mais ici le projet est ignoré et ignorés au lieu de provoquer l’échec de restauration tous. Dans les solutions complexes il existe souvent des autres types de projets qui n’acceptent pas de restauration. |
| **Exemple de message** | *Ignorer la restauration de projet 'c:\a.csproj'. Le fichier projet est peut-être non valides ou manquantes cibles requises pour la restauration.* |
| **Solution** | Cela peut se produire pour les projets qui n’importent pas de propriétés/cibles communes qui importer automatiquement la restauration. Si le projet n’a pas besoin d’être restauré ce message peut être ignoré. Dans le cas contraire, modifiez le projet affecté pour ajouter des cibles pour la restauration. |

## <a name="unexpected-package-version-warnings"></a>Avertissements de version de package inattendue

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problème** | Une dépendance directe a été agrandir à une version plus élevée que le projet spécifié. |
| **Exemple de message** | *Dépendance spécifiée était NuGet.Versioning (> = 3.5.0), mais se terminait avec NuGet.Versioning 4.0.0.* |
| **Solution** | Mettre à jour la dépendance dans le projet à une version appropriée. |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problème** | Une dépendance de package est manquant dans une limite inférieure. Cela n’autorise pas la restauration rechercher la *meilleure correspondance*. Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée. Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur. |
| **Exemple de message** | *NuGet.Packaging 4.0.0 ne fournit pas une limite inférieure inclusive de dépendance NuGet.Versioning (3.5.0 >). Une meilleure correspondance approximative de 3.6.0 a été résolue.* |
| **Solution** | Il s’agit généralement d’un erreur de création de package. Contactez l’auteur du package pour résoudre le problème. |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problème** | Une dépendance de package spécifié une version qui est introuvable. En règle générale, les sources de package ne contiennent pas de la version attendue limite inférieure. Une version ultérieure a été utilisée à la place, ce qui diffère du package qui a été créé par rapport à.<br/><br/>Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*. Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée. Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur. |
| **Exemple de message** | NuGet.Packaging 4.0.0 dépend NuGet.Versioning (> = 4.0.0) mais 4.0.0 n’a pas été trouvé. Une meilleure correspondance approximative de 5.0.0 a été résolue. |
| **Solution** | Si le package attendu n’a pas été lancé. Cela peut être un erreur de création de package. Contactez l’auteur du package pour résoudre le problème. Si le package a été lancé, puis vérifiez qu’il est disponible sur les sources de package que vous utilisez. Si vous utilisez une source privée, vous devrez peut-être mettre à jour le package sur ce flux. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problème** | Une dépendance de projet ne définit pas une limite inférieure.<br/><br/>Cela signifie que la restauration n’a pas trouvé le *meilleure correspondance*. Chaque restauration flotte vers le bas la tentative de recherche d’une version antérieure qui peut être utilisée. Cela signifie que la restauration est mis en ligne pour vérifier toutes les sources de chaque fois au lieu d’utiliser les packages qui existent déjà dans le dossier du package utilisateur. |
| **Exemple de message** | *Projet dépendance NuGet.Versioning (< = 9.0.0) doe ne contient pas une limite inférieure inclusive. Inclure une limite inférieure dans la version de dépendance pour garantir des résultats de la restauration de cohérence.* |
| **Solution** | Mettre à jour du projet `PackageReference` `Version` attribut à inclure une limite inférieure. |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problème** | Un package de dépendance spécifié une contrainte de version sur une version supérieure d’un package au restauration finalement réduite. Autrement dit, en raison de la « plus proche wins » règle lors de la résolution des packages, un package plus proche dans le graphique peut avoir substitution un package distant. |
| **Exemple de message** | *Détecté vers une version antérieure du package : NuGet.Versioning de 4.0.0 vers la version 3.5.0. Référencer le package directement à partir du projet pour sélectionner une autre version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |
| **Solution** | Ajoutez une référence directe au projet pour la version la plus récente du package que vous souhaitez utiliser. |

## <a name="resolver-conflict-warnings"></a>Avertissements de conflit de programme de résolution

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problème** | Un package résolu est supérieur à ce qui permet à une contrainte de dépendance. Cela signifie qu’un package référencé directement par un projet substitue les contraintes de dépendance à partir d’autres packages.|
| **Exemple de message** | *Version du package détectés en dehors de la contrainte de dépendance : x 1.0.0 requiert y (= 1.0.0), mais la version y 2.0.0 a été résolue.* |
| **Solution** | Dans certains cas, cela est intentionnel et l’avertissement peut être supprimé. Dans le cas contraire, modifiez la référence du projet au package d’élargir ses contraintes de version. |

## <a name="package-fallback-warnings"></a>Avertissements de secours de package

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problème** | `PackageTargetFallback` / `AssetTargetFallback` a été utilisé pour sélectionner des éléments multimédias à partir d’un package. L’avertissement permettre aux utilisateurs de savoir que les ressources ne peuvent pas être de 100 % compatible. |
| **Exemple de message** | *Package 'NuGet.Versioning' a été restauré à l’aide de « portable-net45 + win8 » à la place le framework cible du projet 'netstandard1.5'. Ce package ne peut pas être entièrement compatible avec votre projet.* |
| **Solution** | Modifier le framework du projet cible qui prend en charge par le package. |

## <a name="feed-warnings"></a>Flux d’avertissements

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problème** | Une erreur s’est produite lors de la lecture du flux lorsque `IgnoreFailedSources` est définie sur true, le convertir en un avertissement non fatale. Il peut contenir n’importe quel message et générique. |
| **Exemple de message** | N/A |
| **Solution** | Modifier votre configuration pour spécifier les sources valides. |

## <a name="nuget-internal-errors-and-warnings"></a>Avertissements et erreurs internes de NuGet

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problème** | Une erreur interne non spécifique à partir de NuGet. |
| **Solution** | Vérifiez les journaux pour plus d’informations |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problème** | Avertissement interne non spécifique de NuGet. |
| **Solution** | Vérifiez les journaux pour plus d’informations |

## <a name="signed-packages-creation-and-verification"></a>Packages signés (création et la vérification)

*NuGet 4.6.0+*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **Problème** | Une erreur non spécifique associée à la signature du package et signé la vérification du package. |
| **Solution** | Vérifiez les journaux pour plus d’informations. |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **Problème** | Arguments non valides à un le [sign la commande](../tools/cli-ref-sign.md) ou le [Vérifiez la commande](../tools/cli-ref-verify.md). |
| **Solution** | Vérifiez et corrigez les arguments fournis. |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **Problème** | Le `-Timestamper` option n’a pas été spécifiée avec la [commande de connexion nuget](../tools/cli-ref-sign.md). |
| **Exemple de message** | *Le '-Timestamper' option n’a pas été fournie. Le package signé ne sera pas horodaté.* |
| **Solution** | Spécifiez le `-Timestamper` option avec `nuget sign`. |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **Problème** | Un package non signé a été fourni pour le [nuget Vérifiez la commande](../tools/cli-ref-verify.md). |
| **Solution** | Exécutez `nuget verify` avec un package signé. Consultez [signer un package](../create-packages/Sign-a-Package.md). |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **Problème** | Échec de la vérification d’intégrité de package, ce qui signifie que qu’un package signé a été falsifié depuis en cours de signature. |
| **Solution** | Analyser votre ordinateur avec un logiciel antivirus. Puis supprimez le package à partir de l’ordinateur, réinstallez-le et recommencez l’opération. Si le problème persiste, contactez le propriétaire de la source du package et le package. |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **Problème** | Échec de la génération de chaîne de certificat pour la signature principale. Le certificat de signature principal n’est pas fiable, révoqué, ou les informations de révocation du certificat ne sont pas disponibles. |
| **Exemple de message** | *Avertissement : NU3018 : la fonction de révocation n’a pas pu vérifier la révocation du certificat.* |
| **Solution** | Utiliser un certificat approuvé et valide. Vérifiez la connectivité internet. |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **Problème** | Échec de la génération de la chaîne certificat pour la signature d’horodatage. Le certificat de signature d’horodatage n’est pas fiable, révoqué, ou les informations de révocation du certificat ne sont pas disponibles. |
| **Exemple de message** | *Avertissement : NU3028 : la fonction de révocation n’a pas pu vérifier la révocation du certificat.* |
| **Solution** | Utiliser un certificat approuvé et valide. Vérifiez la connectivité internet. |
