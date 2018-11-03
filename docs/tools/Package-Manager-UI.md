---
title: Référence de l’interface utilisateur du Gestionnaire de Package NuGet
description: Instructions sur l’utilisation de l’UI Gestionnaire de Package NuGet dans Visual Studio pour travailler avec les packages NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 1de6ddeca6295c621a90409807af198bc3c7a068
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981182"
---
# <a name="nuget-package-manager-ui"></a>Interface utilisateur du Gestionnaire de Package NuGet

Le Gestionnaire de Package NuGet UI dans Visual Studio sur Windows vous permet facilement installer, désinstaller et mettre à jour les packages NuGet dans les projets et solutions. Pour une expérience dans Visual Studio pour Mac, consultez [, y compris un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough). Le Gestionnaire de Package UI n’est pas inclus avec Visual Studio Code.

Dans cette rubrique :

- [Recherche et installation d’un package (onglet Parcourir)](#finding-and-installing-a-package)
- [Désinstallation d’un package (onglet installé)](#uninstalling-a-package)
- [La mise à jour d’un package (onglets installé et les mises à jour)](#updating-a-package) (inclut le [« Référencée implicitement par un SDK » ou « AutoReferenced » message](#implicit_reference))
- [La gestion des packages pour la solution](#managing-packages-for-the-solution) (travailler avec plusieurs projets en même temps).
- [Sources de package](#package-sources)
- [Contrôlent les Options du Gestionnaire de package](#package-manager-options-control)

> [!Note]
> Si vous êtes pas le Gestionnaire de Package NuGet dans Visual Studio 2015, consultez **Outils > Extensions et mises à jour...**  et recherchez le *Gestionnaire de Package NuGet* extension. Si vous ne parvenez pas à utiliser le programme d’installation des extensions dans Visual Studio, téléchargez l’extension directement à partir de [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> Visual Studio 2017, NuGet et le Gestionnaire de Package NuGet sont installées automatiquement avec n’importe quelle. Charges de travail liées NET. Installer individuellement en sélectionnant le **composants individuels > Outils de Code > Gestionnaire de package NuGet** option dans le programme d’installation de Visual Studio 2017.

## <a name="finding-and-installing-a-package"></a>Recherche et installation d’un package

1. Dans **l’Explorateur de solutions**, avec le bouton droit soit **références** ou un projet, puis sélectionnez **gérer les Packages NuGet...** .

    ![Gérer l’option de menu de Packages NuGet](media/ManagePackagesUICommand.png)

1. Le **Parcourir** onglet affiche les packages par popularité à partir de la source actuellement sélectionnée (consultez [sources de packages](#package-sources)). Recherchez un package spécifique à l’aide de la zone de recherche dans la coin supérieur gauche. Sélectionner un package à partir de la liste pour afficher ses informations, ce qui permet également la **installer** bouton avec une liste déroulante Sélection de la version.

    ![Gérer l’onglet Parcourir de boîte de dialogue de Packages NuGet](media/Search.png)

1. Sélectionnez la version souhaitée dans la liste déroulante et sélectionnez **installer**. Visual Studio installe le package et ses dépendances dans le projet. Vous pouvez être invité à accepter les termes du contrat de licence. Lors de l’installation est terminée, les packages ajoutés s’affichent sur le **installé** onglet. Les packages sont également répertoriés dans le **références** nœud de l’Explorateur de solutions, indiquant que vous puissiez y faire référence dans le projet avec `using` instructions.

    ![Références dans l’Explorateur de solutions](media/References.png)

> [!Tip]
> Pour inclure les versions préliminaires dans la recherche et de proposer des versions préliminaires dans la version de liste déroulante, sélectionnez le **inclure la version préliminaire** option.

## <a name="uninstalling-a-package"></a>Désinstaller un package

1. Dans **l’Explorateur de solutions**, avec le bouton droit soit **références** ou le projet de votre choix, puis sélectionnez **gérer les Packages NuGet...** .
1. Sélectionnez le **installé** onglet.
1. Sélectionnez le package à désinstaller (à l’aide de la recherche pour filtrer la liste si nécessaire), puis sélectionnez **désinstallation**.

    ![Désinstaller un package](media/UninstallPackage.png)

1. Notez que le **inclure la version préliminaire** et **source du Package** contrôles n’ont aucun effet lors de la désinstallation des packages.

## <a name="updating-a-package"></a>Mettre à jour un package

1. Dans **l’Explorateur de solutions**, avec le bouton droit soit **références** ou le projet de votre choix, puis sélectionnez **gérer les Packages NuGet...** . (Dans les projets de site web, cliquez sur le **Bin** dossier.)
1. Sélectionnez le **mises à jour** onglet pour afficher les packages qui ont des mises à jour disponibles à partir des sources de package sélectionné. Sélectionnez **inclure la version préliminaire** à inclure des packages de version préliminaire dans la liste mise à jour.
1. Sélectionnez le package à mettre à jour, sélectionnez la version souhaitée dans la liste déroulante à droite, puis **mettre à jour**.

    ![Mettre à jour un package](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Pour certains packages, les **mise à jour** bouton est désactivé et un message s’affiche indiquant qu’il est « implicitement référencé par un SDK » (ou « AutoReferenced »). Ce message indique que le package fait partie d’un framework plus grand ou le Kit de développement logiciel et ne doit-elle pas être mis à jour indépendamment. (Ces packages sont signalés en interne par `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Par exemple, `Microsoft.NETCore.App` fait partie du SDK .NET Core, et la version du package n’est pas identique à la version de l’infrastructure du runtime utilisée par l’application. Vous devez [mettre à jour votre installation de .NET Core](https://aka.ms/dotnet-download) pour obtenir de nouvelles versions du runtime ASP.NET Core et .NET Core. [Consultez ce document pour plus d’informations sur les métapackages .NET Core et le contrôle de version](/dotnet/core/packages). Cela s’applique aux packages couramment utilisées suivantes :
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Exemple de package la mention implicitement références ou AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Pour mettre à jour plusieurs packages vers leurs versions les plus récentes, sélectionnez-les dans la liste, puis sélectionnez le **mettre à jour** bouton au-dessus de la liste.
1. Vous pouvez également mettre à jour un package individuel à partir de la **installé** onglet. Dans ce cas, les détails pour le package incluent un sélecteur de version (soumis à la **inclure la version préliminaire** option) et un **mise à jour** bouton.

## <a name="managing-packages-for-the-solution"></a>La gestion des packages pour la solution

La gestion des packages pour une solution sont un moyen pratique de travailler avec plusieurs projets simultanément.

1. Sélectionnez le **Outils > Gestionnaire de Package NuGet > Gérer les Packages NuGet pour la Solution...**  menu de commande, ou avec le bouton droit de la solution et sélectionnez **gérer les Packages NuGet...** :

    ![Gérer les packages NuGet pour la solution](media/ManagePackagesSolutionUICommand.png)

1. Lors de la gestion des packages pour la solution, l’interface utilisateur vous permet de sélectionner les projets qui sont affectés par les opérations :

    ![Sélecteur de projet lors de la gestion des packages pour la solution](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Consolider onglet

Les développeurs estiment généralement mauvaise pratique pour utiliser les différentes versions du même package NuGet sur différents projets dans la même solution. Lorsque vous choisissez de gérer les packages pour une solution, le Gestionnaire de Package UI fournit un **consolider** onglet sur lequel vous pouvez facilement voir où les packages avec des numéros de version distincts sont utilisés par différents projets dans la solution :

![Onglet consolider de l’interface utilisateur de gestionnaire de package](media/ConsolidateTab.png)

Dans cet exemple, le projet ClassLibrary1 est à l’aide de EntityFramework 6.2.0, tandis que ConsoleApp1 est à l’aide de EntityFramework 6.1.0. Pour consolider les versions de package, procédez comme suit :

- Sélectionnez les projets à mettre à jour dans la liste des projets.
- Sélectionnez la version à utiliser dans tous ces projets dans le **Version** contrôle, tel qu’Entity Framework 6.2.0.
- Sélectionnez le **installer** bouton.

Le Gestionnaire de Package installe la version du package sélectionné dans tous les projets sélectionnés, après laquelle le package n’apparaît plus dans le **consolider** onglet.

## <a name="package-sources"></a>Sources de package

Pour modifier la source à partir de laquelle Visual Studio obtient les packages, sélectionnez un dans le sélecteur de source :

![Sélecteur de source de package dans l’interface utilisateur du Gestionnaire de package](media/PackageSourceDropDown.png)

Pour gérer les sources de package :

1. Sélectionnez le **paramètres** icône dans le Gestionnaire de Package UI décrites ci-dessous ou utilisez le **Outils > Options** de commandes et accédez à **Gestionnaire de Package NuGet**:

    ![Icône des paramètres de l’interface utilisateur package manager](media/PackageSourceSettings.png)

1. Sélectionnez le **Sources de Package** nœud :

    ![Options de Sources de package](media/options.png)

1. Pour ajouter une source, sélectionnez **+**, modifiez le nom, entrez l’URL ou le chemin d’accès dans le **Source** contrôler, puis sélectionnez **mise à jour**. La source apparaît maintenant dans le sélecteur de liste déroulante.
1. Pour modifier une source de package, sélectionnez-le, apporter des modifications dans le **nom** et **Source** cases, puis sélectionnez **mise à jour**.
1. Pour désactiver une source de package, désactivez la case à gauche du nom dans la liste.
1. Pour supprimer une source de package, sélectionnez-le, puis le **X** bouton.
1. Utilisez le haut et flèche bas pour modifier l’ordre de priorité des sources de package. Visual Studio recherche ces sources dans l’ordre de priorité lors de la restauration des packages pour un projet. Pour plus d’informations, consultez [restauration des packages](../consume-packages/package-restore.md).

> [!Tip]
> Si une source de package s’affiche de nouveau après l’avoir supprimée, devrait être répertoriée dans au niveau de l’ordinateur ou le niveau de l’utilisateur `NuGet.Config` fichiers. Consultez [du comportement de NuGet configuration](../consume-packages/configuring-nuget-behavior.md) pour l’emplacement de ces fichiers, puis supprimer la source en modifiant les fichiers manuellement ou en utilisant le [nuget sources commande](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Contrôlent les Options du Gestionnaire de package

Lorsqu’un package est sélectionné, le Gestionnaire de Package UI affiche un petit, extensible **Options** contrôle sous le sélecteur de version (illustré ici à la fois réduit et développé). Notez que, pour un projet, les types, uniquement le **afficher la fenêtre d’aperçu** option est fournie.

![Options du Gestionnaire de package](media/PackageManagerUIOptions.png)

Les sections suivantes décrivent ces options.

### <a name="show-preview-window"></a>Afficher la fenêtre d’aperçu

Sélectionné, une fenêtre modale affiche ce qui les dépendances d’un package choisi avant que le package est installé :

![Boîte de dialogue Aperçu exemple](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Installer et mettre à jour des Options

(Non disponible pour tous les types de projet).

**Comportement de dépendance** configure la façon dont NuGet décide quelles versions des packages dépendants à installer :

- *Ignorer les dépendances* ignore l’installation de toutes les dépendances, ce qui interrompt généralement le package en cours d’installation.
- *La plus basse* [Default] installe la dépendance avec le numéro de version minimal qui répond aux exigences du package principal choisi.
- *Correctif logiciel le plus élevé* installe la version avec les mêmes numéros de version principale et secondaire, mais le plus grand nombre de correctifs. Par exemple, si version 1.2.2 est spécifiée, la version la plus élevée qui commence par 1.2 sera être installée
- *Mineur le plus élevé* installe la version avec le même numéro de version principale, mais le numéro mineur le plus élevé et le numéro du correctif. Si la version 1.2.2 est spécifiée, la version la plus élevée qui commence par 1 sera installée
- *La plus élevée* installe la version disponible la plus récente du package.

**Action de conflit de fichiers** spécifie la façon dont NuGet doit gérer les packages qui existent déjà dans le projet ou l’ordinateur local :

- *Invite* indique à NuGet demander s’il faut conserver ou remplacer les packages existants.
- *Ignorer tout* indique à NuGet à ignorer le remplacement des packages existants.
- *Remplacer tous les* indique à remplacer tous les packages NuGet.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Options de désinstallation

(Non disponible pour tous les types de projet).

**Supprimer les dépendances**: lorsque sélectionnée, supprime tous les packages dépendants si elles ne sont pas référencées ailleurs dans le projet.

**Forcer la désinstallation même s’il existe des dépendances sur ce dernier**: lorsque sélectionnée, désinstalle un package même s’il est toujours référencé dans le projet. Cela est généralement utilisé en association avec **supprimer les dépendances** pour supprimer un package et ce que les dépendances qu’il est installé. À l’aide de cette option peut, toutefois, entraîner des références rompues dans le projet. Dans ce cas, vous devrez peut-être [réinstaller ces autres packages](../consume-packages/reinstalling-and-updating-packages.md).
