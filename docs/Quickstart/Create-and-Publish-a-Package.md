---
title: "Guide d’introduction à la création et à la publication de package NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Didacticiel expliquant comment créer et publier un package NuGet à l’aide de l’interface de ligne de commande de nuget.exe et de Visual Studio."
keywords: "création de package NuGet, publication de package NuGet, didacticiel NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a>Créer et publier un package

La création d’un package NuGet à partir d’une bibliothèque de classes .NET et sa publication sur nuget.org sont des processus simples. Cet article explique pas à pas comment procéder avec Visual Studio et l’interface de ligne de commande (CLI) NuGet.

## <a name="pre-requisites"></a>Conditions préalables

1. Installez une édition quelconque de Visual Studio 2017 à partir de [visualstudio.com](https://www.visualstudio.com/).

1. Installez l’outil CLI NuGet, `nuget.exe`, en téléchargeant la dernière version de `nuget.exe` à partir de [nuget.org/downloads](https://nuget.org/downloads) et en enregistrant le fichier `.exe` à un emplacement dans votre PATH. Notez que le téléchargement *est* l’outil lui-même, et pas un programme d’installation.

1. Créez un projet de bibliothèque de classes .NET approprié pour le code que vous souhaitez empaqueter. Si vous n’avez pas encore de projet, vous pouvez en créer un simple comme suit :
    1. Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > Windows**, sélectionnez le modèle « Bibliothèque de classes », nommez le projet AppLogger, puis cliquez sur **OK**.
    1. Cliquez avec le bouton droit sur le fichier projet résultant et sélectionnez **Générer** pour être sûr que le projet a été créé correctement. La DLL se trouve dans le dossier Debug (ou Release si vous générez cette configuration).

    Dans un package NuGet réel, bien sûr, vous implémenterez de nombreuses fonctionnalités utiles sur lesquelles d’autres personnes pourront créer des applications. Pour cette procédure pas à pas, toutefois, vous n’écrirez pas de code supplémentaire, car une bibliothèque de classes à partir du modèle suffit pour créer un package.

## <a name="create-the-nuspec-package-manifest-file"></a>Créer le fichier manifeste du package .nuspec

Chaque package NuGet a besoin d’un manifeste &mdash;un fichier `.nuspec`&mdash; pour décrire son contenu et ses dépendances. La commande `nuget spec` crée ce fichier pour vous, et ensuite vous le personnalisez. Dans cet exemple, vous créez le fichier `.nuspec` à partir d’un fichier projet. Vous pouvez également créer le manifeste par d’autres moyens, comme décrit dans [Créer un package](../create-packages/creating-a-package.md).

1. Ouvrez une invite de commandes et accédez au dossier contenant votre fichier projet (`.csproj`).

1. Exécutez la commande CLI NuGet `spec` pour générer le manifeste, qui est nommé d’après votre projet, par exemple `AppLogger.nuspec`:

    ```cli
    nuget spec
    ```

1. Ouvrez le fichier dans un éditeur de texte. Le manifeste ressemble au code ci-dessous, où les jetons au format `<token>` (comme `$id$`) seront remplacés pendant le processus d’empaquetage par des valeurs tirées du fichier Properties/AssemblyInfo.cs du projet. Pour plus d’informations sur les jetons, consultez [Création d’un fichier .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. Sélectionnez un ID de package qui est unique sur nuget.org. Nous vous recommandons d’utiliser les conventions d’affectation de noms décrites dans [Création d’un package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). N’oubliez pas de mettre à jour les balises d’auteur et de description, sinon vous recevrez une erreur à l’étape suivante. Voici un fichier `.nuspec` mis à jour en guise d’exemple :

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Pour les packages générés en vue d’une consommation publique, faites particulièrement attention à l’élément `<tags>`, car ces balises aident l’utilisateur à trouver votre package et à comprendre ce qu’il fait.

## <a name="run-the-pack-command"></a>Exécuter la commande pack

Pour générer un package NuGet (un fichier `.nupkg`) à partir d’un projet, exécutez la commande `pack` :

```cli
nuget pack AppLogger.csproj
```

Cette commande crée `AppLogger.1.0.0.0.nupkg` en utilisant le nom et le numéro de version de package tirés du fichier `.nuspec`. La commande émet des avertissements si vous n’avez pas mis à jour différents champs dans le fichier `.nuspec` et remplacé leurs valeurs par défaut.

## <a name="publish-the-package"></a>Publier le package

Une fois que vous avez un fichier `.nupkg`, vous pouvez le publier sur nuget.org à l’aide de la commande `push`. (Vous pouvez également utiliser le [flux de travail de publication nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).)

> [!Warning]
> Les packages que vous publiez sur nuget.org sont visibles publiquement par d’autres développeurs. Pour héberger des packages en privé, consultez [Hébergement de packages](../hosting-packages/overview.md).

1. Créez un compte gratuit sur [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), ou connectez-vous si vous en avez déjà un. La création d’un compte envoie un e-mail de confirmation. Vous devez confirmer le compte avant de pouvoir charger un package.

1. Une fois connecté, sélectionnez votre nom d’utilisateur (dans le coin supérieur droit), puis **Clés API**.

1. Sélectionnez **Créer**, donnez un nom à votre clé, sélectionnez **Sélectionner les étendues > Push** sous **Clé API**, entrez * pour **Modèle Glob**, puis sélectionnez **Créer**.

1. Une fois la clé créée, sélectionnez **Copier** pour récupérer la clé d’accès dont vous aurez besoin dans l’interface CLI :

    ![Copie de la clé d’API dans le Presse-papiers](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > Enregistrez votre clé à un emplacement sécurisé et ne la divulguez pas. Au cas où elle serait révélée accidentellement, vous pourriez la régénérer à tout moment. Vous pouvez également supprimer la clé API si vous ne souhaitez plus distribuer des packages par le biais de l’interface CLI.

1. À l’invite de commandes, exécutez la commande suivante, en spécifiant votre nom de package et en remplaçant la clé par la valeur copiée à l’étape 4 :

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe affiche les résultats du processus de publication :

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. À partir de votre profil sur nuget.org, sélectionnez **Manage Packages** (Gérer les packages) pour voir celui que vous venez de publier. Vous recevrez aussi un e-mail de confirmation. Notez que l’indexation de votre package et son apparition dans les résultats de la recherche peuvent prendre un certain temps. Pendant ce temps, la page de votre package contient le message ci-dessous :

    ![This package has not been indexed yet. (Ce package n’a pas encore été indexé.) It will appear in search results and will be available for install/restore after indexing is complete. (Il apparaîtra dans les résultats de la recherche et sera disponible pour l’installation/restauration une fois l’indexation terminée.)](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **Analyse antivirus** : tous les packages chargés sur nuget.org sont analysés et rejetés si des virus sont détectés. Tous les packages répertoriés sur nuget.org sont aussi analysés régulièrement.

Et voilà ! Vous venez de publier votre premier package NuGet sur [nuget.org](https://www.nuget.org/). D’autres développeurs peuvent maintenant l’utiliser dans leurs propres projets.

## <a name="related-topics"></a>Rubriques connexes

- [Créer un package](../create-packages/creating-a-package.md)
- [Publier un package](../create-packages/publish-a-package.md)
- [Prendre en charge plusieurs frameworks cibles](../create-packages/supporting-multiple-target-frameworks.md)
- [Gestion des versions de package](../reference/package-versioning.md)
- [Création de packages localisés](../create-packages/creating-localized-packages.md)
