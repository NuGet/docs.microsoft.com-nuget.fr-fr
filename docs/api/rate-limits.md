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
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813193"
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

| API | Type de limite | Valeur limite | UseCase d’API |
|:---|:---|:---|:---|
**Recevoir** `/api/v1/Packages` | IP | 1000/minute | Interroger les métadonnées du package NuGet via v1 OData `Packages` collection |
**Recevoir** `/api/v1/Search()` | IP | 3000/minute | Rechercher des packages NuGet via le point de terminaison de recherche v1 | 
**Recevoir** `/api/v2/Packages` | IP | 20000/minute | Interroger les métadonnées du package NuGet via v2 OData `Packages` collection | 
**Recevoir** `/api/v2/Packages/$count` | IP | 100/minute | Interroger le nombre de packages NuGet via la collecte de `Packages` OData v2 | 

## <a name="package-push-and-unlist"></a>Push et Unlist des packages

| API | Type de limite | Valeur limite | UseCase d’API | 
|:---|:---|:---|:--- |
**Placer** `/api/v2/package` | Clé API | 350/heure | Télécharger un nouveau package NuGet (version) via un point de terminaison Push v2 
**Supprimer** `/api/v2/package/{id}/{version}` | Clé API | 250/heure | Délister un package NuGet (version) via un point de terminaison v2 
