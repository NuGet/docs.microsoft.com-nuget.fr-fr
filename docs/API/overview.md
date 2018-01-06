---
title: "Vue d’ensemble, NuGet API | Documents Microsoft"
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
ms.technology: 
ms.assetid: 8c81f1ac-18c7-44d1-b2e3-584fe85dee6f
description: "L’API de NuGet est un ensemble de points de terminaison HTTP qui peut être utilisé pour télécharger les packages, extraire les métadonnées, publier des nouveaux packages, etc."
keywords: "API de NuGet V3, API V2 de NuGet, NuGet JSON, API d’inscription de NuGet, conteneur plat de NuGet API, NuGet nupkg API, API de métadonnées NuGet, API de recherche NuGet, push de NuGet API, NuGe publier des API, NuGet supprimer API, NuGet retirer de la liste API, protocole de NuGet"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 05ed17f12f413d29d97a253d7d55f154d4910834
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-api"></a>NuGet API

L’API de NuGet est un ensemble de points de terminaison HTTP qui peut être utilisé pour télécharger les packages, extraire les métadonnées, publier les nouveaux packages et effectuer la plupart des opérations disponibles dans les clients NuGet officielles.

Cette API est utilisée par le client de NuGet dans Visual Studio et l’interface CLI .NET nuget.exe pour effectuer les opérations de NuGet [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), recherche dans l’interface utilisateur de Visual Studio, et [ `nuget.exe push` ](../tools/cli-ref-push.md).

Notez dans certains cas, nuget.org a des exigences supplémentaires qui ne sont pas appliquées par d’autres sources de package. Ces différences sont documentées par les [nuget.org protocoles](nuget-protocols.md).

## <a name="service-index"></a>Index de service

Le point d’entrée pour l’API est un document JSON dans un emplacement connu. Ce document est appelé le **index service**.
L’emplacement de l’index de service pour nuget.org est `https://api.nuget.org/v3/index.json`.

Ce document JSON contient une liste de *ressources* qui fournissent des fonctionnalités différentes et répondre aux différents cas d’usage.

Les clients qui prennent en charge l’API doivent accepter un ou plusieurs de ces index URL de service comme moyen de se connecter aux sources de package correspondant.

Pour plus d’informations sur l’index de service, consultez [sa référence de l’API](service-index.md).

## <a name="versioning"></a>Gestion de version

L’API est la version 3 du protocole HTTP de NuGet. Ce protocole est parfois appelée « l’API V3. » Ces documents de référence fait référence à cette version du protocole simplement comme « API. »

La version de schéma d’index service est indiquée par le `version` propriété dans l’index de service. L’API exige qu’un numéro de version principale de la chaîne de version `3`. Comme les modifications sans rupture sont apportées au schéma d’index de service, version mineure de la chaîne version augmente.

Les clients plus anciens (tels que nuget.exe 2.x) ne pas prendre en charge l’API V3 et prennent uniquement en charge l’API V2 plus anciens, ce qui n’est pas documentée ici.

L’API de V3 NuGet est nommé en tant que tel, car il est le successeur de l’API V2, ce qui a été le protocole basé sur OData est implémenté par la version 2.x du client de NuGet officielle. L’API V3 a été tout d’abord pris en charge par la version 3.0 du client de NuGet officiel et est toujours la version de la dernière version majeure protocole pris en charge par le client de NuGet, 4.0 sur. 

Modifications des protocoles sans rupture ont été apportées à l’API depuis sa première version.

## <a name="resources-and-schema"></a>Ressources et schéma

Le **index service** décrit les différentes ressources. L’ensemble actuel de ressources prises en charge sont les suivantes :

