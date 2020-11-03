---
title: Vue d’ensemble de l’API du serveur NuGet
description: L’API serveur NuGet est un ensemble de points de terminaison HTTP qui peuvent être utilisés pour télécharger des packages, récupérer des métadonnées, publier de nouveaux packages, etc.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237807"
---
# <a name="nuget-server-api"></a>API du serveur NuGet

L’API serveur NuGet est un ensemble de points de terminaison HTTP qui peuvent être utilisés pour télécharger des packages, récupérer des métadonnées, publier de nouveaux packages et effectuer la plupart des autres opérations disponibles dans les clients NuGet officiels.

Cette API est utilisée par le client NuGet dans Visual Studio, nuget.exe et l’interface CLI .NET pour effectuer des opérations NuGet telles que, effectuer une [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) recherche dans l’interface utilisateur de Visual Studio, et [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md) .

Remarque dans certains cas, nuget.org a des exigences supplémentaires qui ne sont pas appliquées par d’autres sources de package. Ces différences sont documentées par les [protocoles NuGet.org](nuget-protocols.md).

Pour une énumération simple et le téléchargement des versions nuget.exe disponibles, consultez la [tools.jssur](tools-json.md) le point de terminaison.

## <a name="service-index"></a>Index de service

Le point d’entrée de l’API est un document JSON dans un emplacement bien connu. Ce document est appelé « **index de service** ». L’emplacement de l’index de service pour nuget.org est `https://api.nuget.org/v3/index.json` .

Ce document JSON contient une liste de *ressources* qui fournissent différentes fonctionnalités et remplissent différents cas d’usage.

Les clients qui prennent en charge l’API doivent accepter une ou plusieurs de ces URL d’index de service comme moyen de se connecter aux sources de package respectives.

Pour plus d’informations sur l’index de service, consultez la [référence de son API](service-index.md).

## <a name="versioning"></a>Contrôle de version

L’API est la version 3 du protocole HTTP de NuGet. Ce protocole est parfois appelé « API V3 ». Ces documents de référence feront référence à cette version du protocole simplement comme « l’API ».

La version du schéma d’index de service est indiquée par la `version` propriété dans l’index de service. L’API impose que la chaîne de version ait un numéro de version principale de `3` . À mesure que des modifications sans rupture sont apportées au schéma d’index de service, la version mineure de la chaîne de version est augmentée.

Les clients plus anciens (par exemple, nuget.exe 2. x) ne prennent pas en charge l’API V3 et ne prennent en charge que l’ancienne API v2, qui n’est pas documentée ici.

L’API NuGet v3 est nommée comme telle, car il s’agit du successeur de l’API v2, qui était le protocole OData implémenté par la version 2. x du client officiel NuGet. L’API V3 était d’abord prise en charge par la version 3,0 du client officiel NuGet. il s’agit toujours de la dernière version de protocole prise en charge par le client NuGet, 4,0 et on. 

Des modifications de protocole sans rupture ont été apportées à l’API depuis sa première publication.

## <a name="resources-and-schema"></a>Ressources et schéma

L' **index de service** décrit une variété de ressources. L’ensemble actuel des ressources prises en charge est le suivant :

Nom de la ressource                                                        | Obligatoire | Description
-------------------------------------------------------------------- | -------- | -----------
[Catalogue](catalog-resource.md)                                       | non       | Enregistrement complet de tous les événements de package.
[PackageBaseAddress](package-base-address-resource.md)               | yes      | Obtient le contenu du package (. nupkg).
[PackageDetailsUriTemplate](package-details-template-resource.md)    | non       | Construisez une URL pour accéder à une page Web Détails du package.
[PackagePublish](package-publish-resource.md)                        | yes      | Packages push et Delete (ou annulation de la liste).
[RegistrationsBaseUrl](registration-base-url-resource.md)            | yes      | Obtient les métadonnées du package.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | non       | Construisez une URL pour accéder à une page Web de rapport abus.
[RepositorySignatures](repository-signatures-resource.md)            | non       | Obtenir les certificats utilisés pour la signature du dépôt.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | non       | Détection des ID de package et des versions par sous-chaîne.
[SearchQueryService](search-query-service-resource.md)               | yes      | Filtrez et recherchez des packages par mot clé.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | non       | Envoyer des packages de symboles.

En général, toutes les données non binaires retournées par une ressource d’API sont sérialisées à l’aide de JSON. Le schéma de réponse retourné par chaque ressource dans l’index de service est défini individuellement pour cette ressource. Pour plus d’informations sur chaque ressource, consultez les rubriques indiquées ci-dessus.

À l’avenir, à mesure que le protocole évolue, de nouvelles propriétés peuvent être ajoutées aux réponses JSON. Pour que le client soit à l’avenir, l’implémentation ne doit pas supposer que le schéma de réponse est final et ne peut pas inclure de données supplémentaires. Toutes les propriétés que l’implémentation ne comprend pas doivent être ignorées.

