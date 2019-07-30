---
title: Installer et gérer des packages NuGet à l’aide de la console Visual Studio
description: Instructions pour l’utilisation de la console du gestionnaire de package NuGet dans Visual Studio pour travailler avec des packages.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 1fb12c6cb9f7702c05990f79a6d43b9dd739e8cc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328066"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Installer et gérer des packages avec la console du gestionnaire de package dans Visual Studio (PowerShell)

La console du gestionnaire de package NuGet vous permet d’utiliser des [commandes PowerShell NuGet](../reference/powershell-reference.md) pour rechercher, installer, désinstaller et mettre à jour des packages NuGet. L’utilisation de la console est nécessaire dans les cas où l’interface utilisateur du gestionnaire de package n’offre aucun moyen d’effectuer une opération. Pour utiliser les commandes CLI `nuget.exe` dans la console, consultez [Utilisation de l’interface CLI de nuget.exe dans la console](#use-the-nugetexe-cli-in-the-console).

La console est intégrée dans Visual Studio sur Windows. Elle n’est pas incluse dans Visual Studio pour Mac ou dans Visual Studio Code.

## <a name="find-and-install-a-package"></a>Rechercher et installer un package

Par exemple, la recherche et l’installation d’un package s’effectuent en trois étapes simples :

1. Ouvrez le projet/la solution dans Visual Studio, puis ouvrez la console à l’aide de la commande **Outils > Gestionnaire de package NuGet > Console du gestionnaire de package**.

1. Recherchez le package que vous souhaitez installer. Si vous le connaissez déjà ce cas, passez directement à l’étape 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Exécutez la commande d’installation :

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Toutes les opérations qui sont disponibles dans la console peuvent également être effectuées à l’aide de l’[interface CLI NuGet](../reference/nuget-exe-cli-reference.md). Toutefois, les commandes de la console fonctionnent dans le contexte de Visual Studio et d’un projet/d’une solution enregistrés et accomplissent souvent plus que leurs commandes CLI équivalentes. Par exemple, l’installation d’un package via la console ajoute une référence au projet, contrairement à la commande CLI. Pour cette raison, les développeurs qui travaillent dans Visual Studio préfèrent généralement utiliser la console plutôt que l’interface CLI.

> [!Tip]
> De nombreuses opérations de console dépendent d’une solution ouverte dans Visual Studio avec un nom de chemin connu. Si votre solution est enregistrée ou que vous n’avez pas de solution, vous pouvez voir l’erreur « La solution n’est pas ouverte ou n’est pas enregistrée. Vérifiez que vous disposez d’une solution ouverte et enregistrée. » Ceci indique que la console ne peut pas déterminer le dossier de la solution. L’enregistrement d’une solution non enregistrée, ou la création et l’enregistrement d’une solution si vous n’en avez pas une ouverte, devraient corriger l’erreur.

## <a name="opening-the-console-and-console-controls"></a>Ouverture de la console et des contrôles de la console

1. Ouvrez la console dans Visual Studio à l’aide de la commande **Outils > Gestionnaire de package NuGet > Console du gestionnaire de package**. La console est une fenêtre Visual Studio qui peut être organisée et positionnée comme vous le souhaitez (consultez [Personnaliser les dispositions de fenêtres dans Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Par défaut, les commandes de la console fonctionnent sur une source de package et un projet spécifiques définis dans le contrôle en haut de la fenêtre :

    ![Contrôles de la console du gestionnaire de package pour la source et le projet du package](media/PackageManagerConsoleControls1.png)

1. La sélection d’une autre source et/ou d’un autre projet de package modifie ces valeurs par défaut pour les commandes suivantes. Pour écraser ces paramètres sans modifier les valeurs par défaut, la plupart des commandes prennent en charge les options `-Source` et `-ProjectName`.

1. Pour gérer les sources de packages, sélectionnez l’icône d’engrenage. Il s’agit d’un raccourci vers la boîte de dialogue **Outils > Options > Gestionnaire de package NuGet > Sources des packages**, conformément à la description à la page [Interface utilisateur du gestionnaire de package](install-use-packages-visual-studio.md#package-sources). Le contrôle situé à droite du sélecteur de projets efface également le contenu de la console :

    ![Paramètres de la console du gestionnaire de package et contrôles d’effacement](media/PackageManagerConsoleControls2.png)

1. Le bouton tout à droite interrompt une commande dont l’exécution dure longtemps. Par exemple, l'exécution de listes `Get-Package -ListAvailable -PageSize 500` répertorie les 500 premiers packages sur la source par défaut (par exemple, nuget.org), ce qui peut prendre plusieurs minutes.

    ![Contrôle d’arrêt de la console du gestionnaire de package](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Installer un package

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Consultez [Install-Package](../reference/ps-reference/ps-ref-install-package.md).

L’installation d’un package dans la console effectue les mêmes étapes que celles décrites dans [Processus d’installation d’un package](../concepts/package-installation-process.md), plus ce qui suit :

- La console affiche les termes du contrat de licence applicables dans sa fenêtre et l’accord implicite. Si vous n’acceptez pas les termes du contrat, vous devez désinstaller immédiatement le package.
- Une référence au package est également ajoutée au fichier projet et s’affiche dans l’**Explorateur de solutions** sous le nœud **Références**. Vous devez enregistrer le projet pour voir les modifications directement dans le fichier projet.

## <a name="uninstall-a-package"></a>Désinstaller un package

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Consultez [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md). Utilisez l’option [Get-Package](../reference/ps-reference/ps-ref-get-package.md) pour afficher tous les packages actuellement installés dans le projet par défaut si vous avez besoin de rechercher un identificateur.

La désinstallation d’un package effectue les actions suivantes :

- Supprime les références au package provenant du projet (quel que soit le format de gestion utilisé). Les références ne s’affichent plus dans l’**Explorateur de solutions**. (Vous devrez peut-être régénérer le projet pour le supprimer du dossier **Bin**.)
- Annule toutes les modifications apportées à `app.config` ou à `web.config` lors de l’installation du package.
- Supprime les dépendances précédemment installées si aucun package restant ne les utilise.

## <a name="update-a-package"></a>Mettre à jour un package

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

Consultez [Get-Package](../reference/ps-reference/ps-ref-get-package.md) et [Update-Package](../reference/ps-reference/ps-ref-update-package.md)

## <a name="find-a-package"></a>Rechercher un package

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

Consultez [Find-Package](../reference/ps-reference/ps-ref-find-package.md). Dans Visual Studio 2013 et les versions antérieures, utilisez [Get-Package](../reference/ps-reference/ps-ref-get-package.md) à la place.

## <a name="availability-of-the-console"></a>Disponibilité de la console

À compter de Visual Studio 2017, NuGet et le gestionnaire de package NuGet sont automatiquement installés lorsque vous sélectionnez des charges de travail liées à .NET. Vous pouvez également les installer individuellement en cochant la case de l’option **Composants individuels > Outils de code > Gestionnaire de package NuGet** dans le programme d’installation de Visual Studio.

Donc, si vous n’avez pas le gestionnaire de package NuGet dans Visual Studio 2015 et les versions antérieures, consultez **Outils > Extensions et mises à jour...** et recherchez l’extension pour le gestionnaire de package NuGet. Si vous ne pouvez pas utiliser le programme d’installation des extensions dans Visual Studio, vous pouvez télécharger l'extension directement à partir de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

La console du gestionnaire de package n’est actuellement pas disponible avec Visual Studio pour Mac. Toutefois, les commandes équivalentes sont disponibles par le biais de l’interface [CLI NuGet](../reference/nuget-exe-CLI-reference.md). Visual Studio pour Mac dispose d’une interface utilisateur pour la gestion des packages NuGet. Consultez [Inclusion d’un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).

La console du gestionnaire de package n’est pas incluse dans Visual Studio Code.

## <a name="extend-the-package-manager-console"></a>Étendre la console du gestionnaire de package

Certains packages installent de nouvelles commandes pour la console. Par exemple, `MvcScaffolding` crée des commandes telles que `Scaffold`, indiquée ci-dessous, qui génère des vues et des contrôleurs MVC ASP.NET :

![Installation et utilisation de MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Configurer un profil PowerShell NuGet

Un profil PowerShell vous permet de mettre à disposition des commandes couramment utilisées partout où vous utilisez PowerShell. NuGet prend en charge un profil qui lui est spécifique et se trouve généralement à l’emplacement suivant :

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Pour rechercher le profil, tapez `$profile` dans la console :

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Pour plus d’informations, consultez [Profils Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="use-the-nugetexe-cli-in-the-console"></a>Utiliser l’interface CLI nuget.exe dans la console

Pour rendre l’interface [`nuget.exe`CLI](../reference/nuget-exe-cli-reference.md) disponible dans la console du gestionnaire de package, installez le package [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) à partir de la console :

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
