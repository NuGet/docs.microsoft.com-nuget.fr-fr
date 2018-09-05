---
title: Notes de mise à jour de NuGet 1.0 et 1.1
description: Notes de version 1.1 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547019"
---
# <a name="nuget-10-and-11-release-notes"></a>Notes de mise à jour de NuGet 1.0 et 1.1

[Notes de version 1.2 de NuGet](../release-notes/nuget-1.2.md)

NuGet 1.0 a été publiée le 13 janvier 2011.  NuGet 1.1 a été publiée le 12 février 2011.

## <a name="overview"></a>Vue d'ensemble

Ce document contient les notes de publication pour les différentes versions de 1.0 NuGet regroupés en fonction de la version préliminaire majeure.

NuGet inclut les composants suivants :

* *NuGet.Tools.vsix* * qui se compose de :
  * **Ajouter la boîte de dialogue Package bibliothèque** * boîte de dialogue dans Visual Studio permet de parcourir et installer des packages.
  * **Console du Gestionnaire de package** * Powershell en fonction de la console dans Visual Studio.
* *Outil de ligne de commande NuGet* * outil utilisé pour créer (et finalement publier) des packages.

L’Extension Visual Studio des outils NuGet (*NuGet.Tools.vsix*) nécessite :

* Visual Studio 2010 ou Visual Web Developer 2010 Express.

L’outil de ligne de commande NuGet nécessite :

* Version du .NET framework 4

## <a name="installation"></a>Installation

