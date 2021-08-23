---
title: Dépréciation de packages sur nuget.org
description: Description détaillée du processus d’obsolescence des packages et de la façon dont les clients affichent ces informations
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726962"
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
> Le message personnalisé s’affiche uniquement sur nuget.org, mais pas sur les clients. actuellement, les clients tels que `dotnet.exe` et les NuGet Gestionnaire de package n’affichent pas le message personnalisé.

## <a name="client-experience-for-deprecated-packages"></a>Expérience client pour les packages déconseillés
Une fois qu’un package est déconseillé, ses consommateurs en sont informés de la façon suivante (selon le client utilisé).

### <a name="visual-studio"></a>Visual Studio 
*disponible à partir de Visual Studio 2019 version 16,3*

Visual Studio vous avertit de l’utilisation d’un package obsolète sous l' `Installed` onglet. Il affiche un avertissement pour le package et ses informations d’obsolescence (notamment la raison pour laquelle il a été déconseillé et le package de remplacement à utiliser à la place, le cas échéant).

   ![packages déconseillés sur Visual Studio onglet installé du gestionnaire de package](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Disponible à partir du kit de développement logiciel (SDK) .NET 3,0*

Si vous utilisez dotnet.exe, vous pouvez exécuter la commande `dotnet list package --deprecated` sur le dossier de la solution ou du projet pour obtenir la liste des packages déconseillés, ainsi que les informations de désapprobation :

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>Transférer la popularité vers un package plus récent

Les créateurs de packages qui ont déconseillé un package hérité peuvent choisir de transférer leur « popularité » vers un package plus récent pour améliorer le classement de la recherche du package le plus récent. Cela permet aux clients de découvrir le package le plus récent au lieu du package déconseillé.

Supposons, par exemple, que j’ai deux packages :

* Mon package hérité obsolète, `Contoso.Legacy` avec 3 millions téléchargements
* Mon dernier package, `Contoso.Latest` avec 5 téléchargements

NuGet. org préfère les résultats de recherche avec des téléchargements/popularité plus élevés. À partir de la requête de recherche « contoso », mon package déconseillé `Contoso.Legacy` était probablement classé au-dessus de mon dernier package `Contoso.Latest` dans les résultats de la recherche.

Pour résoudre ce problème, je peux appliquer pour transférer la popularité de mon package hérité obsolète dans mon dernier package. Cela entraînerait un `Contoso.Latest` classement plus élevé dans les résultats de recherche, tandis que le `Contoso.Legacy` classement serait plus faible. Seuls les scores de popularité internes des packages sont affectés, le nombre de téléchargements réel pour chaque package n’est pas affecté.

> [!Note]
> Les transferts de popularité peuvent compliquer considérablement la recherche du package hérité par les consommateurs.

Consultez le tableau ci-dessous pour avoir une idée concrète de la façon dont un transfert de popularité peut avoir un impact sur les classements de recherche pour la requête « contoso » :

| Classement de la recherche    | Avant le transfert de popularité        | Après le transfert de popularité         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso. Legacy, 3 millions de téléchargements*    | *Contoso. derniers, 5 téléchargements*     |
| 2                 | Contoso. scanner, téléchargements de 2 m     | Contoso. scanner, téléchargements de 2 m     |
| 3                 | Téléchargements contoso. Core, 1.5 M     | Téléchargements contoso. Core, 1.5 M     |
| 4                 | Contoso. UI, 1 million de téléchargements          | Contoso. UI, 1 million de téléchargements          |
| ...               | ...                               | ...                               |
| 20                | *Contoso. derniers, 5 téléchargements*     | *Contoso. Legacy, 3 millions de téléchargements*    |

### <a name="popularity-transfer-application-process"></a>Processus d’application de transfert de popularité

1. Passez en revue les [exigences de transfert de popularité](#popularity-transfer-requirements).
2. Envoyez par courrier électronique [account@nuget.org](mailto:account@nuget.org) le package déconseillé dont la popularité doit être transférée, ainsi que la liste des packages stables qui doivent recevoir le transfert de popularité.

Une fois l’application envoyée, nous vous informerons de l’acceptation ou du rejet de votre application (avec les critères qui ont provoqué le rejet). Il nous arrive de poser des questions d’identification supplémentaires pour confirmer l’identité du propriétaire.

#### <a name="popularity-transfer-requirements"></a>Conditions requises pour le transfert de popularité

* Les packages hérités et les nouveaux packages doivent partager tous les propriétaires.
* Les nouveaux packages doivent être clairement liés aux packages hérités dans le nom et la fonction (par exemple, une évolution ou une nouvelle génération).
* Toutes les versions des packages hérités doivent être dépréciées et pointer vers les nouveaux packages recevant le transfert.
* le transfert de la popularité ne doit pas entraîner de confusion pour les utilisateurs de NuGet, ni endommager l’expérience de recherche NuGet.
* Les nouveaux packages doivent avoir une version stable.
* Le package hérité ne doit pas recevoir les transferts de popularité d’un autre package déconseillé.

### <a name="advanced-popularity-transfer-scenarios"></a>Scénarios avancés de transfert de popularité

#### <a name="package-consolidations"></a>Consolidations de packages

Je peux transférer la popularité de plusieurs packages dépréciés en faveur d’un seul nouveau package. Par exemple, supposons que j’ai 3 packages :

* Mon premier package hérité déconseillé, `Contoso.Legacy1`
* Mon deuxième package hérité déconseillé, `Contoso.Legacy2`
* Mon nouveau package consolidé, `Contoso.Latest`

Une fois que j’ai déconseillé `Contoso.Legacy1` et `Contoso.Legacy2` , je peux m’en demander pour transférer sa popularité à `Contoso.Latest` .

#### <a name="package-splits"></a>Fractionnements de packages

La popularité d’un package déconseillé peut être transférée vers jusqu’à 5 packages plus récents. Cela est utile si les fonctionnalités d’un package déconseillé ont été réparties entre plusieurs nouveaux packages. Par exemple, supposons que j’ai 3 packages :

* Mon package hérité obsolète, `Contoso.Legacy`
* Mon premier nouveau package, `Contoso.Web`
* Mon deuxième package, `Contoso.Cloud`

`Contoso.Legacy` comprend des fonctionnalités Web et Cloud, mais j’ai décidé de séparer cette fonctionnalité en différents packages pour la nouvelle génération. Après dépréciation `Contoso.Legacy` , je peux m’en demander pour transférer sa popularité vers `Contoso.Web` et `Contoso.Cloud` .

> [!Warning]
> La popularité transférée sera divisée uniformément entre tous les nouveaux packages. Par conséquent, nous vous recommandons de transférer la popularité de votre package obsolète vers le moins de packages possible.

#### <a name="popularity-transfer-chains"></a>Chaînes de transfert de popularité

Un package déconseillé ne peut pas transférer sa popularité s’il reçoit déjà la popularité d’un autre package déconseillé. Par exemple, imaginons que j’ai 3 packages :

* Mon package hérité obsolète, `Contoso.First`
* Mon package hérité obsolète, `Contoso.Second`
* Mon nouveau package, `Contoso.Latest`

Si `Contoso.First` transfère sa popularité à `Contoso.Second,` , `Contoso.Second` ne peut pas transférer sa popularité à `Contoso.Latest` . Au lieu de cela, nous vous recommandons de transférer la popularité de `Contoso.First` et `Contoso.Second` vers `Contoso.Latest` , conformément au scénario de [consolidation des packages](#package-consolidations) .
