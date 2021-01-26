---
title: Notes de publication de NuGet 3,4
description: Notes de publication de NuGet 3,4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776419"
---
# <a name="nuget-34-release-notes"></a>Notes de publication de NuGet 3,4

Notes de publication [de NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Notes de publication de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3,4 a été publié le 30 mars 2016 dans le cadre de la version préliminaire de Visual Studio 2015 Update 2 et de Visual Studio 15 preview. il a été créé avec quelques principes dans l’esprit :

* Prise en charge multiplateforme
* Amélioration des performances
* Améliorations mineures de l’interface utilisateur

Les fonctionnalités suivantes ont été précédemment ajoutées à la version RC et ont été mises à jour ou terminées pour la version 3,4 :

## <a name="new-features"></a>Nouvelles fonctionnalités

* Les clients NuGet prennent désormais en charge l’encodage de contenu gzip à partir des référentiels
* Prise en charge des fichiers PDB des packages dans les projets xproj
* Prise en charge des actions de génération iOS et Android dans l’élément contentFiles
* Prise en charge des monikers netstandard et nestandardapp Framework

## <a name="new-user-interface-features"></a>Nouvelles fonctionnalités de l’interface utilisateur

* Amélioration significative des performances, en particulier sur les onglets installé, mises à jour et consolider
* La source de l’agrégat « toutes les sources de package » est disponible avec une fusion des résultats de recherche appropriée
* Les onglets installé et mis à jour sont désormais triés par ordre alphabétique
* Ajout d’un bouton d’actualisation permettant d’actualiser une recherche
* Dernières options de build en haut de la liste des versions

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Les packages référencés dans `project.json` et qui ont une version flottante ne sont pas mis à jour sur chaque Build. Au lieu de cela, ils sont mis à jour uniquement lorsqu’ils sont forcés à restaurer, nettoyer, régénérer ou modifier `project.json` .
* les sources de référentiel nuget.org ne sont plus contraints dans une configuration de projet lorsque vous utilisez l’interface utilisateur de configuration de NuGet.
* NuGet ne restaure plus les packages dans les projets partagés et n’écrit pas de fichier de verrouillage.
* Nous avons amélioré les défaillances du réseau et les tentatives de traitement des serveurs inaccessibles ou lents à répondre.
* Les comportements du clavier et de la souris sont améliorés dans l’interface utilisateur du gestionnaire de package Visual Studio.
* Nous prenons maintenant en charge le schéma le plus récent `project.json` dans DNX.

## <a name="breaking-changes"></a>Dernières modifications

* Les numéros de version de package sont maintenant normalisés au format *major*. *mineure*. *correctif logiciel* - *version préliminaire*   Chacune des valeurs majeures, minor et patch est traitée comme des entiers et supprime les zéros non significatifs.  Les informations de préversion sont traitées comme une chaîne et aucune modification n’est appliquée à celle-ci. Ces nombres sont utilisés dans les requêtes des clients NuGet et de la recherche fournie par le service nuget.org.  Vous trouverez plus de détails dans les documents NuGet, sous les [versions préliminaires](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problèmes connus

* **Problème :** Les utilisateurs de Windows 10 v1511 inclut peuvent rencontrer des problèmes ou même un blocage de Visual Studio avec PowerShell dans Visual Studio dans les scénarios suivants :
    * Installation/désinstallation de packages avec des scripts install.ps1/uninstall.ps1
    * Chargement de projets qui ont un script init.ps1 (comme EntityFramework)
    * Publication de contenu Web

* **Solution de contournement :** Vérifiez que les derniers correctifs sont appliqués à votre installation de Windows 10, expecially le 2016 janvier (KB 3124263) ou une mise à jour ultérieure.  Plus de détails sont disponibles sur le [problème GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problème :** Les redirections du protocole NuGet v2 sont rompues.
Les dépôts NuGet personnalisés qui redirigent les demandes vers un autre hôte n’honorent pas ces demandes.
* **Solution de contournement :**  Pour contourner ce problème, configurez l’URI du référentiel de packages dans les paramètres de façon à ce qu’il pointe vers l’emplacement du serveur Redirigé.
Pour plus d’informations, consultez [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).

Nous continuons à suivre les problèmes de notre liste de problèmes GitHub qui se trouvent à l’adresse suivante : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)