---
title: Vue d’ensemble de l’API NuGet
description: L’API NuGet est un ensemble de points de terminaison HTTP qui peut être utilisé pour télécharger les packages, d’extraire des métadonnées, de publier de nouveaux packages, etc.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: bb15b4decef104f1aefe37fd18f3358181a848af
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637660"
---
# <a name="nuget-api"></a>API NuGet

L’API NuGet est un ensemble de points de terminaison HTTP qui peut être utilisé pour télécharger les packages, extraire des métadonnées, publier de nouveaux packages et effectuer la plupart des opérations disponibles dans les clients NuGet officielles.

Cette API est utilisée par le client NuGet dans Visual Studio, nuget.exe et l’interface CLI .NET pour effectuer des opérations NuGet comme [ `dotnet restore` ](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), recherche dans l’interface utilisateur de Visual Studio, et [ `nuget.exe push` ](../tools/cli-ref-push.md).

Notez dans certains cas, nuget.org a des spécifications supplémentaires qui ne sont pas appliquées par d’autres sources de package. Ces différences sont documentées par le [protocoles nuget.org](nuget-protocols.md).

Pour une énumération simple et le téléchargement des versions de nuget.exe disponibles, consultez le [tools.json](tools-json.md) point de terminaison.

## <a name="service-index"></a>Index de service

Le point d’entrée pour l’API est un document JSON dans un emplacement bien connu. Ce document est appelé le **index de service**. L’emplacement de l’index de service pour nuget.org est `https://api.nuget.org/v3/index.json`.

Ce document JSON contient une liste de *ressources* qui fournissent des fonctionnalités différentes et répondre aux différents cas d’usage.

Les clients qui prennent en charge de l’API doivent accepter un ou plusieurs de ces URL du service d’index comme moyen de se connecter aux sources de package correspondant.

Pour plus d’informations sur l’index de service, consultez [sa référence d’API](service-index.md).

## <a name="versioning"></a>Gestion de version

L’API est la version 3 du protocole HTTP de NuGet. Ce protocole est parfois appelé « l’API V3 ». Ces documents de référence fait référence à cette version du protocole simplement en tant que « l’API ».

La version de schéma d’index service est indiquée par le `version` propriété dans l’index de service. L’API impose que la chaîne de version a un numéro de version principale de `3`. Quand des modifications sans rupture sont apportées au schéma d’index de service, version mineure de la chaîne de version sera augmentée.

Les clients plus anciens (tels que nuget.exe 2.x) ne sont pas en charge les API V3 et prennent uniquement en charge l’ancienne API V2, qui n’est pas documenté ici.

L’API V3 de NuGet est nommé en tant que tel, car il est le successeur de l’API V2, qui était le protocole basé sur OData est implémenté par la version 2.x du client NuGet officiel. L’API V3 a été tout d’abord pris en charge par la version 3.0 du client NuGet officiel et est toujours la version de la dernière version majeure protocole pris en charge par le client NuGet, 4.0 et sur. 

Modifications des protocoles sans rupture ont été apportées à l’API depuis sa commercialisation tout d’abord.

## <a name="resources-and-schema"></a>Ressources et schéma

Le **index de service** décrit une variété de ressources. L’ensemble actuel des ressources prises en charge sont les suivantes :

Nom de la ressource                                                        | Obligatoire | Description
-------------------------------------------------------------------- | -------- | -----------
[Catalogue](catalog-resource.md)                                       | Non       | Enregistrement complet de tous les événements de package.
[PackageBaseAddress](package-base-address-resource.md)               | oui      | Obtenir le contenu du package (fichier .nupkg).
[PackageDetailsUriTemplate](package-details-template-resource.md)    | Non       | Construire une URL pour accéder à une page web de détails du package.
[PackagePublish](package-publish-resource.md)                        | oui      | Push et supprimer ou retirer de la liste packages.
[RegistrationsBaseUrl](registration-base-url-resource.md)            | oui      | Obtenir les métadonnées de package.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | Non       | Construire une URL pour accéder à une page web d’abus état.
[RepositorySignatures](repository-signatures-resource.md)            | Non       | Obtenir les certificats utilisés pour la signature du référentiel.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | Non       | Découvrir les ID de package et les versions à la sous-chaîne.
[SearchQueryService](search-query-service-resource.md)               | oui      | Filtrer et rechercher des packages par mot clé.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | Non       | Envoyez des packages de symboles.

En règle générale, toutes les données non binaires renvoyées par une ressource d’API sont sérialisées à l’aide de JSON. Le schéma de réponse retourné par chaque ressource dans l’index de service est défini individuellement pour cette ressource. Pour plus d’informations sur chaque ressource, consultez les rubriques répertoriées ci-dessus.

À l’avenir, comme le protocole évolue, les nouvelles propriétés peuvent être ajoutées à réponses JSON. Pour le client puisse être durable, l’implémentation ne doit pas supposer que le schéma de réponse est définitive et ne peut pas inclure les données supplémentaires. L’implémentation ne comprend pas toutes les propriétés doivent être ignorées.

