---
title: Méthodes d’installation de packages NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: overview
ms.prod: nuget
ms.technology: ''
description: Décrit le processus d’installation des packages NuGet dans un projet, y compris les opérations sur le disque et dans les fichiers projet applicables.
keywords: installer NuGet, consommation de package NuGet, installation de packages NuGet, références de package NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b8cce7bd6c1bd73eb018b8891ddd72b2f4432d55
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Différentes méthodes d’installer un package NuGet

Les packages NuGet se téléchargent et s’installent suivant les méthodes du tableau ci-dessous (consultez la page [Installer des outils clients NuGet](../install-nuget-client-tools.md) s’ils ne sont pas déjà installés). Il est possible de les récupérer dans un cache plutôt que de les télécharger.

| Méthode | Description |
| --- | --- |
| Interface CLI de dotnet.exe<br/>`dotnet add package <package_name>` | (Toutes les plateformes) Récupère le package identifié par \<package_name\> et développe son contenu dans un dossier du répertoire actif, puis ajoute une référence au fichier projet. Récupère et installe également les dépendances.<ul><li>[Installer et utiliser un package (interface CLI dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Commande dotnet add package](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Interface utilisateur du Gestionnaire de package (Visual Studio) | (Windows et Mac) Fournit une interface utilisateur permettant de parcourir, de sélectionner et d’installer des packages et leurs dépendances dans un projet à partir d’une source de package donnée. Ajoute des références aux packages installés dans le fichier projet.<ul><li>[Installer et utiliser un package (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Informations de référence sur l’interface utilisateur du Gestionnaire de package (Windows)](../tools/package-manager-ui.md)</li><li>[Inclusion d’un package NuGet dans votre projet (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Console du Gestionnaire de package (Visual Studio)<br/>`Install-Package <package_name>` | (Windows uniquement) Récupère et installe le package identifié par \<package_name\> dans un projet spécifié au sein de la solution à partir d’une source donnée, puis ajoute une référence au fichier projet. Récupère et installe également les dépendances.<ul><li>[Installer et utiliser un package (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Guide de la console du Gestionnaire de package](../tools/package-manager-console.md)</li></ul> |
| Interface CLI de nuget.exe<br/>`nuget install <package_name>` | (Toutes les plateformes) Récupère le package identifié par \<package_name\> et développe son contenu dans un dossier du répertoire actif ; peut également récupérer tous les packages listés dans un fichier `packages.config`. Récupère et installe également les dépendances, mais n’apporte aucune modification aux fichiers projet ni à `packages.config`.<ul><li>[commande d’installation](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Processus d’installation d’un package

En termes simples, les différents outils NuGet créent généralement une référence à un package dans le fichier projet ou `packages.config`, puis effectuent une restauration de package, ce qui installe le package proprement dit. `nuget install` fait figure d’exception : il développe simplement le package dans un dossier `packages`, sans modifier les autres fichiers.

Le processus général se décompose ainsi :

1. (Tous les outils à l’exception de `nuget.exe`) Enregistrez la version et l’identificateur de package dans le fichier projet ou `packages.config`.

1. Acquérir le package :
    - Déterminez si le package (en fonction du numéro de version et de l’identificateur précis) est déjà installé dans le dossier *global-packages*, comme l’explique la page [Gérer les dossiers de packages globaux et de cache](managing-the-global-packages-and-cache-folders.md).

    - Si le package ne se trouve pas dans le dossier *global-packages*, tentez de le récupérer parmi les sources listées dans les [fichiers de configuration](Configuring-NuGet-Behavior.md). Pour les sources en ligne, tentez tout d’abord de récupérer le package dans le cache, sauf si `-NoCache` est spécifié avec des commandes `nuget.exe`, ou `--no-cache` avec `dotnet restore`. (Visual Studio et `dotnet add package` utilisent toujours le cache.) Si un package est utilisé à partir du cache, « CACHE » s’affiche en sortie. Le cache a un délai d’expiration de 30 minutes.

    - Si le package ne se trouve pas dans le cache, tentez de le télécharger parmi les sources listées dans la configuration. Si un package est téléchargé, « GET » et « OK » apparaissent en sortie.

    - Si aucune source ne permet de récupérer le package, l’installation échoue à ce stade, avec une erreur du type [NU1103](../reference/errors-and-warnings.md#nu1103). Notez que les erreurs des commandes `nuget.exe` affichent uniquement la dernière source vérifiée, mais implique que le package n’était disponible dans aucune source.

    Lors de l’acquisition du package, l’ordre des sources de la configuration NuGet peut s’appliquer :
      - Pour les projets au format PackageReference, NuGet consulte les partages réseau et le dossier local de sources avant de parcourir les sources HTTP.
      - Dans le cas des projets utilisant le format de gestion `packages.config`, NuGet utilise l’ordre des sources de la configuration. Les opérations de restauration font figure d’exception : l’ordre des sources est ignoré et NuGet utilise le package provenant de la première source à répondre.
      - En règle générale, l’ordre dans lequel NuGet vérifie les sources n’est pas particulièrement explicite, car n’importe quel package donné avec un identificateur et un numéro de version spécifiques est exactement le même quelle que soit la source sur laquelle il est trouvé.

1. (Tous les outils à l’exception de `nuget.exe`) Enregistrez une copie du package et d’autres informations dans le dossier *http-cache*, comme l’explique la page [Gérer les dossiers de packages globaux et de cache](managing-the-global-packages-and-cache-folders.md).

1. S’il a été téléchargé, installez le package dans le dossier *global-packages* de l’utilisateur. NuGet crée un sous-dossier par identificateur de package, puis un sous-dossier par version installée du package.

1. Mettez à jour les dossiers et les fichiers projet :

    - Pour les projets qui utilisent PackageReference, mettez à jour le graphique de dépendance de package stocké dans `obj/project.assets.json`. Le contenu des packages proprement dits n’est copié dans aucun dossier du projet.
    - Dans le cas des projets utilisant `packages.config`, copiez les parties du package développé qui correspondent à la version cible de .NET Framework du projet dans le dossier `packages` du projet. (Si vous utilisez `nuget install`, l’ensemble du package développé est copié, car `nuget.exe` n’examine pas les fichiers projet pour identifier la version cible de .NET Framework.)
    - Mettez à jour `app.config` et/ou `web.config` si le package utilise des [transformations de fichiers config et source](../create-packages/source-and-config-file-transformations.md).

1. Installez toutes les dépendances de bas niveau qui ne sont pas déjà présentes dans le projet. Ce processus est susceptible de mettre à jour les versions de package, comme l’explique la page [Résolution de dépendances](../consume-packages/dependency-resolution.md).

1. (Visual Studio uniquement) Affichez le fichier Lisez-moi du package, le cas échéant, dans une fenêtre Visual Studio.

## <a name="related-articles"></a>Articles connexes

- [Vue d’ensemble et flux de travail de consommation de package](../consume-packages/overview-and-workflow.md)
- [Recherche et sélection des packages](../consume-packages/finding-and-choosing-packages.md)
- [Gérer les dossiers global-packages et cache NuGet](managing-the-global-packages-and-cache-folders.md)
- [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md)
