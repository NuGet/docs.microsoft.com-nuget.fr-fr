---
title: Organisations sur nuget.org
description: Les organisations sur nuget.org vous aide à gérer les packages publiés par groupe ou dans une équipe, l’environnement d’entreprise.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551226"
---
# <a name="organization-on-nugetorg"></a>Organisation sur nuget.org

Les organisations permettent aux entreprises et les projets open source pour collaborer sur des packages à l’aide d’une identité unique nuget.org. Pour un consommateur de package, un compte d’organisation apparaît identique à un compte d’utilisateur existant sur nuget.org.

## <a name="user-accounts-vs-organization-accounts"></a>Comptes d’utilisateurs et comptes d’organisation

Votre compte d’utilisateur est votre identité sur nuget.org et peut être un membre de n’importe quel nombre d’organisations. Un package peut appartenir à un compte d’organisation comme il peut appartenir à un compte d’utilisateur. Les consommateurs de package ne voient aucune différence entre un compte d’utilisateur ou le compte d’organisation : les deux s’affichent en tant que package `owners`.

Un compte d’organisation a un ou plusieurs comptes d’utilisateur en tant que ses membres. Ces membres peuvent gérer un ensemble de packages tout en conservant une identité unique pour la propriété.

## <a name="adding-a-new-organization"></a>Ajout d’une organisation

Pour ajouter une nouvelle organisation, sélectionnez votre compte sur nuget.org, puis le **aux organisations de gérer...**  commande de menu :

![Option de menu sur nuget.org pour les organisations Manager](media/org-manage-option.png)

Sur la page suivante, sélectionnez le **ajouter une nouvelle organisation** bouton :

![Bouton permettant de créer une nouvelle organisation sur nuget.org](media/org-add-new-option.png)

Sur la page suivante, indiquez l’adresse e-mail et du nom de l’organisation. Dans la mesure où les comptes d’organisation partagent le même espace de noms en tant que comptes d’utilisateur, le nom d’organisation doit être différent de tout autre organisation existante ou comptes d’utilisateur. L’adresse de messagerie doit également être unique sur tous les comptes.

![Ajouter une nouvelle page de l’organisation sur nuget.org](media/org-add-new-page.png)

Une fois que le compte d’organisation est créé, vous êtes l’administrateur et pouvez envoyer des packages pour l’organisation et ajouter des membres de l’organisation.

### <a name="transform-existing-account-to-an-organization"></a>Transformer le compte existant à une organisation

> [!Warning]
> Conversion de compte est irréversible : vous ne pouvez pas transformer une organisation à un compte d’utilisateur.

Si vous gérez des packages en tant qu’équipe à l’aide d’un seul compte d’utilisateur et que vous souhaitez convertir ce compte dans une organisation, utilisez le **transformer votre compte pour une organisation** option sur le **gérer les organisations** page :

![Option sur nuget.org pour transformer un compte existant à une organisation](media/org-transform-option.png)

Sur la page suivante, spécifiez le compte d’utilisateur différent pour l’affecter en tant que l’administrateur de l’organisation, puis sélectionnez **transformer**.

![Entrer des informations pour la transformation d’un compte d’utilisateur à une organisation](media/org-transform-page.png)

## <a name="managing-organization-members"></a>La gestion des membres de l’organisation

En tant qu’administrateur de l’organisation, vous pouvez ajouter des membres en fournissant nuget.org de chaque membre *nom de compte d’utilisateur*; les adresses de messagerie ne peut pas être utilisés. Marquez ensuite chaque membre en tant que collaborateur ou administrateur disposant des autorisations suivantes :

| Autorisation | Collaborateur | Administrateur |
| --- | --- | --- |
| Gérer les packages de l’organisation<br/>(nouveaux packages, mettre à jour ou de retirer de la liste des packages existants) | Oui | Oui |
| Métadonnées d’organisation de modification<br/>(adresse de messagerie, les paramètres de notification) | Non | Oui |
| Gérer les membres de l’organisation | Non | Oui |
| Demander ou agir sur les demandes de copropriété pour les packages de l’organisation | Non | Oui |

## <a name="managing-packages"></a>La gestion des packages

Vous pouvez afficher tous les packages sur votre compte et toutes les organisations dont vous êtes un membre sur le [gérer les Packages](https://www.nuget.org/account/Packages) page. Pour afficher les packages spécifiques à votre compte ou n’importe quelle organisation spécifique, utilisez le filtre de comptes dans le coin supérieur droit de la page.

![Gestion des packages avec le filtre de compte](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Transfert de packages vers une organisation
Si vous souhaitez transférer certains de vos packages à une organisation nouvellement créée, vous pouvez le faire en demandant le compte d’organisation pour copropriétaires le package, puis en supprimant vous-même en tant que le propriétaire. Si vous êtes un administrateur de l’organisation, il n’existe aucune confirmation demandée d’accepter la propriété. Toutefois, si vous êtes un collaborateur, ajout de l’organisation en tant que propriétaire nécessite l’un des administrateurs pour accepter la propriété.

## <a name="publishing-packages"></a>Publication de packages

Publier des packages à une organisation comme vous publiez des packages à un compte d’utilisateur : en chargeant directement le package sur nuget.org ou en envoyant le package le `nuget push` ou `dotnet nuget push` commandes CLI.

### <a name="uploading-packages"></a>Chargement des packages

Lorsque vous téléchargez directement un nouveau package sur le [nuget.org chargement](https://www.nuget.org/packages/manage/upload) page, vous affectez le propriétaire du package à un compte utilisateur ou de l’organisation :

![Télécharger le package avec l’option de compte](media/org-upload-option.png)

### <a name="using-api-keys"></a>À l’aide de clés API

Pour envoyer un package le `nuget push` ou `dotnet nuget push` des commandes CLI, vous devez obtenir une clé d’API requise par ces commandes. Pour plus d’informations, consultez [publier un package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Lorsque vous créez une nouvelle clé d’API, sélectionnez l’organisation appropriée dans le **propriétaire du Package** liste déroulante. N’importe quelle touche d’API que vous créez s’applique uniquement à l’organisation choisie :

![Clé API avec l’option de compte](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Suppression d’une organisation

En tant qu’utilisateur, vous pouvez vous désinscrire à partir d’une organisation en sélectionnant le `X` bouton illustré par l’appartenance à votre organisation :

![Suppression d’un compte d’utilisateur à partir d’une organisation](media/org-remove-self-option.png)

Les administrateurs peuvent supprimer n’importe quel membre de l’organisation, y compris les autres administrateurs. Si vous êtes le seul administrateur d’une organisation, vous ne pouvez pas vous supprimer sauf si vous ajoutez un autre membre en tant qu’administrateur.

### <a name="deleting-an-organization-account"></a>Suppression d’un compte d’organisation

Cette fonctionnalité sera bientôt disponible.
