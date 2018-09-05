---
title: Notes de publication NuGet 3.3
description: Notes de version de NuGet 3.3, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546645"
---
# <a name="nuget-33-release-notes"></a>Notes de publication NuGet 3.3

[Notes de publication NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [Notes de publication NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 a été publiée le 30 novembre 2015 avec un nombre important de mises à jour d’interface utilisateur et des fonctionnalités de ligne de commande mais aussi un ensemble de correctifs utiles aux clients de NuGet.

## <a name="new-features"></a>Nouvelles fonctionnalités

* Les fournisseurs d’informations d’identification ont été introduites qui permettent aux clients de ligne de commande de NuGet pouvoir travailler en toute transparence avec un flux authentifié. [Obtenir des instructions sur l’installation de Visual Studio Team Services d’informations d’identification de fournisseur ](../api/nuget-exe-credential-providers.md) et configurer le package NuGet à disposition des clients sont disponibles sur NuGet Docs.

## <a name="new-user-interface-features"></a>Nouvelles fonctionnalités d’Interface utilisateur

* Onglets distincts de parcourir, installé et les mises à jour disponible
* Met à jour disponible badge indiquant le nombre de packages avec des mises à jour disponibles
* Badges de package dans la liste des packages pour indiquer si le package est installé ou a une mise à jour disponible
* Télécharger le nombre et l’auteur a ajoutés à la liste des packages
* Numéro de version disponible la plus élevée et le numéro de version actuellement installée sur la liste des packages
* Boutons d’action pour autoriser l’installation rapide, mettre à jour et désinstaller à partir de la liste des packages
* Boutons d’action plus claire dans le volet de détails du package
* Date de mise à jour de package dans le volet de détails du package
* Consolider le panneau de configuration dans la vue de la Solution
* Grille triable de projets et les numéros des versions installées sur la vue de la solution

## <a name="new-command-line-features"></a>Nouvelles fonctionnalités de ligne de commande

Dans cette version, nous avons introduit la `add` et `init` commandes pour initialiser des référentiels basés sur le dossier comme décrit dans la [nuget.exe référence](../tools/nuget-exe-cli-reference.md). Les dépôts qui sont conçus et entretenus avec ce dossier structure sera [offrent les avantages de performances significatifs](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) comme indiqué sur notre blog.

## <a name="contentfiles"></a>contentFiles

Contenu est désormais pris en charge `project.json` gérés projets via la nouvelle `contentFiles` dossier et `.nuspec` `contentFiles` notation de l’élément.  Ce contenu peut être spécifié plus directement par l’auteur du package pour les interactions avec les systèmes de projet.  Plus d’informations sur la configuration de contentFiles dans un `.nuspec` document se trouve dans le [.nuspec référence](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Gestion de Cache de variables locales de NuGet

Le package NuGet de ligne de commande a été mis à jour pour inclure des informations sur la façon de gérer les caches locaux sur une station de travail.  Plus d’informations sur la commande de variables locales sont disponibles dans le [référence de ligne de commande NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Résolution des problèmes

**Problèmes notables**

* NuGet en ligne de commande restaurée prise en charge pour la restauration de packages avec un fichier de solution sur Mono - [1543](https://github.com/NuGet/Home/issues/1543)

Vous trouverez la liste complète des problèmes qui ont été traités dans la version 3.3 sur GitHub sous le [jalon 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

La liste des problèmes corrigés dans la version de ligne de commande 3.3 sont enregistrés dans le [3.3 jalon de ligne de commande](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problèmes connus

Nous continuons à suivre les problèmes sur notre liste de problèmes GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)