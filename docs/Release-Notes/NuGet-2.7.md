---
title: Notes de publication NuGet 2.7 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour 2.7 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 2.7 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 43638626661ae034bb0a1cc28958a2e2929f047f
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-27-release-notes"></a>Notes de version 2.7 NuGet

[NuGet 2.6.1 pour les Notes de publication WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 Notes de publication](../release-notes/nuget-2.7.1.md)

2.7 de NuGet a été publié le 22 août 2013.

## <a name="acknowledgements"></a>Remerciements

Nous aimerions remercier les collaborateurs externes suivantes pour leur contribution significative à NuGet 2.7 :

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Afficher les url de licence lorsque la liste des packages et des commentaires est détaillée.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -ajouter un attribut developmentDependency à `packages.config` et l’utiliser dans la commande pack pour inclure uniquement les packages de runtime
1. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Évitez de clé de propriétés en double dans la commande pack de nuget.exe.
1. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -augmenter la taille du cache de machine à 200.
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -NuGet de corriger de boîte de dialogue affichant des mises à jour dans l’onglet incorrect
    - Correctif Project.TargetFramework peut être null dans ResponsableProjet
    - [#3248](http://nuget.codeplex.com/workitem/3248) -résoudre SharedPackageRepository FindPackage/FindPackagesById échoue sur l’ID de package n’existe pas
1. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -activer la prise en charge pour le projet de Nomad
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -Échec de la commande push correctif avec la sortie de code 0 lorsque le fichier n’existe pas.
1. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -bogue correctif avec la commande Add-BindingRedirect lorsqu’un projet fait référence à un projet de base de données.
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -bogue de correctif de nuget.pack analyse incorrecte des caractères génériques dans l’attribut 'exclude'.
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -correctif de bogue `NuGet.targets` ne passe pas $(Platform) de nuget.exe lors de la restauration des packages.
1. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -bogue de correctif dans la commande d’un package de nuget.exe qui permettrait d’ajout de fichiers avec le même nom mais une casse différente, par la suite à l’origine d’exception de « Élément existe déjà ».
1. [Michel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [#2990](http://nuget.codeplex.com/workitem/2990) -propriété NetPortableProfile classe ajouter une Version.
1. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460) -corriger le bogue NullReferenceException si requireApiKey = true, mais l’en-tête X-NUGET-APIKEY n’est pas présent
1. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) -résout les NuGet.Build cibles le fichier pour qu’il fonctionne correctement sur MonoDevelop
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - Améliorer les performances de commande de restauration en augmentant la parallélisation

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="package-restore-by-default-with-implicit-consent"></a>Restauration des packages par défaut (avec un consentement implicite)

Introduit une nouvelle approche pour la restauration du package NuGet 2.7 et propose également un obstacle important : consentement de restauration de Package est désormais activé par défaut. La combinaison de la nouvelle approche et le consentement simplifie considérablement les scénarios de restauration de package.

#### <a name="implicit-consent"></a>Consentement implicite

Avec les versions 2.0, 2.1, 2.2, 2.5 et 2.6 de NuGet, les utilisateurs nécessaires pour autoriser explicitement NuGet à télécharger les packages manquants lors de build. Si cette autorisation n’a pas été explicitement reçu, puis les solutions qui avaient activé la restauration des packages ne parviennent pas à générer jusqu'à ce que l’utilisateur a donné son consentement.

À compter de NuGet 2.7, consentement de restauration de package est activé par défaut tout en permettant aux utilisateurs d’explicitement *participer* de restauration du package si vous le souhaitez, à l’aide de la case à cocher dans les paramètres de NuGet dans Visual Studio. Cette modification pour un consentement implicite affecte NuGet dans les environnements suivants :

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilitaire de ligne de commande de NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Restauration automatique de packages dans Visual Studio

À partir de NuGet 2.7, NuGet télécharge automatiquement les packages manquants pendant la génération dans Visual Studio, même si la restauration du package n’a pas été explicitement activée pour la solution. Cette restauration automatique des packages qui se produit dans Visual Studio lorsque vous générez un projet ou la solution, mais avant l’appel de MSBuild. Il en résulte plusieurs avantages significatifs :

1. Aucune autre besoin d’utiliser du mouvement « Activer la restauration des packages NuGet » de votre solution
1. Projets ne doivent pas être modifiés et NuGet ne sera pas apporter des modifications à votre projet pour garantir la restauration du package est activée.
1. Tous les packages NuGet, y compris celles incluant des importations de MSBuild pour les fichiers de propriétés/cibles, seront restaurées *avant* MSBuild est appelé, vous être assuré de ces propriétés/cibles sont correctement reconnus lors de la build

Pour pouvoir utiliser la restauration automatique de packages dans Visual Studio, vous devez uniquement effectuer une (action entrant) :

1. Ne pas vérifier votre `packages` dossier

Il existe plusieurs façons pour omettre votre `packages` dossier à partir du contrôle de code source. Pour plus d’informations, consultez la [Packages et contrôle de code Source](../consume-packages/packages-and-source-control.md) rubrique.

Alors que tous les utilisateurs sont implicitement quittent le consentement de la restauration automatique de packages, vous pouvez facilement refuser via les paramètres du Gestionnaire de Package dans Visual Studio.

![Paramètres du Gestionnaire de package](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Restauration simplifiée de Package à partir de la ligne de commande

NuGet 2.7 introduit une nouvelle fonctionnalité de nuget.exe : `nuget.exe restore`

Cette nouvelle commande de restauration vous permet de restaurer facilement tous les packages d’une solution avec une seule commande, en acceptant un fichier solution ou un dossier en tant qu’argument. En outre, cet argument est implicite lorsqu’il existe une seule solution dans le dossier actif. Cela signifie que tous les éléments suivants de travail à partir d’un dossier qui contient un fichier de solution unique (MySolution.sln) :

1. restauration de NuGet.exe MySolution.sln
1. restauration de NuGet.exe.
1. restauration de NuGet.exe

La commande de restauration ouvrez le fichier solution et rechercher tous les projets dans la solution. À partir de là, il trouve le `packages.config` fichiers pour chacun des projets et de restauration de tous les packages. Par ailleurs, les packages au niveau solution trouvées dans le `.nuget\packages.config` fichier. Vous trouverez plus d’informations sur la nouvelle commande de restauration dans le [référence de ligne de commande](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Le nouveau flux de travail de restauration de Package

Nous sommes ravis à ces modifications à la restauration des packages, car elle introduit un nouveau flux de travail. Si vous souhaitez omettre vos packages à partir du contrôle de code source vous simplement ne validez pas le `packages` dossier. Les utilisateurs de Visual Studio qui ouvrent et génèrent la solution seront affiche les packages automatiquement restaurés. Pour les versions de ligne de commande, simplement appeler `nuget.exe restore` avant d’appeler `msbuild`. Vous n’avez plus besoin de penser à utiliser le mouvement de « Activer la restauration des packages NuGet » sur votre solution, et nous allons n’avez plus besoin modifier vos projets pour modifier la build. Cela génère également une expérience considérablement améliorée pour les packages qui incluent des importations de MSBuild, en particulier pour les importations ajoutées via la fonctionnalité de récente de NuGet pour [important automatiquement les fichiers de propriétés/cibles](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) à partir du dossier \build.

Outre le travail que nous avons nous-mêmes, nous travaillons également avec certains partenaires importants pour compléter cette nouvelle approche. Nous n’avons pas chronologies concret de ces encore, mais chaque partenaire est très heureux car nous sommes sur la nouvelle approche.

* Le Service Team Foundation - qu’ils utilisent pour intégrer l’appel à `nuget.exe restore` générer des scénarios dans la valeur par défaut.
* Sites Web Windows Azure - qu’ils utilisent pour envoyer votre projet dans Azure et autoriser `nuget.exe restore` appelé avant la génération de votre site web.
* TeamCity - ils mettent à jour leur plug-in du programme d’installation de NuGet pour TeamCity 8.x
* AppHarbor - ils travaillent pour vous permettent de distribuer votre référentiel à AppHarbor et avoir `nuget.exe restore` appelée avant que votre solution est la build.

Avec chacun des partenaires ci-dessus, il convient d’utiliser leur propre copie de nuget.exe et vous ne devez pas effectuer de nuget.exe dans votre solution.

#### <a name="known-issues"></a>Problèmes connus

Présence de deux problèmes connus avec la restauration de nuget.exe avec la version 2.7 initiale, mais ils ont été résolus 6/9/2013 avec une mise à jour la [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/).  Cette mise à jour est également disponible sur le [page de téléchargement de NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) sur CodePlex.  En cours d’exécution `nuget.exe update -self` met à jour vers la dernière version.

Le texte fixe étaient :

1. [Restauration du package ne fonctionne pas sur Mono lorsque vous utilisez les fichiers SLN](https://nuget.codeplex.com/workitem/3596)
1. [Restauration du package ne fonctionne pas avec les projets Wix](https://nuget.codeplex.com/workitem/3598)

Il existe également un problème connu avec le nouveau flux de travail de restauration de package par laquelle [restauration des packages automatique ne fonctionne pas pour les projets dans un dossier de solution](https://nuget.codeplex.com/workitem/3625). Ce problème a été résolu dans NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Mise à niveau et de reciblage erreurs/avertissements sur la génération du projet

Nombre de fois après reciblage ou la mise à niveau de votre projet, vous trouvez que certains packages NuGet ne sont pas fonctionne correctement. Malheureusement, il n’existe aucune indication de cet et il n’existe pas d’instructions sur la façon de résoudre. Avec NuGet 2.7, nous utilisons maintenant certains événements de Visual Studio pour reconnaître quand vous avez reciblé ou mis à niveau votre projet d’une manière qui affecte vos packages NuGet installées.

Si nous détectons qu’un de vos packages ont été affecté par la mise à niveau ou de reciblage, nous allons générer des erreurs de génération immédiate pour vous informer. En plus de l’erreur de la génération immédiate, nous avons également de conserver un `requireReinstallation="true"` indicateur dans votre `packages.config` fichier pour tous les packages qui ont été affectés par le reciblage et chaque build dans Visual Studio génère les avertissements de génération des packages.

Bien que NuGet ne peut pas effectuer automatiquement une action pour réinstaller les packages concernés, nous espérons que cette indication et avertissement vous guide aide vous découvrez que vous deviez réinstaller les packages. Nous travaillons également [documentation du Guide de réinstallation du package](../consume-packages/reinstalling-and-updating-packages.md) que ces messages d’erreur vous dirigent vers.

### <a name="nuget-configuration-defaults"></a>Valeurs par défaut de la Configuration NuGet

De nombreuses sociétés utilisent NuGet en interne, mais ont des difficultés à guidage leurs développeurs pour utiliser des sources de package interne au lieu de nuget.org. NuGet 2.7 introduit une fonctionnalité de Configuration valeurs par défaut qui autorise les valeurs par défaut de l’échelle de l’ordinateur pour :

1. Sources de package activées
1. Sources de package enregistré, mais est désactivé
1. La source de push de nuget.exe par défaut

Chacun d’eux peut désormais être configuré dans un fichier situé à `%ProgramData%\NuGet\NuGetDefaults.Config`. Si ce fichier de configuration spécifie les sources de package, alors que la source du package par défaut nuget.org ne sera pas enregistrée automatiquement et celles de `NuGetDefaults.Config` sera inscrit à la place.

Ne pas requis pour utiliser cette fonctionnalité, nous pensons qu’aux entreprises de déployer `NuGetDefaults.Config` à l’aide de la stratégie de groupe de fichiers.

*Notez que cette fonctionnalité ne provoque jamais une source de package à supprimer les paramètres d’un développeur NuGet. Cela signifie que si le développeur a déjà utilisé NuGet et donc la source du package nuget.org inscrit, il ne seront pas supprimé après la création d’un `NuGetDefaults.Config` fichier.*

Consultez [par défaut de Configuration NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) pour plus d’informations sur cette fonctionnalité.

### <a name="renaming-the-default-package-source"></a>Modification du nom de la Source du Package par défaut

NuGet a inscrit toujours une source de package par défaut appelée « Officiel source du package NuGet » qui pointe vers nuget.org. Ce nom a été documenté et elle n’a pas également spécifier où il a été réellement pointe. Pour résoudre ces deux problèmes, nous avons renommé cette source de package simplement « nuget.org » dans l’interface utilisateur. L’URL de la source du package a été également modifié pour inclure « www ». préfixe. Après l’utilisation de NuGet 2.7, votre existante « source de package officielle de NuGet » mettra automatiquement à jour « nuget.org » en tant que son nom et « https://www.nuget.org/api/v2/ » en tant que son URL.

### <a name="performance-improvements"></a>Amélioration des performances

Nous avons apporté une amélioration des performances dans 2.7 qui retournera le plus faible encombrement mémoire, moins l’utilisation du disque et l’installation du package plus rapide. Aussi, nous avons apporté des requêtes plus efficacement à des flux OData qui permet de réduire la charge globale.

### <a name="new-extensibility-apis"></a>Nouvelles API d’extensibilité

Nous avons ajouté de nouvelles API à nos services d’extensibilité pour combler les lacunes de fonctionnalités manquantes dans les versions précédentes.

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

Cette fonctionnalité a été fournie par [Adam Ralph](https://twitter.com/adamralph) et il permet aux auteurs de package déclarer des dépendances qui ont été utilisées uniquement au développement de temps et ne nécessitent pas les dépendances de package. En ajoutant un `developmentDependency="true"` un package dans l’attribut `packages.config`, `nuget.exe pack` n’incluront plus de ce package en tant que dépendance.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Supprimer la prise en charge pour Visual Studio 2010 Express pour Windows Phone

Le nouveau modèle de restauration de package de 2.7 est implémenté par un nouveau VSPackage qui est différent du NuGet VSPackage principal. En raison d’un problème technique, ce nouveau VSPackage ne fonctionne pas correctement dans le *Visual Studio 2010 Express pour Windows Phone* référence (SKU) étant donné que nous partagent la même base de code avec d’autres prises en charge références (SKU) de Visual Studio. Par conséquent, à partir de NuGet 2.7, nous allons suppression prise en charge de *Visual Studio 2010 Express pour Windows Phone* à partir de l’extension publiée. Prise en charge de *Visual Studio 2010 Express pour Web* est toujours inclus dans l’extension principale publiée dans la galerie d’extensions Visual Studio.

Étant donné que nous ne savez pas combien les développeurs sont toujours l’utilisation de NuGet dans cette version/édition de Visual Studio, nous sommes une extension Visual Studio distincte spécifiquement pour les utilisateurs de publication et sa publication sur CodePlex (plutôt que la galerie d’extensions Visual Studio) . Nous ne prévoyez pas de continuer à mettre à jour cette extension, mais si cela vous concerne, faites-le nous savoir en créant un problème sur CodePlex.

Pour télécharger le Gestionnaire de Package NuGet (pour Visual Studio 2010 Express pour Windows Phone), visitez le [2.7 de NuGet télécharge](https://nuget.codeplex.com/releases/view/107605) page.

### <a name="bug-fixes"></a>Correctifs de bogues

Outre ces fonctionnalités, cette version de NuGet inclut également plusieurs autres correctifs de bogues. Il existait des problèmes de total 97 traités dans la mise en production. Pour obtenir la liste complète de travail éléments corrigés dans NuGet 2.7, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
