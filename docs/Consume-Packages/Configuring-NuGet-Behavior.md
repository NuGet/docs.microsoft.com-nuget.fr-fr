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
ms.openlocfilehash: 88f10cf15e16013ac99f315e572f932fd3948f73
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/03/2018
---
# <a name="configuring-nuget-behavior"></a>Configuration du comportement de NuGet

Le comportement de NuGet est contrôlé par les paramètres qui sont définis dans un ou plusieurs fichiers `NuGet.Config` (XML) qui peuvent exister au niveau du projet, de l’utilisateur ou de l’ordinateur. Un fichier `NuGetDefaults.Config` global configure également les sources de package. Les paramètres s’appliquent à toutes les commandes émises dans l’interface CLI, la console du gestionnaire de package et l’interface utilisateur du gestionnaire de package.

## <a name="config-file-locations-and-uses"></a>Emplacements et utilisations des fichiers config

| Portée | Emplacement du fichier NuGet.Config | Description |
| --- | --- | --- |
| Projet | Dossier actuel (dossier du projet) ou tout dossier pouvant être situé jusqu’à la racine du lecteur.| Dans un dossier de projet, les paramètres s’appliquent uniquement au projet en question. Dans les dossiers parents qui contiennent plusieurs dossiers de projets, les paramètres s’appliquent à tous les projets des sous-dossiers. |
| Utilisateur | Windows : `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux : `~/.config/NuGet/NuGet.Config` ou `~/.nuget/NuGet/NuGet.Config` (en fonction de la distribution du système d’exploitation) | Les paramètres s’appliquent à toutes les opérations. Toutefois, ils sont substitués par tout paramètre défini au niveau du projet. |
| Ordinateur | Windows : `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux : `$XDG_DATA_HOME`. Si `$XDG_DATA_HOME` est null ou vide, `~/.local/share` ou `/usr/local/share` seront utilisés (en fonction de la distribution du système d’exploitation)  | Les paramètres s’appliquent à toutes les opérations effectuées sur l’ordinateur. Toutefois, ils sont remplacés par tout paramètre défini au niveau de l’utilisateur ou du projet. |

Remarques concernant les versions précédentes de NuGet :
- NuGet 3.3 et versions antérieures utilisaient un dossier `.nuget` pour les paramètres définis au niveau de la solution. Ce fichier n’est plus utilisé dans NuGet 3.4+.
- Pour NuGet 2.6 3.x, le fichier config défini au niveau d’un ordinateur Windows était situé dans %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, où *{IDE}* pouvait correspondre à  *Visual Studio*, *{Version}* à la version de Visual Studio, comme *14.0*, et *{SKU}* à l’édition *Community*, *Pro* ou *Enterprise*. Pour migrer les paramètres vers NuGet 4.0+, copiez simplement le fichier config vers %ProgramFiles(x86)%\NuGet\Config. Sur Linux, l’ancien emplacement était /etc/opt et sur Mac, Library/Application Support.

## <a name="changing-config-settings"></a>Modification des paramètres de configuration

Un fichier `NuGet.Config` est un simple fichier texte XML contenant des paires clé/valeur, comme décrit dans la rubrique [Paramètres de configuration NuGet](../reference/nuget-config-file.md).

Les paramètres sont gérés à l’aide de la [commande config](../tools/cli-ref-config.md) de l’interface CLI de NuGet :
- Par défaut, les modifications sont apportées au fichier config défini au niveau de l’utilisateur.
- Pour modifier les paramètres dans un autre fichier, utilisez le commutateur `-configFile`. Dans ce cas, les fichiers peuvent utiliser n’importe quel nom de fichier.
- Les clés respectent toujours la casse.
- Une élévation des privilèges est nécessaire pour modifier les paramètres du fichier de paramètres défini au niveau de l’ordinateur.

> [!Warning]
> Même si vous pouvez modifier le fichier dans n’importe quel éditeur de texte, NuGet (v3.4.3 et versions ultérieures) ignore silencieusement l’intégralité du fichier de configuration si celui-ci contient du code XML incorrectement formé (balises incompatibles, guillemets non valides, etc.). C’est pourquoi il est préférable de gérer les paramètres à l’aide de `nuget config`.

### <a name="setting-a-value"></a>Définition d’une valeur

Windows :

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

