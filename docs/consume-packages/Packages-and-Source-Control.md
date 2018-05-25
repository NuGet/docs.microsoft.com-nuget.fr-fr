---
title: Packages NuGet et contrôle de code source
description: Informations sur le traitement des packages NuGet dans les systèmes de contrôle de code source et de gestion de versions, et sur l’omission de packages avec git et TFVC.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: bc2c6d5e9933f2f6103363a2e69fbb9b47f80ecf
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/22/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="7fbc8-103">Omission de packages NuGet dans les systèmes de contrôle de code source</span><span class="sxs-lookup"><span data-stu-id="7fbc8-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="7fbc8-104">En règle générale, les développeurs omettent les packages NuGet de leurs référentiels de contrôle de code source et se servent de la [restauration de package](package-restore.md) pour réinstaller les dépendances d’un projet avant la génération.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="7fbc8-105">Les raisons pour lesquelles ils se servent de la restauration de package sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7fbc8-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="7fbc8-106">Les systèmes de gestion de versions distribués, tels que Git, incluent des copies complètes de chacune des versions des fichiers du référentiel.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="7fbc8-107">Les fichiers binaires qui sont fréquemment mis à jour entraînent un encombrement important et ralentissent considérablement le clonage du référentiel.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="7fbc8-108">Lorsque des packages sont inclus dans le référentiel, il peut arriver que les développeurs ajoutent des références directement au contenu de package présent sur le disque, plutôt que de référencer les packages via NuGet, ce qui peut avoir pour résultat des noms de chemins codés en dur dans le projet.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="7fbc8-109">Il est alors plus difficile de nettoyer votre solution de tous les dossiers de package inutilisés, car vous devez faire attention à ne pas supprimer les dossiers de package qui sont en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="7fbc8-110">L’omission de packages vous permet de définir des limites de propriété claires entre votre code et les packages des autres développeurs dont dépend votre code.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="7fbc8-111">De nombreux packages NuGet sont déjà gérés dans leur propre référentiel de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="7fbc8-112">Même si la restauration de package constitue le comportement par défaut de NuGet, certaines opérations manuelles sont nécessaires pour omettre les packages (&mdash;c’est-à-dire le dossier `packages` de votre projet&mdash;) dans le contrôle de code source, comme l’explique cet article.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="7fbc8-113">Omission de packages avec Git</span><span class="sxs-lookup"><span data-stu-id="7fbc8-113">Omitting packages with Git</span></span>

<span data-ttu-id="7fbc8-114">Utilisez le [fichier .gitignore](https://git-scm.com/docs/gitignore) pour ignorer les packages NuGet (`.nupkg`), le dossier `packages` et `project.assets.json`, entre autres.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="7fbc8-115">À titre de référence, consultez [l’exemple `.gitignore` pour les projets Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore) :</span><span class="sxs-lookup"><span data-stu-id="7fbc8-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="7fbc8-116">Les parties importantes du fichier `.gitignore` sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7fbc8-116">The important parts of the `.gitignore` file are:</span></span>

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

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="7fbc8-117">Omission de packages avec Team Foundation Version Control</span><span class="sxs-lookup"><span data-stu-id="7fbc8-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="7fbc8-118">Si possible, suivez ces instructions *avant* d’ajouter votre projet au contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="7fbc8-119">Sinon, supprimez manuellement le dossier `packages` de votre référentiel, puis archivez ce changement avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="7fbc8-120">Pour désactiver l’intégration du contrôle de code source à TFVC pour les fichiers sélectionnés :</span><span class="sxs-lookup"><span data-stu-id="7fbc8-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="7fbc8-121">Créez un dossier appelé `.nuget` dans le dossier de votre solution (où se trouve le fichier `.sln`).</span><span class="sxs-lookup"><span data-stu-id="7fbc8-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="7fbc8-122">Conseil : sur les systèmes Windows, pour créer ce dossier dans l’Explorateur Windows, utilisez le nom `.nuget.` *avec* le point de fin.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="7fbc8-123">Dans ce dossier, créez un fichier nommé `NuGet.Config` et ouvrez-le pour le modifier.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="7fbc8-124">Ajoutez au minimum le texte suivant, où le paramètre [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) indique à Visual Studio d’ignorer tous les éléments du dossier `packages` :</span><span class="sxs-lookup"><span data-stu-id="7fbc8-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="7fbc8-125">Si vous utilisez TFS 2010 ou version antérieure, masquez le dossier `packages` dans vos mappages d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="7fbc8-126">Dans TFS 2012 ou ultérieur, ou avec Visual Studio Team Services, créez un fichier `.tfignore`, comme décrit dans [Ajouter des fichiers sur le serveur](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span><span class="sxs-lookup"><span data-stu-id="7fbc8-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span></span> <span data-ttu-id="7fbc8-127">Dans ce fichier, ajoutez le contenu ci-dessous pour ignorer explicitement les modifications apportées au dossier `\packages` au niveau du référentiel, ainsi qu’à quelques autres fichiers intermédiaires.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="7fbc8-128">Vous pouvez créer le fichier dans l’Explorateur Windows en utilisant le nom `.tfignore.` avec le point de fin. Toutefois, vous devrez peut-être désactiver l’option « Cacher les extensions de fichiers » avant de procéder :</span><span class="sxs-lookup"><span data-stu-id="7fbc8-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="7fbc8-129">Ajoutez `NuGet.Config` et `.tfignore` pour réaliser le contrôle de code source et l’archivage de vos modifications.</span><span class="sxs-lookup"><span data-stu-id="7fbc8-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
