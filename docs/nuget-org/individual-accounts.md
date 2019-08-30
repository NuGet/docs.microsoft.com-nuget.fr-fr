---
title: Comptes individuels - NuGet.org
description: Des comptes individuels sur NuGet.org sont nécessaires pour publier des packages
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 63c6b5eb5ad635e436b4d53a5f833af35f72d76f
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999966"
---
# <a name="individual-accounts-on-nugetorg"></a>Comptes individuels sur NuGet.org

Vous devez créer un compte individuel pour publier et gérer des packages sur NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Comptes individuels et comptes d’organisation

Votre compte individuel (utilisateur) est votre identité sur NuGet.org et peut être membre de plusieurs organisations. Un package peut appartenir à un compte d’organisation ou à un compte individuel. Pour les consommateurs de packages, il n’y a aucune différence entre un compte individuel et le compte d’organisation : tous deux apparaissent comme `owners` de packages.

Un compte d’organisation comprend un ou plusieurs comptes individuels comme membres. Ces membres peuvent gérer un ensemble de packages tout en conservant une identité unique pour appropriation.

## <a name="add-a-new-individual-account"></a>Ajouter un nouveau compte individuel

Pour créer un compte NuGet.org, vous devez disposer d’un compte Microsoft personnel (MSA) ou d’un compte Azure Active Directory (AAD). Si vous n’en avez pas, vous pouvez en [créer](https://signup.live.com) un. Effectuez les étapes suivantes si vous disposez d’un compte MSA ou AAD.

1. Accédez à la [page de connexion de NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Cliquez sur le bouton **Se connecter avec Microsoft**.

1. Entrez les détails de votre compte Microsoft ou Azure Active Directory.

1. Cliquez sur **Oui** pour accepter les autorisations à donner à l’application *NuGet.org*.

   ![Octroi d’autorisations à NuGet.org](media/nuget-org-permissions.png)

1. Vous allez être redirigé vers *nuget.org* et invité à inscrire un nom d’utilisateur.

1. Spécifiez le nom d’utilisateur dans la zone d’entrée. Notez que le nom d’utilisateur **est** sensible à la casse et ne peut pas être changé ou renommé ultérieurement.

   ![Spécifier un nom d’utilisateur sur NuGet.org](media/nuget-org-register.png) 

1. Cliquez sur le bouton **Inscrire**.

Vous disposez maintenant d’un compte NuGet.org. Vous pouvez effectuer la gestion des comptes dans la page des [paramètres du compte](https://www.nuget.org/account).

## <a name="enable-two-factor-authentication-2fa"></a>Activer l’authentification à 2 facteurs (2FA)

Pour mieux protéger votre compte, activez l’authentification à 2 facteurs (recommandé).

1. Une fois connecté à votre compte, ouvrez votre profil et choisissez **Activer** sous **Compte de connexion**.

   ![Activer la 2FA](media/nuget-org-register-2fa.png)

   Vous voyez un message vous indiquant que la prochaine fois que vous vous connecterez *à nuget.org*, vous serez invité à fournir des informations d’identification supplémentaires.

2. Pour terminer l’authentification à ce stade, déconnectez-vous, puis reconnectez-vous.

3. Quand vous vous connectez, choisissez le texte ou le courrier électronique comme deuxième forme d’authentification.

   Vérifiez le numéro de téléphone ou l’adresse e-mail qui est déjà associée à votre compte Microsoft. Vous devrez peut-être entrer un nouveau numéro de téléphone ou une nouvelle adresse e-mail pour votre compte. Dans ce cas, entrez les informations requises comme indiqué, puis cliquez sur **Suivant**.

   ![Activer la 2FA](media/nuget-org-sign-in-2fa.png)

4. Vérifiez votre appareil ou votre compte de messagerie, puis entrez le code que vous venez de recevoir.

   ![Activer la 2FA](media/nuget-org-enter-code-2fa.png)

5. Suivez les instructions supplémentaires pour terminer l’authentification à 2 deux facteurs.

## <a name="delete-a-nugetorg-account"></a>Supprimer un compte NuGet.org

Pour obtenir de l’aide sur d’autres tâches en lien avec les comptes, comme supprimer un compte NuGet.org, consultez [Gestion des comptes NuGet.org](nuget-org-faq.md#nugetorg-account-management).
