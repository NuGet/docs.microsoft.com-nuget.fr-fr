---
title: Présentation et objectifs de NuGet
description: Une introduction complète à ce qu’est et ce que fait NuGet
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: 435103b600f14b9bbf606c09f0c870115204d5c7
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488495"
---
# <a name="an-introduction-to-nuget"></a>Présentation de NuGet

Il est essentiel pour toute plateforme de développement moderne de proposer un mécanisme permettant aux développeurs de créer, de partager et d’exploiter le code qui leur est utile. Souvent, ce code est groupé en « packages » contenant le code compilé (sous forme de DLL) ainsi que tout le contenu nécessaire aux projets qui les utilisent.

Dans le cas de .NET (y compris .NET Core), le mécanisme de partage de code pris en charge par Microsoft est **NuGet**. Il définit la façon dont les packages .NET sont créés, hébergés et utilisés, et [fournit des outils](install-nuget-client-tools.md) pour chacun de ces rôles.

Pour faire simple, un package NuGet est un fichier ZIP avec l’extension `.nupkg`, qui contient du code compilé (des DLL), d’autres fichiers liés à ce code et un manifeste descriptif qui inclut des informations comme le numéro de version du package. Les développeurs qui ont du code à partager créent des packages et les publient sur un hôte public ou privé. Les consommateurs récupèrent ces packages auprès des hôtes correspondants, les ajoutent à leurs projets, puis appellent leurs fonctionnalités dans le code de leur projet. NuGet gère ensuite lui-même tous les détails intermédiaires.

NuGet prenant en charge à la fois les hôtes privés et l’hôte nuget.org public, il est possible d’utiliser des packages NuGet pour partager du code dont une organisation ou un groupe de travail a l’exclusivité. Ils représentent également un moyen pratique d’intégrer son propre code pour l’utiliser uniquement dans ses propres projets. En bref, un package NuGet est une unité de code partageable, qui ne nécessite ni n’implique aucun mode de partage en particulier.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Flux des packages entre les créateurs, les hôtes et les consommateurs

