---
title: "Guide pratique pour gérer la mise en cache des packages NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "Explique comment gérer les différents caches de packages NuGet présents sur un ordinateur, qui sont utilisés lors de l’installation ou de la restauration des packages."
keywords: Cache de package NuGet, mise en cache des packages, caches NuGet, gestion des caches, cache local NuGet, cache global NuGet, commande locals NuGet, vider le cache
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="509e4-104">Gestion du cache NuGet</span><span class="sxs-lookup"><span data-stu-id="509e4-104">Managing the NuGet cache</span></span>

<span data-ttu-id="509e4-105">NuGet gère plusieurs caches locaux pour ne pas avoir à télécharger des packages déjà présents sur l’ordinateur et pour avoir une prise en charge en mode hors connexion.</span><span class="sxs-lookup"><span data-stu-id="509e4-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="509e4-106">NuGet 2.8+ recourt automatiquement au cache lors de l’installation ou de la réinstallation de packages sans connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="509e4-106">NuGet 2.8+ automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="509e4-107">Les emplacements du cache sont disponibles via la [commande locals](../tools/cli-ref-locals.md) :</span><span class="sxs-lookup"><span data-stu-id="509e4-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```
nuget locals all -list
```

<span data-ttu-id="509e4-108">Voici une sortie typique :</span><span class="sxs-lookup"><span data-stu-id="509e4-108">Typical output is as follows:</span></span>

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

<span data-ttu-id="509e4-109">Si vous rencontrez des problèmes avec l’installation des packages ou si vous voulez être sûr que vous installez les packages à partir d’une galerie à distance, utilisez l’option `locals -clear` :</span><span class="sxs-lookup"><span data-stu-id="509e4-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="509e4-110">Notez que la gestion du cache est seulement possible à partir de la ligne de commande NuGet, et non dans Visual Studio ni dans la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="509e4-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="509e4-111">De plus, la gestion du cache 2.x n’est pas prise en charge dans NuGet 3.6 et ultérieur.</span><span class="sxs-lookup"><span data-stu-id="509e4-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="509e4-112">Les erreurs suivantes peuvent se produire lorsque vous utilisez `nuget locals` :</span><span class="sxs-lookup"><span data-stu-id="509e4-112">The following errors can occur when using `nuget locals`:</span></span>

* <span data-ttu-id="509e4-113">**Échec de l’effacement des ressources locales : impossible de supprimer un ou plusieurs fichiers**</span><span class="sxs-lookup"><span data-stu-id="509e4-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
* <span data-ttu-id="509e4-114">**Le répertoire n’est pas vide**</span><span class="sxs-lookup"><span data-stu-id="509e4-114">**The directory is not empty**</span></span>

<span data-ttu-id="509e4-115">Ces erreurs indiquent que vous n’avez pas l’autorisation de supprimer les fichiers du cache, ou qu’un ou plusieurs fichiers du cache sont actuellement utilisés par un autre processus, qui doit être fermé pour que ces fichiers puissent être supprimés.</span><span class="sxs-lookup"><span data-stu-id="509e4-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>
