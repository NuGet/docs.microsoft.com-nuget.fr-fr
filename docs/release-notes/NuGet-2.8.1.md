---
title: Notes de publication de NuGet 2.8.1
description: Notes de publication pour NuGet 2.8.1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776774"
---
# <a name="nuget-281-release-notes"></a>Notes de publication de NuGet 2.8.1

Notes de publication de [NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Notes de publication de NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 a été publié le 2 avril 2014.

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="support-for-windows-phone-81-projects"></a>Prise en charge des projets Windows Phone 8,1
Cette version prend désormais en charge les nouveaux monikers de Framework cible suivants qui peuvent être utilisés pour cibler des projets Windows Phone 8,1 :

* WindowsPhone81/WP81 (pour les projets de Windows Phone basés sur Silverlight)
* WindowsPhoneApp81/WPA81 (pour les projets d’application Windows Phone basés sur WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Mise à jour de l’extension NuGet WebMatrix
Cette version met à jour le client NuGet trouvé dans WebMatrix à l’aide de [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 et intègre des fonctionnalités telles que les transformations xdt. Plus important encore, la mise à jour de base de 2.6.1 permet au client WebMatrix d’installer des packages NuGet qui contiennent des versions plus récentes du `.nuspec` schéma, y compris les packages nuget ASP.net.

Pour plus d’informations sur la mise à jour de l’extension WebMatrix, consultez ces [notes de publication](../release-notes/nuget-2.6.1-for-WebMatrix.md)spécifiques.

### <a name="bug-fixes"></a>Résolutions de bogues
Outre ces fonctionnalités, cette version de NuGet comprend d’autres correctifs de bogues. 16 problèmes ont été résolus dans la version. Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2.8.1, consultez le [suivi des problèmes NuGet pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Réexpédition avec Visual Studio « 14 » CTP
Dans Visual Studio « 14 » CTP publié le 3 juin 2014, NuGet 2.8.1 est fourni dans la zone. Les fonctionnalités qu’il prend en charge restent les unes des autres avec d’autres VSIXes 2.8.1, comme celui de Visual Studio 2013.
