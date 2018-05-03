---
title: Référence de l’interface utilisateur du Gestionnaire de Package NuGet
description: Instructions sur l’utilisation du Gestionnaire de Package NuGet UI dans Visual Studio pour travailler avec les packages NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 99bd51798460a56cb8515d46791a9e75d9e630cc
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-package-manager-ui"></a>Interface utilisateur du Gestionnaire de Package NuGet

Le Gestionnaire de Package NuGet UI dans Visual Studio sur Windows vous permet facilement installer, désinstaller et mettre à jour les packages NuGet dans des projets et solutions. Pour une expérience dans Visual Studio pour Mac, consultez [package, y compris un NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough). Le Gestionnaire de Package UI n’est pas incluse dans Visual Studio Code.

Dans cette rubrique :

- [Rechercher et installer un package (onglet Parcourir)](#finding-and-installing-a-package)
- [Désinstallation d’un package (onglet installé)](#uninstalling-a-package)
- [Mise à jour d’un package (onglets installées et mises à jour)](#updating-a-package) (inclut le [« Référencée par un kit de développement implicitement » ou « AutoReferenced » message](#implicit_reference))
- [Gestion des packages pour la solution](#managing-packages-for-the-solution) (travailler avec plusieurs projets en même temps).
- [Sources de package](#package-sources)
- [Contrôlent des Options du Gestionnaire de package](#package-manager-options-control)

> [!Note]
> Si vous êtes pas le Gestionnaire de Package NuGet dans Visual Studio 2015, consultez **Outils > Extensions et mises à jour...**  et recherchez le *Gestionnaire de Package NuGet* extension. Si vous ne parvenez pas à utiliser le programme d’installation des extensions dans Visual Studio, téléchargez l’extension directement à partir de [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> Visual Studio 2017, NuGet et le Gestionnaire de Package NuGet sont installées automatiquement avec n’importe quelle. Charges de travail liées au réseau. Installer individuellement en sélectionnant le **des composants individuels > Code Outils > Gestionnaire de package NuGet** option dans le programme d’installation de Visual Studio 2017.

## <a name="finding-and-installing-a-package"></a>Rechercher et installer un package

1. Dans **l’Explorateur de solutions**, avec le bouton droit soit **références** ou un projet, puis sélectionnez **gérer les Packages NuGet...** .

    ![Gérer l’option de menu de Packages NuGet](media/ManagePackagesUICommand.png)

1. Le **Parcourir** onglet affiche les packages en popularité à partir de la source actuellement sélectionnée (consultez [sources du package](#package-sources)). Recherchez un package spécifique à l’aide de la zone de recherche dans l’angle supérieur gauche. Sélectionner un package à partir de la liste pour afficher les informations, qui permet également la **installer** bouton avec une liste déroulante Sélection de la version.

    ![Gérer l’onglet Parcourir de boîte de dialogue de Packages NuGet](media/Search.png)

1. Sélectionnez la version souhaitée dans la liste déroulante et sélectionnez **installer**. Visual Studio installe le package et ses dépendances dans le projet. Vous pouvez être invité à accepter les termes du contrat de licence. Lors de l’installation est terminée, l’ajout de packages s’affichent sur le **installé** onglet. Les packages sont également répertoriés dans le **références** nœud de l’Explorateur de solutions, indiquant que vous pouvez y faire référence dans le projet avec `using` instructions.

    ![Références dans l’Explorateur de solutions](media/References.png)

> [!Tip]
> Pour inclure les versions préliminaires dans la recherche et de proposer des versions préliminaires dans la version de liste déroulante, sélectionnez le **inclure la version préliminaire** option.

## <a name="uninstalling-a-package"></a>Désinstaller un package

1. Dans **l’Explorateur de solutions**, avec le bouton droit soit **références** ou le projet de votre choix, puis sélectionnez **gérer les Packages NuGet...** .
1. Sélectionnez le **installé** onglet.
1. Sélectionnez le package à désinstaller (à l’aide de la recherche pour filtrer la liste si nécessaire) et sélectionnez **désinstallation**.

    ![Désinstaller un package](media/UninstallPackage.png)

1. Notez que la **inclure la version préliminaire** et **source du Package** contrôles n’ont aucun effet lors de la désinstallation des packages.

## <a name="updating-a-package"></a>Mettre à jour un package

1. Dans **l’Explorateur de solutions**, avec le bouton droit soit **références** ou le projet de votre choix, puis sélectionnez **gérer les Packages NuGet...** . (Dans les projets de site web, cliquez sur le **Bin** dossier.)
1. Sélectionnez le **mises à jour** onglet pour afficher les packages qui ont des mises à jour disponibles à partir des sources de package sélectionné. Sélectionnez **inclure la version préliminaire** pour inclure les versions préliminaires des packages dans la liste de mise à jour.
1. Sélectionnez le package à mettre à jour, sélectionnez la version souhaitée dans la liste déroulante à droite, puis sélectionnez **mettre à jour**.

    ![Mettre à jour un package](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Pour certains packages, les **mise à jour** bouton est désactivé et un message s’affiche indiquant qu’il est « implicitement référencé par un SDK » (ou « AutoReferenced »). Le message indique que le package, telles que Microsoft.NETCore.App ou Microsoft.NETStandard.Library, fait partie d’un plus grand framework ou kit de développement logiciel et ne doit pas être mis à jour indépendamment. (Ces packages sont marqués en interne avec `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Pour mettre à jour le package, mettre à jour le Kit de développement logiciel auquel il appartient.

    ![Exemple de package est marqué comme implicitement AutoReferenced ou référence](media/PackageManagerUIAutoReferenced.png)

1. Pour mettre à jour plusieurs packages vers leurs versions les plus récents, sélectionnez-les dans la liste et sélectionnez le **mettre à jour** bouton au-dessus de la liste.
1. Vous pouvez également mettre à jour un package individuel à partir de la **installé** onglet. Dans ce cas, les détails du package d’incluent un sélecteur de version (soumis à la **inclure la version préliminaire** option) et un **mise à jour** bouton.

## <a name="managing-packages-for-the-solution"></a>Gestion des packages pour la solution

Gestion des packages pour une solution sont un moyen pratique de travailler avec plusieurs projets simultanément.

1. Sélectionnez le **Outils > Gestionnaire de Package NuGet > Gérer les Packages NuGet pour la Solution...**  menu de commande, ou avec le bouton droit de la solution et sélectionnez **gérer les Packages NuGet...** :

    ![Gérer les packages NuGet pour la solution](media/ManagePackagesSolutionUICommand.png)

1. Lors de la gestion des packages pour la solution, l’interface utilisateur vous permet de sélectionner les projets qui sont affectés par les opérations :

    ![Sélecteur de projet lors de la gestion des packages pour la solution](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Consolider onglet

Les développeurs estiment généralement pas recommandé d’utiliser des versions différentes du même package NuGet sur différents projets dans la même solution. Lorsque vous choisissez de gérer les packages d’une solution, le Gestionnaire de Package UI fournit un **consolider** onglet sur lequel vous pouvez facilement voir où les packages avec des numéros de version distincts sont utilisés par différents projets dans la solution :

![Onglet de consolidation de l’interface utilisateur Gestionnaire de package](media/ConsolidateTab.png)

Dans cet exemple, le projet ClassLibrary1 est à l’aide de EntityFramework 6.2.0, tandis que ConsoleApp1 est à l’aide de EntityFramework 6.1.0. Pour consolider les versions de package, procédez comme suit :

- Sélectionnez les projets à mettre à jour dans la liste des projets.
- Sélectionnez la version à utiliser dans tous les projets de la **Version** contrôle, tels que EntityFramework 6.2.0.
- Sélectionnez le **installer** bouton.

Le Gestionnaire de Package installe la version du package sélectionné dans tous les projets sélectionnés, après laquelle le package n’apparaît plus dans le **consolider** onglet.

## <a name="package-sources"></a>Sources de package

Pour modifier la source à partir de laquelle Visual Studio obtient les packages, sélectionnez une à partir de la sélection de la source :

![Sélecteur de source de package dans l’interface utilisateur du Gestionnaire de package](media/PackageSourceDropDown.png)

Pour gérer les sources de package :

1. Sélectionnez le **paramètres** icône dans le Gestionnaire de Package UI décrites ci-dessous ou utilisez le **Outils > Options** de commandes et accédez à **Gestionnaire de Package NuGet**:

    ![Icône des paramètres de l’interface utilisateur package manager](media/PackageSourceSettings.png)

1. Sélectionnez le **Sources de Package** nœud :

    ![Options de Sources de package](media/options.png)

1. Pour ajouter une source, sélectionnez **+**, modifiez le nom, entrez l’URL ou le chemin d’accès dans le **Source** contrôler, puis sélectionnez **mise à jour**. La source apparaît maintenant dans la liste déroulante du sélecteur.
1. Pour modifier une source de package, sélectionnez-le, apporter des modifications dans le **nom** et **Source** cases, puis sélectionnez **mise à jour**.
1. Pour désactiver une source de package, désactivez la case à gauche du nom dans la liste.
1. Pour supprimer une source de package, sélectionnez-le, puis le **X** bouton.
1. Utilisez le haut et flèche bas pour modifier l’ordre de priorité des sources de package. Visual Studio recherche dans ces sources dans l’ordre de priorité lors de la restauration des packages pour un projet. Pour plus d’informations, consultez [restauration du Package](../consume-packages/package-restore.md).

> [!Tip]
> Si une source de package s’affiche de nouveau après l’avoir supprimée, il peut être répertorié dans un niveau de l’ordinateur ou utilisateur `NuGet.Config` fichiers. Consultez [NuGet de configuration de comportement](../consume-packages/configuring-nuget-behavior.md) pour l’emplacement de ces fichiers, puis supprimer la source en modifiant les fichiers manuellement ou en utilisant le [nuget sources commande](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Contrôlent des Options du Gestionnaire de package

Lorsqu’un package est sélectionné, le Gestionnaire de Package UI affiche un petit, extensible **Options** contrôle ci-dessous le sélecteur de version (illustré à la fois réduit et développé). Notez que, pour certains projets, types, uniquement le **afficher la fenêtre Aperçu** option est fournie.

![Options du Gestionnaire de package](media/PackageManagerUIOptions.png)

Les sections suivantes décrivent ces options.

### <a name="show-preview-window"></a>Afficher la fenêtre d’aperçu

Sélectionné, une fenêtre modale affiche ce qui les dépendances d’un package choisi avant que le package est installé :

![Boîte de dialogue Aperçu exemple](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Installer et mettre à jour des Options

(Non disponible pour tous les types de projet).

**Comportement des dépendances** configure comment NuGet détermine quelles versions des packages dépendants à installer :

- *Ignorer les dépendances* ignore l’installation de toutes les dépendances, qui généralement arrête le package en cours d’installation.
- *La plus basse* [Default] installe la dépendance avec le numéro de version minimal qui répond aux exigences du package principal choisi.
- *Correctif logiciel le plus élevé* installe la version avec les mêmes numéros de version principale et secondaire, mais le numéro de correctif plus élevé. Par exemple, si version 1.2.2 est spécifiée, la version la plus élevée qui commence par une 1.2 sera être installée
- *Mineur plus élevé* installe la version avec le même numéro de version principale, mais le nombre mineur le plus élevé et le nombre de correctifs. Si la version 1.2.2 est spécifiée, la version la plus élevée qui commence par 1 est installée
- *La plus élevée* installe la version disponible la plus récente du package.

**Action de conflit de fichiers** spécifie comment NuGet doit gérer les packages qui existent déjà dans le projet ou l’ordinateur local :

- *Invite de commandes* fait en sorte que NuGet demander s’il faut conserver ou remplacer les packages existants.
- *Ignorer tout* fait en sorte que NuGet pour ignorer le remplacement de des packages existants.
- *Remplacer tous les* fait en sorte que NuGet pour remplacer des packages existants.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Les Options de désinstallation

(Non disponible pour tous les types de projet).

**Supprimer les dépendances**: fois sélectionnée, supprime tous les packages dépendants si elles ne sont pas référencées ailleurs dans le projet.

**Forcer la désinstallation même s’il existe des dépendances sur celui-ci**: lorsque sélectionnée, désinstalle un package même s’il est toujours référencé dans le projet. Cela est généralement utilisé en association avec **supprimer les dépendances** pour supprimer un package et ce que les dépendances qu’il est installé. À l’aide de cette option peut, toutefois, entraîner de références rompues dans le projet. Dans ce cas, vous devrez peut-être [réinstaller ces autres packages](../consume-packages/reinstalling-and-updating-packages.md).
