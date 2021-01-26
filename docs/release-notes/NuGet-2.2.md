---
title: Notes de publication de NuGet 2,2
description: Notes de publication de NuGet 2,2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780429"
---
# <a name="nuget-22-release-notes"></a>Notes de publication de NuGet 2,2

Notes de publication de [NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Notes de publication de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

NuGet 2,2 a été publié le 12 décembre 2012.

## <a name="visual-studio-quick-launch"></a>Lancement rapide Visual Studio
L’une des nouvelles fonctionnalités qui ont été ajoutées dans Visual Studio 2012 était la [boîte de dialogue lancement rapide](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2,2 étend cette boîte de dialogue, ce qui lui permet d’initialiser la boîte de dialogue du gestionnaire de package avec les termes de recherche entrés dans le lancement rapide. Par exemple, l’entrée de « jQuery » dans le lancement rapide comprend désormais une option dans les résultats pour rechercher les packages NuGet correspondant à « jQuery ».

![NuGet dans Visual Studio lancement rapide](./media/quick-launch.png)

Si cette option est sélectionnée, l’expérience de recherche du gestionnaire de package NuGet standard est lancée pour le terme « jQuery ».

![Boîte de dialogue du gestionnaire de package NuGet préremplie](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Spécifier le dossier entier pour le contenu du package
NuGet 2,2 vous permet désormais de spécifier un dossier entier dans l' `<file>` élément du `.nuspec` fichier pour inclure tout le contenu de ce dossier. Par exemple, le code suivant entraîne l’ajout de tous les scripts du dossier scripts du package au dossier contents\scripts lorsque le package est installé dans un projet.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Mise à jour 6/24/16 : les dossiers vides dans le dossier « contenu » sont ignorés lors de l’installation du package.**

## <a name="known-issues"></a>Problèmes connus

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>L’installation du package échoue pour les projets F # lors de l’utilisation de la console du gestionnaire de package
Lorsque vous tentez d’installer un package NuGet dans un projet F # à l’aide de la console du gestionnaire de package, une exception InvalidOperationException est levée. Nous travaillons activement avec l’équipe F # pour résoudre le problème, mais dans le même temps, la solution consiste à installer des packages NuGet dans des projets F # via la boîte de dialogue du gestionnaire de package de NuGet plutôt que la console. Des [informations supplémentaires sont disponibles sur CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Résolutions de bogues
NuGet 2,2 comprend de nombreux correctifs de bogues. Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2,2, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
