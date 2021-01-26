---
title: Notes de publication de NuGet 3.4.4
description: Notes de publication pour NuGet 3.4.4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780220"
---
# <a name="nuget-344-release-notes"></a>Notes de publication de NuGet 3.4.4

Notes de publication de [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [Notes de publication de NuGet 3,5-Beta](../release-notes/nuget-3.5-Beta.md)

L’objectif principal de cette version était d’améliorer la qualité de la version 3.4.3 de nuget.exe avec quelques correctifs de l’extension Visual Studio.

Vous pouvez télécharger les versions VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).

## <a name="344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Journal des modifications complet](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Liste des problèmes](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Modifications

- Améliorations des packs : améliorations de la compression des symboles, compression avec `project.json` et plus de [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)
- Afficher une exception en cas d’échec lors de la recherche de projets dans la commande Update [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- Lire le type de package à partir de l’entrée `.nuspec` et lors de la `project.json` compression [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)
- Mettez NuGet. Shared non un projet. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Utilisez le délai d’expiration de Push comme délai de réponse HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)
- Les fichiers de package avec des heures futures n’auront pas les heures utilisées [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- Mise à jour `NuGet.Core.dll` de la version vers 2.12.0 pour résoudre le problème XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- Support./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- Afficher les erreurs de restauration sans `project.json` ou `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)
- Correction des versions de dépendance lorsque les versions requises diffèrent de [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)