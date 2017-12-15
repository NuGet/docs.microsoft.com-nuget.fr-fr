---
title: Notes de publication NuGet 1.6 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ed433790-99bf-4b71-92a8-17314bd49867
description: "Notes de publication pour 1.6 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 1.6 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7824d62cb73c54205175ec742cfc26d1ca3aa741
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
 # <a name="nuget-16-release-notes"></a>Notes de version 1.6 de NuGet

[Notes de publication NuGet 1.5](../release-notes/nuget-1.5.md) | [Notes de version 1.7 de NuGet](../release-notes/nuget-1.7.md)

NuGet 1.6 a été publiée le 13 décembre 2011.

## <a name="known-installation-issue"></a>Problème connu d’Installation
Si vous exécutez Visual Studio 2010 SP1, vous susceptible de rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet, si vous disposez d’une version plus ancienne est installée.

La solution de contournement consiste à simplement désinstaller NuGet et l’installer à partir de la galerie d’extensions Visual Studio.  Consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) pour plus d’informations.

Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis il est probable que devez redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».

## <a name="features"></a>Fonctionnalités

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Prise en charge pour le contrôle de version sémantique et les versions préliminaires des Packages
NuGet 1.6 introduit la prise en charge pour le contrôle de version sémantique (SemVer). Pour plus d’informations sur la façon dont il utilise SemVer, lisez le [documentation du contrôle de version](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>À l’aide de NuGet sans vérifier dans des Packages (restauration de Package)
NuGet 1.6 prend désormais en charge de première classe pour le flux de travail dans le NuGet packages ne sont pas ajoutés au contrôle de code source, mais au lieu de cela sont restaurés au moment de la génération si manquant. Pour plus d’informations, lisez la [à l’aide de NuGet sans validation des packages pour le contrôle de code source](../consume-packages/packages-and-source-control.md) rubrique.

### <a name="item-templates-that-install-nuget-packages"></a>Modèles d’élément qui installent des Packages NuGet
Basé sur le travail pour prendre en charge les package NuGet préinstallé aux modèles de projet Visual Studio, 1.6 de NuGet ajoute également la prise en charge pour les modèles d’élément Visual Studio. Modèles d’élément peuvent posséder des packages NuGet qui sont installées lorsque le modèle d’invoqué associées.

Pour plus d’informations sur la modification d’un modèle de projet/élément pour installer les packages NuGet, consultez le [Packages dans les modèles Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) rubrique.

### <a name="support-for-disabling-package-sources"></a>Prise en charge de la désactivation des sources de package
Lorsque plusieurs sources de package sont configurés, NuGet recherchera dans chacun d’eux pour les packages lors de l’installation d’un package et ses dépendances. Une source de package est arrêté pour une raison quelconque peut gravement ralentissent NuGet.

Avant NuGet 1.6, vous pourriez supprimer la source du package, mais vous devez mémoriser les détails lorsque vous souhaitez ajouter de nouveau.

NuGet 1.6 permet de désactivation d’une source de package pour le désactiver, mais l’application.

![La désactivation d’un package](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1.6 comportait 106 fixe des éléments de travail. 95 de celles qui ont été classés en tant que bogues et 10 d'entre eux ont des fonctionnalités.

Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.6, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
