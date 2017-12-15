---
title: Notes de publication NuGet 2.9-RC | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 04d76a22-63b0-41d1-9c27-799f4b35058f
description: "Notes de publication pour RC 2.9 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 2.9 RC, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 64b4cd17394ddb902c7101b9117039f381dc8488
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-29-rc-release-notes"></a>Notes de publication NuGet 2.9-RC

[Notes de publication NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [Notes de version préliminaire de NuGet 3.0](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 a été publiée le 10 septembre 2015, comme une mise à jour le 2.8.7 VSIX pour Visual Studio 2012 et 2013.

### <a name="updates-in-this-release"></a>Dans cette version, les mises à jour

* Maintenant ignorer le traitement des packages si leur relation contenant-contenu `.nuspec` document est incorrect - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Correction de la gestion des multipartwebrequest de \r\n pour les scénarios d’Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Correction de l’intégration avec les événements de build dans les éditions Visual Studio Community 2013 - [1180](https://github.com/NuGet/Home/issues/1180)


Vous trouverez la liste complète des correctifs dans cette version sur GitHub dans le [2.8.8 étape majeure](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
