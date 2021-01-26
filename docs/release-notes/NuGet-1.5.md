---
title: Notes de publication de NuGet 1,5
description: Notes de publication de NuGet 1,5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777095"
---
# <a name="nuget-15-release-notes"></a>Notes de publication de NuGet 1,5

Notes de publication de [NuGet 1,4](../release-notes/nuget-1.4.md)  |  [Notes de publication de NuGet 1,6](../release-notes/nuget-1.6.md)

NuGet 1,5 a été publié le 30 août 2011.

## <a name="features"></a>Fonctionnalités

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Modèles de projet avec des packages NuGet préinstallés
Lors de la création d’un nouveau modèle de projet ASP.NET MVC 3, les bibliothèques de scripts jQuery incluses dans le projet y sont placées en installant les packages NuGet.

Le modèle de projet ASP.NET MVC 3 comprend un ensemble de packages NuGet qui sont installés lorsque le modèle de projet est appelé. Cette possibilité d’inclure des packages NuGet avec un modèle de projet est maintenant une fonctionnalité de NuGet que _n’importe quel_ modèle de projet peut désormais tirer parti de.

Pour plus d’informations sur cette fonctionnalité, lisez ce billet [de blog par le développeur de la fonctionnalité](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Références d’assembly explicites

Ajout d’un nouvel `<references />` élément utilisé pour spécifier explicitement les assemblys dans le package à référencer.

Par exemple, si vous ajoutez ce qui suit :

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Ensuite, seuls `xunit.dll` et `xunit.extensions.dll` seront référencés à partir du sous [-dossier Framework/profil](../reference/nuspec.md#explicit-assembly-references) approprié du `lib` dossier, même s’il existe d’autres assemblys dans le dossier.

Si cet élément est omis, le comportement habituel s’applique, qui consiste à référencer chaque assembly dans le `lib` dossier.

__À quoi sert cette fonctionnalité ?__

Cette fonctionnalité prend en charge uniquement les assemblys au moment de la conception. Par exemple, lors de l’utilisation de contrats de code, les assemblys de contrat doivent être en regard des assemblys de Runtime qu’ils ajoutent afin que Visual Studio puisse les trouver, mais les assemblys de contrat ne doivent pas être réellement référencés par le projet et ne doivent pas être copiés dans le `bin` dossier.

De même, la fonctionnalité peut être utilisée pour les infrastructures de tests unitaires telles que XUnit qui nécessitent que ses assemblys d’outils soient situés à côté des assemblys de Runtime, mais exclus des références de projet.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Ajout de la possibilité d’exclure des fichiers dans le fichier. NuSpec
L' `<file>` élément d’un `.nuspec` fichier peut être utilisé pour inclure un fichier spécifique ou un ensemble de fichiers à l’aide d’un caractère générique. Lorsque vous utilisez un caractère générique, il n’existe aucun moyen d’exclure un sous-ensemble spécifique des fichiers inclus. Supposons, par exemple, que vous souhaitiez tous les fichiers texte d’un dossier, à l’exception d’un dossier spécifique.

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

Ou utiliser un caractère générique pour exclure un ensemble de fichiers tels que tous les fichiers de sauvegarde

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Suppression de packages à l’aide de la boîte de dialogue invite à supprimer les dépendances
Lors de la désinstallation d’un package avec des dépendances, NuGet vous invite à supprimer les dépendances d’un package ainsi que le package.

![Suppression de packages dépendants](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` amélioration des commandes
La `Get-Package` commande prend maintenant en charge un `-ProjectName` paramètre. La commande

```
Get-Package –ProjectName A
```

répertorie tous les packages installés dans le projet A.

### <a name="support-for-proxies-that-require-authentication"></a>Prise en charge des proxies qui requièrent une authentification
Lorsque vous utilisez NuGet derrière un proxy qui requiert une authentification, NuGet demande des informations d’identification de proxy. La saisie des informations d’identification permet à NuGet de se connecter au référentiel distant.

### <a name="support-for-repositories-that-require-authentication"></a>Prise en charge des dépôts qui requièrent une authentification
NuGet prend désormais en charge la connexion à des [dépôts privés](../hosting-packages/local-feeds.md) qui requièrent une authentification de base ou NTLM.

La prise en charge de l’authentification Digest sera ajoutée dans une version ultérieure.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Améliorations des performances du référentiel nuget.org
Nous avons apporté plusieurs améliorations de performances à la Galerie de nuget.org pour rendre la liste des packages et accélérer la recherche.

### <a name="solution-dialog-project-filtering"></a>Filtrage de projet de la boîte de dialogue de solution
Dans la boîte de dialogue de niveau solution, lorsque vous êtes invité à entrer les projets à installer, nous affichons uniquement les projets qui sont compatibles avec le package sélectionné.

### <a name="package-release-notes"></a>Notes de publication du package
Les packages NuGet incluent désormais la prise en charge des notes de publication. Les notes de publication s’affichent uniquement lors de l’affichage des _mises à jour_ d’un package. il est donc inutile de les ajouter à votre première version.

![Notes de publication dans l’onglet mises à jour](./media/manage-nuget-packages-release-notes.png)

Pour ajouter des notes de publication à un package, utilisez le nouvel `<releaseNotes />` élément Metadata dans votre fichier NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>. NuSpec &ltfiles/ &gt; amélioration
Le `.nuspec` fichier autorise désormais `<files />` un élément vide, ce qui indique à nuget.exe de ne pas inclure de fichier dans le package.

## <a name="bug-fixes"></a>Résolutions de bogues
NuGet 1,5 avait un total de 107 éléments de travail corrigés. 103 de ceux-ci ont été marqués comme des bogues.

Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 1,5, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Les correctifs de bogues méritent d’être notés :

* [Problème 1273](http://nuget.codeplex.com/workitem/1273): rendre `packages.config` plus convivial le contrôle de version en triant les packages par ordre alphabétique et en supprimant les espaces superflus.
* [Problème 844](http://nuget.codeplex.com/workitem/844): les numéros de version sont désormais normalisés afin que `Install-Package 1.0` fonctionne sur un package avec la version `1.0.0` .
* [Problème 1060](http://nuget.codeplex.com/workitem/1060): lors de la création d’un package à l’aide d' nuget.exe, l' `-Version` indicateur remplace l' `<version />` élément.
