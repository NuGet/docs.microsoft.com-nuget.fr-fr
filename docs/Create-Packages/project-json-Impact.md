---
title: Impact de project.json sur les auteurs de packages NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 983485df-9375-4827-b58b-70065320ee37
description: "Informations sur la façon dont l’implémentation de project.json dans NuGet 3.x affecte les auteurs de packages, notamment en termes de fonctionnalités, de contenu et de format de package non pris en charge."
keywords: "NuGet et project.json, impact de project.json, considérations liées à la création de packages, fonctionnalités de project.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 93a4e9f9cb57c8acbe516a957e01b801bac0e116
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Impact de project.json lors de la création de packages

Le système `project.json` utilisé dans NuGet 3+ affecte les auteurs de packages de plusieurs façons, comme décrit dans les sections suivantes.

## <a name="changes-affecting-existing-packages-usage"></a>Modifications affectant l’utilisation de packages existants

Les packages NuGet traditionnels prennent en charge un ensemble de fonctionnalités qui ne sont pas reportées dans le monde transitif.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Les scripts d’installation et de désinstallation sont ignorés

Le modèle de restauration transitif, décrit dans la [résolution des dépendances](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference-and-projectjson), n’a pas le concept d’« heure d’installation du package ». Un package est soit présent, soit absent, mais il n’existe aucun processus cohérent qui se produit lorsqu’un package est installé.

De plus, les scripts d’installation étaient pris en charge uniquement dans Visual Studio. Les environnements de développement intégrés (IDE) devaient simuler l’API d’extensibilité de Visual Studio pour essayer de prendre en charge de tels scripts, et aucune prise en charge n’était disponible dans les éditeurs courants et les outils en ligne de commande.

### <a name="content-transforms-are-not-supported"></a>Les transformations de contenu ne sont pas prises en charge.

À l’instar des scripts d’installation, les transformations s’exécutent sur l’installation du package et ne sont généralement pas idempotentes. Étant donné qu’il n’existe plus d’heure d’installation, XDT Transform et d’autres fonctionnalités similaires ne sont pas prises en charge et sont ignorées si un tel package est utilisé dans un scénario transitif.


### <a name="content"></a>Contenu

Les packages NuGet traditionnels fournissent des fichiers de contenu comme des fichiers de code source et de configuration. Ils sont en général utilisés dans deux scénarios :

1. Les fichiers initiaux sont déposés dans le projet de sorte que l’utilisateur peut les modifier ultérieurement. Les fichiers de configuration par défaut en sont un exemple type.

2. Les fichiers de contenu sont utilisés comme compléments des assemblys installés dans le projet. Une image de logo utilisée par un assembly en serait un exemple.

La prise en charge du contenu est actuellement désactivée pour des raisons similaires à celle des scripts et transformations, mais nous sommes en train de la concevoir.

Les fichiers de contenu peuvent toujours être déplacés à l’intérieur des packages, même s’ils sont ignorés actuellement, mais l’utilisateur final peut toujours les copier au bon endroit.

Vous pouvez consulter une des propositions de réintégration des fichiers de contenu et suivre sa progression ici : [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Impact pour les auteurs de packages

Les packages qui utilisent les fonctionnalités ci-dessus doivent utiliser un autre mécanisme. Le plus couramment utilisé des mécanismes implique les cibles/propriétés MSBuild qui continuent d’être entièrement pris en charge. Le système de génération peut choisir d’autres conventions dans le package. C’est de cette façon que les cibles MSBuild sont prises en charge, ainsi que les analyseurs Roslyn. Il est possible de générer des packages qui prennent en charge des cibles et des analyseurs pour les scénarios `packages.config` et `project.json`.

Les packages qui essaient de modifier le projet pour en faciliter le démarrage fonctionnent généralement dans un ensemble très limité de scénarios et doivent plutôt fournir un fichier Lisez-moi ou des instructions d’utilisation du package.

La plupart des packages existants n’ont pas besoin d’utiliser le format de package décrit ci-dessous.

Le format active le contenu natif en tant que scénario de première classe. Cela signifie que les assemblys managés qui dépendent d’implémentations matérielles fournissent des implémentations binaires en même temps que les assemblys managés en fonction de la plateforme cible. Par exemple, le package System.IO.Compression utilise cette technologie. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

En résumé, si la fonctionnalité ci-dessus n’est pas indispensable, nous vous recommandons de continuer à utiliser le format de package existant, puisque le format décrit ici est pris en charge uniquement par NuGet 3.x+.

Il est possible de générer des packages utilisables pour les scénarios `packages.config` et `project.json` par ajustement, cependant il est souvent plus simple de structurer uniquement les packages de manière traditionnelle, sans les fonctionnalités dépréciées mentionnées ci-dessus.


## <a name="3x-package-format"></a>Format de package 3.x  ##

Le format de package 3.x permet plusieurs fonctionnalités supplémentaires au-delà de NuGet 2.x :

1. Définition d’un assembly de référence utilisé pour la compilation et d’un jeu d’assemblys d’implémentation utilisé pour le runtime sur différents appareils/plateformes. Ceci vous permet d’exploiter les API propres à la plateforme tout en fournissant une surface d’exposition commune à vos consommateurs. Plus précisément, cela facilite l’écriture de bibliothèques portables intermédiaires.

2. Permet aux packages de tourner sur les plateformes, par exemple les systèmes d’exploitation ou l’architecture UC.

3. Permet de séparer les implémentations spécifiques de plateforme des packages complémentaires.

4. Prise en charge des dépendances natives en tant que citoyen de première classe.