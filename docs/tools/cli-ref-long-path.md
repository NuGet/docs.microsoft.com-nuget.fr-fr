---
title: Prise en charge des chemins d’accès longs CLI de NuGet
description: Référence pour la prise en charge des chemins d’accès longs de nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547824"
---
# <a name="long-path-support-nuget-cli"></a>Prise en charge des chemins d’accès longs (interface CLI NuGet)

**S’applique à :** tous les &bullet; **versions prises en charge :** 4.8 +

Chemins d’accès longs NuGet.exe 4.8 ou version ultérieure prise en charge pour les fichiers et répertoires pour les scénarios tels que Pack, restauration, installation et la plupart des autres scénarios nécessitant des chemins d’accès de fichier.

## <a name="required-operating-system"></a>Système d’exploitation requis

-   Windows 10 (version 1607 ou ultérieure)
-   Windows 10 (version de juillet 2015 ou version 1511) si vous mettez à niveau .NET Framework pour les versions 4.6.2 ou version ultérieure.
-   Windows Server 2016 (toutes versions)

## <a name="enable-win32-long-paths-group-policy"></a>Activer la stratégie de groupe « Win32 les chemins d’accès longs »

Vous devez activer la prise en charge des longs chemins d’accès sur ces systèmes en définissant une stratégie de groupe.

Étapes suivantes :
1. Lancez **éditeur de stratégie de groupe** : tapez « Modifier la stratégie de groupe » dans la barre de recherche démarrer ou exécutez « gpedit.msc » à partir de la commande Exécuter (Windows-R).
2. Dans le **éditeur de stratégie de groupe locale**, activer « Local ordinateur Policy/Computer Configuration/modèles d’administration/tous les chemins d’accès longs paramètres/activer Win32 ».

![Stratégie de chemins d’accès longs](media/LongPathPolicy.png)


> [!Note]
> L’activation d’autres outils de NuGet prendre en charge les chemins d’accès longs
>
> -   Dotnet CLI prend en charge les chemins d’accès longs, quel que soit le système d’exploitation ou la version.
> -   / T Visual : Restore Studio ou msbuild ne prend pas encore en charge les chemins d’accès longs.
> -   Logiciel qui utilise les bibliothèques NuGet pour exécuter la restauration et autres commandes, prendra en charge les chemins d’accès long sur les mêmes systèmes NuGet.exe fonctionnant sur, si elles définissent également longPathAware dans leur fenêtre de manifeste et configurer UseLegacyPathHandling false via App.Config [ Voir plus d’informations](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

