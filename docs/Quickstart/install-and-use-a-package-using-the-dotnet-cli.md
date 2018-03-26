---
title: "Guide d’introduction à l’utilisation des packages NuGet via l’infrastructure CLI dotnet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet .NET Core."
keywords: "installer NuGet, consommation de package NuGet, installation de packages NuGet, références de package NuGet, utilisation de packages NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: accc6d7bb5abff43ffaa083fa55c13cd5b10ce10
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a>Installer et utiliser un package à l’aide de l’interface CLI dotnet

Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets. Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md). Les packages sont installés dans un projet .NET Core à l’aide de la commande `dotnet add package`, comme décrit dans cet article pour le package courant [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).

Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez. Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.

> [!Tip]
> **Commencez par nuget.org** : les développeurs .NET parcourent nutget.org à la recherche de composants qu’ils peuvent réutiliser dans leurs propres applications. Vous pouvez effectuer des recherches directement dans nuget.org, ou rechercher et installer des packages dans Visual Studio comme illustré dans cet article.

## <a name="prerequisites"></a>Prérequis

- Le [kit SDK .NET Core](https://www.microsoft.com/net/download/), qui fournit l’outil en ligne de commande `dotnet`.

## <a name="create-a-project"></a>Créer un projet

Les packages NuGet peuvent être installés dans tout type de projet .NET. Pour cette procédure pas à pas, créez un projet de console .NET Core simple comme suit :

1. Créez un dossier pour le projet.

1. Créez le projet à l’aide de la commande suivante :

    ```cli
    dotnet new console
    ```

1. Utilisez `dotnet run` pour vérifier que l’application a été créée correctement.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Ajouter le package NuGet Newtonsoft.Json

1. Utilisez la commande suivante pour installer le package `Newtonsoft.json` :

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. Une fois la commande terminée, ouvrez le fichier `.csproj` pour voir la référence ajoutée :

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
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

## <a name="related-articles"></a>Articles connexes

- [Vue d’ensemble et flux de travail de consommation de package](../consume-packages/overview-and-workflow.md)
- [Recherche et sélection des packages](../consume-packages/finding-and-choosing-packages.md)
- [Méthodes d’installation d’un package](../consume-packages/ways-to-install-a-package.md)
- [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md)