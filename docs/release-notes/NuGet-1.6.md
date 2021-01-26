---
title: Notes de publication de NuGet 1,6
description: Notes de publication de NuGet 1,6, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777009"
---
 # <a name="nuget-16-release-notes"></a>Notes de publication de NuGet 1,6

Notes de publication de [NuGet 1,5](../release-notes/nuget-1.5.md)  |  [Notes de publication de NuGet 1,7](../release-notes/nuget-1.7.md)

NuGet 1,6 a été publié le 13 décembre 2011.

## <a name="known-installation-issue"></a>Problème d’installation connu
Si vous exécutez VS 2010 SP1, vous pouvez rencontrer une erreur d’installation lors de la tentative de mise à niveau de NuGet si une version antérieure est installée.

La solution consiste à désinstaller simplement NuGet, puis à l’installer à partir de la Galerie d’extensions Visual Studio.  Consultez la rubrique <https://support.microsoft.com/kb/2581019> (éventuellement en anglais) pour plus d'informations.

Remarque : si Visual Studio ne vous permet pas de désinstaller l’extension (le bouton désinstaller est désactivé), vous devrez probablement redémarrer Visual Studio à l’aide de « exécuter en tant qu’administrateur ».

## <a name="features"></a>Fonctionnalités

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Prise en charge du contrôle de version sémantique et des packages de préversion
NuGet 1,6 introduit la prise en charge de la gestion sémantique des versions (SemVer). Pour plus d’informations sur l’utilisation de SemVer, consultez la documentation sur le contrôle de [version](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Utilisation de NuGet sans archiver les packages (restauration des packages)
NuGet 1,6 dispose désormais de la prise en charge de première classe pour le flux de travail dans lequel les packages NuGet ne sont pas ajoutés au contrôle de code source, mais ils sont restaurés au moment de la génération s’ils sont manquants. Pour plus d’informations, consultez la rubrique [utilisation de NuGet sans validation des packages dans le contrôle de code source](../consume-packages/packages-and-source-control.md) .

### <a name="item-templates-that-install-nuget-packages"></a>Modèles d’élément qui installent des packages NuGet
En s’appuyant sur le travail pour prendre en charge le package NuGet préinstallé dans les modèles de projet Visual Studio, NuGet 1,6 ajoute également la prise en charge des modèles d’élément Visual Studio. Les modèles d’élément peuvent avoir des packages NuGet associés qui sont installés lors de l’appel du modèle.

Pour plus d’informations sur la modification d’un modèle de projet/d’élément en vue d’installer des packages NuGet, consultez la rubrique [packages dans les modèles Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .

### <a name="support-for-disabling-package-sources"></a>Prise en charge de la désactivation des sources de packages
Lorsque plusieurs sources de package sont configurées, NuGet les recherche pour les packages lors de l’installation d’un package et de ses dépendances. Une source de package déverrouillée pour une raison quelconque peut gravement ralentir NuGet.

Avant NuGet 1,6, vous pouviez supprimer la source du package, mais vous devez vous souvenir des détails relatifs au moment où vous souhaitez l’ajouter de nouveau dans.

NuGet 1,6 permet de désélectionner une source de package pour la désactiver, tout en la conservant.

![Désactivation d’un package](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Résolutions de bogues
NuGet 1,6 avait un total de 106 éléments de travail corrigés. 95 de celles-ci ont été classées comme des bogues et 10 de ces fonctionnalités.

Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 1,6, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
