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
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Résolution des erreurs de restauration de packages dans Visual Studio

> [!Note]
> Cette page aborde les erreurs rencontrées couramment lors de la restauration de packages dans Visual Studio, ainsi que les étapes de résolution. Pour savoir comment restaurer des packages, consultez [Restauration des packages](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Par défaut, la génération d’un projet dans Visual Studio restaure automatiquement les packages NuGet référencés dans le projet. Toutefois, les générations échouent si la restauration des packages est désactivée dans les paramètres **Outils > Options > Gestionnaire de package NuGet > Restauration de package**, et si les packages nécessaires ne sont pas disponibles sur votre ordinateur. Dans ce cas, vous pouvez voir les erreurs suivantes :

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

Pour activer la restauration des packages, ouvrez **Outils > Options > Gestionnaire de package NuGet**, puis sélectionnez les options **Autoriser NuGet à télécharger les packages manquants** et **Rechercher automatiquement les packages manquants pendant la génération dans Visual Studio** :

![Activation de la restauration des packages NuGet dans Outils/Options](../consume-packages/media/restore-01-autorestoreoptions.png)
