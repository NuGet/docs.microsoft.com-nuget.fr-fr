---
title: Notes de publication NuGet 2.9-RC
description: Notes de publication pour RC 2.9 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 15665e7c3f9f638b434b0d7be2f7ff3215c787c6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819373"
---
# <a name="nuget-29-rc-release-notes"></a>Notes de publication NuGet 2.9-RC

[Notes de publication NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [Notes de version préliminaire de NuGet 3.0](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 a été publiée le 10 septembre 2015, comme une mise à jour le 2.8.7 VSIX pour Visual Studio 2012 et 2013.

### <a name="updates-in-this-release"></a>Dans cette version, les mises à jour

* Maintenant ignorer le traitement des packages si leur relation contenant-contenu `.nuspec` document est incorrect - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Correction de la gestion des multipartwebrequest de \r\n pour les scénarios d’Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Correction de l’intégration avec les événements de build dans les éditions Visual Studio Community 2013 - [1180](https://github.com/NuGet/Home/issues/1180)


Vous trouverez la liste complète des correctifs dans cette version sur GitHub dans le [2.8.8 étape majeure](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
