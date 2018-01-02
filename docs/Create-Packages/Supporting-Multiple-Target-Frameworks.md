---
title: Multi-ciblage pour les packages NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2646ffcd-83ae-4086-8915-a7fba3f53e45
description: "Description des différentes méthodes pour cibler plusieurs versions de .NET Framework à partir d’un seul package NuGet."
keywords: "Ciblage de packages NuGet, versions de .NET Framework, NuGet et .NET, ciblage de plusieurs frameworks, création de packages NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d23158c6dab838b723764994e94fc21cab52f553
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="supporting-multiple-net-framework-versions"></a>Prise en charge de plusieurs versions de .NET Framework

*Pour les projets .NET Core qui utilisent NuGet 4.0 +, consultez [Commandes NuGet pack et restore en tant que cibles MSBuild](../schema/msbuild-targets.md) pour plus d’informations sur le ciblage croisé.*

De nombreuses bibliothèques ciblent une version spécifique de .NET Framework. Par exemple, vous pouvez avoir une première version de votre bibliothèque propre à la plateforme Windows universelle (UWP) et une autre version qui exploite les fonctionnalités de .NET Framework 4.6.

Pour en tenir compte, NuGet prend en charge le placement de plusieurs versions de la même bibliothèque dans un même package dans le cadre de l’utilisation de la méthode de répertoire de travail basée sur une convention décrite dans [Création d’un package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).

Dans cette rubrique :

