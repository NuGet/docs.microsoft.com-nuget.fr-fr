---
title: Notes de publication de NuGet 2.8.5
description: Notes de publication pour NuGet 2.8.5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780358"
---
# <a name="nuget-285-release-notes"></a>Notes de publication de NuGet 2.8.5

Notes de publication de [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Notes de publication de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 a été publié le 30 mars 2015. Il s’agit d’une mise à jour mineure de notre VSIX 2.8.3 avec certains correctifs ciblés.

Dans cette version, la boîte de dialogue prise en charge du gestionnaire de package NuGet a été ajoutée pour les [monikers du Framework cible DNX](https://github.com/aspnet/dnx).  Ces nouveaux monikers de Framework pris en charge sont les suivants :

* **core50** -un moniker de Framework cible’base' (TFM) qui est compatible avec le CLR principal.
* **dnx452** -A TFM spécifique aux applications basées sur DNX utilisant la version 4.5.2 complète de l’infrastructure
* **dnx46** -A TFM spécifique aux applications basées sur DNX utilisant la version 4,6 complète de l’infrastructure
* **dnxcore50** -A TFM spécifique aux applications basées sur DNX à l’aide de la version 5,0 principale de l’infrastructure

Un bogue qui empêchait l’installation correcte des packages dans les projets FSharp a été corrigé :

https://nuget.codeplex.com/workitem/4400