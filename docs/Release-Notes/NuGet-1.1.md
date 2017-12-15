---
title: Notes de version 1.0 et 1.1 de NuGet | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0e7688f7-09d2-4477-9fdf-0e27f572a4de
description: "Notes de version 1.1 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 1.1 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 00b6a8c6095e12ea2f4ca3fb5129d6c999071e3a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-10-and-11-release-notes"></a>Notes de version 1.0 et 1.1 de NuGet

[Notes de version 1.2 de NuGet](../release-notes/nuget-1.2.md)

NuGet 1.0 a été publié le 13 janvier 2011.  NuGet 1.1 a été publiée le 12 février 2011.

## <a name="overview"></a>Vue d'ensemble

Ce document contient les notes de version pour les différentes versions de 1.0 NuGet regroupés en fonction de la version préliminaire principales.

NuGet inclut les composants suivants :

* *NuGet.Tools.vsix* * qui se compose de :
  * **Boîte de dialogue Package bibliothèque ajouter** * boîte de dialogue dans Visual Studio permet de parcourir et installer des packages.
  * **Console du Gestionnaire de package** * Powershell en fonction de console dans Visual Studio.
* *Outil de ligne de commande NuGet* * outil utilisé pour créer (et éventuellement publier) des packages.

L’Extension NuGet outils Visual Studio (*NuGet.Tools.vsix*) requiert :

* Visual Studio 2010 ou Visual Web Developer 2010 Express.

L’outil de ligne de commande NuGet nécessite :

* Version du .NET framework 4

## <a name="installation"></a>Installation

