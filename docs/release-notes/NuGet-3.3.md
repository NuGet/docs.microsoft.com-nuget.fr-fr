---
title: Notes de version 3.3 de NuGet
description: Notes de publication pour 3.3 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: adf193437de237ed32da481e627552a8dba6f656
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-33-release-notes"></a>Notes de version 3.3 de NuGet

[Notes de publication NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [Notes de NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md)

3.3 de NuGet a été publiée le 30 novembre 2015 avec un nombre important de l’interface d’utilisateur mises à jour et des fonctionnalités de ligne de commande ainsi un ensemble de corrections utiles aux clients NuGet.

## <a name="new-features"></a>Nouvelles fonctionnalités

* Les fournisseurs d’informations d’identification ont été introduites qui permettent aux clients de ligne de commande de NuGet être en mesure de fonctionner de manière transparente avec un flux authentifié. [Fournisseur des informations d’identification des instructions sur la façon d’installer Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) et configurer NuGet à disposition des clients sont disponibles sur NuGet Docs.

## <a name="new-user-interface-features"></a>Nouvelles fonctionnalités de l’Interface utilisateur

* Onglets séparés de parcourir, installé et mises à jour disponibles
* Met à jour de badge disponible indiquant le nombre de packages avec des mises à jour disponibles
* Badges de package dans la liste des packages pour indiquer si le package est installé, ou une mise à jour disponibles
* Télécharger le nombre et l’auteur ajouté à la liste des packages
* Numéro de version disponible la plus élevée et le numéro de version actuellement installée sur la liste des packages
* Boutons d’action pour autoriser l’installation rapide, mettre à jour et désinstaller à partir de la liste des packages
* Boutons d’action plus claire dans le volet de détails du package
* Date de mise à jour de package dans le volet de détails du package
* Consolider le panneau de configuration dans la vue de la Solution
* Grille pouvant être trié de projets et les numéros de version installée sur la vue de la solution

## <a name="new-command-line-features"></a>Nouvelles fonctionnalités de ligne de commande

Dans cette version, nous avons présenté la `add` et `init` commandes pour initialiser les référentiels basés sur le dossier comme décrit dans la [nuget.exe référence](../tools/nuget-exe-cli-reference.md). Les dépôts qui sont créés et conservés dans ce dossier de la structure sera [offrent des avantages de performances significatifs](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) comme indiqué sur notre blog.

## <a name="contentfiles"></a>Fichiers

Le contenu est désormais prise en charge dans `project.json` géré des projets à partir de la nouvelle `contentFiles` dossier et `.nuspec` `contentFiles` notation de l’élément.  Ce contenu peut être spécifié directement par l’auteur du package pour les interactions avec les systèmes de projet.  Plus d’informations sur la configuration des fichiers dans un `.nuspec` document se trouve dans le [.nuspec référence](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Gestion de Cache de variables locales de NuGet

NuGet de ligne de commande a été mis à jour pour inclure des informations sur la façon de gérer les caches locales sur une station de travail.  Plus d’informations sur la commande de variables locales est disponible dans le [référence de ligne de commande de NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Résolution des problèmes

**Problèmes importants**

* Les packages NuGet de ligne de commande restaurée prise en charge pour la restauration avec un fichier de solution sur Mono - [1543](https://github.com/NuGet/Home/issues/1543)

Vous trouverez la liste complète des problèmes qui ont été traités dans la version 3.3 sur GitHub sous le [jalon 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

La liste des problèmes corrigés dans la version de ligne de commande 3.3 sont enregistrés dans le [3.3 jalon de ligne de commande](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problèmes connus

Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)