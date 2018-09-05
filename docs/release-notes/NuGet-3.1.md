---
title: Notes de publication NuGet 3.1
description: Notes de publication pour 3.1 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545345"
---
# <a name="nuget-31-release-notes"></a>Notes de publication NuGet 3.1

[Notes de publication de NuGet 3.0](../release-notes/nuget-3.0.0.md) | [Notes de publication de NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3.1 a été publiée le 27 juillet 2015 comme extension groupée dans le SDK de plateforme Windows universelle pour Visual Studio 2015. Nous avons envoyé cette version avec le SDK de plateforme Windows afin que l’expérience de développement Windows peut tirer parti du travail NuGet multiplateforme qui a déjà été démarré. Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.

Nous recommandons aux développeurs qui ont accès à la mise à jour de la galerie Visual Studio à la version la plus récente est disponible, car nous publions toujours les mises à jour avec les correctifs de bogues et de nouvelles fonctionnalités.

## <a name="nuget-visual-studio-extension"></a>Extension NuGet Visual Studio

Problèmes et les fonctionnalités dans cette version sont marquées sur GitHub avec le [« 3.1 RTM UWP transitive prise en charge » jalon](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) au total, nous avons fermé 67 problèmes dans la version 3.1.

### <a name="new-features"></a>Nouvelles fonctionnalités

* `project.json` prise en charge pour la prise en charge Windows UWP et ASP.NET 5
* Installation de package transitives

Description et la définition de ces fonctionnalités peuvent être trouvées ailleurs dans la documentation.

### <a name="deprecated"></a>Déconseillé

Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 :

* Packages au niveau de la solution ne peuvent plus être installés

Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 et les projets qui utilisent le `project.json` spécification

* `install.ps1` et `uninstall.ps1` -ces scripts seront ignorés pendant l’installation du package, la restauration, mettre à jour et désinstaller
* Transformations de configuration va être ignorées
* Contenu est exécuté, mais pas copié dans un projet.
    * L’équipe travaille pour ré-implémenter cette fonctionnalité, suivez la discussion et avancer à : [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problèmes connus

Il existe un nombre de problèmes connus fournies par cette version.

* Installation de la version 3.1 avec le SDK Windows 10 rétrograde n’importe quelle version de l’extension NuGet qui a été précédemment installée

## <a name="nuget-command-line"></a>NuGet en ligne de commande

L’exécutable de ligne de commande NuGet a été mis à jour et déplacé vers un nouvel emplacement distribuable de sorte que les versions historiques de nuget.exe peuvent continuer à être mis à disposition.  Vous pouvez télécharger la version 3.1 bêta de nuget.exe pour Windows à : [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Le nouvel emplacement distribuable réside sur l’hôte dist.nuget.org, avec une structure de dossiers qui suit ce modèle :

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Nouvelles fonctionnalités

* NuGet.exe peut restaurer et installer des packages dans les projets qui utilisent un `project.json` fichier.
* NuGet.exe peut se connecter à et utiliser le protocole v3 de NuGet à : [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problèmes connus ##

1.    Impossible d’exécuter pack par rapport à un `project.json` fichier - [928](https://github.com/NuGet/Home/issues/928)
2.    N’est pas pris en charge sur Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    N’est pas localisé - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    N’est pas signé, à l’instar existant http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
