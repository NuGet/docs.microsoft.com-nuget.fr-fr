---
title: Modèle d’URL Détails du package, API NuGet
description: Le modèle d’URL Détails du package permet aux clients d’afficher dans leur interface utilisateur un lien Web vers d’autres détails sur le package
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 1b84c6e88a56216e5747d5bc602219af6695c305
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812933"
---
# <a name="package-details-url-template"></a>Modèle d’URL Détails du package

Il est possible pour un client de créer une URL qui peut être utilisée par l’utilisateur pour afficher plus de détails sur le package dans son navigateur Web. Cela s’avère utile quand une source de package souhaite afficher des informations supplémentaires sur un package qui ne tiennent pas dans l’étendue de ce que l’application cliente NuGet affiche.

La ressource utilisée pour générer cette URL est la ressource `PackageDetailsUriTemplate` trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les valeurs de `@type` suivantes sont utilisées :

Valeur de @type                     | Remarques
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | La version initiale

## <a name="url-template"></a>Modèle d’URL

L’URL de l’API suivante est la valeur de la propriété `@id` associée à l’une des valeurs de `@type` de ressource mentionnées ci-dessus.

## <a name="http-methods"></a>Méthodes HTTP

Bien que le client ne soit pas destiné à effectuer des requêtes sur l’URL des détails du package pour le compte de l’utilisateur, la page Web doit prendre en charge la méthode `GET` pour permettre l’ouverture facile d’une URL cliquée dans un navigateur Web.

## <a name="construct-the-url"></a>Construire l’URL

Avec un ID de package connu et une version, l’implémentation cliente peut construire une URL utilisée pour accéder à une interface Web. L’implémentation du client doit afficher cette URL construite (ou un lien de clic) pour permettre à l’utilisateur d’ouvrir un navigateur Web à l’URL et d’en savoir plus sur le package. Le contenu de la page Détails du package est déterminé par l’implémentation du serveur.

L’URL doit être une URL absolue et le schéma (protocole) doit être HTTPs.

La valeur de la `@id` dans l’index de service est une chaîne d’URL contenant l’un des jetons d’espaces réservés suivants :

### <a name="url-placeholders"></a>Espaces réservés d’URL

Name        | Type    | Obligatoire | Remarques
----------- | ------- | -------- | -----
`{id}`      | string  | Non       | ID de package pour lequel obtenir des détails
`{version}` | string  | Non       | Version du package pour laquelle obtenir des détails

Le serveur doit accepter les valeurs `{id}` et `{version}` avec n’importe quelle casse. En outre, le serveur ne doit pas être sensible à la [normalisation](../concepts/package-versioning.md#normalized-version-numbers)de la version. En d’autres termes, le serveur doit accepter également les versions non normalisées.

Par exemple, le modèle de détails de package de NuGet. org ressemble à ceci :

    https://www.nuget.org/packages/{id}/{version}

Si l’implémentation du client doit afficher un lien vers les détails du package pour NuGet. version 4.3.0, elle génère l’URL suivante et la fournit à l’utilisateur :

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
