---
title: "Résolution des problèmes de restauration de packages NuGet dans Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Description des erreurs courantes liées à la restauration des packages NuGet dans Visual Studio et résolution de ces erreurs."
keywords: "Restauration des packages NuGet, restauration des packages, résolution des problèmes, résoudre les problèmes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0993e2585452e3c64da28d14bb1bbe1bea27768
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="3409c-104">Résolution des erreurs de restauration de packages dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3409c-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="3409c-105">Cette page aborde les erreurs rencontrées couramment lors de la restauration de packages dans Visual Studio, ainsi que les étapes de résolution.</span><span class="sxs-lookup"><span data-stu-id="3409c-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="3409c-106">Pour savoir comment restaurer des packages, consultez [Restauration des packages](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="3409c-106">For how-to restore packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="3409c-107">Par défaut, la génération d’un projet dans Visual Studio restaure automatiquement les packages NuGet référencés dans le projet.</span><span class="sxs-lookup"><span data-stu-id="3409c-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="3409c-108">Toutefois, les générations échouent si la restauration des packages est désactivée dans les paramètres **Outils > Options > Gestionnaire de package NuGet > Restauration de package**, et si les packages nécessaires ne sont pas disponibles sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3409c-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="3409c-109">Dans ce cas, vous pouvez voir les erreurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="3409c-109">In these cases you may see the following errors:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

<span data-ttu-id="3409c-110">Pour activer la restauration des packages, ouvrez **Outils > Options > Gestionnaire de package NuGet**, puis sélectionnez les options **Autoriser NuGet à télécharger les packages manquants** et **Rechercher automatiquement les packages manquants pendant la génération dans Visual Studio** :</span><span class="sxs-lookup"><span data-stu-id="3409c-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![Activation de la restauration des packages NuGet dans Outils/Options](../consume-packages/media/restore-01-autorestoreoptions.png)
