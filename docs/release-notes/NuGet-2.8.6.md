---
title: Notes de publication de NuGet 2.8.6
description: Notes de publication pour NuGet 2.8.6, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776699"
---
# <a name="nuget-286-release-notes"></a>Notes de publication de NuGet 2.8.6

Notes de publication de [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Notes de publication de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 a été publié le 20 juillet 2015 en tant que mise à jour mineure de notre extension 2.8.5, avec des correctifs et des améliorations ciblés pour prendre en charge les packages qui peuvent être fournis avec la prise en charge du modèle de développement UWP Windows 10.

Cette version de l’extension du gestionnaire de package NuGet prend en charge Visual Studio 2013 uniquement.

Dans cette version, la boîte de dialogue du gestionnaire de package NuGet a été ajoutée pour :

* A introduit le moniker de Framework cible UAP pour prendre en charge le développement d’applications Windows 10.
* Points de terminaison du protocole NuGet version 3
* Prise en charge de [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) attribut protocolVersion sur les sources de référentiel. La valeur par défaut est « 2 »
* Revenir au référentiel distant si une version de package requise n’est pas disponible dans le cache local