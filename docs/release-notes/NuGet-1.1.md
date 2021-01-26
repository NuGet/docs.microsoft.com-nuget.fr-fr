---
title: Notes de publication de NuGet 1,0 et 1,1
description: Notes de publication de NuGet 1,1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdd4bad54b08d956dbfdaf54220971492fd3ab02
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777211"
---
# <a name="nuget-10-and-11-release-notes"></a>Notes de publication de NuGet 1,0 et 1,1

[Notes de publication de NuGet 1,2](../release-notes/nuget-1.2.md)

NuGet 1,0 a été publié le 13 janvier 2011.  NuGet 1,1 a été publié le 12 février 2011.

## <a name="overview"></a>Vue d’ensemble

Ce document contient les notes de publication pour les différentes versions de NuGet 1,0 regroupées en fonction de la version d’évaluation principale.

NuGet comprend les composants suivants :

* *NuGet. Tools. vsix* * qui se compose des éléments suivants :
  * Boîte de dialogue **Ajouter un package de bibliothèque** * dans Visual Studio permet de parcourir et d’installer des packages.
  * **Console du gestionnaire de package** * console PowerShell dans Visual Studio.
* Outil en *ligne de commande NuGet* * outil utilisé pour créer (et éventuellement publier) des packages.

L’extension Visual Studio des outils NuGet (*NuGet. Tools. vsix*) requiert les éléments suivants :

* Visual Studio 2010 ou Visual Web Developer 2010 Express.

L’outil en ligne de commande NuGet requiert :

* .NET Framework version 4

## <a name="installation"></a>Installation

