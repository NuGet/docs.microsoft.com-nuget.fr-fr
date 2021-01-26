---
title: Notes de publication de NuGet 3.5 RTM
description: Notes de publication de NuGet 3,5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776357"
---
# <a name="nuget-35-release-notes"></a>Notes de publication de NuGet 3,5

Notes de publication [de NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)  |  [Notes de publication de NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Résolutions de bogues

* Pack n’utilise pas MSBuild 14,1 sur mono- [#3550](https://github.com/NuGet/Home/issues/3550)

* L’onglet mettre à jour ne sélectionne pas la dernière version disponible pour la mise à jour, à la place sélectionnez version installée actuelle- [#3498](https://github.com/NuGet/Home/issues/3498)

* Correction du blocage après l’authentification d’un flux MyGet privé v2 et en cliquant sur « Afficher x plus de résultats »- [#3469](https://github.com/NuGet/Home/issues/3469)

* Les messages de journal semblent être dans l’ordre inverse pour les [#3446](https://github.com/NuGet/Home/issues/3446) d’interface utilisateur

* v 3.4.4-la restauration NuGet lève « le format du chemin d’accès spécifié n’est pas pris en charge »- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3,6 Beta ne respecte pas-prop configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* Installation lente de NuGet IKVM sur un grand projet- [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe Update-continue à se mettre à jour automatiquement- [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 l’installation/la restauration à partir d’un partage UNC présente une régression des performances de 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)

* Erreur lors de l’installation de MOQ à partir de l’interface utilisateur de gestion des packages pour un projet net451- [#3349](https://github.com/NuGet/Home/issues/3349)

* L’onglet installation au niveau de la solution n’affiche pas la version du package- [#3339](https://github.com/NuGet/Home/issues/3339)

* la `project.json` mise à jour xproj à partir de l’onglet installé perd l’état- [#3303](https://github.com/NuGet/Home/issues/3303)

* L’élément NuGet Pack on `.csproj` ignore les fichiers vides dans le `.nuspec` fichier- [#3257](https://github.com/NuGet/Home/issues/3257)

* Les projets de site Web hébergés dans IIS ne doivent pas provoquer l’échec de la restauration [#3235](https://github.com/NuGet/Home/issues/3235)

* Les informations d’identification ne sont pas récupérées à partir de Nuget.Config lorsque le point de terminaison v3 redirige vers v2- [#3179](https://github.com/NuGet/Home/issues/3179)

* Le Pack NuGet ne parvient pas à résoudre l’assembly lors de la récupération des métadonnées de l’assembly portable- [#3128](https://github.com/NuGet/Home/issues/3128)

* NuGet ne peut pas trouver `msbuild.exe` sur mono- [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe Pack n’autorise pas une balise de préversion qui commence par des chiffres- [#1743](https://github.com/NuGet/Home/issues/1743)

* échec de l’installation du package NuGet sur VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)

* le filtre allowedVersions ne fonctionne pas au niveau de la solution- [#333](https://github.com/NuGet/Home/issues/333)

* La restauration échoue de façon aléatoire avec un élément avec la même clé a déjà été ajouté. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Impossible d’installer NuGet. common dans `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Lorsque vous utilisez l’interface utilisateur pour rechercher une source v2, FindPackagesById est appelé deux fois pour chaque ID- [#2517](https://github.com/NuGet/Home/issues/2517)

* Les packages ne peuvent pas dépendre de projets- [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe Pack-Exclude est documenté, mais n’est pas pris en charge- [#2284](https://github.com/NuGet/Home/issues/2284)

* Problèmes liés aux messages d’erreur quand la section’contentFiles’de `.nuspec` n’est pas valide- [#1686](https://github.com/NuGet/Home/issues/1686)

* Push envoie toujours le package entier à deux reprises avec des sources de packages authentifiés- [#1501](https://github.com/NuGet/Home/issues/1501)

* Aucune information n’a été fournie lors de l’appel de nuget.exe Update *. csproj tant que le projet n’a pas de `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` la restauration ne réessaye pas sur les codes de statut 5xx à partir des sources v2- [#1217](https://github.com/NuGet/Home/issues/1217)

* Le double point dans le fichier src `.nuspec` ne fonctionne pas [#2947](https://github.com/NuGet/Home/issues/2947)

* La restauration de CoreCLR doit ignorer les flux avec le chiffrement- [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe de la gestion Push 403-demande d’informations d’identification incorrectes- [#2910](https://github.com/NuGet/Home/issues/2910)

* La mise à jour NuGet via le gestionnaire de package supprime les propriétés du `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet. PackageManagement. VisualStudio essayez de charger « NuGet. TeamFoundationServer14 », mais ce nom de DLL a été remplacé par « NuGet. TeamFoundationServer »- [#2857](https://github.com/NuGet/Home/issues/2857)

* L’interface utilisateur du gestionnaire de package n’affiche pas la version [#2828](https://github.com/NuGet/Home/issues/2828) récemment mise à jour

* Update : package essayant d’utiliser PackageID, version au lieu de package. version- [#2771](https://github.com/NuGet/Home/issues/2771)

* NuGet Restore csproj doit être erroné si le projet n’utilise pas NuGet ( `packages.config` ou `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)

* L’erreur TFS « [fichier] est introuvable dans votre espace de travail, ou vous n’êtes pas autorisé à y accéder » lors de la mise à niveau ou de la désinstallation quand la solution/le projet est lié au contrôle de code source TFS- [#2739](https://github.com/NuGet/Home/issues/2739)

* le package de mise à jour n’obtient pas de dépendances pour les packages non cibles- [#2724](https://github.com/NuGet/Home/issues/2724)

* Il n’existe aucun moyen de définir le niveau de détail des journaux pour les actions de l’interface utilisateur du gestionnaire de package NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)

* la configuration NuGet n’est pas valide-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource dans `NuGetDefaults.Config` ( `ProgramData\NuGet` ) ne fonctionne pas- [#2653](https://github.com/NuGet/Home/issues/2653)

* la version de NuGet 3.4.3-l’obtention de la valeur ne peut pas être null dans la génération du package- [#2648](https://github.com/NuGet/Home/issues/2648)

* la restauration n’utilise pas les informations d’identification stockées à partir de Nuget.Config pour les flux VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--ConfigFile est relatif au répertoire du projet au lieu du Rép cmd- [#2639](https://github.com/NuGet/Home/issues/2639)

* Allocations excessives dans le code d’analyse de version- [#2632](https://github.com/NuGet/Home/issues/2632)

* Plusieurs instances de nuget.exe tentant d’installer le même package en parallèle entraînent une double écriture [#2628](https://github.com/NuGet/Home/issues/2628)

* Les informations de dépendance ne sont pas mises en cache pour les opérations à plusieurs projets- [#2619](https://github.com/NuGet/Home/issues/2619)

* Installer et mettre à jour les packages de téléchargement sans vérifier le dossier Packages en premier [#2618](https://github.com/NuGet/Home/issues/2618)

* Si la liste source du package est vide, impossible d’ajouter la source du package via l’interface utilisateur (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Erreur trompeuse lors de la tentative d’installation du package qui dépend des façades au moment du design- [#2594](https://github.com/NuGet/Home/issues/2594)

* L’installation d’un package à partir de la console PackageManager avec le paramètre « All » essaie uniquement la première source [#2557](https://github.com/NuGet/Home/issues/2557)

* La dernière version bêta ne décompresse pas ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 crash au démarrage avec NuGet auto-intégré NuGet- [#2419](https://github.com/NuGet/Home/issues/2419)

* La commande de mise à jour peut être un peu plus détaillée si je l’ai demandée...- [#2418](https://github.com/NuGet/Home/issues/2418)

* L’extension VSIX générée localement doit avoir les mêmes dll et fichiers que la build CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Corriger les avertissements de rétrogradation NuGet dans le [#2396](https://github.com/NuGet/Home/issues/2396) de build

* L’échec de l’authentification de la source du package (3 fois) est bloqué indéfiniment [#2362](https://github.com/NuGet/Home/issues/2362)

* Le contenu du package n’est pas restauré correctement lors de l’installation d’un package à partir d’un flux NuGet v 3.3 + avec l’argument-NoCache quand le package contient `.nupkg` des fichiers- [#2354](https://github.com/NuGet/Home/issues/2354)

* Installation de NuGet avec toutes les sources de package, mais le package est absent de 1 source, Fail- [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay : nuget.packagemanagement.visualstudio.dll ! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + * lt ; &gt; c__DisplayClass_0 + &lt; &lt; AddReference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* Installer les blocs si une seule source ne parvient pas à obtenir l’autorisation- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` la plage de versions doit remplacer-IncludeReferencedProjects version- [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package super lent-« tentative de collecte des informations sur les dépendances »- [#1909](https://github.com/NuGet/Home/issues/1909)

* Package NuGet Stealth rétrogrades lors de la mise à jour par lots de ses dépendances- [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe mise à jour supprime le nom fort et l’attribut privé de l’assembly. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Chemin de fichier relatif pour « DefaultPushSource »- [#1746](https://github.com/NuGet/Home/issues/1746)

* Améliorer les messages d’échec du programme de résolution- [#1373](https://github.com/NuGet/Home/issues/1373)

* échec de la mise à jour du package dans v3 avec des packages qui ne sont pas dans le [#1013](https://github.com/NuGet/Home/issues/1013) source spécifié

* L’utilisation de chemins d’accès relatifs pour les sources de package pose problème à l’utilisation de- [#865](https://github.com/NuGet/Home/issues/865)

* Dépendance manquante dans NUPKG-fichier généré à partir du projet si la dépendance indirecte existe déjà avec une spécification de version antérieure- [#759](https://github.com/NuGet/Home/issues/759)

* La suppression d’un projet ferme la fenêtre de l’interface utilisateur correspondante, mais le fait de renommer un projet ne renomme pas la fenêtre de l’interface utilisateur. Notez que PMC écoute les événements renommer le projet et supprimer le projet- [#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web Workload] Création de blocages de la préversion de Razor v3- [#3241](https://github.com/NuGet/Home/issues/3241)

* L’installation/la restauration d’un package particulier échoue avec « le package contient plusieurs fichiers NuSpec ». - [#3231](https://github.com/NuGet/Home/issues/3231)

* ID en minuscules & `packages.config` scénarios- [#3209](https://github.com/NuGet/Home/issues/3209)

* [3,5-bêta2] La restauration du package ne parvient pas à restaurer les packages « hérités »- [#3208](https://github.com/NuGet/Home/issues/3208)

* le Pack NuGet ajoute de force aux fichiers. TT dans le dossier de contenu, quelle que soit la [#3203](https://github.com/NuGet/Home/issues/3203)

* Update-le package de l’application Web ASP.NET génère un avertissement lié au fichier : source- [#3194](https://github.com/NuGet/Home/issues/3194)

* NuGet Pack csproj (avec `project.json` ) se bloque s’il n’existe aucun packOptions et propriétaire dans le fichier JSON- [#3180](https://github.com/NuGet/Home/issues/3180)

* le Pack NuGet pour `project.json` ignore les balises packOptions comme Summary, Authors, Owners, etc. [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via NuGet. Packaging. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)

* Le Pack NuGet ignore les dépendances dans la sortie `.nuspec` pour `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* La mise à jour de plusieurs packages avec la restauration laisse le projet dans un État rompu, [#3139](https://github.com/NuGet/Home/issues/3139)

* Les ContentFiles sous n’importe lequel ne sont pas ajoutés pour les projets netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)

* Impossible de regrouper correctement la bibliothèque .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)

* Fichier > nouveau projet de bibliothèque de classes de > (portable) échoue dans VS2015 et Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* erreur nuGet-1.0.0-* n’est pas une chaîne de version valide- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ne parvient pas à s’afficher mais Install-Package Works [#3068](https://github.com/NuGet/Home/issues/3068)

* Erreur lorsque « Install-Package jQuery. validation » sur dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* le Pack NuGet de xproj est défini par défaut sur un chemin cible non valide- [#3060](https://github.com/NuGet/Home/issues/3060)

* Lors de l’installation de VS 2015 Update 3 sur un VS qui utilise une erreur NuGet version 3.5.0 se produit- [#3053](https://github.com/NuGet/Home/issues/3053)

* « Bloqué par packages.config » dans le `project.json` projet (UWP, a. k. a Build intégré)- [#3046](https://github.com/NuGet/Home/issues/3046)

* Mettez à jour l’interface CLI dotnet installée par le script de compilation dans preview2-003121, qui est la build preview2 officielle. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interface utilisateur du gestionnaire de package : n’affiche pas la nouvelle version après la mise à jour d’un package- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey sur la ligne de commande de suppression n’est pas en lecture/envoi dans 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Chaîne incorrecte : une version stable d’un package ne doit pas avoir une dépendance de préversion. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Le cache OptimizedZipPackage conserve les dossiers vides- [#3029](https://github.com/NuGet/Home/issues/3029)

* Création d’une exception de NullRef de projet PCL (net46 et Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* La mise à jour NuGet doit fournir un message informatif quand une version supérieure est limitée par la contrainte allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)

* Problèmes de restauration NuGet v3- [#2891](https://github.com/NuGet/Home/issues/2891)

* [#2885](https://github.com/NuGet/Home/issues/2885) le plug-in des informations d’identification s’est arrêté avec l’erreur 1/erreur lors du téléchargement du package lors de l’utilisation de fournisseurs d’informations d’identification avec plusieurs sources

* `project.json` la restauration NuGet provoque une recompilation lorsque rien n’est modifié- [#2817](https://github.com/NuGet/Home/issues/2817)

* Les packages de symboles ne doivent jamais être utilisés dans Install ou UPDATE- [#2807](https://github.com/NuGet/Home/issues/2807)

* VS ne prend pas en charge les variables d’environnement dans repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* Étiqueter les UIElements sans étiquette dans l’interface utilisateur du gestionnaire de package pour l’accessibilité- [#2745](https://github.com/NuGet/Home/issues/2745)

* Les infrastructures portables avec des profils avec trait d’Union sont rejetées. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Le gestionnaire de package NuGet doit faire en sorte qu’il soit clair que les options Lister les détails des packages ne s’appliquent pas à `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe Push/Delete n’utilise pas de clé API- [#2627](https://github.com/NuGet/Home/issues/2627)

* Supprimez la propriété locked du fichier de verrouillage- [#2379](https://github.com/NuGet/Home/issues/2379)

* La mise à jour NuGet 3.3.0 échoue avec «une contrainte supplémentaire... défini dans packages.config empêche cette opération.» - [#1816](https://github.com/NuGet/Home/issues/1816)

* L’installation d’un package à partir d’une source locale qui n’existe pas lève une fausse [#1674](https://github.com/NuGet/Home/issues/1674) de messages

* Le filtre « mise à niveau disponible » affiche des mises à niveau qui violent la contrainte de version- [#1094](https://github.com/NuGet/Home/issues/1094)

* Impossible de mettre à jour les packages natifs- [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Fonctionnalités

* Prise en charge du paramètre CopyLocal sur false sur les références ajoutées par NuGet- [#329](https://github.com/NuGet/Home/issues/329)

* Prise en charge nuget.exe pour MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)

* Prise en charge de Pack pour.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Désactiver l’action de l’utilisateur lorsque des actions de l’utilisateur sont exécutées- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet doit ajouter la prise en charge de `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Ajouter des compatibilités de Framework manquantes dans NuGet 2. x (qui sont déjà en 3. x)- [#2720](https://github.com/NuGet/Home/issues/2720)

* Prise en charge des dossiers de package de secours- [#2899](https://github.com/NuGet/Home/issues/2899)

* Concevez et implémentez une notion de type de package pour prendre en charge les packages d’outils- [#2476](https://github.com/NuGet/Home/issues/2476)

* Ajoutez une API pour récupérer le chemin d’accès au dossier de packages globaux- [#2403](https://github.com/NuGet/Home/issues/2403)

* Activer SemVer 2.0.0 dans Pack- [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* Le paramètre nuget.exe Push-Timeout ne fonctionne pas- [#2785](https://github.com/NuGet/Home/issues/2785)

* Le texte de description du package doit être sélectionnable- [#1769](https://github.com/NuGet/Home/issues/1769)

* Activez nuget.exe pour produire `.props` `.targets` des fichiers et pour les `.nuproj` projets [#2711](https://github.com/NuGet/Home/issues/2711)

* Ajouter une API d’extensibilité pour comparer des frameworks à des importations- [#2633](https://github.com/NuGet/Home/issues/2633)

* Masquer les options de dépendance lors de l’utilisation de `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Imprimer l’en-tête de version nuget.exe dans la sortie détaillée- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet doit permettre aux utilisateurs de savoir que la mise à niveau/installation dans un PCL basé sur dotnet TFM peut provoquer des problèmes [#3138](https://github.com/NuGet/Home/issues/3138)

* Signaler une installation/mise à niveau incorrecte pour le projet w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Résoudre les problèmes de performances avec remodeler et NuGet pour Update- [#3044](https://github.com/NuGet/Home/issues/3044)

* Ajouter la prise en charge de netcoreapp11 et netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)

* Tirer parti de l’attribut AssemblyMetadata pour les `.nuspec` remplacements de jetons- [#2851](https://github.com/NuGet/Home/issues/2851)
