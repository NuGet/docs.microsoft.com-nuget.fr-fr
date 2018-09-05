---
title: Notes de publication de NuGet 2.8.2
description: Notes de publication pour NuGet 2.8.2 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551146"
---
# <a name="nuget-282-release-notes"></a>Notes de publication de NuGet 2.8.2

[Notes de publication de NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [Notes de publication de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 a été publiée le 22 mai 2014.  Cette version inclus uniquement les modifications apportées à la ligne de commande de nuget.exe, le package NuGet.Server et autres packages NuGet.  La version n’inclure pas une extension est mise à jour Visual Studio ou WebMatrix.

## <a name="notable-updates"></a>Mises à jour notables

Les mises à jour les plus importants se trouvant dans la ligne de commande de nuget.exe et le package NuGet.Server (pour les flux NuGet auto-hébergé).

### <a name="important-nugetexe-bug-fixes"></a>Correctifs de bogues importants nuget.exe

1. [NuGet.exe Push échoue et effectue une nouvelle tentative](https://nuget.codeplex.com/workitem/4000)
1. [Push de NuGet.exe n’envoie pas correctement les informations d’identification de l’authentification de base](https://nuget.codeplex.com/workitem/4109)
1. [Push de NuGet.exe ne suivez redirection temporaire](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Correctif de bogue important NuGet.Server

1. [Valeur incorrecte de IsAbsoluteLatestVersion retournée par le NuGet.Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Packages mis à jour

Les correctifs de le NuGet.Server nuget.exe de ligne de commande sont fournis en tant que mises à jour de package NuGet.  Autres packages de mise à jour avec la version 2.8.2 ainsi se sont produites.

Voici la liste des packages mis à jour :

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (le package, pas l’extension)

## <a name="all-changes"></a>Toutes les modifications
Portaient les 10 problèmes résolus dans la version. Pour obtenir la liste complète des travaux éléments résolus dans NuGet 2.8.2, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
