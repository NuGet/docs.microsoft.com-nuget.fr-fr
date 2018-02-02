---
title: "Vue d’ensemble et flux de travail de la création de packages NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Vue d’ensemble du processus de création et de publication d’un package NuGet, avec des liens vers d’autres parties particulières du processus."
keywords: "Création de packages NuGet, vue d’ensemble de la création NuGet, flux de travail de la création NuGet, flux de travail de la création de packages, vue d’ensemble de la création de packages."
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 46d7737d57a91ee7b0434f4695c393423730c7bc
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="package-creation-workflow"></a>Flux de travail de la création de packages

La création d’un package commence par le code compilé (en général, des assemblys .NET) à empaqueter et à partager en utilisant la galerie nuget.org publique ou une galerie privée au sein de votre organisation. Le package peut également inclure des fichiers supplémentaires comme un fichier Lisez-moi qui s’affiche pendant son installation, ainsi que des transformations apportées à certains fichiers projet.

Un package peut également servir à uniquement extraire d’autres dépendances, sans contenir de code propre. Ce type de package est un moyen pratique de fournir un kit SDK composé de plusieurs packages indépendants. Dans d’autres cas, un package peut contenir uniquement des fichiers (`.pdb`) de symboles pour faciliter le débogage.

> [!Note]
> Lorsque vous créez un package pour qu’il soit utilisé par d’autres développeurs, il est important de comprendre que ceux-ci deviennent dépendants de votre travail. C’est pourquoi la création et la publication d’un package impliquent aussi de s’engager à corriger les bogues et à apporter d’autres mises à jour, ou tout du moins, à rendre le package disponible en open source afin que d’autres puissent participer à sa maintenance.

Dans tous les cas, la création d’un package commence par déterminer quels assemblys et autres fichiers doivent être empaquetés. Ensuite, vous créez un fichier manifeste, appelé fichier `.nuspec`, pour décrire le contenu du package, ainsi que son identificateur, son numéro de version, ses informations de copyright, ses cibles et propriétés MSBuild, etc.

Lorsque vous avez préparé tous les fichiers nécessaires dans les dossiers appropriés et que vous avez créé le fichier `.nuspec` approprié, utilisez la commande `nuget pack` (ou la [cible MSBuild pack](../reference/msbuild-targets.md)) pour tout placer dans un fichier `.nupkg`. Ensuite, vous êtes prêt à déployer le package sur l’hôte qui le met à la disposition d’autres développeurs.

> [!Tip]
> Un package NuGet portant l’extension `.nupkg` n’est qu’un fichier ZIP. Pour examiner facilement le contenu d’un package, remplacez l’extension par `.zip` et développez son contenu comme d’habitude. Veillez simplement à remodifier l’extension en `.nupkg` avant d’essayer de charger le package sur un hôte.

Pour apprendre et comprendre le processus de création, commencez par [Création d’un package](../create-packages/creating-a-package.md), qui vous guide tout au long des processus de base communs à tous les packages.

À partir de là, vous pouvez envisager plusieurs autres options pour votre package :

- [Prise en charge de plusieurs frameworks cibles](../create-packages/supporting-multiple-target-frameworks.md) décrit comment créer un package avec plusieurs variantes pour différents .NET Framework.
- [Création de packages localisés](../create-packages/creating-localized-packages.md) décrit comment structurer un package avec plusieurs ressources linguistiques et comment utiliser des packages satellites localisés distincts.
- [Packages en préversion](../create-packages/prerelease-packages.md) montre comment publier des packages alpha, bêta et rc pour les clients intéressés.
- [Transformations de fichiers sources et de configuration](../create-packages/source-and-config-file-transformations.md) décrit comment effectuer des remplacements unilatéraux de jetons dans les fichiers ajoutés à un projet et modifier `web.config` et `app.config` avec des paramètres qui s’annulent à la désinstallation du package.
- [Packages de symboles](../create-packages/symbol-packages.md) propose des conseils pour fournir des symboles relatifs à votre bibliothèque visant à permettre aux consommateurs de parcourir votre code pendant le débogage.
- [Gestion des versions de package](../reference/package-versioning.md) explique comment identifier les versions exactes que vous autorisez pour vos dépendances (autres packages que vous consommez à partir de votre package).
- [Packages natifs](../create-packages/native-packages.md) décrit le processus de création d’un package pour les consommateurs C++.

Lorsque vous êtes prêt à publier un package sur nuget.org, suivez le processus simple décrit dans [Publier un package](../create-packages/publish-a-package.md).

Si vous voulez utiliser un flux privé au lieu de nuget.org, consultez [Vue d’ensemble de l’hébergement des packages](../hosting-packages/overview.md).
