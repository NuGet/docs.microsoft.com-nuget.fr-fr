---
title: Préfixe d’identificateur de réservation référence | Documents Microsoft
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Description de fonction de réservation du préfixe d’ID de package et le guide de l’auteur.
keywords: ID de package NuGet, préfixe, la réservation
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7b1956612bd48a1c59503418f1a4d7d9dee900f5
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="package-id-prefix-reservation"></a>Réservation de préfixe ID de package

Les propriétaires de package peuvent de réserver et protéger leur identité en réservant ID préfixes. Les consommateurs de package sont fournis avec des informations supplémentaires lors de l’utilisation de packages qui le package qu’ils consomment ne sont pas trompeurs dans leurs propriétés d’identification. 

[NuGet.org](https://www.nuget.org/) et Visual Studio 2017 15.4 ou version ultérieure afficher un indicateur visuel pour le modèle d’affectation de noms du préfixe de packages qui sont envoyés par les propriétaires avec un préfixe d’ID de package réservé, tant que le package correspond à l’ID réservé. Le ci-dessous référence explique ce qui implique la réservation du préfixe ID, et comment il peut appliquer un propriétaire pour un préfixe d’identificateur.

## <a name="id-prefix-reservation-details"></a>Détails de la réservation préfixe ID

Lorsqu’un préfixe d’ID de package est réservé, plusieurs choses se produisent sur le [nuget.org](https://www.nuget.org/) galerie, ainsi que dans Visual Studio. En outre, il sont des scénarios avancés qui sont pris en charge par les réservations de préfixe d’ID, telles que la définition d’un préfixe sous la forme 'public', déléguer des sous-ensembles de préfixe à plusieurs propriétaires.

### <a name="id-prefix-reservation-on-nugetorg"></a>Réservation de préfixe d’ID sur nuget.org

Lorsqu’un préfixe est réservé dans [nuget.org](https://www.nuget.org/), les éléments suivants se produit :

1. Une réservation de préfixe est associée un propriétaire ou un ensemble de propriétaires sur [nuget.org](https://www.nuget.org/).

1. Chaque fois qu’un lot est soumis au [nuget.org](https://www.nuget.org/) avec un ID qui correspond le préfixe d’identificateur réservé, le package est rejeté, sauf si elle provenance l’ou les propriétaires qui a réservé le préfixe d’ID.

1. N’importe quel package qui correspond le préfixe d’identificateur réservé et de provient l’ou les propriétaires qui a réservé le préfixe d’ID aura un indicateur visuel dans Visual Studio 2017 15.4 ou version ultérieure et sur [nuget.org](https://www.nuget.org/) indiquant que le package se trouve sous un préfixe d’identificateur réservé. Cela est vrai pour les nouvelles demandes de package ainsi que des packages existants sous l’ou les propriétaires. **Remarque :** l’indicateur dans Visual Studio apparaît uniquement si un flux unique est sélectionné comme source du package.

1. Tous les packages existants qui correspondent au préfixe d’ID réservé, mais sont *pas* appartenant au propriétaire de réservée préfixe reste inchangé (ils ne seront pas non répertoriées, mais ils ne disposeront également l’indicateur visuel). En outre, les propriétaires de ces packages sera en mesure de présenter les nouvelles versions du package.

Ces modifications sont basées sur les conditions suivantes et imposent des restrictions supplémentaires plusieurs :

- Qu’un seul propriétaire d’un package doit avoir le préfixe réservé pour l’indicateur visuel à afficher (pour les packages avec les propriétaires de multiple).

- S’il existe plusieurs propriétaires d’un package dans lequel un ou plusieurs propriétaires a le préfixe réservé et un ou plusieurs propriétaires n’a pas le préfixe réservé, l’ou les propriétaires uniquement par le préfixe réservé peut supprimer les autres concernée par un préfixe réservé. Les propriétaires qui n’ont pas le préfixe réservé ne peut pas supprimer les propriétaires par le préfixe réservé. Ils peuvent toujours supprimer des propriétaires qui également, n’ont pas le préfixe réservé.

- Une fois qu’un package a l’indicateur visuel, il doit *toujours* ont l’indicateur visuel (ce qui garantit qu’au moins un propriétaire par le préfixe réservé demeure un propriétaire)

### <a name="advanced-prefix-reservation-scenarios"></a>Scénarios de réservation de préfixe avancées

Il existe plusieurs scénarios de réservation préfixe plus avancées décrites ci-dessous, y compris subprefix délégation et des préfixes de marquage comme étant public. Vous trouverez ci-dessous les réservations de préfixe plus avancées qui peuvent être effectuées. 

- Au cours de la réservation du préfixe, le propriétaire peut demander la délégation des sous-ensembles de préfixe (ou le préfixe) aux autres propriétaires. Par exemple, si «[Microsoft](https://www.nuget.org/profiles/microsoft)' possède ' Microsoft.\*', mais '[aspnet](https://www.nuget.org/profiles/aspnet)' souhaite réserver ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' peut choisir de déléguer ' Microsoft.AspNet. \*' pour le [aspnet](https://www.nuget.org/profiles/aspnet) compte.

- Au cours de la réservation du préfixe, le propriétaire peut choisir rendre un préfixe public. Cela sera toujours leur donner l’indicateur visuel montrant que le package provient d’un préfixe réservé, mais il sera **pas** bloquer les soumissions futures du préfixe pour n’importe quel propriétaire. Cela est utile pour les projets open source avec nombreux collaborateurs - les contributeurs haut ou core peuvent avoir le préfixe réservé, mais il peut toujours être ouvert à tous les collaborateurs. 

### <a name="prefix-reservation-visual-indicator"></a>Indicateur visuel de réservation du préfixe

Si un package proviennent d’un préfixe réservé, vous voyez l’au-dessous des indicateurs visuels sur le [nuget.org](https://www.nuget.org/) la galerie et dans Visual Studio 2017 15.4 ou version ultérieure :

**Galerie de NuGet.org**
![nuget.org galerie](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Processus d’application ID préfixe réservation

1. Passez en revue l’acceptation [critères pour la réservation des ID de préfixe](#id-prefix-reservation-criteria).

1. Déterminer les espaces de noms que vous souhaitez réserver, outre les [préfixe réservation scénarios avancés](#advanced-prefix-reservation-scenarios) vous pouvez avoir besoin.

1. Envoyer un message électronique à [ account@nuget.org ](mailto:account@nuget.org) avec le propriétaire du nom d’affichage sur [nuget.org](https://www.nuget.org/), ainsi que tous les préfixes réservés que vous demandez. Si vous déléguez des sous-ensembles de préfixe à plusieurs propriétaires, assurez-vous que vous indiquez tous les noms complets de propriétaire et des sous-ensembles de préfixe.

Une fois l’application est envoyée, vous êtes informé de l’acceptation ou rejet (avec les critères qui a provoqué le rejet). Nous devons poser des questions d’identification supplémentaires pour confirmer l’identité du propriétaire.

### <a name="id-prefix-reservation-criteria"></a>Critères de réservation de préfixe ID

Lors de la consultation de toute application de réservation du préfixe ID, le [nuget.org](https://www.nuget.org/) équipe évaluera l’application contre les ci-dessous les critères. Pas tous les critères doit être remplie pour un préfixe à réserver, mais l’application peut être refusée s’il n’est pas une preuve importante des critères respectés (avec une explication donnée) :

1. Le préfixe d’ID de package correctement et clairement identifie le propriétaire du lot ?

1. Sont un nombre important des packages qui ont déjà été soumis par le propriétaire sous le préfixe d’ID de package ?

1. Est le préfixe d’ID de package commun ne doit pas appartenir à n’importe quel propriétaire individuel ou l’organisation ?

1. Serait *pas* réserver le préfixe d’ID de package entraînent une ambiguïté et toute confusion pour la Communauté ?

1. Sont les propriétés d’identification des packages qui correspondent au préfixe de ID de package clair et cohérent (notamment l’auteur du package) ?

## <a name="third-party-feed-provider-scenarios"></a>Scénarios de fournisseur de flux de tiers

Si un tiers fournisseur de flux est intéressé par l’implémentation de leur propre service pour fournir les réservations de préfixe, vous pouvez effectuer afin d’en modifiant le service de recherche dans la NuGet V3 flux fournisseurs. L’ajout du service de recherche de flux consiste à ajouter la *vérifié* propriété, avec des exemples de flux V3 ci-dessous. Le client NuGet ne prendra pas en charge la propriété ajoutée dans le flux de V2.

Pour plus d’informations, consultez la [plus d’informations sur le service de recherche de l’API](../api/search-query-service-resource.md).
