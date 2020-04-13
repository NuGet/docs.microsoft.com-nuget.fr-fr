---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68419921"
---
1. [Connectez-vous à votre compte nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) ou créez un compte si vous ne l’avez pas déjà fait.

   Pour plus d’informations sur la création de votre compte, consultez [Comptes individuels](../../nuget-org/individual-accounts.md).

1. Sélectionnez votre nom d’utilisateur (dans le coin supérieur droit), puis **Clés API**.

1. Sélectionnez **Créer**, donnez un nom à votre clé et sélectionnez **Sélectionner les étendues > Envoyer (push)**. Entrez * pour **Modèle Glob**, puis sélectionnez **Créer**. (Consultez la suite pour plus d’informations sur les étendues.)

1. Une fois la clé créée, sélectionnez **Copier** pour récupérer la clé d’accès dont vous avez besoin dans l’interface CLI :

    ![Copie de la clé d’API dans le Presse-papiers](../media/QS_Create-02-APIKey.png)

1. **Important**: enregistrez votre clé dans un emplacement sécurisé car vous ne pourrez plus la recopier par la suite. Si vous retournez sur la page de la clé API, vous devez régénérer la clé pour la copier. Vous pouvez également supprimer la clé API si vous ne souhaitez plus distribuer des packages par le biais de l’interface CLI.

La définition d’étendue permet de créer des clés API distinctes selon les finalités. Chacune a son délai d’expiration et peut être restreinte à des packages (ou des modèles Glob) spécifiques. Chaque clé est également limitée à certaines opérations : transmission de nouveaux packages et de mises à jour, transmission de mises à jour uniquement ou retrait d’une liste. La définition d’étendue permet de créer des clés API pour les différentes personnes qui gèrent des packages dans votre organisation, de sorte qu’elles disposent uniquement des autorisations dont elles ont besoin. Pour plus d’informations, consultez [Clés API délimitées](../../nuget-org/scoped-api-keys.md).