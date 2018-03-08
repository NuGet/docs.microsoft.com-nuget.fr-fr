---
title: Guide de la Console Gestionnaire de Package NuGet | Documents Microsoft
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.nuget.packagemanager.console
description: "Instructions pour à l’aide de la Console du Gestionnaire de Package NuGet dans Visual Studio pour l’utilisation de packages."
keywords: "Console de gestionnaire de package NuGet, powershell NuGet, gérer des packages NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 60c7edd0497e162cc511424e9acfbbfd6f53fd46
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2018
---
# <a name="package-manager-console"></a>Console du Gestionnaire de package

La Console du Gestionnaire de packages NuGet est intégrée à Visual Studio sur Windows 2012 et versions ultérieures. (Il n’est pas inclus dans Visual Studio pour Mac ou Visual Studio Code.)

La console vous permet d’utiliser les [commandes NuGet dans PowerShell](../tools/powershell-reference.md) pour rechercher, installer, désinstaller et mettre à jour les packages NuGet. L’utilisation de la console est nécessaire dans les cas où le Gestionnaire de packages UI ne fournit pas d’une façon d’effectuer une opération. Pour utiliser les commandes `nuget.exe` dans la console, consultez [à l’aide de l’interface CLI de nuget.exe dans la console](#using-the-nugetexe-cli-in-the-console).

Par exemple, rechercher et installer un package s’effectue en trois étapes simples :

1. Ouvrez le projet ou la solution dans Visual Studio, puis ouvrez la console à l’aide de la **Outils > Gestionnaire de Package NuGet > Package Manager Console** commande.

2. Recherchez le package que vous souhaitez installer. Si vous connaissez déjà cela, passez à l’étape 3.

    ```ps
    # Find packages containing the keyword "elmah" 
    Find-Package elmah
    ```

3. Exécutez la commande d’installation :

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Toutes les opérations qui sont disponibles dans la console peuvent également être effectuées avec la [NuGet CLI](../tools/nuget-exe-cli-reference.md). Toutefois, les commandes de la console fonctionnent dans le contexte de Visual Studio et un(e) projet/solution enregistrée et souvent accomplir plus de leurs commandes CLI équivalentes. Par exemple, l’installation d’un package via la console ajoute une référence au projet n’est pas le cas de la commande CLI. Pour cette raison, les développeurs qui travaillent dans Visual Studio en général, préfèrent à l’aide de la console pour l’interface CLI.

> [!Tip]
> Nombre d’opérations console dépendent de disposer d’une solution ouverte dans Visual Studio avec un nom de chemin d’accès connu. Si vous avez une solution non enregistrée, ou aucune solution, vous pouvez voir l’erreur, « La solution n'est pas ouvert ou non enregistrée. Vérifiez que vous avez une solution ouverte et enregistrée. » Cela indique que la console ne peut pas déterminer le dossier de solution. L’enregistrement de la solution non enregistrée, ou en créant et en enregistrant la solution si vous n’en avez pas ouvert, devrait corriger l’erreur.

## <a name="opening-the-console-and-console-controls"></a>Utiliser la console et les contrôles de la console

1. Ouvrez la console dans Visual Studio en utilisant la commande **Outils > Gestionnaire de Package NuGet > Package Manager Console**. La console est une fenêtre de Visual Studio qui peut être organisée et positionnée comme vous le souhaitez (voir [Personnaliser des dispositions de fenêtres dans Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

2. Par défaut, les commandes de la console fonctionnent par rapport à un projet et la source du package spécifique défini dans le contrôle en haut de la fenêtre :

    ![Contrôles de la Console du Gestionnaire de package pour le projet et de la source du package](media/PackageManagerConsoleControls1.png)

3. La sélection d’une source de package et/ou d’un projet différent(e) modifie les valeurs par défaut pour les commandes suivantes. Pour remplacer ces paramètres sans modifier les valeurs par défaut, la plupart des commandes prend en charge les options `-Source` et `-ProjectName`.

1. Pour gérer les sources de package, sélectionnez l’icône d’engrenage. Il s’agit d’un raccourci vers le **Outils > Options > Gestionnaire de Package NuGet > Sources de Package** boîte de dialogue, comme décrit dans la [Package Manager UI](package-manager-ui.md#package-sources) page. En outre, le contrôle situé à droite du sélecteur de projet efface contenu de la console :

    ![Paramètres de la Console du Gestionnaire de package et effacer les contrôles](media/PackageManagerConsoleControls2.png)

5. Le bouton plus à droite interrompt une commande longue. Par exemple, utilisez la commande `Get-Package -ListAvailable -PageSize 500` qui vous permet de répertorier les 500 premiers packages sur la source par défaut (par exemple nuget.org). Celle-ci peut prendre plusieurs minutes pour s’exécuter.

    ![Contrôle d’arrêt de Console du Gestionnaire de package](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Installer un package

```ps
# Add the Elmah package to the default project as specified in the console's project selector

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Consultez [Install-Package](../tools/ps-ref-install-package.md).

L'installation d’un package effectue les actions suivantes :

- Affiche les termes du contrat de licence applicable dans la fenêtre de console avec accord implicite. Si vous n’acceptez pas les termes du contrat, vous devez désinstaller le package immédiatement.
- Ajoute une référence au projet dans le format de référence utilisé. Les références apparaissent par la suite dans l’Explorateur de solutions et le fichier de format de référence applicable. Notez, toutefois, qu'avec PackageReference, vous devez enregistrer le projet pour voir les modifications dans le fichier projet directement.
- Met en cache le package :
  - PackageReference : package est mis en cache dans `%USERPROFILE%\.nuget\packages` et le verrouillage de fichier par exemple, `project.assets.json` est mis à jour.
  - `packages.config`: crée un dossier `packages` à la racine de la solution et copie les fichiers de package dans un sous-dossier. Le fichier `package.config` est mis à jour.
- Les mises à jour `app.config` et/ou `web.config` si le package utilise [source et configuration des transformations de fichiers](../create-packages/source-and-config-file-transformations.md).
- Installe toutes les dépendances, si elles ne sont pas déjà présentes dans le projet. Cela pourrait mettre à jour les versions de package dans le processus, comme décrit dans [résolution de dépendance](../consume-packages/dependency-resolution.md).
- Affiche le fichier Lisez-moi du package si elle est disponible, dans une fenêtre de Visual Studio.

> [!Tip]
> Un des principaux avantages de l’installation des packages avec la commande `Install-Package` dans la console est qu'il ajoute une référence au projet comme si vous aviez utilisé le Gestionnaire de Package UI. En revanche, la commande CLI `nuget install` télécharge le package uniquement et n’ajoute pas automatiquement de référence.

## <a name="uninstalling-a-package"></a>Désinstaller un package

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Consultez la section [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Utilisez [Get-Package](../tools/ps-ref-get-package.md) pour voir tous les packages actuellement installés dans le projet par défaut si vous avez besoin rechercher un identificateur.

La désinstallation d’un package effectue les actions suivantes :

- Supprime les références du package associé au projet (et le format de la référence utilisé). Les références n’apparaissent plus dans l’Explorateur de solutions. (Vous devrez peut-être régénérer le projet pour voir s’il est supprimé du dossier **Bin**.)
- Annule les modifications apportées à `app.config` ou `web.config` lorsque le package a été installé.
- Supprime les dépendances précédemment installées si aucun paquet restant n'utilise ces dépendances.

> [!Tip]
> Comme `Install-Package`, la commande `Uninstall-Package` présente l’avantage de la gestion des références dans le projet, contrairement à la commande CLI `nuget uninstall`.

## <a name="updating-a-package"></a>Mettre à jour un package

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

Voir aussi [Obtenir un package](../tools/ps-ref-get-package.md) et [Mettre à jour un package](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Rechercher un package

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

Voir aussi [Find-Package](../tools/ps-ref-find-package.md). Dans Visual Studio 2013 et versions antérieures, utilisez la commande [Get-Package](../tools/ps-ref-get-package.md).

## <a name="availability-of-the-console"></a>Disponibilité de la console

Dans Visual Studio 2017, NuGet et le Gestionnaire de package NuGet sont installés automatiquement lorsque vous sélectionnez n'importe quelle fonctionnalité liée au .NET ; Vous pouvez également l’installer séparément en cochant l'option **Composants individuels > Code Outils > Gestionnaire de package NuGet** dans le programme d’installation de Visual Studio 2017.

En outre, si vous n'avez pas le Gestionnaire de package NuGet dans Visual Studio 2015 et versions antérieures, vérifiez **Outils > Extensions et mises à jour...** et recherchez l’extension du Gestionnaire de package NuGet. Si vous ne parvenez pas à utiliser le programme d’installation des extensions dans Visual Studio, vous pouvez télécharger l’extension directement à partir de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

La Console du Gestionnaire de Package n’est pas actuellement disponible dans Visual Studio pour Mac. Toutefois, les commandes équivalentes, sont disponibles via le [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio pour Mac possède une interface utilisateur pour la gestion des packages NuGet. Consultez [package, y compris un NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).

La Console du Gestionnaire de Package n’est pas incluse avec Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Etendre la Console du Gestionnaire de package

Certains packages installent de nouvelles commandes de la console. Par exemple, `MvcScaffolding` crée des commandes telles que `Scaffold` illustré ci-dessous, qui génère les contrôleurs ASP.NET MVC et les vues :

![Installation et l’utilisation de MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Configurer un profil de NuGet PowerShell

Un profil PowerShell vous permet de rendre les commandes couramment utilisées disponibles partout où vous utilisez PowerShell. NuGet prend en charge un profil NuGet spécifique qui se trouve généralement à l’emplacement suivant :

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Pour trouver le profil, tapez `$profile` dans la console :

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Pour plus d’informations, reportez-vous à [les profils Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Utiliser l’interface CLI de nuget.exe dans la console

Pour rendre le [ `nuget.exe` CLI](nuget-exe-cli-reference.md) disponibles dans la Console du Gestionnaire de Package, installer le [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package à partir de la console :

```ps
# D'autres versions sont disponibles, voir http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
