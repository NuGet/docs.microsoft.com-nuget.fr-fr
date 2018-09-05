---
title: Notes de publication NuGet 3.4
description: Notes de publication pour NuGet 3.4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551189"
---
# <a name="nuget-34-release-notes"></a>Notes de publication NuGet 3.4

[Notes de publication NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md) | [Notes de publication de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3.4 a été publiée le 30 mars 2016 dans le cadre de Visual Studio 2015 Update 2 et de la version préliminaire de Visual Studio 15 et a été généré avec quelques principes dans l’esprit :

* Prise en charge multiplateforme
* Amélioration des performances
* Améliorations mineures de l’interface utilisateur

Les fonctionnalités suivantes ont été ajoutées précédemment dans la version RC et ont été mis à jour ou terminées pour la version 3.4 :

## <a name="new-features"></a>Nouvelles fonctionnalités

* Les clients NuGet prennent désormais en charge encodage de contenu gzip à partir de référentiels
* Prise en charge pour les fichiers PDB à partir de packages dans des projets xproj
* Actions dans l’élément contentFiles de génération de prise en charge pour iOS et Android
* Prise en charge des monikers netstandard et netstandardapp du framework

## <a name="new-user-interface-features"></a>Nouvelles fonctionnalités d’Interface utilisateur

* Améliorations significatives des performances en particulier sur les onglets installé, les mises à jour et les consolider
* Agrégation 'Toutes les Sources de Package' Source est disponible avec la fusion de résultat de recherche correcte
* Installé et onglets de mises à jour sont maintenant triés par ordre alphabétique
* Ajouter un bouton d’actualisation qui permet une recherche à être actualisé
* Dernières options de Build en haut de la liste des versions

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Les packages référencés dans `project.json` qui ont flottante version ne sera pas mise à jour sur chaque build. Au lieu de cela, ils mettent à jour uniquement lorsqu’il est forcé à restaurer, nettoyer, régénérer ou modifier `project.json`.
* sources de référentiel NuGet.org sont forcés n’est plus dans une configuration de projet lorsque vous utilisez l’interface utilisateur de configuration NuGet.
* NuGet n’est plus restaure les packages dans les projets partagés ni écrit un fichier de verrouillage.
* Nous avez amélioré défaillance réseau et réessayez de gestion pour les serveurs inaccessibles ou ralentir pour répondre.
* Comportements de clavier et souris sont améliorées dans le Gestionnaire de Package Visual Studio UI.
* Nous prennent désormais en charge la dernière version `project.json` schéma dans DNX.

## <a name="breaking-changes"></a>Modifications avec rupture

* Les numéros de version de package sont normalisées maintenant au format *majeure*. *mineure*. *correctif*-*préliminaire* chacun des majeure, mineure et apporter des correctifs sont traités comme des entiers et supprimer les zéros non significatifs.  Les informations de préversion sont traitées comme une chaîne et aucune modification n’est appliquées à ce dernier. Ces nombres sont utilisés dans les requêtes par les clients NuGet et la recherche fournies par le service de nuget.org.  Vous trouverez plus de détails dans la documentation de NuGet sous [Versions de la version préliminaire](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problèmes connus

* **Problème :** Windows 10 v1511 inclut utilisateurs peuvent rencontrer des problèmes ou même un blocage de Visual Studio avec Powershell dans Visual Studio dans les scénarios suivants :
    * L’installation / désinstallation des packages qui ont Install.ps1 / uninstall.ps1 scripts
    * Chargement des projets qui ont un script init.ps1 (comme Entity Framework)
    * Publication de contenu web

* **Solution de contournement :** vous assurer que votre installation de Windows 10 a les derniers correctifs appliqués, spécialement les janvier 2016 (KB 3124263) ou une mise à jour ultérieure.  Informations supplémentaires sont disponibles sur [problème GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problème :** Les redirections du protocole NuGet v2 sont rompues.
Les dépôts NuGet personnalisés qui redirigent les demandes vers un autre hôte n’honorent pas ces demandes.
* **Solution de contournement :** pour contourner ce problème, configurez l’URI de dépôt de packages dans les paramètres pour pointer vers l’emplacement de serveur redirigé.
Pour plus d’informations, consultez [demande de tirage GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

Nous continuons à suivre les problèmes sur notre liste de problèmes GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)