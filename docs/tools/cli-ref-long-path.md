---
title: Prise en charge des chemins d’accès longs CLI de NuGet
description: Référence pour la prise en charge des chemins d’accès longs de nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453492"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="59c24-103">Prise en charge des chemins d’accès longs (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="59c24-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="59c24-104">**S’applique à :** tous les &bullet; **versions prises en charge :** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="59c24-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="59c24-105">Chemins d’accès longs NuGet.exe 4.8 ou version ultérieure prise en charge pour les fichiers et répertoires pour les scénarios tels que Pack, restauration, installation et la plupart des autres scénarios nécessitant des chemins d’accès de fichier.</span><span class="sxs-lookup"><span data-stu-id="59c24-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="59c24-106">Système d’exploitation requis</span><span class="sxs-lookup"><span data-stu-id="59c24-106">Required Operating System</span></span>

-   <span data-ttu-id="59c24-107">Windows 10 (version 1607 ou ultérieure)</span><span class="sxs-lookup"><span data-stu-id="59c24-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="59c24-108">Windows 10 (version de juillet 2015 ou version 1511) si vous mettez à niveau .NET Framework pour les versions 4.6.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="59c24-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="59c24-109">Windows Server 2016 (toutes versions)</span><span class="sxs-lookup"><span data-stu-id="59c24-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="59c24-110">Activer la stratégie de groupe « Win32 les chemins d’accès longs »</span><span class="sxs-lookup"><span data-stu-id="59c24-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="59c24-111">Vous devez activer la prise en charge des longs chemins d’accès sur ces systèmes en définissant une stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="59c24-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="59c24-112">Étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="59c24-112">Steps:</span></span>
1. <span data-ttu-id="59c24-113">Lancez **éditeur de stratégie de groupe** : tapez « Modifier la stratégie de groupe » dans la barre de recherche démarrer ou exécutez « gpedit.msc » à partir de la commande Exécuter (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="59c24-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="59c24-114">Dans le **éditeur de stratégie de groupe locale**, activer « Local ordinateur Policy/Computer Configuration/modèles d’administration/tous les chemins d’accès longs paramètres/activer Win32 ».</span><span class="sxs-lookup"><span data-stu-id="59c24-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Stratégie de chemins d’accès longs](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="59c24-116">L’activation d’autres outils de NuGet prendre en charge les chemins d’accès longs</span><span class="sxs-lookup"><span data-stu-id="59c24-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="59c24-117">Dotnet CLI prend en charge les chemins d’accès longs, quel que soit le système d’exploitation ou la version.</span><span class="sxs-lookup"><span data-stu-id="59c24-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="59c24-118">Visual Studio ou msbuild - t : restauration ne prend pas encore en charge les chemins d’accès longs.</span><span class="sxs-lookup"><span data-stu-id="59c24-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="59c24-119">Logiciel qui utilise les bibliothèques NuGet pour exécuter la restauration et autres commandes, prendra en charge les chemins d’accès long sur les mêmes systèmes NuGet.exe fonctionnant sur, si elles définissent également longPathAware dans leur fenêtre de manifeste et configurer UseLegacyPathHandling false via App.Config [ Voir plus d’informations](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="59c24-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

