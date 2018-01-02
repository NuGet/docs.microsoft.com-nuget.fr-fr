---
title: "Résolution des problèmes de restauration de packages NuGet dans Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: "Description des erreurs courantes liées à la restauration des packages NuGet dans Visual Studio et résolution de ces erreurs."
keywords: "Restauration des packages NuGet, restauration des packages, résolution des problèmes, résoudre les problèmes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Résolution des erreurs de restauration de packages dans Visual Studio

> [!Note]
> Cette page aborde les erreurs rencontrées couramment lors de la restauration de packages dans Visual Studio, ainsi que les étapes de résolution. Pour savoir comment restaurer des packages, consultez [Restauration des packages](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).

Par défaut, la génération d’un projet dans Visual Studio restaure automatiquement les packages NuGet référencés dans le projet. Toutefois, les générations échouent si la restauration des packages est désactivée dans les paramètres **Outils > Options > Gestionnaire de package NuGet > Restauration de package**, et si les packages nécessaires ne sont pas disponibles sur votre ordinateur. Dans ce cas, vous pouvez voir les erreurs suivantes :

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

Pour activer la restauration des packages, ouvrez **Outils > Options > Gestionnaire de package NuGet**, puis sélectionnez les options **Autoriser NuGet à télécharger les packages manquants** et **Rechercher automatiquement les packages manquants pendant la génération dans Visual Studio** :

![Activation de la restauration des packages NuGet dans Outils/Options](../Consume-Packages/media/restore-01-autorestoreoptions.png)

