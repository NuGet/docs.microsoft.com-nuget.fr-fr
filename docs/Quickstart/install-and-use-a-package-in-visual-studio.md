---
title: "Guide d’introduction à l’utilisation des packages NuGet dans Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet Visual Studio."
keywords: "installer NuGet, consommation de package NuGet, installation de packages NuGet, références de package NuGet, utilisation de packages NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff905fec6d6af4fa40fd4331cb970121b6eb0879
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a>Installer et utiliser un package dans Visual Studio

Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets. Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md). Les packages sont installés dans un projet Visual Studio à l’aide de l’interface utilisateur du Gestionnaire de package ou de la Console du Gestionnaire de package, comme décrit dans cet article pour le package courant [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) et un projet de plateforme Windows universelle (UWP).

Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez. Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.

> [!Tip]
> **Commencez par nuget.org** : les développeurs .NET parcourent nutget.org à la recherche de composants qu’ils peuvent réutiliser dans leurs propres applications. Vous pouvez effectuer des recherches directement dans nuget.org, ou rechercher et installer des packages dans Visual Studio comme illustré dans cet article.

## <a name="prerequisites"></a>Prérequis

- Visual Studio 2017 avec la charge de travail Développement pour la plateforme Windows universelle ou
- Visual Studio 2015 Update 3 avec les Outils pour les applications Windows universelles.

Vous pouvez installer l’édition Community 2017 gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser l’édition Professional ou Enterprise.

## <a name="create-a-project"></a>Créer un projet

Les packages NuGet peuvent être installés dans tout type de projet .NET. Pour cette procédure pas à pas, vous utilisez une application Windows universelle (UWP) simple. Créez un projet dans Visual Studio en sélectionnant le menu **Fichier > Nouveau projet...** puis **Windows universel > Application vide (Universal Windows)**. À l’invite, acceptez les valeurs par défaut pour Version cible et Version minimale.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Ajouter le package NuGet Newtonsoft.Json

Pour installer le package, vous pouvez utiliser l’interface utilisateur du Gestionnaire de package ou sur la console du Gestionnaire de package. Quand vous installez un package, NuGet enregistre la dépendance dans votre fichier projet ou un fichier `packages.config`. Pour plus d’informations, consultez [Vue d’ensemble et flux de consommation des packages](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Interface utilisateur du gestionnaire de package

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références** et choisissez **Gérer les packages NuGet**.

    ![Commande Gérer les packages NuGet pour les références de projet](media/QS_Use-02-ManageNuGetPackages.png)

1. Choisissez « nuget.org » comme **Source du package**, sélectionnez l’onglet **Parcourir**, recherchez **Newtonsoft.Json**, sélectionnez-le dans la liste, puis sélectionnez **Installer** :

    ![Recherche du package Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Acceptez toutes les invites de licence.

1. (Visual Studio 2017) Si vous êtes invité à sélectionner un format de gestion de package, sélectionnez **PackageReference dans le fichier projet** :

    ![Sélection d’un format de référence de package](media/QS_Use-03b-SelectFormat.png)

1. Si vous êtes invité à vérifier les modifications, sélectionnez **OK**.

### <a name="package-manager-console"></a>Console du Gestionnaire de package

1. Sélectionnez la commande de menu **Outils -> Gestionnaire de package NuGet -> Console du Gestionnaire de package**.

1. Une fois la console ouverte, vérifiez que la liste déroulante **Projet par défaut** affiche le projet dans lequel vous souhaitez installer le package. Si la solution ne contient qu’un seul projet, il est déjà sélectionné.

    ![Recherche du package Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Entrez la commande `Install-Package Newtonsoft.json` (consultez [Install-Package](../tools/ps-ref-install-package.md)). La fenêtre de la console affiche la sortie de la commande. Les erreurs indiquent généralement que le package n’est pas compatible avec le framework cible du projet.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Utiliser l’API Newtonsoft.Json dans l’application

Le package Newtonsoft.Json étant dans le projet, vous pouvez appeler sa méthode `JsonConvert.SerializeObject` pour convertir un objet en chaîne explicite.

1. Ouvrez `MainPage.xaml` et remplacez l’élément `Grid` existant par l’élément suivant :

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Ouvrez le fichier `MainPage.xaml.cs` (situé sous le nœud `MainPage.xaml` dans l’Explorateur de solutions), puis insérez le code suivant dans le constructeur `MainPage` :

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Bien que vous ayez ajouté le package Newtonsoft.Json au projet, des tildes rouges s’affichent sous `JsonConvert`, car vous avez besoin d’une instruction `using` en haut du fichier de code :

    ```cs
    using Newtonsoft.json;
    ```

1. Générez et exécutez l’application en appuyant sur F5 ou en sélectionnant **Déboguer > Démarrer le débogage** :

    ![Sortie initiale de l’application UWP](media/QS_Use-06-AppStart.png)

1. Cliquez sur le bouton pour remplacer le contenu du TextBlock par du texte JSON :

    ![Sortie de l’application UWP après un clic sur le bouton](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Articles connexes

- [Vue d’ensemble et flux de travail de consommation de package](../consume-packages/overview-and-workflow.md)
- [Recherche et sélection des packages](../consume-packages/finding-and-choosing-packages.md)
- [Méthodes d’installation d’un package](../consume-packages/ways-to-install-a-package.md)
- [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md)