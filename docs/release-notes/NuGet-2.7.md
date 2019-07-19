---
title: Notes de publication de NuGet 2,7
description: Notes de publication de NuGet 2,7, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f26ac80046ec321ce5bdbf2bac23c0e1939cd69a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317084"
---
# <a name="nuget-27-release-notes"></a>Notes de publication de NuGet 2,7

[Notes de publication de NuGet 2.6.1 pour WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) | notes de[publication NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2,7 a été publié le 22 août 2013.

## <a name="acknowledgements"></a>Remerciements

Nous aimerions remercier les contributeurs externes suivants pour leurs contributions significatives à NuGet 2,7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Afficher l’URL de licence lorsque vous répertoriez les packages et le niveau de détail est détaillé.
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -ajouter l’attribut developmentDependency `packages.config` à et l’utiliser dans la commande Pack pour inclure uniquement des packages Runtime
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Évitez la clé de propriétés dupliquées dans la commande de Pack NuGet. exe.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) : augmentez la taille du cache de la machine à 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -corriger la boîte de dialogue NuGet avec les mises à jour dans l’onglet incorrect
    - Corriger Project. TargetFramework peut avoir la valeur null dans ProjectManager
    - [#3248](http://nuget.codeplex.com/workitem/3248) -Fix SharedPackageRepository FindPackage/FindPackagesById échoue sur les packageId inexistants
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -activer la prise en charge pour le projet Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - la commande [#3252](http://nuget.codeplex.com/workitem/3252) -Fix Push échoue avec le code de sortie 0 lorsque le fichier n’existe pas.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -corriger le bogue avec la commande Add-bindingRedirect lorsqu’un projet fait référence à un projet de base de données.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -corriger le bogue du caractère générique d’analyse de NuGet. Pack dans l’attribut’Exclude’de manière incorrecte.
10. [Justin](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -Fix bogue `NuGet.targets` ne passe pas la valeur $ (Platform) à NuGet. exe lors de la restauration des packages.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -corriger le bogue dans la commande de package NuGet. exe qui autorise l’ajout de fichiers portant le même nom mais avec une casse différente, provoquant éventuellement l’exception «élément déjà existant».
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -ajouter la propriété de version à la classe NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -corriger l’exception NullReferenceException si requireApiKey = true, mais que l’en-tête X-NUGET-apikey n’est pas présent
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) : corrige le fichier de cibles NuGet. Build pour qu’il fonctionne correctement sur MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Améliorez les performances des commandes de restauration en renforçant la parallélisation

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="package-restore-by-default-with-implicit-consent"></a>Restauration des packages par défaut (avec consentement implicite)

NuGet 2,7 introduit une nouvelle approche de la restauration des packages et est également un obstacle majeur: Le consentement de restauration de package est maintenant activé par défaut. La combinaison de la nouvelle approche et du consentement implicite simplifie considérablement les scénarios de restauration des packages.

#### <a name="implicit-consent"></a>Consentement implicite

Avec les versions NuGet 2,0, 2,1, 2,2, 2,5 et 2,6, les utilisateurs devaient autoriser explicitement NuGet à télécharger les packages manquants pendant la génération. Si ce consentement n’a pas été explicitement donné, les solutions qui avaient activé la restauration du package ne pourront pas être générées tant que l’utilisateur n’avait pas donné son consentement.

À compter de NuGet 2,7, le consentement de restauration de package est activé par défaut, tout en permettant aux utilisateurs de *refuser* explicitement la restauration des packages, si nécessaire, à l’aide de la case à cocher dans les paramètres de NuGet dans Visual Studio. Ce changement de consentement implicite affecte NuGet dans les environnements suivants:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilitaire de ligne de commande NuGet. exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Restauration automatique des packages dans Visual Studio

À compter de NuGet 2,7, NuGet téléchargera automatiquement les packages manquants lors de la génération dans Visual Studio, même si la restauration de package n’a pas été explicitement activée pour la solution. Cette restauration automatique des packages se produit dans Visual Studio quand vous générez un projet ou la solution, mais avant l’appel de MSBuild. Cela donne quelques avantages significatifs:

1. Vous n’avez plus besoin d’utiliser le geste «activer la restauration des packages NuGet» sur votre solution
1. Les projets n’ont pas besoin d’être modifiés, et NuGet n’apporte pas de modifications à votre projet pour garantir l’activation de la restauration des packages
1. Tous les packages NuGet, y compris ceux qui incluaient les importations MSBuild pour les fichiers props/cibles, seront restaurés avant l’appel de MSBuild, ce qui garantit *que* ces props/cibles sont correctement reconnues pendant la génération

Pour pouvoir utiliser la restauration automatique des packages dans Visual Studio, vous devez effectuer une seule action (dans):

1. Ne pas archiver votre `packages` dossier

Il existe plusieurs façons d’omettre votre `packages` dossier dans le contrôle de code source. Pour plus d’informations, consultez la rubrique [packages et contrôle de code source](../consume-packages/packages-and-source-control.md) .

Bien que tous les utilisateurs choisissent implicitement le consentement de la restauration automatique des packages, vous pouvez facilement désactiver les paramètres du gestionnaire de package dans Visual Studio.

![Paramètres du gestionnaire de package](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Simplification de la restauration des packages à partir de la ligne de commande

NuGet 2,7 introduit une nouvelle fonctionnalité pour NuGet. exe:`nuget.exe restore`

Cette nouvelle commande de restauration vous permet de restaurer facilement tous les packages d’une solution à l’aide d’une seule commande, en acceptant un fichier solution ou un dossier comme argument. En outre, cet argument est implicite lorsqu’il n’existe qu’une seule solution dans le dossier actif. Cela signifie que les éléments suivants fonctionnent tous à partir d’un dossier qui contient un seul fichier solution (MySolution. sln):

1. NuGet. exe Restore MySolution. sln
1. restauration de NuGet. exe.
1. restauration de NuGet. exe

La commande Restore ouvre le fichier solution et recherche tous les projets de la solution. À partir de là, il trouvera `packages.config` les fichiers de chacun des projets et restaurera tous les packages trouvés. Il restaure également les packages de niveau solution trouvés dans le `.nuget\packages.config` fichier. Vous trouverez plus d’informations sur la nouvelle commande Restore dans la référence de la [ligne de commande](../reference/cli-reference/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Le nouveau flux de travail de restauration de package

Nous sommes ravis de ces modifications apportées à la restauration des packages, car elles introduisent un nouveau flux de travail. Si vous souhaitez omettre vos packages dans le contrôle de code source, vous ne `packages` devez tout simplement pas valider le dossier. Les utilisateurs de Visual Studio qui ouvrent et génèrent la solution verront automatiquement les packages restaurés. Pour les générations à partir de la ligne `nuget.exe restore` de commande, `msbuild`appelez simplement avant d’appeler. Vous n’avez plus besoin de vous souvenir d’utiliser le geste «activer la restauration des packages NuGet» sur votre solution, et il n’est plus nécessaire de modifier vos projets pour modifier la Build. Cela offre également une expérience nettement améliorée pour les packages qui incluent des importations MSBuild, en particulier pour les importations ajoutées par le biais de la fonctionnalité récente de NuGet pour l' [importation automatique des fichiers props/targets](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) à partir du dossier \build.

En plus du travail que nous avons fait nous-même, nous travaillons également avec certains partenaires importants pour faire part de cette nouvelle approche. Nous n’avons pas encore de chronologie concrète pour l’une de ces solutions, mais chaque partenaire est ravi de la nouvelle approche.

* Team Foundation Service: ils travaillent à intégrer l’appel à `nuget.exe restore` dans les scénarios de génération par défaut.
* Sites Web Windows Azure: ils travaillent pour vous permettre de pousser votre projet vers Azure et d’avoir `nuget.exe restore` appelé avant la génération de votre site Web.
* TeamCity: ils mettent à jour leur plug-in de programme d’installation NuGet pour TeamCity 8. x
* AppHarbor: ils travaillent pour vous permettre de pousser vos référentiel vers AppHarbor et `nuget.exe restore` de les appeler avant la génération de votre solution.

Avec chacun des partenaires ci-dessus, ils utilisent leur propre copie de NuGet. exe et vous n’avez pas besoin de transporter NuGet. exe dans votre solution.

#### <a name="known-issues"></a>Problèmes connus

Deux problèmes connus liés à la restauration de NuGet. exe se sont produits avec la version 2,7 initiale, mais ils ont été corrigés le 9/6/2013 avec une mise à jour du [package NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/).  Cette mise à jour est également disponible sur la [page de téléchargement de NuGet 2,7](https://nuget.codeplex.com/releases/view/107605) sur CodePlex.  L' `nuget.exe update -self` exécution de est mise à jour vers la dernière version.

Les corrections étaient:

1. [La restauration d’un nouveau package ne fonctionne pas sur mono lors de l’utilisation du fichier SLN](https://nuget.codeplex.com/workitem/3596)
1. [La restauration d’un nouveau package ne fonctionne pas avec les projets WiX](https://nuget.codeplex.com/workitem/3598)

Il existe également un problème connu avec le nouveau flux de travail de restauration de package qui [ne fonctionne pas pour la restauration automatique des packages pour les projets dans un dossier de solution](https://nuget.codeplex.com/workitem/3625). Ce problème a été résolu dans NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Reciblage et mise à niveau du projet erreurs/avertissements de build

Bien souvent, après avoir reciblé ou mis à niveau votre projet, vous constatez que certains packages NuGet ne fonctionnent pas correctement. Malheureusement, il n’y a aucune indication de cela et il n’y a pas d’indications sur la manière de le résoudre. Avec NuGet 2,7, nous utilisons maintenant certains événements Visual Studio pour reconnaître si vous avez reciblé ou mis à niveau votre projet d’une manière qui affecte vos packages NuGet installés.

Si nous détectons que l’un de vos packages était affecté par le reciblage ou la mise à niveau, nous produisons des erreurs de build immédiates pour vous en informer. En plus de l’erreur de build immédiate, nous permettons `requireReinstallation="true"` également un indicateur `packages.config` dans votre fichier pour tous les packages qui ont été affectés par le reciblage, et chaque Build suivante dans Visual Studio déclenchera des avertissements de génération pour ces packages.

Même si NuGet ne peut pas effectuer d’action automatique pour réinstaller les packages affectés, nous espérons que cette indication et cet avertissement vous guideront pour vous aider à découvrir les cas où vous devrez réinstaller des packages. Nous travaillons également sur [la documentation sur la réinstallation des packages](../consume-packages/reinstalling-and-updating-packages.md) que ces messages d’erreur vous dirigent.

### <a name="nuget-configuration-defaults"></a>Valeurs par défaut de la configuration NuGet

De nombreuses entreprises utilisent NuGet en interne, mais ont eu un temps dur pour guider leurs développeurs à utiliser des sources de package internes au lieu de nuget.org. NuGet 2,7 introduit une fonctionnalité de configuration par défaut qui permet de spécifier des valeurs par défaut à l’ensemble de l’ordinateur pour:

1. Sources de packages activées
1. Sources de packages inscrites, mais désactivées
1. Source Push NuGet. exe par défaut

Chacune d’elles peut désormais être configurée dans un fichier situé `%ProgramData%\NuGet\NuGetDefaults.Config`à l’emplacement. Si ce fichier de configuration spécifie des sources de package, la source du package NuGet.org par défaut n’est pas inscrite `NuGetDefaults.Config` automatiquement, et celles dans sont inscrites à la place.

Bien qu’il ne soit pas nécessaire d’utiliser cette fonctionnalité, nous `NuGetDefaults.Config` pensons que les entreprises déploient des fichiers à l’aide de stratégie de groupe.

*Notez que cette fonctionnalité ne provoque jamais la suppression d’une source de package des paramètres NuGet d’un développeur. Cela signifie que si le développeur a déjà utilisé NuGet et qu’il a par conséquent enregistré la source du package NuGet.org, il ne sera pas `NuGetDefaults.Config` supprimé après la création d’un fichier.*

Pour plus d’informations sur cette fonctionnalité, consultez [paramètres de configuration par défaut de NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) .

### <a name="renaming-the-default-package-source"></a>Attribution d’un nouveau nom à la source du package par défaut

NuGet a toujours inscrit une source de package par défaut appelée «source de package officielle NuGet» qui pointe vers nuget.org. Ce nom a été détaillé et n’a pas non plus spécifié l’emplacement de son point. Pour résoudre ces deux problèmes, nous avons renommé la source du package en «nuget.org» dans l’interface utilisateur. L’URL de la source du package a également été modifiée pour inclure le «www.» . Après l’utilisation de NuGet 2,7, votre «source de package officiel NuGet» existante sera automatiquement mise à jour vers «NuGet.org» en<https://www.nuget.org/api/v2/>tant que nom et «» en tant qu’URL.

### <a name="performance-improvements"></a>Amélioration des performances

Nous avons apporté des améliorations de performances dans 2,7, ce qui permet de réduire l’encombrement de mémoire, de réduire l’utilisation du disque et d’accélérer l’installation des packages. Nous avons également apporté des requêtes plus intelligentes aux flux basés sur OData, ce qui réduira la charge utile globale.

### <a name="new-extensibility-apis"></a>Nouvelles API d’extensibilité

Nous avons ajouté de nouvelles API à nos services d’extensibilité pour combler le fossé des fonctionnalités manquantes dans les versions précédentes.

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

Cette fonctionnalité a été fournie par [Adam Ralph](https://twitter.com/adamralph) et permet aux créateurs de packages de déclarer des dépendances qui ont été utilisées uniquement au moment du développement et qui ne nécessitent pas de dépendances de package. En ajoutant un `developmentDependency="true"` attribut à un package dans `packages.config`, `nuget.exe pack` n’inclut plus ce package en tant que dépendance.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Suppression de la prise en charge de Visual Studio 2010 Express pour Windows Phone

Le nouveau modèle de restauration de package de 2,7 est implémenté par un nouveau VSPackage qui est différent du VSPackage NuGet principal. En raison d’un problème technique, ce nouveau VSPackage ne fonctionne pas correctement dans la référence SKU *Visual studio 2010 Express pour Windows Phone* , car nous partageons la même base de code avec d’autres références SKU Visual Studio prises en charge. Par conséquent, à partir de NuGet 2,7, nous supprimons la prise en charge de *Visual Studio 2010 Express pour Windows Phone* de l’extension publiée. La prise en charge de *Visual studio 2010 Express pour le Web* est toujours incluse dans l’extension principale publiée dans la Galerie d’extensions Visual Studio.

Étant donné que nous ne sommes pas certains des développeurs qui utilisent encore NuGet dans cette version/édition de Visual Studio, nous publions une extension Visual Studio distincte spécifiquement pour ces utilisateurs et en les publiant sur CodePlex (plutôt que dans la Galerie d’extensions de Visual Studio) . Nous ne prévoyons pas de continuer à gérer cette extension, mais si cela vous concerne, faites-le nous savoir en signalant un problème sur CodePlex.

Pour télécharger le gestionnaire de package NuGet (pour Visual Studio 2010 Express pour Windows Phone), visitez la page de [téléchargements nuget 2,7](https://nuget.codeplex.com/releases/view/107605) .

### <a name="bug-fixes"></a>Correctifs de bogues

Outre ces fonctionnalités, cette version de NuGet comprend également de nombreux autres correctifs de bogues. 97 problèmes ont été résolus dans la version. Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2,7, consultez le [suivi des problèmes NuGet pour cette version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
