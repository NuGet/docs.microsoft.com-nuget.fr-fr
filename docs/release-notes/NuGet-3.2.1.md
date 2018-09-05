---
title: Notes de publication NuGet 3.2.1
description: Notes de publication pour NuGet 3.2.1 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548188"
---
# <a name="nuget-321-release-notes"></a>Notes de publication NuGet 3.2.1

[Notes de publication de NuGet 3.2](../release-notes/nuget-3.2.md) | [Notes de publication NuGet 3.3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 pour la ligne de commande a été publiée le 12 octobre 2015, avec un certain nombre d’optimisations et les correctifs pour la version 3.2 et est disponible à partir de [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Améliorations

* NuGet utilise désormais le fichier de configuration avec la casse d’origine de `NuGet.Config`.  Ceci est important sur les systèmes d’exploitation respectant la casse [1427](https://github.com/NuGet/Home/issues/1427)
* Restauration NuGet ignore maintenant les projets dnx (`*.xproj`) qui doit être traité avec `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Optimisé l’utilisation du réseau lorsque vous travaillez avec `index.json` et les données de l’inscription du package [1426](https://github.com/NuGet/Home/issues/1426)
* Téléchargement de ressources gérant de manière à être plus robuste avec les services v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correctifs

* Mise à jour de NuGet met correctement à jour `.csproj` / `.vcxproj` références [1483](https://github.com/NuGet/Home/issues/1483)
* Maintenant empêchant toute un dossier local .nuget création lorsqu’un SpecialFolders.UserProfile ne peut pas être localisé [1531](https://github.com/NuGet/Home/issues/1531)
* Une gestion des packages dans le cache local sont endommagés pendant le téléchargement améliorée [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Obtenir la liste complète des problèmes résolus pour la ligne de commande et de Visual Studio se trouve dans NuGet GitHub [3.2.1 jalon](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Problèmes connus

Nous continuons à suivre les problèmes sur notre liste de problèmes GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)