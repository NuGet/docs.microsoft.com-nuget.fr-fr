---
title: Installer et gérer des packages NuGet dans Visual Studio
description: Instructions pour l’utilisation de l’interface utilisateur du gestionnaire de package NuGet dans Visual Studio pour travailler avec des packages NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428694"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Installer et gérer des packages dans Visual Studio à l’aide du gestionnaire de package NuGet

L’interface utilisateur du gestionnaire de package NuGet dans Visual Studio facilite l’installation, la désinstallation et la mise à jour des packages NuGet dans les projets et solutions. Pour en faire l’expérience dans Visual Studio pour Mac, consultez [Inclusion d’un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json). L’interface utilisateur du gestionnaire de package n’est pas incluse dans Visual Studio Code.

> [!NOTE]
> Si vous n’avez pas le gestionnaire de package NuGet dans Visual Studio 2015, consultez **Outils > Extensions et mises à jour...** et recherchez l’extension *Gestionnaire de package NuGet*. Si vous n’êtes pas en mesure d’utiliser l’installateur d’extensions dans Visual Studio, téléchargez l’extension directement à partir de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
>
> À compter de Visual Studio 2017, NuGet et le gestionnaire de package NuGet sont automatiquement installés avec toutes les charges de travail liées à .NET. Installez-les individuellement en sélectionnant l’option **Composants individuels > Outils de code > gestionnaire de package NuGet** dans le programme d’installation de Visual Studio.

## <a name="find-and-install-a-package"></a>Rechercher et installer un package

1. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **Références** ou sur un projet, puis sélectionnez **Gérer les packages NuGet...**.

    ![Option de menu Gérer les packages NuGet](media/ManagePackagesUICommand.png)

1. L'onglet **Parcourir** affiche les packages par popularité à partir de la source actuellement sélectionnée (consultez [Sources de packages](#package-sources)). Recherchez un package spécifique à l’aide de la zone de recherche en haut à gauche. Sélectionnez un package dans la liste pour afficher ses informations, ce qui active également le bouton **Installer** avec une liste déroulante de sélection de version.

    ![Onglet Parcourir la boîte de dialogue Gérer les packages NuGet](media/Search.png)

1. Sélectionnez la version souhaitée dans la liste déroulante, puis sélectionnez **Installer**. Visual Studio installe le package et ses dépendances dans le projet. Vous pouvez être invité à accepter les termes du contrat de licence. Lorsque l’installation est terminée, les paquets ajoutés apparaissent sur **l’onglet Installed.** Les paquets sont également `using` répertoriés dans le nœud de **référence** de Solution Explorer, indiquant que vous pouvez vous référer à eux dans le projet avec des déclarations.

    ![Références dans l’Explorateur de solutions](media/References.png)

> [!Tip]
> Pour inclure des versions préliminaires dans la recherche et rendre les versions préliminaires disponibles dans la liste déroulante des versions, sélectionnez l’option **Inclure la version préliminaire**.