Dans son rôle d’hôte public, NuGet gère lui-même le référentiel central de plus de 100 000 packages différents, sur [nuget.org](https://www.nuget.org). Ces packages sont utilisés chaque jour par des millions de développeurs .NET/.NET Core. NuGet vous permet également d’héberger des packages à titre privé dans le cloud (par exemple sur Azure DevOps), sur un réseau privé ou même seulement sur votre système de fichiers local. Ces packages sont ainsi réservés aux développeurs qui ont accès à l’hôte, ce qui permet de les mettre à la disposition d’un groupe spécifique de consommateurs. Les options sont expliquées dans [Hébergement de vos propres flux NuGet](hosting-packages/overview.md). Les options de configuration permettent également de choisir précisément quels hôtes seront accessibles à chaque ordinateur, ce qui garantit que les packages proviendront de sources spécifiques plutôt que d’un référentiel public comme nuget.org.

Quelle que soit sa nature, un hôte sert de point de connexion entre les *créateurs* et les *consommateurs* de packages. Les créateurs produisent des packages NuGet pratiques et les publient sur un hôte. Les consommateurs recherchent des packages pratiques et compatibles sur les hôtes accessibles, les téléchargent et incluent ces packages dans leurs projets. Une fois installés dans un projet, les API des packages sont disponibles pour le reste du code du projet.

![Relation entre les créateurs de packages, les hôtes de packages et les consommateurs de packages](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Compatibilité du ciblage de packages

Un package « compatible » est un package qui contient des assemblies créés pour au moins une version cible de .NET Framework compatible avec celle du projet qui utilise le package. Les développeurs peuvent soit créer des packages propres à une version, comme avec les contrôles UWP, soit prendre en charge un éventail plus large de versions cibles. Pour optimiser la compatibilité d’un package, ils ciblent [.NET Standard](/dotnet/standard/net-standard), que tous les projets .NET et .NET Core peuvent exploiter. C’est le moyen le plus efficace tant pour les créateurs que pour les consommateurs, car un package unique (qui contient généralement un seul assembly) fonctionne pour tous les projets.

Les développeurs de packages qui ont besoin d’API extérieures à .NET Standard, quant à eux, créent un assembly distinct pour chacune des versions cibles de .NET Framework qu’ils souhaitent prendre en charge, et les intègrent tous dans le même package (« ciblage multiple »). Lorsque un consommateur installe un package de ce type, NuGet extrait seulement les assemblies nécessaires au projet. Ceci réduit l’encombrement du package dans l’application finale et/ou dans les assemblys produits par ce projet. Un package à ciblage multiple est, bien sûr, plus difficile à gérer pour son créateur.

> [!Note]
> L’approche consistant à cibler .NET Standard remplace la précédente, qui impliquait d’utiliser différentes versions cibles de bibliothèques de classes portables (PCL). Cette documentation se concentre donc sur la création de packages pour .NET Standard.

## <a name="nuget-tools"></a>Outils NuGet

En plus de la prise en charge de l’hébergement, NuGet fournit également différents outils utilisés à la fois par les créateurs et par les consommateurs. Pour obtenir des outils spécifiques, consultez [Installation des outils clients NuGet](install-nuget-client-tools.md).

| Outil | Plateformes | Scénarios applicables | Description |
| --- | --- | --- | --- |
| [Interface CLI .NET](consume-packages/install-use-packages-dotnet-cli.md) | Tous | Création, consommation | Outil CLI pour les bibliothèques .NET Core et .NET Standard et pour les projets de style SDK qui ciblent le .NET Framework (consultez [Attribut SDK](/dotnet/core/tools/csproj#additions)). Propose certaines des fonctionnalités de l’interface CLI NuGet directement dans la chaîne d’outils .NET Core. Tout comme l’interface CLI `nuget.exe`, l’interface CLI dotnet n’interagit pas avec les projets Visual Studio. |
| [Interface CLI de nuget.exe](consume-packages/install-use-packages-nuget-cli.md) | Tous | Création, consommation | Outil CLI pour les bibliothèques .NET Framework et les projets qui ne sont pas de style SDK ciblant les bibliothèques .NET Standard. Fournit toutes les fonctionnalités de NuGet, avec certaines commandes s’appliquant spécifiquement aux créateurs de package, certaines seulement aux consommateurs et d’autres aux deux. Par exemple, les créateurs de packages utilisent la commande `nuget pack` pour créer un package à partir de différents assemblies et des fichiers associés, les consommateurs utilisent `nuget install` pour inclure des packages dans un dossier de projet, et tous utilisent `nuget config` pour définir les variables de configuration NuGet. L’interface CLI NuGet, indépendante de la plateforme, n’interagit pas avec les projets Visual Studio. |
| [Console du Gestionnaire de package](consume-packages/install-use-packages-powershell.md) | Visual Studio sur Windows | Consommation | Propose des [commandes PowerShell](reference/Powershell-Reference.md) permettant d’installer et de gérer des packages dans les projets Visual Studio. |
| [Interface utilisateur du Gestionnaire de package](consume-packages/install-use-packages-visual-studio.md) | Visual Studio sur Windows | Consommation | Propose une interface utilisateur facile d’utilisation permettant d’installer et de gérer des packages dans les projets Visual Studio. |
| [Interface utilisateur de gestion de NuGet](/visualstudio/mac/nuget-walkthrough) | Visual Studio pour Mac | Consommation | Propose une interface utilisateur facile d’utilisation permettant d’installer et de gérer des packages dans les projets Mac. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Création, consommation | Offre la possibilité de créer et de restaurer directement des packages utilisés dans un projet avec la chaîne d’outils MSBuild. |

Comme on peut le constater, les outils NuGet à utiliser dépendent fortement de l’activité (création, utilisation ou publication de packages), ainsi que de la plateforme utilisée. Les créateurs de packages en sont en général également des consommateurs, car ils s’appuient sur des fonctionnalités qui existent dans d’autres packages NuGet. Bien sûr, ces packages peuvent à leur tour dépendre d’autres packages.

Pour plus d’informations, commencez par les articles [Workflow de création de packages](create-packages/Overview-and-Workflow.md) et [Workflow d’utilisation de packages](consume-packages/Overview-and-Workflow.md).

## <a name="managing-dependencies"></a>Gestion des dépendances

La facilité à s’appuyer sur le travail des autres est l’un des aspects les plus puissants d’un système de gestion des packages. En conséquence, la plus grande partie du travail effectué par NuGet consiste à gérer cette arborescence ou ce « graphique » de dépendance pour chaque projet. Autrement dit, vous devez vous préoccuper seulement des packages que vous utilisez directement dans un projet. Si l’un d’entre eux utilise lui-même d’autres packages (et ainsi de suite), NuGet se charge de toutes ces dépendances des niveaux inférieurs.

L’illustration suivante montre un projet qui dépend de cinq packages, qui à leur tour dépendent de plusieurs autres.

![Exemple de graphe des dépendances NuGet pour un projet .NET](media/dependency-graph.png)

Notez que certains packages apparaissent plusieurs fois dans le graphe des dépendances. Par exemple, il existe trois consommateurs différents du package B, et chaque consommateur peut également spécifier une version différente pour ce package (non représenté). C’est un cas courant, en particulier pour les packages les plus utilisés. Heureusement, NuGet se charge de tout le travail en identifiant exactement la version du package B qui convient à tous les consommateurs. NuGet fait ensuite de même pour tous les autres packages, quelle que soit la profondeur du graphique de dépendance.

Pour plus d’informations sur la façon dont NuGet réalise ce service, consultez [Résolution des dépendances](concepts/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Suivi des références et restauration de packages

Compte tenu de la simplicité de déplacement de projets entre différents ordinateurs de développeurs, référentiels de contrôle de code source, serveurs de builds, etc., il est très peu pratique de conserver les assemblys binaires de packages NuGet directement liés à un projet. Cela aurait pour effet d’encombrer inutilement chacune des copies du projet (et ainsi de gaspiller de l’espace dans les référentiels de contrôle de code source). Il serait également très difficile de mettre à jour les fichiers binaires des packages, car la nouvelle version devrait s’appliquer à toutes les copies du projet.

NuGet gère plutôt une simple liste de références des packages dont dépend le projet, qui englobe les dépendances de niveau supérieur et de niveau inférieur. Autrement dit, lorsque un package est installé dans un projet à partir d’un hôte, NuGet enregistre l’identificateur et le numéro de version du package dans cette liste de références. (La désinstallation d’un package supprime bien sûr celui-ci de la liste.) NuGet offre un moyen de restaurer tous les packages référencés à la demande, comme le décrit la section [Restauration de packages](consume-packages/package-restore.md).

![Une liste des références NuGet est créée à l’installation du package et elle peut être utilisée pour restaurer des packages ailleurs.](media/nuget-restore.png)

Avec seulement la liste des références, NuGet peut à tout moment réinstaller &mdash; autrement dit, *restaurer* &mdash; tous ces packages à partir d’hôtes publics et privés. Pour valider un projet dans le contrôle de code source ou le partager par un autre moyen, il suffit d’inclure la liste des références et d’exclure les fichiers binaires des packages (consultez la section [Packages et contrôle de code source](consume-packages/packages-and-source-control.md).)

L’ordinateur qui reçoit un projet, par exemple un serveur de builds obtenant une copie du projet dans le cadre d’un système de déploiement automatisé, demande simplement à NuGet de restaurer les dépendances quand elles sont nécessaires. Les systèmes de build, comme Azure DevOps, fournissent des étapes de « restauration NuGet » à cette fin. De même, lorsque les développeurs récupèrent une copie d’un projet (par exemple, en clonant un référentiel), ils peuvent appeler une commande du type `nuget restore` (interface CLI NuGet), `dotnet restore` (interface CLI dotnet) ou `Install-Package` (console du Gestionnaire de package) pour avoir tous les packages nécessaires. Visual Studio, pour sa part, restaure automatiquement les packages lors de la création d’un projet (tant que la restauration automatique est activée, comme l’explique la page [Restauration de package](consume-packages/package-restore.md)).

Le rôle principal de NuGet pour les développeurs est clairement de gérer cette liste de références pour le compte de votre projet, et de fournir les moyens de restaurer efficacement (et de mettre à jour) les packages référencés. Cette liste est gérée dans un des deux *formats de gestion des packages*, nommés :

- [PackageReference](consume-packages/package-references-in-project-files.md) (ou « Références des packages dans les fichiers projet ») : *(NuGet 4.0+)* Gère la liste des dépendances de niveau supérieur d’un projet directement dans le fichier projet ; aucun fichier distinct n’est nécessaire. Un fichier associé, `obj/project.assets.json`, est généré dynamiquement pour gérer le graphique de dépendance global des packages utilisés par un projet, ainsi que toutes les dépendances de bas niveau. PackageReference est toujours utilisé par les projets .NET Core.

- [`packages.config`](reference/packages-config.md) : *(NuGet 1.0+)* Fichier XML qui gère une liste plate de toutes les dépendances du projet, notamment les dépendances des autres packages installés. Les packages installés ou restaurés sont stockés dans un dossier `packages`.

Le format de gestion des packages utilisé dépend du type de projet, ainsi que de la version disponible de NuGet (ou de Visual Studio). Pour savoir quel format est utilisé, recherchez `packages.config` dans la racine du projet après avoir installé votre premier package. Si vous ne possédez pas ce fichier, recherchez l’élément \<PackageReference\> directement dans le fichier projet.

Si vous avez le choix, nous vous recommandons d’utiliser PackageReference. `packages.config` est conservé pour des raisons d’héritage et ne fait plus l’objet d’un développement actif.

> [!Tip]
> Diverses commandes CLI `nuget.exe`, comme `nuget install`, n’ajoutent pas automatiquement le package à la liste de référence. La liste est mise à jour lors de l’installation d’un package avec le Gestionnaire de package de Visual Studio (interface utilisateur ou console) et l’interface CLI `dotnet.exe`.

## <a name="what-else-does-nuget-do"></a>Autres fonctionnalités de NuGet

Nous avons vu jusqu’ici les caractéristiques suivantes de NuGet :

- NuGet propose le référentiel central nuget.org, qui prend en charge l’hébergement privé.
- NuGet fournit les outils dont les développeurs ont besoin pour créer, publier et consommer des packages.
- Plus important encore, NuGet gère la liste des références des packages utilisés dans le projet, et a la capacité de restaurer et de mettre à jour ces packages à partir de cette liste.

Pour que ces processus fonctionnent efficacement, NuGet effectue certaines optimisations en arrière-plan. En particulier, NuGet gère un cache de package et un dossier de packages globaux pour accélérer l’installation et la réinstallation. Le cache évite d’avoir à télécharger un package déjà installé sur l’ordinateur. Grâce au dossier de packages globaux, plusieurs projets peuvent partager le même package installé, ce qui réduit l’encombrement global de NuGet sur l’ordinateur. Le cache et le dossier de packages globaux sont également très pratiques pour restaurer fréquemment un grand nombre de packages, comme sur un serveur de builds. Pour plus d’informations sur ces mécanismes, consultez [Gérer les dossiers de packages globaux et de cache](consume-packages/managing-the-global-packages-and-cache-folders.md).

Pour un projet donné, NuGet gère le graphique de dépendance global, ce qui implique de résoudre à nouveau des références multiples à différentes versions du même package. Il est fréquent qu’un projet ait une dépendance d’un ou plusieurs packages qui ont eux-mêmes les mêmes dépendances. Par exemple, certains des packages utilitaires les plus pratiques de nuget.org sont utilisés par beaucoup d’autres packages. Pris dans sa totalité, le graphique de dépendance peut facilement comporter dix références distinctes à des versions différentes du même package. Pour éviter d’importer plusieurs versions de ce package dans l’application elle-même, NuGet repère la version utilisable par tout le monde. (Pour plus d’informations, consultez la page [Résolution des dépendances](concepts/dependency-resolution.md).)

De plus, NuGet gère toutes les spécifications liées à la façon dont les packages sont structurés (notamment la [localisation](create-packages/creating-localized-packages.md) et les [symboles de débogage](create-packages/symbol-packages.md)) et dont ils sont [référencés](consume-packages/package-references-in-project-files.md) (notamment les [plages de versions](concepts/package-versioning.md#version-ranges-and-wildcards) et les [préversions](create-packages/prerelease-packages.md).) NuGet propose également différentes API permettant d’interagir par programme avec ses services, et offre un support aux développeurs qui écrivent des modèles de projet et des extensions Visual Studio.

Prenez un moment pour parcourir la table des matières de cette documentation : toutes ces fonctionnalités y sont représentées, ainsi que des notes de publication remontant aux débuts de NuGet.

## <a name="comments-contributions-and-issues"></a>Commentaires, contributions et problèmes

Enfin, les commentaires et les contributions à cette documentation sont les bienvenus &mdash; sélectionnez simplement les commandes **Commentaires** et **Modifier** en haut d’une page, ou consultez le [référentiel de documents ](https://github.com/NuGet/docs.microsoft.com-nuget/) et la [liste des documents consacrés aux problèmes](https://github.com/NuGet/docs.microsoft.com-nuget/issues) sur GitHub.

Nous apprécions également les contributions à NuGet à proprement parler sur ses [différents référentiels GitHub](https://github.com/NuGet/Home) ; vous trouverez les problèmes de NuGet sur [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Profitez de votre expérience NuGet !
