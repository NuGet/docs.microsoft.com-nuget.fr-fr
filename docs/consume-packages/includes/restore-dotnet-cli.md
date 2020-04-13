---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825169"
---
<span data-ttu-id="5f3db-101">Utilisez la commande [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) pour restaurer les packages listés dans le fichier projet (consultez [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="5f3db-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="5f3db-102">Avec .NET Core 2.0 et versions ultérieures, la restauration est effectuée automatiquement avec `dotnet build` et `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="5f3db-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="5f3db-103">À compter de NuGet 4.0, cette commande exécute le même code que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="5f3db-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="5f3db-104">Comme avec les autres commandes CLI `dotnet`, ouvrez d’abord une ligne de commande et accédez au répertoire contenant votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="5f3db-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="5f3db-105">Pour restaurer un package à l’aide de la commande `dotnet restore` :</span><span class="sxs-lookup"><span data-stu-id="5f3db-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```