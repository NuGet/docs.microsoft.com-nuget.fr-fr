---
title: Notes de publication NuGet 2.8.1 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet 2.8.1, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 2.8.1 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 99dd050eb06024972132d5b0dcc9f97f965adc12
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-281-release-notes"></a>Notes de mise à jour de NuGet 2.8.1

[Notes de publication NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet point 2.8.2 Notes de publication](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 a été publiée le 2 avril 2014.

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="support-for-windows-phone-81-projects"></a>Prise en charge pour les projets Windows Phone 8.1
Cette version prend désormais en charge des monikers framework cible suivant nouvelle qui peuvent être utilisé pour les projets ciblent Windows Phone 8.1 :

* WindowsPhone81 / WP81 (pour les projets de Windows Phone basés sur Silverlight)
* WindowsPhoneApp81 / WPA81 (pour les projets d’application Windows Phone WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Mise à jour de l’Extension de WebMatrix NuGet
Cette version met à jour le client NuGet trouvé dans WebMatrix pour [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 et met avec elle fonctionnalités telles que les transformations XDT. Plus important encore, le 2.6.1 mise à jour principale permet au client de WebMatrix installer les packages NuGet qui contiennent des versions plus récentes de la `.nuspec` schéma, qui inclut les packages NuGet ASP.NET.

Pour plus d’informations sur la mise à jour de l’Extension de WebMatrix, consultez spécifiques [notes de publication](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Correctifs de bogues
Outre ces fonctionnalités, cette version de NuGet inclut autres correctifs de bogues. Il existait des problèmes de total 16 traités dans la mise en production. Pour obtenir la liste complète des travaux les éléments corrigés dans NuGet 2.8.1, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping avec Visual Studio « 14 » CTP
Dans Visual Studio « 14 » CTP de juin 3e 2014 a publié, NuGet 2.8.1 est fourni dans la zone. Il prend en charge les fonctionnalités de restent dans par avec d’autres 2.8.1 VSIXes tel que celui de Visual Studio 2013.
