---
title: Prise en charge des chemins longs de l’interface CLI NuGet
description: Référence pour la prise en charge nuget.exe des chemins d’accès longs
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238190"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="ffff6-103">Prise en charge des chemins d’accès longs (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="ffff6-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="ffff6-104">**S’applique à :** toutes les &bullet; **versions prises en charge :** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="ffff6-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="ffff6-105">NuGet.exe 4,8 et versions ultérieures prennent en charge des chemins d’accès longs pour les fichiers et les répertoires pour les scénarios tels que le Pack, la restauration, l’installation et la plupart des autres scénarios qui ont besoin de chemins d’accès</span><span class="sxs-lookup"><span data-stu-id="ffff6-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="ffff6-106">Système d’exploitation requis</span><span class="sxs-lookup"><span data-stu-id="ffff6-106">Required Operating System</span></span>

-   <span data-ttu-id="ffff6-107">Windows 10 (version 1607 ou ultérieure)</span><span class="sxs-lookup"><span data-stu-id="ffff6-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="ffff6-108">Windows 10 (version de juillet 2015 ou version 1511) si vous mettez à niveau .NET Framework vers les versions 4.6.2 ou ultérieures.</span><span class="sxs-lookup"><span data-stu-id="ffff6-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="ffff6-109">Windows Server 2016 (toutes les versions)</span><span class="sxs-lookup"><span data-stu-id="ffff6-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="ffff6-110">Activer les « chemins d’accès longs Win32 » stratégie de groupe</span><span class="sxs-lookup"><span data-stu-id="ffff6-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="ffff6-111">Vous devez activer la prise en charge des chemins d’accès longs sur ces systèmes en définissant une stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="ffff6-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="ffff6-112">Étapes :</span><span class="sxs-lookup"><span data-stu-id="ffff6-112">Steps:</span></span>
1. <span data-ttu-id="ffff6-113">Lancer l' **éditeur de stratégie de groupe** : tapez « modifier la stratégie de groupe » dans la barre de recherche, ou exécutez « gpedit. msc » à partir de la commande exécuter (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="ffff6-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="ffff6-114">Dans l' **éditeur de stratégie de groupe local** , activez « stratégie de l’ordinateur local/Configuration ordinateur/modèles d’administration/tous les paramètres/activer les chemins d’accès longs Win32 ».</span><span class="sxs-lookup"><span data-stu-id="ffff6-114">In the **Local Group Policy Editor** , enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Stratégie de chemin d’accès long](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="ffff6-116">Activation d’autres outils NuGet pour prendre en charge des chemins d’accès longs</span><span class="sxs-lookup"><span data-stu-id="ffff6-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="ffff6-117">L’interface CLI dotnet prend en charge des chemins d’accès longs, quel que soit le système d’exploitation ou la version.</span><span class="sxs-lookup"><span data-stu-id="ffff6-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="ffff6-118">Visual Studio ou `msbuild -t:restore` ne prend pas encore en charge les chemins d’accès longs.</span><span class="sxs-lookup"><span data-stu-id="ffff6-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="ffff6-119">Les logiciels qui utilisent des bibliothèques NuGet pour exécuter la restauration et d’autres commandes prennent en charge des chemins d’accès longs sur les mêmes systèmes que ceux sur lesquels NuGet.exe fonctionne, s’ils sont également définis `longPathAware` dans leur manifeste Windows et configurent `UseLegacyPathHandling` sur `false` via App.Config [afficher plus d’informations](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span><span class="sxs-lookup"><span data-stu-id="ffff6-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span></span>