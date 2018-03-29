---
title: Signaler un abus NuGet API, modèle d’URL | Documents Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Le modèle d’URL de rapport abus permet aux clients d’afficher un lien Signaler un abus dans leur interface utilisateur.
keywords: API NuGet signaler un abus, réclamation de fichier API NuGet, modèle d’URL nuget.org rapport
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ded861e3eaf73e45b8d4bd80b96d54bfeb38e9d6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="report-abuse-url-template"></a>Modèle d’URL de rapport abus

Il est possible pour un client générer une URL qui peut être utilisée par l’utilisateur pour signaler un abus sur un package spécifique. Cela est utile lorsqu’une source de package souhaite activer toutes les expériences client (même 3e partie) déléguer les rapports d’abus à la source du package.

La ressource utilisée pour extraire le contenu du package est le `ReportAbuseUriTemplate` ressource trouvée dans le [index service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` les valeurs sont utilisées :

Valeur @type                       | Notes
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | La version initiale
ReportAbuseUriTemplate/3.0.0-rc   | Alias de `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Modèle d’URL

L’URL de l’API suivante est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs.

## <a name="http-methods"></a>Méthodes HTTP

Bien que le client n’est pas destiné à effectuer des demandes à l’URL d’abus de rapports pour le compte de l’utilisateur, la page web doit prendre en charge la `GET` méthode pour autoriser les URL où vous avez cliquée pour être ouvert dans un navigateur web.

## <a name="construct-the-url"></a>Construire l’URL

Étant donné un ID de package connus et la version, l’implémentation du client permet de construire une URL utilisée pour accéder à une interface web. L’implémentation cliente doit afficher cette URL construite (ou un lien cliquable) à l’utilisateur qui permet de les ouvrir un navigateur web à l’URL et que n’importe quel rapport abus nécessaires. L’implémentation de la forme de rapport abus est déterminée par l’implémentation du serveur.

La valeur de la `@id` est une chaîne d’URL contenant l’un des jetons d’espace réservé suivant :

### <a name="url-placeholders"></a>Espaces réservés d’URL

Name        | Type    | Obligatoire | Notes
----------- | ------- | -------- | -----
`{id}`      | chaîne  | Non       | L’ID de package pour signaler un abus pour
`{version}` | chaîne  | Non       | La version du package pour signaler un abus pour

Le `{id}` et `{version}` valeurs interprétée par l’implémentation de serveur doivent être insensible à la casse et n’ont aucune incidence si la version est normalisé.

Par exemple, le modèle d’abus nuget.org rapport ressemble à ceci :

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Si l’implémentation cliente doit afficher un lien vers le formulaire d’abus de rapport pour NuGet.Versioning 4.3.0, il génère l’URL suivante et fournir à l’utilisateur :

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
