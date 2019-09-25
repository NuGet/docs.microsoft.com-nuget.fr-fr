---
title: Dépréciation de packages sur nuget.org
description: Description détaillée du processus d’obsolescence des packages et de la façon dont les clients affichent ces informations
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 120b463fda856fe9dd407b6eba32d60e0918f763
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248896"
---
# <a name="deprecating-packages"></a>Dépréciation des packages

Vous pouvez déconseiller un package si vous ne gérez plus un package ou si vous souhaitez inciter les consommateurs de votre package à le déplacer vers un autre package. 

La désapprobation de package est différente de la **liste** de votre package, comme expliqué ci-dessous :
* Le fait de ne pas **répertorier** un package empêche sa détection, car il est masqué dans les résultats de la recherche. 
* La **dépréciation** d’un package permet aux consommateurs existants de votre package de déterminer s’ils sont installés ou utilisés dans leurs projets. Elle leur permet également de connaître la raison de la désapprobation et un autre package recommandé tel que spécifié par vous (l’éditeur du package). La désapprobation d’un package ne déliste pas le package. 

En tant que serveur de publication, vous pouvez choisir de ne pas répertorier et de déprécier les packages.

## <a name="deprecation-workflow"></a>Flux de travail de désapprobation
1. Pour déprécier un package, accédez à **gérer les packages** et sélectionnez **dépréciation**:

    ![Accéder à l’option déprécier le package](media/deprecation-select-option.png)

2. Sélectionnez la version que vous souhaitez déprécier. Si vous souhaitez déprécier toute la version, choisissez l’option **Sélectionner toutes les versions** .

    ![Sélectionner les versions de package à déprécier](media/deprecation-select-version.png)

3. Choisissez un motif d’obsolescence. Si le package n’est plus conservé, choisissez l’option **hérité** . Si la version spécifique présente un bogue critique, choisissez l’option **a des bogues critiques** . Pour toute autre raison, sélectionnez **autre**. Vous pouvez toujours spécifier un autre package recommandé (et la même version) et un message personnalisé destiné aux propriétaires. 

    ![Sélectionner les raisons de la recommandation du package de substitution et un message personnalisé](media/deprecation-save.png)

> [!Note]
> Le message personnalisé s’affiche uniquement sur nuget.org, mais pas sur les clients. Actuellement, les clients tels `dotnet.exe` que et le gestionnaire de package NuGet n’affichent pas le message personnalisé.

## <a name="client-experience-for-deprecated-packages"></a>Expérience client pour les packages déconseillés
Une fois qu’un package est déconseillé, ses consommateurs en sont informés de la façon suivante (selon le client utilisé).

### <a name="visual-studio"></a>Visual Studio 
*Disponible à partir de Visual Studio 2019 version 16,3*

Visual Studio vous avertit de l’utilisation d’un package déconseillé sous `Installed` l’onglet. Elle vous dirigera vers le package et ses informations d’obsolescence (notamment la raison pour laquelle elle a été dépréciée et le package de remplacement à utiliser à la place, le cas échéant).

   ![Packages déconseillés sur Visual Studio onglet installé du gestionnaire de package](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Disponible à partir du kit de développement logiciel (SDK) .NET 3,0*

Si vous utilisez dotnet. exe, vous pouvez exécuter la commande `dotnet list package --deprecated` sur le dossier de la solution ou du projet pour obtenir la liste des packages déconseillés, ainsi que les informations de désapprobation :

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
