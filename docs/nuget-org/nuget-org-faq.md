---
title: Questions fréquentes (FAQ) sur NuGet.org
description: Questions et réponses courantes concernant l’utilisation de la galerie NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 915f6e4cfc0b21d2b10006c62e8230720d07ce74
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428904"
---
# <a name="nugetorg-frequently-asked-questions"></a>Questions fréquentes (FAQ) sur NuGet.org

## <a name="license-terms"></a>Termes du contrat de licence

**Quels sont les termes du contrat de licence si un package ne fournit pas des informations de licence spécifiques ?**

Chaque package est régi par les conditions qu’il inclut. Vous devez examiner les conditions applicables avant d’accéder à des packages, d’en télécharger ou d’en acquérir. Sur NuGet.org, utilisez le lien **License Info** (Informations de licence) sur la page des packages.

Si un package ne spécifie pas les termes du contrat de licence, contactez le propriétaire du package directement à l’aide du lien **Contact owners** (Contacter les propriétaires) sur la page des packages NuGet.org. Microsoft ne vous accorde pas de licences de droits de propriété intellectuelle pour le compte de fournisseurs de packages tiers et n’est pas responsable des informations fournies par des tiers.

## <a name="managing-packages-on-nugetorg"></a>Gestion des packages sur NuGet.org

**Puis-je modifier les métadonnées d’un package après l’avoir chargé ?**

NuGet recommande de signer tous les packages. Un principe de conception de la signature du package est que le contenu du package signé doit être immuable, ce qui comprend le fichier nuspec. Modifier les métadonnées du package entraîne des modifications du fichier nuspec, invalidant les signatures existantes. Nous vous recommandons de modifier les flux de travail existants de manière à ce qu’il ne soit pas nécessaire de modifier les métadonnées du package une fois ce dernier créé.

Notez que les dépendances répertoriées pour votre package sont générées automatiquement à partir du package lui-même et qu’elles ne peuvent pas être modifiées.

