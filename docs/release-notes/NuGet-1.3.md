---
title: Notes de publication NuGet 1.3
description: Notes de publication pour 1.3 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551349"
---
# <a name="nuget-13-release-notes"></a>Notes de publication NuGet 1.3

[Notes de publication de NuGet 1.2](../release-notes/nuget-1.2.md) | [Notes de publication de NuGet 1.4](../release-notes/nuget-1.4.md)

NuGet 1.3 a été publiée le 25 avril 2011.

## <a name="new-features"></a>Nouvelles fonctionnalités

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Création d’un Package simplifiée avec intégration du serveur de symbole

L’équipe NuGet établi un partenariat avec l’équipe [SymbolSource.org](http://www.symbolsource.org/) pour offrir un moyen vraiment simple de la publication de vos sources et du fichier PDB en même temps que votre package. Cela permet aux consommateurs de votre package de pas à pas détaillé de la source de votre package dans le débogueur. Pour plus d’informations, consultez [création et publication d’un Package de symboles](../create-packages/symbol-packages.md) moyen simple de publier des packages NuGet avec des sources. Vous pouvez également regarder une démonstration en direct de cette fonctionnalité dans le cadre du package NuGet en profondeur pour parler à Mix11. Cette fonctionnalité est expliquée entièrement à partir de la marque de 20 minutes de la vidéo.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Commande

Cette commande rend plus facile accéder à la page de projet pour un package à partir de la console du Gestionnaire de Package. Il fournit également des options permettant d’ouvrir l’URL de licence et la page d’abus de rapport pour le package.
La syntaxe de la commande est :

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

Le `-PassThru` option est utilisée pour retourner la valeur de l’URL spécifiée.

Exemples :

    PM> Open-PackagePage Ninject

Ouvre un navigateur vers l’URL de projet spécifiée dans le package Ninject.

    PM> Open-PackagePage Ninject -License

Ouvre un navigateur vers l’URL de licence spécifiée dans le package Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Ouvre un navigateur vers l’URL de la source du package actuel utilisée pour signaler un abus pour le package spécifié.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Assigne l’URL de licence à la variable, $url, sans ouvrir l’URL dans un navigateur.

### <a name="performance-improvements"></a>Amélioration des performances

NuGet 1.3 introduit de nombreuses améliorations de performances. NuGet 1.3 évite le téléchargement de la même version d’un package plusieurs fois en incluant un cache de l’utilisateur local. Le cache sont accessibles et désactivé via la boîte de dialogue Paramètres du Gestionnaire de Package :

![Boîte de dialogue Options NuGet avec les paramètres de Cache de Package](./media/nuget-options.png)

Autres améliorations des performances incluent la prise en charge de la compression HTTP et améliore la vitesse d’installation de package dans Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio et nuget.exe utilise la même liste de sources de package

Avant NuGet 1.3, la liste des sources de package utilisé par nuget.exe et le complément NuGet Visual Studio n’étaient pas stockées au même endroit. NuGet 1.3 utilise désormais la même liste aux deux emplacements. La liste est stockée dans `NuGet.Config` et stockés dans le dossier AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe ignore les fichiers et dossiers qui commencent par «. » par défaut

Afin d’optimiser NuGet avec les systèmes de contrôle de code source tels que Subversion et le Mercurial, nuget.exe ignore les dossiers et fichiers qui commencent par le '.' caractère lors de la création de packages. Il peut être remplacé à l’aide de deux nouveaux indicateurs :

* __-NoDefaultExcludes__ est utilisé pour remplacer ce paramètre et d’inclure tous les fichiers.
* __-Exclure__ est utilisée pour ajouter d’autres fichiers/dossiers à exclure en indiquant un modèle. Par exemple, pour exclure tous les fichiers portant l’extension de fichier '.bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Remarque : le modèle n’est pas récursive par défaut._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Prise en charge des projets WiX et .NET Micro Framework

Grâce aux contributions de la Communauté, NuGet prend en charge les types de projets WiX, ainsi que .NET Micro Framework.

## <a name="bug-fixes"></a>Correctifs de bogues

Pour obtenir une liste complète des correctifs de bogues, veuillez consulter la [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correctifs de bogues à noter

* Avec les fichiers sources des packages fonctionnent dans les deux sites Web et dans les projets d’Application Web.
Pour les sites Web, les fichiers sources sont copiés dans le `App_Code` dossier
