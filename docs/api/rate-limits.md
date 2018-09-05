---
title: Limites, NuGet API du taux
description: Les APIs NuGet sera ont appliqué les limites de débit pour empêcher les abus.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548675"
---
# <a name="rate-limits"></a>Limites du débit

L’API de NuGet.org applique la limitation du débit pour empêcher les abus. Requêtes qui dépassent la limite de débit renvoient l’erreur suivante : 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

En plus de la demande à l’aide des limites de taux de limitation, certaines API également appliquent des quotas. Requêtes qui dépassent le quota renvoient l’erreur suivante :

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Les tableaux suivants répertorient les limites de taux pour l’API de NuGet.org.

## <a name="package-search"></a>Recherche de package

> [!Note]
> Nous recommandons l’utilisation de NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) pour recherche performante et n’avez aucune limite actuellement. API de recherche pour V1 et V2, les limites followins s’appliquent :


| API | Type de limite | Valeur de la limite | API CasUtilisation |
|:---|:---|:---|:---|
**TÉLÉCHARGER** `/api/v1/Packages` | IP | 1000 / minute | Interroger les métadonnées de package NuGet via OData de v1 `Packages` collection |
**TÉLÉCHARGER** `/api/v1/Search()` | IP | 3000 / minute | Rechercher des packages NuGet via le point de terminaison v1 recherche | 
**TÉLÉCHARGER** `/api/v2/Packages` | IP | 20000 / minute | Interroger les métadonnées de package NuGet via OData de v2 `Packages` collection | 
**TÉLÉCHARGER** `/api/v2/Packages/$count` | IP | 100 / minute | Interroger le nombre de packages NuGet via OData de v2 `Packages` collection | 

## <a name="package-push-and-unlist"></a>Package Push et de retirer de la liste

| API | Type de limite | Valeur de la limite | API CasUtilisation | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Clé API | 250 / heure | Charger un nouveau package NuGet (version) via le point de terminaison v2 push 
**SUPPRIMER** `/api/v2/package/{id}/{version}` | Clé API | 250 / heure | Retirer de la liste un package NuGet (version) via le point de terminaison v2 
