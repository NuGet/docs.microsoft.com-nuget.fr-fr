---
title: Suppression de packages NuGet de nuget.org | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Stratégies de retrait de packages de nuget.org ; la suppression définitive n’est pas prise en charge, sauf quand les packages ne respectent pas les autres stratégies."
keywords: suppression de packages NuGet, suppression de packages NuGet de la liste, utilisations interdites des packages
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6169e46e55176757bc1ad471a3d80885cb50e403
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="deleting-packages"></a>Suppression de packages

NuGet.org ne prend pas en charge la suppression définitive de packages. Cela compromettrait chaque projet dépendant de la disponibilité du package, en particulier dans le cas des workflows de build qui impliquent la restauration du package.

NuGet.org prend en charge *la suppression d’un package de la liste*, opération qui peut être effectuée dans la page de gestion des packages sur le site web. Les packages supprimés de la liste n’apparaissent ni sur nuget.org ni dans l’interface utilisateur de Visual Studio, ni dans les résultats d’une recherche. Toutefois, vous pouvez quand même les télécharger et les installer en utilisant un numéro de version exact qui prend en charge la restauration des packages. De plus, il est toujours possible de découvrir les packages supprimés de la liste dans les scénarios spécifiques suivants :

- Restauration de packages à l’aide de versions flottantes (par exemple, `1.0.0-*`), si le dernier package disponible correspondant aux contraintes de version ou dépendance est un package supprimé de la liste.
- Réplication des packages par le biais du catalogue (qui, lui aussi, contient des packages supprimés de la liste).

## <a name="exceptions"></a>Exceptions

Dans des situations exceptionnelles, comme la violation de droits d’auteur et la présence de contenu potentiellement dangereux, les packages peuvent être supprimés manuellement par l’équipe NuGet. Envoyez une demande de support par le biais de la [Galerie NuGet](http://www.nuget.org) pour démarrer la procédure.

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
