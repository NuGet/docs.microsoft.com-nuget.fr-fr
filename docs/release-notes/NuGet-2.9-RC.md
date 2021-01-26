---
title: Notes de publication de NuGet 2,9-RC
description: Notes de publication de NuGet 2,9 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780311"
---
# <a name="nuget-29-rc-release-notes"></a>Notes de publication de NuGet 2,9-RC

Notes de publication de [NuGet 2.8.7](../release-notes/nuget-2.8.7.md)  |  [Notes de publication de NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)

NuGet 2,9 a été publié le 10 septembre 2015 en tant que mise à jour de 2.8.7 VSIX pour Visual Studio 2012 et 2013.

### <a name="updates-in-this-release"></a>Mises à jour dans cette version

* À présent, les packages de traitement sont ignorés si leur `.nuspec` document contenu est incorrect- [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Correction du traitement multipartwebrequest de \r\n pour les scénarios UNIX/Linux- [776](https://github.com/NuGet/Home/issues/776)
* Correction de l’intégration avec les événements de build dans Visual Studio 2013 Édition Community- [1180](https://github.com/NuGet/Home/issues/1180)


La liste complète des correctifs dans cette version est disponible sur GitHub dans le [jalon 2.8.8](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
