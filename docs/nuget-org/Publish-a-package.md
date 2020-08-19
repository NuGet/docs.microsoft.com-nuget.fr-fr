---
title: Guide pratique pour publier un package NuGet
description: Instructions détaillées sur la manière de publier un package NuGet sur nuget.org ou des flux privés et de gérer la propriété du package sur nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: dc20e43bfb43a4b6e47297fb3446319860034d46
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623022"
---
# <a name="publishing-packages"></a>Publication de packages

Une fois que vous avez créé un package et obtenu votre fichier `.nupkg`, un processus simple permet de le mettre à la disposition d’autres développeurs, de façon publique ou privée :

- Les packages publics sont à la disposition des développeurs du monde entier par le biais de [nuget.org](https://www.nuget.org/packages/manage/upload), comme l’explique cet article (NuGet 4.1.0+ requis).
- Les packages privés sont disponibles uniquement pour une équipe ou une organisation, via leur hébergement sur un partage de fichiers, un serveur NuGet privé, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) ou un dépôt tiers comme myget, ProGet, Nexus Repository ou Artifactory. Pour plus d’informations, consultez [Vue d’ensemble de l’hébergement des packages](../hosting-packages/overview.md).

Cet article traite de la publication sur nuget.org. Pour la publication sur Azure Artifacts, consultez [Gestion des packages](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publier dans nuget.org

Pour nuget.org, vous devez vous connecter avec un compte Microsoft, avec lequel vous serez invité à inscrire le compte auprès de nuget.org. Vous pouvez également vous connecter avec un compte nuget.org créé à l’aide de versions antérieures du portail.

![Emplacement de la connexion NuGet](media/publish_NuGetSignIn.png)

Ensuite, vous pouvez charger le package via le portail web nuget.org, l’envoyer (push) à nuget.org à partir de la ligne de commande (nécessite `nuget.exe` 4.1.0+), ou le publier dans le cadre d’un processus CI/CD via Azure DevOps Services, comme décrit dans les sections suivantes.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portail web : utilisez l’onglet de chargement de package sur nuget.org

1. Sélectionnez **Charger** dans le menu supérieur de nuget.org et accédez à l’emplacement du package.

    ![Charger un package sur nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org indique si le nom du package est disponible. Si ce n’est pas le cas, modifiez l’identificateur du package dans votre projet, relancez la génération et retentez le chargement.

1. Si le nom du package est disponible, nuget.org ouvre une section **Vérifier**, qui permet de consulter les métadonnées du manifeste de package. Pour modifier les métadonnées, modifiez votre projet (fichier projet ou fichier `.nuspec`), relancez la génération, recréez le package et relancez le chargement.

1. Sous **Documentation de l’importation** vous pouvez coller Markdown, pointer sur vos documents avec une URL ou charger un fichier de documentation.

1. Lorsque toutes les informations sont prêtes, sélectionnez le bouton **Envoyer**.

### <a name="command-line"></a>Ligne de commande

Pour transmettre des packages à nuget.org, vous avez d’abord besoin d’une clé API, qui est créée sur nuget.org. Vous devez utiliser dotnet.exe (.NET Core) ou nuget.exe v 4.1.0 ou version ultérieure, qui implémentent les protocoles NuGet requis.
Pour plus d’informations, consultez protocoles [.net Core](https://docs.microsoft.com/dotnet/core/install/), [nuget.exe](https://www.nuget.org/downloads)et [NuGet](../api/nuget-protocols.md).

#### <a name="create-api-keys"></a>Créer des clés API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publier avec dotnet nuget push

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publier avec nuget push

1. Dans une invite de commandes, exécutez la commande suivante en remplaçant `<your_API_key>` par la clé obtenue sur nuget.org :

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Cette commande stocke votre clé API dans votre configuration NuGet, de sorte que vous n’avez pas besoin de répéter cette étape sur le même ordinateur.

    > [!NOTE]
    > La clé API n’est pas utilisée pour l’authentification auprès du flux privé. Reportez-vous à la [ `nuget sources` commande](../reference/cli-reference/cli-ref-sources.md) pour gérer les informations d’identification pour l’authentification auprès de la source.
    > Les clés API peuvent être obtenues à partir des serveurs NuGet individuels. Pour créer et gérer APIKeys pour nuget.org, consultez [créer des clés API](#create-api-keys).

1. Envoyez (push) votre package dans la galerie NuGet à l’aide de la commande suivante :

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publier les paquets signés

Pour pouvoir envoyer les packages signés, vous devez tout d’abord [inscrire le certificat](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) utilisé pour signer les packages. 

> [!Warning]
> nuget.org rejette les packages qui ne répondent pas aux [exigences des packages signés](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Validation du package et indexation

Les packages envoyés sur nuget.org passent par plusieurs validations, notamment des contrôles antivirus. (Tous les packages présents sur nuget.org sont analysés régulièrement.)

Lorsque le package a satisfait à tous les contrôles de validation, son indexation peut prendre un certain temps ainsi que son apparition dans les résultats de recherche. Une fois que l’indexation est terminée, vous recevez un e-mail de confirmation que le package a été correctement publié. Si le package ne satisfait pas à un contrôle de validation, la page des détails du package se met à jour pour afficher l’erreur associée et vous recevez aussi un e-mail vous en informant.

La validation et l’indexation du package prend généralement moins de 15 minutes. Si la publication du package prend plus de temps que prévu, visitez [status.nuget.org](https://status.nuget.org/) pour vérifier si nuget.org rencontre des interruptions. Si tous les systèmes sont opérationnels et que le package n’a pas été correctement publié dans l’heure, connectez-vous à nuget.org et contactez-nous à l’aide du lien permettant de contacter le support disponible dans la page du package.

Pour afficher l’état d’un package, sélectionnez **gérer les packages** sous le nom de votre compte sur NuGet.org. Une fois la validation terminée, vous recevez un e-mail de confirmation.

Notez que l’indexation de votre package peut prendre un certain temps ainsi que son apparition dans les résultats de recherche. Pendant ce délai, le message suivant s’affiche dans la page de votre package :

![Message indiquant qu’un package n’est pas encore publié](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

Si vous envoyez (push) des packages à nuget.org à l’aide d’Azure DevOps Services dans le cadre du processus d’intégration et de déploiement continus (CI/CD), vous devez utiliser `nuget.exe` 4.1 ou une version ultérieure dans les tâches NuGet. D’autres informations sont données dans [Utilisation de la dernière version de NuGet dans votre build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Gestion des propriétaires de packages sur nuget.org

Bien que le fichier `.nuspec` de chaque package NuGet définisse les auteurs du package, la galerie nuget.org n’utilise pas ces métadonnées pour en définir la propriété. Au lieu de cela, nuget.org assigne la propriété initiale à la personne qui publie le package. Il s’agit soit de l’utilisateur connecté qui a chargé le package via l’interface utilisateur de nuget.org, soit des utilisateurs dont la clé API a été utilisée avec `nuget SetApiKey` ou `nuget push`.

Tous les propriétaires de packages disposent d’autorisations complètes sur le package, y compris d’ajout et de suppression d’autres propriétaires, ainsi que de publication de mises à jour.

Pour modifier la propriété d’un package, effectuez les opérations suivantes :

1. Connectez-vous à nuget.org avec le compte qui est le propriétaire actuel du package.
1. Sélectionnez le nom de votre compte, puis **Gérer les packages** et développez **Packages publiés**.
1. Sélectionnez le package que vous souhaitez gérer, puis **Gérer les propriétaires** à droite.

À partir de là, vous disposez de plusieurs options :

1. Supprimez des propriétaires listés sous **Propriétaires actuels**.
1. Ajoutez un propriétaire sous **Ajouter un propriétaire** en entrant son nom d’utilisateur et un message, puis en sélectionnant **Ajouter**. Cette action envoie un e-mail comportant un lien de confirmation à ce nouveau copropriétaire. Une fois la confirmation effectuée, cette personne dispose d’autorisations complètes pour ajouter et supprimer des propriétaires. (Tant que la confirmation n’est pas effectuée, la section **Propriétaires actuels** indique « En attente d’approbation » pour cette personne.)
1. Pour transférer la propriété (quand elle change ou qu’un package n’a pas été publié sous le bon compte), ajoutez le nouveau propriétaire ; une fois qu’il aura confirmé sa propriété, il pourra vous supprimer de la liste.

Pour affecter la propriété à une entreprise ou un groupe, créez un compte nuget.org à l’aide d’un alias de messagerie transféré aux membres d’équipe appropriés. Par exemple, les comptes [microsoft](https://nuget.org/profiles/microsoft) et [aspnet](https://nuget.org/profiles/aspnet) sont propriétaires de divers packages Microsoft ASP.NET.

### <a name="recovering-package-ownership"></a>Récupération des propriétaires des packages

Parfois, un package peut ne pas avoir de propriétaire actif. Par exemple, le propriétaire d’origine peut avoir quitté l’entreprise qui produit le package, les informations d’identification nuget.org sont perdues ou des bogues plus récents dans la galerie ont laissé un package sans propriétaire.

Si vous êtes le propriétaire légitime d’un package et que vous avez besoin d’en récupérer la propriété, utilisez le [formulaire de contact](https://www.nuget.org/policies/Contact) sur nuget.org pour expliquer votre situation à l’équipe NuGet. Nous suivons alors une procédure pour vérifier votre propriété du package, notamment en essayant de localiser le propriétaire existant par le biais de l’URL du projet du package, Twitter, un e-mail ou tout autre moyen. En cas d’échec de toutes ces options, nous pouvons vous envoyer une nouvelle invitation à devenir propriétaire.