Nom de la ressource                                                          | Obligatoire | Description
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | oui      | Push et supprimer ou retirer de la liste packages.
[`SearchQueryService`](search-query-service-resource.md)               | oui      | Filtrer et rechercher des packages par mot clé.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | oui      | Obtenir les métadonnées du package.
[`PackageBaseAddress`](package-base-address-resource.md)               | oui      | Obtenir le contenu du package (.nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Non       | Découvrir les ID de package et les versions à la sous-chaîne.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Non       | Construire une URL pour accéder à une page web de « signaler un abus ».
[`Catalog`](catalog-resource.md)                                       | Non       | Enregistrement complet de tous les événements du package.

En règle générale, toutes les données non binaires renvoyées par une ressource d’API sont sérialisées à l’aide de JSON. Le schéma de réponse renvoyé par chaque ressource dans l’index de service est défini individuellement pour cette ressource. Pour plus d’informations sur chaque ressource, consultez les rubriques répertoriées ci-dessus.

> [!Note]
> Lorsqu’une source n’implémente pas `SearchAutocompleteService` tout comportement de saisie semi-automatique doit être désactivé en douceur. Lorsque `ReportAbuseUriTemplate` n’est pas implémentée, l’officiel revient de client de NuGet à nuget.org abus URL de rapport (suivies par [NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924)). Les autres clients peuvent se tourner simplement ne pas afficher une URL d’abus de rapports à l’utilisateur.

## <a name="timestamps"></a>Horodatages

Tous les horodatages renvoyés par l’API de format UTC ou sont définis à l’aide de [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) représentation. 

## <a name="http-methods"></a>Méthodes HTTP

Verbe   | Utilisez
------ | -----------
GET    | Effectue une opération en lecture seule, en général, la récupération de données.
HEAD   | Extrait les en-têtes de réponse correspondant `GET` demande.
PUT    | Crée une ressource qui n’existe pas ou, s’il n’existe pas, la mise à jour. Certaines ressources ne peuvent pas en charge de mise à jour.
SUPPR | Supprime ou unlists une ressource.

## <a name="http-status-codes"></a>Codes d’état HTTP

Code | Description
---- | -----
200  | Cas de réussite, et qu’il existe un corps de réponse.
201  | Succès et que la ressource a été créé.
202  | Cas de réussite, la demande a été acceptée, mais certaines tâches peuvent toujours être incomplet et terminées en mode asynchrone.
204  | Cas de réussite, mais il n’existe aucun corps de réponse.
301  | Une redirection permanente.
302  | Une redirection temporaire.
400  | Les paramètres dans l’URL ou dans le corps de la demande ne sont pas valides.
401  | Les informations d’identification fournies ne sont pas valides.
403  | L’action n’est pas autorisée fourni les informations d’identification fournies.
404  | La ressource demandée n’existe pas.
409  | Les conflits de la demande avec une ressource existante.
500  | Le service a rencontré une erreur inattendue.
503  | Le service est temporairement indisponible.

N’importe quel `GET` demande adressée à un point de terminaison API peut retourner une redirection HTTP (301 ou 302). Les clients doivent gérer correctement ces redirections en observant la `Location` en-tête et émission suivante `GET`. Documentation concernant les points de terminaison spécifiques n’appellera pas explicitement l’où redirections peuvent être utilisées.

Dans le cas d’un code d’état de niveau 500, le client peut implémenter un mécanisme de nouvelle tentative raisonnable. Les officielle NuGet tentatives trois fois lorsque n’importe quel code d’état de niveau 500 ou une erreur TCP/DNS.

## <a name="http-request-headers"></a>En-têtes de demande HTTP

Name                     | Description
------------------------ | -----------
NuGet-X-ApiKey           | Obligatoire pour par émission de données et la suppression, voir [ `PackagePublish` ressource](package-publish-resource.md)
X-NuGet-Client-Version   | **Déconseillé** et remplacée par`X-NuGet-Protocol-Version`
X-NuGet--Version de protocole | Obligatoire dans certains cas uniquement sur nuget.org, voir [nuget.org protocoles](NuGet-Protocols.md)

## <a name="authentication"></a>Authentification

L’authentification reste jusqu'à l’implémentation de source de package à définir. Pour nuget.org, uniquement le `PackagePublish` ressource requiert une authentification via un en-tête de clé API spécial. Consultez [ `PackagePublish` ressource](package-publish-resource.md) pour plus d’informations.
