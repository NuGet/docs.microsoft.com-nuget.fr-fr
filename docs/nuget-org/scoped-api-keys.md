---
title: Clés API délimitées
description: Prendre le contrôle des clés API que vous utilisez pour envoyer (push) des packages
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: a3d2504528249f3545e2eb5d9bce7713029638db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901588"
---
# <a name="scoped-api-keys"></a>Clés API délimitées

Pour faire de NuGet un environnement plus sécurisé pour la distribution de packages, vous pouvez ajouter des étendues pour prendre le contrôle des clés API.

En définissant des étendues pour vos clés API, vous pouvez mieux contrôler vos API. Vous pouvez :

- Créer plusieurs clés API délimitées pouvant être utilisées pour différents packages avec des délais d’expiration variables
- Obtenir des clés API de manière sécurisée
- Modifier des clés API existantes pour changer l’applicabilité des packages
- Actualiser ou supprimer des clés API existantes sans nuire aux opérations utilisant d’autres clés

## <a name="why-do-we-support-scoped-api-keys"></a>Pourquoi prenons-nous en charge les clés API délimitées ?

La prise en charge des étendues pour les clés API vous permet d’avoir des autorisations plus affinées. Avant, NuGet offrait une clé API unique pour un compte, ce qui présentait plusieurs inconvénients :

- **Une seule clé API pour contrôler tous les packages**. Si vous n’avez qu’une seule clé API pour gérer tous les packages, il est difficile de la partager de manière sécurisée quand plusieurs développeurs sont impliqués dans différents packages et partagent un compte d’éditeur.
- **Toutes les autorisations ou aucune**. Toute personne ayant accès à la clé API bénéficie de toutes les autorisations (publication, envoi [push] et suppression de la liste) sur les packages, ce qui n’est pas vraiment souhaitable dans un environnement composé de plusieurs équipes.
- **Point de défaillance unique**. Une seule clé API implique également un point de défaillance unique. Si la clé est compromise, tous les packages associés au compte peuvent potentiellement être compromis. L’actualisation de la clé API est le seul moyen de remédier à la fuite et d’éviter une interruption de votre workflow CI/CD. Par ailleurs, il peut arriver que vous souhaitiez révoquer l’accès à la clé API pour un individu (par exemple, quand un employé quitte l’organisation). Il n’y a aujourd’hui aucun moyen de gérer convenablement cette situation.

Avec les clés API délimitées, nous essayons de résoudre ces problèmes tout en veillant au bon fonctionnement des workflows existants.

## <a name="acquire-an-api-key"></a>Acquérir une clé API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Créer des clés API délimitées

Vous pouvez créer plusieurs clés API en fonction de vos besoins. Une clé API peut s’appliquer à un ou plusieurs packages, avoir différentes étendues qui accordent des privilèges spécifiques et être associée à une date d’expiration.

Dans l’exemple suivant, vous disposez d’une clé API nommée `Contoso service CI` qui peut être utilisée pour envoyer (push) des packages pour des packages `Contoso.Service` spécifiques. Elle est valide 365 jours. Il s’agit d’un scénario typique dans lequel différentes équipes au sein d’une même organisation travaillent sur différents packages. Les membres de l’équipe reçoivent alors la clé qui leur octroie uniquement des privilèges sur le package sur lequel ils travaillent. L’expiration sert de mécanisme pour éviter les clés obsolètes ou oubliées.

