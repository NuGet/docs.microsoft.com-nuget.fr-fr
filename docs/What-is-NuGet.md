---
title: "Présentation et objectifs de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "Une introduction complète à ce qu’est et ce que fait NuGet"
keywords: "gestionnaire de package NuGet, consommation, création de package, hébergement de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2bc6a9e154df287fee6a7e00cc1349dfa2100643
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="an-introduction-to-nuget"></a>Présentation de NuGet

Un mécanisme à travers lequel les développeurs peuvent créer, partager et consommer du code utile est un outil indispensable pour toutes les plateformes de développement modernes. Souvent, ce code est fourni dans des « packages » qui contiennent du code compilé (sous forme de DLL) et tout autre contenu nécessaire aux projets qui utilisent ces packages.

Pour .NET, le mécanisme de partage de code est **NuGet**, qui définit comment les packages pour .NET sont créés, hébergés et consommés, et qui fournit les outils pour chacun de ces rôles. 

Pour faire simple, un package NuGet est un fichier ZIP avec l’extension `.nupkg`, qui contient du code compilé (des DLL), d’autres fichiers liés à ce code et un manifeste descriptif qui inclut des informations comme le numéro de version du package. Les développeurs de bibliothèques créent des fichiers de package et les publient sur un hôte. Les consommateurs de package reçoivent ces packages, les ajoutent à leurs projets, puis appellent les fonctionnalités de cette bibliothèque dans le code de leur projet. NuGet gère ensuite lui-même tous les détails intermédiaires.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Flux des packages entre les créateurs, les hôtes et les consommateurs