> [!Note]
> NuGet a deux formats dans lesquels [`PackageReference`](package-references-in-project-files.md) [`packages.config`](../reference/packages-config.md)un projet peut utiliser des paquets: et . [La valeur par défaut peut être définie dans la fenêtre d’options de Visual Studio](Package-Restore.md#choose-default-package-management-format).

## <a name="uninstall-a-package"></a>Désinstaller un package

1. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **Références** ou sur le projet souhaité, puis sélectionnez **Gérer les packages NuGet...**.
1. Sélectionnez l’onglet **Installé**.
1. Sélectionnez le package à désinstaller (à l’aide de la recherche pour filtrer la liste si nécessaire) et sélectionnez **Désinstaller**.

    ![Désinstallation d’un package](media/UninstallPackage.png)

1. Notez que les contrôles **Inclure la version préliminaire** et **Code source du package** n’ont aucun effet lors de la désinstallation des packages.

## <a name="update-a-package"></a>Mettre à jour un package

1. Dans **Solution Explorer**, cliquez à droite soit **Références** ou le projet souhaité, et sélectionnez **Manage NuGet Packages...**. (Dans les projets de site Web, cliquez à droite sur le dossier **Bin.)**
1. Sélectionnez l'onglet **Mises à jour** pour afficher les packages pour lesquels des mises à jour sont disponibles à partir des sources de package sélectionnées. Sélectionnez **Inclure la version préliminaire** pour inclure les packages en version préliminaire dans la liste des mises à jour.
1. Sélectionnez le package à mettre à jour, la version souhaitée dans la liste déroulante à droite, puis **Mettre à jour**.

    ![Mise à jour d'un package](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Pour certains packages, le bouton **Mise à jour** est désactivé et un message s’affiche, indiquant qu’il est « implicitement référencé par un kit de développement logiciel (SDK) » (ou « AutoReferenced »). Ce message indique que le package fait partie d’une infrastructure ou d’un kit de développement logiciel (SDK) plus volumineux et ne doit pas être mis à jour de manière indépendante. (Ces paquets sont `<IsImplicitlyDefined>True</IsImplicitlyDefined>`marqués en interne avec .) Par exemple, `Microsoft.NETCore.App` fait partie du SDK core .NET, et la version paquet n’est pas la même que la version du cadre de temps d’exécution utilisé par l’application. Vous devez [mettre à jour votre installation de .NET Core](https://aka.ms/dotnet-download) pour bénéficier de nouvelles versions d’ASP.NET Core et de Runtime .NET Core. [Pour plus d’informations sur les métapaquets et le contrôle de version de .NET Core, consultez ce document](/dotnet/core/packages). Cela s’applique aux packages couramment utilisés suivants :
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Exemple de package marqué comme Implicitement référencé ou AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Pour mettre à jour plusieurs packages vers leurs versions les plus récentes, sélectionnez-les dans la liste, puis sélectionnez le bouton **Mettre à jour** au-dessus de la liste.
1. Vous pouvez également mettre à jour un paquet individuel à partir de l’onglet **Installed.** Dans ce cas, les détails du paquet comprennent un sélecteur de version (sous réserve de **l’option Prérelease Inclus)** et un bouton **de mise à jour.**

## <a name="manage-packages-for-the-solution"></a>Gérer des packages pour la solution

La gestion des packages pour une solution est un moyen pratique de travailler simultanément sur plusieurs projets.

1. Sélectionnez la commande de menu **Outils > Gérer les packages NuGet pour la solution...**, ou cliquez avec le bouton droit sur la solution dans l’Explorateur de solutions et sélectionnez **Gérer les packages NuGet...**  :

    ![Gérer les packages NuGet pour la solution](media/ManagePackagesSolutionUICommand.png)

1. Lorsque vous gérez des packages pour la solution, l’interface utilisateur vous permet de sélectionner les projets affectés par les opérations :

    ![Sélecteur de projet lors de la gestion de packages pour la solution](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Onglet Consolider

Les développeurs considèrent généralement qu’il est déconseillé d’utiliser différentes versions du même package NuGet dans différents projets de la même solution. Lorsque vous choisissez de gérer des packages pour une solution, l’interface utilisateur du gestionnaire de package fournit un onglet **Consolider** sur lequel vous pouvez facilement voir où des packages avec des numéros de version distincts sont utilisés par différents projets dans la solution :

![Onglet Consolider de l’interface utilisateur du gestionnaire de package](media/ConsolidateTab.png)

Dans cet exemple, le projet ClassLibrary1 utilise EntityFramework 6.2.0, tandis que ConsoleApp1 utilise EntityFramework 6.1.0. Pour consolider les versions de package, procédez comme suit :

- Sélectionnez les projets à mettre à jour dans la liste des projets.
- Sélectionnez la version à utiliser dans tous ces projets dans la commande **Version**, par exemple, EntityFramework 6.2.0.
- Sélectionnez le bouton **Installer**.

Le gestionnaire de package installe la version de package sélectionnée dans tous les projets sélectionnés, après quoi le package ne s'affiche plus sous l’onglet **Consolider**.

## <a name="package-sources"></a>Sources de packages

Pour modifier la source à partir de laquelle Visual Studio obtient les packages, sélectionnez-en un dans le sélecteur de source :

![Sélecteur de source de package dans l’interface utilisateur du gestionnaire de package](media/PackageSourceDropDown.png)

Pour gérer les sources de packages :

1. Sélectionnez l’icône **Paramètres** dans l’interface utilisateur du gestionnaire de package présentée ci-dessous, ou utilisez la commande **Outils > Options** et faites défiler jusqu’au **Gestionnaire de package NuGet** :

    ![Icône des paramètres de l’interface utilisateur du gestionnaire de package](media/PackageSourceSettings.png)

1. Sélectionnez le nœud **Sources du package** :

    ![Options des sources de packages](media/options.png)

1. Pour ajouter une **+** source, sélectionnez, modifiez le nom, entrez l’URL ou le chemin dans le contrôle **Source,** et **sélectionnez Mise à jour**. La source apparaît maintenant dans la liste déroulante du sélecteur.
1. Pour modifier une source de package, sélectionnez-la, apportez des modifications aux zones **Nom** et **Source**, puis sélectionnez **Mettre à jour**.
1. Pour désactiver une source de package, décochez la case située à gauche de son nom dans la liste.
1. Pour supprimer une source de package, sélectionnez-la, puis sélectionnez le bouton **X**.
1. L’utilisation des flèches haut et bas ne change pas l’ordre de priorité des sources de packages. Visual Studio ignore l’ordre des sources de packages et utilise le package provenant de la première source à répondre aux requêtes. Pour plus d'informations, consultez [Restauration du package](../consume-packages/package-restore.md).

> [!Tip]
> Si une source de package réapparaît après avoir été supprimée, c’est qu’elle est peut-être répertoriée dans des fichiers `NuGet.Config` au niveau de l’ordinateur ou de l’utilisateur. Consultez [Configurations NuGet courantes](../consume-packages/configuring-nuget-behavior.md) pour localiser ces fichiers, puis supprimez la source en modifiant les fichiers, manuellement ou à l’aide de la [commande Sources nuget](../reference/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Contrôle des options du gestionnaire de package

Lorsqu’un package est sélectionné, l’interface utilisateur du gestionnaire de package affiche un contrôle **Options** de petite taille extensible sous le sélecteur de version (réduit et développé sur l’illustration). Notez que, pour certains types de projets, seule l’option **Afficher la fenêtre d’aperçu** est disponible.

![Options du gestionnaire de package](media/PackageManagerUIOptions.png)

Les sections ci-dessous expliquent ces options.

### <a name="show-preview-window"></a>Afficher la fenêtre d'aperçu

Lorsque cette option est sélectionnée, une fenêtre modale affiche les dépendances d’un package choisi avant de l’installer :

![Exemple de boîte de dialogue d’aperçu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Installer et mettre à jour les options

(Pas disponible pour tous les types de projets.)

**Comportement de dépendance** configure la façon dont NuGet choisit les versions des packages dépendants à installer :

- *Ignorer les dépendances* ignore l’installation de toutes les dépendances, ce qui stoppe généralement l’installation du package.
- *Le plus bas* [par défaut] installe la dépendance avec le numéro de version minimal qui répond aux exigences du package principal choisi.
- *Correctif le plus élevé* installe la version avec les mêmes numéros de version majeur et mineur, mais le numéro de correctif le plus élevé. Par exemple, si la version 1.2.2 est spécifiée, la version la plus élevée commençant par 1.2 est installée.
- *Mineur le plus élevé* installe la version avec le même numéro de version majeur, mais les numéros mineur et de correctif les plus élevés. Si la version 1.2.2 est spécifiée, la version la plus élevée commençant par 1 est installée.
- *Le plus élevé* installe la version disponible la plus élevée du package.

**Action de conflit de fichiers** spécifie comment NuGet doit gérer les packages qui existent déjà dans le projet ou l’ordinateur local :

- *L' invite* demande à NuGet de demander s’il faut conserver ou remplacer les packages existants.
- *Ignorer tout* indique à NuGet de ne pas remplacer les packages existants.
- *Remplacer tout* indique à NuGet de remplacer les packages existants.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Désinstaller les options

(Pas disponible pour tous les types de projets.)

**Supprimer les dépendances** : lorsque cette option est sélectionnée, les packages dépendants sont supprimés s’ils ne sont pas référencés ailleurs dans le projet.

**Forcer la désinstallation même s’il y a des dépendances sur celle-ci** : lorsque cette option est sélectionnée, un package est désinstallé même s’il est toujours référencé dans le projet. Cette option est généralement utilisée en liaison avec **Supprimer les dépendances** pour supprimer un package et les dépendances qu’il a installées. Toutefois, l’utilisation de cette option peut entraîner des références rompues dans le projet. Dans ce cas, vous devrez peut-être [réinstaller ces autres packages](../consume-packages/reinstalling-and-updating-packages.md).
