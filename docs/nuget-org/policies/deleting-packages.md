---
title: Suppression de packages NuGet de nuget.org
description: Stratégies de retrait de packages de nuget.org ; la suppression définitive n’est pas prise en charge, sauf quand les packages ne respectent pas les autres stratégies.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 574ee874e2d6555a2e3e0a0643962e33b7ec1b09
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859445"
---
# <a name="deleting-packages"></a>Supprimer des packages

NuGet.org ne prend pas en charge la suppression définitive de packages. Cela compromettrait chaque projet dépendant de la disponibilité du package, en particulier dans le cas des workflows de build qui impliquent la restauration du package.

nuget.org ne prend pas en charge l’annulation de la [liste d’un package](#unlisting-a-package), ce qui peut être fait dans la page de gestion des packages sur le site Web. Les packages supprimés de la liste n’apparaissent ni sur nuget.org ni dans l’interface utilisateur de Visual Studio, ni dans les résultats d’une recherche. Toutefois, vous pouvez quand même les télécharger et les installer en utilisant un numéro de version exact qui prend en charge la restauration des packages. De plus, il est toujours possible de découvrir les packages supprimés de la liste dans les scénarios spécifiques suivants :

- Restauration de packages à l’aide de versions flottantes (par exemple, `1.0.0-*`), si le dernier package disponible correspondant aux contraintes de version ou dépendance est un package supprimé de la liste.
- Réplication des packages par le biais du catalogue (qui, lui aussi, contient des packages supprimés de la liste).

## <a name="exceptions"></a>Exceptions

Dans des situations exceptionnelles, comme la violation de droits d’auteur et la présence de contenu potentiellement dangereux, les packages peuvent être supprimés manuellement par l’équipe NuGet. Vous pouvez signaler un package à l’aide du bouton « Signaler un abus » disponible dans la page Détails du package sur NuGet.org. Si vous êtes le propriétaire du package, connectez-vous à votre compte NuGet.org pour accéder à la prise en charge de NuGet. Pour cela, utilisez le bouton « Contacter le support » disponible dans la page Détails du package sur NuGet.org.

## <a name="prohibited-use"></a>Utilisation interdite

Les packages qui répondent aux critères suivants ne sont pas autorisés dans la galerie NuGet publique et sont immédiatement supprimés sans discussion. Toutefois, les propriétaires des packages sont informés de leur suppression.

- Contiennent des programmes malveillants, des logiciels de publicité ou tout type de logiciels espions.
- Sont conçus pour endommager la station de travail d’un développeur ou son organisation.
- Violent les droits d’auteur ou les licences.
- Contiennent du contenu illégal.
- Sont utilisés pour monopoliser les identificateurs de package, y compris les packages totalement dépourvus de contenu de production. Les packages doivent contenir du code ou les propriétaires doivent concéder l’identificateur à une personne qui a effectivement un produit à livrer.
- Essaient de faire faire à la galerie une opération pour laquelle elle n’est pas explicitement conçue.

Si vous détectez un package qui contrevient à l’un de ces éléments, cliquez sur le lien **Signaler un abus** sur la page de détails du package et envoyez un rapport.

Notez que l’équipe NuGet et la .NET Foundation se réservent le droit de changer ces critères à tout moment.

## <a name="unlisting-a-package"></a>Délister un package
La désaffichage d’une version de package la masque à partir de la page de détails de la recherche et du package nuget.org. Cela permet aux utilisateurs existants du package de continuer à l’utiliser, tout en réduisant les nouvelles adoptions, car le package n’est pas visible dans la recherche.

Étapes pour délister un package :

1. Sélectionnez `Your account name` (dans le coin supérieur droit) >`Manage packages` > `Published packages`
1. Sélectionner l’icône « gérer le package »
1. Développez la section « Listing » et sélectionnez la version du package
1. Désactivez la case à cocher « liste dans les résultats de la recherche », puis sélectionnez « Enregistrer ».

La version du package spécifique est désormais non listée. Pour vérifier cela, déconnectez-vous de votre compte et accédez à la page du package (sans la partie version), par exemple : https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ . Toutes les versions de ce package ne s’affichent **pas** dans la liste. Toutefois, le propriétaire du package, une fois connecté, peut voir toutes les versions et leur état de liste.

Il est également possible de déprécier une version de package (dans le cas où vous ne pouvez pas supprimer une version de package). Pour plus d’informations sur la dépréciation des versions de packages, consultez [dépréciation de packages](../deprecate-packages.md).
