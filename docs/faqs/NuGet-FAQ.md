---
title: Questions fréquentes (FAQ) sur NuGet
description: Questions courantes et réponses sur l’utilisation de NuGet depuis la ligne de commande et dans Visual Studio et sur l’utilisation de la galerie NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 01/15/2019
ms.topic: conceptual
ms.openlocfilehash: dbdd171321c2560adc06feccbd60fc4e84dcf0a3
ms.sourcegitcommit: a801052aa728a3a137225ca3ef3ff89f2d1c6b76
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54403210"
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
- Azure DevOps fournit [une étape de la génération pour restaurer des packages NuGet](/vsts/build-release/tasks/package/nuget). Vous pouvez également [héberger des flux de packages NuGet privés sur Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

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

**J’essaie d’effectuer un cast de la variable $DTE en type DTE2, mais j’obtiens une erreur : Impossible de convertir la valeur « EnvDTE.DTEClass » de type « EnvDTE.DTEClass » en type « EnvDTE80.DTE2 ». Quel est le problème ?**

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

De plus, le chargement d’un package sur [int.nugettest.org](https://int.nugettest.org) constitue un excellent moyen de le tester et de le valider sans le mettre à disposition dans la galerie publique.

**Est-il possible de réserver des noms pour les packages destinés à être publiés ?**

Oui. Vous pouvez réserver des ID pour les packages sur [nuget.org](https://www.nuget.org/) en demandant un préfixe d’ID de package pour votre compte. Pour demander un préfixe d’ID de package, suivez les instructions de la [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Comment revendiquer la propriété de packages ?**

Consultez [Gestion des propriétaires de packages sur nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Comment négocier avec un propriétaire de package qui viole ma licence de logiciel ?**

Nous invitons la communauté NuGet à collaborer afin de résoudre les litiges pouvant survenir entre les propriétaires de packages et les propriétaires d’autres logiciels. Nous avons conçu un [processus de résolution des litiges](../policies/dispute-resolution.md) à suivre avant de demander aux administrateurs de nuget.org d’intervenir.

**Est-il recommandé de charger mes packages de test sur nuget.org ?**

À des fins de test, vous pouvez utiliser [int.nugettest.org](https://int.nugettest.org) ou d’autres serveurs NuGet publics, comme [myget.org](https://myget.org) ou [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Notez que les packages chargés sur int.nugettest.org ne sont pas nécessairement conservés.

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
- Si votre machine se trouve derrière un pare-feu ou un proxy
- Votre machine se trouve-t-elle sur le centre de données d’un fournisseur cloud (Azure, AWS, etc.) ? Si c’est le cas, indiquez le nom du fournisseur et la région.

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

- V3 : `https://api.nuget.org/v3/index.json`
- V2 : `https://www.nuget.org/api/v2/` (Notez que l’API V2 est dépréciée et ne fonctionne pas avec NuGet 4+.)

## <a name="nugetorg-account-management"></a>Gestion de compte nuget.org

### <a name="how-to-create-a-new-nugetorg-account"></a>Comment créer un compte nuget.org ?

Pour créer un compte nuget.org, vous devez disposer d’un compte Microsoft personnel (MSA) ou d’un compte Azure Active Directory (AAD). Si vous n’en avez pas, vous pouvez en [créer](https://signup.live.com) un. Effectuez les étapes suivantes si vous disposez d’un compte MSA ou AAD.
1. Accédez à la [page de connexion à nuget.org](https://www.nuget.org/users/account/LogOn).
1. Cliquez sur le bouton **Se connecter avec Microsoft**.
1. Entrez les détails de votre compte MSA/AAD.
1. Acceptez les autorisations à donner à l’application *NuGet.org*.
1. Vous allez être redirigé vers nuget.org et invité à inscrire un nom d’utilisateur.
1. Spécifiez le nom d’utilisateur dans la zone d’entrée. Notez que le nom d’utilisateur **respecte** la casse et ne peut pas être changé/renommé ultérieurement.
1. Cliquez sur le bouton **S’inscrire**.

Vous disposez maintenant d’un compte nuget.org. Vous pouvez effectuer la gestion de compte sur la page des [paramètres du compte](https://www.nuget.org/account).

### <a name="how-to-recover-nugetorg-password-login"></a>Comment récupérer le mot de passe de connexion nuget.org ?

Notez que le [mot de passe de connexion nuget.org n’est plus disponible](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) et que la seule façon de se connecter à nuget.org est d’utiliser un compte Microsoft personnel (MSA) ou un compte Azure Active Directory (AAD). Toutefois, si vous ne parvenez pas à accéder à vos comptes MSA/AAD associés, vous devrez peut-être utiliser un mot de passe de connexion pour récupérer votre compte nuget.org. Dans ce cas, suivez les étapes ci-dessous.
- **Exigence :** Vous devez avoir accès à l’adresse e-mail associée au compte pour lequel vous devez récupérer le mot de passe.
- Accédez à la [page Mot de passe oublié](https://www.nuget.org/account/ForgotPassword).
- Entrez l’adresse **e-mail** associée au compte nuget.org que vous voulez récupérer.
- Cliquez sur le bouton **Send** (Envoyer).
- Vous obtenez un e-mail pour le compte d’adresse e-mail spécifié avec un lien pour réinitialiser votre mot de passe. Cliquez sur ce lien et définissez le nouveau mot de passe. Si vous ne trouvez pas l’e-mail, vérifiez votre dossier « Courrier indésirable ».
- Une fois cette opération effectuée, vous pouvez vous connecter à NuGet avec le nom d’utilisateur/mot de passe.
- Pour vous connecter avec un nom d’utilisateur/mot de passe, utilisez le lien **Se connecter à l’aide du compte Nuget.org** sur la [page de connexion à nuget.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Quel compte Microsoft est lié à mon compte nuget.org ?

Si vous avez oublié quel compte Microsoft est associé à votre compte nuget.org, effectuez les étapes ci-dessous pour obtenir de l’aide.
1. Accédez à la [page de connexion à nuget.org](https://www.nuget.org/users/account/LogOn), puis cliquez sur le lien **Vous avez besoin d’aide pour vous connecter ?**.
1. Une boîte de dialogue contextuelle permettant d’obtenir de l’aide s’affiche alors. Effectuez les étapes décrites dans cette boîte de dialogue pour comprendre le ou les comptes Microsoft associés à votre compte nuget.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Comment changer le compte Microsoft que j’utilise pour la connexion à nuget.org ?
Si vous voulez changer le compte Microsoft de l’utilisateur nuget.org, effectuez les étapes ci-dessous. Supposons que votre compte Microsoft avec l’adresse e-mail `account1@outlook.com` est associé à votre compte nuget.org avec le nom d’utilisateur `MyNuGetAccount`. Vous voulez rempalcer les informations de connexion par un autre compte Microsoft avec l’adresse e-mail `account2@outlook.com`
1. Connectez-vous à l’aide du **compte Microsoft actuellement associé**, c’est-à-dire `account1@outlook.com`, sur la [page de connexion](https://www.nuget.org/users/account/LogOn) après avoir cliqué sur **Se connecter avec Microsoft**.
1. Une fois connecté, accédez à la page de vos [paramètres du compte](https://www.nuget.org/account).
1. Développez la section relative au **compte de connexion**. Cliquez sur le bouton **Changer de compte**.
1. Vous allez maintenant être redirigé vers la page de connexion de Microsoft. Connectez-vous avec le compte dont vous voulez changer l’association, à savoir `account2@outlook.com`. **Remarque** : Vous devrez peut-être cliquer sur **Se déconnecter et se connecter avec un autre compte** pendant le flux de connexion pour pouvoir vous connecter avec un autre compte Microsoft.
1. Si vous voyez une erreur comme celle affichée ci-dessous, consultez [Le compte Microsoft est lié à un autre compte nuget.org](#microsoft-account-is-linked-with-another-nugetorg-account) pour plus d’informations.
    >_Échec de la mise à jour du compte Microsoft avec « account2 <account2@outlook.com> ». Cela peut se produire s’il est déjà lié à un autre compte NuGet. Contactez le support technique pour plus d’informations._

1. Une fois que vous êtes connecté avec votre deuxième compte, vous êtes redirigé vers la page des paramètres de votre compte nuget.org et vous devez maintenant voir le nouveau compte Microsoft associé en tant que compte de connexion. Dorénavant, vous devez utiliser ce compte quand vous vous connectez à nuget.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Le compte Microsoft est lié à un autre compte nuget.org.

Vous avez essayé de changer votre connexion Microsoft et l’erreur ci-dessous s’est affichée :
> _Échec de la mise à jour du compte Microsoft avec « account2 <account2@outlook.com> ». Cela peut se produire s’il est déjà lié à un autre compte NuGet. Contactez le support technique pour plus d’informations._

Supposons que vous tentiez de remplacer la connexion au compte Microsoft `account1@outlook.com` pour l’utilisateur nuget.org avec le nom d’utilisateur `MyNuGetAccount1` par un autre compte Microsoft avec l’adresse e-mail `account2@outlook.com`. L’erreur ci-dessus s’affiche alors.

**Que signifie l’erreur ci-dessus ?**

Elle signifie qu’un autre compte nuget.org est associé au compte Microsoft que vous essayez d’utiliser pour le remplacer ; à savoir, dans l’exemple ci-dessus, le compte Microsoft avec l’adresse e-mail `<account2@outlook.com>` est associé à un autre compte nuget.org avec, par exemple, le nom d’utilisateur `MyNuGetAccount2`.

Vous ne pouvez pas remplacer la connexion associée par un compte Microsoft qui est lié à un autre compte nuget.org.

**J’ai oublié que j’avais un autre compte nuget.org. Comment savoir de quel compte nuget.org il s’agit ?**

Connectez-vous avec le deuxième compte Microsoft sur la [page de connexion](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "page de connexion"). Vous serez connecté au compte nuget.org qui est actuellement associé au deuxième compte Microsoft. Vous pouvez alors afficher les packages chargés et effectuer la gestion de compte sur ce compte.

**Ce deuxième compte nuget.org ne m’intéresse pas. Je souhaite changer ma connexion pour utiliser le premier compte nuget.org avec le deuxième compte Microsoft. Que dois-je faire ?**

Vous voulez ne pas vous soucier du deuxième compte nuget.org et quand même réutiliser le compte Microsoft associé avec l’adresse e-mail `account2@outlook.com`. 

Vous pouvez libérer l’association entre le compte Microsoft et le compte nuget.org en supprimant le compte nuget.org.
1. Effectuez les étapes permettant de [supprimer l’utilisateur](#how-to-delete-my-nugetorg-account) pour le deuxième compte nuget.org `MyNuGetAccount2`. 
1. Une fois ce compte supprimé, vous pouvez retenter les étapes permettant de [changer la connexion au compte Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**En fait, je m’intéresse à ce deuxième compte également. Je ne veux pas perdre ce compte, mais changer les informations de connexion de compte associé du premier compte.**

Vous devrez créer/utiliser un troisième compte Microsoft, par exemple avec l’adresse e-mail `account3@outlook.com`. 
1. Vous devez d’abord vous connecter avec votre deuxième compte Microsoft, `account2@outlook.com` sur nuget.org. Suivez les étapes ci-dessus pour changer les connexions associées et associer le troisième compte Microsoft à ce compte nuget.org.
1. Une fois cela effectué, votre deuxième compte Microsoft avec l’adresse e-mail `account2@outlook.com` peut être associé à votre premier compte nuget.org, `MyNuGetAccount1`. Effectuez les mêmes étapes ci-dessus pour changer les informations de connexion Microsoft pour le deuxième compte Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>La connexion avec un compte Microsoft me montre que mon e-mail est lié à un autre compte Microsoft
Si vous avez essayé de vous connecter avec votre compte Microsoft, par exemple avec l’adresse e-mail `account1@outlook.com` et vous voyez une erreur comme celle ci-dessous :
> _Le compte avec l’e-mail « account1@outlook.com » est lié à un autre compte Microsoft._
>
> _Si vous voulez mettre à jour le compte Microsoft lié, vous pouvez le faire à partir de la page des paramètres du compte._

**Que signifie l’erreur ci-dessus ?**

Quand un compte est créé sur nuget.org, une adresse e-mail de communication lui est associée. Elle est généralement identique à l’adresse e-mail utilisée pour le compte Microsoft associé. Toutefois, vous pouvez choisir de spécifier une autre adresse e-mail pour la communication. Par conséquent, techniquement, vous pouvez avoir un autre compte Microsoft, par exemple avec `account2@outlook.com`, lié à un compte nuget.org ayant l’adresse e-mail de communication `account1@outlook.com`.

L’erreur ci-dessus signifie donc qu’il existe déjà un compte nuget.org avec l’adresse e-mail de communication `account1@outlook.com` mais qu’il est associé à un autre compte Microsoft avec une adresse e-mail **qui n’est pas** `account1@outlook.com`.

**Comment savoir quel compte Microsoft est lié à ce compte nuget.org ?**

Vous devez utiliser le flux d’[aide relative à la connexion](#which-microsoft-account-is-linked-to-my-nugetorg-account) pour déterminer quel compte Microsoft est lié au compte nuget.org avec l’adresse e-mail `account1@outlook.com`.

**Je souhaite remplacer ce compte par mon compte Microsoft**

Effectuez les étapes mentionnées dans la section [Impossible d’utiliser la connexion Microsoft. Comment récupérer mon compte nuget.org ?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) pour associer votre compte Microsoft au compte nuget.org existant.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Impossible d’utiliser la connexion Microsoft. Comment récupérer mon compte nuget.org ?

Si vous avez essayé d’utiliser l’[aide relative à la connexion](#which-microsoft-account-is-linked-to-my-nugetorg-account) et que vous n’avez pas accès au compte Microsoft associé à votre compte nuget.org, effectuez les étapes ci-dessous pour lier un nouveau compte Microsoft à votre compte nuget.org.
1. **Exigence** : Vous devez disposer d’un accès à un compte Microsoft (qui n’est associé à aucun compte nuget.org existant). Si vous n’en avez pas, vous pouvez en [créer](https://signup.live.com) un.
2. Suivez les [étapes permettant de récupérer votre mot de passe de connexion](#how-to-recover-nugetorg-password-login). Si vous avez le mot de passe de connexion, ignorez cette étape.
3. [Connectez-vous à nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) à l’aide du nom d’utilisateur/mot de passe de connexion.
4. Une fois que vous êtes connecté, une boîte de dialogue contextuelle semblable à celle ci-dessous s’affiche. Il s’agit de la boîte de dialogue de suspension du mot de passe.
5. **REMARQUE** : Ignorez l’instruction de connexion avec le compte Microsoft spécifié. Vous pouvez maintenant lier votre compte nuget.org à n’importe quelle autre connexion Microsoft.
6. Cliquez sur le bouton **Se connecter avec Microsoft** et connectez-vous avec le compte Microsoft auquel vous avez accès, comme indiqué à l’étape 1.
7. Votre compte est maintenant lié au nouveau compte Microsoft, que vous pouvez dorénavant utiliser pour vous connecter à nuget.org.

    ![Boîte de dialogue de liaison de comptes MSA](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Comment transformer mon compte nuget.org en compte d’organisation ?

Si vous voulez transformer votre compte en compte d’organisation, et que ce compte est déjà associé à une connexion au compte Microsoft, effectuez les étapes indiquées dans la documentation concernant les [comptes d’organisation sur nuget.org](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org).

Toutefois, si votre compte nuget.org n’est pas associé/lié à un compte Microsoft, vous pouvez suivre les étapes ci-dessous pour transformer ce compte en compte d’organisation.
1. **Exigence** : Vous devez disposer d’un compte individuel initialement créé sur nuget.org à utiliser en tant qu’administrateur sur le compte de l’organisation. Si vous n’en avez pas, [créez un compte nuget.org](#how-to-create-a-nugetorg-account).
2. Suivez les [étapes permettant de récupérer votre mot de passe de connexion](#how-to-recover-nugetorg-password-login) pour votre compte nuget.org si vous n’avez pas de mot de passe de connexion. Dans le cas contraire, ignorez cette étape.
3. [Connectez-vous à nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) à l’aide du nom d’utilisateur/mot de passe de connexion.
4. Une fois que vous êtes connecté, une boîte de dialogue contextuelle semblable à celle ci-dessous s’affiche. Il s’agit de la boîte de dialogue de suspension du mot de passe. 
    > [!Important]
    > Ignorez cette boîte de dialogue. Ne cliquez **pas** sur le bouton **Se connecter avec Microsoft**.

5. Accédez à [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). Cela vous permet de convertir le compte nuget.org en compte d’organisation sans créer de lien à un compte Microsoft.
6. Spécifiez le nom d’utilisateur administrateur pour votre compte nuget.org personnel/le compte que vous avez créé à l’étape 1.
7. Suivez les instructions permettant d’effectuer la transformation de ce compte en compte d’organisation.

    ![Boîte de dialogue de liaison de comptes MSA](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Vous rencontrez des problèmes de connexion à nuget.org pour les comptes AAD avec un propriétaire non managé ?

Si vous voyez une erreur comme celle affichée ci-dessous pendant votre flux de connexion avec votre domaine de compte de messagerie (@yourdomain.com), consultez les étapes suivantes pour récupérer votre compte nuget.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**À quoi correspond cet état non managé pendant la connexion ? Et pourquoi cela se produit-il à ce moment-là ?** 

Votre compte semble avoir été précédemment inscrit en tant que compte Microsoft personnel et cela fonctionnait correctement. Toutefois, il semble que votre compte a maintenant été inscrit en tant que locataire « non managé » dans Azure Active Directory (service d’identité que nous utilisons pour authentifier les comptes Microsoft). 

Cela a pu se produire si vous ou une personne de votre organisation (avec l’adresse e-mail @yourdomain.com) vous êtes inscrit auprès de l’un des services intégrés AAD ou si vous avez effectué une [inscription en libre-service pour Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), qui crée un tel locataire « non managé » pour le domaine de compte Microsoft utilisé (@yourdomain.com dans votre cas). 

**Que puis-je faire pour récupérer mon compte ?**

Pour le moment, nous (nuget.org) ne disposons d’aucun moyen pour authentifier les comptes avec de tels comptes de locataires « non managés » dans Azure Active directory. Nous recherchons un meilleur moyen d’authentifier ces comptes.

Si vous voulez vous connecter à nuget.org avec votre compte Microsoft (@yourdomain.com), vous (ou un administrateur de votre entreprise) devez revendiquer la propriété des comptes AAD en effectuant une validation DNS afin d’authentifier les utilisateurs avec l’adresse e-mail « @yourdomain.com ». Suivez les étapes permettant la [prise de contrôle des administrateurs de domaines](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) documentées par Azure Active Directory. Une fois cela effectué, votre connexion normale doit commencer à fonctionner.

**Je ne veux pas effectuer toutes ces opérations. Quelle est l’autre façon de récupérer mon compte ?**

Vous pouvez [créer](https://www.microsoft.com/en-us/account) un compte Microsoft (avec une adresse e-mail **non** associée à @yourdomain.com). Suivez les étapes indiquées dans la section relative à la [récupération de votre compte nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account).

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Comment changer mon nom d’utilisateur de compte nuget.org ?

Vous ne le pouvez pas. En vertu de notre politique, nous n’autorisons pas, pour le moment, le changement des noms d’utilisateurs. La seule façon de changer votre nom d’utilisateur consiste à créer un compte avec le nom d’utilisateur souhaité. Nous vous recommandons de supprimer votre compte existant avant d’en créer un nouveau. Sinon, vous ne pourrez pas réutiliser votre compte Microsoft inscrit.
> [!Important]
> La suppression de l’utilisateur **réserve** toutefois la valeur `username`. Vous ne pourrez pas réutiliser le même nom d’utilisateur et **cela inclut le changement de casse**. Par exemple, si vous avez créé un utilisateur avec le nom d’utilisateur `mycoolname` et que vous voulez le remplacer par `MyCoolName` (changement de casse), ce ne sera pas possible après la suppression de l’utilisateur.

Suivez les étapes indiquées dans la section relative à la [suppression de votre compte nuget.org](#how-to-delete-my-nugetorg-account) et celles permettant d’[inscrire un nouveau compte](#how-to-create-a-new-nugetorg-account) avec le nom d’utilisateur correct.

### <a name="how-to-delete-my-nugetorg-account"></a>Comment supprimer mon compte nuget.org ?

Pour supprimer votre compte, notez que nous vous recommandons de transférer la propriété de tous les packages dont vous êtes l’unique propriétaire. Pour savoir comment procéder, lisez la section relative à la [gestion des propriétaires de packages](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg). Cela nous permettra également d’accélérer votre demande.

> [!Important]
> La suppression de l’utilisateur a les conséquences suivantes :
>  1. Révocation des clés API associées. 
>  2. Suppression du compte en tant que propriétaire des packages enfants.
>  3. Dissociation de toutes les réservations de préfixe d’ID précédemment existantes avec ce compte.
>  4. Suppression du compte en tant que membre d’une organisation.
>  5. Votre nom d’utilisateur sera réservé et personne ne pourra le réutiliser sans notre autorisation.

Effectuez les étapes suivantes pour procéder à la suppression du compte.
1. [Connectez-vous à nuget.org](https://www.nuget.org/users/account/LogOn) avec le compte que vous voulez supprimer.
2. Cliquez sur l’URL [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete), puis effectuez les étapes permettant de soumettre la demande de suppression du compte.

Notre service clientèle traitera cette demande et effectuera la suppression du compte.