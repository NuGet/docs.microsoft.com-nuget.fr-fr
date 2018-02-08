---
title: "Méthodes d’installation des packages NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/30/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Décrit le processus d’installation des packages NuGet dans un projet, y compris les opérations sur le disque et dans les fichiers projet applicables."
keywords: "installer NuGet, consommation de package NuGet, installation de packages NuGet, références de package NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e48bbe813168e773bc46b7fe25af29785ff75df
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Différentes méthodes d’installer un package NuGet

Les packages NuGet sont téléchargés et installés à l’aide d’une des méthodes suivantes (voir [Installer les outils clients NuGet](../install-nuget-client-tools.md) si vous ne les avez pas déjà installés) :

| Méthode | Description |
| --- | --- |
| Interface CLI de dotnet.exe<br/>`dotnet install <package_name>` | (Toutes les plateformes) Télécharge le package identifié par \<package_name\> et développe son contenu dans un dossier du répertoire actif, puis ajoute une référence au fichier projet. Télécharge et installe également les dépendances.<ul><li>[Installer et utiliser un package (interface CLI dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Commandes dotnet](../tools/dotnet-commands.md)</li></ul> |
| Interface utilisateur du Gestionnaire de package (Visual Studio) | (Windows et Mac) Fournit une interface utilisateur dans laquelle vous pouvez parcourir, sélectionner et installer des packages et leurs dépendances dans un projet. Ajoute des références aux packages installés dans le fichier projet.<ul><li>[Installer et utiliser un package (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Informations de référence sur l’interface utilisateur du Gestionnaire de package (Windows)](../tools/package-manager-ui.md)</li><li>[Inclusion d’un package NuGet dans votre projet (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Console du Gestionnaire de package (Visual Studio)<br/>`Install-Package <package_name>` | (Windows uniquement) Télécharge et installe le package identifié par \<package_name\> dans un projet spécifié dans la solution, puis ajoute une référence au fichier projet. Télécharge et installe également les dépendances.<ul><li>[Installer et utiliser un package (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Guide de la console du Gestionnaire de package](../tools/package-manager-console.md)</li></ul> |
| Interface CLI de nuget.exe<br/>`nuget install <package_name>` | (Toutes les plateformes) Télécharge le package identifié par \<package_name\> et développe son contenu dans un dossier du répertoire actif ; peut également télécharger tous les packages répertoriés dans un fichier `packages.config`. Télécharge et installe également des dépendances, mais n’apporte aucune modification aux fichiers projet.<ul><li>[commande d’installation](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Processus général d'installation

En règle générale, NuGet effectue les opérations suivantes pour installer un package :

1. Acquérir le package :
    - Vérifiez si le package demandé existe déjà dans un cache (consultez [Gestion du cache NuGet](managing-the-nuget-cache.md)).
    - Si le package n’est pas dans le cache, essayez de télécharger le package à partir des sources répertoriées dans les fichiers de configuration, en commençant par le premier dans la liste. Ce comportement vous permet d’utiliser des flux de package privés avant de rechercher un package sur nuget.org (voir [Configuration du comportement de NuGet](configuring-nuget-behavior.md)).
    - Si le package a correctement acquis à partir d’une des sources, NuGet l’ajoute au cache. Sinon, l’installation échoue.

1. Développez le package dans le projet.
    - Le développement consiste à décompresser le contenu d’un package dans un sous-dossier approprié. Une copie de l’élément `.nupkg` lui-même est également placée dans ce sous-dossier.
    - Si le package est installé dans un projet Visual Studio ou .NET Core, seuls les fichiers correspondant au framework cible du projet sont développés. Lors de l’installation à l’aide de la ligne de commande nuget.exe, tous les assemblys sont développés.

1. Si le package est installé dans Visual Studio ou l’interface CLI dotnet, une référence est ajoutée au fichier projet approprié (ou `packages.config` pour certains types de projets dans Visual Studio).

## <a name="related-topics"></a>Rubriques connexes

- [Vue d’ensemble et flux de travail de consommation de package](../consume-packages/overview-and-workflow.md)
- [Recherche et sélection des packages](../consume-packages/finding-and-choosing-packages.md)
- [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md)
- [Gestion du cache NuGet](managing-the-nuget-cache.md)
