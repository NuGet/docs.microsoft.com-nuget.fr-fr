---
title: Configuration du comportement de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Les fichiers NuGet.Config permettent de contrôler le comportement de NuGet pour l’ensemble des projets et pour chacun des projets. Pour modifier ces fichiers, utilisez la commande nuget config.
keywords: Fichiers config NuGet, configuration NuGet, paramètres de comportement de NuGet, paramètres NuGet, Nuget.Config, NuGetDefaults.Config, valeurs par défaut
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a575868894d5ca9992b1c9984cf4920bd2858209
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="afc9a-104">Configuration du comportement de NuGet</span><span class="sxs-lookup"><span data-stu-id="afc9a-104">Configuring NuGet behavior</span></span>

<span data-ttu-id="afc9a-105">Le comportement de NuGet est contrôlé par les paramètres qui sont définis dans un ou plusieurs fichiers `NuGet.Config` (XML) qui peuvent exister au niveau du projet, de l’utilisateur ou de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="afc9a-105">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="afc9a-106">Un fichier `NuGetDefaults.Config` global configure également les sources de package.</span><span class="sxs-lookup"><span data-stu-id="afc9a-106">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="afc9a-107">Les paramètres s’appliquent à toutes les commandes émises dans l’interface CLI, la console du gestionnaire de package et l’interface utilisateur du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="afc9a-107">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="afc9a-108">Emplacements et utilisations des fichiers config</span><span class="sxs-lookup"><span data-stu-id="afc9a-108">Config file locations and uses</span></span>

| <span data-ttu-id="afc9a-109">Portée</span><span class="sxs-lookup"><span data-stu-id="afc9a-109">Scope</span></span> | <span data-ttu-id="afc9a-110">Emplacement du fichier NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="afc9a-110">NuGet.Config file location</span></span> | <span data-ttu-id="afc9a-111">Description</span><span class="sxs-lookup"><span data-stu-id="afc9a-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="afc9a-112">Projet</span><span class="sxs-lookup"><span data-stu-id="afc9a-112">Project</span></span> | <span data-ttu-id="afc9a-113">Dossier actuel (dossier du projet) ou tout dossier pouvant être situé jusqu’à la racine du lecteur.</span><span class="sxs-lookup"><span data-stu-id="afc9a-113">Current folder (aka Project folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="afc9a-114">Dans un dossier de projet, les paramètres s’appliquent uniquement au projet en question.</span><span class="sxs-lookup"><span data-stu-id="afc9a-114">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="afc9a-115">Dans les dossiers parents qui contiennent plusieurs dossiers de projets, les paramètres s’appliquent à tous les projets des sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="afc9a-115">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="afc9a-116">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="afc9a-116">User</span></span> | <span data-ttu-id="afc9a-117">Windows : `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="afc9a-117">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="afc9a-118">Mac/Linux : `~/.nuget/NuGet/NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="afc9a-118">Mac/Linux: `~/.nuget/NuGet/NuGet.Config`</span></span> | <span data-ttu-id="afc9a-119">Les paramètres s’appliquent à toutes les opérations. Toutefois, ils sont substitués par tout paramètre défini au niveau du projet.</span><span class="sxs-lookup"><span data-stu-id="afc9a-119">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="afc9a-120">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="afc9a-120">Computer</span></span> | <span data-ttu-id="afc9a-121">Windows : `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="afc9a-121">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="afc9a-122">Mac/Linux : `$XDG_DATA_HOME` (en général, `~/.local/share`)</span><span class="sxs-lookup"><span data-stu-id="afc9a-122">Mac/Linux: `$XDG_DATA_HOME` (typically `~/.local/share`)</span></span> | <span data-ttu-id="afc9a-123">Les paramètres s’appliquent à toutes les opérations effectuées sur l’ordinateur. Toutefois, ils sont substitués par tout paramètre défini au niveau de l’utilisateur ou du projet.</span><span class="sxs-lookup"><span data-stu-id="afc9a-123">Settings apply to all operations on the computer, but are overriden by any user- or project-level settings.</span></span> |

