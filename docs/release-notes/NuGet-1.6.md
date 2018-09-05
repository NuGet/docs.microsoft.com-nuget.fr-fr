---
title: Notes de version 1.6 de NuGet
description: Notes de publication pour 1.6 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549010"
---
 # <a name="nuget-16-release-notes"></a>Notes de version 1.6 de NuGet

[Notes de publication de NuGet 1.5](../release-notes/nuget-1.5.md) | [Notes de publication de NuGet 1.7](../release-notes/nuget-1.7.md)

1.6 de NuGet a été publiée le 13 décembre 2011.

## <a name="known-installation-issue"></a>Problème d’Installation connus
Si vous exécutez Visual Studio 2010 SP1, vous pouvez rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet si vous avez une version antérieure est installée.

La solution de contournement consiste à désinstaller simplement NuGet, puis l’installer à partir de la galerie d’extensions Visual Studio.  Pour plus d’informations, consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis vous avez probablement besoin de redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».

## <a name="features"></a>Fonctionnalités

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Prise en charge pour le contrôle de version sémantique et les Packages de version préliminaire
1.6 de NuGet prend désormais en charge pour la gestion sémantique de version (SemVer). Pour plus d’informations sur la façon dont il utilise SemVer, lisez le [documentation sur le contrôle de version](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>À l’aide de NuGet sans vérifier dans des Packages (restauration de Package)
1.6 de NuGet prend désormais en charge de première classe pour le flux de travail dans le NuGet packages ne sont pas ajoutés au contrôle de code source, mais au lieu de cela sont restaurés au moment de la génération s’il est manquant. Pour plus d’informations, consultez le [à l’aide de NuGet sans validation des packages pour le contrôle de code source](../consume-packages/packages-and-source-control.md) rubrique.

### <a name="item-templates-that-install-nuget-packages"></a>Modèles d’élément qui installer les Packages NuGet
S’appuyant sur le travail pour prendre en charge les packages NuGet préinstallés les modèles de projet Visual Studio, NuGet 1.6 ajoute également la prise en charge pour les modèles d’élément Visual Studio. Modèles d’élément peuvent avoir des packages NuGet qui sont installés lorsque le modèle dans appelé associées.

Pour plus d’informations sur la modification d’un modèle de projet/élément pour installer les packages NuGet, lisez le [Packages dans les modèles Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) rubrique.

### <a name="support-for-disabling-package-sources"></a>Prise en charge de la désactivation des sources de package
Lorsque plusieurs sources de package sont configurées, NuGet recherche dans chacun d’eux pour les packages lors de l’installation d’un package et ses dépendances. Une source de package est arrêté pour une raison quelconque peut sérieusement ralentir NuGet.

Avant NuGet 1.6, vous pouvez supprimer la source du package, mais vous devez ensuite n’oubliez pas les détails du moment où vous souhaitez pour l’ajouter de nouveau.

NuGet 1.6 permet une source de package pour le désactiver, mais gardez-le décochant l’option.

![La désactivation d’un package](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1.6 avait un total de 106 fixe des éléments de travail. 95 de ceux qui ont été classés comme des bogues et 10 de ces étaient des fonctionnalités.

Pour obtenir une liste complète de travail éléments résolus dans NuGet 1.6, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
