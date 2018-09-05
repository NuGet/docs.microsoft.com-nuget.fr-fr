---
title: Guide de la Console Gestionnaire de Package NuGet
description: Instructions sur l’utilisation de la Console du Gestionnaire de Package NuGet dans Visual Studio pour travailler avec des packages.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 88979c67ea7f073f2ea5a02c445186642f77f210
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546876"
---
# <a name="package-manager-console"></a>Console du Gestionnaire de package

La Console du Gestionnaire de packages NuGet est intégrée à Visual Studio sur Windows 2012 et versions ultérieures. (Il n’est pas inclus dans Visual Studio pour Mac ou Visual Studio Code.)

La console vous permet d’utiliser les [commandes NuGet dans PowerShell](../tools/powershell-reference.md) pour rechercher, installer, désinstaller et mettre à jour les packages NuGet. L’utilisation de la console est nécessaire dans les cas où le Gestionnaire de packages UI ne fournit pas d’une façon d’effectuer une opération. Pour utiliser les commandes `nuget.exe` dans la console, consultez [à l’aide de l’interface CLI de nuget.exe dans la console](#using-the-nugetexe-cli-in-the-console).

Par exemple, la recherche et l’installation d’un package s’effectue en trois étapes simples :

1. Ouvrez le projet ou la solution dans Visual Studio, puis ouvrez la console à l’aide de la **Outils > Gestionnaire de Package NuGet > Console du Gestionnaire de Package** commande.

1. Recherchez le package que vous souhaitez installer. Si vous connaissez déjà cela, passez à l’étape 3.

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
> Toutes les opérations qui sont disponibles dans la console peuvent également être effectuées avec la [NuGet CLI](../tools/nuget-exe-cli-reference.md). Toutefois, les commandes de la console fonctionnent dans le contexte de Visual Studio et une projet/solution enregistrée et souvent accomplir plus de leurs commandes CLI équivalentes. Par exemple, installation d’un package via la console ajoute une référence au projet n’est pas le cas de la commande CLI. Pour cette raison, les développeurs qui travaillent dans Visual Studio en général, préfèrent à l’aide de la console à l’interface CLI.

> [!Tip]
> De nombreuses opérations de console dépendent de disposer d’une solution ouverte dans Visual Studio avec un nom de chemin d’accès connus. Si vous avez une solution non enregistrée, ou aucune solution, vous pouvez voir l’erreur, « Solution est pas ouvert ou non enregistrée. Vérifiez que vous disposez d’une solution ouverte et enregistrée. » Cela indique que la console ne peut pas déterminer le dossier de solution. L’enregistrement d’une solution non enregistrée, ou en créant et en enregistrant une solution si vous n’en avez pas ouvert, devrait corriger l’erreur.

## <a name="opening-the-console-and-console-controls"></a>Utiliser la console et les contrôles de la console

1. Ouvrez la console dans Visual Studio en utilisant la commande **Outils > Gestionnaire de Package NuGet > Package Manager Console**. La console est une fenêtre de Visual Studio qui peut être organisée et positionnée comme vous le souhaitez (voir [Personnaliser des dispositions de fenêtres dans Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Par défaut, les commandes de la console fonctionnent par rapport à un projet et la source du package spécifique tel que défini dans le contrôle en haut de la fenêtre :

    ![Contrôles de la Console du Gestionnaire de package pour le projet et de la source du package](media/PackageManagerConsoleControls1.png)

1. La sélection d’une source de package et/ou d’un projet différent(e) modifie les valeurs par défaut pour les commandes suivantes. Pour remplacer ces paramètres sans modifier les valeurs par défaut, la plupart des commandes prend en charge les options `-Source` et `-ProjectName`.

1. Pour gérer les sources de package, sélectionnez l’icône d’engrenage. Il s’agit d’un raccourci vers la boîte de dialogue **Outils > Options > Gestionnaire de Package NuGet > Sources de Package**, comme décrit dans la page [Package Manager UI](package-manager-ui.md#package-sources). En outre, le contrôle situé à droite du sélecteur de projet efface contenu de la console :

    ![Paramètres de la Console du Gestionnaire de package et effacer les contrôles](media/PackageManagerConsoleControls2.png)

1. Le bouton plus à droite interrompt une commande longue. Par exemple, utilisez la commande `Get-Package -ListAvailable -PageSize 500` qui vous permet de répertorier les 500 premiers packages sur la source par défaut (par exemple nuget.org). Celle-ci peut prendre plusieurs minutes pour s’exécuter.

    ![Contrôle d’arrêt de Console du Gestionnaire de package](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Installer un package

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Voir aussi [Install-Package](../tools/ps-ref-install-package.md).

Installation d’un package dans la console effectue les mêmes étapes comme décrit sur [que se passe-t-il lorsqu’un package est installé](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), avec les ajouts suivants :

- La Console affiche les termes du contrat de licence applicable dans sa fenêtre avec un contrat implicite. Si vous n’acceptez pas les termes du contrat, vous devez désinstaller le package immédiatement.
- Également une référence au package est ajoutée au fichier projet et apparaît dans **l’Explorateur de solutions** sous le **références** nœud, vous devez enregistrer le projet pour voir les modifications dans le fichier projet directement.

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

La désinstallation d’un package effectue les actions suivantes :

- Supprime la référence au package dans le projet (et le format de gestion est en cours d’utilisation). Références n’apparaissent plus dans **l’Explorateur de solutions**. (Vous devrez peut-être régénérer le projet pour voir s’il est supprimé du dossier **Bin**.)
- Annule les modifications apportées à `app.config` ou `web.config` lorsque le package a été installé.
- Supprime les dépendances précédemment installées si aucun paquet restant n'utilise ces dépendances.

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

En outre, si vous n'avez pas le Gestionnaire de package NuGet dans Visual Studio 2015 et versions antérieures, vérifiez **Outils > Extensions et mises à jour...** et recherchez l’extension du Gestionnaire de package NuGet. Si vous ne parvenez pas à utiliser le programme d’installation des extensions dans Visual Studio, vous pouvez télécharger l’extension directement à partir de [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

La Console du Gestionnaire de Package n’est pas actuellement disponible avec Visual Studio pour Mac. Toutefois, les commandes équivalentes, sont disponibles via le [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio pour Mac a une interface utilisateur pour la gestion des packages NuGet. Consultez [, y compris un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).

La Console du Gestionnaire de Package n’est pas incluse avec Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Etendre la Console du Gestionnaire de package

Certains packages installent les nouvelles commandes de la console. Par exemple, `MvcScaffolding` crée des commandes telles que `Scaffold` illustré ci-dessous, qui génère les contrôleurs MVC ASP.NET et des vues :

![Installation et l’utilisation de MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Configurer un profil de NuGet PowerShell

Un profil PowerShell vous permet de rendre les commandes couramment utilisées disponibles partout où vous utilisez PowerShell.  NuGet prend en charge un profil NuGet spécifique qui se trouve généralement à l’emplacement suivant :

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Pour trouver le profil, tapez `$profile` dans la console :

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Pour plus d’informations, reportez-vous à [Windows PowerShell profils](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Utiliser l’interface CLI de nuget.exe dans la console

Pour rendre [ CLI`nuget.exe`](nuget-exe-cli-reference.md) disponible dans la Console du Gestionnaire de package, installez le package [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) à partir de la console :

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
