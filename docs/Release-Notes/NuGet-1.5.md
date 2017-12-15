---
title: Notes de publication NuGet 1.5 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3ec1ff28-18fc-4d53-bd43-208619a7270a
description: "Notes de publication pour la version 1.5 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 1.5 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29792f4c7399155bcf5fb3361d7f10ddd1b18ca1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
 # <a name="nuget-15-release-notes"></a>Notes de version 1.5 de NuGet

[Notes de publication NuGet 1.4](../release-notes/nuget-1.4.md) | [NuGet 1.6 Notes de publication](../release-notes/nuget-1.6.md)

NuGet 1.5 a été publiée le 30 août 2011.

## <a name="features"></a>Fonctionnalités

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Modèles de projet avec les Packages NuGet préinstallés
Lorsque vous créez un nouveau modèle de projet ASP.NET MVC 3, les bibliothèques de scripts jQuery inclus dans le projet réellement y sont placés en installant les packages NuGet.

Le modèle de projet ASP.NET MVC 3 inclut un ensemble de packages NuGet installés lorsque le modèle de projet est appelé. Cette possibilité d’inclure les packages NuGet avec un modèle de projet est maintenant une fonctionnalité de NuGet qui _tout_ modèle de projet peut désormais tirer parti de.

Pour plus d’informations sur cette fonctionnalité, lire ce [billet de blog par le développeur de la fonctionnalité](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Références d’Assembly explicite
Ajouté un nouveau `<references />` élément utilisé pour spécifier explicitement les assemblys dans le package doit être référencé.

Par exemple, si vous ajoutez le code suivant :

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Alors seulement le `xunit.dll` et `xunit.extensions.dll` sera référencé à partir de la commande appropriée [sous-dossier de profil du framework/](../schema/nuspec.md#explicit-assembly-references) de la `lib` dossier même si d’autres assemblys dans le dossier.

Si cet élément est omis, le comportement habituel s’applique, qui consiste à faire référence à chaque assembly dans le `lib` dossier.

__Quelle est l’utilité de cette fonctionnalité ?__

Cette fonctionnalité prend en charge les seuls les assemblys au moment du design. Par exemple, lors de l’utilisation de contrats de Code, les assemblys de contrat doivent être en regard des assemblys de runtime qui ils augmentent afin que Visual Studio peut trouver les, mais les assemblys de contrat ne doivent pas réellement référencés par le projet et ne doivent pas être copiés dans le `bin` dossier.

De même, la fonctionnalité peut être utilisée pour les infrastructures de tests unitaires telles que XUnit nécessitant ses assemblys d’outils située en regard des assemblys par le runtime, mais exclus des références de projet.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Possibilité d’exclure les fichiers dans le .nuspec
Le `<file>` élément au sein d’un `.nuspec` fichier peut être utilisé pour inclure un fichier spécifique ou un ensemble de fichiers à l’aide d’un caractère générique. Lorsque vous utilisez un caractère générique, il n’existe aucun moyen pour exclure un sous-ensemble spécifique de fichiers inclus. Par exemple, supposons que vous souhaitez que tous les fichiers texte dans un dossier à l’exception d’une valeur spécifique.

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

Ou utilisez un caractère générique à un ensemble de fichiers tels que tous les fichiers de sauvegarde

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Suppression de packages à l’aide de la boîte de dialogue vous invite à entrer pour supprimer les dépendances
Lorsque vous désinstallez un package avec des dépendances, NuGet vous invite à entrer, ce qui permet la suppression des dépendances d’un package, ainsi que le package.

![Suppression des packages dépendants](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package`amélioration de la commande
Le `Get-Package` commande prend désormais en charge un `-ProjectName` paramètre. Par conséquent, la commande

    Get-Package –ProjectName A

Répertorie tous les packages installés dans le projet A.

### <a name="support-for-proxies-that-require-authentication"></a>Prise en charge des serveurs proxy qui requièrent une authentification
Lorsque vous utilisez NuGet derrière un proxy qui nécessite une authentification, NuGet présent à entrer des informations d’identification du proxy. Entrer les informations d’identification permet de NuGet pour se connecter au référentiel distant.

### <a name="support-for-repositories-that-require-authentication"></a>Prise en charge pour les référentiels qui requièrent une authentification
NuGet prend désormais en charge la connexion à [de dépôts privés](../hosting-packages/local-feeds.md) nécessitant une authentification de base ou NTLM.

Prise en charge pour l’authentification Digest sera ajoutée dans une version ultérieure.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Améliorations des performances pour le référentiel nuget.org
Nous avons apporté plusieurs améliorations de performances dans la galerie nuget.org pour rendre le package répertorier et de recherche.

### <a name="solution-dialog-project-filtering"></a>Filtrage du projet solution boîte de dialogue
Dans le dialogue au niveau Solution, lors de la demande pour les projets installer, nous afficher uniquement les projets qui sont compatibles avec le package sélectionné.

### <a name="package-release-notes"></a>Notes de version de package
Les packages NuGet incluent désormais la prise en charge pour les notes de publication. Ces notes de publication affiche uniquement les lors de l’affichage _mises à jour_ pour un package, par conséquent, il n’a aucune signification pour les ajouter à votre première version.

![Notes de publication dans l’onglet mises à jour](./media/manage-nuget-packages-release-notes.png)

Pour ajouter des notes de publication à un package, utilisez la nouvelle `<releaseNotes />` élément de métadonnées dans votre fichier NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>.NuSpec & ltfiles /&gt; amélioration
Le `.nuspec` fichier permet désormais vide `<files />` élément, ce qui indique à nuget.exe ne pas à inclure n’importe quel fichier dans le package.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1.5 comportait 107 fixe des éléments de travail. 103 d'entre eux ont été marquées en tant que bogues.

Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.5, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correctifs de bogues à noter :

* [Problème 1273](http://nuget.codeplex.com/workitem/1273): apportées `packages.config` plus contrôle de version convivial en packages de tri par ordre alphabétique et en supprimant les espaces blancs supplémentaires.
* [Problème 844](http://nuget.codeplex.com/workitem/844): les numéros de Version sont désormais normalisées afin que `Install-Package 1.0` fonctionne sur un package avec la version `1.0.0`.
* [Problème 1060](http://nuget.codeplex.com/workitem/1060): lors de la création d’un package à l’aide de nuget.exe, le `-Version` indicateur substitue le `<version />` élément.
