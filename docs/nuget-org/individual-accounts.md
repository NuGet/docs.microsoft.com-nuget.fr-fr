---
title: Comptes individuels
description: Des comptes individuels sur NuGet.org sont nécessaires pour publier des packages
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427134"
---
# <a name="individual-accounts"></a>Comptes individuels

Vous devez créer un compte individuel pour publier et gérer des packages sur NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Comptes individuels et comptes d’organisation

Votre compte individuel (utilisateur) est votre identité sur NuGet.org et peut être membre de plusieurs organisations. Un package peut appartenir à un compte d’organisation ou à un compte individuel. Pour les consommateurs de packages, il n’y a aucune différence entre un compte individuel et le compte d’organisation : tous deux apparaissent comme `owners` de packages.

Un compte d’organisation comprend un ou plusieurs comptes individuels comme membres. Ces membres peuvent gérer un ensemble de packages tout en conservant une identité unique pour appropriation.

## <a name="add-a-new-individual-account"></a>Ajouter un nouveau compte individuel

Pour créer un compte NuGet.org, vous devez disposer d’un compte Microsoft personnel (MSA) ou d’un compte Azure Active Directory (AAD). Si vous n’en avez pas, vous pouvez en [créer](https://signup.live.com) un. Effectuez les étapes suivantes si vous disposez d’un compte MSA ou AAD.

1. Accédez à la [page de connexion de NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Cliquez sur le bouton **Se connecter avec Microsoft**.

1. Entrez les détails de votre compte Microsoft ou Azure Active Directory.

1. Cliquez sur **Oui** pour accepter les autorisations à donner à l’application *NuGet.org*.

   ![Octroi d’autorisations à NuGet.org](media/nuget-org-permissions.png)

1. Vous allez être redirigé vers *nuget.org* et invité à inscrire un nom d’utilisateur.

1. Spécifiez le nom d’utilisateur dans la zone d’entrée. Notez que le nom d’utilisateur **est** sensible à la casse et ne peut pas être changé ou renommé ultérieurement.

   ![Spécifier un nom d’utilisateur sur NuGet.org](media/nuget-org-register.png) 

1. Cliquez sur le bouton **Inscrire**.

Vous disposez maintenant d’un compte NuGet.org. Vous pouvez effectuer la gestion des comptes dans la page des [paramètres du compte](https://www.nuget.org/account).