Pour utiliser cette [dernière version](http://nuget.codeplex.com/releases/view/52018):

* Tout d’abord désinstaller votre ancienne version. Vous devez exécuter Visual Studio en tant qu’administrateur pour ce faire.
* Supprimez tous les flux existants dont vous disposez.
* Ajouter un nouveau flux pointant vers [http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

La liste des problèmes résolus dans cette version [se trouve ici](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Un problème a été résolu dans la version RTM depuis la version RC.

* [Problème 474 : Suppression de Packages affecte tous les projets dans la Solution](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Version Release Candidate

Voici les modifications apportées dans cette version finale depuis CTP 2. Visitez le suivi des problèmes pour afficher la liste complète des bogues.

* [Mise à jour de Package à partir de la Console ne met pas à jour les dépendances.](http://nuget.codeplex.com/workitem/443)
* [Ajout récupère package bin pas référence (CTP1) du package](http://nuget.codeplex.com/workitem/442)
* [Un package de mise à jour laisse les références rompues](http://nuget.codeplex.com/workitem/440)
* [Get-Package-mises à jour échoue dans la boîte de dialogue, ou lorsque la source 'All' d’agrégat est sélectionnée dans la console](http://nuget.codeplex.com/workitem/439)
* [Erreurs de vérification des packages de mise en route](http://nuget.codeplex.com/workitem/426)
* [Avertir les utilisateurs quand un package ne peut pas être installé à partir de la boîte de dialogue Package ajouter](http://nuget.codeplex.com/workitem/425)
* [Get-Package-lève des mises à jour lors de la mise à jour du grand nombre de packages](http://nuget.codeplex.com/workitem/424)
* [Améliorer la gestion des erreurs lorsque les fichiers nuspec sont créés de manière incorrecte](http://nuget.codeplex.com/workitem/423)
* [Pack de NuGet ignore les fichiers spécifiés](http://nuget.codeplex.com/workitem/422)
* [Suppression de la source du package de la dernière seconde et puis en cliquant sur « Descendre » de Visual Studio se bloque](http://nuget.codeplex.com/workitem/418)
* [Supprimer la référence d’assembly lors de l’installation des packages](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException lorsque vous ouvrez la boîte de dialogue Paramètres](http://nuget.codeplex.com/workitem/411)
* [Clé d’accès pour la Source du Package dans la Console du Gestionnaire de Package ne fonctionne pas](http://nuget.codeplex.com/workitem/410)
* [Les clés d’accès boîte de dialogue Paramètres NuGet VS donnent le Focus aux champs incorrects](http://nuget.codeplex.com/workitem/409)
* [Intellisense d’ID de package ne doit pas demander trop d’éléments](http://nuget.codeplex.com/workitem/404)
* [Échec de l’ajout du package au projet avec un point dans le nom du projet](http://nuget.codeplex.com/workitem/403)
* [Problème avec les fichiers spécifiés dans nuspec](http://nuget.codeplex.com/workitem/400)
* [Flux officiel correct doit obtenir inscrit lorsque vous utilisez une version plus récente](http://nuget.codeplex.com/workitem/399)
* [Balises doivent utiliser des espaces au lieu de #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata ne dispose pas des informations utiles](http://nuget.codeplex.com/workitem/388)
* [Ajouter un lien Signaler un abus à la boîte de dialogue](http://nuget.codeplex.com/workitem/386)
* [À l’aide de App_Data pour décompresser les sauts de packages dans Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implémentation des balises](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder permet à un package vide sans dépendances doit être créé](http://nuget.codeplex.com/workitem/373)
* [Ajoutez le champ propriétaires pour le Package](http://nuget.codeplex.com/workitem/365)
* [Mettre à jour le manifeste VSIX pour indiquer le Gestionnaire de Package NuGet plutôt que des outils de l’extension VSIX](http://nuget.codeplex.com/workitem/364)
* [Commande Get-Package génère l’erreur lorsque toutes les sources sont sélectionnée.](http://nuget.codeplex.com/workitem/359)
* [Tri des sources de package dans la boîte de dialogue Options](http://nuget.codeplex.com/workitem/356)
* [Package de mise à jour ne supprime pas la version antérieure](http://nuget.codeplex.com/workitem/352)
* [Spécification de plage de versions d’implémenter des dépendances](http://nuget.codeplex.com/workitem/347)
* [Visual Studio se bloque en cliquant sur « Ajouter le nouveau package »](http://nuget.codeplex.com/workitem/346)
* [Afficher les évaluations et les téléchargements dans la boîte de dialogue Ajouter Package](http://nuget.codeplex.com/workitem/345)
* [Modification entre les sources de package dans la boîte de dialogue ne mettre à jour source active](http://nuget.codeplex.com/workitem/344)
* [Supprimer la liaison de clé pour la fenêtre de la Console Gestionnaire de Package](http://nuget.codeplex.com/workitem/339)
* [Package d’installation n’est pas reconnu comme nom d’applet de commande en cours...](http://nuget.codeplex.com/workitem/338)
* [Installation d’un package à partir d’un flux les dépendances sur les flux régulières local ne sont pas résolues](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies doit ignorer les dépendances qui sont en cours d’utilisation](http://nuget.codeplex.com/workitem/331)
* [Si l’annulation de navigation entre les pages, utilisateur ne peut pas accéder à une autre page alors que la demande de page d’origine retourne](http://nuget.codeplex.com/workitem/325)
* [Étudier les performances de NuPack.Server pour traiter les flux avec un grand nombre de packages.](http://nuget.codeplex.com/workitem/324)
* [La deuxième fois qu'appliquer un filtre pour un package, il utilise la source du package « Nouveau », au lieu de la source sélectionnée précédemment.](http://nuget.codeplex.com/workitem/321)
* [Source du package par défaut doit être sélectionné lorsque vous sélectionnez l’onglet « Online » dans la boîte de dialogue.](http://nuget.codeplex.com/workitem/320)
* [Liste de packages doit afficher les packages installés par défaut](http://nuget.codeplex.com/workitem/309)
* [HintPaths de référence d’assembly](http://nuget.codeplex.com/workitem/294)
* [Exception lors de l’ouverture de Console du Gestionnaire de Package](http://nuget.codeplex.com/workitem/268)
* [Console intellisense télécharge l’ensemble du flux](http://nuget.codeplex.com/workitem/259)
* [Source du package 'Default' doit être renommé en 'Active'](http://nuget.codeplex.com/workitem/258)
* [L’interface utilisateur des sources de package : en appuyant sur OK doit ajouter la nouvelle source si les champs de nom/Source sont non vide](http://nuget.codeplex.com/workitem/257)
* [Boîte de dialogue devient très lente lorsque le nombre de packages installés est élevé](http://nuget.codeplex.com/workitem/243)
* [Prend en charge les redirections de liaison d’assemblys avec nom fort](http://nuget.codeplex.com/workitem/238)
* [Ajouter une référence de Package... Interface utilisateur pour inclure les déplacer vers le bas pour la source du Package](http://nuget.codeplex.com/workitem/226)
* [NuPack doit prendre en charge de la transformation de config agnostically du nom de fichier de configuration](http://nuget.codeplex.com/workitem/224)
* [Permet de BasePath pour être remplacée dans NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Comportement de secours de Source de package](http://nuget.codeplex.com/workitem/204)
* [Se bloquer sur l’interface graphique utilisateur](http://nuget.codeplex.com/workitem/201)
* [Ajouter les options de dialogue Ajout d’un Package de tri](http://nuget.codeplex.com/workitem/179)
* [touche de raccourci pour effacer la Console du Gestionnaire de Package](http://nuget.codeplex.com/workitem/174)
* [PowerConsole, Échec de la Console de NuPack](http://nuget.codeplex.com/workitem/166)
* [Console et la boîte de dialogue Package ajouter doivent définir l’agent utilisateur dans les requêtes](http://nuget.codeplex.com/workitem/141)
* [Définissez le numéro de version de l’extension VSIX et NuPack.exe dans la build.](http://nuget.codeplex.com/workitem/134)
* [Masquer les paramètres PowerShell communs de- ?](http://nuget.codeplex.com/workitem/118)
* [Ajouter - une aide détaillée pour les commandes de la console](http://nuget.codeplex.com/workitem/110)
* [Ajouter la boîte de dialogue Package doit permettre de choisir la Source du Package en cours](http://nuget.codeplex.com/workitem/88)
* [Déplacer les classes NuPack.Core dans différents espaces de noms](http://nuget.codeplex.com/workitem/50)
* [Ajouter de l’aide pour les applets de commande](http://nuget.codeplex.com/workitem/23)
* [Vérifier le hachage à partir de flux après le téléchargement du package](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Voici les principales modifications apportées dans CTP 2 :

* Basculer le package de flux d’ATOM à un point de terminaison du service OData : Si vous mettez à niveau vers la version CTP2 de NuGet, veillez à ajouter l’URL suivante comme source de package : [http://go.microsoft.com/fwlink/?LinkID=204820](http://go.microsoft.com/fwlink/?LinkID=204820).
* Renommer la commande Add-Package pour *Install-Package*.
* Mise à jour le `.nuspec` Format. Le `.nuspec` format inclut désormais la *iconUrl* champ pour spécifier une icône de png 32 x 32 qui s’afficheront dans la boîte de dialogue Package ajouter. Veillez à définir pour distinguer votre package. Le `.nuspec` format comprend également la nouvelle *projectUrl* champ que vous pouvez utiliser pour pointer vers une page web qui fournit des informations sur votre package.

Cette build ne fonctionnera pas avec l’ancienne `.nupkg` fichiers. Si vous obtenez des exceptions de référence null, vous utilisez une ancienne `.nupkg` de fichiers et devez la reconstruire avec la mise à jour [outil de ligne de commande NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Voici une liste des fonctionnalités et des bogues qui ont été résolus pour NuGet CTP 2 (n’inclut pas de bogues pour les nettoyages de code mineur etc..).

* [Assemblys de package de décompression erreur lors de la simplicité du TargetFramework pour un assembly.](http://nuget.codeplex.com/workitem/10)
* [Rendre la fenêtre de Console de NuPack plus identifiables](http://nuget.codeplex.com/workitem/14)
* [La version nupack.exe de ILMerge](http://nuget.codeplex.com/workitem/19)
* [Une meilleure gestion de l’exception d’erreur](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core] : PackageManager doit-elle gérer correctement les erreurs liées au flux](http://nuget.codeplex.com/workitem/28)
* [Besoin d’une nouvelle icône pour la console](http://nuget.codeplex.com/workitem/29)
* [Localiser des chaînes dans la boîte de dialogue](http://nuget.codeplex.com/workitem/38)
* [Les caches NuPack .nupack les fichiers téléchargés dans mémoire](http://nuget.codeplex.com/workitem/40)
* [Console de NuPack : Modifier le raccourci par défaut pour l’affichage de la console](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem doit prendre en charge les valeurs par défaut pour les propriétés communes](http://nuget.codeplex.com/workitem/49)
* [En cours d’exécution nupack.exe dans un dossier avec un seul fichier nuspec doit utiliser ce nuspec](http://nuget.codeplex.com/workitem/52)
* [Menu de projet s’affiche même lorsque aucun projet/Solution n’est chargée.](http://nuget.codeplex.com/workitem/54)
* [Build.cmd échoue sur un clone de nettoyage de la base de code](http://nuget.codeplex.com/workitem/56)
* [Fonctionnalité de mises à jour disponible](http://nuget.codeplex.com/workitem/57)
* [Boîte de dialogue : Ajout d’un package via la boîte de dialogue supprime l’invite de commandes dans la console](http://nuget.codeplex.com/workitem/73)
* [Ajout d’un package en cliquant sur « Installer » est souvent lente, aucun retour visuel](http://nuget.codeplex.com/workitem/80)
* [Il n’existe aucun moyen de découvrir des mes packages installés qui ont des mises à jour.](http://nuget.codeplex.com/workitem/82)
* [Il n’existe aucun moyen pour mettre à jour un package installé dans la boîte de dialogue.](http://nuget.codeplex.com/workitem/83)
* [Il n’existe aucun moyen de désinstaller un package installé dans la boîte de dialogue](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Ajouter une référence au Package&hellip; &rdquo; s’affiche dans le menu contextuel de références installés](http://nuget.codeplex.com/workitem/85)
* [Après la mise à jour d’un package à partir de la console, il affiche l’ancienne version et la nouvelle version comme étant installé](http://nuget.codeplex.com/workitem/86)
* [L’activité dans la console, lors de l’utilisation de la boîte de dialogue disparaît après utilisation](http://nuget.codeplex.com/workitem/87)
* [Ligne de commande de nettoyage dans nupack.exe d’analyse](http://nuget.codeplex.com/workitem/89)
* [Ajouter un nom convivial à des sources de package](http://nuget.codeplex.com/workitem/98)
* [.Nuspec de mise à jour pour prendre en charge y compris les icônes de package](http://nuget.codeplex.com/workitem/103)
* [Flux de l’interface utilisateur n’autorise pas la copie de l’URL](http://nuget.codeplex.com/workitem/105)
* [Une meilleure gestion d’erreur remove-package.](http://nuget.codeplex.com/workitem/107)
* [Saisie dans la fenêtre de Console dépend de la sélection du curseur](http://nuget.codeplex.com/workitem/112)
* [Messages d’erreur rechercher énorme](http://nuget.codeplex.com/workitem/116)
* [Les performances du Package de la suppression d’un package qui n’est pas installé soient incorrect](http://nuget.codeplex.com/workitem/117)
* [Suppression d’un package échoue lorsqu’il n’y a aucune source de package](http://nuget.codeplex.com/workitem/119)
* [Remove-Package échoue lorsque la source du package n’est pas disponible](http://nuget.codeplex.com/workitem/120)
* [Ajouter un titre pour les métadonnées de package et le flux.](http://nuget.codeplex.com/workitem/125)
* [Add-paramètre Source vers Add-Package](http://nuget.codeplex.com/workitem/127)
* [Liste de packages doit avoir un - paramètre Source](http://nuget.codeplex.com/workitem/128)
* [Mettre à jour NuPack.Server pour exiger NuPack utilisateur à télécharger le Package de l’Agent](http://nuget.codeplex.com/workitem/142)
* [Dialogue d’acceptation de licence doit répertorier les licences pour toutes les dépendances qui requièrent l’acceptation](http://nuget.codeplex.com/workitem/145)
* [Consigner une erreur lorsqu’un package lève dans le flux](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe ne doit pas permettre vide &lt;licenseurl&gt; élément](http://nuget.codeplex.com/workitem/152)
* [Renommer la liste de packages à Get-Package, ajouter-Package Install-Package et Remove-Package à désinstaller-Package](http://nuget.codeplex.com/workitem/155)
* [Blocage de Visual Studio à l’aide de l’élément de menu Ajouter une référence de Package à partir du navigateur de la Solution](http://nuget.codeplex.com/workitem/158)
* [Étiquette de « sources de package disponibles » est manquant pour un signe deux-points](http://nuget.codeplex.com/workitem/160)
* [Rendre .nuspec xml élément casse mixte constamment la casse](http://nuget.codeplex.com/workitem/161)
* [Manifeste de la NuPack VSIX doit activer le bit « admin »](http://nuget.codeplex.com/workitem/162)
* [Si vous exécutez le Package de la liste avec aucun flux, vous obtenez l’erreur de référence null](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe : spécifiez le chemin d’accès de destination](http://nuget.codeplex.com/workitem/171)
* [Erreurs PowerShell ouvrir la Console de gestion des packages sur Windows XP](http://nuget.codeplex.com/workitem/175)
* [Pannes VS lors de la tentative de chargement de la liste de packages](http://nuget.codeplex.com/workitem/176)
* [Autoriser les packages meta (aucun fichier, uniquement des dépendances)](http://nuget.codeplex.com/workitem/180)
* [Convertir un Script Powershell pour le Module Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [PathResolver doit ignorer les caractères génériques de chemin d’accès partie précédent lors de la cible est spécifiée](http://nuget.codeplex.com/workitem/183)
* [Pas de dépendances](http://nuget.codeplex.com/workitem/186)
* [Erreur d’installation Elmah](http://nuget.codeplex.com/workitem/192)
* [Transformations de configuration ne fonctionnent pas correctement avec &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [La variable ' $global : projectCache' ne peut pas être récupérée, car elle n’a pas été définie](http://nuget.codeplex.com/workitem/203)
* [Ajouter une tâche MSBuild de création de packages de NuPack](http://nuget.codeplex.com/workitem/205)
* [liste de packages doit prendre en charge de la recherche/filtrage](http://nuget.codeplex.com/workitem/206)
* [Toujours afficher un lien vers la licence si l’auteur du package fournit une URL de licence](http://nuget.codeplex.com/workitem/208)
* [Exception de « Accès refusé » occasionnelle avec Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Échec de Tests unitaires : Les InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Autoriser pour un ensemble de secours/par défaut des fichiers si une version de framework spécifique est introuvable.](http://nuget.codeplex.com/workitem/223)
* [Ajouter une référence de Package... L’interface utilisateur ne peut pas supprimer un package](http://nuget.codeplex.com/workitem/225)
* [Ajouter une référence au Package tombe en panne studio lorsqu’un ou plusieurs projet est déchargé](http://nuget.codeplex.com/workitem/228)
* [Transformation Web.config ne semble pas fonctionner sur le fichier web.debug.config](http://nuget.codeplex.com/workitem/229)
* [init.ps1 n’est ne pas exécuté sur le package personnalisé](http://nuget.codeplex.com/workitem/237)
* [Lorsque vous ajoutez des chemins d’accès à la liste de flux, le bouton par défaut est défini sur OK, si vous appuyez sur entrée il ferme automatiquement](http://nuget.codeplex.com/workitem/240)
* [Essayez de désinstaller une dépendance se bloquera VS dans ce cas 2 fois dans une ligne](http://nuget.codeplex.com/workitem/241)
* [Afficher l’URL de projet dans la boîte de dialogue Ajouter un Package](http://nuget.codeplex.com/workitem/253)
* [Par défaut de la boîte de dialogue Add-Package Packages installés](http://nuget.codeplex.com/workitem/254)
* [Modifier un élément de menu de dialogue Ajout d’un Package.](http://nuget.codeplex.com/workitem/261)
* [Renommer les espaces de noms et assemblys](http://nuget.codeplex.com/workitem/274)
* [Renommez le projet NuPack NuGet](http://nuget.codeplex.com/workitem/282)
* [Ajoutez le texte suivant dans la liste des dépendances](http://nuget.codeplex.com/workitem/288)
* [Modifier le texte d’acceptation de licence dans la boîte de dialogue d’acceptation de licence](http://nuget.codeplex.com/workitem/291)
* [Modifier le texte dans la boîte de dialogue licence acceptation au-dessus de la liste des packages](http://nuget.codeplex.com/workitem/292)
* [OData ne fonctionne pas avec une URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Gestionnaire de package UI : mise en cache agressive du nombre de package utilisée pour la pagination](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; erreur de la Console du Gestionnaire de Package](http://nuget.codeplex.com/workitem/335)
* [Ajouter la que boîte de dialogue Package affiche la licence acceptation pour déjà installé empaquetées](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Voici une liste des fonctionnalités et des bogues qui ont été résolus pour NuGet CTP 1.

* [Extension du package doit être renommée .nupack](http://nuget.codeplex.com/workitem/1)
* [Déplacer le fichier de package dans le dossier](http://nuget.codeplex.com/workitem/2)
* [Installation de fusion &amp; commandes Ajouter de PS](http://nuget.codeplex.com/workitem/3)
* [Créer des alias pour les applets de commande verbe-substantif.](http://nuget.codeplex.com/workitem/4)
* [NuPack obtient confondu lors du passage de solution dans Visual Studio](http://nuget.codeplex.com/workitem/6)
* [Nous devons masquer le dossier de solution « packages » par défaut](http://nuget.codeplex.com/workitem/11)
* [Ajouter la prise en charge pour le remplacement des jetons dans les éléments de contenu.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI doit utiliser l’API de PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core] : PackageManager marque packages comme étant installé avant de les installer](http://nuget.codeplex.com/workitem/27)
* [Suppression du projet par défaut à partir de la solution affiche toujours le projet supprimé comme valeur par défaut](http://nuget.codeplex.com/workitem/30)
* [Nouveau Package échoue avec « Impossible d’ajouter partie pour l’URI spécifié, car il est déjà dans le package. »](http://nuget.codeplex.com/workitem/32)
* [Supprimer les chaînes « NuPack » à partir de l’interface utilisateur de Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Ajouter les en-tête Apache à COPYRIGHT.txt d’un fichier](http://nuget.codeplex.com/workitem/36)
* [Supprimer la commande de mise à jour-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Gestionnaire de package inutilisable lors du chargement du profil lève une exception](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 et uninstall.ps1 doivent recevoir d’état supplémentaires](http://nuget.codeplex.com/workitem/41)
* [Combiner la Console et les Packages de l’interface graphique utilisateur dans un Package](http://nuget.codeplex.com/workitem/42)
* [Logique de transformation XML ne fonctionne pas si appliqué au format XML qui n’est pas à la racine](http://nuget.codeplex.com/workitem/43)
* [Gérer la boîte de dialogue Paramètres de sources package ne pas mise à jour de la console NuPack](http://nuget.codeplex.com/workitem/44)
* [IU de la NuPack Console : Renommer la liste déroulante de « Package de flux » à la source du Package](http://nuget.codeplex.com/workitem/45)
* [Options de la Console de NuPack : Renommer 'L’interface utilisateur d’un référentiel' pour être cohérent avec la Console de NuPack](http://nuget.codeplex.com/workitem/46)
* [Ajouter un Package échoue sur un site Web qui a été ouvert à partir d’IIS ou une URL](http://nuget.codeplex.com/workitem/53)
* [Source du Gestionnaire de package ne fonctionne pas avec FwLink](http://nuget.codeplex.com/workitem/55)
* [Définir la source du package par défaut](http://nuget.codeplex.com/workitem/59)
* [Lorsque vous ajoutez des sources de package en option, une seule source est fourni, supposez qu’il est la valeur par défaut.](http://nuget.codeplex.com/workitem/60)
* [L’interface utilisateur de boîte de dialogue affiche les packages de « récentes » fausses](http://nuget.codeplex.com/workitem/62)
* [Options : Cliquez sur Annuler n’annule pas modifications](http://nuget.codeplex.com/workitem/63)
* [Ajouter la que recherche de boîte de dialogue de référence de Package doit être insensible à la casse](http://nuget.codeplex.com/workitem/65)
* [Corrigez les métadonnées de la société dans les fichiers AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Numéro de version de l’extension VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package : Utilisez- ? Affiche l’aide de deux fois](http://nuget.codeplex.com/workitem/72)
* [Exécuter des packages d’installation/désinstallation des packages au niveau du projet](http://nuget.codeplex.com/workitem/74)
* [Impossible de créer des flux lorsqu’un nupack Échec de la validation du serveur](http://nuget.codeplex.com/workitem/90)
* [Remplacer les icônes NuPack](http://nuget.codeplex.com/workitem/94)
* [Serveur proxy http NTLM n’authentifie pas au package de flux.](http://nuget.codeplex.com/workitem/96)
* [La boîte de dialogue ne démarre toujours centré dans la fenêtre Visual Studio](http://nuget.codeplex.com/workitem/100)
* [La plupart des champs de détails de le des packages ne sont pas remplies dans la boîte de dialogue](http://nuget.codeplex.com/workitem/102)
* [Boîte de dialogue interface utilisateur n’affiche les noms des auteurs](http://nuget.codeplex.com/workitem/108)
* [Pourquoi - Version Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Supprimer l’onglet récent de l’interface utilisateur de boîte de dialogue](http://nuget.codeplex.com/workitem/115)
* [Incident Visual Studio lors de la droite cliquez sur le dossier de solution après l’ouverture de l’interface utilisateur de la boîte de dialogue au moins un.](http://nuget.codeplex.com/workitem/126)
* [Modifier le paramètre - Local de liste-Package-installé](http://nuget.codeplex.com/workitem/129)
* [Renommez packages.xml NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Console force le curseur à la fin de ligne](http://nuget.codeplex.com/workitem/135)
* [Remove-Package intellisense est interrompue](http://nuget.codeplex.com/workitem/136)
* [Ajouter RequireLicenseAcceptance indicateur .nuspec et des flux](http://nuget.codeplex.com/workitem/137)
* [Ajouter LicenseUrl au Format de .nuspec et du Package de flux](http://nuget.codeplex.com/workitem/138)
* [Cliquer sur Installer pour le Package nécessite l’acceptation doit afficher dialogue d’acceptation](http://nuget.codeplex.com/workitem/139)
* [Ajouter du texte de l’exclusion de responsabilité dans la boîte de dialogue Ajouter Package](http://nuget.codeplex.com/workitem/140)
* [Ajouter l’exclusion de responsabilité lorsque le Package de Console est exécutée la première fois](http://nuget.codeplex.com/workitem/143)
* [Afficher l’exclusion de responsabilité après l’installation du Package dans la Console](http://nuget.codeplex.com/workitem/144)
* [Renommez l’extension .nupack .nupkg](http://nuget.codeplex.com/workitem/146)