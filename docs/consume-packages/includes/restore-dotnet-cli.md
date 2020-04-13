---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825169"
---
Utilisez la commande [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) pour restaurer les packages listés dans le fichier projet (consultez [PackageReference](../../consume-packages/package-references-in-project-files.md)). Avec .NET Core 2.0 et versions ultérieures, la restauration est effectuée automatiquement avec `dotnet build` et `dotnet run`. À compter de NuGet 4.0, cette commande exécute le même code que `nuget restore`.

Comme avec les autres commandes CLI `dotnet`, ouvrez d’abord une ligne de commande et accédez au répertoire contenant votre fichier projet.

Pour restaurer un package à l’aide de la commande `dotnet restore` :

```dotnetcli
dotnet restore 
```