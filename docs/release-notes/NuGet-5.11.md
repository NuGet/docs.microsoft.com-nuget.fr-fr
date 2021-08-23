---
title: notes de publication de NuGet 5,11
description: notes de publication pour NuGet 5,11, y compris les nouvelles fonctionnalités, les correctifs de bogues et dcr.
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728436"
---
# <a name="nuget-511-release-notes"></a>notes de publication de NuGet 5,11

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio | Disponible dans les SDK .NET |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,11](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> installé avec Visual Studio 2019 avec la charge de travail .net Core
  
> [!NOTE]
> Visual Studio 16,11, MSBuild 16,11 et .net 5.0.400 + requièrent NuGet.exe 5,11 ou version ultérieure.

## <a name="summary-whats-new-in-511"></a>Résumé : nouveautés de 5,11

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Corrigé**

* outils-Options de >-> NuGet Gestionnaire de package chaîne est tronquée- [#10779](https://github.com/NuGet/Home/issues/10779)

* Se bloquer lorsque l’événement PackagesMissingStatusChanged est déclenché- [#10854](https://github.com/NuGet/Home/issues/10854)

* le client NuGet ignore le paramètre NO_PROXY- [#10902](https://github.com/NuGet/Home/issues/10902)

**[Liste de tous les problèmes résolus dans cette version-5,11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[Liste des validations dans cette version-5,11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>Commentaires

Vos commentaires sont très importants pour nous.  en cas de problème avec cette version, consultez nos [GitHub problèmes](https://github.com/NuGet/Home/issues) et [Visual Studio Community de développement](https://developercommunity.visualstudio.com/) pour les problèmes existants.  pour les nouveaux problèmes dans NuGet, signalez un [problème GitHub](https://github.com/NuGet/Home/issues/new).
pour les problèmes d’expérience générale NuGet, faites-le nous savoir via l’option [signaler un problème](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) qui se trouve dans votre IDE favori sous **aide > signaler un problème**.
