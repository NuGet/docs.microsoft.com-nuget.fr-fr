---
title: Notes de publication NuGet 2.5
description: Notes de version de NuGet 2.5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: accea5033e44927259537b5047a4a821babc6146
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2018
ms.locfileid: "32045001"
---
# <a name="nuget-25-release-notes"></a>Notes de publication NuGet 2.5

[Notes de publication NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Notes de publication](../release-notes/nuget-2.6.md)

NuGet 2.5 a été publiée le 25 avril 2013. Cette version a été tellement volumineux, il nous semble tenus à ignorer les versions 2.3 et 2.4 ! La date de fin, il s’agit la plus grand version nous avons eu de NuGet, avec sur [160 des éléments de travail](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) dans la version.

## <a name="acknowledgements"></a>Remerciements

Nous aimerions remercier les collaborateurs externes suivantes pour leur contribution significative à NuGet 2.5 :

1. [Michel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -ajouter des MonoAndroid, MonoTouch et MonoMac à la liste des identificateurs de framework cible connus.
2. [Aragoneses de g. Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -Corrigez l’orthographe du `NuGet.targets` pour un système d’exploitation qui respecte la casse
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Vérifiez la solution build sur Mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Corrigez les tests unitaires échoue sur Mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -commande pack de nuget.exe ne propage pas de propriétés MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - XML modifié la gestion du code pour conserver la mise en forme.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Mots reconnus ajoutés au dictionnaire personnalisé permettant de build.cmd réussisse.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Corrigez les tests unitaires lors de l’exécution dans Visual Studio localisée.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interface extrait à partir de PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -gérer les dépendances du projet lors de la livraison
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -prise en charge clair texte mot de passe lorsque vous stockez des informations d’identification de source de package dans les fichiers de nuget.cofig
12. [James effectifs](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -description d’aide de Get-Package corriger

Nous apprécions également aux personnes suivantes pour la recherche de bogues avec NuGet 2.5 bêta/RC qui ont été approuvées et résolus avant la version finale :

1. [Durée totale de Tony](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) - MSTest rompue avec la dernière NuGet 2.4 et 2.5 versions

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Autoriser les utilisateurs à remplacer les fichiers de contenu qui existent déjà

Une des fonctionnalités plus demandées du temps a été la possibilité de remplacer les fichiers de contenu qui existent déjà sur le disque lorsque inclus dans un package NuGet. À compter de NuGet 2.5, ces conflits sont identifiés et vous êtes invité à remplacer les fichiers, alors que précédemment ces fichiers toujours ignorés.

![Remplacer les fichiers de contenu](./media/NuGet-2.5/overwrite-file.png)

« nuget.exe mise à jour » et « Install-Package' maintenant ont tous deux une nouvelle option '-FileConflictAction' pour définir une valeur par défaut pour les scénarios de ligne de commande.

Définir une action par défaut lorsqu’un fichier à partir d’un package existe déjà dans le projet cible. Pour remplacer les fichiers toujours la valeur « Remplacer ». Défini sur « Ignorer » pour ignorer les fichiers. Si non spécifié, il invite pour chaque fichier en conflit.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importation automatique de MSBuild cibles et des fichiers

Un nouveau dossier classique a été créé au niveau supérieur du package NuGet.  En tant qu’homologue `\lib`, `\content`, et `\tools`, vous pouvez maintenant inclure un `\build` dossier dans votre package.  Sous ce dossier, vous pouvez placer les deux fichiers portant des noms fixes, `{packageid}.targets` ou `{packageid}.props`. Ces deux fichiers peuvent être directement sous `build` ou dans des dossiers spécifiques à l’infrastructure tout comme les autres dossiers. La règle pour le dossier framework mieux mise en correspondance de prélèvement est exactement le même que dans ceux.

Lorsque NuGet installe un package avec les fichiers \build, il ajoute un MSBuild `<Import>` élément dans le fichier projet pointant vers le `.targets` et `.props` fichiers. Le `.props` fichier est ajouté en haut, tandis que le `.targets` fichier est ajouté à la fin.

### <a name="specify-different-references-per-platform-using-references-element"></a>Spécifier différentes références par à l’aide de la plateforme `<References/>` élément

Avant de 2.5, dans `.nuspec` fichier, utilisateur peut uniquement spécifier les fichiers de référence, à ajouter pour tous les framework. Grâce à cette nouvelle fonctionnalité dans 2.5, peut créer un utilisateur à présent le `<reference/>` élément pour chaque de la plateforme prise en charge, par exemple :

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

Voici le flux pour comment NuGet ajoute des références à des projets basés sur le `.nuspec` fichier :

1. Rechercher les `lib` dossier qui est appropriée pour le framework cible et d’obtenir la liste des assemblys de ce dossier
1. Séparément de trouver le groupe de références qui convient pour le framework cible et obtenir la liste des assemblys à partir de ce groupe. Groupe de référence sans infrastructure cible spécifié est le groupe de secours.
1. Recherche l’intersection des deux listes et l’utiliser comme les références à ajouter

Cette nouvelle fonctionnalité permet aux auteurs de package à utiliser la fonctionnalité de références aux sous-ensembles d’assemblys à différentes infrastructures lorsqu’ils ont besoin dans le cas contraire transporter des assemblys en double dans plusieurs `lib` dossiers.

Remarque : vous devez actuellement utiliser pack de nuget.exe pour utiliser cette fonctionnalité ; Explorateur de Package NuGet ne pas encore en charge.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Bouton tout pour permettre la mise à jour de tous les packages à la fois de mettre à jour

Beaucoup d'entre vous savent sur l’applet de commande PowerShell de « Mise à jour de Package » pour mettre à jour tous vos packages ; Il existe désormais un moyen simple pour y parvenir via l’interface utilisateur également.

Pour essayer cette fonctionnalité :

1. Créez une application ASP.NET MVC
1. Lancer la boîte de dialogue « Gérer les Packages NuGet »
1. Sélectionnez les mises à jour. »
1. Cliquez sur le bouton « Tout mettre à jour »

![Mettre à jour le bouton tout dans la boîte de dialogue](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Prise en charge de référence de projet améliorée pour le Pack de nuget.exe

Maintenant le processus de commande de pack de nuget.exe référencé projets avec les règles suivantes :

1. Si le projet référencé a correspondant `.nuspec` de fichiers, par exemple, il existe un fichier appelé `proj1.nuspec` dans le même dossier que `proj1.csproj`, puis ce projet est ajouté en tant que dépendance pour le package, à l’aide de l’id et version lire à partir de la `.nuspec` fichier.
1. Dans le cas contraire, les fichiers du projet référencé sont regroupés dans le package. Puis projets référencés par ce projet sont traités à l’aide de l’Afficheur de manière récursive les règles.
1. Toutes les DLL, `.pdb`, et `.exe` fichiers sont ajoutés.
1. Tous les autres fichiers de contenu sont ajoutés.
1. Toutes les dépendances sont fusionnées.

Cela permet à un projet référencé est traitée comme une dépendance s’il existe un `.nuspec` de fichiers, dans le cas contraire, il devient partie intégrante du package.

Plus de détails ici : [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Ajouter une propriété « NuGet Version Minimum » aux packages

Un nouvel attribut de métadonnées appelé « minClientVersion » peut indiquer maintenant la version du client NuGet minimale nécessaire pour utiliser un package.

Cette fonctionnalité vous aide à l’auteur du package pour spécifier qu’un package fonctionnera uniquement après une version particulière de NuGet. En tant que nouveaux `.nuspec` fonctionnalités sont ajoutés après NuGet 2.5, packages seront en mesure de demander une version minimale de NuGet.

```xml
<metadata minClientVersion="2.6">
```

Si l’utilisateur a installée de NuGet 2.5 et un package est identifié comme nécessitant 2.6, signaux visuels seront accordée à l’utilisateur indiquant que le package ne sera pas installable. L’utilisateur sera ensuite demandé à mettre à jour leur version de NuGet.

Cela améliorera l’expérience dans lequel les packages de commencent à installer mais d’échouer indiquant qu'une version de schéma non reconnu a été identifiée.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Dépendances sont n’est plus inutilement mis à jour lors de l’installation du package

Avant de NuGet 2.5, lorsqu’un package a été installé et que fondées sur un package déjà installé dans le projet, la dépendance sera actualisée dans le cadre de la nouvelle installation, même si la version existante satisfait la dépendance.

À partir de NuGet 2.5, si une version de la dépendance est déjà satisfaite, la dépendance se verra pas pendant les installations des autres packages.

**Le scénario :**

1. Le référentiel source contient le package B avec la version 1.0.0 et la version 1.0.2. Il contient également le package A, qui a une dépendance sur B (> = 1.0.0).
1. Supposons que le projet actif possède déjà la version du package B 1.0.0 installé. Maintenant que vous souhaitez installer le package a

**Dans NuGet, 2.2 et versions antérieure :**

* Lorsque vous installez le package A, NuGet mettra automatiquement à jour B vers la version 1.0.2, même si la version existante 1.0.0 répond déjà à la contrainte de version de dépendance, qui est > = 1.0.0.

**Dans NuGet 2.5 et les versions ultérieures :**

* NuGet est plus mis à jour B, parce qu’il détecte que la version existante 1.0.0 conforme à la contrainte de version de dépendance.

Pour plus d’informations sur cette modification, lisez la section détaillée [élément de travail](http://nuget.codeplex.com/workitem/1681) , ainsi que les [de discussion](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe génère des requêtes http avec des commentaires détaillés

Si vous dépannez nuget.exe ou obtenir des informations que les requêtes HTTP sont effectuées lors des opérations, le '-commentaires détaillés ' commutateur produira désormais des toutes les requêtes HTTP sont effectuées.

![Sortie HTTP à partir de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>push de NuGet.exe prend désormais en charge les sources UNC et le dossier

Avant de NuGet 2.5, lorsque vous essayez d’exécuter 'push de nuget.exe' à une source de package basée sur un chemin d’accès UNC ou un dossier local, l’installation poussée du échouerait. Avec la fonctionnalité de configuration hiérarchique récemment ajouté, il était devenu commun de nuget.exe besoin cibler une source/dossier UNC, ou dans une galerie NuGet basée sur HTTP.

À partir de NuGet 2.5, si nuget.exe identifie une source/dossier UNC, elle effectue la copie du fichier à la source.

La commande suivante fonctionne à présent :

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe prend en charge explicitement spécifié les fichiers de configuration

les commandes de NuGet.exe qui accèdent à présent de configuration (tous sauf « spécification » et « pack ») prend en charge un nouveau '-ConfigFile' option, qui force un fichier de configuration spécifiques à utiliser à la place le fichier de configuration par défaut dans % AppData%\nuget\Nuget.Config.

Exemple :

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Prise en charge pour les projets natifs

Avec NuGet 2.5, les outils de NuGet sont désormais disponible pour les projets natifs dans Visual Studio. Nous prévoyons plus packages natifs utilisent la fonctionnalité d’importations MSBuild ci-dessus, à l’aide d’un outil créé par le [CoApp projet](http://coapp.org). Pour plus d’informations, consultez [les détails de l’outil](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) sur le site Web coapp.org.

Le nom d’infrastructure cible du « native » est introduit pour les packages inclure des fichiers \build \content et \tools lorsque le package est installé dans un projet natif.  Le \`lib' dossier n’est pas utilisé pour les projets natifs.
