---
title: Notes de publication NuGet 3.4 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 80a429f5-7569-4349-ad7f-4fe9218eac23
description: "Notes de version de NuGet 3.4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 3.4, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 911e4377ad9c8b1f865b0721f43ff73b62df6d1e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-release-notes"></a>Notes de publication NuGet 3.4

[Notes de publication NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Notes de publication](../release-notes/nuget-3.4.1.md)

NuGet 3.4 a été publiée le 30 mars 2016 en tant que partie de la version préliminaire de Visual Studio 15 et de Visual Studio 2015 Update 2 et a été généré avec quelques principes dans esprit :

*  Prise en charge multiplateforme
*  Amélioration des performances
*  Petites améliorations de l’interface utilisateur

Les fonctionnalités suivantes ont été ajoutées précédemment dans la version RC et ont été mis à jour ou s’est terminées pour la version 3.4 :

## <a name="new-features"></a>Nouvelles fonctionnalités

* Clients NuGet prennent désormais en charge encodage de contenu gzip à partir de référentiels
* Prise en charge pour les fichiers PDB à partir de packages dans des projets xproj
* Prise en charge pour iOS et Android actions de génération dans l’élément de fichiers
* Prise en charge des monikers netstandard et netstandardapp du framework

## <a name="new-user-interface-features"></a>Nouvelles fonctionnalités de l’Interface utilisateur

* Améliorations significatives des performances en particulier sur les onglets installé, les mises à jour et les consolider
* Source d’agrégat de « Toutes les Sources de Package » n’est disponible avec la fusion de résultats de recherche correcte
* Installé et onglets de mises à jour sont maintenant triés par ordre alphabétique
* Ajouter un bouton d’actualisation qui permet une recherche à actualiser
* Options de génération plus récentes en haut de la liste des versions

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Packages référencés dans `project.json` qui ont flottante version ne sera pas mise à jour à chaque build. Au lieu de cela, ils mettent à jour uniquement quand il est contraint à restaurer, nettoyer, régénérer ou modifier `project.json`.
* sources de référentiel NuGet.org deviennent n’est plus dans une configuration de projet lorsque vous utilisez l’interface de configuration NuGet.
* NuGet n’est plus restaure les packages dans les projets partagés écritures, ni un fichier de verrouillage.
* Nous avez amélioré de défaillance du réseau et recommencez la gestion des serveurs inaccessibles ou lente à répondre.
* Les comportements de clavier et souris sont améliorées dans le Gestionnaire de Package Visual Studio UI.
* Nous prennent désormais en charge la dernière version `project.json` schéma de DNX.

## <a name="breaking-changes"></a>Modifications avec rupture

* Les numéros de version de package sont désormais normalisés au format *majeure*. *mineure*. *correctif*-*préliminaire* chacune de majeure, mineure et de correctif logiciel sont traitées en tant qu’entiers et supprimer les zéros non significatifs.  Les informations de version préliminaire sont traitées comme une chaîne et aucune modification lui n’est appliquées. Ces nombres sont utilisés dans les requêtes par les clients NuGet et la recherche fournies par le service nuget.org.  Vous trouverez plus de détails dans la documentation de NuGet sous [Versions de la version préliminaire](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problèmes connus

* **Problème :** Windows 10 v1511 utilisateurs peuvent rencontrer des problèmes ou même un blocage de Visual Studio avec Powershell dans Visual Studio dans les scénarios suivants :
    * L’installation / désinstallation des packages qui ont install.ps1 / uninstall.ps1 scripts
    * Le chargement des projets qui ont un script init.ps1 (comme EntityFramework)
    * Publication de contenu web

* **Solution de contournement :** vous assurer que votre installation de Windows 10 a les derniers correctifs appliqués, spécialement le janvier 2016 (KB 3124263) ou une mise à jour ultérieure.  Plus de détails sont disponibles sur [problème GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problème :** Les redirections du protocole NuGet v2 sont rompues.
Les dépôts NuGet personnalisés qui redirigent les demandes vers un autre hôte n’honorent pas ces demandes.
* **Solution de contournement :** pour contourner ce problème, configurez l’URI de dépôt de packages dans les paramètres pour pointer vers l’emplacement de serveur redirigé.
Pour plus d’informations, consultez [requête de tirage GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)