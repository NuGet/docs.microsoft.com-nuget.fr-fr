---
title: Sélectionner des assemblys référencés par les projets
description: Mettez un sous-ensemble d’assemblys dans le package à la disposition du compilateur, alors que tous les assemblys sont disponibles au moment de l’exécution.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427474"
---
# <a name="select-assemblies-referenced-by-projects"></a>Sélectionner des assemblys référencés par les projets

Avec les références d’assembly explicites, vous pouvez utiliser un sous-ensemble d’assemblys pour IntelliSense et la compilation, alors que tous les assemblys sont disponibles au moment de l’exécution. Étant donné que `PackageReference` et `packages.config` fonctionnent différemment, les auteurs de packages doivent s’assurer de créer des packages compatibles avec les deux types de projets.

> [!Note]
> Les références d’assembly explicites s’appliquent aux assemblys .NET. Ce n’est pas une méthode permettant de distribuer les assemblys natifs qui sont appelés (P/Invoke) par un assembly managé.

## <a name="packagereference-support"></a>Prise en charge de `PackageReference`

Quand un projet utilise un package avec `PackageReference` et que ce package contient un répertoire `ref\<tfm>\`, NuGet classe ces assemblys en tant que ressources de compilation, alors que les assemblys `lib\<tfm>\` sont classés en tant que ressources d’exécution. Les assemblys dans `ref\<tfm>\` ne sont pas utilisés au moment de l’exécution. Cela implique que chaque assembly dans `ref\<tfm>\` ait un assembly correspondant dans `lib\<tfm>\` ou dans un répertoire `runtime\` correspondant. Sinon, des erreurs d’exécution se produiront certainement. Du fait que les assemblys dans `ref\<tfm>\` ne sont pas utilisés au moment de l’exécution, vous pouvez utiliser des [assemblys de métadonnées uniquement](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) afin de réduire la taille du package.

> [!Important]
> Si un package contient l’élément nuspec `<references>` (utilisé par `packages.config`, comme décrit ci-dessous) et ne contient pas d’assemblys dans `ref\<tfm>\`, NuGet publie les assemblys listés dans l’élément nuspec `<references>` à la fois comme ressources de compilation et ressources d’exécution. Cela signifie qu’il y aura des exceptions de runtime si les assemblys référencés doivent charger un autre assembly dans le répertoire `lib\<tfm>\`.

> [!Note]
> Si le package contient un répertoire `runtime\`, NuGet n’utilise pas les ressources contenues dans le répertoire `lib\`.

## <a name="packagesconfig-support"></a>Prise en charge de `packages.config`

Les projets qui utilisent `packages.config` pour gérer les packages NuGet ajoutent normalement des références à tous les assemblys listés dans le répertoire `lib\<tfm>\`. Le répertoire `ref\` ayant été ajouté pour prendre en charge `PackageReference`, il est ignoré quand `packages.config` est utilisé. Pour définir explicitement quels assemblys sont référencés dans les projets utilisant `packages.config`, le package doit utiliser l’[élément `<references>` dans le fichier nuspec](../reference/nuspec.md#explicit-assembly-references). Par exemple :

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> Le projet `packages.config` utilise un processus appelé [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) pour copier les assemblys dans le répertoire de sortie `bin\<configuration>\`. L’assembly du projet est copié, après quoi le système de build recherche les assemblys référencés dans le manifeste de l’assembly, puis copie ces assemblys, et répète cette séquence de manière récursive pour tous les assemblys. Cela signifie que si un des assemblys du répertoire `lib\<tfm>\` n’est pas référencé dans le manifeste d’aucun autre assembly en tant que dépendance (si l’assembly est chargé au moment de l’exécution avec `Assembly.Load`, MEF ou tout autre framework d’injection de dépendance), il risque de ne pas être copié dans le répertoire de sortie `bin\<configuration>\` de votre projet, même s’il est bien dans `bin\<tfm>\`.

## <a name="example"></a>Exemples

Mon package doit contenir trois assemblys, `MyLib.dll`, `MyHelpers.dll` et `MyUtilities.dll`, qui ciblent .NET Framework 4.7.2. `MyUtilities.dll` contient des classes destinées à être utilisées uniquement par les deux autres assemblys. Je ne veux donc pas que ces classes soient disponibles dans IntelliSense ou au moment de la compilation pour les projets qui utilisent mon package. Mon fichier `nuspec` doit contenir les éléments XML suivants :

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

Le package doit contenir ces fichiers :

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