Mac/Linux :

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
> Dans NuGet 3.4 et versions ultérieures, vous pouvez utiliser des variables d’environnement dans n’importe quelle valeur, comme dans `repositoryPath=%PACKAGEHOME%` (Windows) et `repositoryPath=%PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Suppression dune valeur

Pour supprimer une valeur, spécifiez une clé avec une valeur vide.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Création d’un fichier config

Copiez le modèle ci-dessous dans le nouveau fichier, puis utilisez `nuget config -configFile <filename>` pour définir les valeurs :

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Application des paramètres

L’utilisation de plusieurs fichiers `NuGet.Config` permet de stocker des paramètres à différents emplacements, de manière à les appliquer à un projet, à un groupe de projets ou à l’ensemble des projets. Ces paramètres s’appliquent collectivement à toute opération NuGet appelée à partir de la ligne de commande ou de Visual Studio. Les paramètres « les plus proches » d’un projet ou du dossier actif sont prioritaires.

Plus précisément, NuGet charge les paramètres à partir de plusieurs fichiers config dans l’ordre suivant :

1. Le [fichier NuGetDefaults.Config](#nuget-defaults-file), qui contient les paramètres concernant uniquement les sources de package.
1. Le fichier défini au niveau de l’ordinateur.
1. Le fichier défini au niveau de l’utilisateur.
1. Le fichier spécifié avec `-configFile`.
1. Les fichiers qui se trouvent dans chacun des dossiers du chemin allant de la racine du lecteur au dossier actif (celui où nuget.exe est appelé ou le dossier qui contient le projet Visual Studio). Par exemple, si une commande est appelée dans c:\A\B\C, NuGet recherche et charge les fichiers config dans c:\,, puis c:\A, puis c:\A\B, et enfin, dans c:\A\B\C.

Quand NuGet trouve les paramètres dans ces fichiers, il les applique de la manière suivante :

1. Pour les éléments uniques, NuGet remplaçait toute valeur précédemment trouvée pour la même clé. Cela signifie que les paramètres qui sont « les plus proches » du dossier actif ou du projet remplacent les paramètres trouvés précédemment. Par exemple, le paramètre `defaultPushSource` dans `NuGetDefaults.Config` est remplacé s’il se trouve également dans un autre fichier config.

1. Pour les éléments de collection (tels que `<packageSources>`), NuGet combine les valeurs de tous les fichiers de configuration dans une même collection.

1. Lorsque `<clear />` est présent pour un nœud donné, NuGet ignore les valeurs de configuration définies précédemment pour ce nœud.

### <a name="settings-walkthrough"></a>Procédure pas à pas pour l’application des paramètres

Supposons que vous disposiez de la structure de dossiers suivante sur deux lecteurs distincts :

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Vous avez donc quatre fichiers `NuGet.Config` aux emplacements suivants, avec le contenu spécifié (le fichier défini au niveau de l’ordinateur n’est pas inclus dans cet exemple, toutefois, son comportent est similaire à celui du fichier défini au niveau de l’utilisateur).

Fichier A. Fichier de niveau utilisateur (`%appdata%\NuGet\NuGet.Config` sur Windows, `~/.config/NuGet/NuGet.Config` sur Mac/Linux) :

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Fichier B. disk_drive_2/NuGet.Config :

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

Fichier C. disk_drive_2/Project1/NuGet.Config :

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

Fichier D. disk_drive_2/Project2/NuGet.Config :

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

Ensuite, NuGet charge et applique les paramètres de la manière suivante, en fonction de l’emplacement où ils sont appelés :

- **Appelés à partir de disk_drive_1/users** : seul le référentiel par défaut répertorié dans le fichier de configuration défini au niveau de l’utilisateur (A) est utilisé, car il s’agit du seul fichier trouvé à l’emplacement disk_drive_1.

- **Appelés à partir de disk_drive_2/ ou de disk_drive_/tmp** : le fichier défini au niveau de l’utilisateur (A) est chargé en premier, puis NuGet accède à la racine de disk_drive_2 et trouve le fichier (B). NuGet recherche également un fichier de configuration dans le répertoire /tmp, sans en trouver un. Par conséquent, le référentiel par défaut de nuget.org est utilisé, la restauration de package est activée et les packages sont développés dans disk_drive_2/tmp.

- **Appelés à partir de disk_drive_2/Project1 ou de disk_drive_2/Project1/Source** : le fichier défini au niveau de l’utilisateur (A) est chargé en premier, puis NuGet charge le fichier (B) à partir de la racine de disk_drive_2, suivi du fichier (C). Les paramètres du fichier (C) remplacent ceux des fichiers (B) et (A). Par conséquent, le `repositoryPath` où les packages sont installés est disk_drive_2/Project1/External/Packages et non *disk_drive_2/tmp*. De plus, étant donné que (C) efface `<packageSources>`, nuget.org n’est plus disponible en tant que source, ce qui laisse uniquement `https://MyPrivateRepo/ES/nuget`.

