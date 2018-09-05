---
title: Notes de publication de NuGet 2.8.5
description: Notes de publication pour NuGet 2.8.5, notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548623"
---
# <a name="nuget-285-release-notes"></a>Notes de publication de NuGet 2.8.5

[Notes de publication de NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [Notes de publication de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 a été publiée le 30 mars 2015. Il est une mise à jour mineure sur notre 2.8.3 VSIX avec certains ciblé des correctifs.

Dans cette version, la prise en charge pour la boîte de dialogue Gestionnaire de Package NuGet a été ajoutée pour [Monikers du Framework cible DNX](https://github.com/aspnet/dnx).  Ces nouvelles monikers du framework qui sont pris en charge sont les suivantes :

* **core50** : un moniker du framework (TFM) qui est compatible avec le CLR de base 'base' cible.
* **dnx452** : un moniker du Framework cible des applications spécifiques basée sur DNX à l’aide de la 4.5.2 complète version du framework
* **dnx46** : un moniker du Framework cible des applications spécifiques basée sur DNX à l’aide de la version 4.6 complète du framework
* **: dnxcore50** : un moniker du Framework cible des applications spécifiques basée sur DNX à l’aide de la version 5.0 de Core du framework

Un bogue a été résolu que les packages a empêché de s’installer correctement dans les projets FSharp :

https://nuget.codeplex.com/workitem/4400