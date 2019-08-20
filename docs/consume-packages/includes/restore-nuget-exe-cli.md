---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860579"
---
<span data-ttu-id="3fdf3-101">Utilisez la commande [restore](../../reference/cli-reference/cli-ref-restore.md), qui télécharge et installe tous les packages manquants dans le dossier *packages*.</span><span class="sxs-lookup"><span data-stu-id="3fdf3-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="3fdf3-102">Pour les projets migrés vers PackageReference, utilisez [msbuild-t:restore](../package-restore.md#restore-using-msbuild) à la place pour restaurer les packages.</span><span class="sxs-lookup"><span data-stu-id="3fdf3-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="3fdf3-103">La commande `restore` ajoute seulement les packages sur le disque, sans changer les dépendances du projet.</span><span class="sxs-lookup"><span data-stu-id="3fdf3-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="3fdf3-104">Pour restaurer les dépendances du projet, modifiez `packages.config`, puis utilisez la commande `restore`.</span><span class="sxs-lookup"><span data-stu-id="3fdf3-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="3fdf3-105">Comme avec les autres commandes CLI `nuget.exe`, ouvrez d’abord une ligne de commande et accédez au répertoire contenant votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="3fdf3-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="3fdf3-106">Pour restaurer un package à l’aide de la commande `restore` :</span><span class="sxs-lookup"><span data-stu-id="3fdf3-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```