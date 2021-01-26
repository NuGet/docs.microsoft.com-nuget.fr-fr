---
title: Notes de publication de NuGet 3.2.1
description: Notes de publication pour NuGet 3.2.1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776526"
---
# <a name="nuget-321-release-notes"></a>Notes de publication de NuGet 3.2.1

Notes de publication de [NuGet 3,2](../release-notes/nuget-3.2.md)  |  [Notes de publication de NuGet 3,3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 pour la ligne de commande a été publiée le 12 octobre 2015 avec quelques optimisations et correctifs pour la version de 3,2 et est disponible à partir de [dist.NuGet.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Améliorations

* NuGet utilise désormais le fichier de configuration avec la casse d’origine `NuGet.Config` .  Cela est important sur les systèmes d’exploitation qui respectent la casse [1427](https://github.com/NuGet/Home/issues/1427)
* La restauration NuGet ignore maintenant les projets DNX ( `*.xproj` ) qui doivent être traités avec `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Utilisation optimisée du réseau lors de l’utilisation des `index.json` données d’inscription et de package [1426](https://github.com/NuGet/Home/issues/1426)
* Amélioration de la gestion du téléchargement des ressources pour être plus robuste avec les services v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correctifs

* Mise à jour de NuGet mises à jour correctement `.csproj` / `.vcxproj` références [1483](https://github.com/NuGet/Home/issues/1483)
* Maintenant, vous empêchez la création d’un dossier. NuGet local lorsqu’un SpecialFolders. UserProfile est introuvable [1531](https://github.com/NuGet/Home/issues/1531)
* Amélioration de la gestion des packages dans le cache local endommagés au cours du téléchargement [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Une liste complète des problèmes adressés à la ligne de commande et à l’extension Visual Studio se trouve dans le [Jalon](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) NuGet GitHub 3.2.1.

## <a name="known-issues"></a>Problèmes connus

Nous continuons à suivre les problèmes de notre liste de problèmes GitHub qui se trouvent à l’adresse suivante : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)