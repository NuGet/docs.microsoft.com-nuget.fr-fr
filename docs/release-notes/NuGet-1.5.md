---
title: Notes de version 1.5 de NuGet
description: Notes de publication pour 1.5 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548723"
---
# <a name="nuget-15-release-notes"></a>Notes de version 1.5 de NuGet

[Notes de publication de NuGet 1.4](../release-notes/nuget-1.4.md) | [Notes de publication de NuGet 1.6](../release-notes/nuget-1.6.md)

NuGet 1.5 a été publiée le 30 août 2011.

## <a name="features"></a>Fonctionnalités

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Modèles de projet avec les Packages NuGet préinstallés
Lorsque vous créez un nouveau modèle de projet ASP.NET MVC 3, les bibliothèques de scripts jQuery inclus dans le projet réellement y sont placés en installant les packages NuGet.

Le modèle de projet ASP.NET MVC 3 inclut un ensemble de packages NuGet installés lorsque le modèle de projet est appelé. Cette possibilité d’inclure des packages NuGet avec un modèle de projet est maintenant une fonctionnalité de NuGet qui _n’importe quel_ modèle de projet permettre désormais tirer parti de.

Pour plus d’informations sur cette fonctionnalité, consultez ce [billet de blog par le développeur de la fonctionnalité](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Références d’Assembly explicite

Ajouté une nouvelle `<references />` élément utilisé pour spécifier explicitement les assemblys dans le package doit être référencé.

Par exemple, si vous ajoutez le code suivant :

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Seuls les `xunit.dll` et `xunit.extensions.dll` sera référencé à partir de la commande appropriée [sous-dossier de framework/profil](../reference/nuspec.md#explicit-assembly-references) de la `lib` dossier même si d’autres assemblys dans le dossier.

Si cet élément est omis, le comportement habituel s’applique, qui consiste à faire référence à chaque assembly dans le `lib` dossier.

__Quelle est l’utilité de cette fonctionnalité ?__

Cette fonctionnalité prend en charge les assemblys uniquement au moment du design. Par exemple, lorsque vous utilisez des contrats de Code, les assemblys de contrat doivent être en regard des assemblys de runtime qu’ils augmentent afin que Visual Studio puisse les trouver, mais les assemblys de contrat ne doivent pas réellement être référencés par le projet et ne doivent pas être copiés dans le `bin` dossier.

De même, la fonctionnalité peut être utilisée à pour les infrastructures de tests unitaires comme XUnit nécessitant ses assemblys d’outils située en regard des assemblys par le runtime, mais exclu des références de projet.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Ajout de la possibilité d’exclure des fichiers dans le fichier .nuspec
Le `<file>` élément au sein d’un `.nuspec` fichier peut être utilisé pour inclure un fichier spécifique ou un ensemble de fichiers à l’aide d’un caractère générique. Lorsque vous utilisez un caractère générique, il n’existe aucun moyen pour exclure un sous-ensemble spécifique des fichiers inclus. Par exemple, supposons que vous voulez tous les fichiers de texte dans un dossier à l’exception d’une valeur spécifique.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Utilisez des points-virgules pour spécifier plusieurs fichiers.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Ou utilisez un caractère générique à exclure un ensemble de fichiers tels que tous les fichiers de sauvegarde

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Suppression des packages à l’aide de la boîte de dialogue vous invite à entrer pour supprimer des dépendances
Lorsque vous désinstallez un package avec des dépendances, NuGet vous invite à entrer, ce qui permet la suppression des dépendances d’un package, ainsi que le package.

![Suppression des packages dépendants](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` amélioration de la commande
Le `Get-Package` commande prend désormais en charge un `-ProjectName` paramètre. Par conséquent, la commande

    Get-Package –ProjectName A

Répertorie tous les packages installés dans le projet A.

### <a name="support-for-proxies-that-require-authentication"></a>Prise en charge des serveurs proxy qui requièrent une authentification
Lorsque vous utilisez NuGet derrière un proxy qui requiert une authentification, NuGet vous invite désormais des informations d’identification du proxy. Entrer les informations d’identification permet de NuGet pour se connecter au référentiel distant.

### <a name="support-for-repositories-that-require-authentication"></a>Prise en charge pour les dépôts qui requièrent une authentification
NuGet prend désormais en charge la connexion à [référentiels privés](../hosting-packages/local-feeds.md) nécessitant une authentification de base ou NTLM.

Prise en charge pour l’authentification Digest figurera dans une version ultérieure.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Améliorations des performances pour le référentiel nuget.org
Nous avons apporté plusieurs améliorations de performances dans la galerie nuget.org pour rendre le package de liste et de recherche plus rapidement.

### <a name="solution-dialog-project-filtering"></a>Filtrage de solution boîte de dialogue projet
Dans le niveau de la Solution boîte de dialogue, lors d’une demande pour les projets installer, nous expliquons seulement les projets qui sont compatibles avec le package sélectionné.

### <a name="package-release-notes"></a>Notes de publication de package
Les packages NuGet incluent désormais la prise en charge des notes de publication. Les notes de publication affiche uniquement les lors de l’affichage _mises à jour_ pour un package, par conséquent, il est inutile pour les ajouter à votre première version.

![Notes de publication dans l’onglet mises à jour](./media/manage-nuget-packages-release-notes.png)

Pour ajouter des notes de publication à un package, utilisez la nouvelle `<releaseNotes />` élément de métadonnées dans votre fichier NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>.NuSpec & ltfiles /&gt; amélioration du produit
Le `.nuspec` fichier permet désormais vide `<files />` élément, ce qui indique à nuget.exe ne pas à inclure n’importe quel fichier dans le package.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1.5 comportait 107 fixe des éléments de travail. 103 de ceux ont été marquées comme des bogues.

Pour obtenir une liste complète de travail éléments résolus dans NuGet 1.5, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correctifs de bogues à noter :

* [Problème 1273](http://nuget.codeplex.com/workitem/1273): apportées `packages.config` plus convivial en packages de tri par ordre alphabétique et en supprimant les espaces blancs supplémentaires de contrôle de version.
* [Problème 844](http://nuget.codeplex.com/workitem/844): numéros de Version sont désormais normalisées afin que `Install-Package 1.0` fonctionne sur un package avec la version `1.0.0`.
* [Problème 1060](http://nuget.codeplex.com/workitem/1060): lors de la création d’un package à l’aide de nuget.exe, le `-Version` indicateur substitue le `<version />` élément.
