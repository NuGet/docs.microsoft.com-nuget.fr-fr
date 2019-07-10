---
title: Votre organisation sur NuGet.org
description: Les organisations sur NuGet.org vous aident à gérer les packages qui sont publiés par un groupe ou dans une équipe au sein d’une entreprise.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427074"
---
# <a name="your-organization-on-nugetorg"></a>Votre organisation sur NuGet.org

Les organisations permettent à des projets d’entreprise et des projets open source de travailler ensemble sur des packages en utilisant une identité NuGet.org unique. Pour un consommateur de package, un compte d’organisation se présente de la même façon qu’un compte d’utilisateur existant sur NuGet.org.

## <a name="organization-accounts-vs-individual-accounts"></a>Comptes d’organisation et comptes individuels

Un compte d’organisation comprend un ou plusieurs comptes (d’utilisateur) individuels comme membres. Ces membres peuvent gérer un ensemble de packages tout en conservant une identité unique pour la propriété.

Votre compte individuel constitue votre identité sur NuGet.org et peut être membre de plusieurs organisations. Un package peut appartenir à un compte d’organisation ou à un compte individuel. Pour les consommateurs de packages, il n’y a aucune différence entre un compte individuel et le compte d’organisation : tous deux sont présentés comme les propriétaires (`owners`) des packages.

## <a name="adding-a-new-organization"></a>Ajout d’une nouvelle organisation

Pour ajouter une nouvelle organisation, sélectionnez votre compte sur NuGet.org, puis sélectionnez la commande de menu **Gérer les organisations...**  :

![Option de menu Gérer les organisations sur NuGet.org](media/org-manage-option.png)

Dans la page suivante, sélectionnez le bouton **Ajouter une nouvelle organisation** :

![Bouton pour créer une organisation sur NuGet.org](media/org-add-new-option.png)

Dans la page suivante, entrez le nom et l’adresse e-mail de l’organisation. Dans la mesure où les comptes d’organisation partagent le même espace de noms avec les comptes d’utilisateur, choisissez un nom d’organisation différent des autres noms de compte d’organisation ou d’utilisateur existants. L’adresse e-mail doit également être unique à chaque compte.

![Page Ajouter une nouvelle organisation sur NuGet.org](media/org-add-new-page.png)

Une fois que vous avez créé le compte d’organisation, vous en êtes l’administrateur et, à ce titre, vous pouvez publier des packages pour l’organisation et ajouter des membres à l’organisation.

### <a name="transform-existing-account-to-an-organization"></a>Transformer un compte existant en organisation

> [!Warning]
> La conversion de compte est irréversible : vous ne pouvez plus après transformer une organisation en compte d’utilisateur.

Si vous gérez les packages d’une équipe à l’aide d’un seul compte d’utilisateur et que vous souhaitez convertir ce compte en organisation, utilisez l’option **Transformer votre compte en organisation** dans la page **Gérer les organisations** :

![Option sur NuGet.org pour transformer un compte existant en organisation](media/org-transform-option.png)

Dans la page suivante, sélectionnez un compte d’utilisateur différent et définissez-le en tant qu’administrateur de l’organisation, puis sélectionnez **Transformer**.

![Saisie des informations pour la transformation d’un compte d’utilisateur en organisation](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Gérer les membres de l’organisation

En tant qu’administrateur de l’organisation, vous pouvez ajouter des membres en indiquant le *nom du compte d’utilisateur* NuGet.org de chaque membre (l’ajout avec les adresses e-mail n’est pas possible). Vous définissez ensuite chaque membre comme collaborateur ou administrateur avec les autorisations suivantes :

| Autorisation | Collaborateur | Administrateur |
| --- | --- | --- |
| Gérer les packages de l’organisation<br/>(publier de nouveaux packages, mettre à jour des packages existants ou en retirer de la liste) | Oui | Oui |
| Modifier les métadonnées de l’organisation<br/>(adresse e-mail, paramètres de notification) | Non | Oui |
| Gérer les membres de l’organisation | Non | Oui |
| Demander la copropriété ou agir sur les demandes de copropriété pour les packages de l’organisation | Non | Oui |

## <a name="managing-packages"></a>Gérer les packages

Dans la page [Gérer les packages](https://www.nuget.org/account/Packages), vous pouvez voir tous les packages associés à votre compte et toutes les organisations dont vous êtes membre. Pour voir les packages associés à votre compte ou ceux d’une organisation spécifique, utilisez le filtre de comptes situé en haut à droite de la page.

![Gestion des packages avec le filtre de comptes](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Transférer des packages vers une organisation
Si vous souhaitez transférer certains de vos packages vers une organisation que vous venez de créer, demandez au compte d’organisation d’être copropriétaire du package, puis supprimez votre compte en tant que propriétaire. Si vous êtes un administrateur de l’organisation, aucune confirmation n’est nécessaire pour accepter la propriété. En revanche, si vous êtes un collaborateur, l’ajout de l’organisation en tant que propriétaire nécessite que l’un des administrateurs accepte la propriété.

## <a name="publishing-packages"></a>Publication de packages

Vous pouvez publier des packages dans une organisation comme vous le faites dans un compte d’utilisateur : en chargeant le package directement sur NuGet.org ou en envoyant (push) le package à l’aide des commandes CLI `nuget push` ou `dotnet nuget push`.

### <a name="uploading-packages"></a>Charger des packages

Quand vous chargez un nouveau package directement sur la page [Charger sur NuGet.org](https://www.nuget.org/packages/manage/upload), vous attribuez la propriété du package à un compte d’utilisateur ou d’organisation :

![Charger un package avec l’option du compte](media/org-upload-option.png)

### <a name="using-api-keys"></a>Utiliser des clés API

Pour envoyer (push) un package à l’aide des commandes CLI `nuget push` ou `dotnet nuget push`, vous devez préalablement obtenir la clé API dont ces commandes ont besoin. Pour plus d’informations, consultez [Publier un package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Quand vous créez une clé API, sélectionnez l’organisation appropriée dans le menu déroulant **Propriétaire du package**. Chaque clé API que vous créez s’applique uniquement à l’organisation choisie :

![Clé API avec l’option du compte](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Supprimer une organisation

En tant qu’utilisateur, vous pouvez vous retirer d’une organisation en sélectionnant le bouton **X** à côté de votre appartenance à l’organisation :

![Retrait d’un compte d’utilisateur d’une organisation](media/org-remove-self-option.png)

Les administrateurs peuvent retirer n’importe quel membre de l’organisation, y compris les autres administrateurs. Si vous êtes le seul administrateur d’une organisation, vous ne pouvez pas vous retirer, sauf si vous ajoutez un autre membre comme administrateur.

### <a name="deleting-an-organization-account"></a>Supprimer un compte d’organisation

Vous pouvez supprimer un compte d’organisation en cliquant sur le bouton **Supprimer** figurant dans la page de votre organisation.

![Supprimer une organisation](media/org-delete-option.png)

Pour supprimer l’organisation, vous devez confirmer l’opération en cliquant sur le bouton de confirmation **Supprimer l’organisation**.
