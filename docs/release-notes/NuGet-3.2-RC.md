---
title: Notes de publication de NuGet 3,2 RC
description: Notes de publication de NuGet 3,2 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8132affb8273604ae79d4e1f85e6072d8eaf5ad6
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780296"
---
# <a name="nuget-32-rc-release-notes"></a>Notes de publication de NuGet 3,2 RC

Notes de publication de [NuGet 3.1.1](../release-notes/nuget-3.1.1.md)  |  [Notes de publication de NuGet 3,2](../release-notes/nuget-3.2.md)

La version Release candidate de NuGet 3,2 a été publiée le 2 septembre 2015, sous la forme d’un ensemble d’améliorations et de correctifs pour la version 3.1.1.  En outre, il s’agit des premières mises en production qui sont publiées en premier dans le nouveau référentiel dist.nuget.org.

## <a name="new-features"></a>Nouvelles fonctionnalités

* Les projets qui résident dans le même dossier peuvent maintenant avoir différents `project.json` fichiers dans ce dossier spécifiques à chaque projet.  Pour chaque projet, nommez le `project.json` fichier `{ProjectName}.project.json` et NuGet va correctement faire référence à ce contenu et l’utiliser pour chaque projet.  Cela prend en charge une nouvelle fonctionnalité  [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` prend désormais en charge un globalPackagesFolder en tant que chemin d’accès relatif- [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Mises à jour de ligne de commande

Il s’agit de la première version du client nuget.exe qui prend en charge les serveurs NuGet v3 et de la restauration des packages pour les projets gérés avec un `project.json` fichier.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Un certain nombre de problèmes de flux authentifiés ont été résolus dans cette version pour améliorer les interactions avec le client.

* Les interactions d’installation/restauration soumettent uniquement les informations d’identification de la demande initiale au flux authentifié- [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* La commande Push ne résout pas les informations d’identification de la configuration- [1248](https://github.com/NuGet/Home/issues/1248)
* Les en-têtes et les agents utilisateur sont désormais envoyés aux dépôts NuGet pour faciliter le suivi des statistiques- [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Nous avons apporté un certain nombre d’améliorations pour mieux gérer les défaillances du réseau lors de la tentative d’utilisation d’un référentiel NuGet distant :

* Amélioration des messages d’erreur lorsqu’il est impossible de se connecter aux flux distants- [1238](https://github.com/NuGet/Home/issues/1238)
* Correction de la commande NuGet Restore pour retourner correctement 1 lorsqu’une condition d’erreur se produit- [1186](https://github.com/NuGet/Home/issues/1186)
* À présent, réessaye les connexions réseau tous les 200 $ pour un maximum de 5 tentatives en cas de défaillances HTTP 5xx- [1120](https://github.com/NuGet/Home/issues/1120)
* Amélioration de la gestion des réponses de redirection du serveur lors d’une commande Push- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` prend désormais en charge l’URL ou le nom du référentiel à partir de Nuget.Config en tant qu’argument- [1046](https://github.com/NuGet/Home/issues/1046)
* Les packages manquants qui ne se trouvaient pas dans un référentiel pendant une restauration sont désormais signalés comme des erreurs au lieu des avertissements [1038](https://github.com/NuGet/Home/issues/1038)
* Correction du traitement multipartwebrequest de \r\n pour les scénarios UNIX/Linux- [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Il existe un certain nombre de correctifs pour les problèmes liés à diverses commandes :

* La commande Push n’effectue plus d’extraction avant un PUT sur une source de package- [1237](https://github.com/NuGet/Home/issues/1237)
* La commande list ne répète plus les numéros de version- [1185](https://github.com/NuGet/Home/issues/1185)
* Le Pack avec l’argument-Build prend désormais correctement en charge C# 6,0- [1107](https://github.com/NuGet/Home/issues/1107)
* Correction des problèmes lors de la tentative de compression d’un projet F # généré avec Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)
* Restore now no-OPS quand les packages existent déjà- [1040](https://github.com/NuGet/Home/issues/1040)
* Amélioration des messages d’erreur quand `packages.config` le fichier est incorrect- [1034](https://github.com/NuGet/Home/issues/1034)
* Correction de la commande Restore avec `-SolutionDirectory` switch pour fonctionner avec des chemins d’accès relatifs- [992](https://github.com/NuGet/Home/issues/992)
* Commande améliorée mise à jour pour prendre en charge la mise à jour à l’ensemble de la solution- [924](https://github.com/NuGet/Home/issues/924)

Une liste complète des problèmes résolus dans cette version est disponible dans le jalon de [ligne de commande](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)NuGet github.

## <a name="visual-studio-extension-updates"></a>Mises à jour de l’extension Visual Studio

### <a name="new-features-in-visual-studio"></a>Nouvelles fonctionnalités dans Visual Studio

* Un nouvel élément de menu contextuel a été ajouté à la Explorateur de solutions sur le nœud de la solution qui permet de restaurer les packages sans générer la solution ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nouvel élément de menu contextuel « restaurer les packages »](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Mises à jour et correctifs dans Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Les correctifs pour les flux authentifiés ont également été reportés et résolus dans l’extension.  Les éléments d’authentification suivants ont également été traités dans l’extension :

* À présent, vous devez traiter correctement les flux authentifiés NuGet v3 correctement, et non en tant que flux authentifiés v2- [1216](https://github.com/NuGet/Home/issues/1216)
* Correction de la demande d’informations d’identification d’authentification dans les projets utilisant `project.json` et communiquant avec les flux v2- [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>La connectivité réseau a affecté l’interface utilisateur dans Visual Studio et nous avons résolu ce problème avec les correctifs suivants :

* Amélioration de la maintenance du cache local des versions de package- [1096](https://github.com/NuGet/Home/issues/1096)
* Modification du comportement d’échec lors de la connexion à un flux V3 pour ne plus tenter de le traiter en tant que flux v2- [1253](https://github.com/NuGet/Home/issues/1253)
* Prévention des échecs d’installation lors de l’installation d’un package avec plusieurs sources de package- [1183](https://github.com/NuGet/Home/issues/1183)

Nous avons amélioré la gestion des interactions avec les opérations de génération :

* Maintenant, en continuant à générer des projets si la restauration de packages pour un projet unique échoue- [1169](https://github.com/NuGet/Home/issues/1169)
* L’installation d’un package dans un projet qui dépend d’un autre projet dans la solution force une régénération de solution- [981](https://github.com/NuGet/Home/issues/981)
* Correction des installations de package ayant échoué pour restaurer correctement les modifications apportées à un projet- [1265](https://github.com/NuGet/Home/issues/1265)
* Correction de la suppression par inadvertance de l' `developmentDependency` attribut sur un package dans `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Les appels à `install.ps1` ont maintenant un `$package.AssemblyReferences` objet approprié passé- [1245](https://github.com/NuGet/Home/issues/1245)
* N’empêche plus les désinstallations de packages dans les projets UWP alors que le projet est dans un état incorrect- [1128](https://github.com/NuGet/Home/issues/1128)
* Les solutions contenant un mélange `packages.config` de `project.json` projets et sont maintenant correctement générées sans nécessiter une deuxième opération de génération- [1122](https://github.com/NuGet/Home/issues/1122)
* Localisation correcte des fichiers app.config s’ils sont liés ou situés dans un dossier différent- [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Les projets UWP peuvent désormais installer des packages non listés- [1109](https://github.com/NuGet/Home/issues/1109)
* La restauration des packages est désormais autorisée quand une solution n’est pas dans un état enregistré- [1081](https://github.com/NuGet/Home/issues/1081)


La gestion des mises à jour des fichiers de configuration a été corrigée :

* Ne supprime plus un fichier de cibles remis à partir d’un package lors des générations suivantes d’un `project.json` projet managé- [1288](https://github.com/NuGet/Home/issues/1288)
* Impossible de modifier les fichiers de Nuget.Config lors de la génération de la solution ASP.NET 5- [1201](https://github.com/NuGet/Home/issues/1201)
* Impossible de modifier la contrainte des versions autorisées pendant la mise à jour du package- [1130](https://github.com/NuGet/Home/issues/1130)
* Les fichiers de verrouillage restent maintenant verrouillés pendant la génération- [1127](https://github.com/NuGet/Home/issues/1127)
* `packages.config`À présent, modification et non réécriture lors des mises à jour- [585](https://github.com/NuGet/Home/issues/585)


Les interactions avec le contrôle de code source TFS sont améliorées :

* N’a plus d’échec d’installation pour les packages liés à TFS- [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Correction de l’interface utilisateur NuGet pour autoriser l’intégration de TFS 2013- [1071](https://github.com/NuGet/Home/issues/1071)
* Correction des références aux packages restaurés pour qu’ils proviennent correctement d’un dossier de packages- [1004](https://github.com/NuGet/Home/issues/1004)

Enfin, nous avons également amélioré les éléments suivants :

* Commentaires des messages du journal réduits pour les `project.json` projets managés- [1163](https://github.com/NuGet/Home/issues/1163)
* Affichage correct de la version installée d’un package dans l’interface utilisateur- [1061](https://github.com/NuGet/Home/issues/1061)


Une liste complète des problèmes résolus pour l’extension Visual Studio se trouve dans le jalon NuGet GitHub [3,2](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Problèmes connus

Nous continuons à suivre les problèmes de notre liste de problèmes GitHub qui se trouvent à l’adresse suivante : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)