- [Structure de dossiers de la version du framework](#framework-version-folder-structure)
- [Correspondance entre les versions d’assembly et la version cible de .Net Framework dans un projet](#matching-assembly-versions-and-the-target-framework-in-a-project)
- [Regroupement d’assemblys par version du framework](#grouping-assemblies-by-framework-version)
- [Détermination de la cible NuGet à utiliser](#determining-which-nuget-target-to-use)
- [Fichiers de contenu et scripts PowerShell](#content-files-and-powershell-scripts)


## <a name="framework-version-folder-structure"></a>Structure de dossiers de la version du framework

Lorsque vous créez un package qui contient uniquement une version d’une bibliothèque ou qui cible plusieurs frameworks, vous créez systématiquement des sous-dossiers dans le dossier `lib` en utilisant des noms de framework différents qui respectent la casse selon la convention suivante :

    lib\{framework name}[{version}]

Pour obtenir la liste complète des noms pris en charge, consultez les [informations de référence sur les versions cibles de .Net Framework](../schema/target-frameworks.md#supported-frameworks).

Vous ne devez jamais avoir une version de la bibliothèque qui n’est pas propre à un framework et placée directement dans le dossier `lib` racine. (Cette fonctionnalité était prise en charge uniquement avec `packages.config`). En effet, la bibliothèque serait alors compatible avec n’importe quelle version cible de .Net Framework et pourrait être installée n’importe où, entraînant des erreurs inattendues du runtime. L’ajout d’assemblys dans le dossier racine (comme `lib\abc.dll`) ou des sous-dossiers (comme `lib\abc\abc.dll`) est déprécié et ignoré lorsque vous utilisez le format PackagesReference.

Par exemple, la structure de dossiers suivante prend en charge quatre versions d’un assembly propres à un framework :

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Pour inclure facilement tous ces fichiers lors de la génération du package, utilisez un caractère générique `**` récursif dans la section `<files>` de votre `.nuspec` :

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Dossiers propres à l’architecture 

Si vous avez des assemblys propres à une architecture, autrement dit, des assemblys distincts qui ciblent ARM, x86 et x64, vous devez les placer dans un dossier nommé `runtimes` au sein de sous-dossiers nommés `{platform}-{architecture}\lib\{framework}` ou `{platform}-{architecture}\native`. Par exemple, la structure de dossiers suivante s’adapte à la fois aux DLL natives et managées ciblant Windows 10 et le framework `uap10.0` :

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

Consultez [Créer des packages UWP](../Guides/Create-UWP-Packages.md) pour obtenir un exemple de référencement de ces fichiers dans le manifeste `.nuspec`.


## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Correspondance entre les versions d’assembly et la version cible de .Net Framework dans un projet

Lorsque NuGet installe un package qui a plusieurs versions d’assembly, il essaie de faire correspondre le nom du framework de l’assembly à la version cible de .Net Framework du projet.

Si aucune correspondance n’est trouvée, NuGet copie l’assembly de la version la plus élevée inférieure ou égale à la version cible de .Net Framework du projet, si elle est disponible. Si aucun assembly compatible n’est trouvé, NuGet renvoie un message d’erreur approprié.

Par exemple, considérez la structure de dossiers suivante dans un package :

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll


Quand vous installez ce package dans un projet qui cible .NET Framework 4.6, NuGet installe l’assembly dans le dossier `net45`, car il s’agit de la version disponible la plus élevée inférieure ou égale à 4.6.

D’autre part, si le projet cible .NET Framework 4.6.1, NuGet installe l’assembly dans le dossier `net461`.

Si le projet cible .NET framework 4.0 et des versions antérieures, NuGet envoie un message d’erreur approprié indiquant que l’assembly compatible est introuvable.

## <a name="grouping-assemblies-by-framework-version"></a>Regroupement d’assemblys par version du framework

NuGet copie des assemblys à partir d’un seul dossier de bibliothèque dans le package. Par exemple, supposons qu’un package présente la structure de dossiers suivante :

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Lorsque le package est installé dans un projet qui cible .NET Framework 4.5, `MyAssembly.dll` (v2.0) est le seul assembly installé. `MyAssembly.Core.dll` (v1.0) n’est pas installé, car il n’est pas répertorié dans le dossier `net45`. NuGet se comporte ainsi car `MyAssembly.Core.dll` a peut-être été fusionné dans la version 2.0 de `MyAssembly.dll`.

Si vous voulez que `MyAssembly.Core.dll` soit installé pour .NET Framework 4.5, placez une copie dans le dossier `net45`.

## <a name="grouping-assemblies-by-framework-profile"></a>Regroupement d’assemblys par profil du framework

NuGet prend également en charge le ciblage d’un profil de framework spécifique en ajoutant un tiret et le nom du profil à la fin du dossier.

    lib\{framework name}-{profile}

Les profils pris en charge sont les suivants :

- `client` : Client Profile
- `full` : Full Profile
- `wp` : Windows Phone
- `cf` : Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>Détermination de la cible NuGet à utiliser

Lorsque vous empaquetez des bibliothèques ciblant la bibliothèque de classes portable, il peut être difficile de déterminer quelle cible NuGet vous devez utiliser dans vos noms de dossier et votre fichier `.nuspec`, en particulier si vous ciblez uniquement un sous-ensemble de la bibliothèque de classes portable. Les ressources externes suivantes peuvent vous aider à la déterminer :

- [Profils de framework dans .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [Profils de la bibliothèque de classes portable](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co) : tableau qui énumère les profils de la bibliothèque de classes portable et leurs cibles NuGet équivalentes
- [Outil des profils de la bibliothèque de classes portable](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com) : outil en ligne de commande permettant de déterminer les profils de la bibliothèque de classes portable disponibles sur votre système

## <a name="content-files-and-powershell-scripts"></a>Fichiers de contenu et scripts PowerShell

> [!Warning]
> Des fichiers de contenu mutables et une exécution des scripts sont disponibles au format `packages.config` uniquement ; ils sont dépréciés lorsque vous utilisez `project.json` et des formats PackagesReference et ne doivent pas être utilisés pour de nouveaux packages.

Avec `packages.config`, il est possible de regrouper les fichiers de contenu et les scripts PowerShell par version cible de .Net Framework en utilisant la même convention de dossier à l’intérieur des dossiers `content` et `tools`. Exemple :

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

Si un dossier de framework est vide, NuGet n’y ajoute pas de références d’assembly ni de fichiers de contenu ou n’exécute pas les scripts PowerShell pour ce framework.

> [!Note]
> Étant donné que `init.ps1` s’exécute au niveau de la solution et ne dépend pas du projet, il doit être placé directement sous le dossier `tools`. Ce fichier est ignoré s’il est placé sous un dossier de framework.
