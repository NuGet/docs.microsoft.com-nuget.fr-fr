---
title: Guide pratique pour empaqueter des contrôles IU avec NuGet
description: Comment créer des packages NuGet qui contiennent des contrôles UWP ou WPF, y compris les métadonnées nécessaires et les fichiers de prise en charge pour les concepteurs Visual Studio et Blend.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: fc6ab9e45d18807a6d69bb50ad5bac94b662a638
ms.sourcegitcommit: 80c1a37d8794e9219e310a21a6a6885a65d24e53
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2018
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="3cd72-103">Créer des contrôles IU en tant que packages NuGet</span><span class="sxs-lookup"><span data-stu-id="3cd72-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="3cd72-104">Avec Visual Studio 2017, vous pouvez tirer parti de fonctionnalités qui ont été ajoutées pour les contrôles UWP et WPF que vous mettez à disposition dans les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="3cd72-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="3cd72-105">Ce guide présente ces fonctionnalités dans le contexte des contrôles UWP au moyen de [l’exemple ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="3cd72-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="3cd72-106">Sauf indication contraire, la même procédure s’applique aux contrôles WPF.</span><span class="sxs-lookup"><span data-stu-id="3cd72-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cd72-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="3cd72-107">Prerequisites</span></span>

1. <span data-ttu-id="3cd72-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3cd72-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="3cd72-109">Savoir [créer des packages UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="3cd72-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="3cd72-110">Générer la disposition de la bibliothèque</span><span class="sxs-lookup"><span data-stu-id="3cd72-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="3cd72-111">Cette procédure s’applique uniquement aux contrôles UWP.</span><span class="sxs-lookup"><span data-stu-id="3cd72-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="3cd72-112">La définition de la propriété `GenerateLibraryLayout` garantit la sortie de build du projet dans une disposition prête à être empaquetée, sans recourir à des entrées de fichiers individuels dans le fichier nuspec.</span><span class="sxs-lookup"><span data-stu-id="3cd72-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="3cd72-113">Dans les propriétés du projet, accédez à l’onglet Build, puis cochez la case « Générer la disposition de la bibliothèque ».</span><span class="sxs-lookup"><span data-stu-id="3cd72-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="3cd72-114">Cette option va modifier le fichier projet et définir l’indicateur `GenerateLibraryLayout` sur true pour votre configuration de build et plateforme actuellement sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="3cd72-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="3cd72-115">Vous pouvez également modifier le fichier projet pour ajouter `<GenerateLibraryLayout>true</GenerateLibraryLayout>` au premier groupe de propriétés inconditionnelles.</span><span class="sxs-lookup"><span data-stu-id="3cd72-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="3cd72-116">Cette opération applique la propriété, quelles que soient la plateforme et la configuration de build.</span><span class="sxs-lookup"><span data-stu-id="3cd72-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="3cd72-117">Ajouter la prise en charge de la boîte à outils/du volet Composants pour les contrôles XAML</span><span class="sxs-lookup"><span data-stu-id="3cd72-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="3cd72-118">Pour qu’un contrôle XAML apparaisse dans la boîte à outils du concepteur XAML de Visual Studio et dans le volet Composants de Blend, créez un fichier `VisualStudioToolsManifest.xml` dans la racine du dossier `tools` de votre projet de package.</span><span class="sxs-lookup"><span data-stu-id="3cd72-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="3cd72-119">Ce fichier n’est pas requis si vous n’avez pas besoin que le contrôle apparaisse dans la boîte à outils ou le volet Composants.</span><span class="sxs-lookup"><span data-stu-id="3cd72-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="3cd72-120">La structure du fichier est la suivante :</span><span class="sxs-lookup"><span data-stu-id="3cd72-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="3cd72-121">où :</span><span class="sxs-lookup"><span data-stu-id="3cd72-121">where:</span></span>

- <span data-ttu-id="3cd72-122">*your_package_file* : nom de votre fichier de contrôle, tel que `ManagedPackage.winmd` (« ManagedPackage » est un nom arbitraire utilisé pour cet exemple et n’a aucune signification).</span><span class="sxs-lookup"><span data-stu-id="3cd72-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="3cd72-123">*vs_category* : étiquette du groupe dans lequel le contrôle doit apparaître dans la boîte à outils du concepteur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3cd72-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="3cd72-124">Un `VSCategory` est nécessaire pour que le contrôle apparaisse dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="3cd72-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="3cd72-125">*blend_category* : étiquette du groupe dans lequel le contrôle doit apparaître dans le volet Composants du concepteur Blend.</span><span class="sxs-lookup"><span data-stu-id="3cd72-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="3cd72-126">Un `BlendCategory` est nécessaire pour que le contrôle apparaisse dans le volet Composants.</span><span class="sxs-lookup"><span data-stu-id="3cd72-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="3cd72-127">*type_full_name_n* : nom complet de chaque contrôle, espace de noms compris, tel que `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="3cd72-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="3cd72-128">Notez que le format avec un point est utilisé pour les types managés et natifs.</span><span class="sxs-lookup"><span data-stu-id="3cd72-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="3cd72-129">Dans les scénarios plus avancés, vous pouvez également inclure plusieurs éléments `<File>` dans `<FileList>` quand un package unique contient plusieurs assemblys.</span><span class="sxs-lookup"><span data-stu-id="3cd72-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="3cd72-130">Vous pouvez également avoir plusieurs nœuds `<ToolboxItems>` dans un seul `<File>` si vous souhaitez organiser vos contrôles en catégories distinctes.</span><span class="sxs-lookup"><span data-stu-id="3cd72-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="3cd72-131">Dans l’exemple suivant, le contrôle implémenté dans `ManagedPackage.winmd` s’affiche dans Visual Studio et Blend dans un groupe appelé « Managed Package », tandis que « MyCustomControl » s’affiche dans ce groupe.</span><span class="sxs-lookup"><span data-stu-id="3cd72-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="3cd72-132">Tous ces noms sont arbitraires.</span><span class="sxs-lookup"><span data-stu-id="3cd72-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="3cd72-135">Vous devez spécifier explicitement chaque contrôle que vous aimeriez voir dans la boîte à outils ou le volet Composants.</span><span class="sxs-lookup"><span data-stu-id="3cd72-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="3cd72-136">Vérifiez que vous les spécifiez en utilisant le format `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="3cd72-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="3cd72-137">Ajouter des icônes personnalisées à vos contrôles</span><span class="sxs-lookup"><span data-stu-id="3cd72-137">Add custom icons to your controls</span></span>

<span data-ttu-id="3cd72-138">Pour afficher une icône personnalisée dans la boîte à outils ou le volet Composants, ajoutez une image à votre projet ou au projet `design.dll` correspondant portant le nom « Namespace.ControlName.extension » et définissez l’action de génération sur « Ressource incorporée ».</span><span class="sxs-lookup"><span data-stu-id="3cd72-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="3cd72-139">Les formats pris en charge sont `.png`, `.jpg`, `.jpeg`, `.gif` et `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="3cd72-139">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="3cd72-140">La taille d’image recommandée est 64 pixels par 64 pixels.</span><span class="sxs-lookup"><span data-stu-id="3cd72-140">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="3cd72-141">Dans l’exemple ci-dessous, le projet contient un fichier image nommé « ManagedPackage.MyCustomControl.png ».</span><span class="sxs-lookup"><span data-stu-id="3cd72-141">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Définition d’une icône personnalisée dans un projet](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="3cd72-143">Pour les contrôles natifs, vous devez placer l’icône en tant que ressource dans le projet `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="3cd72-143">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="3cd72-144">Prendre en charge des versions de plateformes Windows spécifiques</span><span class="sxs-lookup"><span data-stu-id="3cd72-144">Support specific Windows platform versions</span></span>

<span data-ttu-id="3cd72-145">Les packages UWP ont une propriété TargetPlatformVersion (TPV) et une propriété TargetPlatformMinVersion (TPMinV) qui définissent les limites supérieure et inférieure de la version de système d’exploitation sur laquelle l’application peut être installée.</span><span class="sxs-lookup"><span data-stu-id="3cd72-145">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="3cd72-146">La propriété TPV spécifie en outre la version du SDK par rapport auquel l’application est générée.</span><span class="sxs-lookup"><span data-stu-id="3cd72-146">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="3cd72-147">Tenez compte de ces propriétés quand vous créez un package UWP : l’utilisation d’API en dehors des limites des versions de plateforme définies dans l’application entraîne l’échec de la génération ou l’échec de l’application au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="3cd72-147">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="3cd72-148">Par exemple, supposons que vous avez défini la propriété TPMinV de votre package de contrôles sur Windows 10 Édition anniversaire (10.0 ; Build 14393), afin que le package soit consommé uniquement par les projets UWP qui correspondent à cette limite inférieure.</span><span class="sxs-lookup"><span data-stu-id="3cd72-148">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="3cd72-149">Pour que le package puisse être utilisé par des projets UWP, les contrôles doivent être empaquetés avec les noms de dossiers suivants :</span><span class="sxs-lookup"><span data-stu-id="3cd72-149">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="3cd72-150">NuGet vérifiera automatiquement la propriété TPMinV du projet de consommation et l’installation échouera si cette valeur est inférieure à Windows 10 Édition anniversaire (10.0; Build 14393)</span><span class="sxs-lookup"><span data-stu-id="3cd72-150">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="3cd72-151">Avec WPF, supposons que vous souhaitez que votre package de contrôles WPF soit consommé par les projets ciblant .NET Framework 4.6.1 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3cd72-151">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="3cd72-152">Pour appliquer cette procédure, vous devez empaqueter vos contrôles avec les noms de dossiers suivants :</span><span class="sxs-lookup"><span data-stu-id="3cd72-152">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="3cd72-153">Ajouter la prise en charge au moment de la conception</span><span class="sxs-lookup"><span data-stu-id="3cd72-153">Add design-time support</span></span>

<span data-ttu-id="3cd72-154">Pour configurer où les propriétés de contrôle apparaissent dans l’inspecteur de propriétés, ajouter des ornements, etc., puis placez votre fichier `design.dll` dans le dossier `lib\uap10.0.14393\Design` en fonction de la plateforme cible.</span><span class="sxs-lookup"><span data-stu-id="3cd72-154">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="3cd72-155">De plus, pour que la fonctionnalité **[Modifier le modèle > Modifier une copie](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** soit opérationnelle, vous devez inclure le fichier `Generic.xaml` et tous les dictionnaires de ressources qu’il fusionne dans le dossier `<your_assembly_name>\Themes` (là encore, en utilisant le nom de votre assembly).</span><span class="sxs-lookup"><span data-stu-id="3cd72-155">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="3cd72-156">(Ce fichier n’a aucun impact sur le comportement d’un contrôle au moment de l’exécution.) La structure de dossiers apparaît donc comme ceci :</span><span class="sxs-lookup"><span data-stu-id="3cd72-156">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="3cd72-157">Pour WPF, poursuivez avec l’exemple dans lequel vous souhaitez que votre package de contrôles WPF soit consommé par les projets ciblant .NET Framework 4.6.1 ou une version ultérieure :</span><span class="sxs-lookup"><span data-stu-id="3cd72-157">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="3cd72-158">Par défaut, les propriétés des contrôles apparaissent sous la catégorie Divers dans l’inspecteur de propriété.</span><span class="sxs-lookup"><span data-stu-id="3cd72-158">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="3cd72-159">Utilisez des chaînes et des ressources</span><span class="sxs-lookup"><span data-stu-id="3cd72-159">Use strings and resources</span></span>

<span data-ttu-id="3cd72-160">Vous pouvez incorporer des ressources de type chaîne (`.resw`) dans votre package qui peuvent être utilisées par votre contrôle ou le projet UWP de consommation ; pour ce faire, définissez la propriété **Action de génération** du fichier `.resw` sur **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="3cd72-160">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="3cd72-161">Pour obtenir un exemple, reportez-vous à [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) dans l’exemple ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="3cd72-161">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="3cd72-162">Cette procédure s’applique uniquement aux contrôles UWP.</span><span class="sxs-lookup"><span data-stu-id="3cd72-162">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="3cd72-163">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3cd72-163">See also</span></span>

- [<span data-ttu-id="3cd72-164">Créer des packages UWP</span><span class="sxs-lookup"><span data-stu-id="3cd72-164">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="3cd72-165">Exemple ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="3cd72-165">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
