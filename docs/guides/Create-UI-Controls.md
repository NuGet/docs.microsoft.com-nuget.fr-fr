---
title: Guide pratique pour empaqueter des contrôles IU avec NuGet
description: Comment créer des packages NuGet qui contiennent des contrôles UWP ou WPF, y compris les métadonnées nécessaires et les fichiers de prise en charge pour les concepteurs Visual Studio et Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 17062d83349fe1b8cd28e57dd888686a226ac9cb
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238021"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="8f9e4-103">Créer des contrôles IU en tant que packages NuGet</span><span class="sxs-lookup"><span data-stu-id="8f9e4-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="8f9e4-104">À compter de Visual Studio 2017, vous pouvez utiliser les fonctionnalités qui ont été ajoutées pour les contrôles UWP et WPF que vous mettez à disposition dans les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="8f9e4-105">Ce guide présente ces fonctionnalités dans le contexte des contrôles UWP au moyen de [l’exemple ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="8f9e4-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="8f9e4-106">Sauf indication contraire, la même procédure s’applique aux contrôles WPF.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f9e4-107">Conditions préalables requises</span><span class="sxs-lookup"><span data-stu-id="8f9e4-107">Prerequisites</span></span>

1. <span data-ttu-id="8f9e4-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8f9e4-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="8f9e4-109">Savoir [créer des packages UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="8f9e4-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="8f9e4-110">Générer la disposition de la bibliothèque</span><span class="sxs-lookup"><span data-stu-id="8f9e4-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="8f9e4-111">Cette procédure s’applique uniquement aux contrôles UWP.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="8f9e4-112">La définition de la propriété `GenerateLibraryLayout` garantit la sortie de build du projet dans une disposition prête à être empaquetée, sans recourir à des entrées de fichiers individuels dans le fichier nuspec.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="8f9e4-113">Dans les propriétés du projet, accédez à l’onglet Build, puis cochez la case « Générer la disposition de la bibliothèque ».</span><span class="sxs-lookup"><span data-stu-id="8f9e4-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="8f9e4-114">Cette option va modifier le fichier projet et définir l’indicateur `GenerateLibraryLayout` sur true pour votre configuration de build et plateforme actuellement sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="8f9e4-115">Vous pouvez également modifier le fichier projet pour ajouter `<GenerateLibraryLayout>true</GenerateLibraryLayout>` au premier groupe de propriétés inconditionnelles.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="8f9e4-116">Cette opération applique la propriété, quelles que soient la plateforme et la configuration de build.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="8f9e4-117">Ajouter la prise en charge de la boîte à outils/du volet Composants pour les contrôles XAML</span><span class="sxs-lookup"><span data-stu-id="8f9e4-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="8f9e4-118">Pour qu’un contrôle XAML apparaisse dans la boîte à outils du concepteur XAML de Visual Studio et dans le volet Composants de Blend, créez un fichier `VisualStudioToolsManifest.xml` dans la racine du dossier `tools` de votre projet de package.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="8f9e4-119">Ce fichier n’est pas requis si vous n’avez pas besoin que le contrôle apparaisse dans la boîte à outils ou le volet Composants.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="8f9e4-120">La structure du fichier est la suivante :</span><span class="sxs-lookup"><span data-stu-id="8f9e4-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="8f9e4-121">où :</span><span class="sxs-lookup"><span data-stu-id="8f9e4-121">where:</span></span>

- <span data-ttu-id="8f9e4-122">*your_package_file* : nom de votre fichier de contrôle, tel que `ManagedPackage.winmd` (« ManagedPackage » est un nom arbitraire utilisé pour cet exemple et n’a aucune signification).</span><span class="sxs-lookup"><span data-stu-id="8f9e4-122">*your_package_file* : the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="8f9e4-123">*vs_category* : étiquette du groupe dans lequel le contrôle doit apparaître dans la boîte à outils du concepteur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-123">*vs_category* : The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="8f9e4-124">Un `VSCategory` est nécessaire pour que le contrôle apparaisse dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
<span data-ttu-id="8f9e4-125">*ui_framework* : le nom de l’infrastructure, tel que « WPF », Notez que `UIFramework` l’attribut est requis sur les nœuds ToolBoxItems dans Visual Studio 16,7 Preview 3 ou version ultérieure pour que le contrôle s’affiche dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-125">*ui_framework* : The name of the Framework, such as 'WPF', note that `UIFramework` attribute is required on ToolboxItems nodes on Visual Studio 16.7 Preview 3 or above for the control to appear in toolbox.</span></span>
- <span data-ttu-id="8f9e4-126">*blend_category* : étiquette du groupe dans lequel le contrôle doit apparaître dans le volet Composants du concepteur Blend.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-126">*blend_category* : The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="8f9e4-127">Un `BlendCategory` est nécessaire pour que le contrôle apparaisse dans le volet Composants.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-127">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="8f9e4-128">*type_full_name_n* : nom complet de chaque contrôle, espace de noms compris, tel que `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-128">*type_full_name_n* : The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="8f9e4-129">Notez que le format avec un point est utilisé pour les types managés et natifs.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-129">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="8f9e4-130">Dans les scénarios plus avancés, vous pouvez également inclure plusieurs éléments `<File>` dans `<FileList>` quand un package unique contient plusieurs assemblys.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-130">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="8f9e4-131">Vous pouvez également avoir plusieurs nœuds `<ToolboxItems>` dans un seul `<File>` si vous souhaitez organiser vos contrôles en catégories distinctes.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-131">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="8f9e4-132">Dans l’exemple suivant, le contrôle implémenté dans `ManagedPackage.winmd` s’affiche dans Visual Studio et Blend dans un groupe appelé « Managed Package », tandis que « MyCustomControl » s’affiche dans ce groupe.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-132">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="8f9e4-133">Tous ces noms sont arbitraires.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-133">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Exemple de contrôle tel qu’il apparaît dans Visual Studio](media/UWP-control-vs-toolbox.png)

![Exemple de contrôle tel qu’il apparaît dans Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="8f9e4-136">Vous devez spécifier explicitement chaque contrôle que vous aimeriez voir dans la boîte à outils ou le volet Composants.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-136">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="8f9e4-137">Vérifiez que vous les spécifiez en utilisant le format `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-137">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="8f9e4-138">Ajouter des icônes personnalisées à vos contrôles</span><span class="sxs-lookup"><span data-stu-id="8f9e4-138">Add custom icons to your controls</span></span>

<span data-ttu-id="8f9e4-139">Pour afficher une icône personnalisée dans la boîte à outils ou le volet Composants, ajoutez une image à votre projet ou au projet `design.dll` correspondant portant le nom « Namespace.ControlName.extension » et définissez l’action de génération sur « Ressource incorporée ».</span><span class="sxs-lookup"><span data-stu-id="8f9e4-139">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="8f9e4-140">Vous devez également vous assurer que le `AssemblyInfo.cs` associé spécifie l’attribut ProvideMetadata : `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-140">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="8f9e4-141">Consultez cet [exemple](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="8f9e4-141">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="8f9e4-142">Les formats pris en charge sont `.png`, `.jpg`, `.jpeg`, `.gif` et `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-142">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="8f9e4-143">Le format recommandé est BMP24 en 16 pixels par 16 pixels.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-143">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Exemple d’icône de boîte à outils](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="8f9e4-145">L’arrière-plan rose est remplacé au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-145">The pink background is replaced at runtime.</span></span> <span data-ttu-id="8f9e4-146">Les icônes sont recolorées quand le thème Visual Studio change et que la couleur d’arrière-plan est attendue.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-146">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="8f9e4-147">Pour plus d’informations, consultez [Images et icônes pour Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="8f9e4-147">For more information, please reference [Images and Icons for Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="8f9e4-148">Dans l’exemple ci-dessous, le projet contient un fichier image nommé « ManagedPackage.MyCustomControl.png ».</span><span class="sxs-lookup"><span data-stu-id="8f9e4-148">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Définition d’une icône personnalisée dans un projet](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="8f9e4-150">Pour les contrôles natifs, vous devez placer l’icône en tant que ressource dans le projet `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-150">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="8f9e4-151">Prendre en charge des versions de plateformes Windows spécifiques</span><span class="sxs-lookup"><span data-stu-id="8f9e4-151">Support specific Windows platform versions</span></span>

<span data-ttu-id="8f9e4-152">Les packages UWP ont une propriété TargetPlatformVersion (TPV) et une propriété TargetPlatformMinVersion (TPMinV) qui définissent les limites supérieure et inférieure de la version de système d’exploitation sur laquelle l’application peut être installée.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-152">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="8f9e4-153">La propriété TPV spécifie en outre la version du SDK par rapport auquel l’application est générée.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-153">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="8f9e4-154">Tenez compte de ces propriétés quand vous créez un package UWP : l’utilisation d’API en dehors des limites des versions de plateforme définies dans l’application entraîne l’échec de la génération ou l’échec de l’application au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-154">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="8f9e4-155">Par exemple, supposons que vous avez défini la propriété TPMinV de votre package de contrôles sur Windows 10 Édition anniversaire (10.0 ; Build 14393), afin que le package soit consommé uniquement par les projets UWP qui correspondent à cette limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-155">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="8f9e4-156">Pour que le package puisse être utilisé par des projets UWP, les contrôles doivent être empaquetés avec les noms de dossiers suivants :</span><span class="sxs-lookup"><span data-stu-id="8f9e4-156">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="8f9e4-157">NuGet vérifiera automatiquement la propriété TPMinV du projet de consommation et l’installation échouera si cette valeur est inférieure à Windows 10 Édition anniversaire (10.0; Build 14393)</span><span class="sxs-lookup"><span data-stu-id="8f9e4-157">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="8f9e4-158">Avec WPF, supposons que vous souhaitez que votre package de contrôles WPF soit consommé par les projets ciblant .NET Framework 4.6.1 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-158">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="8f9e4-159">Pour appliquer cette procédure, vous devez empaqueter vos contrôles avec les noms de dossiers suivants :</span><span class="sxs-lookup"><span data-stu-id="8f9e4-159">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="8f9e4-160">Ajouter la prise en charge au moment de la conception</span><span class="sxs-lookup"><span data-stu-id="8f9e4-160">Add design-time support</span></span>

<span data-ttu-id="8f9e4-161">Pour configurer où les propriétés de contrôle apparaissent dans l’inspecteur de propriétés, ajouter des ornements, etc., puis placez votre fichier `design.dll` dans le dossier `lib\uap10.0.14393\Design` en fonction de la plateforme cible.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-161">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="8f9e4-162">De plus, pour que la fonctionnalité **[Modifier le modèle > Modifier une copie](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** soit opérationnelle, vous devez inclure le fichier `Generic.xaml` et tous les dictionnaires de ressources qu’il fusionne dans le dossier `<your_assembly_name>\Themes` (là encore, en utilisant le nom de votre assembly).</span><span class="sxs-lookup"><span data-stu-id="8f9e4-162">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="8f9e4-163">(Ce fichier n’a aucun impact sur le comportement d’exécution d’un contrôle.) La structure de dossiers devrait donc apparaître comme suit :</span><span class="sxs-lookup"><span data-stu-id="8f9e4-163">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="8f9e4-164">Pour WPF, poursuivez avec l’exemple dans lequel vous souhaitez que votre package de contrôles WPF soit consommé par les projets ciblant .NET Framework 4.6.1 ou une version ultérieure :</span><span class="sxs-lookup"><span data-stu-id="8f9e4-164">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="8f9e4-165">Par défaut, les propriétés des contrôles apparaissent sous la catégorie Divers dans l’inspecteur de propriété.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-165">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="8f9e4-166">Utilisez des chaînes et des ressources</span><span class="sxs-lookup"><span data-stu-id="8f9e4-166">Use strings and resources</span></span>

<span data-ttu-id="8f9e4-167">Vous pouvez incorporer des ressources de type chaîne (`.resw`) dans votre package qui peuvent être utilisées par votre contrôle ou le projet UWP de consommation ; pour ce faire, définissez la propriété **Action de génération** du fichier `.resw` sur **PRIResource** .</span><span class="sxs-lookup"><span data-stu-id="8f9e4-167">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource** .</span></span>

<span data-ttu-id="8f9e4-168">Pour obtenir un exemple, reportez-vous à [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) dans l’exemple ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-168">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="8f9e4-169">Cette procédure s’applique uniquement aux contrôles UWP.</span><span class="sxs-lookup"><span data-stu-id="8f9e4-169">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="8f9e4-170">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8f9e4-170">See also</span></span>

- [<span data-ttu-id="8f9e4-171">Créer des packages UWP</span><span class="sxs-lookup"><span data-stu-id="8f9e4-171">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="8f9e4-172">Exemple ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="8f9e4-172">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)