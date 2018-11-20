---
title: Guide pratique pour empaqueter des contrôles IU avec NuGet
description: Comment créer des packages NuGet qui contiennent des contrôles UWP ou WPF, y compris les métadonnées nécessaires et les fichiers de prise en charge pour les concepteurs Visual Studio et Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: dfbd6a3e6d59dfcea6394891703ea66bce5e8e92
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580270"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Créer des contrôles IU en tant que packages NuGet

Avec Visual Studio 2017, vous pouvez tirer parti de fonctionnalités qui ont été ajoutées pour les contrôles UWP et WPF que vous mettez à disposition dans les packages NuGet. Ce guide présente ces fonctionnalités dans le contexte des contrôles UWP au moyen de [l’exemple ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). Sauf indication contraire, la même procédure s’applique aux contrôles WPF.

## <a name="prerequisites"></a>Prérequis

1. Visual Studio 2017
1. Savoir [créer des packages UWP](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Générer la disposition de la bibliothèque

> [!Note]
> Cette procédure s’applique uniquement aux contrôles UWP.

La définition de la propriété `GenerateLibraryLayout` garantit la sortie de build du projet dans une disposition prête à être empaquetée, sans recourir à des entrées de fichiers individuels dans le fichier nuspec.

Dans les propriétés du projet, accédez à l’onglet Build, puis cochez la case « Générer la disposition de la bibliothèque ». Cette option va modifier le fichier projet et définir l’indicateur `GenerateLibraryLayout` sur true pour votre configuration de build et plateforme actuellement sélectionnées.

Vous pouvez également modifier le fichier projet pour ajouter `<GenerateLibraryLayout>true</GenerateLibraryLayout>` au premier groupe de propriétés inconditionnelles. Cette opération applique la propriété, quelles que soient la plateforme et la configuration de build.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Ajouter la prise en charge de la boîte à outils/du volet Composants pour les contrôles XAML

Pour qu’un contrôle XAML apparaisse dans la boîte à outils du concepteur XAML de Visual Studio et dans le volet Composants de Blend, créez un fichier `VisualStudioToolsManifest.xml` dans la racine du dossier `tools` de votre projet de package. Ce fichier n’est pas requis si vous n’avez pas besoin que le contrôle apparaisse dans la boîte à outils ou le volet Composants.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

La structure du fichier est la suivante :

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

où :

- *your_package_file* : nom de votre fichier de contrôle, tel que `ManagedPackage.winmd` (« ManagedPackage » est un nom arbitraire utilisé pour cet exemple et n’a aucune signification).
- *vs_category* : étiquette du groupe dans lequel le contrôle doit apparaître dans la boîte à outils du concepteur Visual Studio. Un `VSCategory` est nécessaire pour que le contrôle apparaisse dans la boîte à outils.
- *blend_category* : étiquette du groupe dans lequel le contrôle doit apparaître dans le volet Composants du concepteur Blend. Un `BlendCategory` est nécessaire pour que le contrôle apparaisse dans le volet Composants.
- *type_full_name_n* : nom complet de chaque contrôle, espace de noms compris, tel que `ManagedPackage.MyCustomControl`. Notez que le format avec un point est utilisé pour les types managés et natifs.

Dans les scénarios plus avancés, vous pouvez également inclure plusieurs éléments `<File>` dans `<FileList>` quand un package unique contient plusieurs assemblys. Vous pouvez également avoir plusieurs nœuds `<ToolboxItems>` dans un seul `<File>` si vous souhaitez organiser vos contrôles en catégories distinctes.

Dans l’exemple suivant, le contrôle implémenté dans `ManagedPackage.winmd` s’affiche dans Visual Studio et Blend dans un groupe appelé « Managed Package », tandis que « MyCustomControl » s’affiche dans ce groupe. Tous ces noms sont arbitraires.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Exemple de contrôle tel qu’il apparaît dans Visual Studio](media/UWP-control-vs-toolbox.png)

![Exemple de contrôle tel qu’il apparaît dans Blend](media/UWP-control-blend-assets.png)

