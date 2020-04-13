---
title: Suppression de packages NuGet de nuget.org
description: Stratégies de retrait de packages de nuget.org ; la suppression définitive n’est pas prise en charge, sauf quand les packages ne respectent pas les autres stratégies.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581263"
---
# <a name="deleting-packages"></a>Supprimer des packages

NuGet.org ne prend pas en charge la suppression définitive de packages. Cela compromettrait chaque projet dépendant de la disponibilité du package, en particulier dans le cas des workflows de build qui impliquent la restauration du package.

nuget.org prend en charge le [déballage d’un paquet,](#unlisting-a-package)ce qui peut être fait dans la page de gestion du paquet sur le site Web. Les packages supprimés de la liste n’apparaissent ni sur nuget.org ni dans l’interface utilisateur de Visual Studio, ni dans les résultats d’une recherche. Toutefois, vous pouvez quand même les télécharger et les installer en utilisant un numéro de version exact qui prend en charge la restauration des packages. De plus, il est toujours possible de découvrir les packages supprimés de la liste dans les scénarios spécifiques suivants :

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

## <a name="unlisting-a-package"></a>Déballage d’un paquet
La nonlistation d’une version de paquet la cache de la recherche et de nuget.org page de détails de paquet. Cela permet aux utilisateurs existants du paquet de continuer à l’utiliser, mais réduit l’adoption nouvelle puisque le paquet n’est pas visible à la recherche.

Étapes pour déballer un paquet :

1. Sélectionnez `Your account name` (dans le coin supérieur droit) >`Manage packages` > `Published packages`
1. Sélectionnez l’icône "Manage package"
1. Élargir la section «Listing» et sélectionner la version du paquet
1. Décochez la « Liste des résultats de recherche » et sélectionnez « Enregistrer »

La version de paquet spécifique n’a plus été répertoriée. Afin de vérifier cela, logout de votre compte et naviguer vers la page https://www.nuget.org/packages/YOUR-PACKAGE-NAME/de paquet (sans la partie version) par exemple: . Vous verrez toutes les versions de ce paquet qui **n’ont pas** été non cotées. Cependant, le propriétaire du paquet, lorsqu’il est connecté, peut voir toutes les versions et leur statut d’inscription.

Il est également possible de déprécier une version de paquet (au cas où vous ne pouvez pas supprimer une version de paquet). Pour plus d’informations sur la dépréciation des versions de paquets, voir [Les paquets Deprecating](../deprecate-packages.md).
