---
title: Transformations de fichiers sources et de configuration pour les packages NuGet
description: Informations sur la possibilité pour les packages NuGet de transformer des fichiers de code source et de configuration (XML) à l’installation.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 863bf22780313a34690617dd6a1604531272808b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="e186c-103">Transformation de fichiers de code source et de configuration</span><span class="sxs-lookup"><span data-stu-id="e186c-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="e186c-104">Pour les projets utilisant `packages.config`, NuGet offre la possibilité d’effectuer des transformations sur les fichiers de code source et de configuration au moment de l’installation et de la désinstallation des packages.</span><span class="sxs-lookup"><span data-stu-id="e186c-104">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="e186c-105">Seules les transformations du code source sont appliquées en cas d’installation d’un package dans un projet avec [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="e186c-105">Only Source code transformations are applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="e186c-106">Une **transformation de code source** applique un remplacement unilatéral des jetons aux fichiers inclus dans le dossier `content` ou `contentFiles` (`content` pour les clients utilisant `packages.config` et `contentFiles` pour `PackageReference`) au moment où le package est installé, où les jetons font référence aux [propriétés de projet](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e186c-106">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="e186c-107">Ainsi, vous pouvez insérer un fichier dans l’espace de noms du projet, ou bien personnaliser du code qui irait normalement dans `global.asax` dans un projet ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e186c-107">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="e186c-108">Une **transformation de fichier de configuration** vous permet de modifier des fichiers qui existent déjà dans un projet cible, comme `web.config` et `app.config`.</span><span class="sxs-lookup"><span data-stu-id="e186c-108">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="e186c-109">Par exemple, votre package peut avoir besoin d’ajouter un élément à la section `modules` dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="e186c-109">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="e186c-110">Cette transformation est effectuée en incluant des fichiers spéciaux dans le package qui décrivent les sections à ajouter aux fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="e186c-110">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="e186c-111">Lorsqu’un package est désinstallé, ces mêmes modifications sont alors annulées, ce qui en fait une transformation bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="e186c-111">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="e186c-112">Spécification de transformations de code source</span><span class="sxs-lookup"><span data-stu-id="e186c-112">Specifying source code transformations</span></span>

