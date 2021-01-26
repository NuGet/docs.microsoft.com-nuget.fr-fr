---
title: Notes de publication de NuGet 3,1
description: Notes de publication de NuGet 3,1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776529"
---
# <a name="nuget-31-release-notes"></a>Notes de publication de NuGet 3,1

Notes de publication de [NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Notes de publication de NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3,1 a été publié le 27 juillet 2015 en tant qu’extension groupée du kit de développement logiciel (SDK) plateforme Windows universelle pour Visual Studio 2015. Nous avons fourni cette version avec le kit de développement logiciel (SDK) de la plate-forme Windows afin que l’expérience de développement Windows puisse tirer parti du travail multiplateforme NuGet précédemment démarré. Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.

Nous recommandons aux développeurs qui ont accès à la mise à jour de la Galerie Visual Studio d’accéder à la dernière version disponible, car nous publions toujours des mises à jour avec des correctifs de bogues et de nouvelles fonctionnalités.

## <a name="nuget-visual-studio-extension"></a>Extension NuGet Visual Studio

Les problèmes et les fonctionnalités de cette version sont marqués sur GitHub avec le [jalon « 3,1 RTM UWP transitive support »](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  au total, nous avons clos 67 problèmes dans la version 3,1.

### <a name="new-features"></a>Nouvelles fonctionnalités

* `project.json` prise en charge de la prise en charge de Windows UWP et ASP.NET 5
* Installation du package transitif

La description et la définition de ces fonctionnalités sont disponibles ailleurs dans la documentation.

### <a name="deprecated"></a>Déprécié

Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 :

* Les packages au niveau de la solution ne peuvent plus être installés

Les fonctionnalités suivantes ne sont plus disponibles pour Visual Studio 2015 et les projets qui utilisent la `project.json` spécification

* `install.ps1` et `uninstall.ps1` -ces scripts seront ignorés lors de l’installation, de la restauration, de la mise à jour et de la désinstallation du package
* Les transformations de configuration seront ignorées
* Le contenu sera transporté, mais pas copié dans un projet.
    * L’équipe travaille pour réimplémenter cette fonctionnalité, suivre la discussion et la progression à l’adresse suivante : [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problèmes connus

Un certain nombre de problèmes connus ont été fournis avec cette version.

* L’installation de la version 3,1 avec le kit de développement logiciel (SDK) Windows 10 rétrograde toute version de l’extension NuGet précédemment installée

## <a name="nuget-command-line"></a>Ligne de commande NuGet

L’exécutable de ligne de commande NuGet a été mis à jour et déplacé vers un nouvel emplacement distribuable afin que les versions historiques de nuget.exe puissent continuer à être mises à disposition.  Vous pouvez télécharger la version bêta 3,1 de nuget.exe pour Windows à l’adresse suivante : [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Le nouvel emplacement distribuable réside sur l’hôte dist.nuget.org, avec une structure de dossiers qui suit ce modèle :

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>Nouvelles fonctionnalités

* nuget.exe pouvez restaurer et installer des packages dans des projets qui utilisent un `project.json` fichier.
* nuget.exe pouvez vous connecter au protocole NuGet v3 et l’utiliser à l’adresse suivante : [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problèmes connus ##

1.    Impossible d’exécuter le Pack sur un `project.json` fichier- [928](https://github.com/NuGet/Home/issues/928)
2.    N’est pas pris en charge sur mono- [1059](https://github.com/NuGet/Home/issues/1059)
3.    N’est pas localisé- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    N’est pas signé, comme le http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
