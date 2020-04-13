---
title: Questions fréquentes (FAQ) sur NuGet.org
description: Questions et réponses courantes concernant l’utilisation de la galerie NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 915f6e4cfc0b21d2b10006c62e8230720d07ce74
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428904"
---
# <a name="nugetorg-frequently-asked-questions"></a>Questions fréquentes (FAQ) sur NuGet.org

## <a name="license-terms"></a>Termes du contrat de licence

**Quels sont les termes du contrat de licence si un package ne fournit pas des informations de licence spécifiques ?**

Chaque package est régi par les conditions qu’il inclut. Vous devez examiner les conditions applicables avant d’accéder à des packages, d’en télécharger ou d’en acquérir. Sur NuGet.org, utilisez le lien **License Info** (Informations de licence) sur la page des packages.

Si un package ne spécifie pas les termes du contrat de licence, contactez le propriétaire du package directement à l’aide du lien **Contact owners** (Contacter les propriétaires) sur la page des packages NuGet.org. Microsoft ne vous concède aucune licence de propriété intellectuelle de fournisseurs de packages tiers et n’est pas responsable des informations fournies par des tiers.

## <a name="managing-packages-on-nugetorg"></a>Gestion des packages sur NuGet.org

**Puis-je modifier les métadonnées d’un package après l’avoir chargé ?**

NuGet recommande de signer tous les packages. Un principe de conception de la signature du package est que le contenu du package signé doit être immuable, ce qui comprend le fichier nuspec. Modifier les métadonnées du package entraîne des modifications du fichier nuspec, invalidant les signatures existantes. Nous vous recommandons de modifier les flux de travail existants de manière à ce qu’il ne soit pas nécessaire de modifier les métadonnées du package une fois ce dernier créé.

Notez que les dépendances répertoriées pour votre package sont générées automatiquement à partir du package lui-même et qu’elles ne peuvent pas être modifiées.

