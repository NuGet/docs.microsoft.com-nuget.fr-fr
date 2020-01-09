---
title: Notes de publication de NuGet 2,6
description: Notes de publication de NuGet 2.6.1 pour WebMatrix, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5e80965aad4caa69130be31a37b7f5f5ffb12ea6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384122"
---
# <a name="nuget-26-release-notes"></a>Notes de publication de NuGet 2,6

[Notes de publication de nuget 2,5](../release-notes/nuget-2.5.md) | [notes de publication de NuGet 2.6.1 pour WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2,6 a été publié le 26 juin 2013.

## <a name="notable-features-in-the-release"></a>Fonctionnalités notables dans la version

### <a name="support-for-visual-studio-2013"></a>Prise en charge de Visual Studio 2013

NuGet 2,6 est la première version qui assure la prise en charge de Visual Studio 2013. Comme Visual Studio 2012, l’extension du gestionnaire de package NuGet est incluse dans toutes les éditions de Visual Studio.

Afin d’offrir la meilleure prise en charge possible de Visual Studio 2013 tout en prenant en charge à la fois Visual Studio 2010 et Visual Studio 2012, et en conservant la taille de l’extension le plus petit possible, nous générons une extension distincte pour Visual Studio 2013, tandis que le l’extension d’origine continue à cibler à la fois Visual Studio 2010 et 2012.

À compter de NuGet 2,6, nous publierons deux extensions comme indiqué ci-dessous :

1. [Gestionnaire de package NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (s’applique à Visual Studio 2010 et 2012)
1. [Gestionnaire de package NuGet pour Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Avec cette division, le bouton « installer NuGet » de la page d' [NuGet.org](https://nuget.org) d’origine vous amène à la page [installation de NuGet](../install-nuget-client-tools.md) , où vous trouverez plus d’informations sur l’installation des différents clients NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Prise en charge de la transformation Web. config XDT

L’une des fonctionnalités les plus demandées pour le client NuGet a été de prendre en charge des transformations XML plus puissantes à l’aide du moteur de transformation XDT utilisé dans les transformations de configuration de build Visual Studio.

En avril 2013, nous avons créé deux grandes annonces concernant la prise en charge de NuGet pour XDT. La première était que la bibliothèque XDT elle-même était [publiée en tant que package NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) et [Open source sur CodePlex](http://xdt.codeplex.com/). Cette étape permettait au moteur XDT d’être utilisé librement par d’autres logiciels open source, y compris le client NuGet. La deuxième annonce était le plan de prise en charge de l’utilisation du moteur XDT pour les transformations dans le client NuGet. NuGet 2,6 comprend cette intégration.

#### <a name="how-it-works"></a>Fonctionnement

Pour tirer parti de la prise en charge XDT de NuGet, l’mécanique ressemble à celle de la [fonctionnalité de transformation de configuration actuelle](../create-packages/source-and-config-file-transformations.md).
Les fichiers de transformation sont ajoutés au dossier Content du package. Toutefois, tandis que les transformations de configuration utilisent un seul fichier pour l’installation et la désinstallation, les transformations XDT permettent un contrôle affiné sur ces deux processus à l’aide des fichiers suivants :

- Web.config.install.xdt
- Web. config. Uninstall. xdt

En outre, NuGet utilise le suffixe file pour déterminer le moteur à exécuter pour les transformations. par conséquent, les packages qui utilisent les transformations Web. config existants continuent de fonctionner. Les transformations XDT peuvent également être appliquées à n’importe quel fichier XML (pas seulement Web. config). vous pouvez donc tirer parti de ces transformations pour d’autres applications de votre projet.

#### <a name="what-you-can-do-with-xdt"></a>Ce que vous pouvez faire avec XDT

L’une des plus grandes forces d’XDT est sa [syntaxe simple mais puissante](https://docs.microsoft.com/previous-versions/aspnet/dd465326(v=vs.110)) pour la manipulation de la structure d’un DOM XML. Plutôt que de superposer simplement une structure de document fixe à une autre structure, XDT fournit des contrôles pour mettre en correspondance les éléments de différentes façons, du simple nom d’attribut correspondant à la prise en charge de XPath complète. Une fois qu’un élément ou un ensemble d’éléments correspondant est trouvé, XDT fournit un ensemble complet de fonctions pour manipuler les éléments, qu’il s’agisse d’ajouter, de mettre à jour ou de supprimer des attributs, de placer un nouvel élément à un emplacement spécifique ou de remplacer ou de supprimer la totalité et ses enfants.

### <a name="machine-wide-configuration"></a>Configuration à l’ensemble de l’ordinateur

L’un des grands atouts de NuGet est qu’il décompose un exécutable ou une bibliothèque de grande taille dans un ensemble de composants modulaires qui peuvent être intégrés et dont la gestion des versions est la plus importante. Toutefois, l’un des effets secondaires de cela est que l’idée conventionnelle d’un produit ou d’une famille de produits devient potentiellement plus fragmentée.
La fonctionnalité source de package personnalisée de NuGet fournit une méthode d’organisation des packages. Toutefois, les sources de package personnalisées ne sont pas détectables par elles-mêmes.

NuGet 2,6 étend la logique de configuration de NuGet en effectuant une recherche dans l’arborescence des dossiers sous le chemin d’accès% ProgramData%/NuGet/Config. Les programmes d’installation de produit peuvent ajouter des fichiers de configuration NuGet personnalisés dans ce dossier pour inscrire une source de package personnalisée pour leurs produits. En outre, la structure de dossiers prend en charge la sémantique du produit, de la version et même de la référence SKU de l’IDE. Les paramètres de ces répertoires sont appliqués dans l’ordre suivant avec une stratégie de priorité « dernière dans WINS ».

1. %ProgramData%\NuGet\Config\*. config
2. %ProgramData%\NuGet\Config\{IDE}\*. config
3. %ProgramData%\NuGet\Config\{IDE}\{version}\*. config
4. %ProgramData%\NuGet\Config\{IDE}\{version}\{SKU}\*. config

Dans cette liste, l’espace réservé {IDE} est spécifique à l’environnement de développement intégré dans lequel NuGet s’exécute. par conséquent, dans le cas de Visual Studio, il s’agit de « VisualStudio ». Les espaces réservés {version} et {SKU} sont fournis par l’IDE (par exemple, « 11,0 » et « WDExpress », « VWDExpress » et « Pro », respectivement). Le dossier peut ensuite contenir de nombreux fichiers *. config différents.
Par conséquent, la société du composant ACME peut, dans le cadre de son programme d’installation du produit, ajouter une source de package personnalisée qui sera visible uniquement dans les versions Professional et Ultimate de Visual Studio 2012 en créant le chemin de fichier suivant :

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Bien que la structure de dossiers permette aux programmes tels que les programmes d’installation de logiciels d’ajouter des sources de package à l’ensemble de l’ordinateur à la configuration de NuGet, la boîte de dialogue de configuration de NuGet a également été mise à jour pour permettre l’inscription des sources de package comme spécifiques à l’utilisateur (par exemple, inscrit dans% AppData%/NuGet/NuGet.Config) ou à l’ordinateur.

Cette fonctionnalité est utilisée par Visual Studio 2013, où un fichier est installé à l’emplacement suivant :

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Dans ce fichier, une nouvelle source de package appelée « packages .NET Frameworks » est configurée.

![Paramètres étendus de l’ordinateur du fichier de configuration NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Recherche contextuelle

À mesure que le nombre de packages traités par la galerie NuGet continue de croître à un rythme exponentiel, l’amélioration de la recherche reste toujours en haut de la liste de priorité NuGet. L’une des fonctionnalités planifiées pour NuGet est la recherche contextuelle, ce qui signifie que NuGet utilisera les informations relatives à la version et à la référence SKU de Visual Studio que vous utilisez, ainsi que le type de projet que vous générez comme critère pour déterminer la pertinence de la recherche potentielle. about.

À compter de NuGet 2,6, chaque fois qu’un package est installé, le contexte de l’installation est enregistré dans le cadre des données d’opération d’installation.  Les recherches envoient également les mêmes informations de contexte, ce qui permet à la galerie NuGet d’améliorer les résultats de recherche par des tendances d’installation contextuelles.  Une prochaine mise à jour de la galerie NuGet permettra d’améliorer la pertinence du contexte.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Suivi des installations directes et des installations de dépendances

Les auteurs de package reposent davantage et plus d’informations sur les [statistiques de package](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) fournies dans la galerie NuGet.  Un point de données significatif manquant que les auteurs ont demandés est une différenciation entre les installations de package directes et les installations de dépendances.  Jusqu’à présent, le client NuGet n’a pas envoyé de contexte autour de l’opération d’installation pour déterminer si le développeur a installé le package directement ou s’il a été installé pour satisfaire une dépendance.
À compter de NuGet 2,6, ces données sont maintenant envoyées pour l’opération d’installation.  Les statistiques des packages sur la galerie NuGet exposent ces données en tant qu’opérations d’installation distinctes, avec un suffixe « -Dependency ».

* Installez .
* Installation-dépendance
* Mise à jour
* Mise à jour-dépendance
* Réinstallation
* Réinstallation-dépendance

En plus du nom d’opération différent, l’ID de package dépendant est également enregistré pour l’installation.  Une prochaine mise à jour de la galerie NuGet expose les données dans les rapports, ce qui permet aux auteurs de packages de comprendre parfaitement comment les développeurs installent leurs packages.

## <a name="bug-fixes"></a>Correctifs de bogues

NuGet 2,6 comprend également plusieurs correctifs de bogues. Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2,6, consultez le [suivi des problèmes NuGet pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).