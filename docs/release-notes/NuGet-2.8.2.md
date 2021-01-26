---
title: Notes de publication de NuGet 2.8.2
description: Notes de publication pour NuGet 2.8.2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780370"
---
# <a name="nuget-282-release-notes"></a>Notes de publication de NuGet 2.8.2

Notes de publication de [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Notes de publication de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 a été publié le 22 mai 2014.  Cette version inclut uniquement les modifications apportées à la ligne de commande nuget.exe, au package NuGet. Server et à d’autres packages NuGet.  La version n’a pas inclus une extension Visual Studio ou une extension WebMatrix mise à jour.

## <a name="notable-updates"></a>Mises à jour notables

Les mises à jour les plus notable se trouvaient dans la nuget.exe ligne de commande et le package NuGet. Server (pour les flux NuGet auto-hébergés).

### <a name="important-nugetexe-bug-fixes"></a>nuget.exe importantes correctifs de bogues

1. [nuget.exe opération Push échoue et tente à nouvel essai](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe Push n’envoie pas correctement les informations d’identification d’authentification de base](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe Push ne suivra pas la redirection temporaire](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Important correctif de bogue NuGet. Server

1. [Valeur incorrecte de IsAbsoluteLatestVersion retournée par NuGet. Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Packages mis à jour

Les correctifs de ligne de commande nuget.exe et NuGet. Server sont fournis en tant que mises à jour de package NuGet.  D’autres packages ont également été mis à jour avec 2.8.2.

Voici la liste des packages mis à jour :

1. [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet. Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (le package, pas l’extension)

## <a name="all-changes"></a>Toutes les modifications
10 problèmes ont été résolus dans la version. Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2.8.2, consultez le [suivi des problèmes NuGet pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
