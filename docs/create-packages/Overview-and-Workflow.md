---
title: Vue d’ensemble et flux de travail de la création de packages NuGet
description: Vue d’ensemble du processus de création et de publication d’un package NuGet, avec des liens vers d’autres parties particulières du processus.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: e4b9f6dae3a4be69e523888cc9bd2f212b45829c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488844"
---
# <a name="package-creation-workflow"></a>Flux de travail de la création de packages

La création d’un package commence par le code compilé (en général, des assemblys .NET) à empaqueter et à partager en utilisant la galerie nuget.org publique ou une galerie privée au sein de votre organisation. Le package peut également inclure des fichiers supplémentaires comme un fichier Lisez-moi qui s’affiche pendant son installation, ainsi que des transformations apportées à certains fichiers projet.

Un package peut également servir à uniquement extraire d’autres dépendances, sans contenir de code propre. Ce type de package est un moyen pratique de fournir un kit SDK composé de plusieurs packages indépendants. Dans d’autres cas, un package peut contenir uniquement des fichiers (`.pdb`) de symboles pour faciliter le débogage.

> [!Note]
> Lorsque vous créez un package pour qu’il soit utilisé par d’autres développeurs, il est important de comprendre que ceux-ci deviennent dépendants de votre travail. C’est pourquoi la création et la publication d’un package impliquent aussi de s’engager à corriger les bogues et à apporter d’autres mises à jour, ou tout du moins, à rendre le package disponible en open source afin que d’autres puissent participer à sa maintenance.

Quel que soit le cas, la création d’un package commence par déterminer son identificateur, son numéro de version, sa licence, les informations de copyright et tout autre contenu nécessaire. Une fois que vous avez terminé, vous pouvez utiliser la commande « pack » pour placer tous les éléments dans un fichier `.nupkg`. Ce fichier peut être publié dans un flux NuGet, comme nuget.org.

> [!Tip]
> Un package NuGet portant l’extension `.nupkg` n’est qu’un fichier ZIP. Pour examiner facilement le contenu d’un package, remplacez l’extension par `.zip` et développez son contenu comme d’habitude. Veillez simplement à remodifier l’extension en `.nupkg` avant d’essayer de charger le package sur un hôte.

Pour apprendre et comprendre le processus de création, commencez par [Création d’un package](../create-packages/creating-a-package.md), qui vous guide tout au long des processus de base communs à tous les packages.

À partir de là, vous pouvez envisager plusieurs autres options pour votre package :

- [Prise en charge de plusieurs frameworks cibles](../create-packages/supporting-multiple-target-frameworks.md) décrit comment créer un package avec plusieurs variantes pour différents .NET Framework.
- [Création de packages localisés](../create-packages/creating-localized-packages.md) décrit comment structurer un package avec plusieurs ressources linguistiques et comment utiliser des packages satellites localisés distincts.
- [Packages en préversion](../create-packages/prerelease-packages.md) montre comment publier des packages alpha, bêta et rc pour les clients intéressés.
- [Transformations de fichiers sources et de configuration](../create-packages/source-and-config-file-transformations.md) décrit comment effectuer des remplacements unilatéraux de jetons dans les fichiers ajoutés à un projet et modifier `web.config` et `app.config` avec des paramètres qui s’annulent à la désinstallation du package.
- [Packages de symboles](../create-packages/symbol-packages-snupkg.md) propose des conseils pour fournir des symboles relatifs à votre bibliothèque visant à permettre aux consommateurs de parcourir votre code pendant le débogage.
- [Gestion des versions de package](../concepts/package-versioning.md) explique comment identifier les versions exactes que vous autorisez pour vos dépendances (autres packages que vous consommez à partir de votre package).
- [Packages natifs](../guides/native-packages.md) décrit le processus de création d’un package pour les consommateurs C++.
- [Signature de packages](../create-packages/sign-a-package.md) décrit le processus d’ajout d’une signature numérique à un package.

Lorsque vous êtes prêt à publier un package sur nuget.org, suivez le processus simple décrit dans [Publier un package](../nuget-org/publish-a-package.md).

Si vous voulez utiliser un flux privé au lieu de nuget.org, consultez [Vue d’ensemble de l’hébergement des packages](../hosting-packages/overview.md).
