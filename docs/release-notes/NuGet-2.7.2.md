---
title: Notes de publication de NuGet 2.7.2
description: Notes de publication pour NuGet 2.7.2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776776"
---
# <a name="nuget-272-release-notes"></a>Notes de publication de NuGet 2.7.2

Notes de publication de [NuGet 2.7.1](../release-notes/nuget-2.7.1.md)  |  [Notes de publication de NuGet 2,8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 a été publié le 11 novembre 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Fonctionnalités et correctifs de bogues remarquables

### <a name="license-text"></a>Texte de licence
Pendant un certain temps, Microsoft a inclus les packages NuGet pour plusieurs bibliothèques Open source populaires dans le cadre des modèles par défaut pour les projets d’application Web dans Visual Studio. jQuery est probablement l’exemple le plus connu de ce type de bibliothèque. En raison du contrat de support associé aux composants livrés avec un produit, le fichier de script du package contient un texte de licence différent du fichier de script trouvé dans le même package dans la Galerie nuget.org publique. Cette différence de texte peut empêcher des mises à jour de package de se poursuivre en raison des différents blocs de texte de licence, ce qui entraîne des valeurs de hachage de contenu différentes pour les fichiers de script (et donc être traitées comme modifiées dans le projet).

Pour atténuer ce problème, NuGet 2.7.2 permet à l’auteur du script d’inclure le bloc de texte de licence dans une section spécialement marquée qui se présente comme suit.

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

Lors de la mise à jour de packages avec des fichiers de contenu contenant ce bloc, NuGet ne factorise pas le contenu du bloc dans la comparaison avec la version sur la galerie NuGet et peut donc supprimer et mettre à jour le fichier de contenu comme s’il corresponde à la copie d’origine.

Ce bloc est identifié par le texte « NUGET : BEGIN LICENSE TEXT » et « NUGET : END LICENSE TEXT » qui se produit n’importe où sur les lignes de début et de fin.  Il n’existe aucune autre exigence de mise en forme, ce qui permet d’utiliser cette fonctionnalité dans n’importe quel type de fichier texte, quelle que soit la langue.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Ajouter des redirections de liaison pour les assemblys non-Framework
Pour les assemblys qui font partie du .NET Framework, NuGet ignore l’ajout de redirections de liaison dans le fichier de configuration de l’application lors de la mise à jour du package. Ce correctif s’adresse à une régression dans NuGet 2,7, où les redirections de liaison n’ont pas été ajoutées pour certains assemblys, même si ces assemblys ne sont pas considérés comme faisant partie du .NET Framework. NuGet 2.7.2 restaure le comportement précédent de NuGet 2,5 et 2,6 et ajoute les redirections de liaison.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Installation de bibliothèques portables avec les outils Xamarin installés
Lorsque les outils de développement Xamarin sont installés sur un ordinateur, ils modifient les données de configuration des frameworks pris en charge pour spécifier la compatibilité entre les combinaisons de Framework cible existantes et les frameworks Xamarin. Avec la version 2.7.2, NuGet prend désormais en charge ces règles de compatibilité implicites et permet ainsi aux développeurs ciblant des plates-formes Xamarin d’installer des bibliothèques portables compatibles Xamarin, mais qui ne sont pas explicitement marquées comme telles dans les métadonnées du package.

### <a name="machine-wide-configuration-settings-honored"></a>Paramètres de configuration au niveau de l’ordinateur honorés
Lors de l’utilisation de fichiers Nuget.Config hiérarchiques, la clé repositoryPath n’était pas respectée pour les fichiers Nuget.Config les plus proches de la racine de la solution. Dans Visual Studio 2013, NuGet installe un fichier Nuget.Config personnalisé à% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config afin d’ajouter la source de package « Microsoft et .NET ». Par conséquent, la solution de contournement pour l’utilisation d’un repositoryPath personnalisé dans une solution consistait à supprimer la Nuget.Config au niveau de l’ordinateur, qui signifiait également la suppression de la source du package « Microsoft et .NET ». NuGet 2.7.2 honore désormais les règles de précédence pour repositoryPath lors de l’utilisation de fichiers Nuget.Config hiérarchiques.

## <a name="all-changes"></a>Toutes les modifications
Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2.7.2, consultez le [suivi des problèmes NuGet pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