> [!Note]
> Vous devez spécifier explicitement chaque contrôle que vous aimeriez voir dans la boîte à outils ou le volet Composants. Vérifiez que vous les spécifiez en utilisant le format `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Ajouter des icônes personnalisées à vos contrôles

Pour afficher une icône personnalisée dans la boîte à outils ou le volet Composants, ajoutez une image à votre projet ou au projet `design.dll` correspondant portant le nom « Namespace.ControlName.extension » et définissez l’action de génération sur « Ressource incorporée ». Vous devez également vous assurer que le `AssemblyInfo.cs` associé spécifie l’attribut ProvideMetadata : `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`. Consultez cet [exemple](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Les formats pris en charge sont `.png`, `.jpg`, `.jpeg`, `.gif` et `.bmp`. Le format recommandé est BMP24 en 16 pixels par 16 pixels.

![Exemple d’icône de boîte à outils](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

L’arrière-plan rose est remplacé au moment de l’exécution. Les icônes sont recolorées quand le thème Visual Studio change et que la couleur d’arrière-plan est attendue. Pour plus d’informations, consultez [Images et icônes pour Visual Studio](https://docs.microsoft.com/en-us/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).

Dans l’exemple ci-dessous, le projet contient un fichier image nommé « ManagedPackage.MyCustomControl.png ».

![Définition d’une icône personnalisée dans un projet](media/UWP-control-custom-icon.png)

> [!Note]
> Pour les contrôles natifs, vous devez placer l’icône en tant que ressource dans le projet `design.dll`.

## <a name="support-specific-windows-platform-versions"></a>Prendre en charge des versions de plateformes Windows spécifiques

Les packages UWP ont une propriété TargetPlatformVersion (TPV) et une propriété TargetPlatformMinVersion (TPMinV) qui définissent les limites supérieure et inférieure de la version de système d’exploitation sur laquelle l’application peut être installée. La propriété TPV spécifie en outre la version du SDK par rapport auquel l’application est générée. Tenez compte de ces propriétés quand vous créez un package UWP : l’utilisation d’API en dehors des limites des versions de plateforme définies dans l’application entraîne l’échec de la génération ou l’échec de l’application au moment de l’exécution.

Par exemple, supposons que vous avez défini la propriété TPMinV de votre package de contrôles sur Windows 10 Édition anniversaire (10.0 ; Build 14393), afin que le package soit consommé uniquement par les projets UWP qui correspondent à cette limite inférieure. Pour que le package puisse être utilisé par des projets UWP, les contrôles doivent être empaquetés avec les noms de dossiers suivants :

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet vérifiera automatiquement la propriété TPMinV du projet de consommation et l’installation échouera si cette valeur est inférieure à Windows 10 Édition anniversaire (10.0; Build 14393)

Avec WPF, supposons que vous souhaitez que votre package de contrôles WPF soit consommé par les projets ciblant .NET Framework 4.6.1 ou une version ultérieure. Pour appliquer cette procédure, vous devez empaqueter vos contrôles avec les noms de dossiers suivants :

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Ajouter la prise en charge au moment de la conception

Pour configurer où les propriétés de contrôle apparaissent dans l’inspecteur de propriétés, ajouter des ornements, etc., puis placez votre fichier `design.dll` dans le dossier `lib\uap10.0.14393\Design` en fonction de la plateforme cible. De plus, pour que la fonctionnalité **[Modifier le modèle > Modifier une copie](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** soit opérationnelle, vous devez inclure le fichier `Generic.xaml` et tous les dictionnaires de ressources qu’il fusionne dans le dossier `<your_assembly_name>\Themes` (là encore, en utilisant le nom de votre assembly). (Ce fichier n’a aucun impact sur le comportement d’un contrôle au moment de l’exécution.) La structure de dossiers apparaît donc comme ceci :

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Pour WPF, poursuivez avec l’exemple dans lequel vous souhaitez que votre package de contrôles WPF soit consommé par les projets ciblant .NET Framework 4.6.1 ou une version ultérieure :

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Par défaut, les propriétés des contrôles apparaissent sous la catégorie Divers dans l’inspecteur de propriété.

## <a name="use-strings-and-resources"></a>Utilisez des chaînes et des ressources

Vous pouvez incorporer des ressources de type chaîne (`.resw`) dans votre package qui peuvent être utilisées par votre contrôle ou le projet UWP de consommation ; pour ce faire, définissez la propriété **Action de génération** du fichier `.resw` sur **PRIResource**.

Pour obtenir un exemple, reportez-vous à [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) dans l’exemple ExtensionSDKasNuGetPackage.

> [!Note]
> Cette procédure s’applique uniquement aux contrôles UWP.

## <a name="see-also"></a>Voir aussi

- [Créer des packages UWP](create-uwp-packages.md)
- [Exemple ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