- **Appelés à partir de disk_drive_2/Project2 ou de disk_drive_2/Project2/Source** : le fichier défini au niveau de l’utilisateur (A) est chargé en premier, suivi du fichier (B) et du fichier (D). Étant donné que `packageSources` n’est pas effacé, `nuget.org` et `https://MyPrivateRepo/DQ/nuget` sont disponibles en tant que sources. Les packages sont développés dans disk_drive_2/tmp, comme spécifié dans le fichier (B).

## <a name="nuget-defaults-file"></a>Fichier de valeurs par défaut de NuGet

Le fichier `NuGetDefaults.Config` permet de spécifier les sources de package à partir desquelles les packages sont installés et mis à jour, et de contrôler la cible par défaut pour la publication des packages avec `nuget push`. Étant donné que les administrateurs peuvent aisément (à l’aide d’une stratégie de groupe, par exemple) déployer des fichiers `NuGetDefaults.Config` cohérents sur les ordinateurs de développeurs et les ordinateurs de build, ils peuvent être sûrs que tous les membres de l’organisation utilisent les bonnes sources de package plutôt que nuget.org.

> [!Important]
> Le fichier `NuGetDefaults.Config` n’entraîne jamais la suppression d’une source de package de la configuration NuGet d’un développeur. Cela signifie que si le développeur a déjà utilisé NuGet, et donc, que la source du package nuget.org est inscrite, celle-ci ne sera pas supprimée après la création d’un fichier `NuGetDefaults.Config`.
>
> De plus, ni `NuGetDefaults.Config` ni tout autre mécanisme de NuGet ne peuvent empêcher l’accès aux sources de package telles que nuget.org. Si une organisation souhaite bloquer ce type d’accès, elle peut utiliser d’autres moyens, tels que les pare-feu.

### <a name="nugetdefaultsconfig-location"></a>Emplacement du fichier NuGetDefaults.Config

Le tableau suivant explique où le fichier `NuGetDefaults.Config` doit être stocké en fonction du système d’exploitation cible :

| Plateforme du système d’exploitation  | Emplacement de NuGetDefaults.Config |
| --- | --- |
| Windows      | **Visual Studio 2017 ou NuGet 4.x+ :** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 et versions antérieures ou NuGet 3.x et versions antérieures :** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (généralement `~/.local/share` ou `/usr/local/share`, en fonction de la distribution du système d’exploitation)|

### <a name="nugetdefaultsconfig-settings"></a>Paramètres du fichier NuGetDefaults.Config

- `packageSources` : cette collection a la même signification que `packageSources` dans les fichiers config habituels, et spécifie les sources par défaut. NuGet utilise les sources dans l’ordre durant l’installation ou la mise à jour de packages dans les projets utilisant le format de gestion `packages.config`. Pour les projets utilisant le format PackageReference, NuGet utilise tout d’abord les sources locales, puis les sources sur les partages réseau et enfin les sources HTTP, quel que soit l’ordre dans les fichiers de configuration. NuGet ignore toujours l’ordre des sources avec les opérations de restauration.

- `disabledPackageSources` : cette collection a également la même signification que dans les fichiers`NuGet.Config`, où chaque source affectée est répertoriée, avec son nom et une valeur true/false indiquant si elle est activée ou non. Ainsi, le nom et l’URL de la source sont conservés dans `packageSources`, sans que vous ayez à l’activer par défaut. Les développeurs peuvent ensuite réactiver la source en définissant sa valeur sur false dans d’autres fichiers `NuGet.Config`, sans avoir à connaître l’URL correcte. Cela est également utile pour fournir aux développeurs la liste complète des URL sources internes d’une organisation, tout en activant uniquement la source par défaut d’une équipe.

- `defaultPushSource` : spécifie la cible par défaut pour les opérations `nuget push`, en substituant la valeur intégrée par défaut de nuget.org. Les administrateurs peuvent déployer ce paramètre pour éviter de publier par inadvertance des packages internes sur le nuget.org public, puisque les développeurs doivent utiliser `nuget push -Source` pour publier des packages sur nuget.org.

### <a name="example-nugetdefaultsconfig-and-application"></a>Exemple de fichier NuGetDefaults.Config et d’application

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
