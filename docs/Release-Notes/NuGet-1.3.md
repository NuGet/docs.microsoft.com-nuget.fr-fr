---
title: Notes de publication NuGet 1.3 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour 1.3 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 1.3 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-13-release-notes"></a>Notes de version 1.3 de NuGet

[Notes de publication NuGet 1.2](../release-notes/nuget-1.2.md) | [NuGet 1.4 Notes de publication](../release-notes/nuget-1.4.md)

NuGet 1.3 a été publiée le 25 avril 2011.

## <a name="new-features"></a>Nouvelles fonctionnalités

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Création simplifiée d’un Package avec l’intégration du serveur de symboles

L’équipe NuGet en partenariat avec le personnel à [SymbolSource.org](http://www.symbolsource.org/) pour offrir un moyen simple de la publication de vos sources et les du PDB en même temps que votre package. Cela permet aux consommateurs de votre package de pas à pas détaillé de la source de votre package dans le débogueur. Pour plus d’informations, consultez [création et la publication d’un Package de symbole](../create-packages/symbol-packages.md) la méthode simple pour publier des packages NuGet avec des sources. Vous pouvez également regarder une démonstration en direct de cette fonctionnalité dans le cadre de NuGet en profondeur parler à Mix11. Cette fonctionnalité est pleinement démontrée en commençant à la marque de 20 minutes de la vidéo.

### <a name="open-packagepage-command"></a>`Open-PackagePage`Commande

Cette commande facilite l’accès à la page de projet pour un package à partir de la console du Gestionnaire de Package. Il fournit également des options pour ouvrir l’URL de licence et la page du rapport abus pour le package.
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

Assigne l’URL de licence à la variable $url sans ouvrir l’URL dans un navigateur.

### <a name="performance-improvements"></a>Amélioration des performances

NuGet 1.3 introduit de nombreuses améliorations des performances. NuGet 1.3 évite de téléchargement de la même version d’un package plusieurs fois en incluant un cache de l’utilisateur local. Le cache sont accessibles et désactivé via la boîte de dialogue Paramètres du Gestionnaire de Package :

![Boîte de dialogue Options NuGet avec les paramètres de Cache de Package](./media/nuget-options.png)

Autres améliorations des performances incluent la prise en charge de la compression HTTP et améliore la vitesse d’installation de package dans Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio et nuget.exe utilise la même liste de sources de package

Avant de NuGet 1.3, la liste des sources de package utilisé par nuget.exe et le complément NuGet Visual Studio n’étaient pas stockés au même endroit. NuGet 1.3 utilise désormais la même liste dans les deux emplacements. La liste est stockée dans `NuGet.Config` et stockés dans le dossier AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe ignore les fichiers et dossiers qui commencent par «. » par défaut

Pour fonctionner avec les systèmes de contrôle de code source ces Mercurial et la sous-version NuGet, nuget.exe ignore les dossiers et fichiers qui commencent par le '.' caractère lors de la création de packages. Cela peut être substituée à l’aide de deux nouveaux indicateurs :

* __-NoDefaultExcludes__ est utilisée pour remplacer ce paramètre et d’inclure tous les fichiers.
* __-Exclure__ est utilisé pour ajouter d’autres fichiers/dossiers à exclure à l’aide d’un modèle. Par exemple, pour exclure tous les fichiers avec l’extension de fichier '.bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Remarque : le modèle n’est pas récursive par défaut._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Prise en charge des projets WiX et Micro .NET Framework

Grâce aux contributions de la Communauté, NuGet prend en charge les types de projets WiX, ainsi que le Micro de .NET Framework.

## <a name="bug-fixes"></a>Correctifs de bogues

Pour obtenir une liste complète des correctifs de bogues, veuillez consulter le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correctifs de bogues à noter

* Les packages avec les fichiers sources fonctionnent dans les deux sites Web et projets d’Application Web.
Pour les sites Web, les fichiers sources sont copiés dans le `App_Code` dossier
