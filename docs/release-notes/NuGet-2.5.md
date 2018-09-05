---
title: Notes de publication NuGet 2.5
description: Notes de publication pour NuGet 2.5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550481"
---
# <a name="nuget-25-release-notes"></a>Notes de publication NuGet 2.5

[Notes de publication de NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [Notes de publication de NuGet 2.6](../release-notes/nuget-2.6.md)

NuGet 2.5 a été publiée le 25 avril 2013. Cette version a été tellement volumineux, nous avons pensé obligés à ignorer les versions 2.3 et 2.4 ! À ce jour, il s’agit la plus grande version nous offrons pour NuGet, avec sur [160 des éléments de travail](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) dans la version.

## <a name="acknowledgements"></a>Remerciements

Nous aimerions remercier les collaborateurs externes suivants pour leur contribution significative à NuGet 2.5 :

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -MonoAndroid ajouter MonoTouch et MonoMac à la liste des identificateurs de framework cible connus.
2. [Aragoneses g. Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -corriger l’orthographe du `NuGet.targets` pour un système d’exploitation de la casse
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Vérifiez la solution build sur Mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Corrigez les tests unitaires échoue sur Mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -commande pack de nuget.exe ne propage pas les propriétés pour MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - XML modifiés code de gestion pour conserver la mise en forme.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Mots reconnus ajoutés au dictionnaire personnalisé pour autoriser build.cmd réussisse.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Corrigez les tests unitaires lors de l’exécution dans Visual Studio localisée.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interface extraite à partir de PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -gérer les dépendances du projet lors de la compression
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -prise en charge clair texte mot de passe lors du stockage des informations d’identification de source de package dans les fichiers nuget.cofig
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -description de help Get-Package corriger

Nous apprécions également les personnes suivantes pour rechercher les bogues avec NuGet 2.5 Beta/RC qui ont été approuvées et résolus avant la version finale :

1. [Tony mur](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) - MSTest rompue avec la dernière NuGet 2.4 et 2.5 builds

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Autoriser les utilisateurs à remplacer les fichiers de contenu qui existent déjà

Une des fonctionnalités plus demandées de tout le temps a été la possibilité de remplacer les fichiers de contenu qui existent déjà sur le disque lorsque inclus dans un package NuGet. À compter de NuGet 2.5, ces conflits sont identifiés et vous êtes invité à écraser les fichiers, tandis que précédemment ces fichiers étaient toujours ignorés.

![Remplacer les fichiers de contenu](./media/NuGet-2.5/overwrite-file.png)

« mise à jour de nuget.exe » et « Install-Package' maintenant les deux ont une nouvelle option «-FileConflictAction » pour définir une valeur par défaut pour les scénarios de ligne de commande.

Définir une action par défaut lorsqu’un fichier à partir d’un package existe déjà dans le projet cible. La valeur « Remplacer » pour toujours remplacer les fichiers. La valeur est « Ignorer » pour ignorer des fichiers. Si non spécifié, vous êtes invité pour chaque fichier en conflit.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importation automatique des fichiers de cibles et de propriétés MSBuild

Un nouveau dossier traditionnel a été créé au niveau supérieur du package NuGet.  En tant qu’homologue à `\lib`, `\content`, et `\tools`, vous pouvez désormais inclure une `\build` dossier dans votre package.  Dans ce dossier, vous pouvez placer les deux fichiers portant des noms fixes, `{packageid}.targets` ou `{packageid}.props`. Ces deux fichiers peuvent être directement sous `build` ou sous des dossiers spécifiques à l’infrastructure comme les autres dossiers. La règle pour le dossier de framework mieux mise en correspondance de prélèvement est exactement le même que dans ceux.

Quand NuGet installe un package avec des fichiers \build, il ajoutera un MSBuild `<Import>` élément dans le fichier projet pointant vers le `.targets` et `.props` fichiers. Le `.props` fichier est ajouté en haut, tandis que le `.targets` fichier est ajouté au bas.

### <a name="specify-different-references-per-platform-using-references-element"></a>Spécifiez des références différentes par à l’aide de la plateforme `<References/>` élément

Avant de 2.5, dans `.nuspec` fichier, utilisateur peut uniquement spécifier les fichiers de référence, doit être ajouté pour toutes les framework. Maintenant avec cette nouvelle fonctionnalité dans 2.5, l’utilisateur peut créer le `<reference/>` pour chacun de la plateforme prise en charge, par exemple :

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

Voici le flux de la façon dont NuGet ajoute des références aux projets basés sur le `.nuspec` fichier :

1. Rechercher le `lib` dossier qui est approprié pour le framework cible et d’obtenir la liste des assemblys à partir de ce dossier
1. Séparément, recherchez le groupe de références qui convient pour le framework cible et obtenir la liste des assemblys à partir de ce groupe. Groupe de référence sans le framework cible spécifié est le groupe de secours.
1. Recherche l’intersection des deux listes et l’utiliser comme les références à ajouter

Cette nouvelle fonctionnalité permet aux auteurs de package d’utiliser la fonctionnalité de références pour appliquer des sous-ensembles d’assemblys à différentes infrastructures lorsqu’ils ont besoin dans le cas contraire exécuter des assemblys en double dans plusieurs `lib` dossiers.

Remarque : vous devez actuellement utiliser pack de nuget.exe pour utiliser cette fonctionnalité. Explorateur de Package NuGet ne prend pas en charge il.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Bouton tout pour autoriser la mise à jour tous les packages à la fois de mettre à jour

Beaucoup d'entre vous savent sur l’applet de commande PowerShell de « Package de mise à jour » pour mettre à jour tous vos packages ; maintenant il est un moyen simple de le faire via l’interface utilisateur également.

Pour essayer cette fonctionnalité :

1. Créez une application ASP.NET MVC
1. Lancer la boîte de dialogue « Gérer les Packages NuGet »
1. Sélectionnez « Mises à jour »
1. Cliquez sur le bouton « Update All »

![Bouton tous dans la boîte de dialogue Mettre à jour](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Prise en charge des références de projet améliorée pour le Pack de nuget.exe

Maintenant le processus de commande nuget.exe pack référencés projets avec les règles suivantes :

1. Si le projet référencé a correspondant `.nuspec` de fichier, par exemple, il existe un fichier appelé `proj1.nuspec` dans le même dossier que `proj1.csproj`, puis ce projet est ajouté en tant que dépendance au package, à l’aide de l’id et version lire à partir de la `.nuspec` fichier.
1. Sinon, les fichiers du projet référencé sont regroupées dans le package. Les projets référencés par ce projet seront traitées à l’aide de l’Afficheur de manière récursive les règles.
1. Toutes les DLL, `.pdb`, et `.exe` fichiers sont ajoutés.
1. Tous les autres fichiers de contenu sont ajoutés.
1. Toutes les dépendances sont fusionnées.

Cela permet à un projet référencé est traitée comme une dépendance s’il existe un `.nuspec` de fichier, dans le cas contraire, il devient partie intégrante du package.

Plus de détails ici : [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Ajouter une propriété « NuGet Version Minimum » aux packages

Un nouvel attribut de métadonnées appelé « minClientVersion » peut indiquer maintenant la version minimale du client NuGet nécessaire pour utiliser un package.

Cette fonctionnalité vous aide à l’auteur du package pour spécifier qu’un package fonctionnera uniquement après une version particulière de NuGet. En tant que nouveaux `.nuspec` fonctionnalités sont ajoutées après NuGet 2.5, packages seront en mesure de demander une version minimale de NuGet.

```xml
<metadata minClientVersion="2.6">
```

Si l’utilisateur a NuGet 2.5 installé et un package est identifié comme nécessitant 2.6, signaux visuels seront accordée à l’utilisateur qui indique le package ne sera pas installable. L’utilisateur sera ensuite être guidé pour mettre à jour leur version de NuGet.

Cela améliorera l’expérience existant dans lequel les packages commencent à installer, mais échouer puis indiquant qu'une version de schéma non reconnu a été identifiée.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Dépendances ne sont plus inutilement sont mises à jour que lors de l’installation du package

Avant NuGet 2.5, lorsqu’un package a été installé qui dépendent d’un package déjà installé dans le projet, la dépendance est actualisée dans le cadre de la nouvelle installation, même si la version existante satisfait la dépendance.

À partir de NuGet 2.5, si une version de dépendance est déjà satisfaite, la dépendance n’est pas modifiée pendant l’installation des autres packages.

**Le scénario :**

1. Le référentiel source contient le package B version 1.0.0 et version 1.0.2. Il contient également le package A qui a une dépendance sur B (> = 1.0.0).
1. Partons du principe que le projet actif possède déjà la version du package B 1.0.0 installé. Voulez-vous installer a de package.

**Dans NuGet 2.2 et versions antérieure :**

* Lorsque vous installez le package A, NuGet mettra automatiquement à jour B à la version 1.0.2, même si la version 1.0.0 satisfait déjà à la contrainte de version de dépendance, qui est > = 1.0.0.

**Dans NuGet 2.5 et versions ultérieures :**

* NuGet est plus mis à jour B, car il détecte que la version existante 1.0.0 satisfait à la contrainte de version de dépendance.

Pour plus d’informations sur cette modification, consultez le [élément de travail](http://nuget.codeplex.com/workitem/1681) , ainsi que les informations connexes [de discussion](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe génère des requêtes http avec commentaires détaillés

Si vous dépannez nuget.exe ou simplement curieux de savoir quelles requêtes HTTP sont effectuées pendant les opérations, le '-commentaires détaillés ' commutateur sera désormais générer une sortie toutes les requêtes HTTP sont effectuées.

![Sortie HTTP à partir de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>push de NuGet.exe prend désormais en charge les sources UNC et le dossier

Avant NuGet 2.5, si vous essayez d’exécuter 'push de nuget.exe' à une source de package basée sur un chemin d’accès UNC ou un dossier local, l’envoi échouerait. Avec la fonctionnalité de configuration hiérarchique ajoutées récemment, il était devenu commun pour nuget.exe devoir cibler une source/dossier UNC ou une galerie NuGet basée sur HTTP.

À partir de NuGet 2.5, si nuget.exe identifie une source/dossier UNC, elle effectue la copie du fichier à la source.

La commande suivante fonctionnera maintenant :

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe prend en charge explicitement spécifié les fichiers de configuration

les commandes de NuGet.exe qui accèdent à présent de configuration (toutes à l’exception de « spécification » et « pack ») prennent en charge un nouveau »-ConfigFile' option, qui force un fichier de configuration spécifiques à utiliser à la place le fichier de configuration par défaut dans % AppData%\nuget\Nuget.Config.

Exemple :

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Prise en charge pour les projets natifs

Avec NuGet 2.5, les outils de NuGet sont désormais disponible pour les projets natifs dans Visual Studio. Nous prévoyons plus packages natifs utilisera la fonctionnalité d’importations MSBuild ci-dessus, à l’aide d’un outil créé par le [CoApp projet](http://coapp.org). Pour plus d’informations, consultez [les détails de l’outil](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) sur le site Web coapp.org.

Le nom du framework cible du « native » est introduit pour les packages inclure des fichiers \build, \content et \tools lorsque le package est installé dans un projet natif.  Le \`lib' dossier n’est pas utilisé pour les projets natifs.