Pour utiliser cette [dernière version](http://nuget.codeplex.com/releases/view/52018):

* Désinstallez d’abord votre version antérieure. Pour ce faire, vous devez exécuter VS en tant qu’administrateur.
* Supprimez tous les flux existants.
* Ajoutez un nouveau flux pointant vers <https://go.microsoft.com/fwlink/?LinkId=206669> .

## <a name="nuget-11"></a>NuGet 1.1

La liste des problèmes résolus dans cette version est [disponible ici](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0) .

## <a name="nuget-10-rtm"></a>Version finale de NuGet 1,0

Un problème a été résolu pour RTM depuis la version RC.

* [Problème 474 : la suppression de packages affecte tous les projets de la solution](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Version Release Candidate de

Voici les modifications apportées à cette version Release candidate depuis CTP 2. Visitez le suivi des problèmes pour afficher la liste complète des bogues.

* [La mise à jour du package à partir de la console ne met pas à jour les dépendances.](http://nuget.codeplex.com/workitem/443)
* [Ajout d’un package de prélèvements à un emplacement différent de la référence de package (CTP1)](http://nuget.codeplex.com/workitem/442)
* [La mise à jour d’un package laisse des références rompues](http://nuget.codeplex.com/workitem/440)
* [Échec de l’opération de mise à jour des packages dans la boîte de dialogue ou lorsque la source de l’agrégat « tout » est sélectionnée dans la console](http://nuget.codeplex.com/workitem/439)
* [Obtention des erreurs de vérification de package](http://nuget.codeplex.com/workitem/426)
* [Avertir les utilisateurs lorsqu’un package ne peut pas être installé à partir de la boîte de dialogue Ajouter un package](http://nuget.codeplex.com/workitem/425)
* [Get-package-mises à jour lève une exception lors de la mise à jour d’un grand nombre de packages](http://nuget.codeplex.com/workitem/424)
* [Améliorez la gestion des erreurs lorsque les fichiers NuSpec ne sont pas correctement créés](http://nuget.codeplex.com/workitem/423)
* [Le Pack NuGet ignore les fichiers spécifiés](http://nuget.codeplex.com/workitem/422)
* [Suppression de l’avant-dernière source de package, puis clic sur les incidents « descendre » VS](http://nuget.codeplex.com/workitem/418)
* [Supprimer la référence d’assembly lors de l’installation des packages](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException lors de l’ouverture de la boîte de dialogue Paramètres](http://nuget.codeplex.com/workitem/411)
* [La clé d’accès pour la source du package dans la console du gestionnaire de package ne fonctionne pas](http://nuget.codeplex.com/workitem/410)
* [Les clés d’accès de la boîte de dialogue des paramètres NuGet VS permettent de cibler les champs incorrects](http://nuget.codeplex.com/workitem/409)
* [L’ID de package IntelliSense ne doit pas interroger un trop grand nombre d’éléments](http://nuget.codeplex.com/workitem/404)
* [Échec de l’ajout du package au projet avec un point dans le nom du projet](http://nuget.codeplex.com/workitem/403)
* [Problème avec les fichiers spécifiés dans NuSpec](http://nuget.codeplex.com/workitem/400)
* [Un flux officiel correct doit être enregistré lors de l’utilisation d’une version plus récente](http://nuget.codeplex.com/workitem/399)
* [Les balises doivent utiliser des espaces au lieu de #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata ne dispose pas d’informations utiles](http://nuget.codeplex.com/workitem/388)
* [Lien ajouter un rapport d’abus à la boîte de dialogue](http://nuget.codeplex.com/workitem/386)
* [Utilisation de App_Data pour décompresser des packages dans Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implémenter des balises](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder autorise la création d’un package vide sans dépendances](http://nuget.codeplex.com/workitem/373)
* [Ajouter le champ propriétaires pour le package](http://nuget.codeplex.com/workitem/365)
* [Mettre à jour le manifeste VSIX pour indiquer le gestionnaire de package NuGet plutôt que les outils VSIX](http://nuget.codeplex.com/workitem/364)
* [La commande Get-package génère une erreur lorsque toutes les sources sont sélectionnées](http://nuget.codeplex.com/workitem/359)
* [Autoriser le classement des sources du package dans la boîte de dialogue Options](http://nuget.codeplex.com/workitem/356)
* [Update-Package ne supprime pas la version antérieure](http://nuget.codeplex.com/workitem/352)
* [Implémenter la spécification de plage de versions pour les dépendances](http://nuget.codeplex.com/workitem/347)
* [Visual Studio se bloque lorsque vous cliquez sur « Ajouter un nouveau package »](http://nuget.codeplex.com/workitem/346)
* [Afficher les téléchargements et les évaluations dans la boîte de dialogue Ajouter un package](http://nuget.codeplex.com/workitem/345)
* [La modification entre les sources du package dans la boîte de dialogue ne met pas à jour la source active](http://nuget.codeplex.com/workitem/344)
* [Supprimer la combinaison de touches pour la fenêtre de console du gestionnaire de package](http://nuget.codeplex.com/workitem/339)
* [Install-Package n’est pas reconnu comme le nom d’une applet de commande...](http://nuget.codeplex.com/workitem/338)
* [Installation d’un package à partir d’un flux local les dépendances sur les flux standard ne sont pas résolues](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies doit ignorer les dépendances qui sont toujours en cours d’utilisation](http://nuget.codeplex.com/workitem/331)
* [Si vous annulez la navigation entre les pages, l’utilisateur ne peut pas accéder à une page différente pendant que la demande de page d’origine retourne](http://nuget.codeplex.com/workitem/325)
* [Examinez les performances de NuPack. Server pour servir des flux avec un grand nombre de packages.](http://nuget.codeplex.com/workitem/324)
* [La deuxième fois que je filtre un package, il utilise la « nouvelle » source du package, au lieu de la source précédemment sélectionnée.](http://nuget.codeplex.com/workitem/321)
* [La source du package par défaut doit être sélectionnée lors de la sélection de l’onglet « en ligne » dans la boîte de dialogue.](http://nuget.codeplex.com/workitem/320)
* [List-le package doit afficher les packages installés par défaut](http://nuget.codeplex.com/workitem/309)
* [Référence d’assembly HintPaths](http://nuget.codeplex.com/workitem/294)
* [Exception lors de l’ouverture de la console du gestionnaire de package](http://nuget.codeplex.com/workitem/268)
* [La console IntelliSense télécharge le flux entier](http://nuget.codeplex.com/workitem/259)
* [La source du package’default’doit être renommée en’active'](http://nuget.codeplex.com/workitem/258)
* [Interface utilisateur des sources du package : Si vous appuyez sur OK, vous devez ajouter la nouvelle source si les champs nom/source ne sont pas vides.](http://nuget.codeplex.com/workitem/257)
* [La boîte de dialogue devient Super lente lorsque le nombre de packages installés est élevé](http://nuget.codeplex.com/workitem/243)
* [Prendre en charge les redirections de liaison pour les assemblys avec nom fort](http://nuget.codeplex.com/workitem/238)
* [Ajouter une référence de package... Interface utilisateur à inclure dans la liste déroulante pour la source du package](http://nuget.codeplex.com/workitem/226)
* [NuPack doit prendre en charge la transformation de configuration de façon agnostique du nom du fichier de configuration](http://nuget.codeplex.com/workitem/224)
* [Autorise le remplacement de BasePath dans NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Comportement de secours de la source du package](http://nuget.codeplex.com/workitem/204)
* [Blocage sur l’interface graphique](http://nuget.codeplex.com/workitem/201)
* [Ajouter des options de tri à la boîte de dialogue Ajouter un package](http://nuget.codeplex.com/workitem/179)
* [touche de raccourci pour effacer la console du gestionnaire de package](http://nuget.codeplex.com/workitem/174)
* [PowerConsole provoque l’échec de la console NuPack](http://nuget.codeplex.com/workitem/166)
* [La console et la boîte de dialogue Ajouter un package doivent définir agent utilisateur dans les demandes](http://nuget.codeplex.com/workitem/141)
* [Définissez le numéro de version de l’extension VSIX et NuPack.exe dans la Build.](http://nuget.codeplex.com/workitem/134)
* [Masquer les paramètres PowerShell communs de- ?](http://nuget.codeplex.com/workitem/118)
* [Ajouter-aide détaillée pour les commandes de la console](http://nuget.codeplex.com/workitem/110)
* [La boîte de dialogue Ajouter un package doit autoriser le choix de la source du package actuel](http://nuget.codeplex.com/workitem/88)
* [Déplacer les classes NuPack. Core dans des espaces de noms différents](http://nuget.codeplex.com/workitem/50)
* [Ajouter de l’aide aux applets de commande](http://nuget.codeplex.com/workitem/23)
* [Vérifier le hachage à partir du flux après le téléchargement du package](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Les modifications les plus importantes apportées à CTP 2 sont les suivantes :

* Basculement du flux de package ATOM vers un point de terminaison de service OData : Si vous effectuez une mise à niveau vers la version CTP2 de NuGet, veillez à ajouter l’URL suivante en tant que source du package : `https://feed.nuget.org/ctp2/odata/v1/` .
* La commande Add-Package a été renommée en *Install-Package*.
* Mise à jour du `.nuspec` format. Le `.nuspec` format comprend maintenant le champ *IconUrl* pour la spécification d’une icône png 32 x 32 qui s’affichera dans la boîte de dialogue Ajouter un package. Veillez donc à définir cette valeur pour faire la distinction entre votre package. Le `.nuspec` format inclut également le nouveau champ *projectUrl* que vous pouvez utiliser pour pointer vers une page Web qui fournit des informations supplémentaires sur votre package.

Cette Build ne fonctionne pas avec les anciens `.nupkg` fichiers. Si vous recevez des exceptions de référence null, vous utilisez un ancien `.nupkg` fichier et vous devez le régénérer avec l' [outil en ligne de commande NuGet](http://nuget.codeplex.com/releases/52017/download/165468)mis à jour.

La liste suivante répertorie les fonctionnalités et bogues qui ont été corrigés pour NuGet CTP 2 (n’inclut pas les bogues pour les nettoyages de code mineurs, etc.).

* [Erreur lors de la décompression des assemblys de package lors de la spécification de TargetFramework pour un assembly.](http://nuget.codeplex.com/workitem/10)
* [Rendre la fenêtre de console NuPack plus détectable](http://nuget.codeplex.com/workitem/14)
* [ILMerge la version nupack.exe](http://nuget.codeplex.com/workitem/19)
* [Meilleure gestion des erreurs et des exceptions](http://nuget.codeplex.com/workitem/24)
* [[Nupack. Core] : PackageManager doit gérer correctement les erreurs liées aux flux](http://nuget.codeplex.com/workitem/28)
* [Vous avez besoin d’une nouvelle icône pour la console](http://nuget.codeplex.com/workitem/29)
* [Localiser des chaînes dans la boîte de dialogue](http://nuget.codeplex.com/workitem/38)
* [NuPack caches téléchargés. NuPack fichiers en mémoire](http://nuget.codeplex.com/workitem/40)
* [Console NuPack : modifier le raccourci par défaut pour l’affichage de la console](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem doit prendre en charge les valeurs par défaut pour les propriétés communes](http://nuget.codeplex.com/workitem/49)
* [L’exécution de nupack.exe dans un dossier avec un seul fichier NuSpec doit utiliser ce NuSpec](http://nuget.codeplex.com/workitem/52)
* [Le menu projet s’affiche même si aucun projet/solution n’est chargé](http://nuget.codeplex.com/workitem/54)
* [Build. cmd échoue sur un clone propre du code base](http://nuget.codeplex.com/workitem/56)
* [Fonctionnalité mises à jour disponibles](http://nuget.codeplex.com/workitem/57)
* [Boîte de dialogue : l’ajout d’un package via la boîte de dialogue supprime l’invite dans la console.](http://nuget.codeplex.com/workitem/73)
* [L’ajout d’un package en cliquant sur « installer » est souvent lent, sans aucun retour visuel](http://nuget.codeplex.com/workitem/80)
* [Il n’existe aucun moyen de détecter les packages installés qui ont des mises à jour.](http://nuget.codeplex.com/workitem/82)
* [Il n’existe aucun moyen de mettre à jour un package installé dans la boîte de dialogue.](http://nuget.codeplex.com/workitem/83)
* [Il n’existe aucun moyen de désinstaller un package installé dans la boîte de dialogue](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Ajouter une référence &hellip; &rdquo; de package s’affiche dans le menu contextuel des références installées](http://nuget.codeplex.com/workitem/85)
* [Après la mise à jour d’un package à partir de la console, il affiche à la fois l’ancienne version et la nouvelle version installée](http://nuget.codeplex.com/workitem/86)
* [L’activité dans la console, lors de l’utilisation de la boîte de dialogue, disparaît après utilisation](http://nuget.codeplex.com/workitem/87)
* [Analyse de la ligne de commande de nettoyage dans nupack.exe](http://nuget.codeplex.com/workitem/89)
* [Ajouter un nom convivial aux sources du package](http://nuget.codeplex.com/workitem/98)
* [Update. NuSpec pour prendre en charge l’inclusion d’icônes de package](http://nuget.codeplex.com/workitem/103)
* [L’interface utilisateur du flux n’autorise pas la copie de l’URL](http://nuget.codeplex.com/workitem/105)
* [Amélioration de la gestion des erreurs de package.](http://nuget.codeplex.com/workitem/107)
* [La saisie dans la fenêtre de console dépend du focus du curseur](http://nuget.codeplex.com/workitem/112)
* [Les messages d’erreur semblent terribles](http://nuget.codeplex.com/workitem/116)
* [Les performances de Remove-Package pour un package qui n’est pas installé sont incorrectes](http://nuget.codeplex.com/workitem/117)
* [La suppression d’un package échoue lorsqu’il n’existe aucune source de package](http://nuget.codeplex.com/workitem/119)
* [La suppression du package échoue lorsque la source du package n’est pas disponible](http://nuget.codeplex.com/workitem/120)
* [Ajoutez un titre aux métadonnées du package et au flux.](http://nuget.codeplex.com/workitem/125)
* [Rajouter le paramètre-source à Add-Package](http://nuget.codeplex.com/workitem/127)
* [List-le package doit avoir un paramètre-source](http://nuget.codeplex.com/workitem/128)
* [Mettre à jour NuPack. Server pour exiger que l’agent utilisateur NuPack télécharge le package](http://nuget.codeplex.com/workitem/142)
* [La boîte de dialogue acceptation de la licence doit répertorier les licences pour toutes les dépendances qui nécessitent une acceptation](http://nuget.codeplex.com/workitem/145)
* [Consigner une erreur lorsqu’un package est levé dans le flux](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe ne doit pas autoriser un &lt; élément licenseUrl vide &gt;](http://nuget.codeplex.com/workitem/152)
* [Renommez List-Package en Install-Package, Add-Package à Install-Package et Remove-Package à Uninstall-package](http://nuget.codeplex.com/workitem/155)
* [L’utilisation de l’élément de menu Ajouter une référence de package du navigateur de solution bloque Visual Studio](http://nuget.codeplex.com/workitem/158)
* [L’étiquette « sources de package disponibles » ne contient pas de signe deux-points](http://nuget.codeplex.com/workitem/160)
* [Faire en sorte que la casse des éléments XML de NuSpec respecte constamment la casse](http://nuget.codeplex.com/workitem/161)
* [Le manifeste du VSIX NuPack doit activer le bit « admin ».](http://nuget.codeplex.com/workitem/162)
* [Si vous exécutez List-Package sans flux, vous recevez une erreur de référence null](http://nuget.codeplex.com/workitem/164)
* [nuget.exe : spécifier le chemin de destination](http://nuget.codeplex.com/workitem/171)
* [Erreurs PowerShell lors de l’ouverture de la console Package Management sur WinXP](http://nuget.codeplex.com/workitem/175)
* [VS crashs durant la tentative de chargement de la liste des packages](http://nuget.codeplex.com/workitem/176)
* [autoriser les packages méta (aucun fichier, uniquement les dépendances)](http://nuget.codeplex.com/workitem/180)
* [Convertir le script PowerShell en module PowerShell 2,0](http://nuget.codeplex.com/workitem/181)
* [PathResolver doit ignorer la partie du chemin d’accès précédant les caractères génériques lorsque la cible est spécifiée](http://nuget.codeplex.com/workitem/183)
* [Aucune dépendance](http://nuget.codeplex.com/workitem/186)
* [Erreur lors de l’installation de ELMAH](http://nuget.codeplex.com/workitem/192)
* [Les transformations de configuration ne fonctionnent pas correctement avec &lt; configSections&gt;](http://nuget.codeplex.com/workitem/194)
* [Impossible de récupérer la variable « $global :p rojectCache », car elle n’a pas été définie](http://nuget.codeplex.com/workitem/203)
* [Ajouter une tâche MSBuild pour la création de packages NuPack](http://nuget.codeplex.com/workitem/205)
* [List : le package doit prendre en charge la recherche/filtrage](http://nuget.codeplex.com/workitem/206)
* [Afficher toujours un lien vers une licence si l’auteur du package fournit une URL de licence](http://nuget.codeplex.com/workitem/208)
* [Exception occasionnelle « accès refusé » avec Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Tests unitaires en échec : InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Autoriser un jeu de fichiers de secours/par défaut si une version du Framework spécifique est introuvable](http://nuget.codeplex.com/workitem/223)
* [Ajouter une référence de package... L’interface utilisateur ne peut pas supprimer un package](http://nuget.codeplex.com/workitem/225)
* [Ajouter une référence de package bloque Studio quand un ou plusieurs projets sont déchargés](http://nuget.codeplex.com/workitem/228)
* [La transformation de configuration ne semble pas fonctionner sur le fichier web.debug.config](http://nuget.codeplex.com/workitem/229)
* [init.ps1 ne pas déclencher sur un package personnalisé](http://nuget.codeplex.com/workitem/237)
* [Lorsque vous ajoutez des chemins d’accès au tab, le bouton par défaut est défini sur OK, donc si j’appuie sur entrée, il se ferme automatiquement](http://nuget.codeplex.com/workitem/240)
* [La tentative de désinstallation d’une dépendance se bloquera si la tentative est effectuée 2 fois dans une ligne](http://nuget.codeplex.com/workitem/241)
* [Afficher l’URL du projet dans la boîte de dialogue Ajouter un package](http://nuget.codeplex.com/workitem/253)
* [Boîte de dialogue Add-Package par défaut pour les packages installés](http://nuget.codeplex.com/workitem/254)
* [Modifier l’élément de menu de la boîte de dialogue Ajouter un package.](http://nuget.codeplex.com/workitem/261)
* [Renommer les espaces de noms et les assemblys](http://nuget.codeplex.com/workitem/274)
* [Renommer le projet NuPack en NuGet](http://nuget.codeplex.com/workitem/282)
* [Ajoutez le texte suivant sous la liste des dépendances.](http://nuget.codeplex.com/workitem/288)
* [Modifier le texte d’acceptation de licence dans la boîte de dialogue acceptation de la licence](http://nuget.codeplex.com/workitem/291)
* [Modifier le texte de la boîte de dialogue d’acceptation de la licence au-dessus de la liste des packages](http://nuget.codeplex.com/workitem/292)
* [OData ne fonctionne pas avec une URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Interface utilisateur du gestionnaire de package : dépassement de la mise en cache agressive du nombre de packages utilisés pour la pagination](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet- &gt; erreur de la console du gestionnaire de package](http://nuget.codeplex.com/workitem/335)
* [La boîte de dialogue Ajouter un package affiche l’acceptation de la licence pour les packages déjà installés](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

La liste suivante répertorie les fonctionnalités et bogues qui ont été corrigés pour NuGet CTP 1.

* [L’extension du package doit être renommée. nupack](http://nuget.codeplex.com/workitem/1)
* [Déplacer le fichier de package dans le dossier](http://nuget.codeplex.com/workitem/2)
* [Ajouter des commandes PS pour l’installation de fusion &amp;](http://nuget.codeplex.com/workitem/3)
* [Créer des alias pour les applets de commande Verb-Noun](http://nuget.codeplex.com/workitem/4)
* [NuPack est confus lors du basculement de la solution dans Visual Studio](http://nuget.codeplex.com/workitem/6)
* [Nous devrions masquer le dossier de solution « packages » par défaut](http://nuget.codeplex.com/workitem/11)
* [Ajoutez la prise en charge du remplacement de jetons dans les éléments de contenu.](http://nuget.codeplex.com/workitem/12)
* [NuPack. UI doit utiliser l’API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack. Core] : PackageManager marque les packages comme installés avant leur installation](http://nuget.codeplex.com/workitem/27)
* [La suppression du projet par défaut de la solution affiche toujours le projet supprimé par défaut](http://nuget.codeplex.com/workitem/30)
* [Le nouveau package échoue avec « impossible d’ajouter un composant pour l’URI spécifié, car il se trouve déjà dans le package ».](http://nuget.codeplex.com/workitem/32)
* [Supprimer les chaînes « NuPack » de l’interface utilisateur graphique de Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Ajouter un en-tête Apache à un fichier COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Commande supprimer Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Le gestionnaire de package est inutilisable lorsque le chargement du profil lève une exception](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 et uninstall.ps1 devez recevoir un État supplémentaire](http://nuget.codeplex.com/workitem/41)
* [Combiner des packages console et GUI en un seul package](http://nuget.codeplex.com/workitem/42)
* [La logique de transformation XML ne fonctionne pas si elle est appliquée à du code XML qui ne se trouve pas à la racine](http://nuget.codeplex.com/workitem/43)
* [Boîte de dialogue gérer les paramètres des sources du package ne mettant pas à jour la console NuPack](http://nuget.codeplex.com/workitem/44)
* [Interface utilisateur de la console NuPack : renommer la liste déroulante « flux de packages » en « source du package »](http://nuget.codeplex.com/workitem/45)
* [Options de la console NuPack : renommer l’interface utilisateur du référentiel pour qu’elle soit cohérente avec la console NuPack](http://nuget.codeplex.com/workitem/46)
* [Add-Package échoue sur un site Web ouvert à partir d’IIS ou d’une URL](http://nuget.codeplex.com/workitem/53)
* [La source du gestionnaire de package ne fonctionne pas avec FwLink](http://nuget.codeplex.com/workitem/55)
* [Définir la source du package par défaut](http://nuget.codeplex.com/workitem/59)
* [Lorsque vous ajoutez des sources de package dans l’option, quand une seule source est fournie, supposez qu’il s’agit de la valeur par défaut.](http://nuget.codeplex.com/workitem/60)
* [L’interface utilisateur du dialogue affiche des packages « récents » factices](http://nuget.codeplex.com/workitem/62)
* [Options : le fait de cliquer sur Annuler n’annule pas les modifications](http://nuget.codeplex.com/workitem/63)
* [La recherche de la boîte de dialogue Ajouter une référence de package ne doit pas respecter la casse](http://nuget.codeplex.com/workitem/65)
* [Corriger les métadonnées de l’entreprise dans les fichiers AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Numéro de version de l’extension VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package : utilisation de- ? affiche l’aide deux fois](http://nuget.codeplex.com/workitem/72)
* [Exécuter des packages d’installation/désinstallation pour les packages au niveau du projet](http://nuget.codeplex.com/workitem/74)
* [Le serveur ne peut pas créer de flux en cas d’échec de validation d’un nupack](http://nuget.codeplex.com/workitem/90)
* [Vous devez remplacer les icônes NuPack](http://nuget.codeplex.com/workitem/94)
* [Le proxy http NTLM ne s’authentifie pas auprès du flux de package.](http://nuget.codeplex.com/workitem/96)
* [La boîte de dialogue ne commence pas toujours à être centrée dans la fenêtre VS](http://nuget.codeplex.com/workitem/100)
* [La plupart des champs des détails des packages ne sont pas renseignés dans la boîte de dialogue](http://nuget.codeplex.com/workitem/102)
* [L’interface utilisateur du dialogue n’affiche pas les noms des auteurs](http://nuget.codeplex.com/workitem/108)
* [Pourquoi-version pour Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Supprimer l’onglet récent de l’interface utilisateur de la boîte de dialogue](http://nuget.codeplex.com/workitem/115)
* [VS Crash quand vous cliquez avec le bouton droit sur le dossier de solution après l’ouverture de l’interface utilisateur du dialogue au moins un.](http://nuget.codeplex.com/workitem/126)
* [Remplacez le paramètre-local de List-Package par-installed](http://nuget.codeplex.com/workitem/129)
* [Renommez packages.xml NuPack.config](http://nuget.codeplex.com/workitem/132)
* [La console force le curseur jusqu’à la fin de la ligne](http://nuget.codeplex.com/workitem/135)
* [La suppression d’un package IntelliSense est rompue](http://nuget.codeplex.com/workitem/136)
* [Ajouter l’indicateur RequireLicenseAcceptance à. NuSpec et flux](http://nuget.codeplex.com/workitem/137)
* [Ajouter LicenseUrl au format. NuSpec et au flux de packages](http://nuget.codeplex.com/workitem/138)
* [Le fait de cliquer sur installer pour le package qui requiert une acceptation doit afficher la boîte de dialogue d’acceptation](http://nuget.codeplex.com/workitem/139)
* [Ajouter un texte d’exclusion à la boîte de dialogue Ajouter un package](http://nuget.codeplex.com/workitem/140)
* [Ajouter une exclusion de responsabilité lorsque la console de package est exécutée la première fois](http://nuget.codeplex.com/workitem/143)
* [Afficher l’exclusion de responsabilité après l’installation du package dans la console](http://nuget.codeplex.com/workitem/144)
* [Renommez l’extension. nupack en. nupkg](http://nuget.codeplex.com/workitem/146)