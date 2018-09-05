---
title: Notes de publication de NuGet 3.4.3
description: Notes de publication pour NuGet 3.4.3 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549163"
---
# <a name="nuget-343-release-notes"></a>Notes de publication de NuGet 3.4.3

[Notes de publication de NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [Notes de publication de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 a été publiée le 22 avril 2016 pour résoudre plusieurs problèmes qui ont été identifiées dans les versions 3.4 et ultérieures.

Vous pouvez télécharger l’extension VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Une meilleure fiabilité de Visual Studio. Nous avons résolu certains problèmes dans NuGet qui ont provoqué des incidents dans Visual Studio.

## <a name="fixes"></a>Correctifs

* Correction des problèmes d’autorisation avec nuget privé protégé par mot de passe des flux.
* Correction d’un problème autour de l’impossibilité de se restaurer à partir de PCL `project.json` avec des runtimes spécifiés.
* Certains clients étaient en cours d’exécution sur les défaillances intermittentes lors de l’installation des packages. Ce problème a maintenant été résolu dans cette version.
* Correction d’un problème qui provoquait des échecs de restauration en C / c++ / CLI des projets avec `project.json`.
* Certains packages (par ex. ModernHttpClient) où n’est pas décompressé correctement lorsque vous utilisez nuget dans mono. Ce problème a maintenant été résolu dans cette version.

Pour obtenir la liste complète des correctifs et améliorations dans cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).