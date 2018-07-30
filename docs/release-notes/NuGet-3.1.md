---
title: Notes de version 3.1 de NuGet
description: Notes de publication pour 3.1 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820864"
---
# <a name="nuget-31-release-notes"></a>Notes de version 3.1 de NuGet

[Notes de version de NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Notes de publication](../release-notes/nuget-3.1.1.md)

NuGet 3.1 a été publié le 27 juillet 2015 comme extension fournie dans le SDK de plateforme Windows universelle pour Visual Studio 2015. Nous avons fourni cette version avec le SDK de plateforme Windows afin que l’expérience de développement Windows pourrait tirer parti du travail inter-plateformes NuGet qui a déjà été démarré. Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.

Nous vous recommandons des développeurs qui ont accès à la mise à jour de la galerie Visual Studio à la version la plus récente est disponible, comme nous publions toujours les mises à jour avec les correctifs de bogues et de nouvelles fonctionnalités.

## <a name="nuget-visual-studio-extension"></a>Extension NuGet Visual Studio

Les problèmes et les fonctionnalités dans cette version sont marquées sur GitHub avec la [« 3.1 RTM UWP transitive prise en charge » jalon](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) au total, nous avons fermé 67 problèmes dans la version 3.1.

### <a name="new-features"></a>Nouvelles fonctionnalités

* `project.json` prise en charge pour la prise en charge Windows universelle et ASP.NET 5
* Installation du package transitive

Description et la définition de ces fonctionnalités peuvent être trouvées ailleurs dans la documentation.

### <a name="deprecated"></a>Déconseillé

Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 :

* Packages au niveau de la solution ne peuvent plus être installées

Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 et les projets qui utilisent la `project.json` spécification

* `install.ps1` et `uninstall.ps1` -ces scripts seront ignorés lors de l’installation du package, la restauration, mettre à jour et désinstaller
* Transformations de configuration seront ignorées.
* Le contenu sera effectué, mais pas copié dans un projet.
    * L’équipe travaille pour ré-implémenter cette fonctionnalité, suivez la discussion et au niveau de progression : [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problèmes connus

A un nombre de problèmes connus fourni avec cette version.

* Installation de la version 3.1 avec le SDK Windows 10 rétrograde n’importe quelle version de l’extension NuGet qui a déjà été installée

## <a name="nuget-command-line"></a>NuGet de ligne de commande

L’exécutable de ligne de commande NuGet a été mis à jour et déplacé vers un nouvel emplacement distribuable afin que les versions historiques de nuget.exe peuvent continuer à disposition.  Vous pouvez télécharger la version 3.1 bêta de nuget.exe pour Windows à : [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Le nouvel emplacement distribuable réside sur l’hôte dist.nuget.org, avec une structure de dossiers qui suit ce modèle :

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Nouvelles fonctionnalités

* NuGet.exe peut restaurer et installer des packages dans les projets qui utilisent un `project.json` fichier.
* NuGet.exe peut se connecter à et utiliser le protocole v3 NuGet à : [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problèmes connus ##

1.    Impossible d’exécuter le pack par rapport à un `project.json` fichier - [928](https://github.com/NuGet/Home/issues/928)
2.    N’est pas pris en charge sur Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    N’est pas localisée - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    N’est pas signé, tout comme les existantes http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)
