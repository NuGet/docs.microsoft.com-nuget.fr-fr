---
title: Installer et utiliser un forfait NuGet dans Visual Studio pour Mac
description: Un tutoriel pas à pas sur le processus d’installation et d’utilisation d’un paquet NuGet dans un studio visuel pour le projet Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238475"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Quickstart: Installer et utiliser un paquet dans Visual Studio pour Mac

Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets. Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md). Les paquets sont installés dans un projet Visual Studio for Mac à l’aide du gestionnaire de paquets NuGet. Cet article démontre le processus utilisant le populaire forfait [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) et un projet de console .NET Core. Le même processus s’applique à tout autre projet Xamarin ou .NET Core.

Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez. Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.

> [!Tip]
> **Commencez par nuget.org**: Naviguer *nuget.org* est la façon dont les développeurs .NET trouvent généralement des composants qu’ils peuvent réutiliser dans leurs propres applications. Vous pouvez rechercher *nuget.org* directement ou trouver et installer des paquets dans Visual Studio comme indiqué dans cet article. Pour obtenir des informations générales, consultez [Rechercher et évaluer des packages NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Prérequis

- Visual Studio 2019 pour Mac.

Vous pouvez installer l’édition Community 2019 gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser l’édition Professional ou Enterprise.

Si vous utilisez Visual Studio sur Windows, voir [Installer et utiliser un paquet dans Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Création d’un projet

Les packages NuGet peuvent être installés dans n’importe quel projet .NET, à condition qu’ils prennent en charge la même version cible de .NET Framework que le projet.

Pour cette procédure pas à pas, utilisez une application simple .NET Core Console. Créez un projet en studio visuel pour Mac à **l’aide de File > New Solution...**, sélectionnez le modèle **d’application App > > Console .NET Core >.** Cliquez sur **Suivant**. Acceptez les valeurs par défaut pour **Target Framework** lorsqu’elles sont invitées.

Visual Studio crée le projet qui s’ouvre dans l’Explorateur de solutions.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Ajouter le package NuGet Newtonsoft.Json

Pour installer le paquet, vous utilisez le gestionnaire de paquets NuGet. Lorsque vous installez un colis, NuGet enregistre la `packages.config` dépendance dans votre fichier de projet ou dans un fichier (selon le format du projet). Pour plus d’informations, consultez [Vue d’ensemble et flux de consommation des packages](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Gestionnaire de package NuGet

1. Dans Solution Explorer, cliquez à droite **dépendances** et choisissez **Add Packages...**.

    ![Commande Gérer les packages NuGet pour les références de projet](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Choisissez "nuget.org" comme **source de paquet** dans le coin supérieur gauche du dialogue, et recherchez **Newtonsoft.Json**, sélectionnez ce paquet dans la liste, et sélectionnez **Ajouter des paquets...**:

    ![Recherche du package Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Si vous voulez plus d’informations sur le gestionnaire de paquets NuGet, voir [Installer et gérer les paquets à l’aide de Visual Studio pour Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Utiliser l’API Newtonsoft.Json dans l’application

Le package Newtonsoft.Json étant dans le projet, vous pouvez appeler sa méthode `JsonConvert.SerializeObject` pour convertir un objet en chaîne explicite.

1. Ouvrez `Program.cs` le fichier (situé dans le pad de solution) et remplacez le contenu du fichier par le code suivant :

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. Construisez et exécutez l’application en sélectionnant **Run > Start Debugging**:

1. Une fois l’application diffusée, vous verrez la sortie JSON sérialisée apparaître dans la console :

  ![Sortie de l’application Console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Étapes suivantes
Félicitations pour l’installation et l’utilisation de votre premier package NuGet !

> [!div class="nextstepaction"]
> [Installer et gérer des paquets à l’aide de Visual Studio pour Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Pour explorer plus en détail ce que NuGet a à offrir, sélectionnez les liens ci-dessous.

- [Vue d’ensemble et flux de travail de consommation de package](../consume-packages/overview-and-workflow.md)
- [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md)
