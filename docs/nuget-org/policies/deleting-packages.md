---
title: Suppression de packages NuGet de nuget.org
description: Stratégies de retrait de packages de nuget.org ; la suppression définitive n’est pas prise en charge, sauf quand les packages ne respectent pas les autres stratégies.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426974"
---
# <a name="deleting-packages"></a>Suppression de packages

NuGet.org ne prend pas en charge la suppression définitive de packages. Cela compromettrait chaque projet dépendant de la disponibilité du package, en particulier dans le cas des workflows de build qui impliquent la restauration du package.

NuGet.org prend en charge *la suppression d’un package de la liste*, opération qui peut être effectuée dans la page de gestion des packages sur le site web. Les packages supprimés de la liste n’apparaissent ni sur nuget.org ni dans l’interface utilisateur de Visual Studio, ni dans les résultats d’une recherche. Toutefois, vous pouvez quand même les télécharger et les installer en utilisant un numéro de version exact qui prend en charge la restauration des packages. De plus, il est toujours possible de découvrir les packages supprimés de la liste dans les scénarios spécifiques suivants :

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

Si vous trouvez un package qui enfreint un de ces éléments, cliquez sur le lien **Signaler un abus** dans la page des détails du package, puis envoyez un rapport.

Notez que l’équipe NuGet et la .NET Foundation se réservent le droit de changer ces critères à tout moment.
