---
title: "Guide d’introduction à l’utilisation des packages NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet."
keywords: "installer NuGet, consommation de package NuGet, installation de packages NuGet, références de package NuGet, utilisation de packages NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 897419d1e49f12d54fbb996a2462e06e32933e65
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/31/2018
---
# <a name="install-and-use-a-package"></a>Installer et utiliser un package

Les packages NuGet sont des unités de code réutilisables que les autres développeurs mettent à votre disposition pour les utiliser dans vos projets. Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md).

[!INCLUDE [install-methods](../includes/install-methods.md)]

Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez. Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.

Le reste de cette rubrique vous guide tout au long du processus d’installation du package [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) dans un projet de plateforme Windows universelle (UWP, Universal Windows Platform) à l’aide de l’interface utilisateur du Gestionnaire de Package. Il contient ensuite un exemple d’utilisation du package. Vous utilisez un flux de travail similaire pour d’autres packages NuGet.

- [Installer les prérequis](#install-pre-requisites)
- [Créer un projet](#create-a-project)
- [Ajouter le package NuGet Newtonsoft.Json](#add-the-newtonsoftjson-nuget-package)
- [Utiliser l’API Newtonsoft.Json dans l’application](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **Commencez par nuget.org** : l’installation des packages à partir de nuget.org est un flux de travail courant grâce auquel les développeurs .NET peuvent rechercher des composants utilisables dans leurs propres applications. Vous pouvez toujours effectuer des recherches directement dans nuget.org, ou rechercher et installer des packages dans Visual Studio comme illustré dans cette rubrique.

## <a name="install-pre-requisites"></a>Installer les prérequis

Ce didacticiel nécessite Visual Studio 2015 Update 3 avec les Outils pour les applications Windows universelles, ou Visual Studio 2017 avec la charge de travail de développement Plateforme Windows universelle. Si vous avez déjà installé Visual Studio, vous pouvez réexécuter le programme d’installation pour ajouter les outils UWP.

Vous pouvez installer l’édition Community gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser l’édition Professional ou Enterprise. 

## <a name="create-a-project"></a>Créer un projet

Pour installer un package NuGet, vous avez besoin d’un projet .NET dans Visual Studio. Pour cette procédure pas à pas, vous pouvez utiliser une application WPF (Windows Presentation Foundation) ou UWP simple :

- Pour WPF (Windows 7+), choisissez **Fichier > Nouveau > Projet**, développez **Visual C#**, sélectionnez **Bureau classique Windows > Application WPF (.NET Framework)**, puis sélectionnez **OK**.
- Pour UWP (Windows 10), utilisez plutôt **Windows universel > Application vide (Application universelle)**. À l’invite, acceptez les valeurs par défaut pour Version cible et Version minimale.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Ajouter le package NuGet Newtonsoft.Json

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références** et choisissez **Gérer les packages NuGet**.

    ![Commande Gérer les packages NuGet pour les références de projet](media/QS_Use-02-ManageNuGetPackages.png)

1. Choisissez « nuget.org » comme **Source du package**, sélectionnez l’onglet **Parcourir**, recherchez **Newtonsoft.Json**, sélectionnez-le dans la liste, puis sélectionnez **Installer** :

    ![Recherche du package Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Si vous êtes invité à sélectionner un format de gestion de package, choisissez parmi PackageReference (recommandé) et `packages.config` :

    ![Sélection d’un format de référence de package](media/QS_Use-03b-SelectFormat.png)

1. Si vous êtes invité à vérifier les modifications, sélectionnez **OK**.

1. Cliquez avec le bouton droit sur la solution dans l’Explorateur de solutions, puis sélectionnez **Générer la solution**. Cette opération restaure tous les packages NuGet répertoriés sous **Références**. Pour plus d’informations, consultez [Restauration des packages](../consume-packages/package-restore.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Utiliser l’API Newtonsoft.Json dans l’application

Le package Newtonsoft.Json étant dans le projet, vous pouvez appeler sa méthode `JsonConvert.SerializeObject` pour convertir un objet en chaîne explicite.

1. Ouvrez `MainWindow.xaml` (WPF) ou `MainPage.xaml` (UWP) et remplacez l’élément `Grid` existant par les éléments suivants :

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Développez le nœud `MainWindow.xaml` (WPF) ou `MainPage.xaml` (UWP) dans l’Explorateur de solutions, ouvrez le fichier `.cs` et insérez le code suivant à l’intérieur de la classe `MainWindow` ou `MainPage`, après le constructeur :

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

1. Bien que vous ayez ajouté le package Newtonsoft.Json au projet, des tildes rouges s’affichent sous `JsonConvert`, car vous avez besoin d’une instruction `using`. Placez le curseur sur le `JsonConvert` souligné pour faire apparaître l’ampoule et l’option **Afficher les corrections éventuelles** :

    ![Ampoule avec commande Afficher les corrections éventuelles](media/QS_Use-04-ShowPotentialFixes.png)


1. Cliquez sur **Afficher les corrections éventuelles** (ou l’ampoule) et sélectionnez la première correction suggérée, `using Newtonsoft.Json;`. Cela ajoute la ligne nécessaire en haut du fichier.

    ![Ampoule permettant d’ajouter une instruction using](media/QS_Use-05-AddUsing.png)

1. Générez et exécutez l’application en appuyant sur F5 ou en sélectionnant **Déboguer > Démarrer le débogage** (UWP indiqué ici ; WPF est similaire) :

    ![Sortie initiale de l’application UWP](media/QS_Use-06-AppStart.png)

1. Cliquez sur le bouton pour remplacer le contenu du TextBlock par du texte JSON :

    ![Sortie de l’application UWP après un clic sur le bouton](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>Rubriques connexes

- [Vue d’ensemble et flux de travail de consommation de package](../consume-packages/overview-and-workflow.md)
- [Recherche et sélection des packages](../consume-packages/finding-and-choosing-packages.md)
- [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md)
