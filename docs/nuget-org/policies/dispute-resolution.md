---
title: Règlement des litiges autour des noms de packages NuGet
description: Processus de résolution des litiges entre les éditeurs de packages NuGet liés à la personnalisation, aux marques et autres situations de conflit.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 7e725d8114cde3de189dc3a648bc5a6c0b0e785b
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367945"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Résolution des litiges autour des noms de package NuGet

Cet article présente aux membres de la communauté un processus recommandé pour régler les litiges avec d’autres éditeurs NuGet.

Par exemple, supposons que Northwind Traders crée un système CRM pour lequel il fournit des pilotes clients sous la forme d’un fichier MSI téléchargeable à partir de son site web. Nancy, développeuse indépendante, souhaite faciliter l’utilisation de la bibliothèque cliente de Northwind et la convertit en package NuGet appelé `NorthwindTraders.Client`. Peu après, Northwind veut produire de son côté un package NuGet officiel pour leur bibliothèque cliente et souhaite donc contester à Nancy la propriété du nom du package.

Dans ce scénario, Nancy ne semble pas agir avec de mauvaises intentions. Au contraire, elle agit plutôt en faveur des outils et des clients de Northwind en donnant de son temps et en contribuant avec son code. Parallèlement, Northwind est le propriétaire légitime du nom Northwind.

En suivant la procédure ci-dessous, Northwind et Nancy peuvent rechercher ensemble une résolution appropriée, car l’un comme l’autre souhaitent servir la communauté des développeurs. Il n’est généralement pas nécessaire que l’équipe NuGet intervienne, car la collaboration résout généralement tous les problèmes.

## <a name="process"></a>Process

1. Contactez les propriétaires du package pour lequel vous avez un litige en utilisant le lien **Contacter les propriétaires** situé sur la page des détails du package. Décrivez votre problème de façon simple et directe.
2. Envoyez une copie de votre message à [support@nuget.org](mailto:support@nuget.org) afin que NuGet et le .net Foundation soient conscients de votre litige.
3. Attendez un maximum de 30 jours pour une résolution, puis [support@nuget.org](mailto:support@nuget.org) recommencez l’opération. L’équipe de support nuget.org prendra part au dossier afin de résoudre le litige avec les deux parties.
