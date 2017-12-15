---
title: Notes de publication NuGet 2.8.5 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "Notes de publication pour NuGet 2.8.5, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 2.8.5 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
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

https://NuGet.codeplex.com/WorkItem/4400