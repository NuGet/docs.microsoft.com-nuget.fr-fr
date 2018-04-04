---
title: Guide pratique pour gérer la mise en cache des packages NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Explique comment gérer les différents caches de packages NuGet présents sur un ordinateur, qui sont utilisés lors de l’installation ou de la restauration des packages.
keywords: Cache de package NuGet, mise en cache des packages, caches NuGet, gestion des caches, cache local NuGet, cache global NuGet, commande locals NuGet, vider le cache
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09b3560d67ff8a38677dd1e27d85cdf234495aae
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2018
---
# <a name="managing-the-nuget-cache"></a>Gestion du cache NuGet

NuGet gère plusieurs caches locaux pour ne pas avoir à télécharger des packages déjà présents sur l’ordinateur et pour avoir une prise en charge en mode hors connexion. NuGet recourt automatiquement au cache en cas d’installation ou de réinstallation de packages sans connexion réseau.

Les emplacements du cache sont disponibles via la [commande locals](../tools/cli-ref-locals.md) :

```cli
nuget locals all -list
```

Voici une sortie typique :

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

Si vous rencontrez des problèmes avec l’installation des packages ou si vous voulez être sûr que vous installez les packages à partir d’une galerie à distance, utilisez l’option `locals -clear` :

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

Notez que la gestion du cache est seulement possible à partir de la ligne de commande NuGet, et non dans Visual Studio ni dans la console du gestionnaire de package. De plus, la gestion du cache 2.x n’est pas prise en charge dans NuGet 3.6 et ultérieur.

Les erreurs suivantes peuvent se produire lorsque vous utilisez `nuget locals` :

- **Échec de l’effacement des ressources locales : impossible de supprimer un ou plusieurs fichiers**
- **Le répertoire n’est pas vide**

Ces erreurs indiquent que vous n’avez pas l’autorisation de supprimer les fichiers du cache, ou qu’un ou plusieurs fichiers du cache sont actuellement utilisés par un autre processus, qui doit être fermé pour que les fichiers puissent être supprimés.
