---
title: Notes de publication NuGet 2.9-RC
description: Notes de publication pour NuGet 2.9 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548322"
---
# <a name="nuget-29-rc-release-notes"></a>Notes de publication NuGet 2.9-RC

[Notes de publication de NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [Notes de publication de NuGet 3.0 Preview](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 a été publiée le 10 septembre 2015 en tant qu’une mise à jour le 2.8.7 VSIX pour Visual Studio 2012 et 2013.

### <a name="updates-in-this-release"></a>Mises à jour dans cette version

* Maintenant ignorer les packages de traitement si leur relation contenant-contenu `.nuspec` document est incorrect - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Corrigé gestion multipartwebrequest de \r\n pour les scénarios d’Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Correction de l’intégration avec les événements de build dans les éditions de Visual Studio 2013 Community - [1180](https://github.com/NuGet/Home/issues/1180)


Vous trouverez la liste complète des correctifs dans cette version sur GitHub dans le [2.8.8 étape majeure](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
