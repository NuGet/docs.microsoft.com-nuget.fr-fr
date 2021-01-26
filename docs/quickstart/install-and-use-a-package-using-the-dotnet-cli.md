---
title: Installer et utiliser un package NuGet à l’aide de l’interface CLI dotnet
description: Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet .NET Core.
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: adbf8f457d8520e3087e539b91ef932877aec3a0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775450"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Démarrage rapide : Installer et utiliser un package à l’aide de l’interface CLI dotnet

Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets. Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md). Les packages sont installés dans un projet .NET Core à l’aide de la commande `dotnet add package`, comme décrit dans cet article pour le package courant [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).

Une fois l’installation terminée, reportez-vous au package dans le code `using <namespace>` où \<namespace\> est spécifique au package que vous utilisez. Vous pourrez alors utiliser l’API du package.

> [!Tip]
> **Commencez par nuget.org** : les développeurs .NET parcourent nutget.org à la recherche de composants qu’ils peuvent réutiliser dans leurs propres applications. Vous pouvez effectuer des recherches directement dans nuget.org, ou rechercher et installer des packages dans Visual Studio comme illustré dans cet article.

## <a name="prerequisites"></a>Prérequis

- Le [kit SDK .NET Core](https://www.microsoft.com/net/download/), qui fournit l’outil en ligne de commande `dotnet`. À compter de Visual Studio 2017, la CLI dotnet est installée automatiquement avec les charges de travail associées à NET Core.

## <a name="create-a-project"></a>Création d’un projet

Les packages NuGet peuvent être installés dans tout type de projet .NET. Pour cette procédure pas à pas, créez un projet de console .NET Core simple comme suit :

1. Créez un dossier pour le projet.

1. Ouvrez une invite de commandes et basculez vers le nouveau dossier.

1. Créez le projet à l’aide de la commande suivante :

    ```dotnetcli
    dotnet new console
    ```

1. Utilisez `dotnet run` pour vérifier que l’application a été créée correctement.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Ajouter le package NuGet Newtonsoft.Json

1. Utilisez la commande suivante pour installer le package `Newtonsoft.json` :

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Une fois la commande terminée, ouvrez le fichier `.csproj` pour voir la référence ajoutée :

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Utiliser l’API Newtonsoft.Json dans l’application

1. Ouvrez le fichier `Program.cs` et ajoutez la ligne suivante en haut du fichier :

    ```cs
    using Newtonsoft.Json;
    ```

1. Ajoutez le code suivant avant la ligne `class Program` :

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Remplacez la fonction `Main` par ce qui suit :

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. Générez et exécutez l’application à l’aide de la commande `dotnet run`. La sortie doit être la représentation JSON de l’objet `Account` dans le code :

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>Vidéo connexe

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

Recherchez d’autres vidéos NuGet sur [Channel 9](https://channel9.msdn.com/Series/NuGet-101) et [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Étapes suivantes

Félicitations pour l’installation et l’utilisation de votre premier package NuGet !

> [!div class="nextstepaction"]
> [Installer et utiliser des packages à l’aide de l’interface CLI dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Pour explorer plus en détail ce que NuGet a à offrir, sélectionnez les liens ci-dessous.

- [Vue d’ensemble et flux de travail de consommation de package](../consume-packages/overview-and-workflow.md)
- [Recherche et sélection de packages](../consume-packages/finding-and-choosing-packages.md)
- [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md)
