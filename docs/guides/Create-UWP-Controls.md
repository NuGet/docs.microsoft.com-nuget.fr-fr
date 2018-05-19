---
title: Guide pratique pour empaqueter des contrôles UWP avec NuGet
description: Comment créer des packages NuGet qui contiennent des contrôles UWP, y compris les métadonnées nécessaires et les fichiers de prise en charge pour les concepteurs Visual Studio et Blend.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/14/2018
ms.topic: tutorial
ms.openlocfilehash: 963846e857c8757176e4fbe1cd60c92a7397ba01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="a6aa9-103">Création de contrôles UWP en tant que packages NuGet</span><span class="sxs-lookup"><span data-stu-id="a6aa9-103">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="a6aa9-104">Avec Visual Studio 2017, vous pouvez tirer parti de fonctionnalités qui ont été ajoutées pour les contrôles UWP que vous mettez à disposition dans les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="a6aa9-105">Ce guide présente ces fonctionnalités au moyen de [l’exemple ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="a6aa9-105">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a6aa9-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="a6aa9-106">Prerequisites</span></span>

1. <span data-ttu-id="a6aa9-107">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a6aa9-107">Visual Studio 2017</span></span>
1. <span data-ttu-id="a6aa9-108">Savoir [créer des packages UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a6aa9-108">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="a6aa9-109">Ajouter la prise en charge de la boîte à outils/du volet Composants pour les contrôles XAML</span><span class="sxs-lookup"><span data-stu-id="a6aa9-109">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="a6aa9-110">Pour qu’un contrôle XAML apparaisse dans la boîte à outils du concepteur XAML de Visual Studio et dans le volet Composants de Blend, créez un fichier `VisualStudioToolsManifest.xml` dans la racine du dossier `tools` de votre projet de package.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-110">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="a6aa9-111">Ce fichier n’est pas requis si vous n’avez pas besoin que le contrôle apparaisse dans la boîte à outils ou le volet Composants.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-111">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="a6aa9-112">La structure du fichier est la suivante :</span><span class="sxs-lookup"><span data-stu-id="a6aa9-112">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="a6aa9-113">où :</span><span class="sxs-lookup"><span data-stu-id="a6aa9-113">where:</span></span>

- <span data-ttu-id="a6aa9-114">*your_package_file* : nom de votre fichier de contrôle, tel que `ManagedPackage.winmd` (« ManagedPackage » est un nom arbitraire utilisé pour cet exemple et n’a aucune signification).</span><span class="sxs-lookup"><span data-stu-id="a6aa9-114">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="a6aa9-115">*vs_category* : étiquette du groupe dans lequel le contrôle doit apparaître dans la boîte à outils du concepteur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-115">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="a6aa9-116">Un `VSCategory` est nécessaire pour que le contrôle apparaisse dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-116">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="a6aa9-117">*blend_category* : étiquette du groupe dans lequel le contrôle doit apparaître dans le volet Composants du concepteur Blend.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-117">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="a6aa9-118">Un `BlendCategory` est nécessaire pour que le contrôle apparaisse dans le volet Composants.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-118">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="a6aa9-119">*type_full_name_n* : nom complet de chaque contrôle, espace de noms compris, tel que `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-119">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="a6aa9-120">Notez que le format avec un point est utilisé pour les types managés et natifs.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-120">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="a6aa9-121">Dans les scénarios plus avancés, vous pouvez également inclure plusieurs éléments `<File>` dans `<FileList>` quand un package unique contient plusieurs assemblys.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-121">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="a6aa9-122">Vous pouvez également avoir plusieurs nœuds `<ToolboxItems>` dans un seul `<File>` si vous souhaitez organiser vos contrôles en catégories distinctes.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-122">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="a6aa9-123">Dans l’exemple suivant, le contrôle implémenté dans `ManagedPackage.winmd` s’affiche dans Visual Studio et Blend dans un groupe appelé « Managed Package », tandis que « MyCustomControl » s’affiche dans ce groupe.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-123">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="a6aa9-124">Tous ces noms sont arbitraires.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-124">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="a6aa9-127">Vous devez spécifier explicitement chaque contrôle que vous aimeriez voir dans la boîte à outils ou le volet Composants.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-127">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="a6aa9-128">Vérifiez que vous les spécifiez en utilisant le format `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-128">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="a6aa9-129">Ajouter des icônes personnalisées à vos contrôles</span><span class="sxs-lookup"><span data-stu-id="a6aa9-129">Add custom icons to your controls</span></span>

<span data-ttu-id="a6aa9-130">Pour afficher une icône personnalisée dans la boîte à outils ou le volet Composants, ajoutez une image à votre projet ou au projet `design.dll` correspondant portant le nom « Namespace.ControlName.extension » et définissez l’action de génération sur « Ressource incorporée ».</span><span class="sxs-lookup"><span data-stu-id="a6aa9-130">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="a6aa9-131">Les formats pris en charge sont `.png`, `.jpg`, `.jpeg`, `.gif` et `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-131">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="a6aa9-132">La taille d’image recommandée est 64 pixels par 64 pixels.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-132">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="a6aa9-133">Dans l’exemple ci-dessous, le projet contient un fichier image nommé « ManagedPackage.MyCustomControl.png ».</span><span class="sxs-lookup"><span data-stu-id="a6aa9-133">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Définition d’une icône personnalisée dans un projet](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="a6aa9-135">Pour les contrôles natifs, vous devez placer l’icône en tant que ressource dans le projet `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-135">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="a6aa9-136">Prendre en charge des versions de plateformes Windows spécifiques</span><span class="sxs-lookup"><span data-stu-id="a6aa9-136">Support specific Windows platform versions</span></span>

<span data-ttu-id="a6aa9-137">Les packages UWP ont une propriété TargetPlatformVersion (TPV) et une propriété TargetPlatformMinVersion (TPMinV) qui définissent les limites supérieure et inférieure de la version de système d’exploitation sur laquelle l’application peut être installée.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-137">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="a6aa9-138">La propriété TPV spécifie en outre la version du SDK par rapport auquel l’application est générée.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-138">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="a6aa9-139">Tenez compte de ces propriétés quand vous créez un package UWP : l’utilisation d’API en dehors des limites des versions de plateforme définies dans l’application entraîne l’échec de la génération ou l’échec de l’application au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-139">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="a6aa9-140">Par exemple, supposons que vous avez défini la propriété TPMinV de votre package de contrôles sur Windows 10 Édition anniversaire (10.0 ; Build 14393), afin que le package soit consommé uniquement par les projets UWP qui correspondent à cette limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-140">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="a6aa9-141">Pour que le package puisse être utilisé par des projets UWP, les contrôles doivent être empaquetés avec les noms de dossiers suivants :</span><span class="sxs-lookup"><span data-stu-id="a6aa9-141">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0\*
    \ref\uap10.0\*

<span data-ttu-id="a6aa9-142">Pour appliquer la vérification TPMinV appropriée, créez un [fichier de cibles MSBuild](/visualstudio/msbuild/msbuild-targets) et empaquetez-le sous le dossier `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name>\` avec le nom de votre assembly.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-142">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name>\` with the name of your specific assembly.</span></span>

<span data-ttu-id="a6aa9-143">Voici à quoi devrait ressembler le fichier de cibles :</span><span class="sxs-lookup"><span data-stu-id="a6aa9-143">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="a6aa9-144">Ajouter la prise en charge au moment de la conception</span><span class="sxs-lookup"><span data-stu-id="a6aa9-144">Add design-time support</span></span>

<span data-ttu-id="a6aa9-145">Pour configurer où les propriétés de contrôle apparaissent dans l’inspecteur de propriétés, ajouter des ornements, etc., puis placez votre fichier `design.dll` dans le dossier `lib\uap10.0\Design` en fonction de la plateforme cible.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-145">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="a6aa9-146">De plus, pour que la fonctionnalité **[Modifier le modèle > Modifier une copie](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** soit opérationnelle, vous devez inclure le fichier `Generic.xaml` et tous les dictionnaires de ressources qu’il fusionne dans le dossier `<your_assembly_name>\Themes` (là encore, en utilisant le nom de votre assembly).</span><span class="sxs-lookup"><span data-stu-id="a6aa9-146">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="a6aa9-147">(Ce fichier n’a aucun impact sur le comportement d’un contrôle au moment de l’exécution.) La structure de dossiers apparaît donc comme ceci :</span><span class="sxs-lookup"><span data-stu-id="a6aa9-147">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="a6aa9-148">Par défaut, les propriétés des contrôles apparaissent sous la catégorie Divers dans l’inspecteur de propriété.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-148">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="a6aa9-149">Utilisez des chaînes et des ressources</span><span class="sxs-lookup"><span data-stu-id="a6aa9-149">Use strings and resources</span></span>

<span data-ttu-id="a6aa9-150">Vous pouvez incorporer des ressources de type chaîne (`.resw`) dans votre package qui peuvent être utilisées par votre contrôle ou le projet UWP de consommation ; pour ce faire, définissez la propriété **Action de génération** du fichier `.resw` sur **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-150">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="a6aa9-151">Pour obtenir un exemple, reportez-vous à [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) dans l’exemple ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-151">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="a6aa9-152">Empaqueter du contenu tel que des images</span><span class="sxs-lookup"><span data-stu-id="a6aa9-152">Package content such as images</span></span>

<span data-ttu-id="a6aa9-153">Pour empaqueter du contenu tel que des images pouvant être utilisées par votre contrôle ou le projet UWP de consommation, placez ces fichiers dans le dossier `lib\uap10.0`.</span><span class="sxs-lookup"><span data-stu-id="a6aa9-153">To package content such as images that can be used by your control or the consuming UWP project, place those files within the `lib\uap10.0` folder.</span></span>

<span data-ttu-id="a6aa9-154">Vous pouvez également créer un [fichier de cibles MSBuild](/visualstudio/msbuild/msbuild-targets) pour que le composant soit copié dans le dossier de sortie du projet de consommation :</span><span class="sxs-lookup"><span data-stu-id="a6aa9-154">You may also author an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="a6aa9-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a6aa9-155">See also</span></span>

- [<span data-ttu-id="a6aa9-156">Créer des packages UWP</span><span class="sxs-lookup"><span data-stu-id="a6aa9-156">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="a6aa9-157">Exemple ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="a6aa9-157">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)