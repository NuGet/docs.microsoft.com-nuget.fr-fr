---
title: Notes de publication NuGet 3.4.3 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet 3.4.3, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 3.4.3 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-343-release-notes"></a>Notes de mise à jour de NuGet 3.4.3

[Notes de publication NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Notes de publication](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 a été publiée le 22 avril 2016 pour résoudre plusieurs problèmes ont été identifiés dans les versions 3.4 et ultérieures.

Vous pouvez télécharger l’extension VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Une meilleure fiabilité de Visual Studio. Nous avons résolu certains problèmes dans NuGet qui ont provoqué des incidents dans Visual Studio.

## <a name="fixes"></a>Correctifs

* Correction des problèmes d’autorisation avec nuget privé de mot de passe protégé des flux de.
* Correction d’un problème autour de l’impossibilité de restaurer à partir de PCL `project.json` avec des runtimes spécifiés.
* Certains clients étaient en cours d’exécution sur les défaillances intermittentes lors de l’installation des packages. Ce problème a maintenant été corrigé dans cette version.
* Correction d’un problème qui a provoqué des problèmes de restauration dans C + c++ / CLI des projets avec `project.json`.
* Certains packages (par exemple ModernHttpClient) dans lequel n’est ne pas décompressé correctement lorsque vous utilisez nuget en mono. Ce problème a maintenant été corrigé dans cette version.

Pour obtenir la liste complète des correctifs et améliorations apportées dans cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).