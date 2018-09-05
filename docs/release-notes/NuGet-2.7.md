---
title: Notes de publication NuGet 2.7
description: Notes de publication pour NuGet 2.7, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550963"
---
# <a name="nuget-27-release-notes"></a>Notes de publication NuGet 2.7

[NuGet 2.6.1 pour WebMatrix Notes](../release-notes/nuget-2.6.1-for-webmatrix.md) | [Notes de publication de NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2.7 a été publiée le 22 août 2013.

## <a name="acknowledgements"></a>Remerciements

Nous aimerions remercier les collaborateurs externes suivants pour leur contribution significative à NuGet 2.7 :

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Afficher l’url de licence lorsque la liste des packages et des commentaires est détaillée.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -ajouter un attribut developmentDependency à `packages.config` et l’utiliser dans la commande pack pour inclure uniquement les packages de runtime
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Évitez de clé de propriétés en double dans la commande pack de nuget.exe.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -augmenter la taille du cache de machine à 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -NuGet corriger de boîte de dialogue affichant des mises à jour dans l’onglet incorrect
    - Correctif Project.TargetFramework peut être null dans ResponsableProjet
    - [#3248](http://nuget.codeplex.com/workitem/3248) -corriger SharedPackageRepository FindPackage/FindPackagesById échouera sur inexistantes packageId
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -activer la prise en charge pour le projet de Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -Échec de la commande push correctif avec la sortie de code 0 lorsque le fichier n’existe pas.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -corriger le bogue avec la commande Add-BindingRedirect lorsqu’un projet fait référence à un projet de base de données.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -corriger le bogue de nuget.pack l’analyse incorrecte de caractère générique dans l’attribut 'exclude'.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -corriger le bogue `NuGet.targets` ne passe pas $(Platform) de nuget.exe lors de la restauration des packages.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -corriger le bogue dans la commande de package de nuget.exe qui permettrait l’ajout de fichiers avec le même nom mais une casse différente, provoquant des exceptions « Élément existe déjà ».
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -propriété ajouter une Version à NetPortableProfile classe.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -corriger le bogue NullReferenceException si requireApiKey = true, mais l’en-tête X-NUGET-APIKEY n’est pas présent
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -fichier NuGet.Build résout cibles afin qu’il fonctionne correctement sur MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Améliorer les performances de commande de restauration en augmentant la parallélisation

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="package-restore-by-default-with-implicit-consent"></a>Restauration des packages par défaut (avec un consentement implicite)

Introduit une nouvelle approche pour la restauration de package NuGet 2.7 et propose également un obstacle majeur : consentement de restauration de Package est désormais activée par défaut ! La combinaison de la nouvelle approche et un consentement implicite simplifiera considérablement les scénarios de restauration de package.

#### <a name="implicit-consent"></a>Consentement implicite

Avec NuGet les versions 2.0, 2.1, 2.2, 2.5 et 2.6, les utilisateurs nécessaires pour autoriser explicitement NuGet à télécharger les packages manquants pendant générer. Si ce consentement n’avait pas été explicitement spécifiée, puis solutions qui avaient activé la restauration de package échouait générer jusqu'à ce que l’utilisateur a donné son consentement.

À compter de NuGet 2.7, consentement de restauration de package est activé par défaut tout en permettant aux utilisateurs d’explicitement *refus* de restauration de package si vous le souhaitez, à l’aide de la case à cocher dans les paramètres de NuGet dans Visual Studio. Cette modification pour un consentement implicite affecte NuGet dans les environnements suivants :

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilitaire de ligne de commande NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Restauration automatique des packages dans Visual Studio

À compter de NuGet 2.7, NuGet télécharge automatiquement les packages manquants pendant la génération dans Visual Studio, même si la restauration de package n’a pas été explicitement activée pour la solution. Cette restauration automatique des packages qui se produit dans Visual Studio quand vous générez un projet ou la solution, mais avant que MSBuild est appelé. Il en résulte plusieurs avantages significatifs :

1. Aucune autre besoin d’utiliser le mouvement « Activer la restauration des packages NuGet » de votre solution
1. Projets ne doivent pas être modifiés et NuGet ne sont pas apporter des modifications à votre projet pour garantir la restauration de package est activée
1. Tous les packages NuGet, y compris ceux incluant des importations MSBuild pour les fichiers de propriétés/cibles, seront restaurées *avant* MSBuild est appelé pour s’assurer de ces propriétés/cibles sont correctement reconnus lors de la génération

Pour pouvoir utiliser la restauration automatique des packages dans Visual Studio, vous devez uniquement prendre une (action entrant) :

1. N’archivez pas votre `packages` dossier

Il existe plusieurs façons pour omettre votre `packages` dossier à partir du contrôle de code source. Pour plus d’informations, consultez le [Packages et contrôle de code Source](../consume-packages/packages-and-source-control.md) rubrique.

Bien que tous les utilisateurs sont implicitement choisi dans la restauration automatique des packages de consentement, vous pouvez facilement le refuser via les paramètres du Gestionnaire de Package dans Visual Studio.

![Paramètres du Gestionnaire de package](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Restauration simplifiée de Package à partir de la ligne de commande

NuGet 2.7 introduit une nouvelle fonctionnalité de nuget.exe : `nuget.exe restore`

Cette nouvelle commande de restauration vous permet de facilement restaurer tous les packages pour une solution avec une seule commande, en acceptant un fichier solution ou un dossier en tant qu’argument. En outre, cet argument est implicite lorsqu’il existe une seule solution dans le dossier actif. Cela signifie que tous les éléments suivants fonctionnent à partir d’un dossier qui contient un fichier de solution unique (MySolution.sln) :

1. restauration de NuGet.exe MySolution.sln
1. restauration de NuGet.exe.
1. restauration de NuGet.exe

La commande Restore ouvre le fichier de solution et rechercher tous les projets dans la solution. À partir de là, il trouve le `packages.config` fichiers pour chacun des projets et de restauration de tous les packages trouvés. Il restaure également des packages au niveau de la solution qui se trouvent dans le `.nuget\packages.config` fichier. Vous trouverez plus d’informations sur la nouvelle commande de restauration dans le [de ligne de commande référence](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Le nouveau flux de travail de restauration de Package

Nous sommes heureux sur ces modifications à la restauration des packages, comme elle introduit un nouveau flux de travail. Si vous voulez omettre vos packages à partir du contrôle de code source vous ne simplement valider la `packages` dossier. Les utilisateurs de Visual Studio qui ouvrent et générez la solution seront affiche les packages restaurés automatiquement. Pour les builds de ligne de commande, simplement appeler `nuget.exe restore` avant d’appeler `msbuild`. Vous n’avez plus besoin de penser à utiliser le mouvement « Activer la restauration des packages NuGet » sur votre solution, et nous allons devoir n’est plus modifier vos projets pour modifier la build. Et cela génère également une expérience améliorée pour les packages qui incluent des importations MSBuild, en particulier pour les importations ajoutées via la fonctionnalité de récente de NuGet pour [important automatiquement les fichiers de propriétés/cibles](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) à partir du dossier \build.

Outre le travail que nous l’avons fait nous-mêmes, nous travaillons également avec certains partenaires importants pour compléter cette nouvelle approche. Nous n’avons encore chronologies concrètes pour une de ces, mais chaque partenaire est aussi impatients que nous sommes sur la nouvelle approche.

* Team Foundation Service - ils travaillent pour intégrer l’appel à `nuget.exe restore` dans la valeur par défaut des scénarios de génération.
* Sites Web Windows Azure - ils travaillent afin que vous puissiez envoyer votre projet vers Azure et avez `nuget.exe restore` appelé avant la génération de votre site web.
* TeamCity - ils mettent à jour leur plug-in du programme d’installation de NuGet pour TeamCity 8.x
* AppHarbor - ils travaillent afin que vous puissiez transmettre votre référentiel à AppHarbor et avez `nuget.exe restore` appelée avant que votre solution est la build.

Avec chacun des partenaires ci-dessus, ils utilisent leur propre copie de nuget.exe et il serait inutile d’effectuer de nuget.exe dans votre solution.

#### <a name="known-issues"></a>Problèmes connus

Il étaient deux problèmes connus avec la restauration de nuget.exe avec la version 2.7 initiale, mais ils ont été résolus sur 9/6/2013 avec une mise à jour le [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/).  Cette mise à jour est également disponible sur le [page de téléchargement de NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) sur CodePlex.  En cours d’exécution `nuget.exe update -self` met à jour vers la dernière version.

Le texte fixe ont été :

1. [Restauration des packages ne fonctionne pas sur Mono lorsque vous utilisez les fichiers SLN](https://nuget.codeplex.com/workitem/3596)
1. [Restauration des packages ne fonctionne pas avec des projets Wix](https://nuget.codeplex.com/workitem/3598)

Il existe également un problème connu avec le nouveau flux de travail de restauration de package par laquelle [restauration automatique des packages ne fonctionne pas pour les projets dans un dossier de solution](https://nuget.codeplex.com/workitem/3625). Ce problème a été résolu dans NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Reciblage du projet et mise à niveau erreurs/avertissements de Build

Nombre de fois après le reciblage ou mise à niveau votre projet, vous trouvez que certains packages NuGet ne sont pas fonctionne correctement. Malheureusement, il n’existe aucune indication de ce et il n’existe aucune recommandation sur la façon de résoudre. Avec NuGet 2.7, nous utilisons maintenant certains événements de Visual Studio à reconnaître quand vous avez reciblé ou mis à niveau votre projet d’une manière qui affecte vos packages NuGet installés.

Si nous détectons qu’un de vos packages ont été affecté par le reciblage ou la mise à niveau, nous allons générer des erreurs de build immédiate pour vous informer. En plus de l’erreur de build immédiate, nous avons également de conserver un `requireReinstallation="true"` indicateur dans votre `packages.config` fichier tous les packages qui ont été affectés par le reciblage et chaque génération dans Visual Studio génère des avertissements de génération des packages.

Bien que NuGet ne peut pas effectuer automatiquement une action de réinstaller les packages concernés, nous espérons que cette indication et avertissement vous guide aide vous découvrez que vous deviez réinstaller les packages. Nous travaillons également [documentation du Guide de réinstallation du package](../consume-packages/reinstalling-and-updating-packages.md) que ces messages d’erreur vous invitent à.

### <a name="nuget-configuration-defaults"></a>Valeurs par défaut de la Configuration NuGet

De nombreuses entreprises sont à l’aide de NuGet en interne, mais ont eu du mal guider leurs développeurs pour utiliser des sources de package interne au lieu de nuget.org. NuGet 2.7 introduit une fonctionnalité de valeurs par défaut de Configuration qui autorise les valeurs par défaut de l’échelle de l’ordinateur soit spécifiée pour :

1. Sources de package est activée
1. Sources de package enregistré, mais désactivé
1. La source de push de nuget.exe par défaut

Chacun d'entre eux peut désormais être configuré au sein d’un fichier situé dans `%ProgramData%\NuGet\NuGetDefaults.Config`. Si ce fichier de configuration spécifie les sources de package, la source du package nuget.org par défaut ne sera pas enregistrée automatiquement et celles de `NuGetDefaults.Config` sera enregistré à la place.

Bien que ne pas nécessaire pour utiliser cette fonctionnalité, nous pensons aux entreprises de déployer `NuGetDefaults.Config` à l’aide de la stratégie de groupe de fichiers.

*Notez que cette fonctionnalité ne provoque jamais une source de package à supprimer à partir des paramètres de NuGet d’un développeur. Cela signifie que si le développeur a déjà utilisé NuGet et a par conséquent la source du package nuget.org inscrit, il ne sera pas supprimée après la création d’un `NuGetDefaults.Config` fichier.*

Consultez [NuGet Configuration par défaut est](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) pour plus d’informations sur cette fonctionnalité.

### <a name="renaming-the-default-package-source"></a>Modification du nom de la Source du Package par défaut

NuGet a inscrit toujours une source de package par défaut appelée « Officiel source de package NuGet » qui pointe sur nuget.org. Ce nom était détaillé et il n’a pas également spécifier où il a été réellement pointant vers la. Pour résoudre ces deux problèmes, nous avons renommé cette source de package pour simplement « nuget.org » dans l’interface utilisateur. L’URL de la source du package a été également modifié pour inclure « www ». « group. ». Après avoir utilisé NuGet 2.7, existant « NuGet officielle source du package » est automatiquement mise « nuget.org » comme son nom et «<https://www.nuget.org/api/v2/>» en tant que son URL.

### <a name="performance-improvements"></a>Amélioration des performances

Nous avons apporté une amélioration des performances dans 2.7 qui assureront une plus faible encombrement mémoire, moins l’utilisation du disque et l’installation du package plus rapidement. Nous avons apporté également des requêtes plus intelligemment aux flux basé sur OData, ce qui réduiront la charge globale.

### <a name="new-extensibility-apis"></a>Nouvelles API d’extensibilité

Nous avons ajouté certaines nouvelles API à nos services d’extensibilité pour combler le manque de fonctionnalités manquantes dans les versions précédentes.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>Dépendances de développement uniquement

Cette fonctionnalité a été rédigée par [Adam Ralph](https://twitter.com/adamralph) et il permet aux auteurs de package déclarer des dépendances qui ont été utilisées uniquement au développement de temps et ne nécessitent pas de dépendances de package. En ajoutant un `developmentDependency="true"` un package dans l’attribut `packages.config`, `nuget.exe pack` n’incluront plus ce package en tant que dépendance.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Supprimer la prise en charge pour Visual Studio 2010 Express pour Windows Phone

Le nouveau modèle de restauration de package dans 2.7 est implémenté par un VSPackage de nouveau ce qui diffère le NuGet VSPackage principale. En raison d’un problème technique, ce nouveau VSPackage s’affiche ne fonctionne pas correctement dans le *Visual Studio 2010 Express pour Windows Phone* référence (SKU) étant donné que nous partagent la même base de code avec d’autres références prises en charge Visual Studio. Par conséquent, à compter de NuGet 2.7, nous allons la prise en charge pour *Visual Studio 2010 Express pour Windows Phone* à partir de l’extension publiée. Prise en charge de *Visual Studio 2010 Express pour Web* est toujours incluse dans l’extension principale est publiée dans la galerie d’extensions Visual Studio.

Étant donné que nous ne savez pas combien de développeurs est toujours l’utilisation de NuGet dans cette version/édition de Visual Studio, nous utilisons une extension Visual Studio distincte spécifiquement pour les utilisateurs de la publication et publiez-la sur CodePlex (plutôt que de la galerie d’extensions Visual Studio) . Nous ne prévoyons pas de maintenir cette extension, mais si cela vous concerne, contactez-nous en signalant un problème sur CodePlex.

Pour télécharger le Gestionnaire de Package NuGet (pour Visual Studio 2010 Express pour Windows Phone), visitez le [NuGet 2.7 télécharge](https://nuget.codeplex.com/releases/view/107605) page.

### <a name="bug-fixes"></a>Correctifs de bogues

Outre ces fonctionnalités, cette version de NuGet inclut également plusieurs autres correctifs de bogues. Vous rencontrez des problèmes de total 97 résolus dans la version. Pour obtenir une liste complète de travail éléments résolus dans NuGet 2.7, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
