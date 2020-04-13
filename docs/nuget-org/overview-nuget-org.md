---
title: Vue d’ensemble de NuGet.org
description: Vue d’ensemble de NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427014"
---
# <a name="overview-of-nugetorg"></a>Vue d’ensemble de NuGet.org

NuGet.org est un hôte public qui héberge les packages NuGet utilisés par des millions de développeurs .NET et .NET Core chaque jour.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Rôle de NuGet.org dans l’écosystème NuGet

Dans son rôle d’hôte public, NuGet.org elle-même maintient le dépôt central de plus de 100.000 paquets uniques à [nuget.org](https://www.nuget.org). NuGet.org n’est pas le seul hôte possible pour les forfaits. La technologie NuGet vous permet également d’héberger des packages à titre privé dans le cloud (par exemple sur Azure DevOps), sur un réseau privé ou tout simplement sur votre système de fichiers local. Si vous êtes intéressé par un autre hôte ou une autre option d’hébergement, consultez [Hébergement de vos propres flux NuGet](../hosting-packages/overview.md).

NuGet.org, comme tous les autres hôtes de packages NuGet, sert de point de connexion entre les *créateurs* et les *consommateurs* de packages. Les créateurs génèrent des packages NuGet utiles et les publient. Les consommateurs recherchent des packages pratiques et compatibles sur les hôtes accessibles, les téléchargent et incluent ces packages dans leurs projets. Une fois installés dans un projet, les API des packages sont disponibles pour le reste du code du projet.

![Relation entre les créateurs de packages, les hôtes de packages et les consommateurs de packages](media/nuget-roles.png)

## <a name="accounts"></a>Comptes

Pour publier des packages sur NuGet.org, vous créez d’abord un [compte individuel (utilisateur)](individual-accounts.md). Ce compte devient votre identité sur NuGet.org.

NuGet.org vous permet également de créer un [compte d’organisation](organizations-on-nuget-org.md). Un compte d’organisation comprend un ou plusieurs comptes individuels comme membres. Ces derniers peuvent gérer un ensemble de packages tout en conservant une identité unique pour appropriation. Votre compte individuel vous permet d’être membre de plusieurs organisations.

Un package peut appartenir à un compte d’organisation ou à un compte individuel. Pour les consommateurs de packages, il n’y a aucune différence entre un compte individuel et le compte d’organisation : tous deux sont présentés comme les propriétaires (`owners`) des packages.

## <a name="api-keys"></a>Clés API

Maintenant que vous disposez d’un package NuGet (fichier *.nupkg*) à publier, publiez-le sur NuGet.org à l’aide de l’interface CLI nuget.exe ou dotnet.exe, avec une [clé API](scoped-api-keys.md) acquise sur NuGet.org.

Quand vous [publiez un package](../create-packages/creating-a-package.md), incluez la valeur de la clé API dans la commande CLI.

## <a name="id-prefixes"></a>Préfixes d’ID

Quand vous publiez des packages, vous pouvez réserver et protéger votre identité en [réservant des préfixes d’ID](id-prefix-reservation.md). Durant l’installation d’un package, les consommateurs reçoivent des informations supplémentaires indiquant que les propriétés d’identification du package qu’ils consomment ne sont pas trompeuses.

## <a name="api-endpoint-for-nugetorg"></a>Point de terminaison d’API pour NuGet.org

Pour utiliser NuGet.org comme dépôt de packages avec les clients NuGet, vous devez utiliser le point de terminaison d’API V3 suivant : 

`https://api.nuget.org/v3/index.json`

Les clients plus âgés peuvent toujours utiliser le protocole V2 pour atteindre NuGet.org. Toutefois, veuillez noter que les clients de NuGet 3.0 ou plus tard auront un service plus lent et moins fiable en utilisant le protocole V2 :

`https://www.nuget.org/api/v2` (**Le protocole V2 est déprécié !**)
