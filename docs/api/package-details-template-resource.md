---
title: Détails de l’API NuGet, modèle d’URL de package
description: Le modèle d’URL de package détails permet aux clients d’afficher dans leur interface utilisateur web lier à plus de détails de package
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638072"
---
# <a name="package-details-url-template"></a>Modèle d’URL de détails de package

Il est possible pour un client générer une URL qui peut être utilisée par l’utilisateur pour afficher plus de détails de package dans son navigateur web. Cela est utile lorsqu’une source de package souhaite afficher des informations supplémentaires sur un package qui ne correspondre pas dans la portée de ce que montre l’application cliente de NuGet.

La ressource utilisée pour la création de cette URL est la `PackageDetailsUriTemplate` ressource trouvée dans le [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` les valeurs sont utilisées :

Valeur@type                      | Notes
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | La version initiale

## <a name="url-template"></a>Modèle d’URL

L’URL de l’API suivante est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs.

## <a name="http-methods"></a>Méthodes HTTP

Bien que le client n’est pas destiné à effectuer des demandes à l’URL de détails du package pour le compte de l’utilisateur, la page web doit prendre en charge la `GET` méthode pour autoriser une URL consultée être ouvert dans un navigateur web.

## <a name="construct-the-url"></a>Construire l’URL

Étant donné un ID de package connus et la version, l’implémentation du client permettre construire une URL utilisée pour accéder à une interface web. L’implémentation cliente doit afficher cette URL construit (ou un lien interactif) pour l’utilisateur lui permettant d’ouvrir un navigateur web à l’URL et pour en savoir plus sur le package. Le contenu de la page de détails du package est déterminé par l’implémentation du serveur.

L’URL doit être une URL absolue et du modèle (protocole) doit être HTTPS.

La valeur de la `@id` dans le service d’index est une chaîne d’URL contenant un jeton d’espace réservé suivant :

### <a name="url-placeholders"></a>Espace réservé d’URL

Nom        | Type    | Obligatoire | Notes
----------- | ------- | -------- | -----
`{id}`      | string  | Non       | L’ID de package pour obtenir des détails pour
`{version}` | string  | Non       | Pour obtenir des détails pour la version du package

Le serveur doit accepter `{id}` et `{version}` valeurs avec n’importe quel boîtier. En outre, le serveur ne doit pas être sensible aux indique si la version est [normalisée](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers). En d’autres termes, le serveur doit accepter également accepter des versions non normalisée.

Par exemple, le modèle de détails du package nuget.org se présente comme suit :

    https://www.nuget.org/packages/{id}/{version}

Si l’implémentation cliente doit afficher un lien vers les détails du package pour NuGet.Versioning 4.3.0, il serait génère l’URL suivante et fournit à l’utilisateur :

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
