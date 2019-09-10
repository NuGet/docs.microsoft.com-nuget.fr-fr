---
title: Réservation du préfixe d’ID
description: Description de la fonctionnalité Réservation du préfixe d’ID de package et guide de création.
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: 630c2b193500ec0b9aa5a7fe4af3ea95ae52aeec
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815281"
---
# <a name="package-id-prefix-reservation"></a>Réservation du préfixe d’ID de package

Les propriétaires de packages peuvent réserver et protéger leur identité en réservant des préfixes d’ID. Durant l’installation d’un package, les consommateurs reçoivent des informations supplémentaires indiquant que les propriétés d’identification du package qu’ils consomment ne sont pas trompeuses. 

[NuGet.org](https://www.nuget.org/) et Visual Studio 2017 version 15.4 ou ultérieure affichent un indicateur visuel pour les packages soumis par les propriétaires avec un préfixe d’ID de package réservé, et ce tant que le package correspond au modèle de nommage du préfixe d’ID réservé. La référence ci-dessous explique en quoi consiste la réservation d’un préfixe d’ID et comment un propriétaire peut demander un préfixe d’ID.

## <a name="id-prefix-reservation-details"></a>Détails de la réservation de préfixe d’ID

Quand un préfixe d’ID de package est réservé, plusieurs choses se produisent dans la galerie [nuget.org](https://www.nuget.org/) et dans Visual Studio. Les réservations de préfixe d’ID prennent également en charge des scénarios avancés, notamment la définition d’un préfixe « public » et la délégation de sous-ensembles de préfixes à plusieurs propriétaires.

### <a name="id-prefix-reservation-on-nugetorg"></a>Réservation de préfixe d’ID sur nuget.org

Quand un préfixe est réservé sur [nuget.org](https://www.nuget.org/), voilà ce qui se produit :

1. Une réservation de préfixe est associée à un propriétaire ou à un ensemble de propriétaires sur [nuget.org](https://www.nuget.org/).

1. Chaque fois qu’un package est soumis à [nuget.org](https://www.nuget.org/) avec un ID correspondant au préfixe d’ID réservé, le package est rejeté, sauf s’il provient du ou des propriétaires ayant réservé le préfixe d’ID.

1. Tout package correspondant au préfixe d’ID réservé et provenant du ou des propriétaires ayant réservé le préfixe d’ID comporte un indicateur visuel dans Visual Studio 2017 version 15.4 ou ultérieure ainsi que sur [nuget.org](https://www.nuget.org/) pour signaler que le package est associé à un préfixe d’ID réservé. Cela vaut pour les nouvelles soumissions de package ainsi que pour les packages existants sous le ou les propriétaires. **Remarque :** L’indicateur dans Visual Studio apparaît uniquement si un flux unique est sélectionné comme source du package.

1. Tous les packages existants qui correspondent au préfixe d’ID réservé, mais qui *ne sont pas* détenus par le propriétaire du préfixe réservé restent inchangés (ils ne sont pas supprimés de la liste, mais ils n’ont pas non plus d’indicateur visuel). De plus, les propriétaires de ces packages peuvent toujours soumettre de nouvelles versions au package.

Ces changements sont basés sur les conditions suivantes et imposent plusieurs restrictions supplémentaires :

- Il suffit qu’un propriétaire de package ait le préfixe réservé pour que l’indicateur visuel apparaisse (pour les packages ayant plusieurs propriétaires).

- Si un package compte plusieurs propriétaires et que certains ont le préfixe réservé et d’autres pas, seuls ceux ayant le préfixe réservé peuvent supprimer d’autres propriétaires ayant un préfixe réservé. Les propriétaires qui n’ont pas le préfixe réservé ne peuvent pas supprimer les propriétaires ayant ce préfixe. Ils peuvent toutefois supprimer ceux qui n’ont pas non plus le préfixe réservé.

- Une fois qu’un package a l’indicateur visuel, il doit *toujours* l’avoir (ce qui garantit l’existence d’au moins un propriétaire avec le préfixe réservé).

### <a name="advanced-prefix-reservation-scenarios"></a>Scénarios de réservation de préfixe avancés

Plusieurs scénarios de réservation de préfixe plus avancés sont décrits ci-dessous, notamment la délégation de sous-préfixes et le marquage de ces derniers comme étant publics. Vous trouverez ci-dessous les réservations de préfixe plus avancées qui peuvent être effectuées. 

- Durant la réservation du préfixe, le propriétaire peut demander la délégation de sous-ensembles de préfixes (ou du préfixe) à d’autres propriétaires. Par exemple, si « [Microsoft](https://www.nuget.org/profiles/microsoft) » détient « Microsoft.\* », mais que « [aspnet](https://www.nuget.org/profiles/aspnet) » souhaite réserver « Microsoft.AspNet.\* », « [Microsoft](https://www.nuget.org/profiles/microsoft) » peut choisir de déléguer « Microsoft.AspNet.\* » au compte [aspnet](https://www.nuget.org/profiles/aspnet).

- Durant la réservation du préfixe, le propriétaire peut choisir de rendre un préfixe public. Il obtient encore l’indicateur visuel montrant que le package provient d’un préfixe réservé, mais les soumissions de package futures sur le préfixe **ne sont pas bloquées**, et ce quel que soit le propriétaire. Ceci est utile pour les projets open source comptant de nombreux contributeurs : le préfixe peut être réservé pour les contributeurs principaux, mais il peut rester ouvert à tous les contributeurs. 

### <a name="prefix-reservation-visual-indicator"></a>Indicateur visuel de réservation de préfixe

Si un package provient d’un préfixe réservé, vous voyez les indicateurs visuels ci-dessous dans la galerie [nuget.org](https://www.nuget.org/) et dans Visual Studio 2017 version 15.4 ou ultérieure :

**Galerie NuGet.org**
![Galerie nuget.org](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Processus de demande d’une réservation de préfixe d’ID

1. Passez en revue les [critères d’acceptation pour la réservation d’ID de préfixe](#id-prefix-reservation-criteria).

2. Déterminez les préfixes que vous souhaitez réserver en plus des [scénarios de réservation de préfixe avancés](#advanced-prefix-reservation-scenarios) dont vous pouvez avoir besoin.

3. Envoyez un e-mail à [account@nuget.org](mailto:account@nuget.org) avec le nom complet du propriétaire sur [nuget.org](https://www.nuget.org/), ainsi que tous les préfixes réservés que vous demandez. Si vous déléguez des sous-ensembles de préfixes à plusieurs propriétaires, veillez à mentionner tous les noms complets et sous-ensembles de préfixes des propriétaires.

Une fois la demande soumise, vous êtes notifié de son acceptation ou de son rejet (avec les critères ayant provoqué le rejet). Il nous arrive de poser des questions d’identification supplémentaires pour confirmer l’identité du propriétaire.

### <a name="id-prefix-reservation-criteria"></a>Critères de réservation de préfixe d’ID

Au cours de l’examen d’une demande de réservation de préfixe d’ID, l’équipe de [nuget.org](https://www.nuget.org/) évalue l’application par rapport aux critères ci-dessous. Tous les critères ne doivent pas nécessairement être remplis pour qu’un préfixe soit réservé, mais la demande peut être refusée s’il n’y a pas de preuve substantielle que les critères sont remplis (une explication est donnée) :

1. Le préfixe d’ID de package identifie-t-il correctement et clairement le propriétaire du package ?

1. Le propriétaire du package a-t-il [activé 2FA pour son compte NuGet.org](individual-accounts.md#enable-two-factor-authentication-2fa) ?

1. Le propriétaire a-t-il déjà soumis un nombre important de packages sous le préfixe d’ID de package ?

1. Le préfixe d’ID de package est-il un élément commun qui n’est pas censé appartenir à un propriétaire ou à une organisation ?

1. Le fait de *ne pas* réserver le préfixe d’ID de package serait-il source d’ambiguïté et de confusion pour la communauté ?

1. Les propriétés d’identification des packages qui correspondent au préfixe d’ID de package sont-elles claires et cohérentes (en particulier l’auteur du package) ?

1. Les packages ont-ils une licence (qui utilise l’élément de métadonnées [license](../reference/nuspec.md#license) et non licenseUrl qui est déprécié) ?

1. Si les packages ont une icône (à l’aide de l’élément de métadonnées iconUrl), sont-ils également en utilisant l’élément de métadonnées d' [icône](../reference/nuspec.md#icon) (il n’est pas nécessaire de supprimer le IconUrl) ?

## <a name="third-party-feed-provider-scenarios"></a>Scénarios faisant appel à un fournisseur de flux tiers

Si un fournisseur de flux tiers souhaite implémenter son propre service pour fournir des réservations de préfixe, modifiez le service de recherche dans les fournisseurs de flux NuGet V3. Pour cela, ajoutez la propriété *verified* au service de recherche de flux (voir les exemples pour les flux V3 ci-dessous). Le client NuGet ne prend pas en charge la propriété ajoutée dans le flux V2.

Pour plus d’informations, consultez la [documentation sur le service de recherche de l’API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Stratégie de contestation de la réservation de préfixe d’ID de package
Si vous pensez qu’un propriétaire sur [NuGet.org](https://www.nuget.org) s’est vu attribuer une réservation de préfixe d’ID de package qui va à l’encontre des critères listés ci-dessus ou qui enfreint des marques ou des copyrights, envoyez un e-mail à [support@nuget.org](mailto:support@nuget.org) avec le préfixe d’ID en question, le propriétaire du préfixe d’ID et la raison de la contestation de la réservation de préfixe attribuée.

