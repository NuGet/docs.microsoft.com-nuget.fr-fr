---
title: Limites du taux de transfert, API NuGet
description: Les API NuGet auront des limites de débit imposées pour empêcher tout abus.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367932"
---
# <a name="rate-limits"></a>Limites du débit

L’API NuGet.org applique la limitation du débit pour empêcher tout abus. Les demandes qui dépassent la limite de débit retournent l’erreur suivante : 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

En plus de la limitation des demandes à l’aide de limites de débit, certaines API appliquent également le quota. Les demandes qui dépassent le quota renvoient l’erreur suivante :

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Les tableaux suivants répertorient les limites de taux de transfert pour l’API NuGet.org.

## <a name="package-search"></a>Recherche de packages

> [!Note]
> Nous vous recommandons d’utiliser les [API de recherche v3](search-query-service-resource.md) de NuGet. org, car elles ne sont pas limitées au tarif actuellement. Pour les API de recherche v1 et v2, les limites suivantes s’appliquent :

| API | Type de limite | Valeur limite | Cas d’usage d’API |
|:---|:---|:---|:---|
En **savoir** plus`/api/v1/Packages` | IP | 1000/minute | Interroger les métadonnées du package NuGet via la collection OData v1 `Packages` |
En **savoir** plus`/api/v1/Search()` | IP | 3000/minute | Rechercher des packages NuGet via le point de terminaison de recherche v1 | 
En **savoir** plus`/api/v2/Packages` | IP | 20000/minute | Interroger les métadonnées du package NuGet via la collection OData v2 `Packages` | 
En **savoir** plus`/api/v2/Packages/$count` | IP | 100/minute | Interroger le nombre de packages NuGet via la collection OData v2 `Packages` | 

## <a name="package-push-and-unlist"></a>Push et Unlist des packages

| API | Type de limite | Valeur limite | Cas d’usage d’API | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Clé de l’API | 350/heure | Télécharger un nouveau package NuGet (version) via un point de terminaison Push v2 
**Supprimer**`/api/v2/package/{id}/{version}` | Clé de l’API | 250/heure | Délister un package NuGet (version) via un point de terminaison v2 

## <a name="nugetorg-website-page-views"></a>affichages de pages de site Web nuget.org

Si vous accédez aux pages Web nuget.org par programme, envisagez d’examiner nos [API V3](overview.md)documentées. Ces points de terminaison permettent un accès plus simple aux métadonnées et au contenu des packages. L’API V3 offre une meilleure disponibilité et offre des performances supérieures à celles des pages Web de la galerie NuGet, qui sont conçues pour l’interaction du navigateur Web.

| API | Type de limite | Valeur limite | Cas d’usage d’API | 
|:---|:---|:---|:--- |
En **savoir** plus`/package/{id}/{version}` | IP | 50/minute | Affichez la page des détails du package (version). 
