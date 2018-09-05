---
title: Notes de publication NuGet 3.2
description: Notes de publication pour NuGet 3.2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5bdd2aa5621eead9ce79794052663cc2f8a63d45
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549520"
---
# <a name="nuget-32-release-notes"></a>Notes de publication NuGet 3.2

[Notes de publication NuGet 3.2-RC](../release-notes/nuget-3.2-RC.md) | [Notes de publication NuGet 3.2.1](../release-notes/nuget-3.2.1.md)

NuGet 3.2 a été publié le 16 septembre 2015 en tant que collection d’améliorations et correctifs pour le 3.1.1 mise en production et est disponible dans les deux [dist.nuget.org](http://dist.nuget.org/index.html) et [galerie Visual Studio](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).

## <a name="new-features"></a>Nouvelles fonctionnalités

* Les projets qui se trouvent dans le même dossier peuvent désormais avoir différents `project.json` fichiers dans ce dossier spécifique à chaque projet.  Pour chaque projet, nommez le `project.json` fichier `{ProjectName}.project.json` et NuGet privilégie cette configuration pour chaque projet en conséquence.  Cela est uniquement pris en charge avec la version 1.1 des outils de Windows 10 installé - [1102](https://github.com/NuGet/Home/issues/1102)
* Les clients NuGet prennent en charge en spécifiant une variable d’environnement NUGET_PACKAGES globale pour spécifier l’emplacement du dossier de packages global partagé utilisé dans `project.json` des projets avec la version 1.1 de Windows 10 outils managés.

## <a name="command-line-updates"></a>Mises à jour de ligne de commande

C’est la première version du client de nuget.exe qui prend en charge les serveurs v3 de NuGet et restauration des packages pour les projets gérés avec un `project.json` fichier.

Il existe un nombre de problèmes de flux authentifiés qui ont été résolus dans cette version pour améliorer les interactions avec le client.

* Installer / restauration interactions envoyer uniquement les informations d’identification pour la demande initiale au flux authentifié - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Commande push ne résout pas les informations d’identification à partir de la configuration - [1248](https://github.com/NuGet/Home/issues/1248)
* Agent utilisateur et les en-têtes sont désormais soumises à des référentiels de NuGet pour faciliter le suivi des statistiques - [929](https://github.com/NuGet/Home/issues/929)

Nous avons apporté un certain nombre d’améliorations pour mieux gérer les défaillances du réseau lorsque vous tentez d’utiliser un référentiel NuGet à distance :

* Amélioration des messages d’erreur lorsqu’il est impossible de se connecter à des flux à distance - [1238](https://github.com/NuGet/Home/issues/1238)
* Correction de commande de restauration NuGet pour correctement valeur 1 est renvoyée lorsqu’une condition d’erreur se produit - [1186](https://github.com/NuGet/Home/issues/1186)
* Une nouvelle tentative maintenant des connexions réseau chaque 200 ms pour un maximum de 5 tentatives en cas de défaillance de 5xx HTTP - [1120](https://github.com/NuGet/Home/issues/1120)
* Améliorer le traitement des réponses de redirection du serveur pendant une commande push - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` prend désormais en charge les URL ou référentiel au nom Nuget.Config en tant qu’argument - [1046](https://github.com/NuGet/Home/issues/1046)
* Les packages manquants n’étaient pas situées sur un référentiel lors d’une restauration sont désormais signalés comme des erreurs et non des avertissements [1038](https://github.com/NuGet/Home/issues/1038)
* Corrigé gestion multipartwebrequest de \r\n pour les scénarios d’Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

Il existe un nombre de correctifs aux problèmes rencontrés par les différentes commandes :

* Commande push n’effectue plus une commande GET avant une opération PUT sur une source de package - [1237](https://github.com/NuGet/Home/issues/1237)
* Liste commande répète ne sont plus des numéros de version - [1185](https://github.com/NuGet/Home/issues/1185)
* Pack avec-argument build désormais correctement prend en charge c# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Problèmes corrigés, tentative de compression d’un projet F # généré avec Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Restaurer maintenant ne fait rien, lorsqu’il existe déjà des packages - [1040](https://github.com/NuGet/Home/issues/1040)
* Messages d’erreur amélioré quand `packages.config` fichier est incorrect - [1034](https://github.com/NuGet/Home/issues/1034)
* Correction de commande de restauration avec SolutionDirectory - commutateur pour travailler avec les chemins d’accès relatifs - [992](https://github.com/NuGet/Home/issues/992)
* Amélioration des commandes de mise à jour pour prendre en charge la mise à jour de la solution à l’échelle - [924](https://github.com/NuGet/Home/issues/924)

Vous trouverez une liste complète des problèmes résolus dans cette version dans NuGet GitHub [jalon de ligne de commande](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Mises à jour de Visual Studio extension

### <a name="new-features-in-visual-studio"></a>Nouvelles fonctionnalités dans Visual Studio

* Un nouvel élément de menu contextuel a été ajouté à l’Explorateur de solutions sur le nœud de solution qui permet aux packages à restaurer sans générer la solution ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nouvel élément de Menu contextuel « Restaurer les Packages »](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Met à jour et correctifs contenus dans Visual Studio

Les correctifs pour les flux authentifiés ont été reportées et traités dans l’extension également.  Les éléments d’authentification suivants ont également abordés dans l’extension :

* À présent traiter correctement NuGet v3 les flux authentifiés correctement, au lieu de comme v2 authentifié flux - [1216](https://github.com/NuGet/Home/issues/1216)
* Corrigé demande d’informations d’authentification dans les projets utilisant `project.json` et la communication avec les flux v2 - [1082](https://github.com/NuGet/Home/issues/1082)

Connectivité réseau a affecté l’interface utilisateur dans Visual Studio, et nous avons résolu ceci avec les correctifs suivants :

* Amélioration de la maintenance du cache local des versions de package - [1096](https://github.com/NuGet/Home/issues/1096)
* Modifié le comportement d’échec lors de la connexion à un v3 flux n’est plus une tentative de le traiter comme un flux v2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Empêche désormais installer échecs lors de l’installation d’un package avec plusieurs sources de packages - [1183](https://github.com/NuGet/Home/issues/1183)

Nous avons amélioré la gestion des interactions avec les opérations de génération :

* Maintenant continuer à générer des projets si la restauration des packages pour un seul projet échoue - [1169](https://github.com/NuGet/Home/issues/1169)
* Installation d’un package dans un projet qui dépendait par un autre projet dans la solution force une régénération de la solution - [981](https://github.com/NuGet/Home/issues/981)
* Correction des installations de package ayant échoué à l’annuler correctement les modifications apportées à un projet - [1265](https://github.com/NuGet/Home/issues/1265)
* Correction de suppression par inadvertance du `developmentDependency` attribut sur un package dans `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Les appels à `install.ps1` dispose désormais un `$package.AssemblyReferences` objet passé - [1245](https://github.com/NuGet/Home/issues/1245)
* N’empêche plus désinstalle des packages dans les projets UWP alors que le projet est en mauvais état - [1128](https://github.com/NuGet/Home/issues/1128)
* Les solutions contenant un mélange de `packages.config` et `project.json` projets sont générés désormais correctement sans nécessiter une deuxième opération - de génération [1122](https://github.com/NuGet/Home/issues/1122)
* Localisation des fichiers app.config correctement s’ils sont liés ou situés dans un autre dossier - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Les projets UWP peuvent désormais installer des packages non listés - [1109](https://github.com/NuGet/Home/issues/1109)
* Restauration des packages est désormais autorisée pendant une solution n’est pas dans un état enregistré - [1081](https://github.com/NuGet/Home/issues/1081)

Gestion des mises à jour des fichiers qui ont été corrigés de configuration :

* Suppression d’un fichier de cibles n’est plus remis à partir d’un package pour les builds suivantes d’un `project.json` projet managé - [1288](https://github.com/NuGet/Home/issues/1288)
* N’est plus modifier les fichiers Nuget.Config durant la génération de la solution ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Modification n’est plus autorisée de contrainte de versions pendant la mise à jour du package - [1130](https://github.com/NuGet/Home/issues/1130)
* Verrouiller les fichiers restent verrouillés pendant la génération - [1127](https://github.com/NuGet/Home/issues/1127)
* Modifier maintenant `packages.config` et ne réécrire pas pendant les mises à jour - [585](https://github.com/NuGet/Home/issues/585)

Interactions avec contrôle de code source TFS sont améliorées :

* Échec n’est plus installations pour les packages qui sont liés à TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Interface d’utilisateur NuGet corrigée pour permettre l’intégration de TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Correction des références aux packages restaurés pour correctement provient d’un dossier de packages - [1004](https://github.com/NuGet/Home/issues/1004)

Enfin, nous avons également amélioré ces éléments :

* Réduction du niveau de détail des messages du journal pour `project.json` projets - managés [1163](https://github.com/NuGet/Home/issues/1163)
* À présent afficher correctement la version installée d’un package dans l’interface utilisateur - [1061](https://github.com/NuGet/Home/issues/1061)
* Packages avec des plages de dépendance dans leur fichier nuspec est spécifiés maintenant ont des versions préliminaires de ces dépendances pour une version stable de package - [1304](https://github.com/NuGet/Home/issues/1304)

Obtenir la liste complète des problèmes résolus pour l’extension de Visual Studio sont disponibles dans NuGet GitHub [jalon 3.2](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Problèmes connus

Nous continuons à suivre les problèmes sur notre liste de problèmes GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)