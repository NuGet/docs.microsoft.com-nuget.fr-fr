---
title: Notes de mise à jour de NuGet 3.5 bêta
description: Notes de publication pour 3.5 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822589"
---
# <a name="nuget-35-release-notes"></a>Notes de version 3.5 de NuGet

[Notes de publication NuGet 3.5 RC](../release-notes/nuget-3.5-RC.md) | [Notes de version RC de NuGet 4.0](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Correctifs de bogues

* Pack n’utilise pas MSBuild 14,1 sur mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Onglet de mise à jour ne sélectionne pas la dernière version disponible pour mettre à jour au lieu de cela, sélectionnez la version installée en cours - [#3498](https://github.com/NuGet/Home/issues/3498)

* Résoudre l’incident après l’authentification d’un v2 privé MyGet flux et en cliquant sur « Afficher x plus de résultats »- [#3469](https://github.com/NuGet/Home/issues/3469)

* Messages du journal semblent être dans l’ordre inverse pour l’interface utilisateur - [#3446](https://github.com/NuGet/Home/issues/3446)

* V3.4.4 - Nuget restore lève « format du chemin d’accès donné n’est pas pris en charge » - [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 bêta ne tient pas compte - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)

* IKVM NuGet lente installer sur un grand projet - [#3428](https://github.com/NuGet/Home/issues/3428)

* NuGet.exe mise à jour - Self conserve sur la mise à jour lui-même - [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 installation/restauration à partir de partage UNC a régression des performances de 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Erreur lors de l’installation Moq à partir de l’interface utilisateur de gestion de Package pour un projet net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Onglet installation au niveau de la solution n’affiche une version du package - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` mise à jour à partir de l’onglet installé perd l’état - [#3303](https://github.com/NuGet/Home/issues/3303)

* Pack de NuGet sur `.csproj` ignore l’élément de fichiers vides dans `.nuspec` fichier - [#3257](https://github.com/NuGet/Home/issues/3257)

* Les projets de site Web hébergés dans IIS ne devraient pas provoquer l’échec - restauration [#3235](https://github.com/NuGet/Home/issues/3235)

* Informations d’identification ne pas récupérées à partir de Nuget.Config lorsque le point de terminaison v3 redirige vers v2 - [#3179](https://github.com/NuGet/Home/issues/3179)

* Pack de NuGet ne parvient pas à résoudre l’assembly lors de la récupération des métadonnées de l’assembly portable - [#3128](https://github.com/NuGet/Home/issues/3128)

* Impossible de trouver NuGet `msbuild.exe` sur Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* pack de NuGet.exe n’autorise pas une balise en version préliminaire qui commence par nombres - [#1743](https://github.com/NuGet/Home/issues/1743)

* installation du package NuGet échoue sur VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions de filtre de travail au niveau de la solution - [#333](https://github.com/NuGet/Home/issues/333)

* Restauration échoue de manière aléatoire avec un élément avec la même clé a déjà été ajoutée. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Impossible d’installer Nuget.Common dans `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Lorsque vous utilisez l’interface utilisateur pour rechercher une source V2, FindPackagesById est appelée deux fois pour chaque ID - [#2517](https://github.com/NuGet/Home/issues/2517)

* Les packages ne peuvent pas dépendre de projets - [#2490](https://github.com/NuGet/Home/issues/2490)

* pack de NuGet.exe - Exclude est documentée, mais pas pris en charge - [#2284](https://github.com/NuGet/Home/issues/2284)

* Problèmes avec l’erreur messages lorsque section 'fichiers' `.nuspec` n’est pas valide - [#1686](https://github.com/NuGet/Home/issues/1686)

* Push envoie toujours le package entier à deux reprises avec des sources de package - authentifié [#1501](https://github.com/NuGet/Home/issues/1501)

* Aucune information n’a été donnée lors de l’appel *.csproj de mise à jour de nuget.exe lors du projet n’a pas un `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` restauration de ne pas de nouvelle tentative sur les codes d’état 5xx à partir de sources de V2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Deux points dans l’attribut src de fichier dans `.nuspec` ne fonctionne pas - [#2947](https://github.com/NuGet/Home/issues/2947)

* Restauration de CoreCLR doit ignorer les flux avec chiffrement - [#2942](https://github.com/NuGet/Home/issues/2942)

* NuGet.exe push gestion 403 - incorrectement demander des informations d’identification - [#2910](https://github.com/NuGet/Home/issues/2910)

* Mise à jour de NuGet via le Gestionnaire de package supprime des propriétés à partir de la `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio tente de charger « NuGet.TeamFoundationServer14 », mais que le nom de la DLL changé de « NuGet.TeamFoundationServer » - [#2857](https://github.com/NuGet/Home/issues/2857)

* Gestionnaire de package n’affiche pas l’interface utilisateur qui vient d’être mis à jour la version - [#2828](https://github.com/NuGet/Home/issues/2828)

* Essayez d’utiliser l’ID de package, du package de mise à jour version au lieu de package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* NuGet restore csproj doit erreur si le projet n’est pas à l’aide de nuget (`packages.config` ou `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Erreur de TFS » [fichier] est introuvable dans votre espace de travail, ou vous n’êtes pas autorisé à y accéder » au cours de mise à niveau ou désinstaller en cas de solution/projet est lié au contrôle de code source TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* package de mise à jour n’obtenir les dépendances pour les packages non cibles - [#2724](https://github.com/NuGet/Home/issues/2724)

* Il n’existe aucun moyen de définir le niveau de détail des journaux pour les actions de l’interface utilisateur du Gestionnaire de package de Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* la configuration NuGet n’est pas valide - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource dans `NuGetDefaults.Config` (`ProgramData\NuGet`) ne fonctionne pas - [#2653](https://github.com/NuGet/Home/issues/2653)

* version de NuGet 3.4.3 - mise en route de la valeur ne peut pas être null lors de la build du package - [#2648](https://github.com/NuGet/Home/issues/2648)

* restauration n’utilise pas les informations d’identification stockées à partir de Nuget.Config pour les flux VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restauration]--configfile est relatif au répertoire de projet au lieu de la commande dir - [#2639](https://github.com/NuGet/Home/issues/2639)

* Allocations excessives dans le code de comparaison de version - [#2632](https://github.com/NuGet/Home/issues/2632)

* Plusieurs instances de nuget.exe tente d’installer le même package en parallèle provoque une double écriture - [#2628](https://github.com/NuGet/Home/issues/2628)

* Informations de dépendance ne sont pas mis en cache pour les opérations de plusieurs projets - [#2619](https://github.com/NuGet/Home/issues/2619)

* Installer et mettre à jour les packages de téléchargement sans vérifier le dossier packages tout d’abord - [#2618](https://github.com/NuGet/Home/issues/2618)

* Si la liste des sources de package est vide, ne peut pas ajouter la source du package via l’interface utilisateur (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Induire des erreurs lorsque vous tentez d’installer le package dépend au moment du design façades - [#2594](https://github.com/NuGet/Home/issues/2594)

* Installation d’un package à partir de la console PackageManager avec le paramètre « All » tente uniquement de première source - [#2557](https://github.com/NuGet/Home/issues/2557)

* Dernière version bêta ne pas décompresser ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* Panne de VS2015 au démarrage avec NuGet automatique intégrée 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Commande de mise à jour peut être un peu plus détaillée si i lui demander d’être plus.. - [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX généré localement doit avoir les mêmes fichiers DLL et que la build de l’élément de configuration. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Résoudre les avertissements vers une version antérieure de NuGet dans la build - [#2396](https://github.com/NuGet/Home/issues/2396)

* Authentifie source du package (3 fois) est bloquée toujours - [#2362](https://github.com/NuGet/Home/issues/2362)

* Contenu du package n’est pas restauré correctement lors de l’installation d’un package à partir d’un v3.3 nuget + flux avec l’argument - NoCache lorsque le package contient `.nupkg` fichiers - [#2354](https://github.com/NuGet/Home/issues/2354)

* Échec de l’installation de NuGet avec toutes les Sources de Package, mais de package manquant à partir de la source de 1, - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay : nuget.packagemanagement.visualstudio.dll ! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt ; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Installer des blocs si une seule source échoue autorisation - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` version plage doit substituer IncludeReferencedProjects - version - [#1983](https://github.com/NuGet/Home/issues/1983)

* Package de mise à jour lente super - « tentative de collecte des informations de dépendance » - [#1909](https://github.com/NuGet/Home/issues/1909)

* Rétrogradations furtives de NuGet package quand lot mise à jour de ses dépendances - [#1903](https://github.com/NuGet/Home/issues/1903)

* mise à jour de NuGet.exe supprime le nom fort d’assembly et l’attribut privé. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Chemin d’accès relatif pour « DefaultPushSource » - [#1746](https://github.com/NuGet/Home/issues/1746)

* Améliorer les messages d’échec de résolution - [#1373](https://github.com/NuGet/Home/issues/1373)

* package de mise à jour v3 échoue avec des packages pas dans la source spécifiée - [#1013](https://github.com/NuGet/Home/issues/1013)

* À l’aide de chemins d’accès relatifs pour les sources de package peut être problématique pour utiliser - [#865](https://github.com/NuGet/Home/issues/865)

* Pas de dépendance dans le fichier NUPKG généré à partir de projet si la dépendance indirecte existe déjà avec une spécification de version inférieure - [#759](https://github.com/NuGet/Home/issues/759)

* Suppression d’un projet ferme la fenêtre de l’interface utilisateur correspondante, mais renommer un projet ne renomme pas la fenêtre de l’interface utilisateur. Notez que PMC écoute pour renommer le projet et les événements de suppression de projet - [#670](https://github.com/NuGet/Home/issues/670)

* [Salix charge de travail Web] Création de Razor v3 WSP se bloque - [#3241](https://github.com/NuGet/Home/issues/3241)

* Installation/la restauration d’un package particulier échoue avec « Le Package contient plusieurs fichiers nuspec. » - [#3231](https://github.com/NuGet/Home/issues/3231)

* ID de minuscules & `packages.config` scénarios - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 à la bêta 2] Restauration des packages ne parvient pas à restaurer les packages « hérités » - [#3208](https://github.com/NuGet/Home/issues/3208)

* NuGet pack ajoute forcer les fichiers .tt au dossier de contenu quelle - [#3203](https://github.com/NuGet/Home/issues/3203)

* package de mise à jour de l’application web ASP.NET génère l’avertissement lié au fichier : source - [#3194](https://github.com/NuGet/Home/issues/3194)

* NuGet pack csproj (avec `project.json`) se bloque si aucun packOptions et le propriétaire du fichier JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* pack de NuGet pour `project.json` ignore les balises packOptions comme résumé, les auteurs, les propriétaires, etc. - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* Pack de NuGet ignore les dépendances dans la sortie `.nuspec` pour `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Mise à jour de plusieurs packages avec restauration laisse le projet dans un état interrompu - [#3139](https://github.com/NuGet/Home/issues/3139)

* Les fichiers associés ne sont pas ajoutés pour les projets de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Ne peut pas empaqueter bibliothèque ciblant .net Standard correctement - [#3108](https://github.com/NuGet/Home/issues/3108)

* Fichier -> Nouveau projet -> Échec de projet de bibliothèque de classes (Portable) dans VS2015 et Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Erreur de nuGet - 1.0.0-* n’est pas une chaîne de version valide - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ne parvient pas à l’affichage mais works d’Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Erreur lors de la « Install-Package jquery.validation » sur dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* par défaut pour le chemin d’accès de la cible non valide - pack NuGet de xproj [#3060](https://github.com/NuGet/Home/issues/3060)

* Lorsque installé Visual Studio 2015 update 3 sur un VS par NuGet version 3.5.0 erreur - [#3053](https://github.com/NuGet/Home/issues/3053)

* « Bloqué par packages.config » `project.json` (UWP, build ou intégré) projet - [#3046](https://github.com/NuGet/Home/issues/3046)

* mettre à jour cli dotnet installé par le script de compilation preview2-003121, qui est la build preview2 officiel. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interface utilisateur du Gestionnaire de package : n’affiche pas nouvelle version après mise à jour d’un package- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey sur la ligne de commande de suppression n’est pas en lecture/envoyé dans 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Chaîne incorrect : version finale d’un package ne doit pas avoir sur une dépendance de version préliminaire. - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage cache laisse les dossiers vides - [#3029](https://github.com/NuGet/Home/issues/3029)

* Création de get de projet de bibliothèque de classes portables (net46 et windows 10) NullRef exception. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Mise à jour de NuGet doit fournir de message d’information lorsqu’une version plus récente est restreinte par la contrainte d’allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Problèmes de restauration v3 NuGet - [#2891](https://github.com/NuGet/Home/issues/2891)

* Plug-in d’informations d’identification s’est arrêté avec l’erreur -1 / erreur téléchargement du package lors de l’utilisation de fournisseurs d’informations d’identification avec plusieurs sources - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` NuGet restore entraîne une recompilation en l’absence de modification - [#2817](https://github.com/NuGet/Home/issues/2817)

* Les packages de symboles ne doivent pas être déjà utilisé dans l’installation ou de mise à jour - [#2807](https://github.com/NuGet/Home/issues/2807)

* Visual Studio ne prend pas en charge les variables d’environnement dans repositoryPath (nuget.exe fait) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Les éléments d’interface utilisateur sans étiquette dans le Gestionnaire de Package UI d’étiquette pour l’accessibilité - [#2745](https://github.com/NuGet/Home/issues/2745)

* Les infrastructures portables avec des profils de trait d’union sont rejetées. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Gestionnaire de package NuGet doit indiquer clairement que liste d’options dans les packages de détail ne s’applique pas aux `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* push de NuGet.exe/delete ne sont pas utiliser la clé API - [#2627](https://github.com/NuGet/Home/issues/2627)

* Supprimez la propriété verrouillée le fichier de verrouillage - [#2379](https://github.com/NuGet/Home/issues/2379)

* Échec de la mise à jour de NuGet 3.3.0 avec ' une contrainte supplémentaire... défini dans packages.config empêche cette opération. » - [#1816](https://github.com/NuGet/Home/issues/1816)

* L’installation du package à partir d’une source locale qui n’existe pas lève un message erroné - [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtre de « Mise à niveau disponible » affiche les mises à niveau qui violent la contrainte de version - [#1094](https://github.com/NuGet/Home/issues/1094)

* Impossible de mettre à jour les packages natives - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Fonctionnalités

* Prend en charge le paramètre CopyLocal false sur les références ajoutées par NuGet - [#329](https://github.com/NuGet/Home/issues/329)

* prise en charge de NuGet.exe pour MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)

* Pack prise en charge.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Désactiver l’action de l’utilisateur lorsqu’il existe des actions de l’utilisateur en cours d’exécution- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet doit prendre en charge les `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Ajouter des compatibilités framework manquant dans NuGet 2.x (qui sont déjà dans 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Prise en charge des dossiers de package de secours - [#2899](https://github.com/NuGet/Home/issues/2899)

* Concevoir et implémenter une notion de type de package pour prendre en charge les packages de l’outil - [#2476](https://github.com/NuGet/Home/issues/2476)

* Ajouter une API pour obtenir le chemin d’accès au dossier packages global - [#2403](https://github.com/NuGet/Home/issues/2403)

* Activer SemVer 2.0.0 Pack - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* push de NuGet.exe - paramètre de délai d’attente ne fonctionne pas - [#2785](https://github.com/NuGet/Home/issues/2785)

* Texte de Description de package doit-elle être sélectionnés - [#1769](https://github.com/NuGet/Home/issues/1769)

* Activer nuget.exe produire `.props` et `.targets` pour les fichiers `.nuproj` projets [#2711](https://github.com/NuGet/Home/issues/2711)

* Ajouter à comparer les infrastructures des importations - API d’extensibilité [#2633](https://github.com/NuGet/Home/issues/2633)

* Masquer les options de dépendance lors de l’utilisation `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Impression nuget.exe en-tête de version dans une sortie détaillée - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet a besoin informer les utilisateurs que la mise à niveau/installation dans un tfm dotnet basé PCL peut entraîner des problèmes - [#3138](https://github.com/NuGet/Home/issues/3138)

* Avertir l’installation/mise à niveau incorrect pour le projet avec tfm = « dotnet » - [#3137](https://github.com/NuGet/Home/issues/3137)

* Résoudre les problèmes de performances avec ReShaper et NuGet pour la mise à jour - [#3044](https://github.com/NuGet/Home/issues/3044)

* Ajouter la prise en charge netcoreapp11 et netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Attribut de AssemblyMetadata tirent parti de `.nuspec` jeton remplacements - [#2851](https://github.com/NuGet/Home/issues/2851)
