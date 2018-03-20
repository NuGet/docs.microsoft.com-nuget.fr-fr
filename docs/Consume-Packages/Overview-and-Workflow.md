---
title: "Présentation et flux de travail de l’utilisation des packages NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Présentation du processus d’utilisation des packages NuGet dans un projet et liens vers d’autres parties du processus."
keywords: "Consommation des packages NuGet, présentation de la consommation NuGet, flux de travail de la consommation NuGet, flux de travail de la consommation de packages, présentation de la consommation des packages"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 731e0d3eb4ccb887624e4e46a18b4cc77857a784
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="package-consumption-workflow"></a>Flux de travail de la consommation des packages

Entre nuget.org et les galeries privées de packages que votre organisation peut avoir créées, vous avez à disposition des dizaines de milliers de packages très utiles pour vos applications et vos services. Toutefois, quelle que soit la source, la consommation d’un package suit le même flux de travail général que celui indiqué ci-dessous. Pour plus d’informations, consultez [Recherche et sélection des packages](../consume-packages/finding-and-choosing-packages.md) et [Différentes méthodes d’installer un package NuGet](ways-to-install-a-package.md).

![Procédure comprenant l’accès à une source de package, la recherche d’un package, l’installation du package dans un projet, l’ajout d’une instruction using et les appels à l’API du package](media/Overview-01-GeneralFlow.png)

\* _Sauf avec `nuget install` sur la ligne de commande, auquel cas il est nécessaire de modifier manuellement les fichiers de configuration. Consultez la [référence sur la commande install](../tools/cli-ref-install.md)._

NuGet se souvient de l’identité et du numéro de version de chaque package installé. Il les enregistre dans [`packages.config`](../reference/packages-config.md) ou dans le fichier projet, selon le type du projet et votre version de NuGet. Dans NuGet 4.0+, [le stockage des dépendances dans le fichier projet, ou PackageReference](../consume-packages/package-references-in-project-files.md) est généralement effectué par défaut, même si cette opération peut être configurée dans Visual Studio via les [options de l’interface utilisateur du Gestionnaire de package](../tools/package-manager-ui.md). Dans tous les cas, vous pouvez rechercher dans le fichier approprié à tout moment pour voir la liste complète des dépendances de votre projet.

> [!Tip]
> Il est préférable de toujours vérifier la licence pour chaque package que vous souhaitez utiliser dans votre logiciel. Pour vérifier la licence, sur Nuget.org, cliquez sur le lien **License Info** situé à droite, dans la page de description de chaque package. Si un package ne spécifie pas les termes du contrat de licence, contactez le propriétaire du package directement à l’aide de du lien **Contact owners** (Contacter les propriétaires) dans la page du package. Microsoft ne vous accorde pas de licences de droits de propriété intellectuelle pour le compte de fournisseurs de packages tiers et n’est pas responsable des informations fournies par des tiers.

Lors de l’installation des packages, NuGet vérifie généralement si le package est déjà disponible dans son cache. Vous pouvez effacer manuellement le contenu de ce cache à partir de la ligne de commande, comme décrit dans [Gestion du cache NuGet](../consume-packages/managing-the-nuget-cache.md).

NuGet vérifie également que les versions cibles de .NET Framework prises en charge par le package sont compatibles avec votre projet. Si le package ne contient pas d’assemblys compatibles, NuGet affiche un message d’erreur. Consultez [Résolution des erreurs de package incompatible](dependency-resolution.md#resolving-incompatible-package-errors).

Lorsque vous ajoutez du code de projet à un référentiel source, vous n’incluez généralement pas les packages NuGet. Si vous décidez de cloner ultérieurement le référentiel (y compris les agents de build des systèmes tels que Visual Studio Team Services), vous devez restaurer les packages avant d’exécuter une génération :

![Procédure de restauration des packages NuGet par clonage d’un référentiel et utilisation d’une commande de restauration](media/Overview-02-RestoreFlow.png)

La [restauration du package](../consume-packages/package-restore.md) utilise les informations du fichier projet ou de `packages.config` pour réinstaller toutes les dépendances. Notez qu’il existe des différences dans le processus concerné, comme décrit dans [Résolution des dépendances](../consume-packages/dependency-resolution.md).

Il est parfois nécessaire de réinstaller les packages qui sont déjà inclus dans un projet, ce qui peut également réinstaller les dépendances. Pour cela, utilisez la commande `reinstall` sur la ligne de commande NuGet ou dans la console du gestionnaire de package NuGet. Pour plus d’informations, consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md).

Enfin, le comportement de NuGet est régi par des fichiers de configuration `Nuget.Config`. Plusieurs fichiers peuvent être utilisés pour centraliser certains paramètres à différents niveaux, comme expliqué dans [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).

Bénéficiez d’un codage productif avec les packages NuGet !
