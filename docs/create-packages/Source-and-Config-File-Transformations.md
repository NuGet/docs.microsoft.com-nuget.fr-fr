---
title: Transformations de fichiers sources et de configuration pour les packages NuGet
description: Informations sur la possibilité pour les packages NuGet de transformer des fichiers de code source et de configuration (XML) à l’installation.
author: JonDouglas
ms.author: jodou
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 76c589b5ad034127675fb2bbf79ea97992883ebe
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859107"
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="6e3f9-103">Transformation de fichiers de code source et de configuration</span><span class="sxs-lookup"><span data-stu-id="6e3f9-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="6e3f9-104">Une **transformation de code source** applique un remplacement unilatéral des jetons aux fichiers inclus dans le dossier `content` ou `contentFiles` (`content` pour les clients utilisant `packages.config` et `contentFiles` pour `PackageReference`) au moment où le package est installé, où les jetons font référence aux [propriétés de projet](/dotnet/api/vslangproj.projectproperties) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties).</span></span> <span data-ttu-id="6e3f9-105">Ainsi, vous pouvez insérer un fichier dans l’espace de noms du projet, ou bien personnaliser du code qui irait normalement dans `global.asax` dans un projet ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="6e3f9-106">Une **transformation de fichier de configuration** vous permet de modifier des fichiers qui existent déjà dans un projet cible, comme `web.config` et `app.config`.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="6e3f9-107">Par exemple, votre package peut avoir besoin d’ajouter un élément à la section `modules` dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="6e3f9-108">Cette transformation est effectuée en incluant des fichiers spéciaux dans le package qui décrivent les sections à ajouter aux fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="6e3f9-109">Lorsqu’un package est désinstallé, ces mêmes modifications sont alors annulées, ce qui en fait une transformation bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="6e3f9-110">Spécification de transformations de code source</span><span class="sxs-lookup"><span data-stu-id="6e3f9-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="6e3f9-111">Les fichiers que vous voulez insérer à partir du package dans le projet doivent se trouver dans les dossiers `content` et `contentFiles` du package.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="6e3f9-112">Par exemple, si vous voulez installer un fichier appelé `ContosoData.cs` dans un dossier `Models` du projet cible, il doit se trouver à l’intérieur des dossiers `content\Models` et `contentFiles\{lang}\{tfm}\Models` dans le package.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="6e3f9-113">Pour demander à NuGet d’appliquer un remplacement des jetons au moment de l’installation, ajoutez `.pp` au nom du fichier de code source.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="6e3f9-114">Après l’installation, le fichier ne porte pas l’extension `.pp`.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="6e3f9-115">Par exemple, pour effectuer des transformations dans `ContosoData.cs`, nommez le fichier dans le package `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="6e3f9-116">Après l’installation, il s’affiche en tant que `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="6e3f9-117">Dans le fichier de code source, utilisez des jetons ne respectant pas la casse sous la forme `$token$` pour indiquer les valeurs que NuGet doit remplacer par les propriétés de projet :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="6e3f9-118">Lors de l’installation, NuGet remplace `$rootnamespace$` par `Fabrikam` en supposant que le projet cible a pour espace de noms racine `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="6e3f9-119">Le jeton `$rootnamespace$` est la propriété de projet la plus souvent utilisée ; toutes les autres sont listés dans la documentation sur les [propriétés de projet](/dotnet/api/vslangproj.projectproperties).</span><span class="sxs-lookup"><span data-stu-id="6e3f9-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties).</span></span> <span data-ttu-id="6e3f9-120">N’oubliez pas, évidemment, que certaines propriétés peuvent être spécifiques du type de projet.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="6e3f9-121">Spécification de transformations de fichiers de configuration</span><span class="sxs-lookup"><span data-stu-id="6e3f9-121">Specifying config file transformations</span></span>

<span data-ttu-id="6e3f9-122">Comme décrit dans les sections qui suivent, les transformations de fichiers de configuration peuvent être effectuées de deux manières :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="6e3f9-123">Incluez des fichiers `app.config.transform` et `web.config.transform` dans le dossier `content` de votre package, où l’extension `.transform` indique à NuGet que ces fichiers contiennent le code XML à fusionner avec les fichiers de configuration existants lors de l’installation du package.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="6e3f9-124">Lorsqu’un package est désinstallé, ce même code XML est supprimé.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="6e3f9-125">Incluez les fichiers `app.config.install.xdt` et `web.config.install.xdt` dans le dossier `content` de votre package en utilisant la [syntaxe XDT](/previous-versions/aspnet/dd465326(v=vs.110)) pour décrire les changements souhaités.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](/previous-versions/aspnet/dd465326(v=vs.110)) to describe the desired changes.</span></span> <span data-ttu-id="6e3f9-126">Avec cette option, vous pouvez également inclure un fichier `.uninstall.xdt` pour annuler ces modifications lorsque le package est supprimé d’un projet.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="6e3f9-127">Les transformations ne sont pas appliquées aux fichiers `.config` référencés sous forme de lien dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="6e3f9-128">L’avantage d’utiliser la syntaxe XDT est qu’au lieu de simplement fusionner deux fichiers statiques, elle permet de manipuler la structure d’un DOM XML en faisant correspondre éléments et attributs à l’aide d’une prise en charge XPath complète.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="6e3f9-129">La syntaxe XDT permet alors d’ajouter, de mettre à jour ou de supprimer des éléments, de placer de nouveaux éléments à un emplacement spécifique ou de remplacer/supprimer des éléments (y compris des nœuds enfants).</span><span class="sxs-lookup"><span data-stu-id="6e3f9-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="6e3f9-130">La création de transformations de désinstallation qui reviennent sur toutes les transformations effectuées pendant l’installation du package est ainsi facilitée.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="6e3f9-131">Transformations XML</span><span class="sxs-lookup"><span data-stu-id="6e3f9-131">XML transforms</span></span>

<span data-ttu-id="6e3f9-132">Les fichiers `app.config.transform` et `web.config.transform` du dossier `content` d’un package contiennent uniquement les éléments à fusionner dans les fichiers `app.config` et `web.config` existants du projet.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="6e3f9-133">Par exemple, supposons que le projet contienne initialement ce qui suit dans `web.config` :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6e3f9-134">Pour ajouter un élément `MyNuModule` à la section `modules` lors de l’installation d’un package, créez un fichier `web.config.transform` dans le dossier `content` du package qui ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6e3f9-135">Une fois que NuGet a installé le package, `web.config` apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="6e3f9-136">Notez que NuGet n’a pas remplacé la section `modules`, mais y a simplement fusionné la nouvelle entrée en ajoutant uniquement de nouveaux éléments et attributs.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="6e3f9-137">NuGet ne modifie pas les éléments ou attributs existants.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="6e3f9-138">Lorsque le package est désinstallé, NuGet réexamine les fichiers `.transform` et supprime les éléments qu’ils contiennent provenant des fichiers `.config` appropriés.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="6e3f9-139">Notez que ce processus n’affecte pas les lignes du fichier `.config` que vous modifiez après l’installation du package.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="6e3f9-140">Comme un exemple plus complet, le package [Gestionnaires et modules d’enregistrement des erreurs (ELMAH) pour ASP.NET](https://www.nuget.org/packages/elmah/) ajoute de nombreuses entrées dans `web.config`, qui sont de nouveau supprimées lors de la désinstallation d’un package.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="6e3f9-141">Pour examiner son fichier `web.config.transform`, téléchargez le package ELMAH à partir du lien ci-dessus, remplacez l’extension du package `.nupkg` par `.zip`, puis ouvrez `content\web.config.transform` dans ce fichier ZIP.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="6e3f9-142">Pour voir l’effet de l’installation et de la désinstallation du package, créez un projet ASP.NET dans Visual Studio (le modèle est disponible sous **Visual C# > Web** dans la boîte de dialogue Nouveau projet), puis sélectionnez une application ASP.NET vide.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="6e3f9-143">Ouvrez `web.config` pour voir son état initial.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="6e3f9-144">Ensuite, cliquez sur le projet, sélectionnez **Gérer les packages NuGet**, recherchez ELMAH sur nuget.org et installez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="6e3f9-145">Remarquez toutes les modifications apportées à `web.config`.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="6e3f9-146">Désinstallez maintenant le package : `web.config` reviendra à son état antérieur.</span><span class="sxs-lookup"><span data-stu-id="6e3f9-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="6e3f9-147">Transformations XDT</span><span class="sxs-lookup"><span data-stu-id="6e3f9-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="6e3f9-148">Comme indiqué dans la [section problèmes de compatibilité de package de la documentation relative à la migration de `packages.config` vers `PackageReference` ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), les transformations xdt, comme décrit ci-dessous, sont prises en charge uniquement par `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="6e3f9-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="6e3f9-149">Si vous ajoutez les fichiers ci-dessous à votre package, les transformations ne sont pas appliquées aux consommateurs qui utilisent votre package, `PackageReference` (reportez-vous à [cet exemple](https://github.com/NuGet/Samples/tree/main/XDTransformExample) pour faire en sorte que les transformations xdt fonctionnent avec `PackageReference` ).</span><span class="sxs-lookup"><span data-stu-id="6e3f9-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/main/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="6e3f9-150">Vous pouvez modifier des fichiers de configuration en utilisant la [syntaxe XDT](/previous-versions/aspnet/dd465326(v=vs.110)).</span><span class="sxs-lookup"><span data-stu-id="6e3f9-150">You can modify config files using [XDT syntax](/previous-versions/aspnet/dd465326(v=vs.110)).</span></span> <span data-ttu-id="6e3f9-151">Vous pouvez également demander à NuGet de remplacer les jetons par des [propriétés de projet](/dotnet/api/vslangproj.projectproperties) en plaçant leur nom entre les délimiteurs `$` (sans respect de la casse).</span><span class="sxs-lookup"><span data-stu-id="6e3f9-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="6e3f9-152">Par exemple, le fichier `app.config.install.xdt` suivant insère un élément `appSettings` dans `app.config` qui contient les valeurs `FullPath`, `FileName` et `ActiveConfigurationSettings` du projet :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="6e3f9-153">Autre exemple, supposons que le projet contienne initialement ce qui suit dans `web.config` :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6e3f9-154">Pour ajouter un élément `MyNuModule` à la section `modules` pendant l’installation du package, le fichier `web.config.install.xdt` du package doit contenir ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="6e3f9-155">Après avoir installé le package, `web.config` ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="6e3f9-156">Pour supprimer uniquement l’élément `MyNuModule` pendant la désinstallation du package, le fichier `web.config.uninstall.xdt` doit contenir ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="6e3f9-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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