<span data-ttu-id="afc9a-124">Remarques concernant les versions précédentes de NuGet :</span><span class="sxs-lookup"><span data-stu-id="afc9a-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="afc9a-125">NuGet 3.3 et versions antérieures utilisaient un dossier `.nuget` pour les paramètres définis au niveau de la solution.</span><span class="sxs-lookup"><span data-stu-id="afc9a-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="afc9a-126">Ce fichier n’est plus utilisé dans NuGet 3.4+.</span><span class="sxs-lookup"><span data-stu-id="afc9a-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="afc9a-127">Pour NuGet 2.6 3.x, le fichier config défini au niveau d’un ordinateur Windows était situé dans %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, où *{IDE}* pouvait correspondre à  *Visual Studio*, *{Version}* à la version de Visual Studio, comme *14.0*, et *{SKU}* à l’édition *Community*, *Pro* ou *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="afc9a-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="afc9a-128">Pour migrer les paramètres vers NuGet 4.0+, copiez simplement le fichier config vers %ProgramFiles(x86)%\NuGet\Config. Sur Linux, l’ancien emplacement était /etc/opt et sur Mac, Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="afc9a-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="afc9a-129">Modification des paramètres de configuration</span><span class="sxs-lookup"><span data-stu-id="afc9a-129">Changing config settings</span></span>

