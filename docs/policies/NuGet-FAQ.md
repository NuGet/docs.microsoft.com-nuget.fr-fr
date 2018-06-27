---
title: Questions fréquentes (FAQ) sur NuGet
description: Questions courantes et réponses sur l’utilisation de NuGet depuis la ligne de commande et dans Visual Studio et sur l’utilisation de la galerie NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: e3c52f1e49a53b89d7e5c0728c02a7915db2aeb9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817978"
---
# <a name="nuget-frequently-asked-questions"></a>Questions fréquentes (FAQ) sur NuGet

**Quels sont les éléments nécessaires pour exécuter NuGet ?**

Toutes les informations relatives à l’interface utilisateur et aux outils en ligne de commande sont disponibles dans le [guide d’installation](../install-nuget-client-tools.md).

**NuGet prend-il en charge Mono ?**

L’outil en ligne de commande, `nuget.exe`, génère et s’exécute sous Mono 3.2+ et peut créer des packages dans Mono.

Bien que `nuget.exe` fonctionne entièrement sur Windows, il existe des problèmes connus sur Linux et OS X. Consultez [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) (Problèmes Mono) sur GitHub.

Un [client graphique](https://github.com/mrward/monodevelop-nuget-addin) est disponible en guise de complément pour MonoDevelop.

**Comment puis-je déterminer ce que contient un package et s’il est stable et utile pour mon application ?**

La principale source d’apprentissage sur un package est sa page d’annonce sur nuget.org (ou sur un autre flux privé). Chaque page de package sur nuget.org inclut une description du package, son historique des versions et les statistiques d’utilisation. La section **Info** sur la page de package contient également un lien vers le site web du projet où vous trouvez généralement de nombreux exemples et autres documentations pour vous aider à découvrir comment le package est utilisé.

Pour plus d’informations, consultez [Recherche et sélection des packages](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet dans Visual Studio

**Comment NuGet est-il pris en charge dans les différents produits Visual Studio ?**

- Visual Studio sur Windows prend en charge [l’interface utilisateur du Gestionnaire de package](../tools/package-manager-ui.md) et la [console du Gestionnaire de package](../tools/package-manager-console.md).
- Visual Studio pour Mac offre des fonctionnalités NuGet intégrées, comme décrit dans [Inclusion d’un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (toutes les plateformes) n’a pas d’intégration directe de NuGet. Utilisez [l’interface de ligne de commande NuGet](../tools/nuget-exe-cli-reference.md) ou [l’interface de ligne de commande dotnet](../tools/dotnet-commands.md).
- Visual Studio Team Services fournit [une étape de génération pour restaurer les packages NuGet](/vsts/build-release/tasks/package/nuget). Vous pouvez également [héberger les flux de package NuGet privés sur Team Services](https://www.visualstudio.com/docs/package/nuget/publish).

**Comment vérifier la version exacte des outils NuGet qui sont installés ?**

Dans Visual Studio, utilisez la commande **Aide > À propos de Microsoft Visual Studio** et examinez la version affichée en regard de **Gestionnaire de package NuGet**.

Vous pouvez également lancer la console du Gestionnaire de package (**Outils > Gestionnaire de package NuGet > Console du Gestionnaire de package**), puis entrer `$host` pour afficher des informations sur NuGet, notamment la version.

**Quels sont les langages de programmation pris en charge par NuGet ?**

En règle générale, NuGet fonctionne pour les langages .NET et est conçu pour intégrer les bibliothèques .NET dans un projet. Comme il prend également en charge MSBuild et Visual Studio Automation dans certains types de projets, il prend aussi en charge d’autres projets et langages à des degrés divers.

La version la plus récente de NuGet prend en charge C#, Visual Basic, F#, WiX et C++.

**Quels sont les modèles de projet pris en charge par NuGet ?**

NuGet prend totalement en charge de nombreux modèles de projet tels que Windows, Web, Cloud, SharePoint, Wix, etc.

**Comment mettre à jour les packages qui font partie de modèles Visual Studio ?**

Accédez à l’onglet **Mises à jour** dans l’interface utilisateur du Gestionnaire de package et sélectionnez **Mettre à jour tout**, ou utilisez la [commande `Update-Package`](../tools/ps-ref-update-package.md) à partir de la console du Gestionnaire de package.

Pour mettre à jour le modèle lui-même, vous devez mettre à jour manuellement le dépôt du modèle. Consultez le [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) à ce sujet. Notez que cette opération est effectuée à vos risques et périls, étant donné que les mises à jour manuelles peuvent endommager le modèle si les dernières versions de toutes les dépendances ne sont pas compatibles entre elles.

**Puis-je utiliser NuGet en dehors de Visual Studio ?**

Oui, NuGet fonctionne directement à partir de la ligne de commande. Consultez le [guide d’installation](../install-nuget-client-tools.md) et les [informations de référence sur l’interface de ligne de commande](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Ligne de commande NuGet

**Comment obtenir la dernière version de l’outil en ligne de commande NuGet ?**

Consultez le [guide d’installation](../install-nuget-client-tools.md).

**Quelle est la licence pour nuget.exe ?**

Vous êtes autorisé à redistribuer nuget.exe selon les termes de la licence du MIT. Vous êtes responsable de la mise à jour et de la maintenance de toutes les copies de nuget.exe que vous souhaitez redistribuer.

**Est-il possible d’étendre l’outil en ligne de commande NuGet ?**

Oui, vous pouvez ajouter des commandes personnalisées à `nuget.exe`, comme le décrit le [billet de blog de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Console du Gestionnaire de package NuGet (Visual Studio sur Windows)

**Comment accéder à l’objet DTE dans la console du Gestionnaire de package ?**

L’objet de niveau supérieur dans le modèle objet automation Visual Studio est appelé objet DTE (Development Tools Environment). La console le fournit par le biais d’une variable nommée `$DTE`. Pour plus d’informations, consultez [Vue d’ensemble du modèle Automation](/visualstudio/extensibility/internals/automation-model-overview) dans la documentation de l’extensibilité de Visual Studio.

**J’essaie de caster la variable $DTE en type DTE2, mais j’obtiens une erreur indiquant qu’il est impossible de convertir la valeur « EnvDTE.DTEClass » du type « EnvDTE.DTEClass » en type « EnvDTE80.DTE2 ». Quel est le problème ?**

Il s’agit d’un problème connu lié à la façon dont PowerShell interagit avec un objet COM. Essayez l’opération suivante :

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` est une fonction d’assistance ajoutée par l’hôte PowerShell NuGet.

## <a name="creating-and-publishing-packages"></a>Création et publication de packages

**Comment répertorier mon package dans un flux ?**

Consultez [Création et publication d’un package](../quickstart/create-and-publish-a-package.md).

**Plusieurs versions de ma bibliothèque ciblent des versions différentes du .NET Framework. Comment créer un package unique qui prend en charge ce cas de figure ?**

Consultez [Prise en charge de plusieurs versions et profils du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**Comment définir mon propre dépôt ou flux ?**

Consultez la [vue d’ensemble de l’hébergement des packages](../hosting-packages/overview.md).

**Comment charger des packages sur mon flux NuGet en bloc ?**

Consultez [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (Publication de packages NuGet en bloc) (jeffhandly.com).

## <a name="working-with-packages"></a>Utilisation des packages

**Quelle est la différence entre un package au niveau du projet et un package au niveau de la solution ?**

Un package au niveau de la solution (NuGet 3.x+) est installé une seule fois dans une solution, puis est disponible pour tous les projets de la solution. Un package au niveau du projet est installé dans chaque projet qui l’utilise. Un package au niveau de la solution peut également installer de nouvelles commandes qui peuvent être appelées à partir de la console du Gestionnaire de package.

**Est-il possible d’installer des packages NuGet sans connexion Internet ?**

Oui, consultez le billet de Blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Comment installer des packages dans un autre emplacement que le dossier de packages par défaut ?**

Définissez le paramètre [`repositoryPath`](../reference/nuget-config-file.md#config-section) dans `Nuget.Config` en utilisant `nuget config -set repositoryPath=<path>`.

**Comment éviter d’ajouter le dossier de packages NuGet dans le contrôle de code source ?**

Définissez [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) dans `Nuget.Config` sur `true`. Cette clé, qui fonctionne au niveau de la solution, doit être ajoutée au fichier `$(Solutiondir)\.nuget\Nuget.Config`. L’activation de la restauration des packages à partir de Visual Studio crée ce fichier automatiquement.

**Comment désactiver la restauration des packages ?**

Consultez [Activation et désactivation de la restauration des packages](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Quand j’installe un package local avec des dépendances distantes, j’obtiens un message indiquant qu’il est impossible de résoudre une erreur de dépendance. Pourquoi ?**

Vous devez sélectionner la source **Tous** durant l’installation d’un package local dans le projet. Cette option regroupe tous les flux au lieu d’en utiliser un seul. Cette erreur est liée au fait que les utilisateurs d’un dépôt local souhaitent souvent éviter d’installer accidentellement un package distant en raison de stratégies d’entreprise.

**J’ai plusieurs projets dans le même dossier ; comment utiliser des fichiers packages.config distincts pour chaque projet ?**

Dans la plupart des projets où des projets distincts se trouvent dans des dossiers séparés, ce n’est pas un problème, car NuGet identifie les fichiers `packages.config` dans chaque projet. Si vous utilisez NuGet 3.3+ et que plusieurs projets se trouvent dans le même dossier, vous pouvez insérer le nom du projet dans les noms de fichier `packages.config` et utiliser le modèle `packages.{project-name}.config` ; NuGet utilise alors ce fichier.

Cela n’est pas un problème si vous utilisez PackageReference, car chaque fichier de projet contient sa propre liste de dépendances.

**Je ne vois pas nuget.org dans la liste des dépôts ; comment le récupérer ?**

- Ajoutez `https://api.nuget.org/v3/index.json` à votre liste de sources, ou
- Supprimez `%appdata%\.nuget\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) et laissez NuGet le recréer.

**Quels sont les termes du contrat de licence si un package ne fournit pas des informations de licence spécifiques ?**

Chaque package est régi par les conditions qu’il inclut. Vous devez examiner les conditions applicables avant d’accéder à des packages, d’en télécharger ou d’en acquérir. Sur nuget.org, utilisez le lien **License Info** (Informations de licence) sur la page des packages.

Si un package ne spécifie pas les termes du contrat de licence, contactez le propriétaire du package directement à l’aide du lien **Contact owners** (Contacter les propriétaires) sur la page des packages nuget.org. Microsoft ne vous concède aucune licence de propriété intellectuelle de fournisseurs de packages tiers et n’est pas responsable des informations fournies par des tiers.

## <a name="managing-packages-on-nugetorg"></a>Gestion des packages sur nuget.org

**Puis-je modifier les métadonnées d’un package après l’avoir chargé ?**

NuGet recommande de signer tous les packages. Un principe de conception de la signature du package est que le contenu du package signé doit être immuable, ce qui comprend le fichier nuspec. Modifier les métadonnées du package entraîne des modifications du fichier nuspec, invalidant les signatures existantes. Nous vous recommandons de modifier les flux de travail existants de manière à ce qu’il ne soit pas nécessaire de modifier les métadonnées du package une fois ce dernier créé.

Notez que les dépendances répertoriées pour votre package sont générées automatiquement à partir du package lui-même et qu’elles ne peuvent pas être modifiées.

De plus, le chargement d’un package sur [staging.nuget.org](http://staging.nuget.org) est un excellent moyen de le tester et de le valider sans le mettre à disposition dans la galerie publique.

**Est-il possible de réserver des noms pour les packages destinés à être publiés ?**

Oui. Vous pouvez réserver des ID pour les packages sur [nuget.org](https://www.nuget.org/) en demandant un préfixe d’ID de package pour votre compte. Pour demander un préfixe d’ID de package, suivez les instructions de la [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Comment revendiquer la propriété de packages ?**

Consultez [Gestion des propriétaires de packages sur nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Comment négocier avec un propriétaire de package qui viole ma licence de logiciel ?**

Nous invitons la communauté NuGet à collaborer afin de résoudre les litiges pouvant survenir entre les propriétaires de packages et les propriétaires d’autres logiciels. Nous avons conçu un [processus de résolution des litiges](../policies/dispute-resolution.md) à suivre avant de demander aux administrateurs de nuget.org d’intervenir.

**Est-il recommandé de charger mes packages de test sur nuget.org ?**

À des fins de test, vous pouvez utiliser [staging.nuget.org](http://staging.nuget.org), ou d’autres serveurs NuGet publics comme [myget.org](https://myget.org) ou [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Notez que les packages chargés sur staging.nuget.org ne sont pas nécessairement conservés. Consultez [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).

**Quelle est la taille maximale des packages que je peux charger sur nuget.org ?**

La taille maximale de package autorisée par nuget.org est de 250 Mo, mais nous vous recommandons de limiter la taille des packages à 1 Mo maximum si possible et de les lier à l’aide de dépendances. En règle générale, les packages contiennent un seul assembly pour éviter les collisions.

NuGet utilisant HTTP pour télécharger les packages, l’installation d’un package risque d’autant plus d’échouer que celui-ci est volumineux.

Vous pouvez partager des dépendances entre plusieurs packages, pour réduire la taille totale du téléchargement pour les consommateurs de vos packages NuGet.

Les dépendances sont principalement statiques et ne changent jamais. Quand vous résolvez un bogue dans le code, il peut s’avérer superflu de mettre à jour les dépendances. Si vous regroupez des dépendances, vous finissez systématiquement par relivrer des packages plus volumineux. Si vous fractionnez les packages NuGet en dépendances connexes, les mises à niveau sont beaucoup plus précises pour les consommateurs de votre package.

## <a name="nugetorg-not-accessible"></a>nuget.org inaccessible

**Pourquoi ne puis-je pas télécharger de packages à partir de nuget.org ou en y charger ?**

Tout d’abord, veillez à utiliser les dernières versions de NuGet. Si cette version continue à échouer, [contactez le support technique](https://www.nuget.org/policies/Contact) et fournissez des informations supplémentaires pour la résolution du problème de connexion, notamment les suivantes :

- Version de NuGet que vous utilisez
- Sources de package que vous utilisez
- Journal de restauration avec commentaires détaillés
- MTR ou traces Fiddler (voir ci-dessous)
- Votre zone géographique
- Version de votre système d’exploitation
- Configuration de la machine (processeur, réseau, disque dur)
- Si votre machine se trouve derrière un pare-feu ou proxy
- Versions de .NET installées sur la machine
- Versions des outils multiplateformes telles que l’interface de ligne de commande .NET ou DNU que vous utilisez

*Pour capturer MTR :*

- Téléchargez WinMTR à partir de [http://winmtr.net/download/](http://winmtr.net/).
- Entrez `api.nuget.org` comme nom d’hôte et cliquez sur **Start** (Démarrer).
- Attendez que la colonne **Sent** (Envoyé) soit supérieure ou égale à 100.

    ![Capture de MTR](media/mtr.png)

- Copiez le texte dans le Presse-papiers.

*Pour capturer Fiddler :*

- Installez la version la plus récente de [Fiddler](http://www.telerik.com/download/fiddler).
- Démarrez Fiddler et désactivez la capture du trafic à l’aide du menu **File > Capture Traffic** (Fichier > Capturer le trafic).
- Supprimez toutes les sessions (sélectionnez tous les éléments de la liste, puis appuyez sur la touche **Supprimer**).
- Configurez Fiddler pour capturer le trafic HTTPS en cochant **Decrypt HTTPS traffic** (Déchiffrer le trafic HTTPS) sous l’onglet **HTTPS** du menu **Tools > Fiddler Options...** (Outils > Options Fiddler...).
- Fermez Visual Studio.
- Activez **l’option Capture Traffic (Capturer le trafic) dans le menu File (Fichier)**.
- Démarrez Visual Studio ou nuget.exe et effectuez les actions qui ne fonctionnent pas. Le trafic généré par ces actions doit s’afficher dans Fiddler.
- Une fois les actions exécutées, utilisez **File > Save > All Sessions** (Fichier > Enregistrer > Toutes les sessions) pour stocker les sessions capturées.

Remarque : Il peut être nécessaire de définir la variable d’environnement `HTTP_PROXY` sur `http://127.0.0.1:8888` pour router le trafic NuGet via Fiddler.

Si cette opération échoue, essayez les [conseils mentionnés dans ce billet de StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

**Quels sont les points de terminaison d’API pour nuget.org ?**

V3 : `https://api.nuget.org/v3/index.json` V2 : `https://www.nuget.org/api/v2/` (Notez que l’API V2 est dépréciée et ne fonctionne pas avec NuGet 4+.)
