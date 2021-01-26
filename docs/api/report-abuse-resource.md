---
title: Modèle d’URL du rapport d’abus, API NuGet
description: Le modèle URL du rapport d’abus permet aux clients d’afficher un lien signaler un abus dans leur interface utilisateur.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775233"
---
# <a name="report-abuse-url-template"></a>Modèle d’URL d’abus de rapport

Il est possible pour un client de créer une URL qui peut être utilisée par l’utilisateur pour signaler un abus sur un package spécifique. Cela est utile quand une source de package souhaite activer toutes les expériences client (même tierces) pour déléguer des rapports d’abus à la source du package.

La ressource utilisée pour générer cette URL est la `ReportAbuseUriTemplate` ressource trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Contrôle de version

Les `@type` valeurs suivantes sont utilisées :

Valeur @type                       | Notes
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-bêta | La version initiale
ReportAbuseUriTemplate/3.0.0-RC   | Alias de `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL template

L’URL de l’API suivante est la valeur de la `@id` propriété associée à l’une des valeurs de ressource mentionnées ci-dessus `@type` .

## <a name="http-methods"></a>Méthodes HTTP

Bien que le client ne soit pas destiné à effectuer des demandes à l’URL d’abus de rapport pour le compte de l’utilisateur, la page Web doit prendre en charge la `GET` méthode pour permettre l’ouverture facile d’une URL cliquée dans un navigateur Web.

## <a name="construct-the-url"></a>Construire l’URL

Avec un ID de package connu et une version, l’implémentation cliente peut construire une URL utilisée pour accéder à une interface Web. L’implémentation du client doit afficher cette URL construite (ou un lien de clic) pour permettre à l’utilisateur d’ouvrir un navigateur Web à l’URL et de faire tout rapport d’abus nécessaire. L’implémentation du formulaire de rapport d’abus est déterminée par l’implémentation du serveur.

La valeur de `@id` est une chaîne d’URL contenant l’un des jetons d’espace réservé suivants :

### <a name="url-placeholders"></a>Espaces réservés d’URL

Nom        | Type    | Obligatoire | Notes
----------- | ------- | -------- | -----
`{id}`      | string  | non       | ID de package pour signaler un abus pour
`{version}` | string  | non       | Version du package pour signaler un abus pour

Les `{id}` `{version}` valeurs et interprétées par l’implémentation de serveur doivent être insensibles à la casse et ne pas être sensibles au fait que la version est normalisée ou non.

Par exemple, le modèle de rapport d’abus de NuGet. org ressemble à ceci :

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

Si l’implémentation du client doit afficher un lien vers le formulaire signaler un abus pour NuGet. version 4.3.0, elle génère l’URL suivante et la fournit à l’utilisateur :

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
