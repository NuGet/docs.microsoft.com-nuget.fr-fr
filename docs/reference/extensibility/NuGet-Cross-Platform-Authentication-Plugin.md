---
title: Plug-in d’authentification multiplateforme NuGet
description: Plug-ins d’authentification inter-plateforme NuGet pour NuGet. exe, dotnet. exe, MSBuild. exe et Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317277"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>Plug-in d’authentification multiplateforme NuGet

Dans la version 4.8 +, tous les clients NuGet (NuGet. exe, Visual Studio, dotnet. exe et MSBuild. exe) peuvent utiliser un plug-in d’authentification basé sur le modèle de [plug-ins inter-plateforme NuGet](NuGet-Cross-Platform-Plugins.md) .

## <a name="authentication-in-dotnetexe"></a>Authentification dans dotnet. exe

Visual Studio et NuGet. exe sont interactifs par défaut. NuGet. exe contient un commutateur pour le rendre [non interactif](../nuget-exe-CLI-Reference.md).
En outre, les plug-ins NuGet. exe et Visual Studio invitent l’utilisateur à entrer des données.
Dans dotnet. exe, il n’y a aucune invite et la valeur par défaut est non interactive.

Le mécanisme d’authentification dans dotnet. exe est le workflow de l’appareil. Lorsque l’opération de restauration ou d’ajout de package est exécutée de manière interactive, l’opération se bloque et les instructions de l’utilisateur sur la façon d’effectuer les authentifications sont fournies sur la ligne de commande.
Lorsque l’utilisateur termine l’authentification, l’opération se poursuit.

Pour que l’opération soit interactive, l’une `--interactive`d’elles doit réussir.
Actuellement, seules les `dotnet restore` commandes `dotnet add package` explicites et explicites prennent en charge un commutateur interactif.
Il n’existe aucun commutateur interactif `dotnet build` sur `dotnet publish`et.

## <a name="authentication-in-msbuild"></a>Authentification dans MSBuild

À l’instar de dotnet. exe, MSBuild. exe est par défaut non interactif. le mécanisme d’authentification MSBuild. exe est le workflow de l’appareil.
Pour permettre à la restauration de s’interrompre et d’attendre l’authentification, `msbuild -t:restore -p:NuGetInteractive="true"`appelez Restore with.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Création d’un plug-in d’authentification multiplateforme

Vous trouverez un exemple d’implémentation dans le [plug-in du fournisseur d’informations d’identification Microsoft](https://github.com/Microsoft/artifacts-credprovider).

Il est très important que les plug-ins soient conformes aux exigences de sécurité stipulées par les outils clients NuGet.
La version minimale requise pour qu’un plug-in soit un plug-in d’authentification est *2.0.0*.
NuGet effectue le protocole de transfert avec le plug-in et la requête pour les revendications d’opération prises en charge.
Pour plus d’informations sur les messages spécifiques, reportez-vous aux [messages de protocole](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) du plug-in NuGet Cross Platform.

NuGet définit le niveau de journalisation et fournit les informations de proxy au plug-in, le cas échéant.
La journalisation dans la console NuGet n’est acceptable qu’une fois que NuGet a défini le niveau de journalisation sur le plug-in.

- Comportement d’authentification du plug-in .NET Framework

Dans .NET Framework, les plug-ins sont autorisés à inviter un utilisateur à entrer des données, sous la forme d’une boîte de dialogue.

- Comportement d’authentification du plug-in .NET Core

Dans .NET Core, une boîte de dialogue ne peut pas être affichée. Les plug-ins doivent utiliser le workflow de l’appareil pour s’authentifier.
Le plug-in peut envoyer des messages de journal à NuGet avec des instructions à l’utilisateur.
Notez que la journalisation est disponible une fois que le niveau de journalisation a été défini sur le plug-in.
NuGet n’effectue aucune entrée interactive à partir de la ligne de commande.

Lorsque le client appelle le plug-in avec des informations d’identification d’authentification, les plug-ins doivent être conformes au commutateur d’interactivité et respecter le commutateur de boîte de dialogue. 

Le tableau suivant résume la façon dont le plug-in doit se comporter pour toutes les combinaisons.

| IsNonInteractive | CanShowDialog | Comportement du plug-in |
| ---------------- | ------------- | --------------- |
| true | true | Le commutateur IsNonInteractive est prioritaire sur le commutateur de boîte de dialogue. Le plug-in n’est pas autorisé à dépiler une boîte de dialogue. Cette combinaison est uniquement valide pour les plug-ins .NET Framework |
| true | false | Le commutateur IsNonInteractive est prioritaire sur le commutateur de boîte de dialogue. Le plug-in n’est pas autorisé à bloquer. Cette combinaison est uniquement valide pour les plug-ins .NET Core |
| false | true | Le plug-in doit afficher une boîte de dialogue. Cette combinaison est uniquement valide pour les plug-ins .NET Framework |
| false | false | Le plug-in ne peut pas afficher une boîte de dialogue. Le plug-in doit utiliser le workflow de l’appareil pour s’authentifier en consignant un message d’instruction via l’enregistreur d’événements. Cette combinaison est uniquement valide pour les plug-ins .NET Core |

Pour plus d’informations sur l’écriture d’un plug-in, reportez-vous aux spécifications suivantes.

- [Plug-in de téléchargement de package NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Plug-in d’authentification Cross plat NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
