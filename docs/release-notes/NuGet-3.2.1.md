---
title: Notes de mise à jour de NuGet 3.2.1
description: Notes de publication pour NuGet 3.2.1, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820142"
---
# <a name="nuget-321-release-notes"></a>Notes de mise à jour de NuGet 3.2.1

[Notes de publication NuGet 3.2](../release-notes/nuget-3.2.md) | [NuGet 3.3 Notes de publication](../release-notes/nuget-3.3.md)

NuGet 3.2.1 pour la ligne de commande a été publiée le 12 octobre 2015, avec quelques optimisations et correctifs pour la version 3.2 et est disponible à partir de [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Améliorations apportées à

* NuGet utilise désormais le fichier de configuration avec la casse d’origine de `NuGet.Config`.  Ceci est important sur les systèmes d’exploitation qui respecte la casse [1427](https://github.com/NuGet/Home/issues/1427)
* NuGet restore ignore désormais des projets dnx (`*.xproj`) qui doit être traité avec `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Optimisé l’utilisation du réseau lorsque vous travaillez avec `index.json` et les données de l’enregistrement du package [1426](https://github.com/NuGet/Home/issues/1426)
* Téléchargement de ressources gérant de manière à être plus robustes avec les services v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correctifs

* Met à jour correctement mise à jour de NuGet `.csproj` / `.vcxproj` références [1483](https://github.com/NuGet/Home/issues/1483)
* Maintenant empêchant toute un dossier .nuget local création lorsque Impossible de trouver un SpecialFolders.UserProfile [1531](https://github.com/NuGet/Home/issues/1531)
* Amélioration de la gestion des packages dans le cache local qui sont endommagés pendant le téléchargement [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Une liste complète des problèmes résolus pour les en ligne de commande et de Visual Studio se trouve dans NuGet GitHub [3.2.1 jalon](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Problèmes connus

Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)