De plus, le chargement d’un package sur [int.nugettest.org](https://int.nugettest.org) constitue un excellent moyen de le tester et de le valider sans le mettre à disposition dans la galerie publique. Point de terminaison d’API : https://apiint.nugettest.org/v3/index.json

**Puis-je supprimer un package déjà publié sur NuGet.org ?**

En général, nous ne prenons pas en charge la suppression d’un package publié sur NuGet.org. En savoir plus sur notre [stratégie sur la suppression des packages](policies/deleting-packages.md).

**Est-il possible de réserver des noms pour les packages destinés à être publiés ?**

Oui. Vous pouvez réserver des ID pour les packages sur [NuGet.org](https://www.nuget.org/) en demandant un préfixe d’ID de package pour votre compte. Pour demander un préfixe d’ID de package, suivez les instructions de la [documentation](id-prefix-reservation.md).

**Comment revendiquer la propriété de packages ?**

Consultez [Gestion des propriétaires de packages sur NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

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

- Téléchargez [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download).
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
- Activez **l’option Capture Traffic (Capturer le trafic) dans le menu File (Fichier)** .
- Démarrez Visual Studio ou nuget.exe et effectuez les actions qui ne fonctionnent pas. Le trafic généré par ces actions doit s’afficher dans Fiddler.
- Une fois les actions exécutées, utilisez **File > Save > All Sessions** (Fichier > Enregistrer > Toutes les sessions) pour stocker les sessions capturées.

Remarque : Il peut être nécessaire de définir la variable d’environnement `HTTP_PROXY` sur `http://127.0.0.1:8888` pour router le trafic NuGet via Fiddler.

Si cette opération échoue, essayez les [conseils mentionnés dans ce billet de StackOverflow](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>Gestion de compte NuGet.org

### <a name="how-to-recover-nugetorg-password-login"></a>Comment récupérer le mot de passe de connexion NuGet.org ?

Notez que le [mot de passe de connexion NuGet.org n’est plus disponible](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) et que la seule façon de se connecter à NuGet.org est d’utiliser un compte Microsoft personnel (MSA) ou un compte Azure Active Directory (AAD). Toutefois, si vous ne parvenez pas à accéder à vos comptes MSA/AAD associés, vous devrez peut-être utiliser un mot de passe de connexion pour récupérer votre compte NuGet.org. Dans ce cas, suivez les étapes ci-dessous.
- **Condition requise :** Vous devez avoir accès à l’adresse de messagerie associée au compte pour lequel vous devez récupérer le mot de passe.
- Accédez à la [page Mot de passe oublié](https://www.nuget.org/account/ForgotPassword).
- Entrez l’adresse **e-mail** associée au compte NuGet.org que vous voulez récupérer.
- Cliquez sur le bouton **Send** (Envoyer).
- Vous obtenez un e-mail pour le compte d’adresse e-mail spécifié avec un lien pour réinitialiser votre mot de passe. Cliquez sur ce lien et définissez le nouveau mot de passe. Si vous ne trouvez pas l’e-mail, vérifiez votre dossier « Courrier indésirable ».
- Une fois cette opération effectuée, vous pouvez vous connecter à NuGet avec le nom d’utilisateur/mot de passe.
- Pour vous connecter avec un nom d’utilisateur/mot de passe, utilisez le lien **Se connecter à l’aide du compte Nuget.org** sur la [page de connexion à NuGet.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Quel compte Microsoft est lié à mon compte NuGet.org ?

Si vous avez oublié quel compte Microsoft est associé à votre compte NuGet.org, effectuez les étapes ci-dessous pour obtenir de l’aide.
1. Accédez à la [page de connexion à NuGet.org](https://www.nuget.org/users/account/LogOn), puis cliquez sur le lien **Vous avez besoin d’aide pour vous connecter ?** .
1. Une boîte de dialogue contextuelle permettant d’obtenir de l’aide s’affiche alors. Effectuez les étapes décrites dans cette boîte de dialogue pour comprendre le ou les comptes Microsoft associés à votre compte NuGet.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Comment changer le compte Microsoft que j’utilise pour la connexion à NuGet.org ?
Si vous voulez changer le compte Microsoft de l’utilisateur NuGet.org, effectuez les étapes ci-dessous. Supposons que votre compte Microsoft avec l’adresse e-mail `account1@outlook.com` est associé à votre compte NuGet.org avec le nom d’utilisateur `MyNuGetAccount`. Vous voulez rempalcer les informations de connexion par un autre compte Microsoft avec l’adresse e-mail `account2@outlook.com`
1. Connectez-vous à l’aide du **compte Microsoft actuellement associé**, c’est-à-dire `account1@outlook.com`, sur la [page de connexion](https://www.nuget.org/users/account/LogOn) après avoir cliqué sur **Se connecter avec Microsoft**.
1. Une fois connecté, accédez à la page de vos [paramètres du compte](https://www.nuget.org/account).
1. Développez la section relative au **compte de connexion**. Cliquez sur le bouton **Changer de compte**.
1. Vous allez maintenant être redirigé vers la page de connexion de Microsoft. Connectez-vous avec le compte pour lequel vous souhaitez modifier l’Association, c.-à-d. `account2@outlook.com`. **Remarque**: vous devrez peut-être cliquer sur **se déconnecter et vous connecter avec un autre compte** au cours du processus de connexion pour pouvoir vous connecter avec une autre compte Microsoft.
1. Si vous voyez une erreur comme celle affichée ci-dessous, consultez [Le compte Microsoft est lié à un autre compte NuGet.org](#microsoft-account-is-linked-with-another-nugetorg-account) pour plus d’informations.
    >_Échec de la mise à jour de la compte Microsoft avec « Account2 <account2@outlook.com>». Cela peut se produire s’il est déjà lié à un autre compte NuGet. Pour plus d’informations, contactez le support._

1. Une fois que vous êtes connecté avec votre deuxième compte, vous êtes redirigé vers la page des paramètres de votre compte NuGet.org et vous devez maintenant voir le nouveau compte Microsoft associé en tant que compte de connexion. Dorénavant, vous devez utiliser ce compte quand vous vous connectez à NuGet.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Le compte Microsoft est lié à un autre compte NuGet.org.

Vous avez essayé de changer votre connexion Microsoft et l’erreur ci-dessous s’est affichée :
> _Échec de la mise à jour de la compte Microsoft avec « Account2 <account2@outlook.com>». Cela peut se produire s’il est déjà lié à un autre compte NuGet. Pour plus d’informations, contactez le support._

Supposons que vous tentiez de remplacer la connexion au compte Microsoft `account1@outlook.com` pour l’utilisateur NuGet.org avec le nom d’utilisateur `MyNuGetAccount1` par un autre compte Microsoft avec l’adresse e-mail `account2@outlook.com`. L’erreur ci-dessus s’affiche alors.

**Que signifie l’erreur ci-dessus ?**

Elle signifie qu’un autre compte NuGet.org est associé au compte Microsoft que vous essayez d’utiliser pour le remplacer ; à savoir, dans l’exemple ci-dessus, le compte Microsoft avec l’adresse e-mail `<account2@outlook.com>` est associé à un autre compte NuGet.org avec, par exemple, le nom d’utilisateur `MyNuGetAccount2`.

Vous ne pouvez pas remplacer la connexion associée par un compte Microsoft qui est lié à un autre compte NuGet.org.

**J’ai oublié que j’avais un autre compte NuGet.org. Comment savoir de quel compte NuGet.org il s’agit ?**

Connectez-vous avec le deuxième compte Microsoft sur la [page de connexion](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "page de connexion"). Vous serez connecté au compte NuGet.org qui est actuellement associé au deuxième compte Microsoft. Vous pouvez alors afficher les packages chargés et effectuer la gestion de compte sur ce compte.

**Je ne m’intéresse pas à ce deuxième compte NuGet.org, je souhaite modifier ma connexion pour le premier compte NuGet.org avec le deuxième compte Microsoft. Que dois-je faire ?**

Vous voulez ne pas vous soucier du deuxième compte NuGet.org et quand même réutiliser le compte Microsoft associé avec l’adresse e-mail `account2@outlook.com`. 

Vous pouvez libérer l’association entre le compte Microsoft et le compte NuGet.org en supprimant le compte NuGet.org.
1. Effectuez les étapes permettant de [supprimer l’utilisateur](#how-to-delete-my-nugetorg-account) pour le deuxième compte NuGet.org `MyNuGetAccount2`. 
1. Une fois ce compte supprimé, vous pouvez retenter les étapes permettant de [changer la connexion au compte Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Attendez, je m’intéresse également à ce deuxième compte. Je ne souhaite pas perdre ce compte, mais je modifie les connexions de compte associées pour le premier compte.**

Vous devrez créer/utiliser un troisième compte Microsoft, par exemple avec l’adresse e-mail `account3@outlook.com`. 
1. Tout d’abord, vous devez vous connecter avec votre deuxième compte Microsoft, `account2@outlook.com` sur NuGet.org. Suivez les étapes ci-dessus pour modifier les connexions associées et associer le troisième compte Microsoft à ce compte NuGet.org.
1. Une fois cela effectué, votre deuxième compte Microsoft avec l’adresse e-mail `account2@outlook.com` peut être associé à votre premier compte NuGet.org, `MyNuGetAccount1`. Effectuez les mêmes étapes ci-dessus pour changer les informations de connexion Microsoft pour le deuxième compte Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>La connexion avec un compte Microsoft me montre que mon e-mail est lié à un autre compte Microsoft

Si vous avez essayé de vous connecter avec votre compte Microsoft, par exemple avec l’adresse e-mail `account1@outlook.com` et vous voyez une erreur comme celle ci-dessous :
> _Le compte avec l’e-mail « account1@outlook.com » est lié à un autre compte Microsoft._
>
> _Si vous voulez mettre à jour le compte Microsoft lié, vous pouvez le faire à partir de la page des paramètres du compte._

**Que signifie l’erreur ci-dessus ?**

Quand un compte est créé sur NuGet.org, une adresse e-mail de communication lui est associée. Elle est généralement identique à l’adresse e-mail utilisée pour le compte Microsoft associé. Toutefois, vous pouvez choisir de spécifier une autre adresse e-mail pour la communication. Par conséquent, techniquement, vous pouvez avoir un autre compte Microsoft, par exemple avec `account2@outlook.com`, lié à un compte NuGet.org ayant l’adresse e-mail de communication `account1@outlook.com`.

Par conséquent, l’erreur ci-dessus signifie qu’il existe déjà un compte NuGet.org avec une adresse de messagerie de communication `account1@outlook.com` mais qu’il est associé à un autre compte Microsoft avec un e-mail **qui n’est pas** `account1@outlook.com`.

**Comment savoir quel compte Microsoft est lié à ce compte NuGet.org ?**

Vous devez utiliser le flux d’[aide relative à la connexion](#which-microsoft-account-is-linked-to-my-nugetorg-account) pour déterminer quel compte Microsoft est lié au compte NuGet.org avec l’adresse e-mail `account1@outlook.com`.

**Je souhaite remplacer ce compte par mon compte Microsoft**

Effectuez les étapes mentionnées dans la section [Impossible d’utiliser la connexion Microsoft. Comment récupérer mon compte NuGet.org ?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) pour associer votre compte Microsoft au compte NuGet.org existant.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Impossible d’utiliser la connexion Microsoft. Comment récupérer mon compte NuGet.org ?

Si vous avez essayé d’utiliser l’[aide relative à la connexion](#which-microsoft-account-is-linked-to-my-nugetorg-account) et que vous n’avez pas accès au compte Microsoft associé à votre compte NuGet.org, effectuez les étapes ci-dessous pour lier un nouveau compte Microsoft à votre compte NuGet.org.
1. **Exigence**: vous aurez besoin d’un accès à un compte Microsoft qui n’est associé à aucun compte NuGet.org existant. Si vous n’en avez pas, vous pouvez en [créer](https://signup.live.com) un.
2. Si vous avez oublié votre nom d’utilisateur et le mot de passe associés à votre compte NuGet.org, suivez ces [étapes pour récupérer votre mot de passe de connexion](#how-to-recover-nugetorg-password-login).
3. [Connectez-vous à NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) à l’aide du nom d’utilisateur/mot de passe de connexion.
4. Une fois que vous êtes connecté, une boîte de dialogue contextuelle semblable à celle ci-dessous s’affiche. Il s’agit de la boîte de dialogue de suspension du mot de passe.
5. **Remarque**: ignorez l’instruction pour vous connecter avec le compte Microsoft spécifié. Vous pouvez maintenant lier votre compte NuGet.org à n’importe quelle autre connexion Microsoft.
6. Cliquez sur le bouton **Se connecter avec Microsoft** et connectez-vous avec le compte Microsoft auquel vous avez accès, comme indiqué à l’étape 1.
7. Votre compte est maintenant lié au nouveau compte Microsoft, que vous pouvez dorénavant utiliser pour vous connecter à NuGet.org.

    ![Boîte de dialogue de liaison de comptes MSA](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Comment transformer mon compte NuGet.org en compte d’organisation ?

Si vous voulez transformer votre compte en compte d’organisation, et que ce compte est déjà associé à une connexion au compte Microsoft, effectuez les étapes indiquées dans la documentation concernant les [comptes d’organisation sur nuget.org](organizations-on-nuget-org.md).

Toutefois, si votre compte NuGet.org n’est pas associé/lié à un compte Microsoft, vous pouvez suivre les étapes ci-dessous pour transformer ce compte en compte d’organisation.
1. **Exigence**: vous devez d’abord créer un compte individuel sur NuGet.org pour l’utiliser en tant qu’administrateur sur le compte d’organisation. Si vous n’en avez pas, [créez un compte NuGet.org](individual-accounts.md).
2. Suivez les [étapes permettant de récupérer votre mot de passe de connexion](#how-to-recover-nugetorg-password-login) pour votre compte NuGet.org si vous n’avez pas de mot de passe de connexion. Dans le cas contraire, ignorez cette étape.
3. [Connectez-vous à NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) à l’aide du nom d’utilisateur/mot de passe de connexion.
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

**Qu’est-ce que l’état non géré pendant la connexion ? Et pourquoi cela se produit-il maintenant ?** 

Votre compte semble avoir été précédemment inscrit en tant que compte Microsoft personnel et cela fonctionnait correctement. Toutefois, il semble que votre compte a maintenant été inscrit en tant que locataire « non managé » dans Azure Active Directory (service d’identité que nous utilisons pour authentifier les comptes Microsoft). 

Cela a pu se produire si vous ou une personne de votre organisation (avec l’adresse e-mail @yourdomain.com) vous êtes inscrit auprès de l’un des services intégrés AAD ou si vous avez effectué une [inscription en libre-service pour Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup), qui crée un tel locataire « non managé » pour le domaine de compte Microsoft utilisé (@yourdomain.com dans votre cas). 

**Que puis-je faire pour récupérer mon compte ?**

Pour le moment, nous (NuGet.org) ne disposons d’aucun moyen pour authentifier les comptes avec de tels comptes de locataires « non managés » dans Azure Active directory. Nous recherchons un meilleur moyen d’authentifier ces comptes.

Si vous voulez vous connecter à NuGet.org avec votre compte Microsoft (@yourdomain.com), vous (ou un administrateur de votre entreprise) devez revendiquer la propriété des comptes AAD en effectuant une validation DNS afin d’authentifier les utilisateurs avec l’adresse e-mail « @yourdomain.com ». Suivez les étapes permettant la [prise de contrôle des administrateurs de domaines](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover) documentées par Azure Active Directory. Une fois cela effectué, votre connexion normale doit commencer à fonctionner.

**Je ne veux pas effectuer toutes ces opérations. Quelle est l’autre façon de récupérer mon compte ?**

Vous pouvez [créer](https://www.microsoft.com/account) un compte Microsoft (avec une adresse e-mail **non** associée à @yourdomain.com). Suivez les étapes indiquées dans la section relative à la [récupération de votre compte NuGet.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account).

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Comment changer mon nom d’utilisateur de compte NuGet.org ?

Ce n’est pas possible. En matière de stratégie, nous n’autorisons pas la modification des noms d’utilisateur. En outre, il s’agit d’une modification avec rupture pour les utilisateurs qui peuvent avoir défini des [stratégies d’approbation de package basées sur le propriétaire du package](../consume-packages/installing-signed-packages.md#trust-package-owners). La seule façon de changer votre nom d’utilisateur consiste à créer un compte avec le nom d’utilisateur souhaité. Nous vous recommandons de supprimer votre compte existant avant d’en créer un nouveau. Sinon, vous ne pourrez pas réutiliser votre compte Microsoft inscrit.
> [!Important]
> La suppression de l’utilisateur **réserve** toutefois la valeur `username`. Vous ne pourrez pas réutiliser le même nom d’utilisateur et **cela inclut le changement de casse**. Par exemple, si vous avez créé un utilisateur avec le nom d’utilisateur `mycoolname` et que vous voulez le remplacer par `MyCoolName` (changement de casse), ce ne sera pas possible après la suppression de l’utilisateur.

Suivez les étapes indiquées dans la section relative à la [suppression de votre compte NuGet.org](#how-to-delete-my-nugetorg-account) et celles permettant d’[inscrire un nouveau compte](individual-accounts.md) avec le nom d’utilisateur correct.

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
1. [Connectez-vous à NuGet.org](https://www.nuget.org/users/account/LogOn) avec le compte que vous voulez supprimer.
2. Cliquez sur l’URL [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete), puis effectuez les étapes permettant de soumettre la demande de suppression du compte.

Notre service clientèle traitera cette demande et effectuera la suppression du compte.