De plus, le chargement d’un package sur [int.nugettest.org](https://int.nugettest.org) constitue un excellent moyen de le tester et de le valider sans le mettre à disposition dans la galerie publique. Point de terminaison d’API : https://apiint.nugettest.org/v3/index.json

**Puis-je supprimer un package déjà publié sur NuGet.org ?**

En général, nous ne sommes pas en faveur de la suppression d’un paquet publié à NuGet.org. En savoir plus sur notre [politique sur la suppression des paquets](policies/deleting-packages.md).

**Est-il possible de réserver les noms des packages qui doivent être publiés à l’avenir ?**

Oui. Vous pouvez réserver des ID pour les packages sur [NuGet.org](https://www.nuget.org/) en demandant un préfixe d’ID de package pour votre compte. Pour demander un préfixe d’ID de package, suivez les instructions de la [documentation](id-prefix-reservation.md).

**Comment revendiquer la propriété de packages ?**

Voir [Gérer les propriétaires de forfaits sur NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Comment négocier avec un propriétaire de package qui viole ma licence de logiciel ?**

Nous invitons la communauté NuGet à collaborer afin de résoudre les litiges pouvant survenir entre les propriétaires de packages et les propriétaires d’autres logiciels. Nous avons conçu un [processus de résolution des litiges](policies/dispute-resolution.md) à suivre avant de demander aux administrateurs de NuGet.org d’intervenir.

**Est-il recommandé de charger mes packages de test sur NuGet.org ?**

À des fins de test, vous pouvez utiliser [int.nugettest.org](https://int.nugettest.org) ou d’autres serveurs NuGet publics, comme [myget.org](https://myget.org) ou [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Notez que les packages chargés sur int.nugettest.org ne sont pas nécessairement conservés.

**Quelle est la taille maximale des packages que je peux charger sur NuGet.org ?**

La taille maximale de package autorisée par NuGet.org est de 250 Mo, mais nous vous recommandons de limiter la taille des packages à 1 Mo maximum si possible et de les lier à l’aide de dépendances. En règle générale, les packages contiennent un seul assembly pour éviter les collisions.

NuGet utilisant HTTP pour télécharger les packages, l’installation d’un package risque d’autant plus d’échouer que celui-ci est volumineux.

Vous pouvez partager des dépendances entre plusieurs packages, pour réduire la taille totale du téléchargement pour les consommateurs de vos packages NuGet.

Les dépendances sont principalement statiques et ne changent jamais. Quand vous résolvez un bogue dans le code, il peut s’avérer superflu de mettre à jour les dépendances. Si vous regroupez des dépendances, vous finissez systématiquement par relivrer des packages plus volumineux. Si vous fractionnez les packages NuGet en dépendances connexes, les mises à niveau sont beaucoup plus précises pour les consommateurs de votre package.

## <a name="nugetorg-not-accessible"></a>NuGet.org inaccessible

**Pourquoi ne puis-je pas télécharger de packages à partir de NuGet.org ou en y charger ?**

Tout d’abord, veillez à utiliser les dernières versions de NuGet. Si cette version continue à échouer, [contactez le support technique](https://www.nuget.org/policies/Contact) et fournissez des informations supplémentaires pour la résolution du problème de connexion, notamment les suivantes :

- Version de NuGet que vous utilisez
- Sources de package que vous utilisez
- Journal de restauration avec commentaires détaillés
- MTR ou traces Fiddler (voir ci-dessous)
- Votre zone géographique
- Si votre machine se trouve derrière un pare-feu ou un proxy
- Votre machine se trouve-t-elle sur le centre de données d’un fournisseur cloud (Azure, AWS, etc.) ? Si c’est le cas, indiquez le nom du fournisseur et la région.

*Pour capturer MTR :*

- Télécharger [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download).
- Entrez `api.nuget.org` comme nom d’hôte et cliquez sur **Start** (Démarrer).
- Attendez que la colonne **Sent** (Envoyé) soit supérieure ou égale à 100.

    ![Capture de MTR](media/mtr.png)

- Copiez le texte dans le Presse-papiers.

*Pour capturer Fiddler :*

- Installez la version la plus récente de [Fiddler](https://www.telerik.com/download/fiddler).
- Démarrez Fiddler et désactivez la capture du trafic à l’aide du menu **File > Capture Traffic** (Fichier > Capturer le trafic).
- Supprimez toutes les sessions (sélectionnez tous les éléments de la liste, puis appuyez sur la touche **Supprimer**).
- Configurez Fiddler pour capturer le trafic HTTPS en cochant **Decrypt HTTPS traffic** (Déchiffrer le trafic HTTPS) sous l’onglet **HTTPS** du menu **Tools > Fiddler Options...** (Outils > Options Fiddler...).
- Fermez Visual Studio.
- Activez **l’option Capture Traffic (Capturer le trafic) dans le menu File (Fichier)**.
- Démarrez Visual Studio ou nuget.exe et effectuez les actions qui ne fonctionnent pas. Le trafic généré par ces actions doit s’afficher dans Fiddler.
- Une fois les actions exécutées, utilisez **File > Save > All Sessions** (Fichier > Enregistrer > Toutes les sessions) pour stocker les sessions capturées.

Remarque : Il peut être nécessaire de définir la variable d’environnement `HTTP_PROXY` sur `http://127.0.0.1:8888` pour router le trafic NuGet via Fiddler.

Si cette opération échoue, essayez les [conseils mentionnés dans ce billet de StackOverflow](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>Gestion de compte NuGet.org

### <a name="how-to-recover-nugetorg-password-login"></a>Comment récupérer le mot de passe de connexion NuGet.org ?

Veuillez noter que la [connexion NuGet.org Password a été interrompue](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) et que la seule façon de se connecter à NuGet.org est avec un compte Personnel Microsoft (MSA) ou Azure Active Directory (AAD). Toutefois, si vous ne parvenez pas à accéder à vos comptes MSA/AAD associés, vous devrez peut-être utiliser un mot de passe de connexion pour récupérer votre compte NuGet.org. Dans ce cas, suivez les étapes ci-dessous.
- **Exigence:** Vous devrez avoir accès à l’e-mail qui est associé au compte dont vous avez besoin pour récupérer le mot de passe.
- Accédez à la [page Mot de passe oublié](https://www.nuget.org/account/ForgotPassword).
- Entrez l’adresse **e-mail** associée au compte NuGet.org que vous souhaitez récupérer.
- Cliquez sur le bouton **Send** (Envoyer).
- Vous obtenez un e-mail pour le compte d’adresse e-mail spécifié avec un lien pour réinitialiser votre mot de passe. Cliquez sur ce lien et définissez le nouveau mot de passe. Si vous ne trouvez pas l’e-mail, vérifiez votre dossier « Courrier indésirable ».
- Une fois cette opération effectuée, vous pouvez vous connecter à NuGet avec le nom d’utilisateur/mot de passe.
- Pour vous connecter avec le nom d’utilisateur/mot de passe, utilisez le **Signe à l’aide d’Nuget.org** lien de compte sur la [page de connexion NuGet.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Quel compte Microsoft est lié à mon compte NuGet.org ?

Si vous avez oublié quel compte Microsoft est associé à votre compte NuGet.org, effectuez les étapes ci-dessous pour obtenir de l’aide.
1. Allez [à NuGet.org page de connexion](https://www.nuget.org/users/account/LogOn) et cliquez sur **l’aide besoin de connexion?** lien.
1. Une boîte de dialogue contextuelle permettant d’obtenir de l’aide s’affiche alors. Effectuez les étapes décrites dans cette boîte de dialogue pour comprendre le ou les comptes Microsoft associés à votre compte NuGet.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Comment changer le compte Microsoft que j’utilise pour la connexion à NuGet.org ?
Si vous voulez changer le compte Microsoft de l’utilisateur NuGet.org, effectuez les étapes ci-dessous. Supposons que votre compte Microsoft avec l’adresse e-mail `account1@outlook.com` est associé à votre compte NuGet.org avec le nom d’utilisateur `MyNuGetAccount`. Vous voulez rempalcer les informations de connexion par un autre compte Microsoft avec l’adresse e-mail `account2@outlook.com`
1. Connectez-vous à l’aide du **compte Microsoft actuellement associé**, c’est-à-dire `account1@outlook.com`, sur la [page de connexion](https://www.nuget.org/users/account/LogOn) après avoir cliqué sur **Se connecter avec Microsoft**.
1. Une fois connecté, accédez à la page de vos [paramètres du compte](https://www.nuget.org/account).
1. Développez la section relative au **compte de connexion**. Cliquez sur le bouton **Changer de compte**.
1. Vous allez maintenant être redirigé vers la page de connexion de Microsoft. Veuillez vous connecter au compte que vous souhaitez changer `account2@outlook.com`l’association à c’est-à-dire . **Remarque**: vous devrez peut-être cliquer sur **Vous connecter et vous connecter à différents comptes** pendant le flux de connexion pour pouvoir vous connecter avec un autre compte Microsoft.
1. Si vous voyez une erreur comme ci-dessous, voir [compte Microsoft est lié à un autre compte NuGet.org](#microsoft-account-is-linked-with-another-nugetorg-account) pour plus de détails.
    >_Échec de mettre à jour <account2@outlook.com>le compte Microsoft avec 'account2'. Cela pourrait se produire si elle est déjà liée à un autre compte NuGet. Contactez le support pour plus d’informations._

1. Une fois que vous êtes connecté avec votre deuxième compte, vous êtes redirigé vers la page des paramètres de votre compte NuGet.org et vous devez maintenant voir le nouveau compte Microsoft associé en tant que compte de connexion. Dorénavant, vous devez utiliser ce compte quand vous vous connectez à NuGet.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Le compte Microsoft est lié à un autre compte NuGet.org.

Vous avez essayé de changer votre connexion Microsoft et l’erreur ci-dessous s’est affichée :
> _Échec de mettre à jour <account2@outlook.com>le compte Microsoft avec 'account2'. Cela pourrait se produire si elle est déjà liée à un autre compte NuGet. Contactez le support pour plus d’informations._

Supposons que vous tentiez de remplacer la connexion au compte Microsoft `account1@outlook.com` pour l’utilisateur NuGet.org avec le nom d’utilisateur `MyNuGetAccount1` par un autre compte Microsoft avec l’adresse e-mail `account2@outlook.com`. L’erreur ci-dessus s’affiche alors.

**Que signifie l’erreur ci-dessus ?**

Elle signifie qu’un autre compte NuGet.org est associé au compte Microsoft que vous essayez d’utiliser pour le remplacer ; à savoir, dans l’exemple ci-dessus, le compte Microsoft avec l’adresse e-mail `<account2@outlook.com>` est associé à un autre compte NuGet.org avec, par exemple, le nom d’utilisateur `MyNuGetAccount2`.

Vous ne pouvez pas remplacer la connexion associée par un compte Microsoft qui est lié à un autre compte NuGet.org.

**J’ai oublié que j’avais un autre compte NuGet.org, comment puis-je savoir quel NuGet.org compte qu’il est?**

Connectez-vous avec le deuxième compte Microsoft sur la [page de connexion](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "page de connexion"). Vous serez connecté au compte NuGet.org qui est actuellement associé au deuxième compte Microsoft. Vous pouvez alors afficher les packages chargés et effectuer la gestion de compte sur ce compte.

**Je ne me soucie pas de ce deuxième compte NuGet.org, je veux changer ma connexion pour le premier compte NuGet.org avec le deuxième compte Microsoft. Qu’est-ce que je fais ?**

Vous voulez ne pas vous soucier du deuxième compte NuGet.org et quand même réutiliser le compte Microsoft associé avec l’adresse e-mail `account2@outlook.com`. 

Vous pouvez libérer l’association entre le compte Microsoft et le compte NuGet.org en supprimant le compte NuGet.org.
1. Suivez les étapes pour [supprimer l’utilisateur](#how-to-delete-my-nugetorg-account) `MyNuGetAccount2`pour le deuxième compte NuGet.org . 
1. Une fois ce compte supprimé, vous pouvez retenter les étapes permettant de [changer la connexion au compte Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Attends, je tiens à ce deuxième compte aussi. Je ne veux pas perdre ce compte mais changer mes connexions de compte associés pour le premier compte.**

Vous devrez créer/utiliser un troisième compte Microsoft, par exemple avec l’adresse e-mail `account3@outlook.com`. 
1. Vous devez d’abord vous connecter `account2@outlook.com` à votre deuxième compte Microsoft, sur NuGet.org. Suivez les étapes ci-dessus pour modifier les connexions associées et associez le troisième compte Microsoft à ce compte NuGet.org.
1. Une fois cela effectué, votre deuxième compte Microsoft avec l’adresse e-mail `account2@outlook.com` peut être associé à votre premier compte NuGet.org, `MyNuGetAccount1`. Effectuez les mêmes étapes ci-dessus pour changer les informations de connexion Microsoft pour le deuxième compte Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>La connexion avec un compte Microsoft me montre que mon e-mail est lié à un autre compte Microsoft

Si vous avez essayé de vous connecter avec votre compte Microsoft, par exemple avec l’adresse e-mail `account1@outlook.com` et vous voyez une erreur comme celle ci-dessous :
> _Le compte avec l’e-mail « account1@outlook.com » est lié à un autre compte Microsoft._
>
> _Si vous voulez mettre à jour le compte Microsoft lié, vous pouvez le faire à partir de la page des paramètres du compte._

**Que signifie l’erreur ci-dessus ?**

Quand un compte est créé sur NuGet.org, une adresse e-mail de communication lui est associée. Elle est généralement identique à l’adresse e-mail utilisée pour le compte Microsoft associé. Toutefois, vous pouvez choisir de spécifier une autre adresse e-mail pour la communication. Par conséquent, techniquement, vous pouvez avoir un autre compte Microsoft, par exemple avec `account2@outlook.com`, lié à un compte NuGet.org ayant l’adresse e-mail de communication `account1@outlook.com`.

L’erreur ci-dessus signifie donc qu’il existe déjà un compte NuGet.org avec l’adresse e-mail de communication `account1@outlook.com` mais qu’il est associé à un autre compte Microsoft avec une adresse e-mail **qui n’est pas** `account1@outlook.com`.

**Comment puis-je trouver quel compte Microsoft est lié à ce compte NuGet.org ?**

Vous devez utiliser le [flux d’assistance de signe](#which-microsoft-account-is-linked-to-my-nugetorg-account) pour déterminer quel compte Microsoft `account1@outlook.com`est lié au compte NuGet.org avec l’adresse e-mail .

**Je souhaite remplacer ce compte par mon compte Microsoft**

Suivez les étapes de [l’utilisation de la connexion microsoft, comment récupérer ma](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) section de compte NuGet.org pour associer votre compte Microsoft au compte NuGet.org existant.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Impossible d’utiliser la connexion Microsoft. Comment récupérer mon compte NuGet.org ?

Si vous avez essayé d’utiliser le [signe dans l’assistance](#which-microsoft-account-is-linked-to-my-nugetorg-account) et que vous n’avez pas accès au compte Microsoft associé à votre compte NuGet.org, veuillez suivre les étapes ci-dessous pour lier un nouveau compte Microsoft à votre compte NuGet.org.
1. **Exigence**: Vous aurez besoin d’accéder à un compte Microsoft qui n’est associé à aucun compte NuGet.org existant. Si vous n’en avez pas, vous pouvez en [créer](https://signup.live.com) un.
2. Si vous avez oublié votre nom d’utilisateur et le mot de passe associés à votre compte NuGet.org, suivez ces [étapes pour récupérer votre mot de passe de connexion](#how-to-recover-nugetorg-password-login).
3. [Connectez-vous à NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) à l’aide du nom d’utilisateur/mot de passe.
4. Une fois que vous êtes connecté, une boîte de dialogue contextuelle semblable à celle ci-dessous s’affiche. Il s’agit de la boîte de dialogue de suspension du mot de passe.
5. **REMARQUE**: Veuillez ignorer l’instruction de vous connecter au compte Microsoft spécifié. Vous pouvez maintenant lier votre compte NuGet.org à n’importe quelle autre connexion Microsoft.
6. Cliquez sur le bouton **Se connecter avec Microsoft** et connectez-vous avec le compte Microsoft auquel vous avez accès, comme indiqué à l’étape 1.
7. Votre compte est maintenant lié au nouveau compte Microsoft, que vous pouvez dorénavant utiliser pour vous connecter à NuGet.org.

    ![Boîte de dialogue de liaison de comptes MSA](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Comment transformer mon compte NuGet.org en compte d’organisation ?

Si vous voulez transformer votre compte en compte d’organisation, et que ce compte est déjà associé à une connexion au compte Microsoft, effectuez les étapes indiquées dans la documentation concernant les [comptes d’organisation sur nuget.org](organizations-on-nuget-org.md).

Toutefois, si votre compte NuGet.org n’est pas associé/lié à un compte Microsoft, vous pouvez suivre les étapes ci-dessous pour transformer ce compte en compte d’organisation.
1. **Exigence**: Vous devez avoir un compte individuel créé pour la première fois sur NuGet.org pour être utilisé comme administrateur sur le compte org. Si vous n’en avez pas, veuillez [créer un nouveau compte NuGet.org](individual-accounts.md)
2. Suivez les [étapes pour récupérer votre connexion de mot de passe](#how-to-recover-nugetorg-password-login) pour votre compte NuGet.org si vous n’avez pas de connexion de mot de passe pour elle, si vous le faites, sauter cette étape.
3. [Connectez-vous à NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) à l’aide du nom d’utilisateur/mot de passe.
4. Une fois que vous êtes connecté, une boîte de dialogue contextuelle semblable à celle ci-dessous s’affiche. Il s’agit de la boîte de dialogue de suspension du mot de passe. 
    > [!Important]
    > Ignorez cette boîte de dialogue. Ne cliquez **pas** sur le bouton **Se connecter avec Microsoft**.

5. Accédez à [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). Cela vous permet de convertir le compte NuGet.org en compte d’organisation sans créer de lien à un compte Microsoft.
6. Spécifiez le nom d’utilisateur administrateur pour votre compte NuGet.org personnel/le compte que vous avez créé à l’étape 1.
7. Suivez les instructions permettant d’effectuer la transformation de ce compte en compte d’organisation.

    ![Boîte de dialogue de liaison de comptes MSA](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Vous rencontrez des problèmes de connexion à NuGet.org pour les comptes AAD avec un propriétaire non managé ?

Si vous voyez une erreur comme celle affichée ci-dessous pendant votre flux de connexion avec votre domaine de compte de messagerie (@yourdomain.com), consultez les étapes suivantes pour récupérer votre compte NuGet.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Qu’est-ce que cette chose état non gestion pendant la connexion? Et pourquoi cela se produit-il maintenant?** 

Votre compte semble avoir été précédemment inscrit en tant que compte Microsoft personnel et cela fonctionnait correctement. Toutefois, il semble que votre compte a maintenant été inscrit en tant que locataire « non managé » dans Azure Active Directory (service d’identité que nous utilisons pour authentifier les comptes Microsoft). 

Cela a pu se produire si vous ou une personne de votre organisation (avec l’adresse e-mail @yourdomain.com) vous êtes inscrit auprès de l’un des services intégrés AAD ou si vous avez effectué une [inscription en libre-service pour Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup), qui crée un tel locataire « non managé » pour le domaine de compte Microsoft utilisé (@yourdomain.com dans votre cas). 

**Que puis-je faire pour récupérer mon compte ?**

Pour le moment, nous (NuGet.org) ne disposons d’aucun moyen pour authentifier les comptes avec de tels comptes de locataires « non managés » dans Azure Active directory. Nous recherchons un meilleur moyen d’authentifier ces comptes.

Si vous voulez vous connecter à NuGet.org avec votre compte Microsoft (@yourdomain.com), vous (ou un administrateur de votre entreprise) devez revendiquer la propriété des comptes AAD en effectuant une validation DNS afin d’authentifier les utilisateurs avec l’adresse e-mail « @yourdomain.com ». Suivez les étapes permettant la [prise de contrôle des administrateurs de domaines](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover) documentées par Azure Active Directory. Une fois cela effectué, votre connexion normale doit commencer à fonctionner.

**Je ne veux pas effectuer toutes ces opérations. Quelle est l’autre façon de récupérer mon compte ?**

Vous pouvez [créer](https://www.microsoft.com/account) un compte Microsoft (avec une adresse e-mail **non** associée à @yourdomain.com). Suivez les étapes données dans [la récupération de votre section de compte NuGet.org.](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Comment changer mon nom d’utilisateur de compte NuGet.org ?

Ce n’est pas possible. En matière de politique, nous n’autorisons pas le changement de nom d’utilisateur. En outre, cela est un changement de rupture pour les utilisateurs qui peuvent avoir défini [les stratégies de fiducie de paquet basée sur le propriétaire du paquet](../consume-packages/installing-signed-packages.md#trust-package-owners). La seule façon de changer votre nom d’utilisateur consiste à créer un compte avec le nom d’utilisateur souhaité. Nous vous recommandons de supprimer votre compte existant avant d’en créer un nouveau. Sinon, vous ne pourrez pas réutiliser votre compte Microsoft inscrit.
> [!Important]
> La suppression de l’utilisateur **réserve** toutefois la valeur `username`. Vous ne pourrez pas réutiliser le même nom d’utilisateur et **cela inclut le changement de casse**. Par exemple, si vous avez créé un utilisateur avec le nom d’utilisateur `mycoolname` et que vous voulez le remplacer par `MyCoolName` (changement de casse), ce ne sera pas possible après la suppression de l’utilisateur.

Suivez les étapes données pour [supprimer votre](#how-to-delete-my-nugetorg-account) section NuGet.org compte et enregistrer un nouveau [compte](individual-accounts.md) avec un nom d’utilisateur correct.

### <a name="how-to-delete-my-nugetorg-account"></a>Comment supprimer mon compte NuGet.org ?

Pour supprimer votre compte, notez que nous vous recommandons de transférer la propriété de tous les packages dont vous êtes l’unique propriétaire. Pour savoir comment procéder, lisez la section relative à la [gestion des propriétaires de packages](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg). Cela nous permettra également d’accélérer votre demande.

Si vous envisagez de transformer votre compte en organisation, suivez les étapes indiquées dans [transformer mon compte NuGet.org en organisation.](#how-to-transform-my-nugetorg-account-to-an-organization)

> [!Important]
> La suppression de l’utilisateur a les conséquences suivantes :
>  1. Votre nom d’utilisateur sera réservé et personne ne pourra l’utiliser à nouveau pour créer un compte individuel ou un compte d’organisation
>  1. Révocation des clés API associées. 
>  1. Suppression du compte en tant que propriétaire des packages enfants.
>  1. Dissociation de toutes les réservations de préfixe d’ID précédemment existantes avec ce compte.
>  1. Suppression du compte en tant que membre d’une organisation.

Effectuez les étapes suivantes pour procéder à la suppression du compte.
1. [Connectez-vous pour NuGet.org](https://www.nuget.org/users/account/LogOn) avec le compte que vous souhaitez supprimer.
2. Cliquez sur cette [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) URL: et suivez les étapes pour soumettre la demande de suppression du compte.

Notre service clientèle traitera cette demande et effectuera la suppression du compte.
