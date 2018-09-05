---
title: Notes de publication de NuGet 2.7.2
description: Notes de publication pour NuGet 2.7.2, notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550068"
---
# <a name="nuget-272-release-notes"></a>Notes de publication de NuGet 2.7.2

[Notes de publication de NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [Notes de publication NuGet 2.8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 a été publiée le 11 novembre 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Les correctifs de bogues dignes d’intérêt et de fonctionnalités

### <a name="license-text"></a>Texte de la licence
Pendant un certain temps, Microsoft a inclus les packages NuGet pour plusieurs bibliothèques open source populaires dans le cadre des modèles par défaut pour les projets d’application Web dans Visual Studio. jQuery est probablement le plus connu exemple de ce type de bibliothèque. En raison de l’accord de prise en charge associé aux composants qui sont fournies avec un produit, le fichier du package script contient du texte de licences différent que le fichier de script trouvé dans le même package dans la galerie nuget.org publique. Cette différence de texte peut empêcher les mises à jour de package aboutir à la suite les blocs de texte de licences différent à l’origine les fichiers de script à avoir des valeurs de hachage de contenu différente (et par conséquent, pour être considérées comme modifié dans le projet).

Pour résoudre ce problème, NuGet 2.7.2 permet à l’auteur de script inclure le bloc de texte de licence dans une section spécialement marquée qui se présente comme suit.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Lors de la mise à jour des packages avec du contenu fichiers contenant ce bloc, NuGet ne pas factoriser le contenu du bloc dans la comparaison avec la version dans la galerie NuGet et peut donc supprimer et mettre à jour le fichier de contenu comme s’il correspond à la copie d’origine.

Ce bloc est identifié par le texte « NUGET : commencer licence TEXT » et « NUGET : fin licence TEXT » qui se produisent n’importe où sur le début et fin de ligne.  Aucune autre condition de mise en forme requise n’existe, ce qui permet cette fonctionnalité à utiliser dans n’importe quel type de fichier texte, quel que soit le langage.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Ajouter des redirections de liaison pour les assemblys non Framework
Pour les assemblys qui font partie du .NET Framework, NuGet ignore l’ajout des redirections de liaison dans le fichier de configuration de l’application lors de la mise à jour le package. Les adresses de ce correctif une régression dans NuGet 2.7 par laquelle les redirections de liaison ont été pas ajoutées pour certains assemblys, même si ces assemblys ne sont pas considérés comme une partie du .NET Framework. NuGet 2.7.2 restaure la précédente NuGet 2.5 et 2.6 comportement et ajoute les redirections de liaison.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>L’installation des bibliothèques portables avec des outils Xamarin installé
Lorsque les outils de développement de Xamarin sont installés sur un ordinateur, ils modifier les données de configuration des frameworks pris en charge pour spécifier la compatibilité entre les infrastructures de Xamarin et les combinaisons de framework cible existant. Avec la version 2.7.2, NuGet est désormais compatible avec ces règles de compatibilité implicite et par conséquent facilite pour les développeurs ciblant des plates-formes de Xamarin installer les bibliothèques portables qui sont compatibles avec Xamarin, mais pas explicitement marquée en tant que tel dans le package métadonnées.

### <a name="machine-wide-configuration-settings-honored"></a>Paramètres de configuration de l’ordinateur honorées
Lorsque vous utilisez des fichiers Nuget.Config hiérarchiques, la clé repositoryPath a été pas respectée pour les fichiers Nuget.Config le plus proche de la racine de la solution. Dans Visual Studio 2013, NuGet installe un fichier Nuget.Config personnalisé à %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config afin d’ajouter la source du package « Microsoft et .NET ». Par conséquent, la solution de contournement pour l’utilisation d’un repositoryPath personnalisé dans une solution a été de supprimer le fichier Nuget.Config au niveau de l’ordinateur - ce qui signifiait également la suppression de la source du package « Microsoft et .NET ». NuGet 2.7.2 respecte désormais les règles de priorité pour repositoryPath lors de l’utilisation de fichiers hiérarchiques de Nuget.Config.

## <a name="all-changes"></a>Toutes les modifications
Pour obtenir une liste complète de travail éléments résolus dans NuGet 2.7.2, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
