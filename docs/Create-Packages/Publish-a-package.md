---
title: Guide pratique pour publier un package NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/5/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2342aabd-983e-4db1-9230-57c84fa36969
description: "Instructions détaillées sur la manière de publier un package NuGet sur nuget.org ou des flux privés et de gérer la propriété du package sur nuget.org."
keywords: "Publication de packages NuGet, publier un package NuGet, propriété de package NuGet, publier sur nuget.org, flux NuGet privés"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: fab25931165afb65aa3fd09c5bc37492ce814a49
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="publishing-packages"></a>Publication de packages

Une fois que vous avez [créé un package](../create-packages/creating-a-package.md) avec `nuget pack`, un processus simple permet de le mettre à la disposition d’autres développeurs, de façon publique ou privée :

- Les packages publics sont accessibles à tous les développeurs de la planète via [nuget.org](https://www.nuget.org/packages/manage/upload), comme décrit dans cette rubrique.
- Les packages privés sont disponibles uniquement pour une équipe ou organisation, via leur hébergement sur un partage de fichiers, un serveur NuGet privé, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish) ou un dépôt tiers comme myget, ProGet, Nexus Repository et Artifactory. Pour plus d’informations, consultez [Vue d’ensemble de l’hébergement des packages](../hosting-packages/overview.md).