Dans son rôle d’hôte, NuGet gère lui-même le référentiel central de plus de 60 000 packages différents, disponible à titre public sur [nuget.org](https://www.nuget.org). Ces packages sont utilisés chaque jour par des millions de développeurs .NET. NuGet vous permet également d’héberger des packages à titre privé dans le cloud, sur un réseau privé ou même seulement sur votre système de fichiers local. De cette façon, ces packages sont disponibles seulement pour les développeurs au sein d’une organisation particulière ou d’un certain groupe chez un client. Les options sont expliquées dans [Hébergement de vos propres flux NuGet](Hosting-Packages/Overview.md).

Quelle que soit sa nature, un hôte sert de point de connexion entre les *créateurs* de packages et les *consommateurs* de packages. Les créateurs produisent des packages NuGet pratiques et les publient sur un hôte. Les consommateurs recherchent des packages pratiques et compatibles sur les hôtes accessibles, les téléchargent et incluent ces packages dans leurs projets. Une fois installés dans un projet, les API des packages sont disponibles pour le reste du code du projet.

![Relation entre les créateurs de packages, les hôtes de packages et les consommateurs de packages](media/nuget-roles.png)

Dans ce cas, un package « compatible » signifie qu’il contient des assemblys générés pour au moins un framework .NET cible qui est compatible avec le framework cible du projet qui consomme le package. Pour rendre un package compatible à une grande échelle, son créateur compile des assemblys distincts pour différents frameworks cibles et les inclut tous dans le même package. Quand un consommateur installe ce package, NuGet extrait seulement les assemblys qui sont nécessaires pour le projet. Ceci réduit l’encombrement du package dans l’application finale et/ou dans les assemblys produits par ce projet.

## <a name="nuget-tools"></a>Outils NuGet

En plus de la prise en charge de l’hébergement, NuGet fournit également différents outils utilisés à la fois par les créateurs et par les consommateurs :

| Outil | Plateformes | Scénarios applicables | Description |
| --- | --- | --- | --- |
| [Interface CLI de nuget.exe](Tools/nuget-exe-CLI-Reference.md) | Tous | Création, consommation | Fournit toutes les fonctionnalités de NuGet, avec certaines commandes s’appliquant spécifiquement aux créateurs de package, certaines seulement aux consommateurs et d’autres aux deux. Par exemple, les créateurs de packages utilisent la commande `nuget pack` pour créer un package à partir de différents assemblys et de fichiers associés, les consommateurs de packages utilisent `nuget install` pour inclure des packages dans un projet, et tous utilisent `nuget config` pour définir les variables de configuration de NuGet.  |
| [Interface utilisateur du Gestionnaire de package](Tools/Package-Manager-UI.md) | Visual Studio sur Windows | Consommation | Fournit une interface utilisateur facile à utiliser pour l’installation et la gestion des packages dans les projets .NET. | 
| [Interface utilisateur de gestion de NuGet](/visualstudio/mac/nuget-walkthrough) | Visual Studio pour Mac | Consommation | Fournit une interface utilisateur facile à utiliser pour l’installation et la gestion des packages dans les projets .NET. |
| [Console du Gestionnaire de package](Tools/Package-Manager-Console.md) | Visual Studio sur Windows | Consommation | Fournit des [commandes PowerShell](Tools/Powershell-Reference.md) pour l’installation et la gestion des packages dans les projets .NET. | 
| [Interface CLI .NET](Tools/dotnet-Commands.md) | Tous | Création, consommation | Fournit certaines fonctionnalités de l’interface utilisateur de NuGet directement dans la chaîne d’outils .NET Core. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Création, consommation | Fournit la possibilité de créer et de restaurer des packages utilisés dans un projet directement via la chaîne d’outils MSBuild. |

Comme vous pouvez le voir, les outils que vous utilisez avec NuGet dépendent fortement du fait que vous créez (et vous publiez) des packages ou que vous les consommez, ainsi que de la plateforme sur laquelle vous travaillez. Vous pouvez trouver des détails plus spécifiques dans les rubriques [Flux de travail de création des packages](Create-Packages/Overview-and-Workflow.md) et [Flux de travail de consommation des packages](Consume-Packages/Overview-and-Workflow.md), ainsi que dans d’autres rubriques de ces sections. 

Les créateurs de packages en sont en général également des consommateurs, car ils s’appuient sur des fonctionnalités qui existent dans d’autres packages NuGet. Bien sûr, ces packages peuvent à leur tour dépendre d’autres packages.

## <a name="managing-dependencies"></a>Gestion des dépendances

La possibilité de créer facilement en s’appuyant sur le travail des autres est une des choses qui rend un système de gestion de packages si puissant. En conséquence, la plus grande partie du travail effectué par NuGet est de gérer cette arborescence des dépendances ou « graphe » pour le compte de votre projet. Autrement dit, vous devez vous préoccuper seulement des packages que vous utilisez directement dans un projet. Si un de ces packages consomme lui-même d’autres packages (qui peuvent consommer des packages), NuGet se charge de toutes ces dépendances des niveaux inférieurs.

L’illustration suivante montre un projet qui dépend de cinq packages, qui à leur tour dépendent de plusieurs autres.  

![Exemple de graphe des dépendances NuGet pour un projet .NET](media/dependency-graph.png)

Notez que certains packages apparaissent plusieurs fois dans le graphe des dépendances. Par exemple, il existe trois consommateurs différents du package B, et chaque consommateur peut également spécifier une version différente pour ce package (non représenté). Comme il s’agit d’une situation courante, NuGet se charge heureusement de tout le travail permettant de déterminer exactement quelle version du package B correspond à tous ses consommateurs. NuGet fait ensuite de même pour tous les autres packages, quelle que soit la profondeur du graphe des dépendances.

Pour plus d’informations sur la façon dont NuGet réalise ce service, consultez [Résolution des dépendances](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Suivi des références et restauration de packages

Comme les projets peuvent facilement être déplacés entre les ordinateurs des développeurs, entre les référentiels de contrôle de code source, entre les serveurs de builds, etc., il est très peu pratique de conserver les assemblys binaires des packages NuGet directement liés à un projet. Non seulement ceci rendrait chaque copie du projet inutilement surchargée (et gaspillerait donc de l’espace dans les référentiels de contrôle de code source), mais cela rendrait aussi très difficile la mise à jour des fichiers binaires du package vers des versions plus récentes, car la mise à jour devrait être effectuée sur toutes les copies du projet. 

Au lieu de cela, NuGet gère une liste des références des packages dont un projet dépend (y compris les dépendances des niveaux supérieurs et des niveaux inférieurs), et offre la possibilité de restaurer à la demande tous les packages référencés, comme décrit dans [Restaurer des packages](Consume-Packages/Package-Restore.md). Autrement dit, quand vous installez un package dans un projet à partir d’un hôte, NuGet enregistre l’identificateur du package et le numéro de sa version dans cette liste de références. (La désinstallation d’un package supprime bien sûr celui-ci de la liste.) 

![Une liste des références NuGet est créée à l’installation du package et elle peut être utilisée pour restaurer des packages ailleurs.](media/nuget-restore.png)

Avec seulement la liste des références NuGet peut alors à tout moment réinstaller, &mdash;autrement dit, restaurer&mdash;, tous ces packages à partir d’hôtes publics et/ou privés. (Pour cette raison, nuget.org n’autorise pas la suppression définitive des packages publiés, même s’ils peuvent être masqués. Consultez [Suppression de packages](Policies/deleting-packages.md).) Lors de la validation d’un projet dans le contrôle de code source ou lors du partage d’un projet par un autre moyen, vous devez seulement inclure la liste des références : vous n’avez pas besoin d’inclure les fichiers binaires des packages (consultez [Packages et contrôle de code source](Consume-Packages/Packages-and-Source-Control.md).)

L’ordinateur qui reçoit un projet, par exemple un serveur de builds obtenant une copie du projet dans le cadre d’un système de déploiement automatisé, demande simplement à NuGet de restaurer les dépendances quand elles sont nécessaires. Les systèmes de génération, comme Visual Studio Team Services, fournissent des étapes de « restauration NuGet » à cette fin. De même, quand des développeurs obtiennent une copie d’un projet (comme lors du clonage d’un référentiel), puis ouvrent le projet dans Visual Studio et effectuent une génération, Visual Studio restaure automatiquement les packages NuGet nécessaires. Les développeurs peuvent également indiquer à tout moment à NuGet de restaurer des packages avec la commande CLI `nuget restore` ou l’applet de commande `Install-Package` dans la console du Gestionnaire de package.

Le rôle principal de NuGet pour les développeurs est clairement de gérer cette liste de références pour le compte de votre projet, et de fournir les moyens de restaurer efficacement (et de mettre à jour) les packages référencés.

La façon dont cela se passe exactement a évolué au fil des différentes versions de NuGet, aboutissant à plusieurs *formats de gestion des packages* qui s’appellent comme suit :

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0+)* Un fichier XML qui gère une liste plate de toutes les dépendances du projet, y compris les dépendances des autres packages installés. 
- [`project.json`](Schema/project-json.md): *(NuGet 3.0+)* Un fichier JSON qui gère une liste des dépendances du projet avec un graphe global des packages dans un fichier associé, `project.lock.json`. Cette structure offre de meilleures performances que `packages.config`, comme cela est décrit dans [Résolution des dépendances](Consume-Packages/Dependency-Resolution.md), notamment pour la restauration transitive, mais elle a elle-même généralement été remplacée par PackageReference, décrit ci-dessous.
- [Références des packages dans les fichiers projet ](Consume-Packages/Package-References-in-Project-Files.md) (également appelé « PackageReference ») | *(NuGet 4.0 +)* Gère une liste des dépendances des niveaux supérieurs d’un projet directement dans le fichier projet, aucun fichier distinct n’étant alors nécessaire. Un fichier associé, `project.assets.json`, est généré dynamiquement, ainsi que `project.lock.json`, pour gérer le graphe des dépendances global.

Le format de gestion des packages utilisé dans un projet donné dépend du type de projet, ainsi que de la version disponible de NuGet et de Visual Studio. Pour trouver le format est utilisé, il suffit de rechercher `packages.config` ou `project.json` dans la racine du projet après l’installation de votre premier package. Si vous ne voyez aucun de ces fichiers, recherchez un élément &lt;PackageReference&gt; directement dans le fichier projet.

Par exemple, dans Visual Studio 2017, la plupart des types de projet utilisent `packages.config`, à l’exception des projets UWP C# et .NET Core, qui utilisent PackageReference. 

## <a name="what-else-does-nuget-do"></a>Autres fonctionnalités de NuGet

Pour résumer ce que nous venons de voir, on peut dire que NuGet fournit (dans son rôle d’hébergement) le référentiel nuget.org central et qu’il prend en charge l’hébergement privé. NuGet fournit les outils dont les développeurs ont besoin pour créer, publier et consommer des packages. Plus important, NuGet gère une liste des références des packages utilisés dans un projet, et a la capacité de restaurer et de mettre à jour ces packages à partir de cette liste.

Pour que ces processus fonctionnent efficacement, NuGet effectue certaines optimisations en arrière-plan. Plus particulièrement, NuGet gère des caches de packages à la fois au niveau de l’ordinateur et au niveau du projet, de façon à réduire le temps nécessaire à l’installation et à la réinstallation. Pour ce qui concerne le cache au niveau de l’ordinateur, les packages que vous téléchargez et que vous installez dans un projet sont stockés dans le cache : ainsi, l’installation d’un même package dans un autre projet ne nécessite pas son retéléchargement. Ceci est réellement très pratique quand vous restaurez fréquemment un grand nombre de packages, comme sur un serveur de builds. Pour plus d’informations sur ce mécanisme et comment l’utiliser, consultez [Gestion du cache NuGet](Consume-Packages/Managing-the-Nuget-Cache.md).

Dans un projet individuel, NuGet effectue un travail considérable pour gérer le graphe des dépendances global. (Quand vous utilisez `project.json` ou &lt;PackageReference&gt;, NuGet conserve ces informations dans des fichiers secondaires, appelés respectivement `project.lock.json` et `project.assets.json`.) Cela inclut à nouveau la résolution de plusieurs références à des versions différentes du même package.

Autrement dit, il est fréquent qu’un projet ait une dépendance d’un ou plusieurs packages qui ont eux-mêmes les mêmes dépendances. Par exemple, certains des packages d’utilitaires les plus utiles sur nuget.org sont utilisés par de nombreux autres packages. Dans tout le graphique des dépendances, vous pouvez facilement avoir dix références différentes à des versions différentes du même package. Vous ne voulez cependant pas importer plusieurs versions de ce package dans l’application elle-même : NuGet filtre donc la version que tout le monde peut utiliser. (Pour plus d’informations à ce sujet, consultez [Résolution des dépendances](Consume-Packages/Dependency-Resolution.md).)

De plus, NuGet gère toutes les spécifications liées à la façon dont les packages sont structurés (notamment la [localisation](Create-Packages/Creating-Localized-Packages.md) et les [symboles de débogage](Create-Packages/Symbol-Packages.md)) et dont ils sont référencés (notamment les [plages de versions](reference/package-versioning.md#version-ranges-and-wildcards) et les [préversions](create-packages/Prerelease-Packages.md).) NuGet fournit également des API pour les fournisseurs d’informations d’identification (pour accéder à des hôtes privés), et pour les développeurs qui écrivent des extensions et des modèles de projet Visual Studio.

Prenez un moment pour parcourir la table des matières de cette documentation : vous pouvez y voir figurer toutes ces fonctionnalités, ainsi que des notes de publication remontant aux débuts de NuGet.

## <a name="comments-contributions-and-issues"></a>Commentaires, contributions et problèmes

Enfin, nous apprécions beaucoup les commentaires et les contributions pour cette documentation&mdash;sélectionnez simplement les commandes **Commentaires** et **Modifier** sur une page, ou visitez le [dépôt de documents ](https://github.com/NuGet/docs.microsoft.com-nuget/) et la [liste des documents consacrés aux problèmes](https://github.com/NuGet/docs.microsoft.com-nuget/issues) sur GitHub.

Nous apprécions également les contributions à NuGet lui-même via ses [différents dépôts GitHub](https://github.com/NuGet/Home). Vous pouvez trouver les problèmes de NuGet sur [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Profitez de votre expérience NuGet !
