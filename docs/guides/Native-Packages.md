---
title: Création de packages NuGet natifs
description: Informations sur la création de packages NuGet natifs contenant du code C++ au lieu de code managé, à utiliser dans des projets C++.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 2a95fca2ce5496512627e913273e5b66128e34c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774205"
---
# <a name="creating-native-packages"></a>Création de packages natifs

Un package natif contient des binaires natifs au lieu d’assemblys managés, ce qui lui permet d’être utilisé dans des projets C++ (ou similaires). (Consultez [Packages C++ natifs](../consume-packages/finding-and-choosing-packages.md#native-c-packages) dans la section Consommer.)

Pour être consommable dans un projet C++, un package doit cibler le framework `native`. Actuellement, aucun numéro de version n’est associé à ce framework car NuGet traite tous les projets C++ de la même façon.

> [!Note]
> Veillez à inclure *natif* dans la section `<tags>` de votre `.nuspec` pour aider les autres développeurs à trouver votre package en recherchant cette étiquette.

Les packages NuGet natifs ciblant `native` fournissent ensuite des fichiers dans des dossiers `\build`, `\content` et `\tools` ; `\lib` n’est pas utilisé dans ce cas (NuGet ne peut pas ajouter directement des références à un projet C++). Un package peut également inclure des cibles et des fichiers props dans `\build` que NuGet va automatiquement importer dans les projets qui consomment le package. Ces fichiers doivent être nommés de la même façon que l’ID de package et porter des extensions `.targets` et/ou `.props`. Par exemple, le package [cpprestsdk](https://nuget.org/packages/cpprestsdk/) inclut un fichier `cpprestsdk.targets` dans son dossier `\build`.

Le dossier `\build` peut être utilisé pour tous les packages NuGet et pas simplement les packages natifs. Le dossier `\build` respecte les frameworks cibles à l’instar des dossiers `\content`, `\lib` et `\tools`. Cela signifie que vous pouvez créer un dossier `\build\net40` et un dossier `\build\net45` pour que NuGet importe les fichiers de propriétés et de cibles appropriés dans le projet. (L’utilisation de scripts PowerShell pour importer des cibles MSBuild n’est pas nécessaire.)
