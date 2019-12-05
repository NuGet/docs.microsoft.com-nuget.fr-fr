---
title: Notes de publication de NuGet 1,3
description: Notes de publication de NuGet 1,3, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825263"
---
# <a name="nuget-13-release-notes"></a>Notes de publication de NuGet 1,3

[Notes de publication de nuget 1,2](../release-notes/nuget-1.2.md) | [notes de publication de NuGet 1,4](../release-notes/nuget-1.4.md)

NuGet 1,3 a été publié le 25 avril 2011.

## <a name="new-features"></a>Nouvelles fonctionnalités

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Création de packages rationalisée avec intégration de serveur de symboles

L’équipe NuGet a fait ses partenariats avec les personnes de [SymbolSource.org](http://www.symbolsource.org/) pour offrir un moyen simple de publier vos sources et vos PDB avec votre package. Cela permet aux consommateurs de votre package d’effectuer un pas à pas détaillé dans la source de votre package dans le débogueur. Pour plus d’informations, consultez [création et publication d’un package de symboles](../create-packages/symbol-packages.md) le moyen le plus simple de publier des packages NuGet avec des sources. Vous pouvez également regarder une démonstration en direct de cette fonctionnalité dans le cadre de la Conférence NuGet en profondeur sur MIX11. Cette fonctionnalité est entièrement démontrée à partir de 20 minutes de la vidéo.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Command

Cette commande permet d’accéder facilement à la page de projet d’un package à partir de la console du gestionnaire de package. Il fournit également des options pour ouvrir l’URL de licence et la page signaler un abus pour le package.
La syntaxe de la commande est la suivante :

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

L’option `-PassThru` est utilisée pour retourner la valeur de l’URL spécifiée.

Exemples :

    PM> Open-PackagePage Ninject

Ouvre un navigateur à l’URL du projet spécifiée dans le package Ninject.

    PM> Open-PackagePage Ninject -License

Ouvre un navigateur à l’URL de licence spécifiée dans le package Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Ouvre un navigateur à l’URL de la source de package actuelle utilisée pour signaler un abus pour le package spécifié.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Affecte l’URL de licence à la variable, $url, sans ouvrir l’URL dans un navigateur.

### <a name="performance-improvements"></a>Améliorations apportées aux performances

NuGet 1,3 introduit de nombreuses améliorations en matière de performances. NuGet 1,3 évite de télécharger plusieurs fois la même version d’un package en incluant un cache par utilisateur local. Le cache est accessible et effacé via la boîte de dialogue des paramètres du gestionnaire de package :

![Boîte de dialogue Options NuGet avec les paramètres du cache du package](./media/nuget-options.png)

D’autres améliorations de performances incluent l’ajout de la prise en charge de la compression HTTP et l’amélioration de la vitesse d’installation du package dans Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio et NuGet. exe utilisent la même liste de sources de packages

Avant NuGet 1,3, la liste des sources de package utilisées par NuGet. exe et le complément NuGet Visual Studio n’étaient pas stockées au même endroit. NuGet 1,3 utilise désormais la même liste aux deux emplacements. La liste est stockée dans `NuGet.Config` et stockée dans le dossier AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet. exe ignore les fichiers et les dossiers qui commencent par « . » par défaut

Pour que NuGet fonctionne correctement avec les systèmes de contrôle de code source tels que Subversion et mercurial, NuGet. exe ignore les dossiers et les fichiers qui commencent par le caractère « . » lors de la création de packages. Vous pouvez le remplacer à l’aide de deux nouveaux indicateurs :

* __-NoDefaultExcludes__ est utilisé pour remplacer ce paramètre et inclure tous les fichiers.
* __-Exclude__ est utilisé pour ajouter d’autres fichiers/dossiers à exclure à l’aide d’un modèle. Par exemple, pour exclure tous les fichiers avec l’extension de fichier « . bak »

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Remarque : le modèle n’est pas récursif par défaut._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Prise en charge des projets WiX et de .NET micro Framework

Grâce aux contributions de la Communauté, NuGet prend en charge les types de projets WiX, ainsi que le .NET micro Framework.

## <a name="bug-fixes"></a>Correctifs de bogues

Pour obtenir la liste complète des correctifs de bogues, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correction des bogues à noter

* Les packages avec des fichiers sources fonctionnent dans les deux sites Web et dans les projets d’application Web.
Pour les sites Web, les fichiers sources sont copiés dans le dossier `App_Code`
