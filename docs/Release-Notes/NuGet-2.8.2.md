---
title: Notes de mise à jour de NuGet point 2.8.2
description: Notes de publication pour NuGet point 2.8.2, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-282-release-notes"></a>Notes de mise à jour de NuGet point 2.8.2

[Notes de publication NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Notes de publication](../release-notes/nuget-2.8.3.md)

NuGet point 2.8.2 a été publiée le 22 mai 2014.  Cette version inclus uniquement les modifications apportées à la ligne de commande de nuget.exe, le package NuGet.Server et autres packages NuGet.  La mise en production n’incluait pas une mise à jour de l’extension Visual Studio ou d’une extension WebMatrix.

## <a name="notable-updates"></a>Mises à jour importantes

Les mises à jour plus notables se trouvaient dans la ligne de commande de nuget.exe et package NuGet.Server (pour les flux NuGet auto-hébergé).

### <a name="important-nugetexe-bug-fixes"></a>Correctifs de bogues importants nuget.exe

1. [NuGet.exe Push échoue et effectue une nouvelle tentative](https://nuget.codeplex.com/workitem/4000)
1. [Push de NuGet.exe n’envoie pas correctement les informations d’identification de l’authentification de base](https://nuget.codeplex.com/workitem/4109)
1. [Push de NuGet.exe ne suivez redirection temporaire](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Correctif de bogue NuGet.Server important

1. [Valeur incorrecte de IsAbsoluteLatestVersion retournée par NuGet.Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Packages mis à jour

Les nuget.exe de ligne de commande et les correctifs NuGet.Server sont fournis en tant que mises à jour du package NuGet.  Autres packages de mise à jour avec le point 2.8.2 ainsi a été effectuée.

Voici la liste des packages mis à jour :

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (le package, pas l’extension)

## <a name="all-changes"></a>Toutes les modifications
Comportaient 10 problèmes résolus dans la version. Pour obtenir la liste complète des travaux les éléments corrigés dans NuGet point 2.8.2, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
