---
title: Limites du taux de | Documents Microsoft
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Les APIs NuGet sera ont appliqué les limites de taux pour prévenir les abus.
keywords: Limitation du débit NuGet API,
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a>Limites du débit

L’API NuGet.org applique la limitation du débit pour prévenir les abus. Requêtes qui dépassent la limite du taux renvoient l’erreur suivante : 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Les tableaux suivants répertorient les limites de taux pour l’API NuGet.org.

## <a name="package-search"></a>Recherche de package

> [!Note]
> Nous vous recommandons d’utiliser des NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) pour la recherche est performant et n’avez aucune limite actuellement. Pour V1 et V2 les API de recherche, les limites followins s’appliquent :


| API | Type de limite | Valeur limite | API usecase |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000 / minute | Interroger les métadonnées de package NuGet via v1 OData `Packages` collection |
**GET** `/api/v1/Search()` | IP | 3000 / minute | Rechercher les packages NuGet via le point de terminaison recherche v1 | 
**GET** `/api/v2/Packages` | IP | 20000 / minute | Interroger les métadonnées de package NuGet via v2 OData `Packages` collection | 
**GET** `/api/v2/Packages/$count` | IP | 100 / minute | Nombre de package NuGet via v2 OData de requête `Packages` collection | 

## <a name="package-push-and-unlist"></a>Package Push et de retrait de la liste

| API | Type de limite | Valeur limite | APU usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Clé API | 100 / minute | Téléchargez un nouveau package NuGet (version) via le point de terminaison par émission de données v2 
**SUPPRIMER** `/api/v2/package/{id}/{version}` | Clé API | 100 / minute | Retrait de la liste un package NuGet (version) via le point de terminaison v2 
