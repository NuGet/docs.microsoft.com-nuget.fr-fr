---
title: Notes de publication NuGet 2.7.2 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c775d1d7-de26-476c-bf9e-0cf95986a22f
description: "Notes de publication pour NuGet 2.7.2, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 2.7.2 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5bb1eb346666c5d5ee790fcdcd7d844bfd37b22e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-272-release-notes"></a>Notes de mise à jour de NuGet 2.7.2

[Notes de publication NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Notes de publication](../release-notes/nuget-2.8.md)

NuGet 2.7.2 a été publiée le 11 novembre 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Correctifs de bogues importantes et des fonctionnalités

### <a name="license-text"></a>Texte de la licence
Pendant un certain temps, Microsoft a inclus les packages NuGet pour plusieurs bibliothèques open source populaires dans le cadre des modèles par défaut pour les projets d’application Web dans Visual Studio. jQuery est probablement le plus connu exemple de ce type de bibliothèque. En raison de l’accord de prise en charge associé aux composants qui sont fournies avec un produit, le fichier du package script contient du texte de licences différent que le fichier de script trouvé dans le même package dans la galerie publics nuget.org. Cette différence de texte peut empêcher les mises à jour du package à partir de procéder à la suite les blocs de texte de licences différent à l’origine pour que les valeurs de hachage du contenu, les fichiers de script (et par conséquent, pour être considérées comme modifié dans le projet).

Pour résoudre ce problème, NuGet 2.7.2 permet à l’auteur de script inclure le bloc de texte de licence au sein d’une section spécialement marquée qui se présente comme suit.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Lors de la mise à jour des packages avec le contenu contenant ce bloc, les fichiers NuGet ne pas contribuer le contenu du bloc de la comparaison avec la version de la galerie NuGet et peuvent donc supprimer et mettre à jour le fichier de contenu comme si elle correspond à la copie d’origine.

Ce bloc est identifié par le texte « NUGET : commencer licence » et « NUGET : fin licence texte » qui se produisent n’importe où sur le début et de fin de ligne.  Aucune autre condition requise mise en forme n’existe, ce qui permet cette fonctionnalité à utiliser dans n’importe quel type de fichier texte, quelle que soit la langue.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Ajoutez des redirections de liaison d’assemblys non Framework
Pour les assemblys qui font partie du .NET Framework, NuGet ignore l’ajout des redirections de liaison dans le fichier de configuration de l’application lorsque le package de mise à jour. Les adresses de ce correctif une régression dans 2.7 NuGet dans laquelle les redirections de liaison ont été pas ajoutées pour certains assemblys, même si ces assemblys ne sont pas considérés comme une partie du .NET Framework. NuGet 2.7.2 restaure la précédente NuGet 2.5 et comportement 2.6 et ajoute les redirections de liaison.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>L’installation des bibliothèques portables avec des outils Xamarin installé
Lorsque les outils de développement de Xamarin sont installés sur un ordinateur, ils modifier les données de configuration des infrastructures prises en charge pour spécifier la compatibilité entre les combinaisons de framework cible existantes et des infrastructures de Xamarin. Avec la version 2.7.2, NuGet est désormais prenant en charge de ces règles de compatibilité implicite et par conséquent facilite aux développeurs de cibler des plateformes de Xamarin installer les bibliothèques portables qui sont compatibles avec Xamarin, mais ne sont pas explicitement marquée en tant que tel dans le package métadonnées.

### <a name="machine-wide-configuration-settings-honored"></a>Paramètres de configuration de l’échelle de l’ordinateur respectés
Lorsque vous utilisez des fichiers de Nuget.Config hiérarchiques, la clé repositoryPath a été pas été respectée pour les fichiers de Nuget.Config le plus proche de la racine de la solution. Dans Visual Studio 2013, NuGet installe un fichier Nuget.Config personnalisé à %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config afin d’ajouter la source du package « Microsoft et .NET ». Par conséquent, la solution de contournement pour l’utilisation d’un repositoryPath personnalisé dans une solution a été de supprimer le niveau de l’ordinateur Nuget.Config - ce qui signifiait également la suppression de la source du package « Microsoft et .NET ». NuGet 2.7.2 honore désormais les règles de priorité pour repositoryPath lors de l’utilisation des fichiers de Nuget.Config hiérarchiques.

## <a name="all-changes"></a>Toutes les modifications
Pour obtenir la liste complète de travail éléments fixes dans NuGet 2.7.2, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