![Créer des clés API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Utiliser des modèles Glob

Si vous travaillez sur plusieurs packages et que vous avez une longue liste de packages à gérer, vous pouvez choisir d’utiliser des modèles Glob pour sélectionner plusieurs packages en même temps. Par exemple, si vous voulez accorder des étendues spécifiques à une clé pour tous les packages dont l’ID commence par `Fabrikam.Service`, vous pouvez spécifier `fabrikam.service.*` dans la zone de texte **Modèle Glob**.

![Créer des clés API-2](media/scoped-api-keys-glob-pattern.png)

L’utilisation de modèles Glob pour déterminer les autorisations de clé API s’applique également aux nouveaux packages correspondant au modèle Glob. Par exemple, si vous essayez d’envoyer (push) un nouveau package nommé `Fabrikam.Service.Framework`, vous pouvez utiliser la clé créée précédemment dans la mesure où le package correspond au modèle Glob `fabrikam.service.*`.

## <a name="obtain-api-keys-securely"></a>Obtenir des clés API de manière sécurisée

Pour des raisons de sécurité, une clé qui vient d’être créée n’est jamais affichée sur l’écran et n’est disponible qu’à l’aide du bouton **Copier**. De même, la clé n’est pas accessible une fois la page actualisée.

![Créer des clés d’API-3](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Modifier des clés API existantes

Vous pouvez également mettre à jour les autorisations et les étendues d’une clé sans changer la clé. Si vous avez une clé avec une ou plusieurs étendues spécifiques pour un seul package, vous pouvez choisir d’appliquer la ou les mêmes étendues à un ou plusieurs packages.

![Créer des clés d’API-4](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Actualiser ou supprimer des clés API existantes

Le propriétaire du compte peut choisir d’actualiser la clé, auquel cas l’autorisation (sur les packages), l’étendue et l’expiration restent les mêmes. Toutefois, une nouvelle clé est émise, rendant l’ancienne clé inutilisable. C’est utile pour gérer les clés obsolètes ou en cas de risque de fuite des clés API.

![Créer des clés API-5](media/scoped-api-keys-refresh.png)

Vous pouvez également choisir de supprimer ces clés si elles ne sont plus nécessaires. Cette opération supprime la clé et la rend inutilisable.

## <a name="faqs"></a>Foire aux questions

### <a name="what-happens-to-my-old-legacy-api-key"></a>Qu’advient-il de mon ancienne clé API (existante) ?

Votre ancienne clé API (existante) est opérationnelle et peut le rester aussi longtemps que vous le souhaitez. Toutefois, elle est supprimée au bout de 365 jours si elle n’est pas utilisée pour envoyer (push) un package. Pour plus d’informations, consultez le billet de blog traitant des [changements apportés aux clés API arrivant à expiration](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Vous ne pouvez plus actualiser cette clé. Vous devez supprimer la clé existante et créer une clé délimitée à la place.

> [!NOTE]
> Cette clé a toutes les autorisations sur tous les packages et n’expire jamais. Pensez à supprimer cette clé et à créer des clés avec des autorisations délimitées et une date d’expiration définitive.

### <a name="how-many-api-keys-can-i-create"></a>Combien de clés API puis-je créer ?

Le nombre de clés API que vous pouvez créer n’est pas limité. Cependant, nous vous conseillons de limiter le nombre de clés à un nombre raisonnable pour ne pas vous retrouver avec une grande quantité de clés obsolètes sans savoir où elles sont utilisées et par qui.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Puis-je supprimer ma clé API existante ou cesser de l’utiliser maintenant ?

Oui. Vous pouvez supprimer votre clé API existante (il est même préférable de le faire).

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Puis-je récupérer une clé API que j’ai supprimée par erreur ?

Non. Une fois une clé supprimée, il vous reste à en créer une autre. Les clés supprimées accidentellement ne peuvent pas être récupérées.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>L’ancienne clé API fonctionne-t-elle encore après l’actualisation de la clé API ?

Non. Une fois que vous actualisez une clé, une nouvelle clé est générée avec les mêmes étendue, autorisation et date d’expiration que l’ancienne. L’ancienne clé n’existe plus.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Puis-je donner plus d’autorisations à une clé API existante ?

Vous ne pouvez pas modifier son étendue, mais vous pouvez modifier la liste de packages à laquelle elle s’applique.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Comment savoir si l’une de mes clés est arrivée à expiration ou est sur le point de l’être ?

Si une clé arrive à expiration, nous vous en informons par le biais d’un message d’avertissement en haut de la page. Nous envoyons également un e-mail d’avertissement au titulaire du compte dix jours avant l’expiration de la clé afin qu’il puisse prendre les devants.