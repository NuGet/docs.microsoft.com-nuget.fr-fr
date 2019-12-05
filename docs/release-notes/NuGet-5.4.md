---
title: Notes de publication de NuGet 5,4
description: Notes de publication de NuGet 5,4, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828407"
---
# <a name="nuget-54-release-notes"></a>Notes de publication de NuGet 5,4

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio| Disponible dans les SDK .NET|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core

## <a name="summary-whats-new-in-54"></a>Résumé : nouveautés de 5,4

* Temps de chargement de solution plus rapide-la surcharge d’exécution du code NuGet pendant la première charge de la solution a été réduite par le biais de NGen partiel pour réduire le coût JIT- [#6007](https://github.com/NuGet/Home/issues/6007)

* Nouvelle fonction d’assistance : à partir d’une liste d’ID de package et de versions, récupérez les packages de niveau supérieur probables. - [#8316](https://github.com/NuGet/Home/issues/8316)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Bogues**

* Plug-in : la précision de la journalisation est désactivée sur Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)

* La suppression d’un plug-in peut parfois lever et faire échouer l’intégralité de l’opération. - [#8732](https://github.com/NuGet/Home/issues/8732)

* Arrêter l’affichage des doublons de version dans la liste des versions autorisées et bloquées dans PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)

* Le fichier de verrouillage n’est pas généré correctement-l’ordonnancement du Framework ne doit pas avoir d’impact sur la restauration avec lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)

* La validation LockFile échoue pour les projets avec <RuntimeIdentifiers> défini dans le kit de développement logiciel (SDK) 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)

* La validation de signature rejettera désormais correctement les signatures avec des horodateurs qui ont 2 valeurs sous le même OID- [#8629](https://github.com/NuGet/Home/issues/8629)

* Mettre à jour la liste de licences- [#8544](https://github.com/NuGet/Home/issues/8544)

**DCR**

* Intégration des fichiers de diagnostic à IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)

**[Liste de tous les problèmes résolus dans cette version-5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
