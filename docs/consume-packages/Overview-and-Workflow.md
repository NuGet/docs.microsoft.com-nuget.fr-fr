---
title: Présentation et flux de travail de l’utilisation des packages NuGet
description: Présentation du processus d’utilisation des packages NuGet dans un projet et liens vers d’autres parties du processus.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 506a093ff4d62c10c896246f746e6765f64f33f4
ms.sourcegitcommit: a801052aa728a3a137225ca3ef3ff89f2d1c6b76
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54403162"
---
# <a name="package-consumption-workflow"></a>Flux de travail de la consommation des packages

Entre nuget.org et les galeries privées de packages que votre organisation peut avoir créées, vous avez à disposition des dizaines de milliers de packages très utiles pour vos applications et vos services. Toutefois, quelle que soit la source, la consommation d’un package suit le même flux de travail général.

![Procédure comprenant l’accès à une source de package, la recherche d’un package, l’installation du package dans un projet, l’ajout d’une instruction using et les appels à l’API du package](media/Overview-01-GeneralFlow.png)

\* _Visual Studio et `dotnet.exe` uniquement. La commande `nuget install` ne change pas les fichiers projet, ni le fichier `packages.config`. Les entrées doivent être gérées manuellement._

Pour plus d’informations, consultez les pages [Trouver et choisir des packages](../consume-packages/finding-and-choosing-packages.md) et [Différentes façons d’installer un package NuGet](ways-to-install-a-package.md).

NuGet se souvient de l’identité et du numéro de version de chaque package installé. Il les enregistre dans [`packages.config`](../reference/packages-config.md) ou dans le fichier projet (avec [PackageReference](../consume-packages/package-references-in-project-files.md)), selon le type du projet et la version de NuGet. Avec NuGet 4.0 +, PackageReference est recommandé, bien que cela soit configurable dans Visual Studio au moyen des [options de l’interface utilisateur du Gestionnaire de package](../tools/package-manager-ui.md). Dans tous les cas, vous pouvez rechercher dans le fichier approprié à tout moment pour voir la liste complète des dépendances de votre projet.

> [!Tip]
> Il est préférable de toujours vérifier la licence pour chaque package que vous souhaitez utiliser dans votre logiciel. Pour vérifier la licence, sur Nuget.org, cliquez sur le lien **License Info** situé à droite, dans la page de description de chaque package. Si un package ne spécifie pas les termes du contrat de licence, contactez le propriétaire du package directement à l’aide de du lien **Contact owners** (Contacter les propriétaires) dans la page du package. Microsoft ne vous concède aucune licence de propriété intellectuelle de fournisseurs de packages tiers et n’est pas responsable des informations fournies par des tiers.

Lors de l’installation des packages, NuGet vérifie généralement si le package est déjà disponible dans son cache. Vous pouvez effacer manuellement ce cache en ligne de commande, comme l’explique la page [Gérer les dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet vérifie également que les versions cibles de .NET Framework prises en charge par le package sont compatibles avec votre projet. Si le package ne contient pas d’assemblys compatibles, NuGet affiche une erreur. Consultez [Résolution des erreurs de package incompatible](dependency-resolution.md#resolving-incompatible-package-errors).

Lorsque vous ajoutez du code de projet à un référentiel source, vous n’incluez généralement pas les packages NuGet. Si vous décidez de cloner ultérieurement le référentiel ou d’acquérir le projet d’une autre manière (y compris avec des agents de génération sur des systèmes comme Visual Studio Team Services), vous devrez restaurer les packages avant d’exécuter une génération :

![Procédure de restauration des packages NuGet par clonage d’un référentiel et utilisation d’une commande de restauration](media/Overview-02-RestoreFlow.png)

La [restauration du package](../consume-packages/package-restore.md) utilise les informations du fichier projet ou de `packages.config` pour réinstaller toutes les dépendances. Notez qu’il existe des différences dans le processus concerné, comme décrit dans [Résolution des dépendances](../consume-packages/dependency-resolution.md). Par ailleurs, le diagramme ci-dessus ne montre pas de commande de restauration pour la console du Gestionnaire de package. En effet, si vous êtes dans la console, celle-ci se trouve déjà dans le contexte de Visual Studio, qui en général restaure automatiquement les packages et fournit la commande indiquée au niveau de la solution.

Il est parfois nécessaire de réinstaller les packages qui sont déjà inclus dans un projet, ce qui peut également réinstaller les dépendances. Pour cela, utilisez la commande `nuget reinstall` ou la console du Gestionnaire de package NuGet. Pour plus d’informations, consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md).

Enfin, le comportement de NuGet est régi par des fichiers `Nuget.Config`. Plusieurs fichiers peuvent être utilisés pour centraliser certains paramètres à différents niveaux, comme expliqué dans [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).

Bénéficiez d’un codage productif avec les packages NuGet !