Pour utiliser cet [dernière version](http://nuget.codeplex.com/releases/view/52018):

* Tout d’abord désinstaller votre build plus ancienne. Vous devez exécuter Visual Studio en tant qu’administrateur pour ce faire.
* Supprimer tous les flux existants que vous avez.
* Ajouter un nouveau flux pointant vers [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

La liste des problèmes résolus dans cette version [est disponible ici](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Un problème a été résolu dans la version RTM depuis la version RC.

* [Problème 474 : Suppression des Packages affecte tous les projets dans la Solution](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Version Release Candidate

Voici les modifications apportées dans cette version Release Candidate depuis CTP 2. Visitez le suivi des problèmes pour afficher la liste complète des bogues.

* [La mise à jour de Package à partir de la Console n’actualise pas les dépendances.](http://nuget.codeplex.com/workitem/443)
* [Ajout récupère package bin ne package pas de référence (CTP1)](http://nuget.codeplex.com/workitem/442)
* [La mise à jour un package laisse les références rompues](http://nuget.codeplex.com/workitem/440)
* [Get-Package-mises à jour échoue dans la boîte de dialogue, ou lorsque la source d’agrégation 'Tout' est sélectionnée dans la console](http://nuget.codeplex.com/workitem/439)
* [Obtenez des erreurs de vérification de package](http://nuget.codeplex.com/workitem/426)
* [Avertir les utilisateurs lorsqu’un package ne peut pas être installé à partir de la boîte de dialogue Package ajouter](http://nuget.codeplex.com/workitem/425)
* [Get-Package-lève des mises à jour lors de la mise à jour du grand nombre de packages](http://nuget.codeplex.com/workitem/424)
* [Améliorer la gestion des erreurs lorsque les fichiers de nuspec sont créés de manière incorrecte](http://nuget.codeplex.com/workitem/423)
* [Pack de NuGet ignore les fichiers spécifiés](http://nuget.codeplex.com/workitem/422)
* [Suppression de la source du package de la dernière seconde, puis cliquez sur « Descendre » de Visual Studio se bloque](http://nuget.codeplex.com/workitem/418)
* [Supprimer la référence d’assembly lors de l’installation des packages](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException lorsque vous ouvrez la boîte de dialogue Paramètres](http://nuget.codeplex.com/workitem/411)
* [Clé d’accès pour la Source du Package dans la Console du Gestionnaire de Package ne fonctionne pas](http://nuget.codeplex.com/workitem/410)
* [Clés d’accès de boîte de dialogue Paramètres NuGet VS donnent le Focus aux champs incorrects](http://nuget.codeplex.com/workitem/409)
* [Package ID intellisense ne doit pas interroger trop d’éléments](http://nuget.codeplex.com/workitem/404)
* [Échec de l’ajout du package au projet avec un caractère de point dans le nom du projet](http://nuget.codeplex.com/workitem/403)
* [Problème avec les fichiers spécifiés dans le fichier nuspec](http://nuget.codeplex.com/workitem/400)
* [Flux officiel correct doit obtenir inscrit lorsque vous utilisez une version plus récente](http://nuget.codeplex.com/workitem/399)
* [Balises doivent utiliser des espaces au lieu de #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata ne dispose pas des informations utiles](http://nuget.codeplex.com/workitem/388)
* [Ajouter un lien Signaler un abus à la boîte de dialogue](http://nuget.codeplex.com/workitem/386)
* [À l’aide de App_Data de décompresser des sauts de packages dans Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implémentation des balises](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder permet à un package vide sans dépendances doit être créé](http://nuget.codeplex.com/workitem/373)
* [Ajouter un champ de propriétaires pour le Package](http://nuget.codeplex.com/workitem/365)
* [Mettre à jour le manifeste VSIX pour indiquer le Gestionnaire de Package NuGet plutôt que des outils de VSIX](http://nuget.codeplex.com/workitem/364)
* [Commande Get-Package génère l’erreur lorsque toutes les sources sont sélectionnée.](http://nuget.codeplex.com/workitem/359)
* [Tri des sources de package dans la boîte de dialogue Options](http://nuget.codeplex.com/workitem/356)
* [Package de mise à jour ne supprime pas la version antérieure](http://nuget.codeplex.com/workitem/352)
* [Spécification de plage de versions d’implémenter les dépendances](http://nuget.codeplex.com/workitem/347)
* [Visual Studio se bloque lorsque vous cliquez sur « Ajouter nouveau package »](http://nuget.codeplex.com/workitem/346)
* [Afficher les évaluations et les téléchargements dans la boîte de dialogue Add Package](http://nuget.codeplex.com/workitem/345)
* [Modification entre des sources de package dans la boîte de dialogue ne met à jour source active](http://nuget.codeplex.com/workitem/344)
* [Supprimer la liaison de clé pour la fenêtre de Console de gestionnaire de Package](http://nuget.codeplex.com/workitem/339)
* [Package d’installation n’est pas reconnu comme nom d’applet de commande...](http://nuget.codeplex.com/workitem/338)
* [Installation d’un package à partir d’un flux les dépendances sur les flux régulières local ne sont pas résolues](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies doit ignorer les dépendances qui sont en cours d’utilisation](http://nuget.codeplex.com/workitem/331)
* [Si l’annulation de la navigation entre les pages utilisateur ne peut pas accéder à une autre page alors que la demande de page d’origine retourne](http://nuget.codeplex.com/workitem/325)
* [Analysez les performances du NuPack.Server afin de servir des flux avec un grand nombre de packages.](http://nuget.codeplex.com/workitem/324)
* [La deuxième fois pour filtrer pour un package, il utilise la source du package « Nouveau », au lieu de la source sélectionnée précédemment.](http://nuget.codeplex.com/workitem/321)
* [Source du package par défaut doit être sélectionné lorsque vous sélectionnez l’onglet « En ligne » dans la boîte de dialogue.](http://nuget.codeplex.com/workitem/320)
* [Package de la liste doit afficher les packages installés par défaut](http://nuget.codeplex.com/workitem/309)
* [HintPaths de référence d’assembly](http://nuget.codeplex.com/workitem/294)
* [Exception lors de l’ouverture de Console du Gestionnaire de Package](http://nuget.codeplex.com/workitem/268)
* [Console intellisense télécharge l’ensemble du flux](http://nuget.codeplex.com/workitem/259)
* [Source du package 'Default' doit être renommé en 'Active'](http://nuget.codeplex.com/workitem/258)
* [L’interface utilisateur des sources de package : en appuyant sur OK doit ajouter la nouvelle source si les champs de nom/Source sont non vide](http://nuget.codeplex.com/workitem/257)
* [Boîte de dialogue devient très lent lorsque le nombre de packages installés est élevée](http://nuget.codeplex.com/workitem/243)
* [Prise en charge des redirections de liaison des assemblys avec nom fort](http://nuget.codeplex.com/workitem/238)
* [Ajouter une référence de Package... Interface utilisateur pour inclure les déplacer vers le bas pour la source du Package](http://nuget.codeplex.com/workitem/226)
* [NuPack doit prendre en charge de la transformation de config agnostically du nom de fichier de configuration](http://nuget.codeplex.com/workitem/224)
* [Permet de BasePath pour être remplacée dans NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Comportement de secours de Source de package](http://nuget.codeplex.com/workitem/204)
* [Se bloquer sur l’interface graphique utilisateur](http://nuget.codeplex.com/workitem/201)
* [Ajouter les options de dialogue Ajouter un Package de tri](http://nuget.codeplex.com/workitem/179)
* [touche de raccourci pour effacer la Console du Gestionnaire de Package](http://nuget.codeplex.com/workitem/174)
* [PowerConsole, Échec de la Console de NuPack](http://nuget.codeplex.com/workitem/166)
* [Console et ajoutez le boîte de dialogue Package doivent définir l’agent utilisateur dans les demandes](http://nuget.codeplex.com/workitem/141)
* [Définissez le numéro de version de l’extension VSIX et NuPack.exe dans la build.](http://nuget.codeplex.com/workitem/134)
* [Masquer les paramètres PowerShell communs à partir de- ?](http://nuget.codeplex.com/workitem/118)
* [Ajouter - une aide détaillée pour les commandes de la console](http://nuget.codeplex.com/workitem/110)
* [Ajouter la boîte de dialogue Package devrait permettre de choisir la Source du Package en cours](http://nuget.codeplex.com/workitem/88)
* [Déplacer des classes de NuPack.Core dans différents espaces de noms](http://nuget.codeplex.com/workitem/50)
* [Ajouter une aide aux applets de commande](http://nuget.codeplex.com/workitem/23)
* [Vérifier le hachage à partir de flux après le téléchargement du package](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Voici les principales modifications apportées dans CTP 2 :

* Basculer le package de flux d’ATOM à un point de terminaison du service OData : Si vous mettez à niveau vers la version CTP2 de NuGet, veillez à ajouter l’URL suivante comme source de package : `https://feed.nuget.org/ctp2/odata/v1/`.
* Renommé la commande Add-Package pour *Install-Package*.
* Mise à jour le `.nuspec` Format. Le `.nuspec` format inclut désormais la *iconUrl* champ pour spécifier une icône de png de 32 x 32 qui s’afficheront dans la boîte de dialogue Package ajouter. Par conséquent, veillez à définir à distinguer votre package. Le `.nuspec` format inclut également la nouvelle *projectUrl* champ que vous pouvez utiliser pour pointer vers une page web qui fournit des informations sur votre package.

Cette build ne fonctionne pas avec l’ancienne `.nupkg` fichiers. Si vous obtenez des exceptions de référence null, vous utilisez une ancienne `.nupkg` de fichiers et devez la reconstruire avec la mise à jour [outil de ligne de commande NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Voici une liste des fonctionnalités et des bogues qui ont été résolus pour NuGet CTP 2 (n’inclut pas de bogues pour les nettoyages de code mineur etc..).

* [Assemblys de package de décompression erreur lors de la spécification du TargetFramework pour un assembly.](http://nuget.codeplex.com/workitem/10)
* [Rendre la fenêtre de Console de NuPack plus détectable](http://nuget.codeplex.com/workitem/14)
* [ILMerge la version nupack.exe](http://nuget.codeplex.com/workitem/19)
* [Meilleure gestion des erreurs/exceptions](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core] : PackageManager devrait gérer proprement les erreurs liées au flux](http://nuget.codeplex.com/workitem/28)
* [Besoin d’une nouvelle icône pour la console](http://nuget.codeplex.com/workitem/29)
* [Localiser les chaînes dans la boîte de dialogue](http://nuget.codeplex.com/workitem/38)
* [Les caches NuPack .nupack les fichiers téléchargement dans mémoire](http://nuget.codeplex.com/workitem/40)
* [Console de NuPack : Modifier le raccourci par défaut pour l’affichage de la console](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem doit prendre en charge les valeurs par défaut pour les propriétés courantes](http://nuget.codeplex.com/workitem/49)
* [En cours d’exécution nupack.exe dans un dossier avec un fichier nuspec doit utiliser ce nuspec](http://nuget.codeplex.com/workitem/52)
* [Menu du projet s’affiche même lorsque aucun projet/Solution n’est chargée](http://nuget.codeplex.com/workitem/54)
* [Build.cmd échoue sur un clone de nettoyage de la base de code](http://nuget.codeplex.com/workitem/56)
* [Fonctionnalité de mises à jour disponible](http://nuget.codeplex.com/workitem/57)
* [Boîte de dialogue : Ajout d’un package via la boîte de dialogue supprime l’invite dans la console](http://nuget.codeplex.com/workitem/73)
* [Ajout d’un package en cliquant sur « Installer » est souvent lente, avec aucun retour visuel](http://nuget.codeplex.com/workitem/80)
* [Il n’existe aucun moyen de découvrir quelles Mes packages installés disposent des mises à jour.](http://nuget.codeplex.com/workitem/82)
* [Il n’existe aucun moyen pour mettre à jour un package installé dans la boîte de dialogue.](http://nuget.codeplex.com/workitem/83)
* [Il n’existe aucun moyen pour désinstaller un package installé dans la boîte de dialogue](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Ajouter une référence de Package&hellip; &rdquo; s’affiche dans le menu contextuel de références installés](http://nuget.codeplex.com/workitem/85)
* [Après la mise à jour un package à partir de la console, il affiche l’ancienne version et la nouvelle version qu’installé](http://nuget.codeplex.com/workitem/86)
* [L’activité dans la console, lors de l’utilisation de la boîte de dialogue disparaît après utilisation](http://nuget.codeplex.com/workitem/87)
* [Ligne de commande de nettoyage dans nupack.exe d’analyse](http://nuget.codeplex.com/workitem/89)
* [Ajouter un nom convivial à des sources de package](http://nuget.codeplex.com/workitem/98)
* [.Nuspec de mise à jour pour prendre en charge y compris les icônes de package](http://nuget.codeplex.com/workitem/103)
* [Flux de l’interface utilisateur n’autorise pas la copie de l’URL](http://nuget.codeplex.com/workitem/105)
* [Une meilleure gestion d’erreur de remove-package.](http://nuget.codeplex.com/workitem/107)
* [Saisie dans la fenêtre de Console dépend de la sélection du curseur](http://nuget.codeplex.com/workitem/112)
* [Les messages d’erreur se présentent terribles](http://nuget.codeplex.com/workitem/116)
* [Les performances de Remove-Package pour un package qui n’est pas installé sont incorrecte](http://nuget.codeplex.com/workitem/117)
* [Suppression d’un package échoue lorsqu’il n’y a aucune source de package](http://nuget.codeplex.com/workitem/119)
* [Remove-Package échoue lorsque la source du package n’est pas disponible](http://nuget.codeplex.com/workitem/120)
* [Ajouter un titre pour les métadonnées du package et le flux.](http://nuget.codeplex.com/workitem/125)
* [Add - paramètre Source retour Add-Package](http://nuget.codeplex.com/workitem/127)
* [Package de la liste doit avoir un - paramètre Source](http://nuget.codeplex.com/workitem/128)
* [NuPack.Server pour exiger NuPack utilisateur Agent à télécharger le Package de mise à jour](http://nuget.codeplex.com/workitem/142)
* [Boîte de dialogue de l’acceptation de la licence doit répertorier les licences pour toutes les dépendances nécessitant l’acceptation](http://nuget.codeplex.com/workitem/145)
* [Consigner une erreur lorsqu’un package lève dans le flux](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe ne doit pas autoriser vide &lt;licenseurl&gt; élément](http://nuget.codeplex.com/workitem/152)
* [Renommer le Package de la liste à Get-Package, Add-Package et Install-Package, Remove-Package à désinstaller-Package](http://nuget.codeplex.com/workitem/155)
* [À l’aide de l’élément de menu Ajouter une référence de Package à partir du navigateur de Solution, Visual Studio se bloque](http://nuget.codeplex.com/workitem/158)
* [Étiquette de « sources de package disponible » n’a pas un signe deux-points](http://nuget.codeplex.com/workitem/160)
* [Rendre .nuspec xml élément casse mixte systématiquement la casse](http://nuget.codeplex.com/workitem/161)
* [Fichier de manifeste de le NuPack VSIX doit activer le bit « admin »](http://nuget.codeplex.com/workitem/162)
* [Si vous exécutez un Package de liste avec aucun flux, vous obtenez l’erreur de référence null](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe : spécifiez le chemin d’accès de destination](http://nuget.codeplex.com/workitem/171)
* [Erreurs PowerShell ouvrant la Console de gestion de Package sur Windows XP](http://nuget.codeplex.com/workitem/175)
* [Blocages de VS lors de la tentative de charger la liste des packages](http://nuget.codeplex.com/workitem/176)
* [permettre aux packages meta (aucun fichier, uniquement les dépendances)](http://nuget.codeplex.com/workitem/180)
* [Convertir un Script Powershell pour le Module Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [PathResolver doit ignorer les caractères génériques de chemin d’accès partie précédent lors de la cible est spécifiée](http://nuget.codeplex.com/workitem/183)
* [Aucune dépendance](http://nuget.codeplex.com/workitem/186)
* [Erreur durant l’installation Elmah](http://nuget.codeplex.com/workitem/192)
* [Transformations de configuration ne fonctionnent pas correctement avec &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [La variable ' $global : projectCache' ne peut pas être récupérée, car il n’a pas été défini](http://nuget.codeplex.com/workitem/203)
* [Ajouter une tâche MSBuild de création de packages de NuPack](http://nuget.codeplex.com/workitem/205)
* [package de la liste doit prendre en charge de la recherche et le filtrage](http://nuget.codeplex.com/workitem/206)
* [Toujours afficher un lien à licence si l’auteur du package fournit une URL de licence](http://nuget.codeplex.com/workitem/208)
* [Exception « Accès refusé » occasionnelle avec Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Échec de Tests unitaires : InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Autoriser pour un ensemble de secours/par défaut des fichiers si une version de framework spécifique est introuvable.](http://nuget.codeplex.com/workitem/223)
* [Ajouter une référence de Package... L’interface utilisateur ne peut pas supprimer un package](http://nuget.codeplex.com/workitem/225)
* [Ajouter une référence de Package se bloque studio lorsqu’un ou plusieurs de projet est déchargé](http://nuget.codeplex.com/workitem/228)
* [Transformation de configuration ne semble pas fonctionner sur le fichier web.debug.config](http://nuget.codeplex.com/workitem/229)
* [init.ps1 n’est ne pas exécuté sur le package personnalisé](http://nuget.codeplex.com/workitem/237)
* [Lorsque vous ajoutez des chemins d’accès à la liste de flux, le bouton par défaut a la valeur OK, donc si j’appuie sur entrée sa fermeture automatique](http://nuget.codeplex.com/workitem/240)
* [Tentez de désinstaller une dépendance se bloque VS dans ce cas 2 fois dans une ligne](http://nuget.codeplex.com/workitem/241)
* [Affiche l’URL du projet dans la boîte de dialogue Ajouter un Package](http://nuget.codeplex.com/workitem/253)
* [Par défaut de la boîte de dialogue Add-Package Packages installés](http://nuget.codeplex.com/workitem/254)
* [Modifier un élément de menu de dialogue Ajouter un Package.](http://nuget.codeplex.com/workitem/261)
* [Renommer les espaces de noms et assemblys](http://nuget.codeplex.com/workitem/274)
* [Renommez le projet NuPack NuGet](http://nuget.codeplex.com/workitem/282)
* [Ajoutez le texte suivant dans la liste des dépendances](http://nuget.codeplex.com/workitem/288)
* [Modifier le texte de l’acceptation de licence dans la boîte de dialogue de l’acceptation de licence](http://nuget.codeplex.com/workitem/291)
* [Modifier le texte dans la boîte de dialogue de l’acceptation de licence au-dessus de la liste des packages](http://nuget.codeplex.com/workitem/292)
* [OData ne fonctionne pas avec une URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Gestionnaire de package UI : sur la mise en cache agressive de nombre de packages utilisée pour la pagination](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; erreur de la Console du Gestionnaire de Package](http://nuget.codeplex.com/workitem/335)
* [Ajouter la que boîte de dialogue de Package affiche la licence d’acceptation pour déjà installé empaquetées](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Voici une liste des fonctionnalités et des bogues qui ont été résolus pour NuGet CTP 1.

* [Extension de package doit être renommée en .nupack](http://nuget.codeplex.com/workitem/1)
* [Déplacer le fichier de package dans le dossier](http://nuget.codeplex.com/workitem/2)
* [Installation de fusion &amp; commandes PS ajouter](http://nuget.codeplex.com/workitem/3)
* [Créer des alias pour les applets de commande verbe-nom](http://nuget.codeplex.com/workitem/4)
* [NuPack obtient confondu lors du changement de solution dans Visual Studio](http://nuget.codeplex.com/workitem/6)
* [Nous devons masquer le dossier de solution « packages » par défaut](http://nuget.codeplex.com/workitem/11)
* [Ajouter la prise en charge pour le remplacement des jetons dans les éléments de contenu.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI doit utiliser l’API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core] : PackageManager marque les packages installés avant d’installer les](http://nuget.codeplex.com/workitem/27)
* [Suppression du projet par défaut à partir de la solution affiche toujours le projet supprimé comme valeur par défaut](http://nuget.codeplex.com/workitem/30)
* [Nouveau Package échoue avec « Ne peut pas ajouter partie pour l’URI spécifié, car il est déjà dans le package ».](http://nuget.codeplex.com/workitem/32)
* [Supprimer les chaînes « NuPack » à partir de l’interface utilisateur de Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Ajouter les en-tête Apache à COPYRIGHT.txt d’un fichier](http://nuget.codeplex.com/workitem/36)
* [Supprimer la commande de mise à jour-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Gestionnaire de package inutilisable lors du chargement du profil lève une exception](http://nuget.codeplex.com/workitem/39)
* [init.ps1, Install.ps1 et uninstall.ps1 doivent recevoir état supplémentaire](http://nuget.codeplex.com/workitem/41)
* [Combiner la Console et les Packages de l’interface graphique utilisateur dans un Package](http://nuget.codeplex.com/workitem/42)
* [Logique de transformation XML ne fonctionne pas si appliqué au format XML qui n’est pas à la racine](http://nuget.codeplex.com/workitem/43)
* [Gérer la boîte de dialogue Paramètres de sources package ne pas la mise à jour la console NuPack](http://nuget.codeplex.com/workitem/44)
* [IU de la NuPack Console : Renommer la liste déroulante de « Flux de packages » à la source du Package](http://nuget.codeplex.com/workitem/45)
* [Options de la Console de NuPack : Renommer « L’interface utilisateur d’un référentiel » pour être cohérent avec la Console de NuPack](http://nuget.codeplex.com/workitem/46)
* [Ajouter un Package échoue sur un site Web qui a été ouvert à partir d’IIS ou une URL](http://nuget.codeplex.com/workitem/53)
* [Source du Gestionnaire de package ne fonctionne pas avec FwLink](http://nuget.codeplex.com/workitem/55)
* [Définir la source du package par défaut](http://nuget.codeplex.com/workitem/59)
* [Lorsque vous ajoutez des sources de package dans l’option, lorsqu’une seule source est fournie, supposons qu’il est la valeur par défaut.](http://nuget.codeplex.com/workitem/60)
* [L’interface utilisateur de boîte de dialogue affiche fausses packages « récents »](http://nuget.codeplex.com/workitem/62)
* [Options : Cliquer sur Annuler n’annule pas modifications](http://nuget.codeplex.com/workitem/63)
* [Ajouter la que recherche de boîte de dialogue de référence de Package doit respecter la casse](http://nuget.codeplex.com/workitem/65)
* [Corrigez les métadonnées de la société dans les fichiers AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Numéro de version pour l’extension VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package : Vous utilisez- ? Affiche l’aide de deux fois](http://nuget.codeplex.com/workitem/72)
* [Exécutez installer/désinstaller des packages pour les packages au niveau du projet](http://nuget.codeplex.com/workitem/74)
* [Impossible de créer des flux lorsqu’un nupack Échec de la validation du serveur](http://nuget.codeplex.com/workitem/90)
* [Remplacer les icônes NuPack](http://nuget.codeplex.com/workitem/94)
* [Le proxy http NTLM n’authentifie pas pour le flux du package.](http://nuget.codeplex.com/workitem/96)
* [La boîte de dialogue ne démarre toujours centrée dans la fenêtre de Visual Studio](http://nuget.codeplex.com/workitem/100)
* [Plusieurs champs dans les détails de le des packages ne sont pas remplis dans la boîte de dialogue](http://nuget.codeplex.com/workitem/102)
* [Boîte de dialogue interface utilisateur n’affiche les noms des auteurs](http://nuget.codeplex.com/workitem/108)
* [Pourquoi - Version Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Supprimer l’onglet récent sur l’interface utilisateur de boîte de dialogue](http://nuget.codeplex.com/workitem/115)
* [Blocage de VS lors de la droite cliquez sur le dossier de solution après l’ouverture de l’interface utilisateur de la boîte de dialogue au moins un.](http://nuget.codeplex.com/workitem/126)
* [Modifier le paramètre - Local de liste-Package-installé](http://nuget.codeplex.com/workitem/129)
* [Renommez packages.xml en NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Console force le curseur à la fin de ligne](http://nuget.codeplex.com/workitem/135)
* [Remove-Package intellisense est interrompue](http://nuget.codeplex.com/workitem/136)
* [Ajouter l’indicateur Licenseacceptance .nuspec et flux](http://nuget.codeplex.com/workitem/137)
* [Ajouter LicenseUrl au Format de fichier .nuspec et du Package de flux](http://nuget.codeplex.com/workitem/138)
* [En cliquant sur Installer pour le Package nécessite l’acceptation doit afficher l’acceptation de la boîte de dialogue](http://nuget.codeplex.com/workitem/139)
* [Ajouter du texte de l’exclusion de responsabilité à la boîte de dialogue Add Package](http://nuget.codeplex.com/workitem/140)
* [Ajouter l’exclusion de responsabilité lorsque la Console du Package est exécutée la première fois](http://nuget.codeplex.com/workitem/143)
* [Afficher les avis de non-responsabilité après l’installation du Package dans la Console](http://nuget.codeplex.com/workitem/144)
* [Renommez l’extension .nupack .nupkg](http://nuget.codeplex.com/workitem/146)