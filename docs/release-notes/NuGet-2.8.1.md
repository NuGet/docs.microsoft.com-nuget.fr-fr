---
title: Notes de publication de NuGet 2.8.1
description: Notes de publication pour NuGet 2.8.1 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545237"
---
# <a name="nuget-281-release-notes"></a>Notes de publication de NuGet 2.8.1

[Notes de publication NuGet 2.8](../release-notes/nuget-2.8.md) | [Notes de publication de NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 a été publiée le 2 avril 2014.

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="support-for-windows-phone-81-projects"></a>Prise en charge pour les projets Windows Phone 8.1
Cette version prend désormais en charge les suivant monikers du framework cible nouvelle qui peuvent être utilisé pour les projets ciblent Windows Phone 8.1 :

* WindowsPhone81 / WP81 (pour les projets de Windows Phone basé sur Silverlight)
* WindowsPhoneApp81 / WPA81 (pour les projets d’application Windows Phone WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Mise à jour de l’Extension de WebMatrix NuGet
Cette version met à jour le client NuGet trouvé dans WebMatrix pour [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 et apporte avec elle fonctionnalités telles que les transformations XDT. Plus important encore, le 2.6.1 mises à jour core permet au client de WebMatrix installer les packages NuGet qui contiennent des versions plus récentes de la `.nuspec` schéma, qui inclut les packages NuGet ASP.NET.

Pour plus d’informations sur la mise à jour de l’Extension de WebMatrix, consultez ces spécifiques [notes de version](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Correctifs de bogues
Outre ces fonctionnalités, cette version de NuGet inclut des correctifs de bogues. Vous rencontrez des problèmes de total 16 résolus dans la version. Pour obtenir la liste complète des travaux éléments résolus dans NuGet 2.8.1, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping avec Visual Studio « 14 » CTP
Dans les CTP Visual Studio « 14 » publié en juin 3e 2014, NuGet 2.8.1 est fourni dans la zone. Les fonctionnalités il prend en charge restent dans pair avec les autres 2.8.1 VSIXes tel que celui pour Visual Studio 2013.
