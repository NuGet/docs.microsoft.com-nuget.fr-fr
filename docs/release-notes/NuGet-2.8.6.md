---
title: Notes de mise à jour de NuGet 2.8.6
description: Notes de publication pour NuGet 2.8.6, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819716"
---
# <a name="nuget-286-release-notes"></a>Notes de mise à jour de NuGet 2.8.6

[Notes de publication NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Notes de publication](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 a été publiée le 20 juillet 2015 comme une mise à jour mineure notre 2.8.5 VSIX avec certains ciblés correctifs et améliorations pour prendre en charge les packages qui peuvent être livrés avec prise en charge pour le modèle de développement Windows 10 UWP.

Cette version de l’extension de gestionnaire de package NuGet fournit la prise en charge de Visual Studio 2013 uniquement.

Dans cette version, la boîte de dialogue Gestionnaire de Package NuGet comportait prend désormais en charge :

* A introduit le Moniker du Framework cible UAP pour prendre en charge le développement d’applications Windows 10.
* Points de terminaison NuGet protocol version 3
* Prise en charge de [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) attribut protocolVersion sur des sources de référentiel. Valeur par défaut est « 2 »
* Retour à l’espace de stockage à distance, si une version de package nécessaire n’est pas disponible dans le cache local