<span data-ttu-id="afc9a-130">Un fichier `NuGet.Config` est un simple fichier texte XML contenant des paires clé/valeur, comme décrit dans la rubrique [Paramètres de configuration NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="afc9a-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="afc9a-131">Les paramètres sont gérés à l’aide de la [commande config](../tools/cli-ref-config.md) de l’interface CLI de NuGet :</span><span class="sxs-lookup"><span data-stu-id="afc9a-131">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="afc9a-132">Par défaut, les modifications sont apportées au fichier config défini au niveau de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afc9a-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="afc9a-133">Pour modifier les paramètres dans un autre fichier, utilisez le commutateur `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="afc9a-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="afc9a-134">Dans ce cas, les fichiers peuvent utiliser n’importe quel nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="afc9a-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="afc9a-135">Les clés respectent toujours la casse.</span><span class="sxs-lookup"><span data-stu-id="afc9a-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="afc9a-136">Une élévation des privilèges est nécessaire pour modifier les paramètres du fichier de paramètres défini au niveau de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="afc9a-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="afc9a-137">Même si vous pouvez modifier le fichier dans n’importe quel éditeur de texte, NuGet (v3.4.3 et versions ultérieures) ignore silencieusement l’intégralité du fichier de configuration si celui-ci contient du code XML incorrectement formé (balises incompatibles, guillemets non valides, etc.).</span><span class="sxs-lookup"><span data-stu-id="afc9a-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="afc9a-138">C’est pourquoi il est préférable de gérer les paramètres à l’aide de `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="afc9a-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="afc9a-139">Définition d’une valeur</span><span class="sxs-lookup"><span data-stu-id="afc9a-139">Setting a value</span></span>

<span data-ttu-id="afc9a-140">Windows :</span><span class="sxs-lookup"><span data-stu-id="afc9a-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="afc9a-141">Mac/Linux :</span><span class="sxs-lookup"><span data-stu-id="afc9a-141">Mac/Linux:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="afc9a-142">Dans NuGet 3.4 et versions ultérieures, vous pouvez utiliser des variables d’environnement dans n’importe quelle valeur, comme dans `repositoryPath=%PACKAGEHOME%` (Windows) et `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="afc9a-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="afc9a-143">Suppression dune valeur</span><span class="sxs-lookup"><span data-stu-id="afc9a-143">Removing a value</span></span>

<span data-ttu-id="afc9a-144">Pour supprimer une valeur, spécifiez une clé avec une valeur vide.</span><span class="sxs-lookup"><span data-stu-id="afc9a-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="afc9a-145">Création d’un fichier config</span><span class="sxs-lookup"><span data-stu-id="afc9a-145">Creating a new config file</span></span>

<span data-ttu-id="afc9a-146">Copiez le modèle ci-dessous dans le nouveau fichier, puis utilisez `nuget config -configFile <filename>` pour définir les valeurs :</span><span class="sxs-lookup"><span data-stu-id="afc9a-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="afc9a-147">Application des paramètres</span><span class="sxs-lookup"><span data-stu-id="afc9a-147">How settings are applied</span></span>

<span data-ttu-id="afc9a-148">L’utilisation de plusieurs fichiers `NuGet.Config` permet de stocker des paramètres à différents emplacements, de manière à les appliquer à un projet, à un groupe de projets ou à l’ensemble des projets.</span><span class="sxs-lookup"><span data-stu-id="afc9a-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="afc9a-149">Ces paramètres s’appliquent collectivement à toute opération NuGet appelée à partir de la ligne de commande ou de Visual Studio. Les paramètres « les plus proches » d’un projet ou du dossier actif sont prioritaires.</span><span class="sxs-lookup"><span data-stu-id="afc9a-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="afc9a-150">Plus précisément, NuGet charge les paramètres à partir de plusieurs fichiers config dans l’ordre suivant :</span><span class="sxs-lookup"><span data-stu-id="afc9a-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="afc9a-151">Le [fichier NuGetDefaults.Config](#nuget-defaults-file), qui contient les paramètres concernant uniquement les sources de package.</span><span class="sxs-lookup"><span data-stu-id="afc9a-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="afc9a-152">Le fichier défini au niveau de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="afc9a-152">The computer-level file.</span></span>
1. <span data-ttu-id="afc9a-153">Le fichier défini au niveau de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afc9a-153">The user-level file.</span></span>
1. <span data-ttu-id="afc9a-154">Le fichier spécifié avec `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="afc9a-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="afc9a-155">Les fichiers qui se trouvent dans chacun des dossiers du chemin allant de la racine du lecteur au dossier actif (celui où nuget.exe est appelé ou le dossier qui contient le projet Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="afc9a-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="afc9a-156">Par exemple, si une commande est appelée dans c:\A\B\C, NuGet recherche et charge les fichiers config dans c:\,, puis c:\A, puis c:\A\B, et enfin, dans c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="afc9a-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="afc9a-157">Quand NuGet trouve les paramètres dans ces fichiers, il les applique de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="afc9a-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="afc9a-158">Pour les éléments uniques, NuGet remplaçait toute valeur précédemment trouvée pour la même clé.</span><span class="sxs-lookup"><span data-stu-id="afc9a-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="afc9a-159">Cela signifie que les paramètres qui sont « les plus proches » du dossier actif ou du projet remplacent les paramètres trouvés précédemment.</span><span class="sxs-lookup"><span data-stu-id="afc9a-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="afc9a-160">Par exemple, le paramètre `defaultPushSource` dans `NuGetDefaults.Config` est remplacé s’il se trouve également dans un autre fichier config.</span><span class="sxs-lookup"><span data-stu-id="afc9a-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="afc9a-161">Pour les éléments de collection (tels que `<packageSources>`), NuGet combine les valeurs de tous les fichiers de configuration dans une même collection.</span><span class="sxs-lookup"><span data-stu-id="afc9a-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="afc9a-162">Lorsque `<clear />` est présent pour un nœud donné, NuGet ignore les valeurs de configuration définies précédemment pour ce nœud.</span><span class="sxs-lookup"><span data-stu-id="afc9a-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="afc9a-163">Procédure pas à pas pour l’application des paramètres</span><span class="sxs-lookup"><span data-stu-id="afc9a-163">Settings walkthrough</span></span>

<span data-ttu-id="afc9a-164">Supposons que vous disposiez de la structure de dossiers suivante sur deux lecteurs distincts :</span><span class="sxs-lookup"><span data-stu-id="afc9a-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="afc9a-165">Vous avez donc quatre fichiers `NuGet.Config` aux emplacements suivants, avec le contenu spécifié</span><span class="sxs-lookup"><span data-stu-id="afc9a-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="afc9a-166">(le fichier défini au niveau de l’ordinateur n’est pas inclus dans cet exemple, toutefois, son comportent est similaire à celui du fichier défini au niveau de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="afc9a-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="afc9a-167">Fichier A. Fichier de niveau utilisateur (`%appdata%\NuGet\NuGet.Config` sur Windows, `~/.nuget/NuGet/NuGet.Config` sur Mac/Linux) :</span><span class="sxs-lookup"><span data-stu-id="afc9a-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="afc9a-168">Fichier B. disk_drive_2/NuGet.Config :</span><span class="sxs-lookup"><span data-stu-id="afc9a-168">File B. disk_drive_2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="afc9a-169">Fichier C. disk_drive_2/Project1/NuGet.Config :</span><span class="sxs-lookup"><span data-stu-id="afc9a-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="afc9a-170">Fichier D. disk_drive_2/Project2/NuGet.Config :</span><span class="sxs-lookup"><span data-stu-id="afc9a-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="afc9a-171">Ensuite, NuGet charge et applique les paramètres de la manière suivante, en fonction de l’emplacement où ils sont appelés :</span><span class="sxs-lookup"><span data-stu-id="afc9a-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="afc9a-172">**Appelés à partir de disk_drive_1/users** : seul le référentiel par défaut répertorié dans le fichier de configuration défini au niveau de l’utilisateur (A) est utilisé, car il s’agit du seul fichier trouvé à l’emplacement disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="afc9a-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="afc9a-173">**Appelés à partir de disk_drive_2/ ou de disk_drive_/tmp** : le fichier défini au niveau de l’utilisateur (A) est chargé en premier, puis NuGet accède à la racine de disk_drive_2 et trouve le fichier (B).</span><span class="sxs-lookup"><span data-stu-id="afc9a-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="afc9a-174">NuGet recherche également un fichier de configuration dans le répertoire /tmp, sans en trouver un.</span><span class="sxs-lookup"><span data-stu-id="afc9a-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="afc9a-175">Par conséquent, le référentiel par défaut de nuget.org est utilisé, la restauration de package est activée et les packages sont développés dans disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="afc9a-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="afc9a-176">**Appelés à partir de disk_drive_2/Project1 ou de disk_drive_2/Project1/Source** : le fichier défini au niveau de l’utilisateur (A) est chargé en premier, puis NuGet charge le fichier (B) à partir de la racine de disk_drive_2, suivi du fichier (C).</span><span class="sxs-lookup"><span data-stu-id="afc9a-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="afc9a-177">Les paramètres du fichier (C) remplacent ceux des fichiers (B) et (A). Par conséquent, le `repositoryPath` où les packages sont installés est disk_drive_2/Project1/External/Packages et non *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="afc9a-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="afc9a-178">De plus, étant donné que (C) efface `<packageSources>`, nuget.org n’est plus disponible en tant que source, ce qui laisse uniquement `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="afc9a-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="afc9a-179">**Appelés à partir de disk_drive_2/Project2 ou de disk_drive_2/Project2/Source** : le fichier défini au niveau de l’utilisateur (A) est chargé en premier, suivi du fichier (B) et du fichier (D).</span><span class="sxs-lookup"><span data-stu-id="afc9a-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="afc9a-180">Étant donné que `packageSources` n’est pas effacé, `nuget.org` et `https://MyPrivateRepo/DQ/nuget` sont disponibles en tant que sources.</span><span class="sxs-lookup"><span data-stu-id="afc9a-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="afc9a-181">Les packages sont développés dans disk_drive_2/tmp, comme spécifié dans le fichier (B).</span><span class="sxs-lookup"><span data-stu-id="afc9a-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="afc9a-182">Fichier de valeurs par défaut de NuGet</span><span class="sxs-lookup"><span data-stu-id="afc9a-182">NuGet defaults file</span></span>

<span data-ttu-id="afc9a-183">Le fichier `NuGetDefaults.Config` permet de spécifier les sources de package à partir desquelles les packages sont installés et mis à jour, et de contrôler la cible par défaut pour la publication des packages avec `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="afc9a-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="afc9a-184">Étant donné que les administrateurs peuvent aisément (à l’aide d’une stratégie de groupe, par exemple) déployer des fichiers `NuGetDefaults.Config` cohérents sur les ordinateurs de développeurs et les ordinateurs de build, ils peuvent être sûrs que tous les membres de l’organisation utilisent les bonnes sources de package plutôt que nuget.org.</span><span class="sxs-lookup"><span data-stu-id="afc9a-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="afc9a-185">Le fichier `NuGetDefaults.Config` n’entraîne jamais la suppression d’une source de package de la configuration NuGet d’un développeur.</span><span class="sxs-lookup"><span data-stu-id="afc9a-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="afc9a-186">Cela signifie que si le développeur a déjà utilisé NuGet, et donc, que la source du package nuget.org est inscrite, celle-ci ne sera pas supprimée après la création d’un fichier `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="afc9a-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="afc9a-187">De plus, ni `NuGetDefaults.Config` ni tout autre mécanisme de NuGet ne peuvent empêcher l’accès aux sources de package telles que nuget.org. Si une organisation souhaite bloquer ce type d’accès, elle peut utiliser d’autres moyens, tels que les pare-feu.</span><span class="sxs-lookup"><span data-stu-id="afc9a-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="afc9a-188">Emplacement du fichier NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="afc9a-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="afc9a-189">Le tableau suivant explique où le fichier `NuGetDefaults.Config` doit être stocké en fonction du système d’exploitation cible :</span><span class="sxs-lookup"><span data-stu-id="afc9a-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="afc9a-190">Plateforme du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="afc9a-190">OS Platform</span></span>  | <span data-ttu-id="afc9a-191">Emplacement de NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="afc9a-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="afc9a-192">Windows</span><span class="sxs-lookup"><span data-stu-id="afc9a-192">Windows</span></span>      | <span data-ttu-id="afc9a-193">**Visual Studio 2017 ou NuGet 4.x+ :** %ProgramFiles(x86)%\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="afc9a-193">**Visual Studio 2017 or NuGet 4.x+:** %ProgramFiles(x86)%\NuGet\Config</span></span> <br /><span data-ttu-id="afc9a-194">**Visual Studio 2015 et antérieur ou NuGet 3.x et antérieur :** %PROGRAMDATA%\NuGet</span><span class="sxs-lookup"><span data-stu-id="afc9a-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** %PROGRAMDATA%\NuGet</span></span> |
| <span data-ttu-id="afc9a-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="afc9a-195">Mac/Linux</span></span>    | <span data-ttu-id="afc9a-196">$XDG_DATA_HOME (en général, ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="afc9a-196">$XDG_DATA_HOME (typically ~/.local/share)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="afc9a-197">Paramètres du fichier NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="afc9a-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="afc9a-198">`packageSources` : cette collection a la même signification que `packageSources` dans les fichiers config habituels, et spécifie les sources par défaut.</span><span class="sxs-lookup"><span data-stu-id="afc9a-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="afc9a-199">NuGet utilise les sources dans l’ordre durant l’installation ou la mise à jour de packages dans les projets utilisant le format de gestion `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="afc9a-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="afc9a-200">Pour les projets utilisant le format PackageReference, NuGet utilise tout d’abord les sources locales, puis les sources sur les partages réseau et enfin les sources HTTP, quel que soit l’ordre dans les fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="afc9a-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="afc9a-201">NuGet ignore toujours l’ordre des sources avec les opérations de restauration.</span><span class="sxs-lookup"><span data-stu-id="afc9a-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="afc9a-202">`disabledPackageSources` : cette collection a également la même signification que dans les fichiers`NuGet.Config`, où chaque source affectée est répertoriée, avec son nom et une valeur true/false indiquant si elle est activée ou non.</span><span class="sxs-lookup"><span data-stu-id="afc9a-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="afc9a-203">Ainsi, le nom et l’URL de la source sont conservés dans `packageSources`, sans que vous ayez à l’activer par défaut.</span><span class="sxs-lookup"><span data-stu-id="afc9a-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="afc9a-204">Les développeurs peuvent ensuite réactiver la source en définissant sa valeur sur false dans d’autres fichiers `NuGet.Config`, sans avoir à connaître l’URL correcte.</span><span class="sxs-lookup"><span data-stu-id="afc9a-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="afc9a-205">Cela est également utile pour fournir aux développeurs la liste complète des URL sources internes d’une organisation, tout en activant uniquement la source par défaut d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="afc9a-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="afc9a-206">`defaultPushSource` : spécifie la cible par défaut pour les opérations `nuget push`, en substituant la valeur intégrée par défaut de nuget.org. Les administrateurs peuvent déployer ce paramètre pour éviter de publier par inadvertance des packages internes sur le nuget.org public, puisque les développeurs doivent utiliser `nuget push -Source` pour publier des packages sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="afc9a-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="afc9a-207">Exemple de fichier NuGetDefaults.Config et d’application</span><span class="sxs-lookup"><span data-stu-id="afc9a-207">Example NuGetDefaults.Config and application</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
