---
title: Créer et publier un package .NET Standard NuGet - Visual Studio sur Windows
description: Ce tutoriel explique pas à pas comment créer et publier un package NuGet .NET Standard avec Visual Studio sous Windows.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429030"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Démarrage rapide : Créer et publier un package NuGet avec Visual Studio (.NET Standard, Windows uniquement)

La création d’un package NuGet à partir d’une bibliothèque de classes .NET Standard dans Visual Studio sous Windows est un processus simple, de même que sa publication sur nuget.org avec un outil de ligne de commande (CLI).

> [!Note]
> Si vous utilisez Visual Studio pour Mac, consultez [ces informations](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) sur la création d’un package NuGet ou utilisez les [outils CLI dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Conditions préalables requises

1. Installez une édition de Visual Studio 2019 à l’adresse [visualstudio.com](https://www.visualstudio.com/) avec n’importe quelle charge de travail liée à .NET Core.

1. Si ce n'est déjà fait, installez l’interface CLI `dotnet`.

   Pour la CLI `dotnet`, à compter de Visual Studio 2017, la CLI `dotnet` est installée automatiquement avec les charges de travail associées à NET Core. Dans le cas contraire, installez le [SDK .NET Core](https://www.microsoft.com/net/download/) pour obtenir la CLI `dotnet`. La CLI `dotnet` dotnet est requise pour les projets .NET Standard qui utilisent le [format de style SDK](../resources/check-project-format.md) (attribut SDK). Le modèle de bibliothèque de classes .NET Standard par défaut dans Visual Studio 2017 et les versions ultérieures, qui est utilisé dans cet article, utilise l’attribut SDK.
   
   > [!Important]
   > Si vous utilisez un projet qui n’est pas de type SDK, suivez les procédures décrites dans [Créer et publier un package .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) pour créer et publier le package à la place. Pour cet article, la CLI `dotnet` est recommandée. Bien que vous puissiez publier un package NuGet à l’aide de la CLI `nuget.exe`, certaines des étapes décrites dans cet article sont spécifiques aux projets de type SDK et à la CLI dotnet. La cLI nuget.exe est utilisée pour les [projets qui ne sont pas de type SDK](../resources/check-project-format.md) (généralement .NET Framework).

1. [Créez un compte gratuit sur nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) si vous n’avez pas encore de compte. La création d’un compte envoie un e-mail de confirmation. Vous devez confirmer le compte avant de pouvoir charger un package.

## <a name="create-a-class-library-project"></a>Créer un projet de bibliothèque de classes

Vous pouvez utiliser un projet de bibliothèque de classes .NET Standard existant pour le code à empaqueter, ou bien en créer un de la façon suivante :

1. Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > .NET Standard**, sélectionnez le modèle « Bibliothèque de classes (.NET Standard) », nommez le projet AppLogger, puis cliquez sur **OK**.

   > [!Tip]
   > Sauf cas particulier, .NET Standard est la cible privilégiée pour les packages NuGet, car c’est celle qui assure la compatibilité avec le plus grand nombre de projets.

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

## <a name="configure-package-properties"></a>Configurer les propriétés de package

1. Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions et choisissez la commande de menu **Propriétés**, puis sélectionnez l’onglet **Package**.

   L’onglet **Package** s’affiche uniquement pour les projets de type SDK dans Visual Studio, généralement les projets de bibliothèque de classes .NET Standard ou .NET Core. Si vous ciblez un projet qui n’est pas de style SDK (généralement .NET Framework), [migrez le projet](../consume-packages/migrate-packages-config-to-package-reference.md) ou consultez [Créer et publier un package .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) à la place des instructions pas à pas.

    ![Propriétés de package NuGet dans un projet Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **Tags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.

1. Donnez à votre package un identificateur unique et remplissez les propriétés souhaitées. Pour un mappage des propriétés MSBuild (projet de type SDK) aux propriétés d'un fichier *.nuspec*, voir [Cibles de pack](../reference/msbuild-targets.md#pack-target). Pour les descriptions des propriétés, voir la référence du fichier [.nuspec ](../reference/nuspec.md). Toutes ces propriétés sont ajoutées au manifeste `.nuspec` créé par Visual Studio pour le projet.

    > [!Important]
    > Vous devez donner au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez. Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).
    >
    > Si vous tentez de publier un package avec un nom qui existe déjà, une erreur se produira.

1. (Facultatif) Pour afficher les propriétés directement dans le fichier projet, cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions et sélectionnez **Modifier AppLogger.csproj**.

   Cette option n’est disponible qu’à partir de Visual Studio 2017 pour les projets qui utilisent l’attribut de style SDK. Sinon, cliquez avec le bouton droit sur le projet et choisissez **Décharger le projet**. Cliquez ensuite avec le bouton droit sur le projet déchargé, puis choisissez **Modifier AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Exécuter la commande pack

1. Définissez la configuration en **Release**.

1. Cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis sélectionnez la commande **Empaqueter** :

    ![Commande pack de NuGet dans le menu contextuel du projet Visual Studio](media/qs_create-vs-02-pack-command.png)

    Si vous ne voyez pas la commande **Pack**, cela signifie que votre projet n’est probablement pas un projet de type SDK et que vous devez utiliser la CLI `nuget.exe`. [Migrez le projet](../consume-packages/migrate-packages-config-to-package-reference.md) et utilisez la CLI `dotnet`, ou consultez [Créer et publier un package .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) à la place pour obtenir des instructions détaillées.

1. Visual Studio génère le projet et crée le fichier `.nupkg`. Lisez les informations qui apparaissent sur la fenêtre **Sortie** (comme dans la capture d’écran suivante), notamment le chemin d’accès du fichier de package. Notez également que l’assembly généré est dans `bin\Release\netstandard2.0` comme il convient à la cible .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>(Facultatif) Générer le package à la création

Vous pouvez configurer Visual Studio pour générer automatiquement le package NuGet lorsque vous générez le projet.

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet et choisissez **Propriétés**.

2. Dans l’onglet **Package**, sélectionnez **Générer le package NuGet à la création**.

   ![Générer automatiquement le package à la création](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Lorsque vous créez automatiquement le package, le délai d’attente augmente la durée de création de votre projet.

### <a name="optional-pack-with-msbuild"></a>(Facultatif) Compresser avec MSBuild

En guise d’alternative à l’utilisation de la commande de menu **Pack**, NuGet 4.x+ et MSBuild 15.1+ prennent en charge une cible `pack` quand le projet contient les données de package nécessaires. Ouvrez une invite de commandes, accédez au dossier de votre projet et exécutez la commande suivante. (Il est généralement recommandé de démarrer l’invite de commandes développeur pour Visual Studio à partir du menu Démarrer, car elle est configurée avec tous les chemins nécessaires pour MSBuild.)

Pour plus d’informations, consultez [Créer un package avec MSBuild](../create-packages/creating-a-package-msbuild.md).

## <a name="publish-the-package"></a>Publier le package

Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de l’interface CLI `nuget.exe` ou `dotnet.exe`, avec une clé API acquise sur nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Obtenir une clé API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>Publier avec l’interface CLI dotnet ou nuget.exe

Sélectionnez l'onglet de votre outil CLI, soit **.NET Core CLI** (CLI dotnet) ou **NuGet** (CLI nuget.exe).

# <a name="net-core-cli"></a>[CLI .NET Core](#tab/netcore-cli)

Cette étape est l’alternative recommandée à l’utilisation de `nuget.exe`.

Avant de pouvoir publier le package, vous devez d’abord ouvrir une ligne de commande.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[NuGet](#tab/nuget)

Cette étape aboutit au même résultat que `dotnet.exe`.

1. Ouvrez une ligne de commande et accédez au dossier contenant le fichier `.nupkg`.

1. Exécutez la commande suivante, en spécifiant le nom de votre package (ID de package unique) et en remplaçant la valeur de la clé par celle de votre clé API :

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

Voir [nuget push](../reference/cli-reference/cli-ref-push.md).

---

### <a name="publish-errors"></a>Erreurs de publication

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Gérer le package publié

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Ajout d’un fichier Lisez-moi et d’autres fichiers

Pour spécifier directement les fichiers à inclure dans le package, modifiez le fichier projet et utilisez la propriété `content` :

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Cela inclut un fichier nommé `readme.txt` dans la racine du package. Visual Studio affiche le contenu de ce fichier sous forme de texte brut immédiatement après avoir installé le package directement. (Les fichiers Lisez-moi ne s’affichent pas pour les packages installés en tant que dépendances). Par exemple, voici comment s’affiche le fichier Lisez-moi du package HtmlAgilityPack :

![Affichage d’un fichier Lisez-moi pour un package NuGet lors de l’installation](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Le simple ajout du fichier readme.txt à la racine du projet ne permet pas de l’ajouter dans le package résultant.

## <a name="related-video"></a>Vidéo connexe

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

Recherchez d’autres vidéos NuGet sur [Channel 9](https://channel9.msdn.com/Series/NuGet-101) et [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="related-topics"></a>Rubriques connexes

- [Créer un package](../create-packages/creating-a-package-dotnet-cli.md)
- [Publier un package](../nuget-org/publish-a-package.md)
- [Packages de préversion](../create-packages/Prerelease-Packages.md)
- [Prendre en charge plusieurs frameworks cibles](../create-packages/multiple-target-frameworks-project-file.md)
- [Gestion de version des packages](../concepts/package-versioning.md)
- [Création de packages localisés](../create-packages/creating-localized-packages.md)
- [Documentation de la bibliothèque .NET Standard](/dotnet/articles/standard/library)
- [Portage vers .NET Core à partir du .NET Framework](/dotnet/articles/core/porting/index)