Cette rubrique traite de la publication sur nuget.org ; pour la publication sur Visual Studio Team Services, consultez [Gestion des packages](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publier dans nuget.org

Pour nuget.org, vous devez d’abord vous [inscrire pour créer un compte gratuit](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) ou vous connecter si vous êtes déjà inscrit :

![Inscription à NuGet et emplacement de connexion](media/publish_NuGetSignIn.png)

Ensuite, vous pouvez télécharger le package via le portail web nuget.org, l’envoyer (push) à nuget.org à partir de la ligne de commande ou le publier dans le cadre d’un processus CI/CD via Visual Studio Team Services, comme décrit dans les sections suivantes.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portail web : utilisez l’onglet de chargement de package sur nuget.org :

![Charger un package avec le gestionnaire de package NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>Ligne de commande :
> [!Important]
> Pour envoyer (push) des packages à nuget.org, vous devez utiliser [nuget.exe v4.1.0 ou plus](https://www.nuget.org/downloads), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) requis.

1. Cliquez sur votre nom d’utilisateur pour accéder aux paramètres de votre compte.
2. Sous **Clé API**, cliquez sur **copier dans le Presse-papiers** pour récupérer la clé d’accès nécessaire dans l’interface CLI :

    ![Copie d’une clé API à partir des paramètres de compte](media/publish_APIKey.png)

3. À l’invite de commandes, exécutez la commande suivante :

    ```
    nuget setApiKey Your-API-Key
    ```

    Votre clé API est ainsi stockée sur l’ordinateur afin que vous n’ayez pas à répéter cette étape sur le même ordinateur.

4. Envoyez (push) votre package à la galerie NuGet à l’aide de la commande :

    ```
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

5. Avant de devenir publics, tous les packages chargés sur nuget.org sont analysés et rejetés si des virus sont détectés. Tous les packages répertoriés sur nuget.org sont aussi analysés régulièrement.

6. Dans votre compte sur nuget.org, cliquez sur **Gérer mes packages** pour voir celui que vous venez de publier ; vous recevez également un e-mail de confirmation. Notez que l’indexation de votre package peut prendre un certain temps ainsi que son apparition dans les résultats de recherche. Pendant ce délai, le message suivant s’affiche dans la page de votre package :

    ![Message indiquant qu’un package n’est pas encore indexé](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>Validation du package et indexation

Les packages envoyés à NuGet.org passent par plusieurs validations. Lorsque le package a satisfait à tous les contrôles de validation, son indexation peut prendre un certain temps ainsi que son apparition dans les résultats de recherche. Une fois que l’indexation est terminée, vous recevez un e-mail de confirmation que le package a été correctement publié. Si le package ne satisfait pas à un contrôle de validation, la page des détails du package se met à jour pour afficher l’erreur associée et vous recevez aussi un e-mail vous en informant.

La validation et l’indexation du package prend généralement moins de 15 minutes. Si la publication du package prend plus de temps que prévu, visitez [status.nuget.org](https://status.nuget.org/) pour vérifier si NuGet.org rencontre des interruptions. Si tous les systèmes sont opérationnels et que le package n’a pas été correctement publié dans l’heure, connectez-vous à NuGet.org et contactez-nous à l’aide du lien permettant de contacter le support disponible dans la page du package.

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Si vous envoyez des packages à nuget.org à l’aide de Visual Studio Team Services dans le cadre du processus d’intégration/déploiement continus (CI/CD), vous devez utiliser nuget.exe 4.1 ou une version ultérieure dans les tâches NuGet. D’autres informations sont données dans [Utilisation de la dernière version de NuGet dans votre build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Gestion des propriétaires de packages sur nuget.org

Bien que le fichier `.nuspec` de chaque package NuGet définisse les auteurs du package, la galerie nuget.org n’utilise pas ces métadonnées pour en définir la propriété. Au lieu de cela, nuget.org assigne la propriété initiale à la personne qui publie le package. Il s’agit soit de l’utilisateur connecté qui a chargé le package via l’interface utilisateur de nuget.org, soit des utilisateurs dont la clé API a été utilisée avec `nuget SetApiKey` ou `nuget push`.

Tous les propriétaires de packages disposent d’autorisations complètes sur le package, y compris d’ajout et de suppression d’autres propriétaires, ainsi que de publication de mises à jour.

Pour modifier la propriété d’un package, effectuez les opérations suivantes :

1. Connectez-vous à nuget.org avec le compte qui est le propriétaire actuel du package.
1. Cliquez sur votre nom d’utilisateur, puis sous **Gérer mes packages**, cliquez sur le package à gérer.
1. Cliquez sur le lien **Gérer les propriétaires** à gauche.

À partir de là, vous disposez de plusieurs options :

1. Pour ajouter un propriétaire, entrez le nom de leur compte NuGet, puis cliquez sur **Ajouter**. Un e-mail est envoyé à ce nouveau copropriétaire avec un lien de confirmation. Une fois la confirmation effectuée, cette personne dispose d’autorisations complètes pour ajouter et supprimer des propriétaires. (Tant que la confirmation n’est pas effectuée, la page **Gérer les propriétaires** indique « En attente d’approbation » pour cette personne).
1. Pour supprimer un propriétaire, sélectionnez son nom sous **Gérer les propriétaires** et cliquez sur **Supprimer**.
1. Pour transférer la propriété (quand elle change ou quand un package a été publié sous un compte incorrect), ajoutez simplement le nouveau propriétaire, puis une fois qu’il a confirmé sa propriété, il peut vous supprimer de la liste.

Pour affecter la propriété à une entreprise ou un groupe, créez un compte nuget.org à l’aide d’un alias de messagerie transféré aux membres d’équipe appropriés. Par exemple, les comptes [microsoft](http://nuget.org/profiles/microsoft) et [aspnet](http://nuget.org/profiles/aspnet) sont propriétaires de divers packages Microsoft ASP.NET.

### <a name="recovering-package-ownership"></a>Récupération des propriétaires des packages

Parfois, un package peut ne pas avoir de propriétaire actif. Par exemple, le propriétaire d’origine peut avoir quitté l’entreprise qui produit le package, les informations d’identification nuget.org sont perdues ou des bogues plus récents dans la galerie ont laissé un package sans propriétaire.

Si vous êtes le propriétaire légitime d’un package et que vous avez besoin d’en récupérer la propriété, utilisez le [formulaire de contact](https://www.nuget.org/policies/Contact) sur nuget.org pour expliquer votre situation à l’équipe NuGet. Nous suivons alors une procédure pour vérifier votre propriété du package, notamment en essayant de localiser le propriétaire existant par le biais de l’URL du projet du package, Twitter, un e-mail ou tout autre moyen. En cas d’échec de toutes ces options, nous pouvons vous envoyer une nouvelle invitation à devenir propriétaire.
