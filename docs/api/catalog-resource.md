---
title: Ressource catalogue, API NuGet v3
description: Le catalogue est un index de tous les packages créés et supprimés sur nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6c04453fec9beb7b0998953384ec60694e1213c1
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990145"
---
# <a name="catalog"></a>Catalogue

Le **catalogue** est une ressource qui enregistre toutes les opérations de package sur une source de package, telles que les créations et les suppressions. La ressource de catalogue a le `Catalog` type dans l' [index de service](service-index.md). Vous pouvez utiliser cette ressource pour [Rechercher tous les packages publiés](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Étant donné que le catalogue n’est pas utilisé par le client NuGet officiel, toutes les sources de package n’implémentent pas le catalogue.

> [!Note]
> Actuellement, le catalogue nuget.org n’est pas disponible en Chine. Pour plus d’informations, consultez [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Contrôle de version

La `@type` valeur suivante est utilisée :

Valeur @type   | Notes
------------- | -----
Catalogue/3.0.0 | La version initiale

## <a name="base-url"></a>URL de base

L’URL du point d’entrée pour les API suivantes est la valeur de la `@id` propriété associée aux valeurs de ressource mentionnées ci-dessus `@type` . Cette rubrique utilise l’URL de l’espace réservé `{@id}` .

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvées dans la ressource de catalogue prennent uniquement en charge les méthodes HTTP `GET` et `HEAD` .

## <a name="catalog-index"></a>Index du catalogue

L’index de catalogue est un document dans un emplacement connu qui contient une liste d’éléments de catalogue, classés par ordre chronologique. Il s’agit du point d’entrée de la ressource de catalogue.

L’index est constitué de pages de catalogue. Chaque page de catalogue contient des éléments de catalogue. Chaque élément de catalogue représente un événement concernant un package unique à un moment donné. Un élément de catalogue peut représenter un package qui a été créé, supprimé de la liste, rerépertorié ou supprimé de la source du package. En traitant les éléments de catalogue par ordre chronologique, le client peut créer une vue à jour de chaque package existant sur la source du package v3.

En bref, les objets BLOB de catalogue ont la structure hiérarchique suivante :

- **Index**: point d’entrée du catalogue.
- **Page**: regroupement d’éléments de catalogue.
- **Feuille**: document représentant un élément de catalogue, qui est un instantané de l’état d’un package unique.

Chaque objet Catalogue a une propriété appelée `commitTimeStamp` qui représente le moment où l’élément a été ajouté au catalogue. Les éléments de catalogue sont ajoutés à une page de catalogue par lots appelés validations. Tous les éléments de catalogue dans la même validation ont le même horodatage de validation ( `commitTimeStamp` ) et l’ID de validation ( `commitId` ). Les éléments de catalogue placés dans la même validation représentent des événements qui se sont produits à peu près au même point dans le temps de la source du package. Il n’y a aucun classement dans une validation de catalogue.

Étant donné que chaque ID de package et version est unique, il n’y aura jamais plus d’un élément de catalogue dans une validation. Cela permet de s’assurer que les éléments du catalogue d’un package unique peuvent toujours être triés sans ambiguïté par rapport au datage de validation.

Il n’y a jamais plus d’une validation dans le catalogue par `commitTimeStamp` . En d’autres termes, le `commitId` est redondant avec le `commitTimeStamp` .

Contrairement à la [ressource de métadonnées du package](registration-base-url-resource.md), qui est indexée par ID de package, le catalogue est indexé (et peut être interrogé) uniquement par heure.

Les éléments de catalogue sont toujours ajoutés au catalogue dans un ordre chronologique croissant. Cela signifie que si une validation de catalogue est ajoutée à l’heure X, aucune validation de catalogue ne sera jamais ajoutée avec une heure inférieure ou égale à X.

La requête suivante extrait l’index du catalogue.

```
GET {@id}
```

L’index de catalogue est un document JSON qui contient un objet avec les propriétés suivantes :

Nom            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
commitId        | string           | Oui      | ID unique associé à la validation la plus récente
commitTimeStamp | string           | Oui      | Horodateur de la validation la plus récente
count           | entier          | Oui      | Nombre de pages dans l’index
items           | tableau d’objets | Oui      | Tableau d’objets, chaque objet représentant une page

Chaque élément du `items` tableau est un objet avec des détails minimes sur chaque page. Ces objets de page ne contiennent pas les feuilles de catalogue (éléments). L’ordre des éléments dans ce tableau n’est pas défini. Les pages peuvent être triées par le client en mémoire à l’aide de leur `commitTimeStamp` propriété.

À mesure que de nouvelles pages sont introduites, l' `count` est incrémenté et de nouveaux objets s’affichent dans le `items` tableau.

Au fur et à mesure que des éléments sont ajoutés au catalogue, l’index est `commitId` modifié et l' `commitTimeStamp` opération augmente. Ces deux propriétés sont essentiellement un résumé de toutes les pages `commitId` et `commitTimeStamp` valeurs du `items` tableau.

### <a name="catalog-page-object-in-the-index"></a>Objet de page de catalogue dans l’index

Les objets de page de catalogue trouvés dans la propriété de l’index de catalogue `items` ont les propriétés suivantes :

Nom            | Type    | Obligatoire | Notes
--------------- | ------- | -------- | -----
@id             | string  | Oui      | URL de récupération de la page de catalogue
commitId        | string  | Oui      | ID unique associé à la validation la plus récente dans cette page
commitTimeStamp | string  | Oui      | Horodateur de la dernière validation dans cette page
count           | entier | Oui      | Nombre d’éléments dans la page de catalogue

Contrairement à la [ressource de métadonnées de package](registration-base-url-resource.md) , qui, dans certains cas, insère des feuilles dans l’index, les feuilles de catalogue ne sont jamais inline dans l’index et doivent toujours être extraites à l’aide de l’URL de la page `@id` .

### <a name="sample-request"></a>Exemple de requête

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Page catalogue

La page catalogue est une collection d’éléments de catalogue. Il s’agit d’un document extrait à l’aide de l’une des `@id` valeurs figurant dans l’index du catalogue. L’URL d’une page de catalogue n’est pas destinée à être prévisible et doit être découverte à l’aide de l’index de catalogue uniquement.

Les nouveaux éléments de catalogue sont ajoutés à la page dans l’index de catalogue uniquement avec l’horodateur de validation le plus élevé ou vers une nouvelle page. Une fois qu’une page avec un horodateur de validation plus élevé est ajoutée au catalogue, les anciennes pages ne sont jamais ajoutées ou modifiées.

Le document de page de catalogue est un objet JSON avec les propriétés suivantes :

Nom            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
commitId        | string           | Oui      | ID unique associé à la validation la plus récente dans cette page
commitTimeStamp | string           | Oui      | Horodateur de la dernière validation dans cette page
count           | entier          | Oui      | Nombre d’éléments dans la page
items           | tableau d’objets | Oui      | Éléments du catalogue dans cette page
parent          | string           | Oui      | URL de l’index du catalogue

Chaque élément du `items` tableau est un objet avec des détails minimes sur l’élément du catalogue. Ces objets d’élément ne contiennent pas toutes les données de l’élément de catalogue. L’ordre des éléments dans le tableau de la page `items` n’est pas défini. Les éléments peuvent être triés par le client en mémoire à l’aide de leur `commitTimeStamp` propriété.

Le nombre d’éléments de catalogue dans une page est défini par l’implémentation du serveur. Pour nuget.org, il y a au plus 550 éléments dans chaque page, bien que le nombre réel puisse être plus petit pour certaines pages en fonction de la taille du lot de validation suivant à un moment donné.

À mesure que de nouveaux éléments sont introduits, le `count` est incrémenté et les nouveaux objets d’élément de catalogue apparaissent dans le `items` tableau.

À mesure que des éléments sont ajoutés à la page, les `commitId` modifications et `commitTimeStamp` augmentent. Ces deux propriétés sont essentiellement un résumé de toutes `commitId` les `commitTimeStamp` valeurs et dans le `items` tableau.

### <a name="catalog-item-object-in-a-page"></a>Objet d’élément de catalogue dans une page

Les objets d’élément de catalogue trouvés dans la propriété de la page du catalogue `items` ont les propriétés suivantes :

Nom            | Type    | Obligatoire | Notes
--------------- | ------- | -------- | -----
@id             | string  | Oui      | URL permettant de récupérer l’élément de catalogue
@type           | string  | Oui      | Type de l’élément de catalogue
commitId        | string  | Oui      | ID de validation associé à cet élément de catalogue
commitTimeStamp | string  | Oui      | Horodatage de validation de cet élément de catalogue
NuGet : ID        | string  | Oui      | ID de package associé à ce nœud terminal
NuGet : version   | string  | Oui      | Version du package à laquelle cette feuille est associée

La `@type` valeur sera l’une des deux valeurs suivantes :

1. `nuget:PackageDetails`: correspond au `PackageDetails` type dans le document feuille du catalogue.
1. `nuget:PackageDelete`: correspond au `PackageDelete` type dans le document feuille du catalogue.

Pour plus d’informations sur la signification de chaque type, consultez le [type d’élément correspondant](#item-types) ci-dessous.

### <a name="sample-request"></a>Exemple de requête

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Feuille du catalogue

Le catalogue feuille contient des métadonnées sur un ID de package et une version spécifiques à un moment donné. Il s’agit d’un document extrait à l’aide de la `@id` valeur trouvée dans une page de catalogue. L’URL d’une feuille de catalogue n’est pas destinée à être prévisible et doit être découverte à l’aide d’une page de catalogue uniquement.

Le document feuille du catalogue est un objet JSON avec les propriétés suivantes :

Nom                    | Type                       | Obligatoire | Notes
----------------------- | -------------------------- | -------- | -----
@type                   | chaîne ou tableau de chaînes | Oui      | Type (s) de l’élément de catalogue
Catalogue : commitId        | string                     | Oui      | ID de validation associé à cet élément de catalogue
Catalogue : commitTimeStamp | string                     | Oui      | Horodatage de validation de cet élément de catalogue
id                      | string                     | Oui      | ID de package de l’élément de catalogue
published               | string                     | Oui      | Date de publication de l’élément du catalogue de packages
version                 | string                     | Oui      | Version du package de l’élément de catalogue

### <a name="item-types"></a>Types d’éléments

La `@type` propriété est une chaîne ou un tableau de chaînes. Pour plus de commodité, si la `@type` valeur est une chaîne, elle doit être traitée comme n’importe quel tableau de taille 1. Toutes les valeurs possibles pour `@type` ne sont pas documentées. Toutefois, chaque élément de catalogue a exactement une des deux valeurs de type chaîne suivantes :

1. `PackageDetails`: représente un instantané des métadonnées du package
1. `PackageDelete`: représente un package qui a été supprimé.

### <a name="package-details-catalog-items"></a>Détails du package éléments du catalogue

Les éléments de catalogue avec le type `PackageDetails` contiennent un instantané des métadonnées du package pour un package spécifique (combinaison ID-version). Un élément de catalogue Détails du package est généré quand une source de package rencontre l’un des scénarios suivants :

1. Un package fait l’objet d’un **Push**.
1. Un package est **listé**.
1. Un package n’est pas **répertorié**.
1. Un package est **redistribué**.

Un redistribution de package est un geste administratif qui génère essentiellement un faux push d’un package existant sans modification du package lui-même. Sur nuget.org, un redistribution est utilisé après avoir corrigé un bogue dans l’une des tâches en arrière-plan qui consomment le catalogue.

Les clients qui utilisent les éléments du catalogue ne doivent pas tenter de déterminer lequel de ces scénarios a produit l’élément de catalogue. Au lieu de cela, le client doit simplement mettre à jour toute vue ou tout index géré avec les métadonnées contenues dans l’élément du catalogue. En outre, les éléments de catalogue dupliqués ou redondants doivent être gérés normalement (manière idempotente).

Détails du package les éléments du catalogue ont les propriétés suivantes en plus de celles [incluses dans tous les feuilles de catalogue](#catalog-leaf).

Nom                    | Type                       | Obligatoire | Notes
----------------------- | -------------------------- | -------- | -----
authors                 | string                     | non       |
created                 | string                     | non       | Horodateur du moment où le package a été créé pour la première fois. Propriété de secours : `published` .
dependencyGroups        | tableau d’objets           | non       | Les dépendances du package, regroupées par version cible du .NET Framework ([même format que la ressource de métadonnées du package](registration-base-url-resource.md#package-dependency-group))
désapprobation             | object                     | non       | La désapprobation associée au package ([même format que la ressource de métadonnées du package](registration-base-url-resource.md#package-deprecation))
description             | string                     | non       |
iconUrl                 | string                     | non       |
isPrerelease            | boolean                    | non       | Indique si la version du package est préliminaire. Peut être détecté à partir de `version` .
langage                | string                     | non       |
licenseUrl              | string                     | non       |
liste                  | boolean                    | non       | Indique si le package est ou non listé
minClientVersion        | string                     | non       |
packageHash             | string                     | Oui      | Hachage du package, encodage à l’aide de la [base standard 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | string                     | Oui      |
empaqueter             | entier                    | Oui      | Taille du package. nupkg en octets
packageTypes            | tableau d’objets           | non       | Types de packages spécifiés par l’auteur.
projectUrl              | string                     | non       |
releaseNotes            | string                     | non       |
requireLicenseAgreement | boolean                    | non       | Supposer `false` si exclu
Récapitulatif                 | string                     | non       |
tags                    | tableau de chaînes           | non       |
title                   | string                     | non       |
verbatimVersion         | string                     | non       | Chaîne de version telle qu’elle est trouvée à l’origine dans le. NuSpec
vulnérabilités         | tableau d’objets           | non       | Les failles de sécurité du package

La propriété de package `version` est la chaîne de version complète après la normalisation. Cela signifie que les données de build SemVer 2.0.0 peuvent être incluses ici.

L' `created` horodateur est le moment où le package a été reçu pour la première fois par la source du package, ce qui correspond généralement à une brève période avant l’horodatage de validation de l’élément de catalogue.

`packageHashAlgorithm`Est une chaîne définie par l’implémentation de serveur qui représente l’algorithme de hachage utilisé pour produire le `packageHash` . nuget.org a toujours utilisé la `packageHashAlgorithm` valeur de `SHA512` .

La `packageTypes` propriété est présente uniquement si un type de package a été spécifié par l’auteur. S’il est présent, il aura toujours au moins une entrée (1). Chaque élément du `packageTypes` tableau est un objet JSON avec les propriétés suivantes :

Nom      | Type    | Obligatoire | Notes
--------- | ------- | -------- | -----
name      | string  | Oui      | Nom du type de package.
version    | string  | non       | Version du type de package. Présent uniquement si l’auteur a spécifié explicitement une version dans le NuSpec.

L' `published` horodateur est l’heure de la dernière liste du package.

> [!Note]
> Sur nuget.org, la `published` valeur est définie sur l’année 1900 lorsque le package est non répertorié.

#### <a name="vulnerabilities"></a>Vulnérabilités

Tableau d'objets `vulnerability`. Chaque vulnérabilité a les propriétés suivantes :

Nom         | Type   | Obligatoire | Notes
------------ | ------ | -------- | -----
advisoryUrl  | string | Oui      | Emplacement de l’avis de sécurité pour le package
severity     | string | Oui      | Gravité de l’avis : "0" = faible, "1" = modéré, "2" = élevé, "3" = critique

Si la `severity` propriété contient des valeurs autres que celles répertoriées ici, la gravité de l’avis doit être considérée comme faible.

#### <a name="sample-request"></a>Exemple de requête

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Supprimer le package des éléments du catalogue

Les éléments de catalogue avec le type `PackageDelete` contiennent un ensemble minimal d’informations indiquant aux clients du catalogue qu’un package a été supprimé de la source du package et qu’il n’est plus disponible pour les opérations de package (telles que la restauration).

> [!NOTE]
> Il est possible de supprimer un package et de le republier ultérieurement à l’aide du même ID de package et de la même version. Sur nuget.org, il s’agit d’un cas très rare, car il arrête l’hypothèse du client officiel qu’un ID de package et une version impliquent un contenu de package spécifique. Pour plus d’informations sur la suppression de packages sur nuget.org, consultez [notre stratégie](../nuget-org/policies/deleting-packages.md).

Les éléments du catalogue de suppression de package n’ont pas de propriétés supplémentaires en plus de celles [incluses dans tous les feuilles de catalogue](#catalog-leaf).

La `version` propriété est la chaîne de version d’origine trouvée dans le package. nuspec.

La `published` propriété est l’heure à laquelle le package a été supprimé, ce qui correspond généralement à une heure très brève avant l’horodateur de validation de l’élément de catalogue.

#### <a name="sample-request"></a>Exemple de requête

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Curseur

### <a name="overview"></a>Vue d’ensemble

Cette section décrit un concept client qui, bien qu’il ne soit pas obligatoirement obligatoire par le protocole, doit faire partie de toute implémentation de client de catalogue pratique.

Étant donné que le catalogue est une structure de données d’ajout uniquement indexée par heure, le client doit stocker un **curseur** localement, ce qui indique jusqu’à quel point dans le temps le client a traité les éléments du catalogue. Notez que cette valeur de curseur ne doit jamais être générée à l’aide de l’horloge de l’ordinateur du client. Au lieu de cela, la valeur doit provenir de la valeur d’un objet catalogue `commitTimestamp` .

Chaque fois que le client souhaite traiter de nouveaux événements sur la source du package, il doit uniquement interroger le catalogue pour tous les éléments du catalogue dont l’horodateur de validation est supérieur à celui de son curseur stocké. Une fois que le client a traité tous les nouveaux éléments de catalogue, il enregistre le dernier horodatage de validation des éléments de catalogue qui vient d’être traité comme sa nouvelle valeur de curseur.

À l’aide de cette approche, le client peut s’assurer de ne jamais manquer les événements de package qui se sont produits sur la source du package.
En outre, le client n’a jamais à retraiter les anciens événements avant l’horodateur de validation enregistré du curseur.

Ce concept puissant de curseurs est utilisé pour de nombreuses tâches en arrière-plan nuget.org et est utilisé pour maintenir à jour l’API V3. 

### <a name="initial-value"></a>Valeur initiale

Quand le client de catalogue démarre pour la première fois (et qu’il n’a donc pas de valeur de curseur), il doit utiliser une valeur de curseur par défaut de. Le réseau `System.DateTimeOffset.MinValue` ou une certaine notion analogue de l’horodateur minimal représentable.

### <a name="iterating-over-catalog-items"></a>Itération sur les éléments du catalogue

Pour interroger l’ensemble suivant d’éléments de catalogue à traiter, le client doit :

1. Extrait la valeur de curseur enregistrée à partir d’un magasin local.
1. Téléchargez et désérialisez l’index du catalogue.
1. Recherche toutes les pages du catalogue dont l’horodateur de validation est *supérieur* au curseur.
1. Déclarez une liste vide d’éléments de catalogue à traiter.
1. Pour chaque page de catalogue correspondante à l’étape 3 :
   1. Téléchargez et désérialisez la page catalogue.
   1. Recherche tous les éléments du catalogue dont l’horodateur de validation est *supérieur* au curseur.
   1. Ajoutez tous les éléments de catalogue correspondants à la liste déclarée à l’étape 4.
1. Trie la liste d’éléments de catalogue par horodatage de validation.
1. Traiter chaque élément de catalogue dans l’ordre :
   1. Télécharger et désérialiser l’élément de catalogue.
   1. Réagissez en fonction du type de l’élément de catalogue.
   1. Traitez le document d’élément de catalogue de manière spécifique au client.
1. Enregistrez le dernier horodatage de validation de l’élément de catalogue en tant que nouvelle valeur de curseur.

Avec cet algorithme de base, l’implémentation cliente peut générer une vue complète de tous les packages disponibles sur la source du package. Le client doit uniquement exécuter régulièrement cet algorithme pour connaître toujours les dernières modifications apportées à la source du package.

> [!Note]
> Il s’agit de l’algorithme utilisé par nuget.org pour conserver les [métadonnées du package](registration-base-url-resource.md), le [contenu du package](package-base-address-resource.md), la [recherche](search-query-service-resource.md) et la [saisie semi-automatique](search-autocomplete-service-resource.md) des ressources à jour.

### <a name="dependent-cursors"></a>Curseurs dépendants

Supposons que deux clients de catalogue possèdent une dépendance inhérente où la sortie d’un client dépend de la sortie d’un autre client. 

#### <a name="example"></a>Exemple

Par exemple, sur nuget.org, un package qui vient d’être publié ne doit pas apparaître dans la ressource de recherche avant d’apparaître dans la ressource de métadonnées du package. Cela est dû au fait que l’opération de « restauration » effectuée par le client NuGet officiel utilise la ressource de métadonnées du package. Si un client Découvre un package à l’aide du service de recherche, il doit être en mesure de restaurer ce package à l’aide de la ressource de métadonnées du package. En d’autres termes, la ressource de recherche dépend de la ressource de métadonnées du package. Chaque ressource a une tâche en arrière-plan du client du catalogue qui met à jour cette ressource. Chaque client possède son propre curseur.

Étant donné que les deux ressources sont créées à partir du catalogue, le curseur du client de catalogue qui met à jour la ressource de recherche *ne doit pas dépasser* le curseur du client du catalogue de métadonnées du package.

#### <a name="algorithm"></a>Algorithm

Pour implémenter cette restriction, il vous suffit de modifier l’algorithme ci-dessus pour qu’il soit :

1. Extrait la valeur de curseur enregistrée à partir d’un magasin local.
1. Téléchargez et désérialisez l’index du catalogue.
1. Recherche toutes les pages du catalogue dont l’horodateur de validation est *supérieur* au curseur **inférieur ou égal au curseur de la dépendance.**
1. Déclarez une liste vide d’éléments de catalogue à traiter.
1. Pour chaque page de catalogue correspondante à l’étape 3 :
   1. Téléchargez et désérialisez la page catalogue.
   1. Recherche tous les éléments du catalogue dont l’horodateur de validation est *supérieur* **ou égal au curseur de la dépendance.**
   1. Ajoutez tous les éléments de catalogue correspondants à la liste déclarée à l’étape 4.
1. Trie la liste d’éléments de catalogue par horodatage de validation.
1. Traiter chaque élément de catalogue dans l’ordre :
   1. Télécharger et désérialiser l’élément de catalogue.
   1. Réagissez en fonction du type de l’élément de catalogue.
   1. Traitez le document d’élément de catalogue de manière spécifique au client.
1. Enregistrez le dernier horodatage de validation de l’élément de catalogue en tant que nouvelle valeur de curseur.

À l’aide de cet algorithme modifié, vous pouvez créer un système de clients de catalogue dépendants qui produisent tous leurs propres index, artefacts, etc.
