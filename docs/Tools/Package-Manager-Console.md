---
title: Guide de la Console Gestionnaire de Package NuGet | Documents Microsoft
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords: vs.nuget.packagemanager.console
description: "Instructions pour à l’aide de la Console du Gestionnaire de Package NuGet dans Visual Studio pour l’utilisation de packages."
keywords: "Console de gestionnaire de package NuGet, powershell NuGet, gérer des packages NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b89c51812cee0f64c6f5c39cd9d86bc4a0be068e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="package-manager-console"></a>Console du Gestionnaire de package

La Console du Gestionnaire de packages NuGet est intégrée à Visual Studio sur Windows 2012 et versions ultérieures. (Il n’est pas inclus dans Visual Studio pour Mac ou Visual Studio Code.)

La console vous permet d’utiliser les [commandes NuGet dans PowerShell](../tools/powershell-reference.md) pour rechercher, installer, désinstaller et mettre à jour les packages NuGet. L’utilisation de la console est nécessaire dans les cas où le Gestionnaire de packages UI ne fournit pas d’une façon d’effectuer une opération. Pour utiliser les commandes `nuget.exe` dans la console, consultez [à l’aide de l’interface CLI de nuget.exe dans la console](#using-the-nugetexe-cli-in-the-console).

Par exemple, rechercher et installer un package s’effectue en trois étapes simples :

1. Ouvrez le projet ou la solution dans Visual Studio, puis ouvrez la console à l’aide de la **Outils > Gestionnaire de Package NuGet > Package Manager Console** commande.

2. Recherchez le package que vous souhaitez installer. Si vous connaissez déjà cela, passez à l’étape 3.

    ```ps
    # Cherche des paquets contenant le mot-clé "elmah"
    Find-Package elmah
    ```

3. Exécutez la commande d’installation :

    ```ps
    # Installe le package Elmah sur le projet MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Toutes les opérations qui sont disponibles dans la console peuvent également être effectuées avec la [NuGet CLI](../tools/nuget-exe-cli-reference.md). Toutefois, les commandes de la console fonctionnent dans le contexte de Visual Studio et un(e) projet/solution enregistrée et souvent accomplir plus de leurs commandes CLI équivalentes. Par exemple, l’installation d’un package via la console ajoute une référence au projet n’est pas le cas de la commande CLI. Pour cette raison, les développeurs qui travaillent dans Visual Studio en général, préfèrent à l’aide de la console pour l’interface CLI.

> [!Tip]
> Nombre d’opérations console dépendent de disposer d’une solution ouverte dans Visual Studio avec un nom de chemin d’accès connu. Si vous avez une solution non enregistrée, ou aucune solution, vous pouvez voir l’erreur, « La solution n'est pas ouvert ou non enregistrée. Vérifiez que vous avez une solution ouverte et enregistrée. » Cela indique que la console ne peut pas déterminer le dossier de solution. L’enregistrement de la solution non enregistrée, ou en créant et en enregistrant la solution si vous n’en avez pas ouvert, devrait corriger l’erreur.

## <a name="opening-the-console-and-console-controls"></a>Utiliser la console et les contrôles de la console

1. Pour utiliser la console dans Visual Studio en utilisant le **Outils > Gestionnaire de Package NuGet > Package Manager Console** commande. La console est une fenêtre de Visual Studio qui peut être organisée et positionnée comme vous le souhaitez (voir [personnaliser des dispositions de fenêtres dans Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

2. Par défaut, les commandes de la console fonctionnent par rapport à un projet et la source du package spécifique défini dans le contrôle en haut de la fenêtre :

    ![Contrôles de la Console du Gestionnaire de package pour le projet et de la source du package](media/PackageManagerConsoleControls1.png)

3. Sélectionnez une source de package différent et/ou d’un projet modifie les valeurs par défaut pour les commandes suivantes. Pour  d’ignorer ces paramètres sans modifier les valeurs par défaut, la plupart des commandes prennent en charge `-Source` et `-ProjectName` options.

4. Pour gérer les sources de package, sélectionnez l’icône d’engrenage. Il s’agit d’un raccourci vers le **Outils > Options > Gestionnaire de Package NuGet > Sources de Package** de la boîte de dialogue, comme décrit dans la page [Package Manager UI](Package-Manager-UI.md#package-sources). En outre, le contrôle situé à droite du sélecteur de projet efface contenu de la console :

    ![Paramètres de la Console du Gestionnaire de package et effacer les contrôles](media/PackageManagerConsoleControls2.png)

5. Le bouton plus à droite interrompt une commande longue. Par exemple, utilisez la commande `Get-Package -ListAvailable -PageSize 500` qui vous permet de répertorier les packages top 500 sur la source par défaut (par exemple nuget.org). Celle-ci peut prendre plusieurs minutes pour s’exécuter.

    ![Contrôle d’arrêt de Console du Gestionnaire de package](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Installer un package

```ps
# Ajouter le package Elmah au projet par défaut comme spécifié dans le sélecteur de projet de la console.
Install-Package Elmah

# Ajouter le package Elmah à un projet nommé UtilitiesLib qui n'est pas celui par défaut.
Install-Package Elmah -ProjectName UtilitiesLib
```

Voir aussi [Install-Package](../tools/ps-ref-install-package.md).

L'installation d’un package effectue les actions suivantes :

- Affiche les termes du contrat de licence applicable dans la fenêtre de console avec accord implicite. Si vous n’acceptez pas les termes du contrat, vous devez désinstaller le package immédiatement.
- Ajoute une référence au projet dans le format de la référence est en cours d’utilisation. Les références apparaissent par la suite dans l’Explorateur de solutions et le fichier de format de référence applicable. Notez, toutefois, avec PackageReference, vous devez enregistrer le projet pour voir les modifications dans le fichier projet directement.
- Met en cache le package :
  - PackageReference : le(s) package(s) est/sont mis en cache dans `%USERPROFILE%\.nuget\packages` et le verrouillage de fichier par exemple, `project.assets.json` est mis à jour.
  - `packages.config`: crée un dossier `packages` à la racine de la solution et copie les fichiers de package dans un sous-dossier. Le `package.config` fichier est mis à jour.
- Les mises à jour `app.config` et/ou `web.config` si le package utilise [source et configuration des transformations de fichiers](../create-packages/source-and-config-file-transformations.md).
- Installe toutes les dépendances, si elles ne sont pas déjà présentes dans le projet. Cela pourrait mettre à jour les versions de package dans le processus, comme décrit dans [résolution de dépendance](../consume-packages/dependency-resolution.md).
- Affiche le fichier Lisez-moi du package si elle est disponible, dans une fenêtre de Visual Studio.

> [!Tip]
> Un des principaux avantages de l’installation des packages avec la commade `Install-Package` dans la console est qu'il ajoute une référence au projet comme si vous avez utilisé le Gestionnaire de Package UI. En revanche, la commade CLI `nuget install`  télécharge le package uniquement et n’ajoute pas automatiquement une référence.

## <a name="uninstalling-a-package"></a>Désinstaller un package

```ps
# Désinstalle le paquet Elmah du projet par défaut
Uninstall-Package Elmah

# Désinstalle le paquet Elmah et toutes ses dépendances inutilisées
Uninstall-Package Elmah -RemoveDependencies 

# Désinstalle le paquet Elmah même si un autre paquet en dépend
Uninstall-Package Elmah -Force
```

Consultez la section [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Utilisez [Get-Package](../tools/ps-ref-get-package.md) pour voir tous les packages actuellement installés dans le projet par défaut si vous avez besoin rechercher un identificateur.

La désinstallation d’un package effectue les actions suivantes :

- Supprime les références du package associé au projet (et le format de la référence est en cours d’utilisation). Les références n’apparaissent plus dans l’Explorateur de solutions. (Vous devrez peut-être régénérer le projet pour voir qu’il est supprimé de la **Bin** dossier.)
- Annule les modifications apportées à `app.config` ou `web.config` lorsque le package a été installé.
- Supprime les dépendances précédemment installées si aucun paquet restant n'utilise ces dépendances.

> [!Tip]
> Comme `Install-Package`, la commande `Uninstall-Package` présente l’avantage de la gestion des références dans le projet, contrairement à la commande CLI `nuget uninstall`.

## <a name="updating-a-package"></a>Mettre à jour un package

```ps
# Vérifie si des versions plus récentes sont disponibles pour tous les packages installés
Get-Package -updates

# Met à jour un package spécifique en utilisant son identifiant, dans ce cas jQuery
Update-Package jQuery

# Met à jour tous les packages du projet MyProject (tel qu'il apparaît dans Solution Explorer)
Update-Package -ProjectName MyProject

# Met à jour tous les paquets de la solution
Update-Package
```

Voir aussi [Get-Package](../tools/ps-ref-get-package.md) et [Package de mise à jour](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Rechercher un package

```ps
# Trouver des paquets contenant des mots-clés
Find-Package elmah
Find-Package logging

# Liste les paquets dont l'ID commence par Elmah
Find-Package Elmah -StartWith

# Par défaut, Get-Package renvoie une liste de 20 paquets; utilisez le paramètre -First pour afficher plus de paquets.
Find-Package logging -First 100

# Listez toutes les versions du paquet avec l'ID de "jquery".
Find-Package jquery -AllVersions -ExactMatch
```

Voir aussi [Find-Package](../tools/ps-ref-find-package.md). Dans Visual Studio 2013 et versions antérieures, utilisez la commande [Get-Package](../tools/ps-ref-get-package.md).

## <a name="availability-of-the-console"></a>Disponibilité de la console

Dans Visual Studio 2017, NuGet et le Gestionnaire de Package NuGet sont installés automatiquement lorsque vous sélectionnez n'importe quelle fonctionnalité liée au .NET ; Vous pouvez également l’installer séparément en cochant l'otpion **des composants individuels > Code Outils > Gestionnaire de package NuGet** dans le programme d’installation de Visual Studio 2017.

En outre, si vous n'avez pas le Gestionnaire de Package NuGet dans Visual Studio 2015 et versions antérieures, vérifiez **Outils > Extensions et mises à jour...**  et recherchez l’extension du Gestionnaire de Package NuGet. Si vous ne parvenez pas à utiliser le programme d’installation des extensions dans Visual Studio, vous pouvez télécharger l’extension directement à partir de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

La Console du Gestionnaire de Package n’est pas actuellement disponible dans Visual Studio pour Mac. Toutefois, les commandes équivalentes, sont disponibles via le [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio pour Mac possède une interface utilisateur pour la gestion des packages NuGet. Consultez [package, y compris un NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).

La Console du Gestionnaire de Package n’est pas incluse avec Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Etendre la Console du Gestionnaire de Package

Certains packages installent de nouvelles commandes de la console. Par exemple, `MvcScaffolding` crée des commandes telles que `Scaffold` illustré ci-dessous, qui génère les contrôleurs ASP.NET MVC et les vues :

![Installation et l’utilisation de MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Configurer un profil de NuGet PowerShell

Un profil PowerShell vous permet de rendre les commandes couramment utilisées disponible partout où vous utilisez PowerShell. NuGet prend en charge un profil NuGet spécifique qui se trouve généralement à l’emplacement suivant :

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Pour trouver le profil, tapez `$profile` dans la console :

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Pour plus d’informations, reportez-vous à [les profils Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Utiliser l’interface CLI de nuget.exe dans la console

Pour rendre le [ `nuget.exe` CLI](nuget-exe-CLI-Reference.md) disponibles dans la Console du Gestionnaire de Package, installer le package [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) à partir de la console :

```ps
# D'autres versions sont disponibles, voir http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
