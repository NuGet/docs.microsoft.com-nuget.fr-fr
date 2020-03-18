---
title: Notes de publication de NuGet 2,5
description: Notes de publication de NuGet 2,5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428715"
---
# <a name="nuget-25-release-notes"></a>Notes de publication de NuGet 2,5

[Notes de publication de NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notes de publication de NuGet 2,6](../release-notes/nuget-2.6.md)

NuGet 2,5 a été publié le 25 avril 2013. Cette version était tellement importante, nous avons pensé à ignorer les versions 2,3 et 2,4 ! À ce jour, il s’agit de la plus grande version de NuGet, avec plus de [160 éléments de travail](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) dans la version.

## <a name="acknowledgements"></a>Remerciements

Nous aimerions remercier les contributeurs externes suivants pour leurs contributions significatives à NuGet 2,5 :

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -ajoutez monoandroid, unitouch et MonoMac à la liste des identificateurs de Framework cible connus.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -correction de l’orthographe des `NuGet.targets` pour un système d’exploitation qui respecte la casse
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Rendez la génération de la solution sur mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Corriger les tests unitaires qui échouent sur mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -la commande du Pack NuGet. exe ne propage pas les propriétés à MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - Code de gestion XML modifié par [#1511](https://nuget.codeplex.com/workitem/1511) pour préserver la mise en forme.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Ajout de mots reconnus au dictionnaire personnalisé pour permettre à Build. cmd de s’effectuer correctement.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Corriger les tests unitaires lors de l’exécution dans les
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interface extraite de PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) : gère les dépendances de projet lors de la compression
11. [Xavier DECHARGEMENT](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -prendre en charge le mot de passe en texte clair lors du stockage des informations d’identification de la source du package dans les fichiers NuGet. cofig
12. [James Equipment](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -corriger la description de l’aide sur la récupération de package

Nous apprécions également les personnes suivantes pour trouver des bogues avec NuGet 2,5 Beta/RC qui ont été approuvés et résolus avant la version finale :

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest endommagé avec les dernières builds NuGet 2,4 et 2,5

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Autoriser les utilisateurs à remplacer les fichiers de contenu qui existent déjà

L’une des fonctionnalités les plus demandées de tout le temps est la possibilité de remplacer les fichiers de contenu qui existent déjà sur le disque lorsqu’ils sont inclus dans un package NuGet. À compter de NuGet 2,5, ces conflits sont identifiés et vous êtes invité à remplacer les fichiers, tandis que ces fichiers étaient toujours ignorés.

![Remplacer les fichiers de contenu](./media/NuGet-2.5/overwrite-file.png)

« NuGet. exe Update » et « Install-Package » disposent désormais d’une nouvelle option « -FileConflictAction » pour définir des valeurs par défaut pour les scénarios de ligne de commande.

Définissez une action par défaut lorsqu’un fichier d’un package existe déjà dans le projet cible. Définissez sur « overwrite » pour toujours remplacer les fichiers. Définissez sur « Ignorer » pour ignorer les fichiers. S’il n’est pas spécifié, il demande à chaque fichier en conflit.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importation automatique de cibles et de fichiers props MSBuild

Un nouveau dossier conventionnel a été créé au niveau supérieur du package NuGet.  En tant qu’homologue pour `\lib`, `\content`et `\tools`, vous pouvez désormais inclure un dossier `\build` dans votre package.  Dans ce dossier, vous pouvez placer deux fichiers avec des noms fixes, `{packageid}.targets` ou `{packageid}.props`. Ces deux fichiers peuvent être directement sous `build` ou sous des dossiers spécifiques à l’infrastructure, tout comme les autres dossiers. La règle de sélection du dossier Framework le mieux adapté est exactement la même que celle de celles-ci.

Quand NuGet installe un package avec des fichiers \Build, il ajoute un élément `<Import>` MSBuild dans le fichier projet pointant vers les fichiers `.targets` et `.props`. Le fichier `.props` est ajouté en haut, tandis que le fichier `.targets` est ajouté en bas.

### <a name="specify-different-references-per-platform-using-references-element"></a>Spécifier différentes références par plateforme à l’aide de `<References/>` élément

Avant le 2,5, dans `.nuspec` fichier, l’utilisateur ne peut spécifier que les fichiers de référence, à ajouter pour tous les frameworks. Désormais, avec cette nouvelle fonctionnalité dans 2,5, l’utilisateur peut créer l’élément `<reference/>` pour chacune des plateformes prises en charge, par exemple :

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

Voici le déroulement de la façon dont NuGet ajoute des références aux projets basés sur le fichier `.nuspec` :

1. Recherchez le dossier `lib` approprié pour la version cible de .NET Framework et obtenez la liste des assemblys à partir de ce dossier
1. Recherchez séparément le groupe de références qui est approprié pour la version cible de .NET Framework et obtenez la liste des assemblys de ce groupe. Le groupe de référence sans Framework cible spécifié est le groupe de secours.
1. Recherchez l’intersection des deux listes et utilisez-la comme référence à ajouter

Cette nouvelle fonctionnalité permet aux créateurs de packages d’utiliser la fonctionnalité de références pour appliquer des sous-ensembles d’assemblys à différents frameworks lorsqu’ils doivent autrement transporter des assemblys en double dans plusieurs dossiers de `lib`.

Remarque : vous devez actuellement utiliser le Pack NuGet. exe pour utiliser cette fonctionnalité. L’Explorateur de package NuGet ne le prend pas encore en charge.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Bouton mettre à jour tout pour autoriser la mise à jour de tous les packages à la fois

Un grand nombre d’entre vous en savent plus sur l’applet de commande PowerShell « Update-Package » pour mettre à jour tous vos packages. Il existe désormais un moyen simple de le faire via l’interface utilisateur.

Pour essayer cette fonctionnalité, procédez comme suit :

1. Créer une application ASP.NET MVC
1. Lancer la boîte de dialogue « gérer les packages NuGet »
1. Sélectionner « mises à jour »
1. Cliquez sur le bouton « mettre à jour tout »

![Bouton tout mettre à jour dans la boîte de dialogue](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Prise en charge améliorée de la référence de projet pour le Pack NuGet. exe

La commande NuGet. exe Pack traite désormais les projets référencés avec les règles suivantes :

1. Si le projet référencé a un fichier `.nuspec` correspondant, par exemple s’il existe un fichier nommé `proj1.nuspec` dans le même dossier que `proj1.csproj`, ce projet est ajouté en tant que dépendance au package, à l’aide de l’ID et de la version lus dans le fichier `.nuspec`.
1. Dans le cas contraire, les fichiers du projet référencé sont regroupés dans le package. Les projets référencés par ce projet seront ensuite traités à l’aide des règles SAMES de manière récursive.
1. Tous les fichiers DLL, `.pdb`et `.exe` sont ajoutés.
1. Tous les autres fichiers de contenu sont ajoutés.
1. Toutes les dépendances sont fusionnées.

Cela permet à un projet référencé d’être traité comme une dépendance s’il existe un fichier de `.nuspec`, sinon il devient une partie du package.

Plus de détails ici : [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Ajouter une propriété’version minimale de NuGet’aux packages

Un nouvel attribut de métadonnées appelé « minClientVersion » peut maintenant indiquer la version minimale du client NuGet requise pour utiliser un package.

Cette fonctionnalité permet à l’auteur du package de spécifier qu’un package ne fonctionnera qu’après une version particulière de NuGet. À mesure que de nouvelles fonctionnalités de `.nuspec` sont ajoutées après NuGet 2,5, les packages peuvent revendiquer une version minimale de NuGet.

```xml
<metadata minClientVersion="2.6">
```

Si NuGet 2,5 est installé sur l’utilisateur et qu’un package est identifié comme nécessitant 2,6, des signaux visuels seront fournis à l’utilisateur pour indiquer que le package ne pourra pas être installé. L’utilisateur sera ensuite guidé pour mettre à jour sa version de NuGet.

Cela permet d’améliorer l’expérience existante où les packages commencent à s’installer, mais qui échouent, indiquant qu’une version de schéma non reconnue a été identifiée.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Les dépendances ne sont plus mises à jour inutilement lors de l’installation du package

Avant la version antérieure de NuGet 2,5, quand un package était installé et dépendait d’un package déjà installé dans le projet, la dépendance serait mise à jour dans le cadre de la nouvelle installation, même si la version existante satisfaisait la dépendance.

À compter de NuGet 2,5, si une version de dépendance est déjà satisfaite, la dépendance ne sera pas mise à jour lors des autres installations de package.

**Le scénario :**

1. Le référentiel source contient le package B avec les versions 1.0.0 et 1.0.2. Il contient également le package A qui a une dépendance sur B (> = 1.0.0).
1. Supposons que le projet actuel a déjà le package B version 1.0.0 installé. Vous souhaitez maintenant installer le package A.

**Dans NuGet 2,2 et les versions antérieures :**

* Lors de l’installation du package A, NuGet met automatiquement à jour B vers 1.0.2, même si la version existante 1.0.0 satisfait déjà à la contrainte de version de dépendance, qui est > = 1.0.0.

**Dans NuGet 2,5 et versions ultérieures :**

* NuGet ne mettra plus à jour B, car il détecte que la version existante 1.0.0 est conforme à la contrainte de version de dépendance.

Pour plus d’informations sur cette modification, consultez l' [élément de travail](http://nuget.codeplex.com/workitem/1681) détaillé ainsi que le [thread de discussion](http://nuget.codeplex.com/discussions/436712)associé.

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet. exe génère des requêtes http avec un niveau de détail détaillé

Si vous dépannez NuGet. exe ou que vous voulez simplement connaître les requêtes HTTP effectuées au cours des opérations, le commutateur « -verbosity detailed » génère désormais toutes les requêtes HTTP effectuées.

![Sortie HTTP de NuGet. exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>NuGet. exe Push prend désormais en charge les sources UNC et de dossier

Avant NuGet 2,5, si vous tentiez d’exécuter « NuGet. exe push » dans une source de package en fonction d’un chemin UNC ou d’un dossier local, l’envoi échoue. Avec la fonctionnalité de configuration hiérarchique récemment ajoutée, il fallait que NuGet. exe doive cibler une source UNC/dossier ou une galerie NuGet basée sur HTTP.

À compter de NuGet 2,5, si NuGet. exe identifie une source UNC/dossier, il effectuera la copie de fichiers vers la source.

La commande suivante fonctionne désormais :

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet. exe prend en charge les fichiers de configuration spécifiés explicitement

les commandes NuGet. exe qui accèdent à la configuration (toutes sauf « spec » et « Pack ») prennent désormais en charge une nouvelle option « -ConfigFile », qui force l’utilisation d’un fichier de configuration spécifique à la place du fichier de configuration par défaut sur%AppData%\nuget\Nuget.Config.

Exemple :

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Prise en charge des projets natifs

Avec NuGet 2,5, les outils NuGet sont désormais disponibles pour les projets natifs dans Visual Studio. Nous pensons que la plupart des packages natifs utiliseront la fonctionnalité importations MSBuild ci-dessus, à l’aide d’un outil créé par le [projet CoApp](http://coapp.org). Pour plus d’informations, consultez les [Détails de l’outil](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) sur le site Web coapp.org.

Le nom du Framework cible « native » est introduit pour que les packages incluent les fichiers dans \Build, \Content et \Tools lorsque le package est installé dans un projet natif.  Le dossier \`lib» n’est pas utilisé pour les projets natifs.
