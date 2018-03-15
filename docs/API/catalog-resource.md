---
title: Catalogue, les API NuGet V3 | Documents Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Le catalogue est un index de tous les packages créés et supprimés sur nuget.org."
keywords: "Catalogue de NuGet V3 API, le journal des transactions nuget.org répliquer nuget.org, clone nuget.org, un enregistrement en mode append-only de nuget.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: be30b21d488c323c439a59fff290a95adaefd902
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="catalog"></a>Catalogue

Le **catalogue** est une ressource qui enregistre toutes les opérations de package sur une source de package, telles que les créations et suppressions. La ressource de catalogue a la `Catalog` de type dans le [index service](service-index.md).

> [!Note]
> Étant donné que le catalogue n’est pas utilisé par le client NuGet officiels, pas toutes les sources de package implémentent le catalogue.

> [!Note]
> Actuellement, le catalogue nuget.org n’est pas disponible en Chine. Pour plus d’informations, consultez [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` valeur est utilisée :

Valeur @type   | Notes
------------- | -----
Catalog/3.0.0 | La version initiale

## <a name="base-url"></a>URL de base

L’URL de point d’entrée pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeurs. Cette rubrique utilise l’URL de l’espace réservé `{@id}`.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvés dans la prise en charge de la ressource catalogue uniquement les méthodes HTTP `GET` et `HEAD`.

## <a name="catalog-index"></a>Index du catalogue

L’index du catalogue est un document dans un emplacement connu qui contient une liste d’éléments de catalogue, classés par ordre chronologique. Il est le point d’entrée de la ressource de catalogue.

L’index se compose de pages de catalogue. Chaque page de catalogue contient des éléments de catalogue. Chaque élément de catalogue représente un événement concernant un package unique à un point dans le temps. Un élément de catalogue peut représenter un package qui a été créé, non répertoriées, remis ou supprimés à partir de la source du package. En traitant les éléments de catalogue dans l’ordre chronologique, le client peut générer une vue à jour de chaque package existe sur la source du package V3.

En bref, les objets BLOB de catalogue ont la structure hiérarchique suivante :

- **Index**: le point d’entrée pour le catalogue.
- **Page**: un regroupement d’éléments de catalogue.
- **Feuille**: un document qui représente un élément de catalogue qui est un instantané de l’état d’un package unique.

Chaque objet du catalogue a une propriété appelée le `commitTimeStamp` représentant lorsque l’élément a été ajouté au catalogue. Les éléments de catalogue sont ajoutés à une page du catalogue dans des lots est validée. Tous les éléments de catalogue dans la même validation ont le même horodateur de validation (`commitTimeStamp`) et ID de validation (`commitId`). Les éléments de catalogue placés dans la même validation représentent des événements survenus le même point dans le temps sur la source du package. Il n’existe aucun classement au sein d’une validation du catalogue.

Étant donné que chaque ID de package et la version soient unique, il y aura jamais plus d’un élément de catalogue dans une instruction commit. Cela garantit que les éléments de catalogue pour un package unique peuvent toujours être sans ambiguïté classées en ce qui concerne l’horodateur de validation.

Il ne jamais plus d’une validation dans le catalogue par `commitTimeStamp`. En d’autres termes, le `commitId` est redondant avec le `commitTimeStamp`.

Contrairement à la [ressource de métadonnées du package](registration-base-url-resource.md), qui est indexé par ID de package, le catalogue est indexée (et requêtables) uniquement par heure.

Éléments de catalogue sont toujours ajoutées au catalogue dans un ordre chronologique monolithique. Cela signifie que si une validation du catalogue est ajoutée au moment de X, aucune validation du catalogue n’est toujours ajoutée avec un temps inférieur ou égal à X.

La requête suivante extrait l’index du catalogue.

    GET {@id}

L’index du catalogue est un document JSON qui contient un objet avec les propriétés suivantes :

Name            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
commitId        | chaîne           | oui      | Un ID unique associé à la dernière validation
commitTimeStamp | chaîne           | oui      | Un horodateur de la dernière validation
count           | entiers          | oui      | Le nombre de pages dans l’index
Éléments           | Tableau d’objets | oui      | Un tableau d’objets, chaque objet qui représente une page

Chaque élément dans le `items` tableau est un objet avec le minimum de certains détails sur chaque page. Ces objets de la page ne contiennent pas les feuilles de catalogue (éléments). L’ordre des éléments dans ce tableau n’est pas défini. Pages peuvent être triées par le client dans la mémoire à l’aide de leurs `commitTimeStamp` propriété.

Comme les nouvelles pages sont ajoutées, les `count` sera incrémenté et de nouveaux objets seront affichent dans le `items` tableau.

Comme les éléments sont ajoutés à, l’index du catalogue `commitId` change et la `commitTimeStamp` augmente. Ces deux propriétés sont essentiellement un résumé sur la page tous les `commitId` et `commitTimeStamp` des valeurs dans le `items` tableau.

### <a name="catalog-page-object-in-the-index"></a>Objet page dans l’index du catalogue

Les objets de la page catalogue se trouvant dans l’index de catalogue `items` propriété ont les propriétés suivantes :

Name            | Type    | Obligatoire | Notes
--------------- | ------- | -------- | -----
@id             | chaîne  | oui      | L’URL de page de catalogue fetch
commitId        | chaîne  | oui      | Un ID unique associé à la validation la plus récente de cette page
commitTimeStamp | chaîne  | oui      | Un horodateur de la validation la plus récente de cette page
count           | entiers | oui      | Le nombre d’éléments dans la page catalogue

Contrairement à la [ressource de métadonnées du package](registration-base-url-resource.md) qui, dans certains cas incorporations laisse dans l’index, les feuilles de catalogue ne sont jamais incorporées dans l’index et doivent toujours être extraite à l’aide de la page `@id` URL.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Page du catalogue

La page de catalogue est une collection d’éléments de catalogue. Il s’agit d’un document extrait à l’aide d’une de la `@id` valeurs trouvées dans l’index du catalogue. L’URL vers une page de catalogue n’est pas destinée à être prévisible et doit-elle être détectée à l’aide de l’index du catalogue uniquement.

Nouveaux éléments de catalogue sont ajoutés à la page dans l’index du catalogue uniquement avec l’horodateur de validation la plus élevée ou vers une nouvelle page. Une fois qu’une page avec un horodateur de validation plus élevée est ajoutée au catalogue, des pages plus anciens ne sont jamais ajoutées ou modifiées.

Le document de la page catalogue est un objet JSON avec les propriétés suivantes :

Name            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
commitId        | chaîne           | oui      | Un ID unique associé à la validation la plus récente de cette page
commitTimeStamp | chaîne           | oui      | Un horodateur de la validation la plus récente de cette page
count           | entiers          | oui      | Le nombre d’éléments dans la page
Éléments           | Tableau d’objets | oui      | Les éléments de catalogue dans cette page
parent          | chaîne           | oui      | Une URL à l’index du catalogue

Chaque élément dans le `items` tableau est un objet avec le minimum de certains détails sur l’élément de catalogue. Des objets de ces éléments ne contiennent pas toutes les données de l’élément de catalogue. L’ordre des éléments dans la page `items` tableau n’est pas défini. Éléments peuvent être triés par le client dans la mémoire à l’aide de leurs `commitTimeStamp` propriété.

Le nombre d’éléments de catalogue dans une page est défini par l’implémentation du serveur. Pour nuget.org, est au maximum 550 éléments dans chaque page, le nombre réel peut être plus petit pour certaines pages selon la taille du lot de validation suivante au point dans le temps.

Comme de nouveaux éléments sont ajoutées, les `count` est objets des éléments de catalogue incrémenté et nouvelle s’affichent dans le `items` tableau.

Comme les éléments sont ajoutés à la page, le `commitId` modifications et la `commitTimeStamp` augmente. Ces deux propriétés sont essentiellement un résumé de toutes `commitId` et `commitTimeStamp` des valeurs dans le `items` tableau.

### <a name="catalog-item-object-in-a-page"></a>Objet d’élément dans une page du catalogue

Les objets d’élément de catalogue trouvant dans la page de catalogue `items` propriété ont les propriétés suivantes :

Name            | Type    | Obligatoire | Notes
--------------- | ------- | -------- | -----
@id             | chaîne  | oui      | L’URL pour extraire l’élément de catalogue
@type           | chaîne  | oui      | Le type de l’élément de catalogue
commitId        | chaîne  | oui      | L’ID de validation associé à cet élément de catalogue
commitTimeStamp | chaîne  | oui      | L’horodateur de validation de cet élément de catalogue
NuGet:ID        | chaîne  | oui      | L’ID de package correspondant à cette feuille
nuget:version   | chaîne  | oui      | La version du package associé à cette feuille.

Le `@type` aura l’une des deux valeurs suivantes :

1. `nuget:PackageDetails`: cela correspond à `PackageDetails` type dans le document de feuille de catalogue.
1. `nuget:PackageDelete`: cela correspond à la `PackageDelete` type dans le document de feuille de catalogue.

Pour plus d’informations sur la chaque type, consultez la [correspondant les éléments de type](#item-types) ci-dessous.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Feuille de catalogue

La feuille de catalogue contient les métadonnées relatives à un ID de package spécifique et une version à un moment donné dans le temps. Il s’agit d’un document extrait à l’aide de la `@id` valeur trouvée dans une page du catalogue. L’URL à une feuille de catalogue n’est pas destinée à être prévisible et doit être découvert à l’aide d’une page de catalogue.

Le document de feuille de catalogue est un objet JSON avec les propriétés suivantes :

Name                    | Type                       | Obligatoire | Notes
----------------------- | -------------------------- | -------- | -----
@type                   | chaîne ou tableau de chaînes | oui      | Les types de l’élément de catalogue
catalog:commitId        | chaîne                     | oui      | Un ID de validation associé à cet élément de catalogue
catalog:commitTimeStamp | chaîne                     | oui      | L’horodateur de validation de cet élément de catalogue
ID                      | chaîne                     | oui      | L’ID de package de l’élément de catalogue
publié               | chaîne                     | oui      | La date de publication de l’élément de catalogue du package
version                 | chaîne                     | oui      | La version du package de l’élément de catalogue

### <a name="item-types"></a>Types d’éléments

Le `@type` propriété est une chaîne ou un tableau de chaînes. Pour plus de commodité, si le `@type` valeur est une chaîne, il doit être traité comme n’importe quel tableau de taille. Toutes les valeurs possibles `@type` sont documentées. Toutefois, chaque élément de catalogue a un seul des deux valeurs de type de chaîne suivantes :

1. `PackageDetails`: représente une capture instantanée de métadonnées de package
1. `PackageDelete`: représente un package qui a été supprimé

### <a name="package-details-catalog-items"></a>Détails du package des éléments de catalogue

Éléments avec le type de catalogue `PackageDetails` contiennent un instantané des métadonnées de package pour un package spécifique (combinaison de l’ID et la version). Un élément de catalogue de détails du package est généré lorsqu’une source de package rencontre un des scénarios suivants :

1. Un package est **envoyées**.
1. Un package est **répertoriés**.
1. Un package est **non listées**.
1. Un package est **réorganisé**.

Une redistribution du package est un mouvement d’administration qui essentiellement génère une fausse par émission de données d’un package existant sans modification au package lui-même. Sur nuget.org, une redistribution est utilisée après avoir corrigé un bogue dans une des tâches en arrière-plan qui consomment le catalogue.

Clients consommant les éléments de catalogue ne doivent pas tenter de déterminer laquelle de ces scénarios produites à l’élément de catalogue. Au lieu de cela, le client doit simplement mettre à jour toute vue gérée ou un index avec les métadonnées contenues dans l’élément de catalogue. En outre, les éléments de catalogue dupliquée ou redondante doivent être gérées normalement (manière idempotente).

Détails des éléments de catalogue package ont les propriétés suivantes en plus de ceux [inclus sur toutes les feuilles de catalogue](#catalog-leaf).

Name                    | Type                       | Obligatoire | Notes
----------------------- | -------------------------- | -------- | -----
authors                 | chaîne                     | Non       |
created                 | chaîne                     | oui      | Lorsque le package a été créé pour la première horodateur
dependencyGroups        | Tableau d’objets           | Non       | Même format que le [ressource de métadonnées du package](registration-base-url-resource.md#package-dependency-group)
Description             | chaîne                     | Non       |
iconUrl                 | chaîne                     | Non       |
isPrerelease            | boolean                    | oui      | Indique si la version du package est préliminaire
language                | chaîne                     | Non       |
licenseUrl              | chaîne                     | Non       |
liste                  | boolean                    | Non       | Indique si le package s’affiche.
minClientVersion        | chaîne                     | Non       |
packageHash             | chaîne                     | oui      | Le hachage du package, à l’aide de l’encodage [standard base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | chaîne                     | oui      |
packageSize             | entiers                    | oui      | La taille de la .nupkg package en octets
projectUrl              | chaîne                     | Non       |
releaseNotes            | chaîne                     | Non       |
requireLicenseAgreement | boolean                    | Non       | Supposons que `false` si exclu
résumé                 | chaîne                     | Non       |
étiquettes                    | Tableau de chaînes           | Non       |
titre                   | chaîne                     | Non       |
verbatimVersion         | chaîne                     | Non       | La chaîne de version, telle qu’elle est trouvée à l’origine dans le .nuspec

Le package `version` propriété est la chaîne de version complet, normalisé. Cela signifie que les données de build SemVer 2.0.0 peuvent être incluses ici.

Le `created` timestamp est lorsque le package a été reçu par la source du package, qui est généralement une brève période avant l’horodateur de validation de l’élément de catalogue.

Le `packageHashAlgorithm` est une chaîne définie par l’implémentation de serveur qui représente l’algorithme de hachage utilisé pour produire le `packageHash`. NuGet.org toujours utilisé la `packageHashAlgorithm` valeur `SHA512`.

Le `published` timestamp est le temps lorsque le package a été indiqué dernier.

> [!Note]
> Sur nuget.org, le `published` a la valeur à l’année 1900 lorsque le package n’est pas spécifié.

#### <a name="sample-request"></a>Exemple de demande

TÉLÉCHARGER https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Supprimer des éléments de catalogue package

Éléments avec le type de catalogue `PackageDelete` contiennent un ensemble minimal d’informations, ce qui indique aux clients de catalogue qu’un package a été supprimé de la source du package n’est plus disponible pour toute opération de package (par exemple la restauration).

> [!Note]
> Il est possible pour un package à supprimer et republié plus tard à l’aide de la même ID de package et la version. Sur nuget.org, c’est le cas très rare qu’interrompt le principe du client officiel qu’un ID de package et une version impliquent un contenu de package spécifique. Pour plus d’informations sur la suppression du package sur nuget.org, consultez [notre stratégie](../policies/deleting-packages.md).

Supprimer des éléments de catalogue package qu’aucune propriété supplémentaire en plus de ceux [inclus sur toutes les feuilles de catalogue](#catalog-leaf).

Le `version` propriété est la chaîne de version d’origine trouvée dans le package .nuspec.

Le `published` propriété est le temps lorsque le package a été supprimé, ce qui indique généralement que peu de temps avant l’horodateur de validation de l’élément de catalogue.

#### <a name="sample-request"></a>Exemple de demande

TÉLÉCHARGER https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Curseur

### <a name="overview"></a>Vue d'ensemble

Cette section décrit un concept de client qui, bien que n’est ne pas nécessairement autorisé par le protocole, doit faire partie de toute implémentation de client de pratiques de catalogue.

Étant donné que le catalogue est une structure de données ajout uniquement indexée par heure, le client doit stocker un **curseur** localement, représentant jusqu'à quel point dans le temps que le client a traité les éléments de catalogue. Notez que cette valeur de curseur doit jamais être générée à l’aide d’horloge d’ordinateur du client. Au lieu de cela, la valeur doit provenir d’un objet de catalogue `commitTimestamp` valeur.

Chaque fois que le client souhaite traiter les nouveaux événements sur la source du package, il devez uniquement interroger le catalogue pour tous les éléments de catalogue avec un horodateur de validation supérieure à son curseur stockée. Une fois que le client traite correctement tous les nouveaux éléments de catalogue, elle enregistre l’horodateur de la dernière validation d’éléments de catalogue simplement traités en tant que sa nouvelle valeur de curseur.

À l’aide de cette approche, le client peut être sûr de ne jamais manquer des événements de package qui s’est produite sur la source du package.
En outre, le client n’a jamais de retraiter les anciens événements avant l’horodateur de validation enregistré du curseur.

Ce concept puissant de curseurs est utilisé pour la plupart des tâches en arrière-plan de nuget.org et est utilisé pour maintenir l’API V3 lui-même à jour. 

### <a name="initial-value"></a>Valeur initiale

Lorsque le client de catalogue démarre pour la première fois (et par conséquent n’a aucune valeur de curseur), elle doit utiliser la valeur de curseur par défaut. Du NET `System.DateTimeOffset.MinValue` ou certains analogue notion d’horodateur représentable minimal.

### <a name="iterating-over-catalog-items"></a>Itérer au sein des éléments de catalogue

Pour rechercher l’ensemble suivant d’éléments de catalogue à traiter, le client doit :

1. Extraire la valeur de curseur enregistrée à partir d’un magasin local.
1. Télécharger et la désérialisation de l’index du catalogue.
1. Rechercher toutes les pages avec un horodateur de validation du catalogue *supérieur* le curseur.
1. Déclarer une liste vide d’éléments de catalogue à traiter.
1. Pour chaque page du catalogue correspondant à l’étape 3 :
   1. Télécharger et la désérialisation de la page du catalogue.
   1. Rechercher tous les éléments avec un horodateur de validation de catalogue *supérieur* le curseur.
   1. Ajouter tous les éléments du catalogue correspondant à la liste déclarée à l’étape 4.
1. Trier la liste d’éléments de catalogue horodateur de validation.
1. Traitement de chaque élément de catalogue dans la séquence :
   1. Télécharger et de désérialiser l’élément de catalogue.
   1. Réagir de façon appropriée pour le type de l’élément de catalogue.
   1. Traiter le document d’élément de catalogue de manière spécifiques au client.
1. Enregistrer l’horodateur de validation du dernier élément catalogue en tant que la nouvelle valeur du curseur.

Avec cet algorithme de base, l’implémentation du client peut générer une vue complète de tous les packages disponibles sur la source du package. Le client suffit d’exécuter cet algorithme régulièrement pour toujours connaître les dernières modifications apportées à la source du package.

> [!Note]
> Ceci est l’algorithme que nuget.org utilise pour conserver le [les métadonnées du Package](registration-base-url-resource.md), [le contenu du Package](package-base-address-resource.md), [recherche](search-query-service-resource.md) et [la saisie semi-automatique](search-autocomplete-service-resource.md) ressources de mise à jour.

### <a name="dependent-cursors"></a>Curseurs dépendants

Supposons qu’il existe deux clients de catalogue qui ont une dépendance inhérente à la sortie d’un client où dépend de sortie du client à un autre. 

#### <a name="example"></a>Exemple

Par exemple, sur nuget.org un package qui vient d’être publié ne doit pas apparaître dans la ressource de recherche qu’il apparaisse dans la ressource de métadonnées de package. Il s’agit, car l’opération de « restore » par le client NuGet officiel utilise la ressource de métadonnées de package. Si un client détecte un package en utilisant le service de recherche, ils doivent être en mesure de restaurer correctement ce package à l’aide de la ressource de métadonnées de package. En d’autres termes, la ressource de recherche dépend de la ressource de métadonnées de package. Chaque ressource a une tâche en arrière-plan de client catalogue mise à jour de cette ressource. Chaque client possède son propre curseur.

Étant donné que les deux ressources sont générés sur le catalogue, le curseur du client de catalogue qui met à jour la ressource de recherche *ne doivent pas aller au-delà de* le curseur du client de catalogue de métadonnées de package.

#### <a name="algorithm"></a>Algorithme

Pour implémenter cette restriction, modifiez simplement l’algorithme ci-dessus pour être :

1. Extraire la valeur de curseur enregistrée à partir d’un magasin local.
1. Télécharger et la désérialisation de l’index du catalogue.
1. Rechercher toutes les pages avec un horodateur de validation du catalogue *supérieur* le curseur **inférieure ou égale à un curseur de la dépendance.**
1. Déclarer une liste vide d’éléments de catalogue à traiter.
1. Pour chaque page du catalogue correspondant à l’étape 3 :
   1. Télécharger et la désérialisation de la page du catalogue.
   1. Rechercher tous les éléments avec un horodateur de validation de catalogue *supérieur* le curseur **inférieure ou égale à un curseur de la dépendance.**
   1. Ajouter tous les éléments du catalogue correspondant à la liste déclarée à l’étape 4.
1. Trier la liste d’éléments de catalogue horodateur de validation.
1. Traitement de chaque élément de catalogue dans la séquence :
   1. Télécharger et de désérialiser l’élément de catalogue.
   1. Réagir de façon appropriée pour le type de l’élément de catalogue.
   1. Traiter le document d’élément de catalogue de manière spécifiques au client.
1. Enregistrer l’horodateur de validation du dernier élément catalogue en tant que la nouvelle valeur du curseur.

À l’aide de cet algorithme modifié, vous pouvez créer un système de clients de catalogue dépendant produisant toutes leurs propres des index spécifiques, les artefacts, etc.
