---
title: Notes de publication de NuGet 3,3
description: Notes de publication de NuGet 3,3, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 482c03a4f6ca39edf317b6ef8d535e79b53d5d16
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317041"
---
# <a name="nuget-33-release-notes"></a>Notes de publication de NuGet 3,3

[Notes de publication de NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [-notes de publication de NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)

NuGet 3,3 a été publié le 30 novembre, 2015 avec un nombre important de mises à jour de l’interface utilisateur et de fonctionnalités de ligne de commande, ainsi qu’une collection de correctifs utiles pour les clients NuGet.

## <a name="new-features"></a>Nouvelles fonctionnalités

* Des fournisseurs d’informations d’identification ont été introduits, qui permettent aux clients de ligne de commande NuGet de fonctionner de manière transparente avec un flux authentifié. Les [instructions relatives à l’installation du fournisseur d’informations d’identification Visual Studio Team Services](../api/nuget-exe-credential-providers.md) et à la configuration des clients NuGet pour l’utiliser sont disponibles sur les documents NuGet.

## <a name="new-user-interface-features"></a>Nouvelles fonctionnalités de l’interface utilisateur

* Séparer les onglets disponibles parcourir, installer et mettre à jour
* Badge des mises à jour disponibles indiquant le nombre de packages avec des mises à jour disponibles
* Badges de package dans la liste des packages pour indiquer si le package est installé ou si une mise à jour est disponible
* Nombre de téléchargements et auteur ajoutés à la liste des packages
* Numéro de version disponible le plus élevé et numéro de version actuellement installé dans la liste des packages
* Boutons d’action pour permettre l’installation, la mise à jour et la désinstallation rapides dans la liste des packages
* Boutons d’action plus clairs dans le panneau Détails du package
* Date de mise à jour du package dans le panneau Détails du package
* Panneau consolider dans la vue solution
* Grille pouvant être triée des projets et numéros de version installés dans la vue de la solution

## <a name="new-command-line-features"></a>Nouvelles fonctionnalités de ligne de commande

Dans cette version, nous avons `add` introduit `init` les commandes et pour initialiser les référentiels basés sur des dossiers, comme décrit dans la [référence de NuGet. exe](../reference/nuget-exe-cli-reference.md). Les référentiels construits et gérés avec cette structure de dossiers offrent des [avantages significatifs](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) en matière de performances, comme indiqué sur notre blog.

## <a name="contentfiles"></a>ContentFiles

Le contenu est désormais pris `project.json` en charge dans les projets `contentFiles` managés par le biais de la nouvelle notation de dossier et `.nuspec` `contentFiles` d’élément.  Ce contenu peut être spécifié plus directement par l’auteur du package pour les interactions avec les systèmes de projet.  Vous trouverez plus d’informations sur la configuration de `.nuspec` contentFiles dans un document dans la [référence. NuSpec](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Gestion du cache des variables locales NuGet

La ligne de commande NuGet a été mise à jour pour inclure des informations sur la gestion des caches locaux sur une station de travail.  Vous trouverez plus d’informations sur la commande variables locales dans la référence de la [ligne de commande NuGet](../reference/cli-reference/cli-ref-locals.md).

## <a name="fixed-issues"></a>Problèmes résolus

**Problèmes notables**

* Prise en charge de la restauration de la ligne de commande NuGet pour la restauration de packages avec un fichier solution sur mono- [1543](https://github.com/NuGet/Home/issues/1543)

La liste complète des problèmes qui ont été résolus dans la version 3,3 se trouve sur GitHub, sous la [étape majeure de 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

La liste des problèmes corrigés dans la version de ligne de commande 3,3 est enregistrée dans le [jalon de ligne de commande 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problèmes connus

Nous continuons à suivre les problèmes de notre liste de problèmes GitHub qui se trouvent à l’adresse suivante:[http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)