1. <span data-ttu-id="e186c-113">Les fichiers que vous voulez insérer à partir du package dans le projet doivent se trouver dans les dossiers `content` et `contentFiles` du package.</span><span class="sxs-lookup"><span data-stu-id="e186c-113">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="e186c-114">Par exemple, si vous voulez installer un fichier appelé `ContosoData.cs` dans un dossier `Models` du projet cible, il doit se trouver à l’intérieur des dossiers `content\Models` et `contentFiles\{lang}\{tfm}\Models` dans le package.</span><span class="sxs-lookup"><span data-stu-id="e186c-114">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="e186c-115">Pour demander à NuGet d’appliquer un remplacement des jetons au moment de l’installation, ajoutez `.pp` au nom du fichier de code source.</span><span class="sxs-lookup"><span data-stu-id="e186c-115">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="e186c-116">Après l’installation, le fichier ne porte pas l’extension `.pp`.</span><span class="sxs-lookup"><span data-stu-id="e186c-116">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="e186c-117">Par exemple, pour effectuer des transformations dans `ContosoData.cs`, nommez le fichier dans le package `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="e186c-117">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="e186c-118">Après l’installation, il s’affiche en tant que `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="e186c-118">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="e186c-119">Dans le fichier de code source, utilisez des jetons ne respectant pas la casse sous la forme `$token$` pour indiquer les valeurs que NuGet doit remplacer par les propriétés de projet :</span><span class="sxs-lookup"><span data-stu-id="e186c-119">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    <span data-ttu-id="e186c-120">Lors de l’installation, NuGet remplace `$rootnamespace$` par `Fabrikam` en supposant que le projet cible a pour espace de noms racine `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="e186c-120">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="e186c-121">Le jeton `$rootnamespace$` est la propriété de projet la plus souvent utilisée ; toutes les autres sont listés dans la documentation sur les [propriétés de projet](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="e186c-121">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="e186c-122">N’oubliez pas, évidemment, que certaines propriétés peuvent être spécifiques du type de projet.</span><span class="sxs-lookup"><span data-stu-id="e186c-122">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="e186c-123">Spécification de transformations de fichiers de configuration</span><span class="sxs-lookup"><span data-stu-id="e186c-123">Specifying config file transformations</span></span>

<span data-ttu-id="e186c-124">Comme décrit dans les sections qui suivent, les transformations de fichiers de configuration peuvent être effectuées de deux manières :</span><span class="sxs-lookup"><span data-stu-id="e186c-124">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="e186c-125">Incluez des fichiers `app.config.transform` et `web.config.transform` dans le dossier `content` de votre package, où l’extension `.transform` indique à NuGet que ces fichiers contiennent le code XML à fusionner avec les fichiers de configuration existants lors de l’installation du package.</span><span class="sxs-lookup"><span data-stu-id="e186c-125">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="e186c-126">Lorsqu’un package est désinstallé, ce même code XML est supprimé.</span><span class="sxs-lookup"><span data-stu-id="e186c-126">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="e186c-127">Incluez les fichiers `app.config.install.xdt` et `web.config.install.xdt` dans le dossier `content` de votre package en utilisant la [syntaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx) pour décrire les changements souhaités.</span><span class="sxs-lookup"><span data-stu-id="e186c-127">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="e186c-128">Avec cette option, vous pouvez également inclure un fichier `.uninstall.xdt` pour annuler ces modifications lorsque le package est supprimé d’un projet.</span><span class="sxs-lookup"><span data-stu-id="e186c-128">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="e186c-129">Les transformations ne sont pas appliquées aux fichiers `.config` référencés sous forme de lien dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e186c-129">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="e186c-130">L’avantage d’utiliser la syntaxe XDT est qu’au lieu de simplement fusionner deux fichiers statiques, elle permet de manipuler la structure d’un DOM XML en faisant correspondre éléments et attributs à l’aide d’une prise en charge XPath complète.</span><span class="sxs-lookup"><span data-stu-id="e186c-130">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="e186c-131">La syntaxe XDT permet alors d’ajouter, de mettre à jour ou de supprimer des éléments, de placer de nouveaux éléments à un emplacement spécifique ou de remplacer/supprimer des éléments (y compris des nœuds enfants).</span><span class="sxs-lookup"><span data-stu-id="e186c-131">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="e186c-132">La création de transformations de désinstallation qui reviennent sur toutes les transformations effectuées pendant l’installation du package est ainsi facilitée.</span><span class="sxs-lookup"><span data-stu-id="e186c-132">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="e186c-133">Transformations XML</span><span class="sxs-lookup"><span data-stu-id="e186c-133">XML transforms</span></span>

<span data-ttu-id="e186c-134">Les fichiers `app.config.transform` et `web.config.transform` du dossier `content` d’un package contiennent uniquement les éléments à fusionner dans les fichiers `app.config` et `web.config` existants du projet.</span><span class="sxs-lookup"><span data-stu-id="e186c-134">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="e186c-135">Par exemple, supposons que le projet contienne initialement ce qui suit dans `web.config` :</span><span class="sxs-lookup"><span data-stu-id="e186c-135">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="e186c-136">Pour ajouter un élément `MyNuModule` à la section `modules` lors de l’installation d’un package, créez un fichier `web.config.transform` dans le dossier `content` du package qui ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="e186c-136">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="e186c-137">Une fois que NuGet a installé le package, `web.config` apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="e186c-137">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="e186c-138">Notez que NuGet n’a pas remplacé la section `modules`, mais y a simplement fusionné la nouvelle entrée en ajoutant uniquement de nouveaux éléments et attributs.</span><span class="sxs-lookup"><span data-stu-id="e186c-138">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="e186c-139">NuGet ne modifie pas les éléments ou attributs existants.</span><span class="sxs-lookup"><span data-stu-id="e186c-139">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="e186c-140">Lorsque le package est désinstallé, NuGet réexamine les fichiers `.transform` et supprime les éléments qu’ils contiennent provenant des fichiers `.config` appropriés.</span><span class="sxs-lookup"><span data-stu-id="e186c-140">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="e186c-141">Notez que ce processus n’affecte pas les lignes du fichier `.config` que vous modifiez après l’installation du package.</span><span class="sxs-lookup"><span data-stu-id="e186c-141">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="e186c-142">Comme un exemple plus complet, le package [Gestionnaires et modules d’enregistrement des erreurs (ELMAH) pour ASP.NET](https://www.nuget.org/packages/elmah/) ajoute de nombreuses entrées dans `web.config`, qui sont de nouveau supprimées lors de la désinstallation d’un package.</span><span class="sxs-lookup"><span data-stu-id="e186c-142">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="e186c-143">Pour examiner son fichier `web.config.transform`, téléchargez le package ELMAH à partir du lien ci-dessus, remplacez l’extension du package `.nupkg` par `.zip`, puis ouvrez `content\web.config.transform` dans ce fichier ZIP.</span><span class="sxs-lookup"><span data-stu-id="e186c-143">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="e186c-144">Pour voir l’effet de l’installation et de la désinstallation du package, créez un projet ASP.NET dans Visual Studio (le modèle est disponible sous **Visual C# > Web** dans la boîte de dialogue Nouveau projet), puis sélectionnez une application ASP.NET vide.</span><span class="sxs-lookup"><span data-stu-id="e186c-144">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="e186c-145">Ouvrez `web.config` pour voir son état initial.</span><span class="sxs-lookup"><span data-stu-id="e186c-145">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="e186c-146">Ensuite, cliquez sur le projet, sélectionnez **Gérer les packages NuGet**, recherchez ELMAH sur nuget.org et installez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="e186c-146">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="e186c-147">Remarquez toutes les modifications apportées à `web.config`.</span><span class="sxs-lookup"><span data-stu-id="e186c-147">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="e186c-148">Désinstallez maintenant le package : `web.config` reviendra à son état antérieur.</span><span class="sxs-lookup"><span data-stu-id="e186c-148">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="e186c-149">Transformations XDT</span><span class="sxs-lookup"><span data-stu-id="e186c-149">XDT transforms</span></span>

<span data-ttu-id="e186c-150">Vous pouvez modifier des fichiers de configuration en utilisant la [syntaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="e186c-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="e186c-151">Vous pouvez également demander à NuGet de remplacer les jetons par des [propriétés de projet](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) en plaçant leur nom entre les délimiteurs `$` (sans respecter la casse).</span><span class="sxs-lookup"><span data-stu-id="e186c-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="e186c-152">Par exemple, le fichier `app.config.install.xdt` suivant insère un élément `appSettings` dans `app.config` qui contient les valeurs `FullPath`, `FileName` et `ActiveConfigurationSettings` du projet :</span><span class="sxs-lookup"><span data-stu-id="e186c-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

<span data-ttu-id="e186c-153">Autre exemple, supposons que le projet contienne initialement ce qui suit dans `web.config` :</span><span class="sxs-lookup"><span data-stu-id="e186c-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="e186c-154">Pour ajouter un élément `MyNuModule` à la section `modules` pendant l’installation du package, le fichier `web.config.install.xdt` du package doit contenir ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="e186c-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="e186c-155">Après avoir installé le package, `web.config` ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="e186c-155">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="e186c-156">Pour supprimer uniquement l’élément `MyNuModule` pendant la désinstallation du package, le fichier `web.config.uninstall.xdt` doit contenir ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="e186c-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
