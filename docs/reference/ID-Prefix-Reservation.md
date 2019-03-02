---
title: Référence de réservation de préfixe d’identificateur
description: Description de fonction de réservation de préfixe d’ID de package et le guide de l’auteur.
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e8b902c89427333afb7a27ee9de0eeb99a92f391
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225873"
---
# <a name="package-id-prefix-reservation"></a>Réservation de préfixe ID de package

Propriétaires de packages peuvent de réserver et de protéger leur identité par les préfixes d’ID de réservation. Consommateurs de packages sont fournis avec des informations supplémentaires lors de la consommation des packages qui le package qu’ils consomment ne sont pas trompeurs dans leurs propriétés d’identification. 

[NuGet.org](https://www.nuget.org/) et Visual Studio 2017 version 15.4 ou ultérieure afficher un indicateur visuel pour le modèle d’affectation de noms du préfixe de packages qui sont soumises par les propriétaires avec un préfixe d’ID de package réservé, tant que le package correspond à l’ID réservé. Le ci-dessous référence explique ce qui implique la réservation de préfixe d’ID, et comment il peut appliquer un propriétaire pour un préfixe d’identificateur.

## <a name="id-prefix-reservation-details"></a>Détails de la réservation préfixe ID

Lorsqu’un préfixe d’ID de package est réservé, plusieurs choses se produisent sur le [nuget.org](https://www.nuget.org/) galerie, ainsi que dans Visual Studio. En outre, il existe des scénarios sont pris en charge par les réservations de préfixe d’ID, telles que la définition d’un préfixe sous la forme 'public', déléguer des sous-ensembles de préfixe à plusieurs propriétaires.

### <a name="id-prefix-reservation-on-nugetorg"></a>Réservation du préfixe ID sur nuget.org

Quand un préfixe est réservé sur [nuget.org](https://www.nuget.org/), ce qui suit se produit :

1. Une réservation de préfixe est associée à un propriétaire ou un ensemble de propriétaires sur [nuget.org](https://www.nuget.org/).

1. Chaque fois qu’un package est soumis à [nuget.org](https://www.nuget.org/) avec un ID qui correspond au préfixe d’identificateur réservé, le package est rejeté, sauf si elle provient de propriétaires qui a réservé le préfixe d’ID.

1. N’importe quel package qui correspond le préfixe d’identificateur réservé et provient de propriétaires qui a réservé le préfixe d’ID aura un indicateur visuel dans Visual Studio 2017 version 15.4 ou ultérieure et sur [nuget.org](https://www.nuget.org/) indiquant que le package est sous un préfixe d’identificateur réservé. Cela est vrai pour les nouvelles soumissions de package ainsi que des packages existants sous les propriétaires. **Remarque :** L’indicateur dans Visual Studio apparaît uniquement si un flux unique est sélectionné comme source du package.

1. Tous les packages existants qui correspondent au préfixe d’ID réservé, mais sont *pas* appartenant au propriétaire de réservée préfixe restera inchangé (ils ne seront pas retirée de la liste, mais ils ne disposeront également l’indicateur visuel). En outre, les propriétaires de ces packages sera toujours en mesure de soumettre de nouvelles versions du package.

Ces modifications sont basées sur les conditions suivantes et imposent plusieurs restrictions supplémentaires :

- Qu’un seul propriétaire d’un package doit avoir le préfixe réservé pour l’indicateur visuel à afficher (pour les packages avec les propriétaires de plusieurs).

- S’il existe plusieurs propriétaires d’un package dans lequel un ou plusieurs propriétaires a le préfixe réservé et un ou plusieurs propriétaires n’a pas le préfixe réservé, propriétaires uniquement par le préfixe réservé peuvent supprimer les autres propriétaires avec un préfixe réservé. Les propriétaires qui n’ont pas le préfixe réservé ne peut pas supprimer des propriétaires avec le préfixe réservé. Ils peuvent toujours supprimer les autres propriétaires qui n’ont pas le préfixe réservé.

- Une fois qu’un package a l’indicateur visuel, il le devrait *toujours* ont l’indicateur visuel (ce qui garantit qu’au moins un propriétaire par le préfixe réservé restera toujours un propriétaire)

### <a name="advanced-prefix-reservation-scenarios"></a>Scénarios de réservation de préfixe avancées

Il existe plusieurs scénarios de réservation préfixe plus avancées décrites ci-dessous, y compris la délégation de subprefix et des préfixes de marquage comme étant public. Voici les réservations de préfixe plus avancées qui peuvent être apportées. 

- Au cours de la réservation du préfixe, le propriétaire peut demander délégation de sous-ensembles de préfixe (ou le préfixe) aux autres propriétaires. Par exemple, si «[Microsoft](https://www.nuget.org/profiles/microsoft)' possède ' Microsoft.\*', mais '[aspnet](https://www.nuget.org/profiles/aspnet)' souhaite réserver ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' peut choisir de déléguer ' Microsoft.AspNet. \*» à la [aspnet](https://www.nuget.org/profiles/aspnet) compte.

- Au cours de la réservation du préfixe, le propriétaire peut choisir de rendre un préfixe public. Cela sera toujours leur donner l’indicateur visuel montrant que le package provient d’un préfixe réservé, mais il sera **pas** bloquer soumissions ultérieures du package sur le préfixe pour n’importe quel propriétaire. Cela est utile pour les projets open source avec de nombreux contributeurs : les contributeurs de haut ou core peuvent avoir le préfixe réservé, mais il peut toujours être ouverte à tous les collaborateurs. 

### <a name="prefix-reservation-visual-indicator"></a>Indicateur visuel de réservation de préfixe

Si un package proviennent d’un préfixe réservé, vous voyez le dessous des indicateurs visuels sur le [nuget.org](https://www.nuget.org/) galerie et dans Visual Studio 2017 version 15.4 ou ultérieure :

**Galerie NuGet.org**
![galerie nuget.org](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Processus d’application ID préfixe réservation

1. Passez en revue l’acceptation [critères pour la réservation du préfixe ID](#id-prefix-reservation-criteria).

2. Déterminer les préfixes que vous souhaitez réserver, en plus [des scénarios de réservation de préfixe avancés](#advanced-prefix-reservation-scenarios) vous pouvez avoir besoin.

3. Envoyer un e-mail à [ account@nuget.org ](mailto:account@nuget.org) avec le propriétaire du nom d’affichage sur [nuget.org](https://www.nuget.org/), ainsi que tous les préfixes réservés que vous demandez. Si vous déléguez des sous-ensembles de préfixe à plusieurs propriétaires, assurez-vous que vous indiquez tous les noms complets de propriétaire et des sous-ensembles de préfixe.

Une fois l’application est envoyée, vous êtes informé de l’acceptation ou le rejet (avec les critères qui a provoqué le rejet). Nous devons poser des questions d’identification pour confirmer l’identité du propriétaire.

### <a name="id-prefix-reservation-criteria"></a>Critères de réservation de préfixe ID

Lors de la révision de toute application de réservation de préfixe d’ID, le [nuget.org](https://www.nuget.org/) équipe évaluera l’application contre les critères ci-dessous. Pas tous les critères doit être remplie pour un préfixe à réserver, mais l’application peut être refusée si on n'a pas les critères respectés (avec une explication donnée) :

1. Le préfixe d’ID de package correctement et clairement identifie le propriétaire du package ?

1. Sont un nombre important des packages qui ont déjà été soumises par le propriétaire sous le préfixe d’ID de package ?

1. Est le préfixe d’ID de package commun qui ne doivent pas appartenir à n’importe quel propriétaire individuel ou une organisation ?

1. Voulez-vous *pas* réservant le préfixe d’ID de package entraînent une ambiguïté et source de confusion pour la Communauté ?

1. Sont les propriétés d’identification des packages qui correspondent au préfixe de ID de package clair et cohérent (en particulier l’auteur du package) ?

1. Les packages ont une licence (à l’aide de la [licence](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license) métadonnées élément et licenseUrl pas devenu obsolète) ?

## <a name="third-party-feed-provider-scenarios"></a>Scénarios de fournisseur de flux de tiers

Si un tiers fournisseur de flux est souhaitent implémenter leur propre service pour fournir les réservations de préfixe, vous pouvez le faire en modifiant le service de recherche dans le NuGet V3 flux fournisseurs. L’ajout dans le service de recherche de flux consiste à ajouter le *vérifié* propriété, avec des exemples pour les flux V3 ci-dessous. Le client NuGet ne prendra pas en charge l’ajout de la propriété dans le flux de V2.

Pour plus d’informations, consultez le [documentation sur le service de recherche de l’API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Stratégie de litige de réservation de préfixe d’identificateur de package
Si vous pensez qu’un propriétaire sur [NuGet.org](https://www.nuget.org) a été affectée à une réservation de préfixe des ID de package qui va à l’encontre des critères listés ci-dessus, ou enfreint sur les marques déposées ou les droits d’auteur, veuillez e-mail [ support@nuget.org ](mailto:support@nuget.org)avec le préfixe d’ID en question, le propriétaire du préfixe d’ID et la raison pour contester la réservation du préfixe attribué.

