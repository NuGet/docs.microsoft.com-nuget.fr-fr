---
title: NuGet cross plug-in d’authentification de plateforme
description: NuGet cross plug-ins de plateforme d’authentification pour NuGet.exe, dotnet.exe, msbuild.exe et Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: d80339eb81ade1cf2c323a604cc4fac06dcb1012
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981052"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet cross plug-in d’authentification de plateforme

Dans la version 4.8 +, NuGet tous les clients (NuGet.exe, Visual Studio, dotnet.exe et MSBuild.exe) peuvent utiliser un plug-in d’authentification créé par-dessus la [NuGet entre les plug-ins de la plateforme](NuGet-Cross-Platform-Plugins.md) modèle.

## <a name="authentication-in-dotnetexe"></a>Authentification dans dotnet.exe

Visual Studio et NuGet.exe sont par défaut interactive. NuGet.exe contiendra un commutateur pour le rendre [non interactive](../../tools/nuget-exe-CLI-Reference.md).
En outre, les plug-ins NuGet.exe et Visual Studio invitent l’utilisateur pour l’entrée.
Dans dotnet.exe il n’existe aucune invite et la valeur par défaut est non interactif.

Le mécanisme d’authentification dans dotnet.exe est un flux de l’appareil. Lors de la restauration ou ajouter l’opération de package est exécutée de manière interactive, les blocs de l’opération et les instructions à l’utilisateur comment à complète les authentifications doivent être fournies sur la ligne de commande.
Lorsque l’utilisateur termine l’authentification de l’opération continue.

Pour effectuer l’opération interactive, un doit passer `--interactive`.
Actuellement uniquement l’explicite `dotnet restore` et `dotnet add package` commandes prennent en charge un commutateur interactif.
Il n’existe aucun commutateur interactive sur `dotnet build` et `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Authentification dans MSBuild

Semblable à dotnet.exe, MSBuild.exe par défaut est non qu'interactive, le mécanisme d’authentification MSBuild.exe est flux d’appareil.
Pour permettre la restauration interrompre et attendre que l’authentification, appelez la restauration avec `msbuild /t:restore /p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Création d’un plug-in d’authentification d’inter-plateformes

Vous trouverez un exemple d’implémentation dans [plug-in du fournisseur d’informations d’identification Microsoft](https://github.com/Microsoft/artifacts-credprovider).

Il est très important que les plug-ins est conforme aux exigences de sécurité définies par les outils clients NuGet.
Le minimum nécessaire est la version pour un plug-in être un plug-in d’authentification *2.0.0*.
NuGet effectue la négociation avec le plug-in et la requête pour les revendications de l’opération prise en charge.
Reportez-vous à NuGet entre plug-in de la plateforme [messages de protocole](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) pour plus d’informations sur les messages spécifiques.

NuGet définit le niveau de journalisation et fournissent des informations de proxy pour le plug-in, le cas échéant.
Journalisation dans le package NuGet console n’est acceptable une fois que NuGet a défini le niveau de journalisation sur le plug-in.

- Comportement de .NET framework plug-in d’authentification

Dans .NET Framework, les plug-ins sont autorisés à inviter un utilisateur pour l’entrée, sous la forme d’une boîte de dialogue.

- Comportement de .NET core plug-in d’authentification

Dans .NET Core, une boîte de dialogue ne peut pas être affiché. Les plug-ins doivent utiliser des flux de l’appareil pour s’authentifier.
Le plug-in peut envoyer des messages de journal à NuGet avec des instructions pour l’utilisateur.
Notez que la journalisation est disponible une fois que le niveau de journal a été défini pour le plug-in.
NuGet ne prendra aucune entrée interactive à partir de la ligne de commande.

Lorsque le client appelle le plug-in avec une authentification obtenir d’informations d’identification, les plug-ins doivent sont conformes au commutateur interactivité et respectent le commutateur de la boîte de dialogue. 

Le tableau suivant résume comment le plug-in doit se comporter pour toutes les combinaisons.

| IsNonInteractive | CanShowDialog | Comportement de plug-in |
| ---------------- | ------------- | --------------- |
| true | true | Le commutateur IsNonInteractive est prioritaire sur le commutateur de la boîte de dialogue. Le plug-in n’est pas autorisé à afficher une boîte de dialogue. Cette combinaison est valide uniquement pour les plug-ins de .NET Framework |
| true | False | Le commutateur IsNonInteractive est prioritaire sur le commutateur de la boîte de dialogue. Le plug-in n’est pas autorisé à bloquer. Cette combinaison est uniquement valide pour plug-ins .NET Core |
| False | true | Le plug-in doit afficher une boîte de dialogue. Cette combinaison est valide uniquement pour les plug-ins de .NET Framework |
| False | False | Le plug-in doit/peut pas afficher une boîte de dialogue. Le plug-in doit utiliser des flux de l’appareil pour l’authentification en se connectant à un message d’instruction par le biais de l’enregistreur d’événements. Cette combinaison est uniquement valide pour plug-ins .NET Core |

Avant d’écrire un plug-in, consultez les spécifications suivantes.

- [Plug-in de téléchargement de Package NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet cross plat plug-in d’authentification](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
