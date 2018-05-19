---
title: Création de packages NuGet natifs
description: Informations sur la création de packages NuGet natifs contenant du code C++ au lieu de code managé, à utiliser dans des projets C++.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 1fa8bf23a3fbed686b99f1c783b0ce55b373e548
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="creating-native-packages"></a><span data-ttu-id="fe39d-103">Création de packages natifs</span><span class="sxs-lookup"><span data-stu-id="fe39d-103">Creating native packages</span></span>

<span data-ttu-id="fe39d-104">Un package natif contient du code C++ natif au lieu de code managé, ce qui lui permet d’être utilisé dans des projets C++.</span><span class="sxs-lookup"><span data-stu-id="fe39d-104">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="fe39d-105">(Consultez [Packages C++ natifs](../consume-packages/finding-and-choosing-packages.md#native-c-packages) dans la section Consommer.)</span><span class="sxs-lookup"><span data-stu-id="fe39d-105">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) in the Consume section.)</span></span>

<span data-ttu-id="fe39d-106">Pour être consommable dans un projet C++, un package doit cibler le framework `native`.</span><span class="sxs-lookup"><span data-stu-id="fe39d-106">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="fe39d-107">Actuellement, aucun numéro de version n’est associé à ce framework car NuGet traite tous les projets C++ de la même façon.</span><span class="sxs-lookup"><span data-stu-id="fe39d-107">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="fe39d-108">Veillez à inclure *natif* dans la section `<tags>` de votre `.nuspec` pour aider les autres développeurs à trouver votre package en recherchant cette étiquette.</span><span class="sxs-lookup"><span data-stu-id="fe39d-108">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="fe39d-109">Les packages NuGet natifs ciblant `native` fournissent ensuite des fichiers dans des dossiers `\build`, `\content` et `\tools` ; `\lib` n’est pas utilisé dans ce cas (NuGet ne peut pas ajouter directement des références à un projet C++).</span><span class="sxs-lookup"><span data-stu-id="fe39d-109">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="fe39d-110">Un package peut également inclure des cibles et des fichiers props dans `\build` que NuGet va automatiquement importer dans les projets qui consomment le package.</span><span class="sxs-lookup"><span data-stu-id="fe39d-110">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="fe39d-111">Ces fichiers doivent être nommés de la même façon que l’ID de package et porter des extensions `.targets` et/ou `.props`.</span><span class="sxs-lookup"><span data-stu-id="fe39d-111">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="fe39d-112">Par exemple, le package [cpprestsdk](https://nuget.org/packages/cpprestsdk/) inclut un fichier `cpprestsdk.targets` dans son dossier `\build`.</span><span class="sxs-lookup"><span data-stu-id="fe39d-112">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="fe39d-113">Le dossier `\build` peut être utilisé pour tous les packages NuGet et pas simplement les packages natifs.</span><span class="sxs-lookup"><span data-stu-id="fe39d-113">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="fe39d-114">Le dossier `\build` respecte les frameworks cibles à l’instar des dossiers `\content`, `\lib` et `\tools`.</span><span class="sxs-lookup"><span data-stu-id="fe39d-114">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="fe39d-115">Cela signifie que vous pouvez créer un dossier `\build\net40` et un dossier `\build\net45` pour que NuGet importe les fichiers de propriétés et de cibles appropriés dans le projet.</span><span class="sxs-lookup"><span data-stu-id="fe39d-115">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="fe39d-116">(L’utilisation de scripts PowerShell pour importer des cibles MSBuild n’est pas nécessaire.)</span><span class="sxs-lookup"><span data-stu-id="fe39d-116">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>