---
title: Ressource de catalogue, les API NuGet V3
description: Le catalogue est un index de tous les packages créés et supprimés sur nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8e4fb376e471a207333d241aeb414da7d5c3571e
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496541"
---
# <a name="catalog"></a>Catalogue

Le **catalogue** est une ressource qui enregistre toutes les opérations de package sur une source de package, telles que les créations et suppressions. La ressource de catalogue a le `Catalog` tapez dans le [index de service](service-index.md). Vous pouvez utiliser cette ressource pour [de requête pour tous les packages publiés](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Étant donné que le catalogue n’est pas utilisé par le client NuGet officiel, pas toutes les sources de package implémentent le catalogue.

> [!Note]
> Actuellement, le catalogue de nuget.org n’est pas disponible en Chine. Pour plus d’informations, consultez [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Gestion de version

Ce qui suit `@type` valeur est utilisée :

Valeur@type   | Notes
------------- | -----
Catalog/3.0.0 | La version initiale

## <a name="base-url"></a>URL de base

L’URL de point d’entrée pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeurs. Cette rubrique utilise l’URL de l’espace réservé `{@id}`.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvés dans la prise en charge de la ressource catalogue uniquement les méthodes HTTP `GET` et `HEAD`.

## <a name="catalog-index"></a>Index du catalogue

L’index du catalogue est un document dans un emplacement connu qui contient une liste des éléments de catalogue, classés par ordre chronologique. Il est le point d’entrée de la ressource de catalogue.

L’index se compose de pages de catalogue. Chaque page de catalogue contient des éléments de catalogue. Chaque élément de catalogue représente un événement concernant un package unique à un point dans le temps. Un élément de catalogue peut représenter un package qui a été créé, retirée de la liste, remise dans la liste ou supprimés à partir de la source du package. En traitant les éléments de catalogue dans l’ordre chronologique, le client peut générer une vue à jour de chaque package existe sur la source du package V3.

En bref, les objets BLOB de catalogue ont la structure hiérarchique suivante :

- **Index**: le point d’entrée pour le catalogue.
- **Page**: un regroupement d’éléments de catalogue.
- **Feuille**: un document qui représente un élément de catalogue, qui est un instantané de l’état d’un package unique.

Chaque objet de catalogue a une propriété appelée le `commitTimeStamp` représentant lorsque l’élément a été ajouté au catalogue. Éléments de catalogue sont ajoutés à une page de catalogue dans des lots nommés validations. Tous les éléments de catalogue dans la même validation ont le même horodateur de validation (`commitTimeStamp`) et ID de validation (`commitId`). Les éléments de catalogue placés dans la même validation représentent les événements qui se sont produits autour du même point dans le temps sur la source du package. Il n’existe aucun classement au sein d’une validation de catalogue.

Étant donné que chaque ID de package et la version est unique, il y aura jamais plus d’un élément de catalogue dans une validation. Cela garantit que les éléments de catalogue pour un package unique peuvent toujours être clairement classés en ce qui concerne l’horodateur de validation.

Il est jamais y avoir plus d’une validation dans le catalogue par `commitTimeStamp`. En d’autres termes, le `commitId` sont redondantes avec le `commitTimeStamp`.

Contrairement à la [ressource des métadonnées du package](registration-base-url-resource.md), ce qui est indexé par ID de package, le catalogue est indexée (et peut être interrogée) uniquement par heure.

Éléments de catalogue sont toujours ajoutées au catalogue dans un ordre chronologique croissant. Cela signifie que si une validation de catalogue est ajoutée au moment X puis aucune validation de catalogue n’est jamais être ajoutée avec un temps inférieur ou égal à X.

La requête suivante extrait l’index du catalogue.

    GET {@id}

L’index du catalogue est un document JSON qui contient un objet avec les propriétés suivantes :

Nom            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
commitId        | string           | oui      | Un ID unique associé à la validation la plus récente
commitTimeStamp | string           | oui      | Un horodatage de la validation la plus récente
count           | entiers          | oui      | Le nombre de pages dans l’index
éléments           | tableau d’objets | oui      | Un tableau d’objets, chaque objet qui représente une page

Chaque élément dans le `items` tableau est un objet avec un minimum de détails sur chaque page. Ces objets de page ne contiennent pas les feuilles de catalogue (éléments). L’ordre des éléments dans ce tableau n’est pas défini. Pages peuvent être triées par le client dans la mémoire à l’aide de leurs `commitTimeStamp` propriété.

Comme de nouvelles pages sont introduites, le `count` sera incrémenté et de nouveaux objets seront affichent dans le `items` tableau.

Comme les éléments sont ajoutés à, l’index du catalogue `commitId` changera et le `commitTimeStamp` augmentera. Ces deux propriétés sont essentiellement un résumé sur la page toutes les `commitId` et `commitTimeStamp` des valeurs dans le `items` tableau.

### <a name="catalog-page-object-in-the-index"></a>Objet de page dans l’index du catalogue

Les objets de la page catalogue trouvés dans l’index de catalogue `items` propriété ont les propriétés suivantes :

Nom            | Type    | Obligatoire | Notes
--------------- | ------- | -------- | -----
@id             | string  | oui      | L’URL de page de catalogue fetch
commitId        | string  | oui      | Un ID unique associé à la validation la plus récente de cette page
commitTimeStamp | string  | oui      | Un horodatage de la validation la plus récente de cette page
count           | entiers | oui      | Le nombre d’éléments dans la page catalogue

Contrairement à la [ressource des métadonnées du package](registration-base-url-resource.md) qui, dans certains cas incorporations laisse dans l’index, les feuilles de catalogue ne sont jamais inline dans l’index et doivent toujours être extraite à l’aide de la page `@id` URL.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Page de catalogue

La page de catalogue est une collection d’éléments de catalogue. Il s’agit d’un document extrait en utilisant une de la `@id` valeurs trouvées dans l’index du catalogue. L’URL vers une page de catalogue n’est pas destinée à être prévisible et doit-elle être détectée à l’aide de l’index du catalogue uniquement.

Nouveaux éléments de catalogue sont ajoutés à la page dans l’index du catalogue uniquement avec l’horodateur de validation la plus élevée ou à une nouvelle page. Une fois qu’une page avec un horodateur de validation plus élevée est ajoutée au catalogue, les pages anciennes ne sont jamais ajoutées ou modifiées.

Le document de page de catalogue est un objet JSON avec les propriétés suivantes :

Nom            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
commitId        | string           | oui      | Un ID unique associé à la validation la plus récente de cette page
commitTimeStamp | string           | oui      | Un horodatage de la validation la plus récente de cette page
count           | entiers          | oui      | Le nombre d’éléments dans la page
éléments           | tableau d’objets | oui      | Les éléments de catalogue dans cette page
parent          | string           | oui      | Une URL vers l’index du catalogue

Chaque élément dans le `items` tableau est un objet avec un minimum de détails sur l’élément de catalogue. Ces objets d’élément ne contiennent pas toutes les données de l’élément de catalogue. L’ordre des éléments dans la page `items` tableau n’est pas défini. Éléments peuvent être commandés par le client dans la mémoire à l’aide de leurs `commitTimeStamp` propriété.

Le nombre d’éléments de catalogue dans une page est défini par l’implémentation du serveur. Pour nuget.org, comportent au maximum 550 éléments dans chaque page, même si le nombre réel peut être plus petit pour certaines pages selon la taille du lot de validation suivant au point dans le temps.

Comme de nouveaux éléments sont présentés, le `count` est objets d’élément incrémenté et nouveau catalogue s’affichent dans le `items` tableau.

Comme les éléments sont ajoutés à la page, le `commitId` modifications et la `commitTimeStamp` augmente. Ces deux propriétés sont essentiellement un résumé sur l’ensemble `commitId` et `commitTimeStamp` des valeurs dans le `items` tableau.

### <a name="catalog-item-object-in-a-page"></a>Objet d’élément dans une page de catalogue

Les objets d’élément de catalogue trouvant dans la page catalogue `items` propriété ont les propriétés suivantes :

Nom            | Type    | Obligatoire | Notes
--------------- | ------- | -------- | -----
@id             | string  | oui      | L’URL pour récupérer l’élément de catalogue
@type           | string  | oui      | Le type de l’élément de catalogue
commitId        | string  | oui      | L’ID de validation associé à cet élément de catalogue
commitTimeStamp | string  | oui      | L’horodateur de validation de cet élément de catalogue
NuGet:ID        | string  | oui      | L’ID de package qui concerne cette feuille
nuget:version   | string  | oui      | La version du package associé à cette feuille

Le `@type` aura l’une des deux valeurs suivantes :

1. `nuget:PackageDetails`: cela correspond à `PackageDetails` type dans le document de feuille de catalogue.
1. `nuget:PackageDelete`: cela correspond à la `PackageDelete` type dans le document de feuille de catalogue.

Pour plus d’informations sur la chaque type, consultez la [correspondant les éléments de type](#item-types) ci-dessous.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Feuille de catalogue

La feuille de catalogue contient des métadonnées sur un ID de package spécifique et une version à un moment donné dans le temps. Il s’agit d’un document extrait en utilisant le `@id` valeur trouvée dans une page de catalogue. L’URL à une feuille de catalogue n’est pas destinée à être prévisible et doit être découvert à l’aide d’une page de catalogue.

Le document de feuille de catalogue est un objet JSON avec les propriétés suivantes :

Nom                    | Type                       | Obligatoire | Notes
----------------------- | -------------------------- | -------- | -----
@type                   | chaîne ou tableau de chaînes | oui      | L’ou les types de l’élément de catalogue
catalog:commitId        | string                     | oui      | Un ID de validation associé à cet élément de catalogue
catalog:commitTimeStamp | string                     | oui      | L’horodateur de validation de cet élément de catalogue
ID                      | string                     | oui      | L’ID de package de l’élément de catalogue
Publié               | string                     | oui      | La date de publication de l’élément de catalogue du package
version                 | string                     | oui      | La version du package de l’élément de catalogue

### <a name="item-types"></a>Types d’éléments

Le `@type` propriété est une chaîne ou un tableau de chaînes. Pour plus de commodité, si le `@type` valeur est une chaîne, il doit être traité comme n’importe quel tableau de taille d’un. Toutes les valeurs possibles pour `@type` sont documentées. Toutefois, chaque élément de catalogue a exactement l’une des deux valeurs de type chaîne suivantes :

1. `PackageDetails`: représente un instantané des métadonnées du package
1. `PackageDelete`: représente un package qui a été supprimé

### <a name="package-details-catalog-items"></a>Détails du package des éléments de catalogue

Éléments avec le type de catalogue `PackageDetails` contiennent un instantané de métadonnées du package pour un package spécifique (combinaison de l’ID et la version). Un élément de catalogue de détails du package est généré lorsqu’une source de package rencontre l’un des scénarios suivants :

1. Un package est **poussé**.
1. Un package est **répertoriés**.
1. Un package est **non listé**.
1. Un package est **réorganisé**.

Un redistribution du package est un mouvement d’administration qui génère essentiellement un faux push d’un package existant sans aucune modification au package lui-même. Sur nuget.org, une redistribution est utilisée après avoir corrigé un bogue dans un des travaux en arrière-plan qui consomment le catalogue.

Les clients de consommer les éléments de catalogue ne devraient pas essayer déterminer lequel de ces scénarios produit l’élément de catalogue. Au lieu de cela, le client doit simplement mettre à jour toute vue mise à jour ou un index avec les métadonnées contenues dans l’élément de catalogue. En outre, les éléments de catalogue en double ou redondantes doivent être gérées normalement (idempotente).

Détails des éléments de catalogue package ont les propriétés suivantes en plus de ceux [inclus sur toutes les feuilles de catalogue](#catalog-leaf).

Nom                    | Type                       | Obligatoire | Notes
----------------------- | -------------------------- | -------- | -----
authors                 | string                     | Non       |
created                 | string                     | Non       | Un horodatage de date de création tout d’abord le package. Propriété de secours : `published`.
dependencyGroups        | tableau d’objets           | Non       | Les dépendances du package, regroupées par le framework cible ([même format que la ressource de métadonnées de package](registration-base-url-resource.md#package-dependency-group))
Dépréciation             | object                     | Non       | La désapprobation associée au package ([même format que la ressource de métadonnées de package](registration-base-url-resource.md#package-deprecation))
Description             | string                     | Non       |
iconUrl                 | string                     | Non       |
isPrerelease            | boolean                    | Non       | Indique si la version du package est préliminaire. Peut être détectée à partir de `version`.
language                | string                     | Non       |
licenseUrl              | string                     | Non       |
liste                  | boolean                    | Non       | Le package est répertorié ou non
minClientVersion        | string                     | Non       |
packageHash             | string                     | oui      | Le hachage du package, à l’aide de codage [base 64 standard](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | string                     | oui      |
packageSize             | entiers                    | oui      | La taille de la .nupkg package en octets
projectUrl              | string                     | Non       |
releaseNotes            | string                     | Non       |
requireLicenseAgreement | boolean                    | Non       | Supposons que `false` si exclu
résumé                 | string                     | Non       |
étiquettes                    | tableau de chaînes           | Non       |
titre                   | string                     | Non       |
verbatimVersion         | string                     | Non       | La chaîne de version, tel qu’il se trouve à l’origine dans le fichier .nuspec

Le package `version` propriété est la chaîne de version complète après la normalisation. Cela signifie que les données de build de SemVer 2.0.0 peuvent être incluses ici.

Le `created` timestamp est lorsque le package a été tout d’abord reçu par la source du package, qui est généralement un court délai avant l’horodateur de validation de l’élément de catalogue.

Le `packageHashAlgorithm` est une chaîne définie par l’implémentation de serveur représentant l’algorithme de hachage utilisé pour produire le `packageHash`. NuGet.org toujours utilisé la `packageHashAlgorithm` valeur `SHA512`.

Le `published` timestamp est le temps lorsque le package a été répertorié pour la dernière.

> [!Note]
> Sur nuget.org, le `published` a la valeur à l’année 1900 lorsque le package n’est pas répertorié.

#### <a name="sample-request"></a>Exemple de demande

TÉLÉCHARGER https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Éléments de catalogue de suppression de package

Éléments avec le type de catalogue `PackageDelete` contiennent un ensemble minimal des informations indiquant aux clients du catalogue qu’un package a été supprimé de la source du package et n’est plus disponible pour toute opération de package (telles que la restauration).

> [!NOTE]
> Il est possible pour un package à supprimer et à l’aide republié plus tard le même ID de package et la version. Sur nuget.org, c’est un cas très rare car cela rompt l’hypothèse du client officiel qu’un ID de package et une version impliquent un contenu de package spécifique. Pour plus d’informations sur la suppression du package sur nuget.org, consultez [notre stratégie](../nuget-org/policies/deleting-packages.md).

Supprimer des éléments de catalogue package n’ont aucune propriété supplémentaire en plus de ceux [inclus sur toutes les feuilles de catalogue](#catalog-leaf).

Le `version` propriété est la chaîne de version d’origine trouvée dans le package .nuspec.

Le `published` propriété est le temps lorsque le package a été supprimé, ce qui est en général comme un court délai avant l’horodateur de validation de l’élément de catalogue.

#### <a name="sample-request"></a>Exemple de demande

TÉLÉCHARGER https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Curseur

### <a name="overview"></a>Vue d'ensemble

Cette section décrit un concept de client qui, bien que n’est ne pas nécessairement autorisé par le protocole, doit faire partie de toute implémentation de client de pratiques de catalogue.

Étant donné que le catalogue est une structure de données en ajout seul indexée par le temps, le client doit stocker un **curseur** localement, allant jusqu'à quel point dans le temps que le client a traité les éléments de catalogue. Notez que cette valeur de curseur doit jamais être générée à l’aide d’horloge de la machine du client. Au lieu de cela, la valeur doit provenir d’un objet de catalogue `commitTimestamp` valeur.

Chaque fois que le client souhaite traiter les nouveaux événements sur la source du package, il devez uniquement interroger le catalogue pour tous les éléments de catalogue avec un horodateur de validation supérieure à son curseur stockée. Une fois que le client traite correctement tous les nouveaux éléments de catalogue, il enregistre l’horodateur de la dernière validation des éléments du catalogue traités simplement comme sa nouvelle valeur de curseur.

À l’aide de cette approche, le client peut veillez à ne manquez jamais tous les événements de package qui s’est produite sur la source du package.
En outre, le client n’a jamais de retraiter les anciens événements avant l’horodateur de validation enregistré du curseur.

Ce concept puissant des curseurs est utilisé pour la plupart des tâches en arrière-plan de nuget.org et est utilisé pour maintenir l’API V3 lui-même à jour. 

### <a name="initial-value"></a>Valeur initiale

Lorsque le client de catalogue démarre pour la première fois (et par conséquent n’a aucune valeur de curseur), il doit utiliser le curseur comme valeur par défaut. NET `System.DateTimeOffset.MinValue` ou certains analogue notion d’horodateur représentable minimal.

### <a name="iterating-over-catalog-items"></a>Itération au sein des éléments de catalogue

Pour rechercher l’ensemble suivant d’éléments de catalogue à traiter, le client doit :

1. Extraire la valeur de curseur enregistrée à partir d’un magasin local.
1. Télécharger et désérialiser l’index du catalogue.
1. Rechercher toutes les pages avec un horodateur de validation du catalogue *supérieur* le curseur.
1. Déclarez une liste vide d’éléments de catalogue à traiter.
1. Pour chaque page de catalogue mis en correspondance à l’étape 3 :
   1. Télécharger et la désérialisation de la page du catalogue.
   1. Rechercher tous les éléments avec un horodateur de validation de catalogue *supérieur* le curseur.
   1. Ajouter tous les éléments du catalogue correspondant à la liste déclarée à l’étape 4.
1. Trier la liste d’éléments de catalogue en horodateur de validation.
1. Traiter chaque élément de catalogue dans la séquence :
   1. Télécharger et désérialiser l’élément de catalogue.
   1. Réagir de façon appropriée pour le type de l’élément de catalogue.
   1. Traiter le document d’élément de catalogue de manière spécifique au client.
1. Enregistrez l’horodateur de validation est du dernier élément catalogue en tant que la nouvelle valeur de curseur.

Avec cet algorithme de base, l’implémentation du client peut s’accumuler une vue complète de tous les packages disponibles sur la source du package. Le client suffit d’exécuter cet algorithme régulièrement pour toujours être informé des dernières modifications à la source du package.

> [!Note]
> Ceci est l’algorithme que nuget.org utilise pour maintenir la [les métadonnées du Package](registration-base-url-resource.md), [le contenu du Package](package-base-address-resource.md), [recherche](search-query-service-resource.md) et [la saisie semi-automatique](search-autocomplete-service-resource.md) ressources à jour.

### <a name="dependent-cursors"></a>Curseurs dépendants

Supposons qu’il existe deux clients de catalogue qui ont une dépendance inhérente où les sortie d’un client dépend de sortie du client à un autre. 

#### <a name="example"></a>Exemple

Par exemple, sur nuget.org un package qui vient d’être publié ne doit pas apparaître dans la ressource de recherche avant d’apparaître dans la ressource de métadonnées de package. Il s’agit, car l’opération « restore » effectuée par le client NuGet officiel utilise la ressource de métadonnées de package. Si un client découvre un package en utilisant le service de recherche, ils doivent être restaurés correctement ce package à l’aide de la ressource de métadonnées de package. En d’autres termes, la ressource de recherche dépend de la ressource de métadonnées de package. Chaque ressource a une tâche en arrière-plan de client de catalogue la mise à jour de cette ressource. Chaque client possède son propre curseur.

Étant donné que les deux ressources sont créées sur le catalogue, le curseur du client de catalogue qui met à jour de la ressource de recherche *ne doit pas dépasser* le curseur du client de catalogue de métadonnées de package.

#### <a name="algorithm"></a>Algorithme

Pour implémenter cette restriction, modifiez simplement l’algorithme ci-dessus pour être :

1. Extraire la valeur de curseur enregistrée à partir d’un magasin local.
1. Télécharger et désérialiser l’index du catalogue.
1. Rechercher toutes les pages avec un horodateur de validation du catalogue *supérieur* le curseur **inférieur ou égal au curseur de la dépendance.**
1. Déclarez une liste vide d’éléments de catalogue à traiter.
1. Pour chaque page de catalogue mis en correspondance à l’étape 3 :
   1. Télécharger et la désérialisation de la page du catalogue.
   1. Rechercher tous les éléments avec un horodateur de validation de catalogue *supérieur* le curseur **inférieur ou égal au curseur de la dépendance.**
   1. Ajouter tous les éléments du catalogue correspondant à la liste déclarée à l’étape 4.
1. Trier la liste d’éléments de catalogue en horodateur de validation.
1. Traiter chaque élément de catalogue dans la séquence :
   1. Télécharger et désérialiser l’élément de catalogue.
   1. Réagir de façon appropriée pour le type de l’élément de catalogue.
   1. Traiter le document d’élément de catalogue de manière spécifique au client.
1. Enregistrez l’horodateur de validation est du dernier élément catalogue en tant que la nouvelle valeur de curseur.

À l’aide de cet algorithme modifié, vous pouvez créer un système de clients du catalogue dépendant production tous leurs propres des index spécifiques, les artefacts, etc.
