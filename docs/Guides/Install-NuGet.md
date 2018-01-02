---
title: Installation des outils clients NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Conseils sur l’installation des outils clients, de l’interface de ligne de commande (CLI) et du Gestionnaire de package pour Visual Studio."
keywords: CLI NuGet.exe, outils clients NuGet, gestionnaire de package NuGet, console du gestionnaire de package NuGet, NuGet pour Visual Studio, NuGet Beta Channel
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>Installation des outils clients NuGet

> [!Tip]
> **Vous souhaitez installer un package ? Consultez [Démarrage rapide - Utiliser un package](../Quickstart/Use-a-Package.md).**

Il existe deux outils principaux pour créer, publier et consommer des packages NuGet :

1. [**L’interface de ligne de commande NuGet**](#nuget-cli) est l’utilitaire en ligne de commande pour Windows qui fournit toutes les fonctionnalités NuGet ; il peut également être exécuté sur Mac OSX et Linux à l’aide de Mono ou via l’interface de ligne de commande .NET Core (`dotnet`).
1. Le [**Gestionnaire de package NuGet dans Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows uniquement) est un outil GUI pour la gestion des packages et inclut une console PowerShell par le biais de laquelle vous pouvez utiliser certaines commandes NuGet directement dans Visual Studio. La console et l’interface utilisateur du Gestionnaire de package sont inclus dans Visual Studio (sur Windows) versions 2012 et ultérieures et peuvent être installées manuellement pour les versions antérieures.

    Avec Visual Studio pour Mac, les fonctionnalités NuGet sont intégrées directement. Consultez [Inclusion d’un package NuGet dans votre projet](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) pour une procédure pas à pas.

    À l’heure actuelle, Visual Studio Code n’a pas de prise en charge intégrée de NuGet. Utilisez l’interface de ligne de commande NuGet ou [l’interface de ligne de commande dotnet](../Tools/dotnet-Commands.md).

Le Gestionnaire de package et l’interface de ligne de commande NuGet prennent en charge les opérations suivantes :

- Rechercher des packages
- Installer des packages
- Mettre à jour des packages
- Désinstaller des packages
- Restaurer des packages (interface utilisateur uniquement dans le Gestionnaire de package)
- Gérer les sources NuGet

Les fonctionnalités suivantes sont uniquement prises en charge dans l’interface de ligne de commande NuGet :

- Gérer les packages (nuget.org ou flux privé)
- Créer des packages 
- Publier des packages
- Gérer Nuget.Config
- Gérer le cache NuGet
- Répliquer un package

> [!Note]
> Un autre bon outil est [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), outil autonome open source permettant d’explorer, de créer et de modifier des packages NuGet visuellement. Il est très utile, par exemple, pour apporter des modifications expérimentales à une structure de package sans avoir à reconstruire le package systématiquement.
> La chaîne d’outils multiplateforme de [l’interface de ligne de commande .NET Core](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation), utilisée pour développer des applications .NET Core, prend en charge une série de commandes NuGet, telles que delete, locals, push, pack et restore. 

## <a name="nuget-cli"></a>Interface de ligne de commande NuGet

L’interface de ligne de commande NuGet fournit l’accès à toutes les fonctionnalités NuGet et peut être exécutée sur Windows, Mac OSX et Linux, comme décrit dans les sections suivantes.

### <a name="windows"></a>Windows

**Téléchargement direct :**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> Avec NuGet 1.4+, vous pouvez utiliser `nuget update -self` pour mettre à jour votre nuget.exe existant vers la dernière version.

**Autres méthodes :**

- **Chocolatey** : installez le package Chocolatey [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) à l’aide du client [Chocolatey](http://chocolatey.org). 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio** : installez le package [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) à partir de la console du Gestionnaire de package dans Visual Studio.

    > [!Note]
    > **Pour les utilisateurs de NuGet 2.x** : en raison de modifications avec rupture introduites dans NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) pointe vers la dernière version stable de NuGet 2.x pour empêcher les ruptures potentielles des systèmes d’intégration continue.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX et Linux

Sur Mac OSX et Linux, il existe deux façons d’exécuter l’interface de ligne de commande NuGet :

- Installez le [SDK .NET Core](https://www.microsoft.com/net/download/core), qui inclut les fonctionnalités principales de NuGet. Des téléchargements sont également répertoriés dans la page [github.com/dotnet/cli](https://github.com/dotnet/cli). Si vous avez besoin de fonctionnalités plus complètes, utilisez la deuxième option ci-dessous pour utiliser `nuget.exe` avec Mono.

- Installez [Mono](http://www.mono-project.com/docs/getting-started/install/), puis utilisez l’exécutable en ligne de commande `nuget.exe` pour Windows (version 3.2 et ultérieures) à partir de [nuget.org/downloads](https://nuget.org/downloads). L’exécution de NuGet sur Mono est soumise aux limitations suivantes :

    - Commandes dont le fonctionnement a été confirmé au moyen de tests :
        - config
        - delete
        - help
        - install
        - list
        - push
        - setApiKey
        - sources
        - spec

    - Commandes fonctionnant partiellement :
        - pack : fonctionne avec des fichiers `.nuspec`, mais pas avec des fichiers projet.
        - restore : fonctionne avec des fichiers `packages.config` et `project.json`, mais pas avec des fichiers solution (`.sln`).

    - Commandes qui ne fonctionnent pas :
        - update

### <a name="related-topics"></a>Rubriques connexes

- [Informations de référence sur l’interface de ligne de commande NuGet](../tools/nuget-exe-cli-reference.md)
- [Création d’un package](../create-packages/creating-a-package.md)
- [Publication d’un package](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Gestionnaire de package NuGet dans Visual Studio

Le Gestionnaire de package NuGet est inclus dans toutes les éditions de Visual Studio sur Windows (versions 2012 et ultérieures). Il inclut l’interface utilisateur du Gestionnaire de package ([référence](../tools/package-manager-ui.md)), ainsi que la console du Gestionnaire de package par le biais de laquelle vous pouvez accéder aux outils fournis avec certains packages ([référence](../tools/package-manager-console.md)).

Le programme d’installation de Visual Studio 2017 inclut le Gestionnaire de package NuGet avec toute charge de travail qui utilise .NET. Pour effectuer une installation séparément, ou pour vérifier que le Gestionnaire de package est installé, exécutez le programme d’installation de Visual Studio 2017 et cochez l’option sous **Composants individuels > Outils de code > Gestionnaire de package NuGet**.

> [!Note]
> La console requiert [PowerShell 2.0](http://support.microsoft.com/kb/968929), déjà installé sur Windows 7 ou version ultérieure et Windows Server 2008 R2 ou version ultérieure.
>
> De plus, les commandes de la console du Gestionnaire de package fonctionnent uniquement dans Visual Studio sur Windows. Utilisez l’interface de ligne de commande NuGet en dehors de cet environnement, y compris avec Visual Studio pour Mac et Visual Studio Code.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Installation du Gestionnaire de package pour Visual Studio 2010 et antérieur

*Ces étapes ne sont pas nécessaires pour Visual Studio 2012 et ultérieur, qui incluent déjà le Gestionnaire de package.*

1. Dans Visual Studio 2010 et antérieur, cliquez sur **Outils > Extensions et mises à jour**.
1. Accédez à **En ligne**, puis recherchez « Gestionnaire de package NuGet dans Visual Studio » et cliquez sur **Télécharger**.
1. Dans la boîte de dialogue du programme d’installation, cliquez sur **Installer**.
1. Une fois l’installation terminée, redémarrez Visual Studio.

> [!Tip]
> Si vous ne pouvez pas utiliser la boîte de dialogue **Extensions et mises à jour** dans Visual Studio (par exemple, si elle est bloquée par un proxy), vous pouvez télécharger des extensions pour Visual Studio 2013 et 2015 directement depuis l’adresse [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

### <a name="updating-the-package-manager"></a>Mise à jour du Gestionnaire de package

Pour Visual Studio 2015 Update 2 et ultérieur, le Gestionnaire de package est automatiquement mis à jour avec la dernière version stable.

Pour Visual Studio 2015 Update 1 ou antérieur, sélectionnez la commande **Outils > Extensions et mises à jour**, puis cliquez sur l’onglet **Mises à jour** pour voir si une nouvelle version du Gestionnaire de package est disponible.  

### <a name="nuget-previews"></a>Aperçus de NuGet

Si vous souhaitez avoir un aperçu des fonctionnalités NuGet à venir, installez [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), qui fonctionne côte à côte avec les versions stables de Visual Studio.

Notez que la version NuGet Beta Channel précédente (`https://dotnet.myget.org/F/nuget-beta/vsix/`) pour Visual Studio 2015 n’est plus utilisée.

Pour signaler des problèmes avec une version de NuGet ou pour partager des idées, ouvrez un sujet sur le [dépôt GitHub NuGet](https://github.com/Nuget/Home).

### <a name="related-topics"></a>Rubriques connexes

- [Informations de référence sur l’interface utilisateur du Gestionnaire de package](../tools/package-manager-ui.md)
- [Informations de référence sur la console du Gestionnaire de package](../tools/package-manager-console.md)
- [Informations de référence sur la console du Gestionnaire de package (version PowerShell)](../tools/powershell-reference.md)