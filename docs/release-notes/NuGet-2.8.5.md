---
title: Notes de mise à jour de NuGet 2.8.5
description: Notes de publication pour NuGet 2.8.5, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820077"
---
# <a name="nuget-285-release-notes"></a>Notes de mise à jour de NuGet 2.8.5

[Notes de publication NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Notes de publication](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 a été publiée le 30 mars 2015. Il est une mise à jour mineure sur notre 2.8.3 VSIX avec certains ciblé des correctifs.

Dans cette version, la prise en charge pour la boîte de dialogue Gestionnaire de Package NuGet a été ajouté pour [Monikers du Framework cible DNX](https://github.com/aspnet/dnx).  Ces nouveaux monikers d’infrastructure qui sont prises en charge sont les suivantes :

* **core50** - un moniker du framework (TFM) qui est compatible avec la version CLR de base 'base' cible.
* **dnx452** : à l’aide de la 4.5.2 complète des applications spécifiques à DNX TFM d’une version du framework
* **dnx46** - A TFM des applications spécifiques en fonction de DNX à l’aide de la version 4.6 complète de l’infrastructure
* **dnxcore50** - A TFM des applications spécifiques en fonction de DNX à l’aide de la version 5.0 de cœur du framework

Un bogue a été résolu que les packages a empêché de s’installer correctement dans les projets FSharp :

https://nuget.codeplex.com/workitem/4400