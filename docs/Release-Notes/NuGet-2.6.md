---
title: Notes de publication NuGet 2.6 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d99bbf29-2b9a-4dc5-a823-5eb4f9e30f7f
description: "Notes de publication pour 2.6 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 2.6 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b34c0049a5ba42f6bcd5b36fa5b0ba261e27ecd5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-26-release-notes"></a>Notes de version 2.6 de NuGet

[Notes de publication NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 pour les Notes de publication WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 a été publiée le 26 juin 2013.

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="support-for-visual-studio-2013"></a>Prise en charge pour Visual Studio 2013

NuGet 2.6 est la première version qui prend en charge pour Visual Studio 2013. Et comme Visual Studio 2012, l’extension du Gestionnaire de Package NuGet est incluse dans toutes les éditions de Visual Studio.

Afin d’offrir la meilleure prise en charge possible pour Visual Studio 2013, tout en prenant en charge de Visual Studio 2010 et Visual Studio 2012 et en conservant la taille d’extension aussi petite que possible, nous allons produisant une extension distincte pour Visual Studio 2013, lors de la extension d’origine se poursuit pour Visual Studio 2010 et 2012.

À compter de NuGet 2.6, nous publierons deux extensions, comme indiqué ci-dessous :

1. [Gestionnaire de Package NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (s’applique à Visual Studio 2010 et 2012)
1. [Gestionnaire de Package NuGet pour Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Avec cette division, le [nuget.org](https://nuget.org) bouton « Installer NuGet » de la page d’accueil va vous guider pour la [l’installation de NuGet](../guides/install-nuget.md) page, où vous trouverez plus d’informations sur l’installation des clients NuGet différents.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Prise en charge de la transformation XDT Web.config

Une des fonctionnalités plus fortement demandées pour le client NuGet a été pour prendre en charge les transformations XML plus puissantes en utilisant le moteur de transformation XDT qui est utilisé dans les transformations de configuration de build de Visual Studio.

En avril 2013, nous avons apporté deux annonces big concernant la prise en charge de NuGet pour XDT. La première est que la bibliothèque XDT lui-même était en cours lui-même [publiés sous la forme d’un package NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) et [open source sur CodePlex](http://xdt.codeplex.com/). Cette étape activé le moteur XDT être librement utilisés par d’autres logiciels open source, y compris le client de NuGet. La deuxième annonce a été le plan pour prendre en charge l’utilisation du moteur XDT pour les transformations dans le client de NuGet. NuGet 2.6 inclut cette intégration.

#### <a name="how-it-works"></a>Son fonctionnement

Pour tirer parti de la prise en charge XDT de NuGet, les mécanismes de présenter un aspect similaires à celles de la [fonctionnalité actuelle de la transformation de config](../create-packages/source-and-config-file-transformations.md).
Fichiers de transformation sont ajoutés au dossier de contenu du package. Toutefois, alors que les transformations de configuration utilisent un seul fichier pour l’installation et la désinstallation, les transformations de XDT permettent un contrôle affiné sur ces deux processus à l’aide de fichiers suivants :

- Web.config.Install.xdt
- Web.config.Uninstall.xdt

En outre, NuGet utilise le suffixe de fichier pour déterminer le moteur à exécuter pour les transformations, afin de packages à l’aide de la web.config.transforms existants continueront de fonctionner. XDT transformations peuvent également être appliquées à n’importe quel fichier XML (pas seulement le fichier web.config), donc vous pouvez exploiter ceci pour d’autres applications dans votre projet.

#### <a name="what-you-can-do-with-xdt"></a>Ce que vous pouvez faire avec XDT

Matérialiser de XDT est son [syntaxe simple mais puissante](http://msdn.microsoft.com/library/dd465326.aspx) permettant de manipuler la structure d’un DOM. XML Au lieu de simplement recouvrir une structure de document fixe sur une autre structure, XDT fournit des contrôles pour les éléments correspondants dans une variété de différentes manières, à partir de la correspondance de noms attribut simple pour la prise en charge de XPath complète. Une fois qu’un élément correspondant ou un ensemble d’éléments est trouvé, XDT fournit un rich ensemble de fonctions permettant de manipuler les éléments, que ce soit pour ajout, mise à jour, suppression d’attributs, placer un nouvel élément à un emplacement spécifique, ou remplacer ou supprimer l’intégralité du élément et ses enfants.

### <a name="machine-wide-configuration"></a>Configuration de l’échelle de l’ordinateur

Une des forces excellentes de NuGet est qu’elle décompose une grande dans le cas contraire exécutable ou une bibliothèque dans un ensemble de composants modulaires qui peut être intégré et surtout à maintenir et contrôle de version du indépendamment. Un effet secondaire de cette opération, toutefois, est que l’idée classique d’un produit ou une famille de produits potentiellement plus fragmentée.
Fonctionnalité de source de package personnalisé de NuGet offre un moyen d’organiser les packages ; Toutefois, les sources de package personnalisé ne sont pas détectables sur leurs propres.

NuGet 2.6 étend la logique de configuration NuGet en parcourant la hiérarchie de dossiers sous le chemin d’accès du ProgramData%/NuGet/Config. Programmes d’installation du produit peuvent ajouter des fichiers de configuration NuGet personnalisée sous ce dossier pour enregistrer une source de package personnalisées pour leurs produits. En outre, la structure de dossiers prend en charge la sémantique de produit, la version et même référence (SKU) de l’IDE. Paramètres à partir de ces répertoires sont appliquées dans l’ordre suivant avec une stratégie de priorité « dernier dans wins ».

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{référence (SKU)}\*.config

Dans cette liste, l’espace réservé {IDE} est spécifique à l’IDE dans lequel NuGet est en cours d’exécution, dans le cas de Visual Studio, il est donc « VisualStudio ». La Version {} et des espaces réservés {SKU} sont fournis par l’IDE (par exemple) « 11.0 » et « WDExpress », « VWDExpress » et « Pro », respectivement). Le dossier peut contenir plusieurs fichiers *.config différents.
Par conséquent, la société de composant ACME peut, dans le cadre de son programme d’installation du produit, ajoutez une source de package personnalisé qui sera visible uniquement dans les versions Professionnel et Édition intégrale de Visual Studio 2012 en créant le chemin d’accès suivant :

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Alors que la structure de dossiers simplifie pour les programmes tels que des programmes d’installation de logiciel pour ajouter des sources de package de l’échelle de l’ordinateur à la configuration de NuGet, la boîte de dialogue de configuration NuGet a également été mis à jour pour permettre l’inscription des sources de package en tant que un utilisateur spécifique (par exemple, il est enregistré dans % AppData%/NuGet/NuGet.Config) ou à l’échelle de l’ordinateur.

Cette fonctionnalité est utilisée par Visual Studio 2013, où un fichier est installé sur :

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Dans ce fichier, une nouvelle source de package appelée « Les Packages .NET Framework » est configurée.

![Paramètres NuGet le fichier de configuration machine](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>CONTEXTUALISATION recherche

Comme le nombre de packages pris en charge par la galerie NuGet continue de croître à un rythme exponentiels, amélioration de la recherche reste toujours en haut de la liste de priorité de NuGet. Une des fonctionnalités planifiées pour NuGet est une recherche contextuelle, ce qui signifie que NuGet utiliser plus d’informations sur la version et de référence (SKU) de Visual Studio que vous utilisez et le type de projet que vous générez comme critère pour déterminer la pertinence de recherche potentiel résultats.

À compter de NuGet 2.6, chaque fois qu’un package est installé, le contexte de l’installation est enregistré en tant que partie des données d’opération de l’installation.  Recherche également envoyer les mêmes informations de contexte qui permettent de la galerie NuGet optimiser les résultats de la recherche des tendances de l’installation contextuelles.  Une prochaine mise à jour dans la galerie NuGet activera cette augmentation de la pertinence contextuelle.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Visual Studio installe Direct suivi. Installe de dépendance

Les auteurs de package reposent de plus en plus sur les [Package statistiques](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) fourni dans la galerie NuGet.  L’une du point de données de manquantes importantes que les auteurs ont demandé est une différenciation entre direct package installe et installe de dépendance.  Jusqu'à présent, le client NuGet n’a pas envoyé n’importe quel contexte autour de l’opération d’installation pour que le développeur installé directement le package ou si elle a été installée pour répondre à une dépendance.
En commençant avec NuGet 2.6, que les données sont désormais envoyées pour l’opération d’installation.  Statistiques de package dans la galerie NuGet va exposer ces données en tant qu’opérations d’installation distinct, avec un «-dépendance « suffixe.

* Installez
* Dépendance d’installation
* Mise à jour
* Dépendance de la mise à jour
* Réinstallation
* Dépendance réinstaller

En plus du nom de l’autre opération, l’id de package dépendant est également enregistré pour l’installation.  Une prochaine mise à jour dans la galerie NuGet exposer les données dans les rapports, ce qui permet aux auteurs de package afin de mieux comprendre comment les développeurs installez les packages.

## <a name="bug-fixes"></a>Correctifs de bogues

NuGet 2.6 inclut également plusieurs résolutions de bogue. Pour obtenir la liste complète de travail éléments corrigés dans NuGet 2.6, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).