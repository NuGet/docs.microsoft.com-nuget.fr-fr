---
title: Notes de publication NuGet 3.4.4 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet 3.4.4, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 3.4.4 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fabc10ae5c8e0bd43581f85c7763eb23e9483aaf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-344-release-notes"></a>Notes de mise à jour de NuGet 3.4.4

[Notes de publication NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [Notes de version bêta de 3.5 NuGet](../release-notes/nuget-3.5-Beta.md)

Le principal objectif de cette version : les améliorations de la qualité du 3.4.3 version de nuget.exe avec quelques correctifs ainsi l’extension de Visual Studio.

Vous pouvez télécharger l’extension VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Journal complet](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Liste des problèmes](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Modifications

- Améliorations du Pack : Les améliorations à la compression des symboles, de livraison avec `project.json` plus [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Afficher l’exception lors de l’échec de recherche de projets dans la commande de mise à jour [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- Lire le type de package à partir de l’entrée `.nuspec` et `project.json` lors de la livraison [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Vérifiez NuGet.Shared pas un projet. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Utilisez le délai d’attente de transmission en tant que le délai d’attente de la réponse HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Fichiers de package avec la prochaine fois n’auront pas leurs utilisations [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Mise à jour `NuGet.Core.dll` version 2.12.0 pour résoudre le problème de XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Affichage erreur restauration sans `project.json` ou `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Résolution des versions de la dépendance lorsque les versions requises diffèrent [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)