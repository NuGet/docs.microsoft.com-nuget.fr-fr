---
title: Notes de publication de NuGet 2.8.6
description: Notes de publication pour NuGet 2.8.6, notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546489"
---
# <a name="nuget-286-release-notes"></a>Notes de publication de NuGet 2.8.6

[Notes de publication de NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [Notes de publication de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 a été publiée le 20 juillet 2015 en tant qu’une mise à jour mineure pour notre 2.8.5 ciblés de VSIX avec certains correctifs et améliorations pour prendre en charge les packages qui peuvent être livrés avec prise en charge pour le modèle de développement Windows 10 UWP.

Cette version de l’extension de gestionnaire de package NuGet fournit la prise en charge de Visual Studio 2013 uniquement.

Dans cette version, la boîte de dialogue Gestionnaire de Package NuGet avait prend désormais en charge :

* A introduit le Moniker du Framework cible UAP pour prendre en charge le développement d’applications Windows 10.
* Points de terminaison NuGet protocol version 3
* Prise en charge de [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) attribut protocolVersion sur les sources de référentiel. Valeur par défaut est « 2 »
* Revenir au référentiel distant si une version de package requis n’est pas disponible dans le cache local