---
title: Installer et utiliser un package NuGet dans Visual Studio pour Mac
description: Didacticiel de procédure pas à pas sur le processus d’installation et d’utilisation d’un package NuGet dans un projet de Visual Studio pour Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238475"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Démarrage rapide : Installer et utiliser un package dans Visual Studio pour Mac

Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets. Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md). Les packages sont installés dans un projet Visual Studio pour Mac à l’aide du gestionnaire de package NuGet. Cet article présente le processus qui utilise le package [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) populaire et un projet de console .net core. Le même processus s’applique à tout autre projet Xamarin ou .NET Core.

Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez. Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.

> [!Tip]
> **Prise en main de nuget.org** : Les développeurs .NET parcourent *nutget.org* à la recherche de composants qu’ils peuvent réutiliser dans leurs propres applications. Vous pouvez effectuer des recherches directement dans *nuget.org*, ou rechercher et installer des packages dans Visual Studio comme illustré dans cet article. Pour obtenir des informations générales, consultez [Rechercher et évaluer des packages NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Prérequis

- Visual Studio 2019 pour Mac.

Vous pouvez installer l’édition Community 2019 gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser l’édition Professional ou Enterprise.

Si vous utilisez Visual Studio sur Windows, consultez [installer et utiliser un package dans Visual Studio (Windows uniquement)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Création d’un projet

Les packages NuGet peuvent être installés dans n’importe quel projet .NET, à condition qu’ils prennent en charge la même version cible de .NET Framework que le projet.

Pour cette procédure pas à pas, utilisez une application console .NET Core simple. Créez un projet dans Visual Studio pour Mac utilisant **fichier > nouvelle solution...** , sélectionnez le modèle **application console du > .net Core >** . Cliquez sur **Suivant**. Lorsque vous y êtes invité, acceptez les valeurs par défaut de la version **cible du .NET Framework** .

Visual Studio crée le projet qui s’ouvre dans l’Explorateur de solutions.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Ajouter le package NuGet Newtonsoft.Json

Pour installer le package, vous utilisez le gestionnaire de package NuGet. Quand vous installez un package, NuGet enregistre la dépendance dans votre fichier projet ou dans un `packages.config` fichier (en fonction du format du projet). Pour plus d’informations, consultez [Vue d’ensemble et flux de consommation des packages](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Gestionnaire de package NuGet

1. Dans Explorateur de solutions, cliquez avec le bouton droit sur **dépendances** , puis choisissez **Ajouter des packages...** .

    ![Commande Gérer les packages NuGet pour les références de projet](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Choisissez « nuget.org » comme **source du package** dans le coin supérieur gauche de la boîte de dialogue et recherchez **Newtonsoft. JSON**, sélectionnez ce package dans la liste, puis sélectionnez **Ajouter des packages...** :

    ![Recherche du package Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Si vous souhaitez plus d’informations sur le gestionnaire de package NuGet, consultez [installer et gérer des packages à l’aide de Visual Studio pour Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Utiliser l’API Newtonsoft.Json dans l’application

Le package Newtonsoft.Json étant dans le projet, vous pouvez appeler sa méthode `JsonConvert.SerializeObject` pour convertir un objet en chaîne explicite.

1. Ouvrez le `Program.cs` fichier (situé dans le panneau solutions) et remplacez le contenu du fichier par le code suivant :

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

1. Générez et exécutez l’application en sélectionnant **exécuter > démarrer le débogage**:

1. Une fois l’application exécutée, la sortie JSON sérialisée s’affiche dans la console :

  ![Sortie de l’application console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Étapes suivantes
Félicitations pour l’installation et l’utilisation de votre premier package NuGet !

> [!div class="nextstepaction"]
> [Installer et gérer des packages à l’aide de Visual Studio pour Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Pour explorer plus en détail ce que NuGet a à offrir, sélectionnez les liens ci-dessous.

- [Vue d’ensemble et flux de travail de consommation de package](../consume-packages/overview-and-workflow.md)
- [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md)
