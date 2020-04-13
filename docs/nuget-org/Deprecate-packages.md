---
title: Déprécier les paquets sur nuget.org
description: Description détaillée du processus de dépréciation des paquets et de la façon dont les clients affichent ces informations
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096883"
---
# <a name="deprecating-packages"></a>Déprécier les paquets

Vous pouvez déprécier un forfait si vous ne conservez plus un forfait ou si vous souhaitez encourager les consommateurs de votre forfait à passer à un autre forfait. 

La dépréciation du paquet est différente de la **non-cotation de** votre colis comme expliqué ci-dessous :
* **Le déballage d’un** paquet empêche sa découverte parce qu’il est caché dans les résultats de recherche. 
* **La dépréciation d’un** paquet permet aux consommateurs existants de votre colis de savoir s’ils l’ont installé ou utilisé dans leurs projets. Il leur permet également de connaître la raison de la dépréciation et un autre paquet recommandé tel que spécifié par vous (l’éditeur de paquets). Déprécier un paquet ne désiste pas le paquet. 

En tant qu’éditeur, vous pouvez choisir de non-liste ainsi que de déprécier les paquets.

## <a name="deprecation-workflow"></a>Flux de travail de dépréciation
1. Pour déprécier un forfait, **rendez-vous** sur Gérer les forfaits et sélectionnez **Déprécation**:

    ![Aller à déprécier l’option paquet](media/deprecation-select-option.png)

2. Sélectionnez la version que vous souhaitez déprécier. Si vous souhaitez déprécier toutes les **versions, choisissez Sélectionnez toutes les versions** option.

    ![Sélectionnez des versions de paquet pour déprécier](media/deprecation-select-version.png)

3. Choisissez une raison de dépréciation. Si le paquet n’est plus maintenu, choisissez l’option **Legacy.** Si la version spécifique a un bogue critique, choisissez **l’option des bogues critiques.** Pour toute autre raison, sélectionnez **Autre**. Vous pouvez toujours spécifier un autre paquet recommandé (et la version) et un message personnalisé aux propriétaires. 

    ![Sélectionnez des raisons de recommandation de paquet alternative et de message personnalisé](media/deprecation-save.png)

> [!Note]
> Le message personnalisé n’est affiché que sur nuget.org mais pas auprès des clients. Actuellement, les `dotnet.exe` clients tels que et le gestionnaire de paquets NuGet ne montrent pas le message personnalisé.

## <a name="client-experience-for-deprecated-packages"></a>Expérience client pour les forfaits dépréciés
Une fois qu’un colis a été déprécié, ses consommateurs en sont informés de la façon suivante (selon le client utilisé).

### <a name="visual-studio"></a>Visual Studio 
*Disponible à partir de Visual Studio 2019 version 16.3*

Visual Studio met en garde contre l’utilisation `Installed` d’un paquet déprécié sur l’onglet. Il montrera un avertissement pour le paquet et ses informations de dépréciation (y compris la raison pour laquelle il a été déprécié et le paquet alternatif à utiliser à la place, si présent).

   ![Paquets dépréciés sur Visual Studio onglet installé de gestionnaire de paquets](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Disponible en commençant par .NET SDK 3.0*

Si vous utilisez dotnet.exe, vous `dotnet list package --deprecated` pouvez exécuter la commande sur la solution ou le dossier de projet pour obtenir une liste de paquets dépréciés ainsi que les informations de dépréciation:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
