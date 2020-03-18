---
title: Présentation et flux de travail de l’utilisation des packages NuGet
description: Présentation du processus d’utilisation des packages NuGet dans un projet et liens vers d’autres parties du processus.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: ddd1d163e18ed4ce1e7cbf41ed152acc40c1c423
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428883"
---
# <a name="package-consumption-workflow"></a>Flux de travail de la consommation des packages

Entre nuget.org et les galeries privées de packages que votre organisation peut avoir créées, vous avez à disposition des dizaines de milliers de packages très utiles pour vos applications et vos services. Toutefois, quelle que soit la source, la consommation d’un package suit le même flux de travail général.

![Procédure comprenant l’accès à une source de package, la recherche d’un package, l’installation du package dans un projet, l’ajout d’une instruction using et les appels à l’API du package](media/Overview-01-GeneralFlow.png)

\* _Visual Studio et `dotnet.exe` uniquement. La commande `nuget install` ne modifie pas les fichiers projet ou le fichier `packages.config` ; les entrées doivent être gérées manuellement._

Pour plus d’informations, consultez [Trouver et choisir des packages](../consume-packages/finding-and-choosing-packages.md) et [Processus d’installation d’un package](../concepts/package-installation-process.md).

NuGet se souvient de l’identité et du numéro de version de chaque package installé. Il les enregistre le fichier projet (avec [PackageReference](../consume-packages/package-references-in-project-files.md)) ou dans [`packages.config`](../reference/packages-config.md), selon le type du projet et la version de NuGet. Avec NuGet 4.0+, PackageReference est recommandé, bien que cela soit configurable dans Visual Studio à l’aide de l’[interface utilisateur du Gestionnaire de package](install-use-packages-visual-studio.md). Dans tous les cas, vous pouvez rechercher dans le fichier approprié à tout moment pour voir la liste complète des dépendances de votre projet.

> [!Tip]
> Il est préférable de toujours vérifier la licence pour chaque package que vous souhaitez utiliser dans votre logiciel. Pour vérifier la licence, sur Nuget.org, cliquez sur le lien **License Info** situé à droite, dans la page de description de chaque package. Si un package ne spécifie pas les termes du contrat de licence, contactez le propriétaire du package directement à l’aide de du lien **Contact owners** (Contacter les propriétaires) dans la page du package. Microsoft ne vous accorde pas de licences de droits de propriété intellectuelle pour le compte de fournisseurs de packages tiers et n’est pas responsable des informations fournies par des tiers.

Lors de l’installation des packages, NuGet vérifie généralement si le package est déjà disponible dans son cache. Vous pouvez effacer manuellement ce cache en ligne de commande, comme l’explique la page [Gérer les dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet vérifie également que les versions cibles de .NET Framework prises en charge par le package sont compatibles avec votre projet. Si le package ne contient pas d’assemblys compatibles, NuGet affiche une erreur. Consultez [Résolution des erreurs de package incompatible](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

Lorsque vous ajoutez du code de projet à un référentiel source, vous n’incluez généralement pas les packages NuGet. Si vous décidez de cloner ultérieurement le référentiel ou d’acquérir le projet d’une autre manière (y compris avec des agents de génération sur des systèmes comme Visual Studio Team Services), vous devrez restaurer les packages avant d’exécuter une génération :

![Procédure de restauration des packages NuGet par clonage d’un référentiel et utilisation d’une commande de restauration](media/Overview-02-RestoreFlow.png)

La [restauration du package](../consume-packages/package-restore.md) utilise les informations du fichier projet ou de `packages.config` pour réinstaller toutes les dépendances. Notez qu’il existe des différences dans le processus concerné, comme décrit dans [Résolution des dépendances](../concepts/dependency-resolution.md). Par ailleurs, le diagramme ci-dessus ne montre pas de commande de restauration pour la console du Gestionnaire de package. En effet, si vous êtes dans la console, celle-ci se trouve déjà dans le contexte de Visual Studio, qui en général restaure automatiquement les packages et fournit la commande indiquée au niveau de la solution.

Il est parfois nécessaire de réinstaller les packages qui sont déjà inclus dans un projet, ce qui peut également réinstaller les dépendances. Pour cela, utilisez la commande `nuget reinstall` ou la console du Gestionnaire de package NuGet. Pour plus d’informations, consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md).

Enfin, le comportement de NuGet est régi par des fichiers `Nuget.Config`. Plusieurs fichiers peuvent être utilisés pour centraliser certains paramètres à différents niveaux, comme expliqué dans [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Méthodes d’installation d’un package NuGet

Les packages NuGet peuvent être téléchargés et installés à l’aide des méthodes présentées dans le tableau suivant.

| Outil | Description |
| --- | --- |
| [Interface CLI dotnet.exe](install-use-packages-dotnet-cli.md) | (Toutes les plateformes) Outil CLI pour les bibliothèques .NET Core et .NET Standard et pour les projets de style SDK qui ciblent le .NET Framework (consultez [Attribut Sdk](/dotnet/core/tools/csproj#additions)). Récupère le package identifié par \<package_name\> et ajoute une référence au fichier projet. Récupère et installe également les dépendances. |
| Visual Studio | (Windows et Mac) Fournit une interface utilisateur permettant de parcourir, de sélectionner et d’installer des packages et leurs dépendances dans un projet à partir d’une source de package donnée. Ajoute des références aux packages installés dans le fichier projet.<ul><li>[Installer et gérer des packages à l’aide de Visual Studio](install-use-packages-visual-studio.md)</li><li>[Inclusion d’un package NuGet dans votre projet (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Console du Gestionnaire de package (Visual Studio)](install-use-packages-powershell.md) | (Windows uniquement) Récupère et installe le package identifié par \<package_name\> dans un projet spécifié au sein de la solution à partir d’une source donnée, puis ajoute une référence au fichier projet. Récupère et installe également les dépendances. |
| [Interface CLI de nuget.exe](install-use-packages-nuget-cli.md) | (Toutes les plateformes) Outil CLI pour les bibliothèques .NET Framework et les projets qui ne sont pas de style SDK ciblant les bibliothèques .NET Standard. Récupère le package identifié par \<package_name\> et développe son contenu dans un dossier du répertoire actif. Peut également récupérer tous les packages listés dans un fichier `packages.config`. Récupère et installe également les dépendances, mais n’apporte aucune modification aux fichiers projet ni à `packages.config`. |
