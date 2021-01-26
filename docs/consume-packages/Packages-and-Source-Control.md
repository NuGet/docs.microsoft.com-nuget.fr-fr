---
title: Packages NuGet et contrôle de code source
description: Informations sur le traitement des packages NuGet dans les systèmes de contrôle de code source et de gestion de versions, et sur l’omission de packages avec git et TFVC.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9bae65573ca49c68d07250228c1923890e0f14ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775008"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Omission de packages NuGet dans les systèmes de contrôle de code source

En règle générale, les développeurs omettent les packages NuGet de leurs référentiels de contrôle de code source et se servent de la [restauration de package](package-restore.md) pour réinstaller les dépendances d’un projet avant la génération.

Les raisons pour lesquelles ils se servent de la restauration de package sont les suivantes :

1. Les systèmes de gestion de versions distribués, tels que Git, incluent des copies complètes de chacune des versions des fichiers du référentiel. Les fichiers binaires qui sont fréquemment mis à jour entraînent un encombrement important et ralentissent considérablement le clonage du référentiel.
1. Lorsque des packages sont inclus dans le référentiel, il peut arriver que les développeurs ajoutent des références directement au contenu de package présent sur le disque, plutôt que de référencer les packages via NuGet, ce qui peut avoir pour résultat des noms de chemins codés en dur dans le projet.
1. Il est alors plus difficile de nettoyer votre solution de tous les dossiers de package inutilisés, car vous devez faire attention à ne pas supprimer les dossiers de package qui sont en cours d’utilisation.
1. L’omission de packages vous permet de définir des limites de propriété claires entre votre code et les packages des autres développeurs dont dépend votre code. De nombreux packages NuGet sont déjà gérés dans leur propre référentiel de contrôle de code source.

Même si la restauration de package constitue le comportement par défaut de NuGet, certaines opérations manuelles sont nécessaires pour omettre les packages (&mdash;c’est-à-dire le dossier `packages` de votre projet&mdash;) dans le contrôle de code source, comme l’explique cet article.

## <a name="omitting-packages-with-git"></a>Omission de packages avec Git

Utilisez le [fichier .gitignore](https://git-scm.com/docs/gitignore) pour ignorer les packages NuGet (`.nupkg`), le dossier `packages` et `project.assets.json`, entre autres. Pour obtenir des informations de référence, consultez l' [exemple `.gitignore` pour les projets Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Les parties importantes du fichier `.gitignore` sont les suivantes :

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Omission de packages avec Team Foundation Version Control

> [!Note]
> Si possible, suivez ces instructions *avant* d’ajouter votre projet au contrôle de code source. Sinon, supprimez manuellement le dossier `packages` de votre référentiel, puis archivez ce changement avant de continuer.

Pour désactiver l’intégration du contrôle de code source à TFVC pour les fichiers sélectionnés :

1. Créez un dossier appelé `.nuget` dans le dossier de votre solution (où se trouve le fichier `.sln`).
    - Conseil : sur les systèmes Windows, pour créer ce dossier dans l’Explorateur Windows, utilisez le nom `.nuget.` *avec* le point de fin.

1. Dans ce dossier, créez un fichier nommé `NuGet.Config` et ouvrez-le pour le modifier.

1. Ajoutez au minimum le texte suivant, où le paramètre [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) indique à Visual Studio d’ignorer tous les éléments du dossier `packages` :

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Si vous utilisez TFS 2010 ou version antérieure, masquez le dossier `packages` dans vos mappages d’espace de travail.

1. Dans TFS 2012 ou ultérieur, ou avec Visual Studio Team Services, créez un fichier `.tfignore`, comme décrit dans [Ajouter des fichiers sur le serveur](/vsts/tfvc/add-files-server?view=vsts#tfignore). Dans ce fichier, ajoutez le contenu ci-dessous pour ignorer explicitement les modifications apportées au dossier `\packages` au niveau du référentiel, ainsi qu’à quelques autres fichiers intermédiaires. Vous pouvez créer le fichier dans l’Explorateur Windows en utilisant le nom `.tfignore.` avec le point de fin. Toutefois, vous devrez peut-être désactiver l’option « Cacher les extensions de fichiers » avant de procéder :

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Ajoutez `NuGet.Config` et `.tfignore` pour réaliser le contrôle de code source et l’archivage de vos modifications.
