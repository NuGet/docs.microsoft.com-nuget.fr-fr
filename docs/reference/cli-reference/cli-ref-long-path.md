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
# <a name="long-path-support-nuget-cli"></a>Prise en charge des chemins d’accès longs (interface CLI NuGet)

**S’applique à :** toutes les &bullet; **versions prises en charge :** 4.8 +

NuGet.exe 4,8 et versions ultérieures prennent en charge des chemins d’accès longs pour les fichiers et les répertoires pour les scénarios tels que le Pack, la restauration, l’installation et la plupart des autres scénarios qui ont besoin de chemins d’accès

## <a name="required-operating-system"></a>Système d’exploitation requis

-   Windows 10 (version 1607 ou ultérieure)
-   Windows 10 (version de juillet 2015 ou version 1511) si vous mettez à niveau .NET Framework vers les versions 4.6.2 ou ultérieures.
-   Windows Server 2016 (toutes les versions)

## <a name="enable-win32-long-paths-group-policy"></a>Activer les « chemins d’accès longs Win32 » stratégie de groupe

Vous devez activer la prise en charge des chemins d’accès longs sur ces systèmes en définissant une stratégie de groupe.

Étapes :
1. Lancer l' **éditeur de stratégie de groupe** : tapez « modifier la stratégie de groupe » dans la barre de recherche, ou exécutez « gpedit. msc » à partir de la commande exécuter (Windows-R).
2. Dans l' **éditeur de stratégie de groupe local** , activez « stratégie de l’ordinateur local/Configuration ordinateur/modèles d’administration/tous les paramètres/activer les chemins d’accès longs Win32 ».

![Stratégie de chemin d’accès long](media/LongPathPolicy.png)


> [!Note]
> Activation d’autres outils NuGet pour prendre en charge des chemins d’accès longs
>
> -   L’interface CLI dotnet prend en charge des chemins d’accès longs, quel que soit le système d’exploitation ou la version.
> -   Visual Studio ou `msbuild -t:restore` ne prend pas encore en charge les chemins d’accès longs.
> -   Les logiciels qui utilisent des bibliothèques NuGet pour exécuter la restauration et d’autres commandes prennent en charge des chemins d’accès longs sur les mêmes systèmes que ceux sur lesquels NuGet.exe fonctionne, s’ils sont également définis `longPathAware` dans leur manifeste Windows et configurent `UseLegacyPathHandling` sur `false` via App.Config [afficher plus d’informations](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)