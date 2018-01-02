---
title: "Guide pratique pour empaqueter des contrôles UWP avec NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "Comment créer des packages NuGet qui contiennent des contrôles UWP, y compris les métadonnées nécessaires et les fichiers de prise en charge pour les concepteurs Visual Studio et Blend."
keywords: "contrôles UWP NuGet, concepteur XAML Visual Studio, concepteur Blend, contrôles personnalisés"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f51dbabd406199752e4f9d612b498f59ffb54021
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>Création de contrôles UWP en tant que packages NuGet

Avec Visual Studio 2017, vous pouvez tirer parti de fonctionnalités qui ont été ajoutées pour les contrôles UWP que vous mettez à disposition dans les packages NuGet. Ce guide présente ces fonctionnalités au moyen de [l’exemple ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). 

## <a name="pre-requisites"></a>Prérequis :

1.  Visual Studio 2017
1.  Savoir [créer des packages UWP](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Ajouter la prise en charge de la boîte à outils/du volet Composants pour les contrôles XAML

Pour qu’un contrôle XAML apparaisse dans la boîte à outils du concepteur XAML de Visual Studio et dans le volet Composants de Blend, créez un fichier `VisualStudioToolsManifest.xml` dans la racine du dossier `tools` de votre projet de package. Ce fichier n’est pas requis si vous n’avez pas besoin que le contrôle apparaisse dans la boîte à outils ou le volet Composants.

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

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

Pour afficher une icône personnalisée dans la boîte à outils ou le volet Composants, ajoutez une image à votre projet ou au projet `design.dll` correspondant portant le nom « Namespace.ControlName.extension » et définissez l’action de génération sur « Ressource incorporée ». Les formats pris en charge sont `.png`, `.jpg`, `.jpeg`, `.gif` et `.bmp`. La taille d’image recommandée est 64 pixels par 64 pixels.

Dans l’exemple ci-dessous, le projet contient un fichier image nommé « ManagedPackage.MyCustomControl.png ».

![Définition d’une icône personnalisée dans un projet](media/UWP-control-custom-icon.png)

> [!Note]
> Pour les contrôles natifs, vous devez placer l’icône en tant que ressource dans le projet `design.dll`.

## <a name="support-specific-windows-platform-versions"></a>Prendre en charge des versions de plateformes Windows spécifiques

Les packages UWP ont une propriété TargetPlatformVersion (TPV) et une propriété TargetPlatformMinVersion (TPMinV) qui définissent les limites supérieure et inférieure de la version de système d’exploitation sur laquelle l’application peut être installée. La propriété TPV spécifie en outre la version du SDK par rapport auquel l’application est générée. Tenez compte de ces propriétés quand vous créez un package UWP : l’utilisation d’API en dehors des limites des versions de plateforme définies dans l’application entraîne l’échec de la génération ou l’échec de l’application au moment de l’exécution.

Par exemple, supposons que vous avez défini la propriété TPMinV de votre package de contrôles sur Windows 10 Édition anniversaire (10.0 ; Build 14393), afin que le package soit consommé uniquement par les projets UWP qui correspondent à cette limite inférieure. Pour que votre package puisse être consommé par les projets UWP basés sur `project.json`, vous devez empaqueter vos contrôles avec les noms de dossier suivants :

```
\lib\uap10.0\*
\ref\uap10.0\*
```

Pour appliquer la vérification TPMinV appropriée, créez un [fichier de cibles MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) et empaquetez-le sous le dossier de build (en remplaçant « your_assembly_name » par le nom de votre assembly) :

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

Voici à quoi devrait ressembler le fichier de cibles :

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>Ajouter la prise en charge au moment de la conception

Pour configurer où les propriétés de contrôle apparaissent dans l’inspecteur de propriétés, ajouter des ornements, etc., puis placez votre fichier `design.dll` dans le dossier `lib\<platform>\Design` en fonction de la plateforme cible. De plus, pour que la fonctionnalité **[Modifier le modèle > Modifier une copie](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** soit opérationnelle, vous devez inclure le `Generic.xaml` et tous les dictionnaires de ressources qu’il fusionne dans le dossier `<AssemblyName>\Themes`. (Ce fichier n’a aucun impact sur le comportement d’un contrôle au moment de l’exécution.)


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> Par défaut, les propriétés des contrôles apparaissent sous la catégorie Divers dans l’inspecteur de propriété.


## <a name="use-strings-and-resources"></a>Utilisez des chaînes et des ressources

Vous pouvez incorporer des ressources de type chaîne (`.resw`) dans votre package qui peuvent être utilisées par votre contrôle ou le projet UWP de consommation ; pour ce faire, définissez la propriété **Action de génération** du fichier `.resw` sur **PRIResource**.

Pour obtenir un exemple, reportez-vous à [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) dans l’exemple ExtensionSDKasNuGetPackage.

## <a name="package-content-such-as-images"></a>Empaqueter du contenu tel que des images

Pour empaqueter du contenu tel que des images pouvant être utilisées par votre contrôle ou le projet UWP de consommation, ajoutez ces fichiers au `lib\uap10.0.14393.0` dossier comme suit (« your_assembly_name » doit correspondre à nouveau à votre contrôle particulier) :

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

Vous pouvez également créer un [fichier de cibles MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) pour que le composant soit copié dans le dossier de sortie du projet de consommation :

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>Voir aussi

- [Créer des packages UWP](create-uwp-packages.md)
- [Exemple ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
