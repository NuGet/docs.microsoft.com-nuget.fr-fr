---
title: Règlement des litiges autour des noms de packages NuGet
description: Processus de résolution des litiges entre les éditeurs de packages NuGet liés à la personnalisation, aux marques et autres situations de conflit.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426934"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Résolution des litiges autour des noms de package NuGet

Cet article présente aux membres de la communauté un processus recommandé pour régler les litiges avec d’autres éditeurs NuGet.

Par exemple, supposons que Northwind Traders crée un système CRM pour lequel il fournit des pilotes clients sous la forme d’un fichier MSI téléchargeable à partir de son site web. Nancy, développeuse indépendante, souhaite faciliter l’utilisation de la bibliothèque cliente de Northwind et la convertit en package NuGet appelé `NorthwindTraders.Client`. Peu après, Northwind veut produire de son côté un package NuGet officiel pour leur bibliothèque cliente et souhaite donc contester à Nancy la propriété du nom du package.

Dans ce scénario, Nancy ne semble pas agir avec de mauvaises intentions. Au contraire, elle agit plutôt en faveur des outils et des clients de Northwind en donnant de son temps et en contribuant avec son code. Parallèlement, Northwind est le propriétaire légitime du nom Northwind.

En suivant la procédure ci-dessous, Northwind et Nancy peuvent rechercher ensemble une résolution appropriée, car l’un comme l’autre souhaitent servir la communauté des développeurs. Il n’est généralement pas nécessaire que l’équipe NuGet intervienne, car la collaboration résout généralement tous les problèmes. En fait, à ce jour, chaque litige soumis à l’équipe NuGet a été résolu sans qu’elle ait dû se prononcer.

## <a name="process"></a>Process

1. Contactez les propriétaires du package pour lequel vous avez un litige en utilisant le lien **Contacter les propriétaires** situé sur la page des détails du package. Décrivez votre problème de façon simple et directe.
2. Envoyez une copie de [support@nuget.org](mailto:support@nuget.org) votre message pour que NuGet et la Fondation .NET soient au courant de votre différend.
3. Attendez un maximum de 30 jours pour [support@nuget.org](mailto:support@nuget.org) une résolution, puis notez à nouveau. L’équipe de support nuget.org prendra part au dossier afin de résoudre le litige avec les deux parties.
