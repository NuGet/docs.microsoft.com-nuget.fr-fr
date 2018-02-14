---
title: "Packages NuGet et contrôle de code source | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informations sur le traitement des packages NuGet dans les systèmes de contrôle de code source et de gestion de versions, et sur l’omission de packages avec git et TFVC."
keywords: "Contrôle de code source NuGet, gestion de versions NuGet, NuGet et git, NuGet et TFS, NuGet et TFVC, omission de packages, référentiels de contrôle de code source, référentiels de gestion de versions"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6261625d5d7eaa748f9ad15510b7b2af3c814e44
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Omission de packages NuGet dans les systèmes de contrôle de code source

En règle générale, les développeurs omettent les packages NuGet de leurs référentiels de contrôle de code source et se servent de la [restauration de package](../consume-packages/package-restore.md) pour réinstaller les dépendances d’un projet avant la génération.

Les raisons pour lesquelles ils se servent de la restauration de package sont les suivantes :

1. Les systèmes de gestion de versions distribués, tels que Git, incluent des copies complètes de chacune des versions des fichiers du référentiel. Les fichiers binaires qui sont fréquemment mis à jour entraînent un encombrement important et ralentissent considérablement le clonage du référentiel.
1. Lorsque des packages sont inclus dans le référentiel, il peut arriver que les développeurs ajoutent des références directement au contenu de package présent sur le disque, plutôt que de référencer les packages via NuGet, ce qui peut avoir pour résultat des noms de chemins codés en dur dans le projet.
1. Il est alors plus difficile de nettoyer votre solution de tous les dossiers de package inutilisés, car vous devez faire attention à ne pas supprimer les dossiers de package qui sont en cours d’utilisation.
1. L’omission de packages vous permet de définir des limites de propriété claires entre votre code et les packages des autres développeurs dont dépend votre code. De nombreux packages NuGet sont déjà gérés dans leur propre référentiel de contrôle de code source.

Même si la restauration de packages constitue le comportement par défaut de NuGet, certaines opérations manuelles sont nécessaires pour omettre les packages (c’est-à-dire le dossier `packages` de votre projet) du contrôle de code source, comme le décrivent les sections suivantes.

## <a name="omitting-packages-with-git"></a>Omission de packages avec Git

Utilisez le [fichier .gitignore](https://git-scm.com/docs/gitignore) pour ne pas inclure le dossier `packages` dans le contrôle de code source. Pour référence, consultez [l’exemple `.gitignore` pour projets Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Les parties importantes du fichier `.gitignore` sont les suivantes :

```gitignore
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
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

1. Dans TFS 2012 ou ultérieur, ou avec Visual Studio Team Services, créez un fichier `.tfignore`, comme décrit dans [Ajouter des fichiers sur le serveur](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore). Dans ce fichier, ajoutez le contenu ci-dessous pour ignorer explicitement les modifications apportées au dossier `\packages` au niveau du référentiel, ainsi qu’à quelques autres fichiers intermédiaires. Vous pouvez créer le fichier dans l’Explorateur Windows en utilisant le nom `.tfignore.` avec le point de fin. Toutefois, vous devrez peut-être désactiver l’option « Cacher les extensions de fichiers » avant de procéder :

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Ajoutez `NuGet.Config` et `.tfignore` pour réaliser le contrôle de code source et l’archivage de vos modifications.
