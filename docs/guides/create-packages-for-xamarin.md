---
title: Créer des packages NuGet pour Xamarin (pour iOS, Android et Windows) avec Visual Studio 2017 ou 2019
description: Procédure pas à pas de bout en bout montrant comment créer des packages NuGet pour Xamarin qui utilisent des API natives sur iOS, Android et Windows.
author: JonDouglas
ms.author: jodou
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fdabeeac57ca12716f6ed2614d036f1623407b20
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774223"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Créer des packages pour Xamarin avec Visual Studio 2017 ou 2019

Un package pour Xamarin contient du code qui utilise des API natives sur iOS, Android et Windows, suivant le système d’exploitation du runtime. Bien que cela soit simple à faire, il est préférable de permettre aux développeurs d’utiliser le package à partir d’une bibliothèque de classes portable ou de bibliothèques .NET Standard par le biais d’une surface d’exposition d’API communes.

Dans cette procédure pas à pas, vous utilisez Visual Studio 2017 ou 2019 pour créer un package NuGet multiplateforme qui peut être utilisé dans des projets mobiles sur iOS, Android et Windows.

1. [Conditions préalables](#prerequisites)
1. [Créer la structure du projet et le code d’abstraction](#create-the-project-structure-and-abstraction-code)
1. [Écrire du code spécifique de la plateforme](#write-your-platform-specific-code)
1. [Créer et mettre à jour le fichier .nuspec](#create-and-update-the-nuspec-file)
1. [Empaqueter le composant](#package-the-component)
1. [Rubriques connexes](#related-topics)

## <a name="prerequisites"></a>Prérequis

1. Visual Studio 2017 ou 2019 avec plateforme Windows universelle (UWP) et Xamarin. Installez l’édition Community gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/) ; bien entendu, vous pouvez également utiliser les éditions Professional et Enterprise. Pour inclure les outils Xamarin et UWP, sélectionnez une installation personnalisée et cochez les options appropriées.
1. Interface de ligne de commande NuGet. Téléchargez la dernière version de nuget.exe à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix. Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.

> [!Note]
> nuget.exe étant l’outil CLI proprement dit, pas un programme d’installation, veillez à enregistrer le fichier téléchargé à partir de votre navigateur au lieu de l’exécuter.

## <a name="create-the-project-structure-and-abstraction-code"></a>Créer la structure du projet et le code d’abstraction

1. Téléchargez et exécutez l' [extension de modèles de plug-in .NET standard multiplateforme](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pour Visual Studio. Ces modèles facilitent la création de la structure de projet nécessaire pour cette procédure pas à pas.
1. Dans Visual Studio 2017, **fichier > nouveau projet de >**, recherchez `Plugin` , sélectionnez le modèle de **plug-in bibliothèque multiplateforme .NET standard** , remplacez le nom par LoggingLibrary, puis cliquez sur OK.

    ![Nouveau projet application vide (Xamarin. Forms portable) dans VS 2017](media/CrossPlatform-NewProject.png)

    Dans Visual Studio 2019, **fichier > nouveau projet de >**, recherchez `Plugin` , sélectionnez le modèle de **plug-in bibliothèque .NET standard multiplateforme** , puis cliquez sur suivant.

    ![Nouveau projet application vide (Xamarin. Forms portable) dans VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    Remplacez le nom par LoggingLibrary, puis cliquez sur créer.

    ![Configuration de la nouvelle application vide (Xamarin. Forms portable) dans VS 2019](media/CrossPlatform-NewProject19-Part2.png)

La solution obtenue contient deux projets partagés, ainsi qu’un large éventail de projets spécifiques à la plateforme :

- Le `ILoggingLibrary` projet, qui est contenu dans le `ILoggingLibrary.shared.cs` fichier, définit l’interface publique (la surface d’exposition de l’API) du composant. C’est là que vous définissez l’interface de votre bibliothèque.
- L’autre projet partagé contient du code dans `CrossLoggingLibrary.shared.cs` qui localise une implémentation spécifique à la plateforme de l’interface abstraite au moment de l’exécution. En général, vous n’avez pas besoin de modifier ce fichier.
- Les projets spécifiques à la plateforme, tels que `LoggingLibrary.android.cs` , contiennent chacun une implémentation native de l’interface dans leurs `LoggingLibraryImplementation.cs` fichiers respectifs (vs 2017) ou `LoggingLibrary.<PLATFORM>.cs` (vs 2019). C’est là que vous générez le code de votre bibliothèque.

Par défaut, le fichier ILoggingLibrary.shared.cs du `ILoggingLibrary` projet contient une définition d’interface, mais aucune méthode. Dans le cadre de cette procédure pas à pas, vous devez ajouter une méthode `Log` comme suit :

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>Écrire du code spécifique de la plateforme

Pour implémenter une implémentation spécifique de la plateforme de l’interface `ILoggingLibrary` et ses méthodes, effectuez les étapes suivantes :

1. Ouvrez le `LoggingLibraryImplementation.cs` fichier (vs 2017) ou `LoggingLibrary.<PLATFORM>.cs` (vs 2019) de chaque projet de plateforme, puis ajoutez le code nécessaire. Par exemple (à l’aide du `Android` projet de plateforme) :

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. Répétez cette implémentation dans les projets pour chaque plateforme que vous souhaitez prendre en charge.
1. Cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour vérifier votre travail et générer les artefacts que vous allez ensuite empaqueter. Si vous obtenez des erreurs liées à des références manquantes, cliquez avec le bouton droit sur la solution, sélectionnez **Restaurer des packages NuGet** pour installer des dépendances, puis regénérez la solution.

> [!Note]
> Si vous utilisez Visual Studio 2019, avant de sélectionner **restaurer les packages NuGet** et d’essayer de reconstruire, vous devez modifier la version de en `MSBuild.Sdk.Extras` `2.0.54` `LoggingLibrary.csproj` . Pour accéder à ce fichier, vous devez tout d’abord cliquer avec le bouton droit sur le projet (sous la solution) et sélectionner `Unload Project` , après quoi vous cliquez avec le bouton droit sur le projet déchargé et sélectionnez `Edit LoggingLibrary.csproj` .

> [!Note]
> Pour effectuer une génération dans le cadre d’iOS, vous avez besoin d’un Mac en réseau connecté à Visual Studio, comme décrit dans [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) (Présentation de Xamarin.iOS pour Visual Studio). Si vous ne disposez pas d’un Mac, désactivez le projet iOS dans le gestionnaire de configuration (étape 3 ci-dessus).

## <a name="create-and-update-the-nuspec-file"></a>Créer et mettre à jour le fichier .nuspec

1. Ouvrez une invite de commandes, accédez au dossier `LoggingLibrary` qui se trouve un niveau en dessous du fichier `.sln` et exécutez la commande NuGet `spec` pour créer le fichier `Package.nuspec` initial :

    ```cli
    nuget spec
    ```

1. Renommez ce fichier `LoggingLibrary.nuspec` et ouvrez-le dans un éditeur.
1. Mettez à jour le fichier afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée. La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> Vous pouvez apposer à la version de votre package le suffixe `-alpha`, `-beta` ou `-rc` pour marquer votre package en tant que préversion ; consultez [Préversions](../create-packages/prerelease-packages.md) pour plus d’informations sur les préversions.

### <a name="add-reference-assemblies"></a>Ajouter des assemblys de référence

Pour inclure des assemblys de référence propres à la plateforme, ajoutez le code suivant à l’élément `<files>` de `LoggingLibrary.nuspec` en fonction de vos plateformes prises en charge :

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> Pour raccourcir les noms des fichiers DLL et XML, cliquez avec le bouton droit sur un projet donné, sélectionnez l’onglet **Bibliothèque** et changez les noms d’assembly.

### <a name="add-dependencies"></a>Ajout de dépendances

Si vous avez des dépendances spécifiques pour des implémentations natives, utilisez l’élément `<dependencies>` avec des éléments `<group>` pour les spécifier, par exemple :

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

Par exemple, le code suivant définit iTextSharp en tant que dépendance pour la cible UAP :

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Fichier .nuspec final

Votre fichier `.nuspec` final doit maintenant ressembler au code ci-après, où vous devez là aussi remplacer YOUR_NAME par une valeur appropriée :

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>Empaqueter le composant

Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :

```cli
nuget pack LoggingLibrary.nuspec
```

Cela a pour effet de générer `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et que vous développez tous les nœuds, le contenu suivant apparaît :

![NuGet Package Explorer affichant le package LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Un fichier `.nupkg` est simplement un fichier zip avec une extension différente. Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.

Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Rubriques connexes

- [Référence NuSpec](../reference/nuspec.md)
- [Packages de symboles](../create-packages/symbol-packages.md)
- [Gestion des versions de package](../concepts/package-versioning.md)
- [Prise en charge de plusieurs versions du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Inclure des cibles et des propriétés MSBuild dans un package](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Création de packages localisés](../create-packages/creating-localized-packages.md)
