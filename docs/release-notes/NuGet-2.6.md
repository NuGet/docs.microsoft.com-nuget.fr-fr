---
title: Notes de publication NuGet 2.6
description: Notes de publication pour NuGet 2.6.1 pour WebMatrix, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551941"
---
# <a name="nuget-26-release-notes"></a>Notes de publication NuGet 2.6

[Notes de publication de NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 pour WebMatrix Notes de publication](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 a été publiée le 26 juin 2013.

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="support-for-visual-studio-2013"></a>Prise en charge de Visual Studio 2013

NuGet 2.6 est la première version qui prend en charge pour Visual Studio 2013. Et comme Visual Studio 2012, l’extension du Gestionnaire de Package NuGet est incluse dans toutes les éditions de Visual Studio.

Afin d’offrir la meilleure prise en charge possible pour Visual Studio 2013, tout en prenant en charge de Visual Studio 2010 et Visual Studio 2012 et en conservant les tailles d’extension aussi petites que possible, nous allons produisant aucune extension distincte pour Visual Studio 2013 lors de la extension d’origine continue à cibler à la fois Visual Studio 2010 et 2012.

À compter de NuGet 2.6, nous publierons deux extensions comme indiqué ci-dessous :

1. [Gestionnaire de Package NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (s’applique à Visual Studio 2010 et 2012)
1. [Gestionnaire de Package NuGet pour Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Avec cette division, le [nuget.org](https://nuget.org) bouton « Installer NuGet » de la page d’accueil permet d’accéder à la [installation NuGet](../install-nuget-client-tools.md) page, où vous trouverez plus d’informations sur l’installation des différents clients NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Prise en charge de transformation XDT Web.config

Une des fonctionnalités plus demandés pour le client NuGet a été pour prendre en charge les transformations XML plus puissantes en utilisant le moteur de transformation XDT qui est utilisé dans les transformations de configuration de build de Visual Studio.

En avril 2013, nous avons apporté deux annonces big concernant la prise en charge de NuGet pour XDT. La première était que la bibliothèque XDT elle-même était en cours de lui-même [publié sous forme de package NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) et [open source sur CodePlex](http://xdt.codeplex.com/). Cette étape activé le moteur XDT utilisable librement à d’autres logiciels open source, y compris le client NuGet. L’annonce du deuxième était prévu pour prendre en charge l’utilisation du moteur XDT pour les transformations dans le client NuGet. NuGet 2.6 inclut cette intégration.

#### <a name="how-it-works"></a>Son fonctionnement

Pour tirer parti de la prise en charge XDT de NuGet, les mécanismes ressembler à celles de la [fonctionnalité de transformation actuelle config](../create-packages/source-and-config-file-transformations.md).
Fichiers de transformation sont ajoutés au dossier de contenu du package. Toutefois, tandis que les transformations de configuration utilisent un seul fichier pour l’installation et la désinstallation, les transformations de XDT permettent un contrôle affiné sur ces deux processus en utilisant les fichiers suivants :

- Web.config.install.xdt
- Web.config.Uninstall.xdt

En outre, NuGet utilise le suffixe de fichier pour déterminer quel moteur pour exécuter des transformations, afin de packages à l’aide de la web.config.transforms existants continueront de fonctionner. XDT transformations peuvent également être appliquées à n’importe quel fichier XML (pas seulement web.config), vous pouvez ainsi de profiter cela pour d’autres applications dans votre projet.

#### <a name="what-you-can-do-with-xdt"></a>Ce que vous pouvez faire avec XDT

Un des principaux atouts de XDT est son [syntaxe simple mais puissant](http://msdn.microsoft.com/library/dd465326.aspx) pour manipuler la structure d’un DOM. XML Au lieu de simplement superposition d’une structure de document fixe sur une autre structure, XDT fournit des contrôles pour la correspondance des éléments de plusieurs façons, à partir de l’attribut simple correspondance de noms pour la prise en charge de XPath complète. Une fois qu’un élément correspondant ou un ensemble d’éléments est trouvé, XDT fournit un ensemble complet de fonctions permettant de manipuler les éléments, que ce soit pour ajout, la mise à jour, ou suppression d’attributs, placer un nouvel élément à un emplacement spécifique, ou du remplacement ou suppression de l’ensemble élément et ses enfants.

### <a name="machine-wide-configuration"></a>Configuration de l’ordinateur

Une des forces exceptionnelles de NuGet est qu’elle décompose une grande sinon exécutable ou une bibliothèque en un ensemble de composants modulaires qui peut être intégré et plus important encore mise à jour et avec contrôle de version indépendamment. Un effet secondaire de cette approche, cependant, est que l’idée conventionnelle d’un produit ou une famille de produits devienne potentiellement plus en plus fragmentée.
Fonctionnalité de source de package personnalisé de NuGet fournit une manière d’organiser des packages ; Toutefois, les sources de package personnalisé ne sont pas détectables sur leurs propres.

NuGet 2.6 étend la logique de configuration NuGet en parcourant la hiérarchie de dossiers sous le chemin d’accès % ProgramData%/NuGet/Config. Programmes d’installation du produit peuvent ajouter des fichiers de configuration NuGet personnalisés dans ce dossier pour inscrire une source de package personnalisées pour leurs produits. En outre, la structure de dossiers prend en charge la sémantique pour le produit, la version et même référence (SKU) de l’IDE. Paramètres à partir de ces répertoires sont appliquées dans l’ordre suivant avec une stratégie de priorité « dernier dans wins ».

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{référence (SKU)}\*.config

Dans cette liste, l’espace réservé {IDE} étant spécifique à l’IDE dans lequel NuGet est en cours d’exécution, dans le cas de Visual Studio, il sera « VisualStudio ». La Version de {} et des espaces réservés {SKU} sont fournies par l’IDE (par exemple) « 11.0 » et « WDExpress », « VWDExpress » et « Pro », respectivement). Le dossier peut contenir plusieurs fichiers *.config différents.
Par conséquent, la société de composant ACME peut, dans le cadre de leur programme d’installation du produit, ajoutez une source de package personnalisé qui sera visible uniquement dans les versions Professionnel et Édition intégrale de Visual Studio 2012 en créant le chemin d’accès suivant :

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Alors que la structure de dossiers rend simple pour les programmes, tels que des programmes d’installation de logiciel pour ajouter des sources de package de l’échelle de l’ordinateur à la configuration de NuGet, la boîte de dialogue de configuration NuGet a également été mis à jour pour permettre l’inscription des sources de package en tant que soit spécifique à l’utilisateur (par exemple, il est enregistré dans % AppData%/NuGet/NuGet.Config) ou à l’échelle de l’ordinateur.

Cette fonctionnalité est utilisée par Visual Studio 2013, où un fichier est installé sur :

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Dans ce fichier, une nouvelle source de package appelée « Packages.NET Framework » est configurée.

![Paramètres globaux de l’ordinateur de fichier de configuration NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>CONTEXTUALISATION de recherche

Comme le nombre de packages pris en charge par la galerie NuGet continue de croître à un rythme exponentielle, amélioration de la recherche reste toujours en haut de la liste de priorité de NuGet. L’une des fonctionnalités planifiées pour NuGet est d’effectuer une recherche contextuelle, ce qui signifie que NuGet utilise les informations sur la version et de référence (SKU) de Visual Studio que vous utilisez et le type de projet que vous générez comme critère pour déterminer la pertinence de recherche potentiel résultats.

À compter de NuGet 2.6, chaque fois qu’un package est installé, le contexte pour l’installation est enregistré en tant que partie des données d’opération de l’installation.  Recherches envoient également les mêmes informations de contexte, ce qui permettent la galerie NuGet améliorer les résultats de la recherche des tendances de l’installation contextuelles.  Une mise à jour future de la galerie NuGet permettra de cette amélioration de la pertinence contextuelle.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Visual Studio installe Direct suivi. Installations de dépendance

Les auteurs de packages comptez plus sur le [Package statistiques](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) fourni dans la galerie NuGet.  Une importante de données manquant point que les auteurs ont demandé est une distinction entre les installations de package direct et les installations de dépendance.  Jusqu'à présent, le client NuGet n’a pas envoyé n’importe quel contexte autour de l’opération d’installation pour que le développeur installés directement le package ou si elle a été installée pour répondre à une dépendance.
À partir de NuGet 2.6, que les données sont désormais envoyées pour l’opération d’installation.  Statistiques de package dans la galerie NuGet exposera ces données en tant qu’opérations d’installation distincte, avec un «-dépendance « suffixe.

* Installez
* Dépendance d’installation
* Mise à jour
* Dépendances de mise à jour
* Réinstallation
* Dépendance réinstaller

En plus de l’autre nom d’opération, l’id de package dépendant est également enregistré pour l’installation.  Une mise à jour future de la galerie NuGet exposer les données dans les rapports, ce qui permet aux auteurs de package afin de mieux comprendre comment les développeurs installez les packages.

## <a name="bug-fixes"></a>Correctifs de bogues

NuGet 2.6 inclut également plusieurs résolutions de bogues. Pour obtenir une liste complète de travail éléments résolus dans NuGet 2.6, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).