> [!Note]
> Quand une source n’implémente pas `SearchAutocompleteService` tout comportement de saisie semi-automatique doit être désactivé en douceur. Lorsque `ReportAbuseUriTemplate` n’est pas implémentée, la repasse de client NuGet officiel à nuget.org signaler un abus URL (suivies par [NuGet/accueil #4924](https://github.com/NuGet/Home/issues/4924)). Autres clients peuvent choisir de simplement afficher une URL d’abus de rapport à l’utilisateur.

### <a name="undocumented-resources-on-nugetorg"></a>Ressources non documentées sur nuget.org

L’index de service V3 sur nuget.org dispose de ressources qui ne sont pas documentés ci-dessus. Il existe quelques raisons pour documenter ne pas une ressource.

Tout d’abord, nous n’aborderons pas les ressources utilisées comme un détail d’implémentation de nuget.org. Le `SearchGalleryQueryService` fait partie de cette catégorie. [NuGetGallery](https://github.com/NuGet/NuGetGallery) utilise cette ressource pour déléguer certaines V2 (OData) des requêtes à notre index de recherche au lieu d’utiliser la base de données. Cette ressource a été introduite pour des raisons d’évolutivité et n’est pas destinée à un usage externe.

Ensuite, nous n’aborderons pas les ressources jamais fourni dans une version RTM du client officiel.
`PackageDisplayMetadataUriTemplate` et `PackageVersionDisplayMetadataUriTemplate` appartiennent à cette catégorie.

Troisièmement, nous n’aborderons pas les ressources qui sont étroitement couplées avec le protocole V2, qui elle-même est intentionnellement non documentée. Le `LegacyGallery` ressource fait partie de cette catégorie. Cette ressource permet à un index de service V3 pointer vers une URL de source correspondante V2. Cette ressource prend en charge la `nuget.exe list`.

Si une ressource n’est pas documentée ici, nous *fortement* est recommandé que vous n’établissez pas de dépendance sur ces derniers. Nous pouvons supprimer ou modifier le comportement de ces ressources non documentés qui endommage votre implémentation de façon inattendue.

## <a name="timestamps"></a>Horodatages

Tous les horodatages renvoyés par l’API sont au format UTC ou contraire à l’aide de [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) représentation. 

## <a name="http-methods"></a>Méthodes HTTP

Verbe   | Utilisez
------ | -----------
GET    | Effectue une opération en lecture seule, généralement récupérer des données.
HEAD   | Extrait les en-têtes de réponse correspondants `GET` demande.
PUT    | Crée une ressource qui n’existe pas ou, s’il n’existe pas, il le met à jour. Certaines ressources ne peuvent pas en charge de mise à jour.
SUPPR | Supprime ou retire une ressource.

## <a name="http-status-codes"></a>Codes d’état HTTP

Code | Description
---- | -----
200  | Cas de réussite, et qu’il existe un corps de réponse.
201  | Réussite et que la ressource a été créé.
202  | Cas de réussite, la demande a été acceptée, mais un travail peut toujours être incomplet et terminée en mode asynchrone.
204  | Cas de réussite, mais il n’existe aucun corps de réponse.
301  | Une redirection permanente.
302  | Une redirection temporaire.
400  | Les paramètres dans l’URL ou dans le corps de demande ne sont pas valides.
401  | Les informations d’identification fournies ne sont pas valides.
403  | L’action n’est pas autorisée étant donné les informations d’identification fournies.
404  | La ressource demandée n’existe pas.
409  | Les conflits de la demande avec une ressource existante.
500  | Le service a rencontré une erreur inattendue.
503  | Le service est temporairement indisponible.

N’importe quel `GET` demande adressée à un point de terminaison d’API peut-être retourner une redirection HTTP (301 ou 302). Les clients doivent gérer correctement ces redirections en observant le `Location` en-tête et émettre une ultérieure `GET`. Documentation concernant les points de terminaison spécifiques n’appelle pas explicitement l’où redirections peuvent être utilisées.

Dans le cas d’un code d’état de niveau 500, le client peut implémenter un mécanisme de nouvelle tentative raisonnable. Le client de NuGet officielle retente trois fois lorsqu’il rencontre des n’importe quel code d’état de niveau 500 ou une erreur TCP/DNS.

## <a name="http-request-headers"></a>En-têtes de requête HTTP

Nom                     | Description
------------------------ | -----------
X-NuGet-ApiKey           | Obligatoire pour les push et delete, consultez [ `PackagePublish` ressource](package-publish-resource.md)
X-NuGet-Client-Version   | **Déconseillé** et remplacée par `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Obligatoire dans certains cas que sur nuget.org, voir [protocoles nuget.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Facultatif*. NuGet clients version 4.7 + identifient les requêtes HTTP qui font partie de la même session de client NuGet.

Le `X-NuGet-Session-Id` a une valeur unique pour toutes les opérations liées à une restauration unique dans `PackageReference`. Pour d’autres scénarios tels que la saisie semi-automatique et `packages.config` restauration qu’il peut y avoir plusieurs autre session ID en raison de la façon dont le code est pris en compte.

## <a name="authentication"></a>Authentification

L’authentification est laissée à l’implémentation de source de package pour définir. Pour nuget.org, uniquement le `PackagePublish` ressource requiert l’authentification via un en-tête de clé API spécial. Consultez [ `PackagePublish` ressource](package-publish-resource.md) pour plus d’informations.
