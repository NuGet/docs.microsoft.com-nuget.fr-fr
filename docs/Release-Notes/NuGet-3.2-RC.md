---
title: Notes de version RC de NuGet 3.2
description: Notes de publication pour RC 3.2 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0310bac6fdb3ef92176f9224ace1620a230664af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-32-rc-release-notes"></a>Notes de version RC de NuGet 3.2

[Notes de publication NuGet 3.1.1](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 Notes de publication](../release-notes/nuget-3.2.md)

Version release candidate de NuGet 3.2 a été publiée le 2 septembre 2015 comme un ensemble d’améliorations et correctifs pour le 3.1.1 libérer.  En outre, il s’agit des première versions publiées tout d’abord sur le nouveau référentiel dist.nuget.org.

## <a name="new-features"></a>Nouvelles fonctionnalités

* Les projets qui se trouvent dans le même dossier peuvent désormais avoir différents `project.json` fichiers dans le dossier spécifique à chaque projet.  Pour chaque projet, nommez le `project.json` fichier `{ProjectName}.project.json` et NuGet sera correctement référencer et utiliser ce contenu pour chaque projet en conséquence.  Il prend en charge une nouvelle fonctionnalité [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` prend désormais en charge un globalPackagesFolder comme un chemin d’accès relatif - [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Mises à jour de ligne de commande

C’est la première version du client qui prend en charge les serveurs de v3 NuGet nuget.exe et de restauration des packages pour les projets gérés avec un `project.json` fichier.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>A un nombre de problèmes de flux authentifiés qui ont été traités dans cette version pour améliorer les interactions avec le client.

* Installer / restauration interactions envoyer uniquement les informations d’identification pour la demande initiale du flux authentifié - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Commande push ne résout pas les informations d’identification à partir de la configuration - [1248](https://github.com/NuGet/Home/issues/1248)
* Agent utilisateur et les en-têtes sont désormais envoyées aux dépôts NuGet pour faciliter le suivi des statistiques - [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Nous avons apporté un certain nombre d’améliorations pour mieux gérer les défaillances du réseau lors de la tentative travailler avec un référentiel NuGet à distance :

* Amélioration des messages d’erreur lorsqu’il est impossible de se connecter à des flux à distance - [1238](https://github.com/NuGet/Home/issues/1238)
* Correction de commande de restauration de NuGet au retour de 1 lorsqu’une condition d’erreur se produit - [1186](https://github.com/NuGet/Home/issues/1186)
* Une nouvelle tentative maintenant des connexions réseau chaque 200 ms pour un maximum de 5 tentatives en cas de défaillance de 5xx HTTP - [1120](https://github.com/NuGet/Home/issues/1120)
* Améliorer le traitement des réponses de redirection du serveur pendant une commande push - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` prend désormais en charge le nom de l’URL ou le référentiel à partir de Nuget.Config en tant qu’argument - [1046](https://github.com/NuGet/Home/issues/1046)
* Les packages manquants qui n’étaient pas situées sur un référentiel lors d’une restauration sont maintenant signalées comme des erreurs et non des avertissements [1038](https://github.com/NuGet/Home/issues/1038)
* Correction de la gestion des multipartwebrequest de \r\n pour les scénarios d’Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Il existe un nombre de correctifs pour les problèmes liés à différentes commandes :

* Commande push n’effectue plus une commande GET avant un placement par rapport à une source de package - [1237](https://github.com/NuGet/Home/issues/1237)
* Commande liste répète n’est plus de numéros de version - [1185](https://github.com/NuGet/Home/issues/1185)
* Pack avec-argument build maintenant correctement prend en charge c# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Problèmes corrigés tentative de compression d’un projet F # généré avec Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Restaurer des opérations non maintenant lorsqu’il existe déjà des packages - [1040](https://github.com/NuGet/Home/issues/1040)
* Messages d’erreur améliorée lorsque `packages.config` fichier est incorrect - [1034](https://github.com/NuGet/Home/issues/1034)
* Correction de commande de restauration avec `-SolutionDirectory` commutateur pour travailler avec les chemins d’accès relatifs - [992](https://github.com/NuGet/Home/issues/992)
* Amélioration des commandes de mise à jour pour prendre en charge la mise à jour de la solution à l’échelle - [924](https://github.com/NuGet/Home/issues/924)

Vous trouverez une liste complète des problèmes mentionnés dans cette version de NuGet GitHub [étape majeure de ligne de commande](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Mises à jour des extensions Visual Studio

### <a name="new-features-in-visual-studio"></a>Nouvelles fonctionnalités dans Visual Studio

* Un nouvel élément de menu de contexte a été ajouté à l’Explorateur de solutions sous le nœud de solution qui permet de restaurer sans générer la solution ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nouvel élément de Menu contextuel « Restaurer les Packages »](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Met à jour et correctifs dans Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Les correctifs pour les flux authentifiés ont été reportées et traités dans l’extension et.  Les éléments d’authentification suivants ont été également traités dans l’extension :

* À présent traiter correctement les NuGet v3 authentifié correctement, les flux au lieu de que v2 authentification flux - [1216](https://github.com/NuGet/Home/issues/1216)
* Corrigé demande des informations d’identification de l’authentification dans les projets à l’aide de `project.json` et la communication avec des flux v2 - [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Connectivité réseau a affecté à l’interface utilisateur dans Visual Studio, et nous avons résolu ce avec les correctifs suivants :

* Amélioration de la maintenance du cache local de versions de package - [1096](https://github.com/NuGet/Home/issues/1096)
* Modifié le comportement d’échec lors de la connexion à un v3 flux n’est plus une tentative de le traiter comme un flux v2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Empêche désormais installer des échecs lors de l’installation d’un package avec plusieurs sources de package - [1183](https://github.com/NuGet/Home/issues/1183)

Nous avons amélioré la gestion des interactions avec les opérations de génération :

* Maintenant continuer à générer des projets si la restauration des packages pour un seul projet échoue - [1169](https://github.com/NuGet/Home/issues/1169)
* Installation d’un package dans un projet qui dépendait par un autre projet dans la solution force une régénération de la solution - [981](https://github.com/NuGet/Home/issues/981)
* Correction des installations de package ayant échoué pour annuler correctement les modifications apportées à un projet - [1265](https://github.com/NuGet/Home/issues/1265)
* Correction d’une suppression accidentelle de le `developmentDependency` attribut sur un package dans `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Les appels à `install.ps1` dispose maintenant un `$package.AssemblyReferences` objet passé - [1245](https://github.com/NuGet/Home/issues/1245)
* N’empêche plus désinstalle des packages dans les projets UWP alors que le projet est en mauvais état - [1128](https://github.com/NuGet/Home/issues/1128)
* Solutions contenant un mélange de `packages.config` et `project.json` sont maintenant correctement projets sans nécessiter une seconde opération - de génération [1122](https://github.com/NuGet/Home/issues/1122)
* Localiser correctement les fichiers app.config s’ils sont liés ou situés dans un dossier différent - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Les projets UWP peuvent désormais installer des packages non listées - [1109](https://github.com/NuGet/Home/issues/1109)
* Restauration du package est maintenant autorisée pendant une solution n’est pas dans un état enregistré - [1081](https://github.com/NuGet/Home/issues/1081)


La gestion des mises à jour des fichiers ont été corrigés de configuration :

* Suppression d’un fichier de cibles n’est plus remis à partir d’un package pour les builds suivantes d’un `project.json` projet managé - [1288](https://github.com/NuGet/Home/issues/1288)
* N’est plus en modifiant les fichiers de Nuget.Config lors de la génération de solution ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Modification n’est plus autorisé de contrainte de versions au cours de la mise à jour du package - [1130](https://github.com/NuGet/Home/issues/1130)
* Verrouiller les fichiers restent verrouillés lors de la génération - [1127](https://github.com/NuGet/Home/issues/1127)
* Modifie `packages.config` et ne réécrite pas pendant les mises à jour - [585](https://github.com/NuGet/Home/issues/585)


Interactions avec contrôle de code source TFS sont améliorées :

* N’est plus échouent installe des packages qui sont liés à TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Interface d’utilisateur NuGet corrigée pour permettre l’intégration de TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Correction des références aux packages restaurés pour correctement provient d’un dossier de packages - [1004](https://github.com/NuGet/Home/issues/1004)

Enfin, nous avons amélioré également ces éléments :

* Détail des messages du journal réduite pour `project.json` gérés projets - [1163](https://github.com/NuGet/Home/issues/1163)
* À présent correctement en affichant la version installée d’un package dans l’interface utilisateur - [1061](https://github.com/NuGet/Home/issues/1061)


Une liste complète des problèmes résolus de l’extension Visual Studio se trouvent dans NuGet GitHub [jalon 3.2](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Problèmes connus

Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)