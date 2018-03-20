---
title: "Guide d’introduction à la création et à la publication de package NuGet .NET Standard avec Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/18/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Ce didacticiel explique pas à pas comment créer et publier un package NuGet .NET Standard avec Visual Studio 2017."
keywords: "Création de package NuGet, publication de package NuGet, didacticiel NuGet, création de package NuGet avec Visual Studio, pack msbuild"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 733fee616601e1d15d8fb5814b5bfb7905ff4a33
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-standard"></a>Créer et publier un package avec Visual Studio (.NET Standard)

La création d’un package NuGet à partir d’une bibliothèque de classes .NET Standard dans Visual Studio est un processus simple, de même que sa publication sur nuget.org avec un outil de ligne de commande (CLI).

## <a name="prerequisites"></a>Prérequis

1. Installez une édition de Visual Studio 2017 à l’adresse [visualstudio.com](https://www.visualstudio.com/) avec n’importe quelle charge de travail liée à .NET. Visual Studio 2017 intègre automatiquement les fonctionnalités NuGet lorsqu’une charge de travail .NET est installée.

1. Installez l’interface CLI `nuget.exe` en la téléchargeant sur [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) : enregistrez ce fichier `.exe` dans un dossier approprié et ajoutez ce dossier à votre variable d’environnement PATH.

    Si le [Kit de développement logiciel (SDK) .NET Core](https://www.microsoft.com/net/download/) est installé, vous pouvez également utiliser l’interface CLI `dotnet`.

1. [Créez un compte gratuit sur nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si vous n’avez pas encore de compte. La création d’un compte envoie un e-mail de confirmation. Vous devez confirmer le compte avant de pouvoir charger un package.

## <a name="create-a-class-library-project"></a>Créer un projet de bibliothèque de classes

Vous pouvez utiliser un projet de bibliothèque de classes .NET Standard existant pour le code à empaqueter, ou bien en créer un de la façon suivante :

1. Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > .NET Standard**, sélectionnez le modèle « Bibliothèque de classes (.NET Standard) », nommez le projet AppLogger, puis cliquez sur **OK**.

1. Cliquez avec le bouton droit sur le fichier projet résultant et sélectionnez **Générer** pour être sûr que le projet a été créé correctement. La DLL se trouve dans le dossier Debug (ou Release si vous générez cette configuration).

Dans un package NuGet réel, vous implémenterez bien sûr de nombreuses fonctionnalités utiles, grâce auxquelles d’autres personnes pourront créer des applications. Pour cette procédure pas à pas, toutefois, vous n’écrirez pas de code supplémentaire, car une bibliothèque de classes à partir du modèle suffit pour créer un package. Néanmoins, si vous souhaitez obtenir du code fonctionnel pour le package, utilisez ce qui suit :

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> Sauf cas particulier, .NET Standard est la cible privilégiée pour les packages NuGet, car c’est celle qui assure la compatibilité avec le plus grand nombre de projets.

## <a name="configure-package-properties"></a>Configurer les propriétés de package

1. Sélectionnez la commande de menu **Projet > Propriétés**, puis l’onglet **Package**. (L’onglet **Package** s’affiche uniquement pour les projets de bibliothèque de classes .NET Standard ; si vous ciblez le .NET Framework, consultez [Créer et publier un package .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md).)

    ![Propriétés de package NuGet dans un projet Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **Tags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.

1. Donnez à votre package un identificateur unique et remplissez les propriétés souhaitées. Vous trouverez une description des différentes propriétés dans la section [Informations de référence sur le fichier .nuspec](../reference/nuspec.md). Toutes ces propriétés sont ajoutées au manifeste `.nuspec` créé par Visual Studio pour le projet.

    > [!Important]
    > Vous devez donner au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez. Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).
    >
    > Si vous tentez de publier un package avec un nom qui existe déjà, une erreur se produira.

1. Facultatif : pour afficher les propriétés directement dans le fichier projet, cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions et sélectionnez **Modifier AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Exécuter la commande pack

1. Définissez la configuration en **Release**.

1. Cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis sélectionnez la commande **Empaqueter** :

    ![Commande pack de NuGet dans le menu contextuel du projet Visual Studio](media/qs_create-vs-02-pack-command.png)

1. Visual Studio génère le projet et crée le fichier `.nupkg`. Lisez les informations qui apparaissent sur la fenêtre **Sortie** (comme dans la capture d’écran suivante), notamment le chemin d’accès du fichier de package. Notez également que l’assembly généré est dans `bin\Release\netstandard2.0` comme il convient à la cible .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Autre option : pack avec MSBuild

En guise d’alternative à l’utilisation de la commande de menu **Pack**, NuGet 4.x+ et MSBuild 15.1+ prennent en charge une cible `pack` quand le projet contient les données de package nécessaires. Ouvrez une invite de commandes, accédez au dossier de votre projet et exécutez la commande suivante. (Il est généralement recommandé de démarrer l’invite de commandes développeur pour Visual Studio à partir du menu Démarrer, car elle est configurée avec tous les chemins nécessaires pour MSBuild.)

```cli
msbuild /t:pack /p:Configuration=Release
```

Vous trouverez alors le package dans le dossier `bin\Release`.

Pour plus d’options avec `msbuild /t:pack`, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Publier le package

Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de l’interface CLI `nuget.exe` ou `dotnet.exe`, avec une clé API acquise sur nuget.org.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Obtenir une clé API

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publier avec nuget push

Cette étape aboutit au même résultat que `dotnet.exe`.

1. Accédez au dossier contenant le fichier `.nupkg`.

1. Exécutez la commande suivante, en spécifiant le nom de votre package et en remplaçant la valeur de la clé par celle de votre clé API :

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe affiche les résultats du processus de publication :

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Voir [nuget push](../tools/cli-ref-push.md).

### <a name="publish-with-dotnet-nuget-push"></a>Publier avec dotnet nuget push

Cette étape aboutit au même résultat que `nuget.exe`.

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Erreurs de publication

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Gérer le package publié

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Rubriques connexes

- [Créer un package](../create-packages/creating-a-package.md)
- [Publier un package](../create-packages/publish-a-package.md)
- [Prendre en charge plusieurs frameworks cibles](../create-packages/supporting-multiple-target-frameworks.md)
- [Gestion des versions de package](../reference/package-versioning.md)
- [Création de packages localisés](../create-packages/creating-localized-packages.md)
- [Documentation de la bibliothèque .NET Standard](/dotnet/articles/standard/library)
- [Portage vers .NET Core à partir du .NET Framework](/dotnet/articles/core/porting/index)