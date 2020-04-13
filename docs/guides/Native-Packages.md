---
title: Création de packages NuGet natifs
description: Informations sur la création de packages NuGet natifs contenant du code C++ au lieu de code managé, à utiliser dans des projets C++.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69520519"
---
# <a name="creating-native-packages"></a>Création de packages natifs

Un package natif contient des binaires natifs au lieu d’assemblys managés, ce qui lui permet d’être utilisé dans des projets C++ (ou similaires). (Consultez [Packages C++ natifs](../consume-packages/finding-and-choosing-packages.md#native-c-packages) dans la section Consommer.)

Pour être consommable dans un projet C++, un package doit cibler le framework `native`. Actuellement, aucun numéro de version n’est associé à ce framework car NuGet traite tous les projets C++ de la même façon.

> [!Note]
> Veillez à inclure *natif* dans la section `<tags>` de votre `.nuspec` pour aider les autres développeurs à trouver votre package en recherchant cette étiquette.

Les packages NuGet natifs ciblant `native` fournissent ensuite des fichiers dans des dossiers `\build`, `\content` et `\tools` ; `\lib` n’est pas utilisé dans ce cas (NuGet ne peut pas ajouter directement des références à un projet C++). Un package peut également inclure des cibles et des fichiers props dans `\build` que NuGet va automatiquement importer dans les projets qui consomment le package. Ces fichiers doivent être nommés de la même façon que l’ID de package et porter des extensions `.targets` et/ou `.props`. Par exemple, le package [cpprestsdk](https://nuget.org/packages/cpprestsdk/) inclut un fichier `cpprestsdk.targets` dans son dossier `\build`.

Le dossier `\build` peut être utilisé pour tous les packages NuGet et pas simplement les packages natifs. Le dossier `\build` respecte les frameworks cibles à l’instar des dossiers `\content`, `\lib` et `\tools`. Cela signifie que vous pouvez créer un dossier `\build\net40` et un dossier `\build\net45` pour que NuGet importe les fichiers de propriétés et de cibles appropriés dans le projet. (L’utilisation de scripts PowerShell pour importer des cibles MSBuild n’est pas nécessaire.)
