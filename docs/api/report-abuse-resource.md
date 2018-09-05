---
title: Signaler un abus API NuGet, modèle d’URL
description: Le modèle d’URL de rapport abus permet aux clients d’afficher un lien Signaler un abus dans leur interface utilisateur.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549337"
---
# <a name="report-abuse-url-template"></a>Modèle d’URL de rapport un abus

Il est possible pour un client générer une URL qui peut être utilisée par l’utilisateur pour signaler un abus sur un package spécifique. Cela est utile lorsqu’une source de package souhaite activer toutes les expériences client (même 3e partie) déléguer les rapports d’abus pour la source du package.

La ressource utilisée pour la création de cette URL est la `ReportAbuseUriTemplate` ressource trouvée dans le [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` les valeurs sont utilisées :

Valeur @type                       | Notes
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | La version initiale
ReportAbuseUriTemplate/3.0.0-rc   | Alias de `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Modèle d’URL

L’URL de l’API suivante est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs.

## <a name="http-methods"></a>Méthodes HTTP

Bien que le client n’est pas destiné à effectuer des demandes à l’URL d’abus de rapports pour le compte de l’utilisateur, la page web doit prendre en charge la `GET` méthode pour autoriser une URL consultée être ouvert dans un navigateur web.

## <a name="construct-the-url"></a>Construire l’URL

Étant donné un ID de package connus et la version, l’implémentation du client permettre construire une URL utilisée pour accéder à une interface web. L’implémentation cliente doit afficher cette URL construit (ou un lien interactif) pour l’utilisateur leur permettant d’ouvrir un navigateur web à l’URL et que n’importe quel rapport abus nécessaire. L’implémentation de la forme de rapports d’abus est déterminée par l’implémentation du serveur.

La valeur de la `@id` est une chaîne d’URL contenant un jeton d’espace réservé suivant :

### <a name="url-placeholders"></a>Espace réservé d’URL

Name        | Type    | Obligatoire | Notes
----------- | ------- | -------- | -----
`{id}`      | chaîne  | Non       | L’ID de package pour signaler un abus pour
`{version}` | chaîne  | Non       | La version du package pour signaler un abus pour

Le `{id}` et `{version}` valeurs interprétée par l’implémentation de serveur doivent être de la casse et pas la casse pour que la version est normalisée.

Par exemple, modèle d’abus de nuget.org rapport ressemble à ceci :

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Si l’implémentation cliente doit afficher un lien vers le formulaire d’abus de rapport pour NuGet.Versioning 4.3.0, il serait génère l’URL suivante et fournit à l’utilisateur :

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
