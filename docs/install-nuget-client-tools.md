---
title: Installation des outils clients NuGet
description: Conseils sur l’installation des outils clients, des interfaces de ligne de commande (CLI) dotnet et nuget et du Gestionnaire de package pour Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: a4a3f5509792e56c09d18b3da98588d17f4756ee
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67841939"
---
# <a name="install-nuget-client-tools"></a>Installer les outils clients NuGet

> **Vous souhaitez installer un package ? Voir [Méthodes d'installation des packages NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Pour utiliser NuGet en tant que consommateur ou créateur de packages, vous pouvez utiliser les outils de l’interface de ligne de commande (CLI) ainsi que les fonctionnalités NuGet dans Visual Studio. Cet article présente brièvement les fonctionnalités des différents outils et explique comment les installer, avec une comparaison de la [disponibilité des fonctionnalités](#feature-availability). Pour commencer à utiliser NuGet pour consommer des packages, consultez [Installer et utiliser un package (CLI .NET)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) et [Installer et utiliser un package (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Pour commencer à créer des packages NuGet, consultez [Créer et publier un package NET Standard (interface CLI dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) et [Créer et publier un package NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Outil&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Télécharger&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Outil CLI pour les bibliothèques .NET Core et .NET Standard et tout [projet de style SDK](resources/check-project-format.md) comme celui ciblant le .NET Framework. Inclus avec le kit SDK .NET Core et fournit des fonctionnalités NuGet de base sur toutes les plateformes. (À compter de Visual Studio 2017, la CLI dotnet est installée automatiquement avec les charges de travail associées à NET Core.)| [SDK .NET Core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Outil CLI pour les bibliothèques .NET Framework et les [projets qui ne sont pas de style SDK](resources/check-project-format.md) ciblant les bibliothèques .NET Standard. Fournit toutes les fonctionnalités NuGet sous Windows et la plupart des fonctionnalités sous Mac et Linux en cas d’exécution sous Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Sous Windows, fournit des fonctionnalités NuGet par le biais de l’interface utilisateur et de la console du Gestionnaire de package ; avec des charges de travail liées à .NET. Sous Mac, fournit certaines fonctionnalités par le biais de l’interface utilisateur. Dans Visual Studio Code, les fonctionnalités NuGet sont fournies sous la forme d’extensions. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

L’[interface CLI MSBuild](reference/msbuild-targets.md) offre également la possibilité de restaurer et de créer des packages, ce qui est surtout utile sur les serveurs de build. MSBuild n’est pas un outil à usage général pour NuGet.

## <a name="cli-tools"></a>Outils de l’interface CLI

Les deux outils de l’interface CLI NuGet sont `dotnet.exe` et `nuget.exe`. Consultez la [disponibilité des fonctionnalités](#feature-availability) pour obtenir une comparaison.

* Pour cibler .NET Core ou .NET Standard, utilisez l’interface CLI dotnet. L’interface CLI dotnet est requise pour le format de projet de style SDK, qui utilise [l’attribut SDK](/dotnet/core/tools/csproj#additions).
* Pour cibler le .NET Framework (projet n’étant pas de style SDK uniquement), utilisez `nuget.exe CLI`. Si le projet est migré de `packages.config` vers PackageReference, utilisez la CLI dotnet.

### <a name="dotnetexe-cli"></a>Interface CLI de dotnet.exe

L’interface CLI de .NET Core 2.0, `dotnet.exe`, qui fonctionne sur toutes les plateformes (Windows, Mac et Linux), fournit des fonctionnalités NuGet de base comme l’installation, la restauration et la publication de packages. `dotnet` assure une intégration directe avec les fichiers projet .NET Core (par exemple, `.csproj`), ce qui est utile dans la plupart des cas. `dotnet` est également intégré directement pour chaque plateforme et ne nécessite pas l’installation de Mono.

Installation :

- Sur les ordinateurs des développeurs, installez le [kit SDK .NET Core](https://aka.ms/dotnetcoregs). À compter de Visual Studio 2017, la CLI dotnet est installée automatiquement avec les charges de travail associées à NET Core.
- Pour les serveurs de build, suivez les instructions de la rubrique [Utilisation du SDK et des outils .NET Core avec l’intégration continue](/dotnet/core/tools/using-ci-with-cli).

Pour savoir comment utiliser les commandes de base avec l’interface CLI dotnet, consultez [Installer et utiliser des packages à l’aide de l’interface CLI dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>Interface CLI de nuget.exe

L’interface CLI `nuget.exe`, `nuget.exe`, est l’utilitaire de ligne de commande pour Windows qui offre toutes les fonctionnalités NuGet. Elle peut également s’exécuter sous Mac OS X et Linux à l’aide de [Mono](http://www.mono-project.com/docs/getting-started/install/), avec certaines limitations.

Pour savoir comment utiliser les commandes de base avec l’interface CLI `nuget.exe`, consultez [Installer et utiliser des packages à l’aide de l’interface CLI nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

Installation :

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Utilisez `nuget update -self` sur Windows pour mettre à jour un nuget.exe existant vers la dernière version.

> [!Note]
> La dernière interface CLI de NuGet est toujours disponible à l’adresse `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Pour des raisons de compatibilité avec d’anciens systèmes d’intégration continue, une URL précédente, `https://nuget.org/nuget.exe`, fournit actuellement [l’outil CLI 2.8.6 déconseillé](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code : Les fonctionnalités NuGet sont disponibles via des extensions Marketplace, ou vous pouvez utiliser les outils CLI `dotnet.exe` ou `nuget.exe`.

- Visual Studio pour Mac : certaines fonctionnalités NuGet sont intégrées directement. Consultez [Inclusion d’un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough) pour une procédure pas à pas. Pour d’autres fonctionnalités, utilisez les outils CLI `dotnet.exe` ou `nuget.exe`.

- Visual Studio sur Windows : Le **Gestionnaire de package NuGet** est inclus avec Visual Studio 2012 et versions ultérieures. Visual Studio fournit l’[interface utilisateur du Gestionnaire de package](tools/package-manager-ui.md) et la [console du Gestionnaire de package](tools/package-manager-console.md) pour vous permettre d’exécuter la plupart des opérations NuGet.
  - À compter de Visual Studio 2017, le programme d’installation inclut le Gestionnaire de package NuGet avec toute charge de travail utilisant .NET. Pour effectuer une installation séparément ou vérifier que le Gestionnaire de package est installé, exécutez le programme d’installation de Visual Studio et cochez l’option sous **Composants individuels > Outils de code > Gestionnaire de package NuGet**.
  - L’interface utilisateur et la console du Gestionnaire de package sont uniques à Visual Studio sous Windows. À l’heure actuelle, elles ne sont pas disponibles dans Visual Studio pour Mac.
  - Un outil CLI est requis pour prendre en charge des fonctionnalités NuGet dans l’IDE. Vous pouvez utiliser CLI `dotnet` ou CLI `nuget.exe`. L’interface CLI `dotnet` est installée avec certaines charges de travail Visual Studio, comme .NET Core. L’interface CLI `nuget.exe` doit être installée séparément, comme décrit précédemment.
  - Les commandes de la console du Gestionnaire de package fonctionnent uniquement dans Visual Studio sous Windows et non dans d’autres environnements PowerShell.
  - Pour Visual Studio 2010 et versions antérieures, installez l’extension « NuGet Package Manager for Visual Studio ».
  - Des extensions NuGet pour Visual Studio 2013 et 2015 sont également téléchargeables sur le site [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Si vous souhaitez avoir un aperçu des fonctionnalités NuGet à venir, installez [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), qui fonctionne côte à côte avec les versions stables de Visual Studio. Pour signaler des problèmes ou partager des idées concernant les préversions, ouvrez un sujet sur le [dépôt GitHub NuGet](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Disponibilité des fonctionnalités

| Fonctionnalité | Interface CLI dotnet | Interface CLI NuGet (Windows) | Interface CLI NuGet (Mono) | Visual Studio (Windows) | Visual Studio pour Mac |
| --- | --- | --- | --- | --- | --- |
| Rechercher des packages |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Installer/désinstaller des packages | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Mettre à jour des packages | &#10004; | &#10004; | | &#10004; | &#10004; |
| Restaurer des packages | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Gérer des flux de packages (sources) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Gérer des packages sur un flux | &#10004; | &#10004; | &#10004; | | |
| Définir des clés d’API pour des flux | | &#10004; | &#10004; | | |
| Créer des packages(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Publier des packages | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Répliquer des packages |  | &#10004; | &#10004; | | |
| Gérer les dossiers *global-package* et cache | &#10004; | &#10004; | &#10004; | | |
| Gérer la configuration NuGet | | &#10004; | &#10004; | | |

(1) N’affecte pas les fichiers projet ; utilisez `dotnet.exe` à la place.

(2) Fonctionne uniquement avec un fichier `packages.config` et non avec des fichiers (`.sln`) de solution.

(3) Différentes fonctionnalités de package avancées sont disponibles via l’interface CLI uniquement si elles ne sont pas représentées dans les outils de l’interface utilisateur Visual Studio.

(4) Fonctionne avec des fichiers `.nuspec`, mais pas avec des fichiers projet.

### <a name="related-topics"></a>Rubriques connexes

- [Installer et gérer des packages à l’aide de Visual Studio](tools/package-manager-ui.md)
- [Installer et gérer des packages à l’aide de la Console du Gestionnaire de package](tools/package-manager-console.md)
- [Installer et gérer des packages à l’aide de l’interface CLI dotnet](consume-packages/install-use-packages-dotnet-cli.md)
- [Installer et gérer des packages à l’aide de l’interface CLI nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Informations de référence sur la console du Gestionnaire de package (version PowerShell)](tools/powershell-reference.md)
- [Création d’un package](create-packages/creating-a-package.md)
- [Publication d’un package](nuget-org/publish-a-package.md)

Les développeurs qui utilisent Windows peuvent également explorer [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), un outil autonome open source permettant d’explorer, de créer et de modifier des packages NuGet visuellement. Il est très utile, par exemple, pour apporter des modifications expérimentales à une structure de package sans avoir à reconstruire le package.