> [!Note]
> Lorsqu’une source n’implémente `SearchAutocompleteService` aucun comportement de saisie semi-automatique doit être désactivée normalement. Lorsque `ReportAbuseUriTemplate` n’est pas implémenté, le client NuGet officiel revient à l’URL d’abus des rapports de NuGet. org (suivie par [NuGet/4924](https://github.com/NuGet/Home/issues/4924)). D’autres clients peuvent choisir de ne pas afficher une URL d’abus de rapport à l’utilisateur.

### <a name="undocumented-resources-on-nugetorg"></a>Ressources non documentées sur nuget.org

L’index du service v3 sur nuget.org contient des ressources qui ne sont pas documentées ci-dessus. Il existe plusieurs raisons pour lesquelles il n’est pas possible de documenter une ressource.

Tout d’abord, nous ne documentons pas les ressources utilisées en tant que détail d’implémentation de nuget.org. Le se `SearchGalleryQueryService` trouve dans cette catégorie. [NuGetGallery](https://github.com/NuGet/NuGetGallery) utilise cette ressource pour déléguer certaines requêtes v2 (OData) à notre index de recherche au lieu d’utiliser la base de données. Cette ressource a été introduite pour des raisons d’évolutivité et n’est pas destinée à un usage externe.

Deuxièmement, nous ne documentons pas les ressources qui ne sont jamais fournies dans une version RTM du client officiel.
`PackageDisplayMetadataUriTemplate` et `PackageVersionDisplayMetadataUriTemplate` appartiennent à cette catégorie.

Troisièmement, nous ne documentons pas les ressources qui sont étroitement couplées avec le protocole v2, qui lui-même est intentionnellement non documenté. La `LegacyGallery` ressource appartient à cette catégorie. Cette ressource permet à un index de service v3 de pointer vers une URL source v2 correspondante. Cette ressource prend en charge `nuget.exe list` .

Si une ressource n’est pas documentée ici, nous vous recommandons *vivement* de ne pas dépendre de celle-ci. Nous pouvons supprimer ou modifier le comportement de ces ressources non documentées, ce qui pourrait perturber votre implémentation de manière inattendue.

## <a name="timestamps"></a>Horodatages

Tous les horodateurs retournés par l’API sont au format UTC ou sont spécifiés à l’aide d’une représentation [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) . 

## <a name="http-methods"></a>Méthodes HTTP

Verbe   | Utilisez
------ | -----------
GET    | Effectue une opération en lecture seule, en général la récupération des données.
TÊTE   | Récupère les en-têtes de réponse pour la `GET` requête correspondante.
PUT    | Crée une ressource qui n’existe pas ou, si elle existe, la met à jour. Certaines ressources peuvent ne pas prendre en charge la mise à jour.
Suppression | Supprime ou déliste une ressource.

## <a name="http-status-codes"></a>Codes d’état HTTP

Code | Description
---- | -----
200  | La réussite est un corps de réponse.
201  | Réussite, et la ressource a été créée.
202  | Réussite, la demande a été acceptée, mais un travail peut encore être incomplet et terminé de façon asynchrone.
204  | Opération réussie, mais il n’existe pas de corps de réponse.
301  | Redirection permanente.
302  | Une redirection temporaire.
400  | Les paramètres dans l’URL ou dans le corps de la demande ne sont pas valides.
401  | Les informations d’identification fournies ne sont pas valides.
403  | L’action n’est pas autorisée étant donné les informations d’identification fournies.
404  | La ressource demandée n’existe pas.
409  | La demande est en conflit avec une ressource existante.
500  | Le service a rencontré une erreur inattendue.
503  | Le service est temporairement indisponible.

Toutes les `GET` demandes adressées à un point de terminaison d’API peuvent retourner une redirection http (301 ou 302). Les clients doivent gérer correctement ces redirections en observant l' `Location` en-tête et en émettant une suivante `GET` . La documentation relative à des points de terminaison spécifiques n’appellera pas explicitement l’endroit où les redirections peuvent être utilisées.

Dans le cas d’un code d’état de niveau 500, le client peut implémenter un mécanisme de nouvelle tentative raisonnable. Le client NuGet officiel effectue une nouvelle tentative trois fois lorsqu’il rencontre un code d’état de niveau 500 ou une erreur TCP/DNS.

## <a name="http-request-headers"></a>En-têtes de requête HTTP

Nom                     | Description
------------------------ | -----------
X-NuGet-ApiKey           | Requis pour l’envoi et la suppression, consultez la [ `PackagePublish` ressource](package-publish-resource.md)
X-NuGet-client-version   | **Déconseillé** et remplacé par `X-NuGet-Protocol-Version`
X-NuGet-Protocol-version | Obligatoire dans certains cas uniquement sur nuget.org, consultez [protocoles NuGet.org](NuGet-Protocols.md)
X-NuGet-session-ID       | *Facultatif* . Les clients NuGet v 4.7 + identifient les requêtes HTTP qui font partie de la même session cliente NuGet.

Le `X-NuGet-Session-Id` n’a qu’une seule valeur pour toutes les opérations liées à une restauration unique dans `PackageReference` . Pour d’autres scénarios tels que la saisie semi-automatique et `packages.config` la restauration, il peut y avoir plusieurs ID de session différents en raison de la façon dont le code est pondéré.

## <a name="authentication"></a>Authentification

L’authentification est laissée à l’implémentation de la source du package à définir. Pour nuget.org, seule la `PackagePublish` ressource requiert une authentification via un en-tête de clé API spécial. Pour plus d’informations, consultez la [ `PackagePublish` ressource](package-publish-resource.md) .
