---
title: Création de packages NuGet natifs | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informations sur la création de packages NuGet natifs contenant du code C++ au lieu de code managé, à utiliser dans des projets C++.
keywords: Packages NuGet natifs, packages NuGet C++, packages de code natif, ciblant des projets C++
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ed33f906f11a80c0d033292f7de151e93b8368fd
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="creating-native-packages"></a>Création de packages natifs

Un package natif contient du code C++ natif au lieu de code managé, ce qui lui permet d’être utilisé dans des projets C++. (Consultez [Packages C++ natifs](../consume-packages/finding-and-choosing-packages.md#native-c-packages) dans la section Consommer.)

Pour être consommable dans un projet C++, un package doit cibler le framework `native`. Actuellement, aucun numéro de version n’est associé à ce framework car NuGet traite tous les projets C++ de la même façon.

> [!Note]
> Veillez à inclure *natif* dans la section `<tags>` de votre `.nuspec` pour aider les autres développeurs à trouver votre package en recherchant cette étiquette.

Les packages NuGet natifs ciblant `native` fournissent ensuite des fichiers dans des dossiers `\build`, `\content` et `\tools` ; `\lib` n’est pas utilisé dans ce cas (NuGet ne peut pas ajouter directement des références à un projet C++). Un package peut également inclure des cibles et des fichiers props dans `\build` que NuGet va automatiquement importer dans les projets qui consomment le package. Ces fichiers doivent être nommés de la même façon que l’ID de package et porter des extensions `.targets` et/ou `.props`. Par exemple, le package [cpprestsdk](https://nuget.org/packages/cpprestsdk/) inclut un fichier `cpprestsdk.targets` dans son dossier `\build`.

Le dossier `\build` peut être utilisé pour tous les packages NuGet et pas simplement les packages natifs. Le dossier `\build` respecte les frameworks cibles à l’instar des dossiers `\content`, `\lib` et `\tools`. Cela signifie que vous pouvez créer un dossier `\build\net40` et un dossier `\build\net45` pour que NuGet importe les fichiers de propriétés et de cibles appropriés dans le projet. (L’utilisation de scripts PowerShell pour importer des cibles MSBuild n’est pas nécessaire.)
