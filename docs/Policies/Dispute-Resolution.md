---
title: "Résolution des litiges autour des noms de package NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6d664378-3f7b-426e-aef3-2254d745fe60
description: "Processus de résolution des litiges entre les éditeurs de packages NuGet liés à la personnalisation, aux marques et autres situations de conflit."
keywords: "litiges autour des packages NuGet, résolution des litiges autour de NuGet, processus de résolution des litiges"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32f5f766a49a2e4254a81978757d973fc5353db1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Résolution des litiges autour des noms de package NuGet

Ce document présente un processus de résolution recommandé à l’attention des membres de la communauté pour résoudre les litiges avec d’autres éditeurs NuGet.  

Par exemple, supposons que Northwind Traders crée un système CRM pour lequel il fournit des pilotes clients sous la forme d’un fichier MSI téléchargeable à partir de son site web. Nancy, développeuse indépendante, souhaite faciliter l’utilisation de la bibliothèque cliente de Northwind et la convertit en package NuGet appelé `NorthwindTraders.Client`. Peu après, Northwind veut produire de son côté un package NuGet officiel pour leur bibliothèque cliente et souhaite donc contester à Nancy la propriété du nom du package.

Dans ce scénario, Nancy ne semble pas agir avec de mauvaises intentions. Au contraire, elle agit plutôt en faveur des outils et des clients de Northwind en donnant de son temps et en contribuant avec son code. Parallèlement, Northwind est le propriétaire légitime du nom Northwind.

En suivant la procédure ci-dessous, Northwind et Nancy peuvent rechercher ensemble une résolution appropriée, car l’un comme l’autre souhaitent servir la communauté des développeurs. Il n’est généralement pas nécessaire que l’équipe NuGet intervienne, car la collaboration résout généralement tous les problèmes. En fait, à ce jour, chaque litige soumis à l’équipe NuGet a été résolu sans qu’elle ait dû se prononcer.


## <a name="process"></a>Procédure

1. Contactez les propriétaires du package auxquels vous oppose le litige en utilisant le lien **Contact Owners** (Contacter les propriétaires) dans la page de détails du package. Expliquez votre problème de manière claire et courtoise.
2. Envoyez une copie de votre message à [support@nuget.org](mailto:support@nuget.org) afin que NuGet et la .NET Foundation prennent connaissance de votre litige.
3. Si le litige n’est pas résolu au bout de 30 jours, renotifiez [support@nuget.org](mailto:support@nuget.org). L’équipe de support nuget.org prendra part au dossier afin de résoudre le litige avec les deux parties.
