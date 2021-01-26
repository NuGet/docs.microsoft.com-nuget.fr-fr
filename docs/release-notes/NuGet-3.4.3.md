---
title: Notes de publication de NuGet 3.4.3
description: Notes de publication pour NuGet 3.4.3, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776468"
---
# <a name="nuget-343-release-notes"></a>Notes de publication de NuGet 3.4.3

Notes de publication de [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Notes de publication de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 a été publié le 22 avril 2016 pour résoudre plusieurs problèmes identifiés dans le 3,4 et dans les versions ultérieures.

Vous pouvez télécharger les versions VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Amélioration de la fiabilité de Visual Studio. Nous avons résolu certains problèmes dans NuGet qui provoquaient des blocages dans Visual Studio.

## <a name="fixes"></a>Correctifs

* Correction de certains problèmes d’autorisation avec les flux NuGet privés protégés par mot de passe.
* Résolution d’un problème lié à l’impossibilité de restaurer les bibliothèques de classes portable à partir de `project.json` avec des runtimes spécifiés.
* Certains clients étaient confrontés à des défaillances intermittentes lors de l’installation des packages. Ce problème a été résolu dans cette version.
* Correction d’un problème qui provoquait des échecs de restauration dans les projets C++/CLI avec `project.json` .
* Certains packages (par exemple, ModernHttpClient) où ne sont pas décompressés correctement lorsque vous utilisez NuGet en mono. Ce problème a été résolu dans cette version.

Pour obtenir la liste complète des correctifs et améliorations de cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).