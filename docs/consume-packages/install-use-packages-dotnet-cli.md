---
title: Installer et gérer des packages NuGet à l’aide de l’interface CLI dotnet
description: Instructions d’utilisation de l’interface CLI dotnet pour gérer des packages NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: fecf14f0f04d5063f89080b2756f988739c1412c
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859263"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Installer et gérer des packages à l’aide de l’interface CLI dotnet

L’outil CLI facilite l’installation, la désinstallation et la mise à jour des packages NuGet dans les projets et solutions. Il s’exécute sur Windows, Mac OS X et Linux.

Vous pouvez utiliser l’interface CLI dotnet dans votre projet .NET Core et .NET Standard (types de projets de style SDK) et dans tous les autres projets de style SDK (par exemple, un projet de style SDK qui cible le .NET Framework). Pour plus d’informations, consultez [Attribut Sdk](/dotnet/core/tools/csproj#additions).

Cet article explique l’utilisation de base de quelques-unes des commandes de la CLI dotnet les plus courantes. Pour la plupart de ces commandes, l’outil CLI recherche un fichier projet dans le répertoire actif, sauf si vous avez spécifié un fichier projet particulier dans la commande (le fichier projet est un commutateur facultatif). Pour obtenir une liste complète des commandes et des arguments disponibles, consultez les [outils de l’interface de ligne de commande (CLI) de .NET Core](../reference/dotnet-commands.md).

## <a name="prerequisites"></a>Prérequis

- Le [kit SDK .NET Core](https://www.microsoft.com/net/download/), qui fournit l’outil en ligne de commande `dotnet`. À compter de Visual Studio 2017, la CLI dotnet est installée automatiquement avec les charges de travail associées à NET Core.

## <a name="install-a-package"></a>Installer un package

[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) ajoute une référence de package au fichier projet, puis exécute `dotnet restore` pour installer le package.

1. Ouvrez une ligne de commande et accédez au répertoire contenant votre fichier projet.

2. Utilisez la commande suivante pour installer un package Nuget :

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Par exemple, pour installer le package `Newtonsoft.Json`, utilisez cette commande :

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Une fois que la commande est terminée, examinez le fichier projet pour vérifier que le package a été installé.

   Vous pouvez ouvrir le fichier `.csproj` pour voir la référence ajoutée :

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Installer une version particulière d’un package

Si vous ne spécifiez pas de version, NuGet installe la dernière version disponible du package. Vous pouvez également utiliser la commande [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) pour installer une version particulière d’un package Nuget :

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

Par exemple, pour ajouter la version 12.0.1 du package `Newtonsoft.Json`, utilisez cette commande :

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a>Lister les références de package

Vous pouvez lister les références de package pour votre projet en utilisant la commande [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Supprimer un package

Utilisez la commande [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) pour supprimer une référence de package dans le fichier projet.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Par exemple, pour supprimer le package `Newtonsoft.Json`, utilisez cette commande :

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Mettre à jour un package

NuGet installe la dernière version du package quand vous utilisez la commande `dotnet add package`, sauf si vous spécifiez une version particulière du package (commutateur `-v`).

## <a name="restore-packages"></a>Restaurer des packages

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
