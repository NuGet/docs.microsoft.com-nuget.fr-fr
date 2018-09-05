---
title: Notes de publication de NuGet 3.4.4
description: Notes de publication pour NuGet 3.4.4, notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547471"
---
# <a name="nuget-344-release-notes"></a>Notes de publication de NuGet 3.4.4

[Notes de publication de NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [Notes de publication NuGet 3.5 bêta](../release-notes/nuget-3.5-Beta.md)

Le principal objectif de cette version a été améliorations apportées à la qualité de 3.4.3 version de nuget.exe avec quelques correctifs à l’extension de Visual Studio et.

Vous pouvez télécharger l’extension VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Journal des modifications complet](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Liste des problèmes](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Modifications

- Améliorations du Pack : Améliorations pour la compression des symboles, de livraison avec `project.json` et plus [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Afficher l’exception lors de l’échec de recherche de projets dans la commande de mise à jour [\#605](https://github.com/NuGet/NuGet.Client/pull/605)
- Lire le type de package à partir de l’entrée `.nuspec` et `project.json` lors de la compression [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Rendre NuGet.Shared pas un projet. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Utiliser le délai d’attente de transmission en tant que le délai d’expiration de la réponse HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Fichiers de package avec des dates futures n’aura pas leurs utilisations [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- La mise à jour `NuGet.Core.dll` version à 2.12.0 pour résoudre le problème de XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Prise en charge de v -./NuGet.CommandLine.XPlat \<commentaires\> \<mode\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Restauration d’erreur complet sans `project.json` ou `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Résolution des versions de dépendances lorsque diffèrent des versions requises [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)