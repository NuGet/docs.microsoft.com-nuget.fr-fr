---
title: Notes de publication NuGet 2.2 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour 2.2 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 2.2 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 63a1ae2315ea0c26fb5d26507ac0bcba8567aa9a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-22-release-notes"></a>Notes de version 2.2 NuGet

[Notes de publication NuGet 2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Notes de publication](../release-notes/nuget-2.2.1.md)

2.2 de NuGet a été publiée le 12 décembre 2012.

## <a name="visual-studio-quick-launch"></a>Lancement rapide Visual Studio
L’une des nouvelles fonctionnalités qui a été ajoutée dans Visual Studio 2012 était le [boîte de dialogue de lancement rapide](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 étend cette boîte de dialogue, ce qui lui permet d’initialiser la boîte de dialogue de gestionnaire de package avec les termes de recherche entrés dans le volet Lancement rapide. Par exemple, si vous saisissez 'jquery' dans Lancement rapide maintenant inclut une option dans les résultats pour rechercher les packages NuGet correspondant à 'jquery'.

![NuGet dans Lancement rapide Visual Studio](./media/quick-launch.png)

Cette option lancera standard NuGet package manager fonctions de recherche pour le terme 'jquery'.

![Boîte de dialogue Gestionnaire de Package NuGet prédéfinie](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Spécifiez la totalité du dossier pour le contenu du Package
2.2 de NuGet vous permet désormais de spécifier un dossier entier dans le `<file>` élément de la `.nuspec` fichier à inclure tout le contenu de ce dossier. Par exemple, les éléments suivants provoquent tous les scripts dans le dossier de scripts du package à ajouter au dossier contents\scripts lorsque le package est installé dans un projet.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Mettre à jour 24/6/16 : les dossiers vides dans le dossier « content » sont ignorés lors de l’installation du package.**

## <a name="known-issues"></a>Problèmes connus

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Installation du package échoue pour les projets F # lors de l’utilisation de la console du Gestionnaire de package
Lorsque vous tentez d’installer un package NuGet dans un projet F # à l’aide de la console du Gestionnaire de package, une exception InvalidOperationException est levée. Nous travaillons activement avec F # à l’équipe de résoudre le problème, mais en attendant, la solution de contournement consiste à installer des packages NuGet dans des projets F # via la boîte de dialogue Gestionnaire de package de NuGet au lieu de la console. [Informations supplémentaires sont disponibles sur CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 2.2 inclut de nombreux correctifs de bogues. Pour obtenir la liste complète de travail éléments corrigés dans NuGet 2.2, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
