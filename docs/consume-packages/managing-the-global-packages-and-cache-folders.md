---
title: Gérer les dossiers de packages globaux, les dossiers de cache et les dossiers temporaires dans NuGet
description: Guide pratique pour gérer le dossier d’installation des packages globaux, le cache de package et les dossiers temporaires présents sur un ordinateur et utilisés lors de l’installation, la restauration et la mise à jour de packages.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e5585267d4ce2563d77ff30ec5c31e196d98686a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774798"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="cfeec-103">Gérer les dossiers de packages globaux, les dossiers de cache et les dossiers temporaires</span><span class="sxs-lookup"><span data-stu-id="cfeec-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="cfeec-104">Chaque fois que vous installez, mettez à jour ou restaurez un package, NuGet gère les packages et les informations associées dans plusieurs dossiers extérieurs à la structure de votre projet :</span><span class="sxs-lookup"><span data-stu-id="cfeec-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="cfeec-105">Nom</span><span class="sxs-lookup"><span data-stu-id="cfeec-105">Name</span></span> | <span data-ttu-id="cfeec-106">Description et emplacement (par utilisateur)</span><span class="sxs-lookup"><span data-stu-id="cfeec-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="cfeec-107">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="cfeec-107">global&#8209;packages</span></span> | <span data-ttu-id="cfeec-108">C’est dans le dossier *global-packages* que NuGet installe les packages téléchargés.</span><span class="sxs-lookup"><span data-stu-id="cfeec-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="cfeec-109">Chaque package est entièrement développé dans un sous-dossier qui correspond à son identificateur et à son numéro de version.</span><span class="sxs-lookup"><span data-stu-id="cfeec-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="cfeec-110">Les projets qui utilisent le format [PackageReference](package-references-in-project-files.md) utilisent toujours des packages directement à partir de ce dossier.</span><span class="sxs-lookup"><span data-stu-id="cfeec-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="cfeec-111">Lorsque [packages.config](../reference/packages-config.md) est utilisé, les packages sont installés dans le dossier *global-packages*, puis copiés dans le dossier `packages` du projet.</span><span class="sxs-lookup"><span data-stu-id="cfeec-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="cfeec-112">Windows : `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="cfeec-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="cfeec-113">Mac/Linux : `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="cfeec-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="cfeec-114">Écrasez avec la variable d’environnement NUGET_PACKAGES, les  [paramètres de configuration](../reference/nuget-config-file.md#config-section)`globalPackagesFolder` ou `repositoryPath` (respectivement pour PackageReference et `packages.config`) ou la propriété MSBuild `RestorePackagesPath` (MSBuild uniquement).</span><span class="sxs-lookup"><span data-stu-id="cfeec-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="cfeec-115">La variable d’environnement a la priorité sur le paramètre de configuration.</span><span class="sxs-lookup"><span data-stu-id="cfeec-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="cfeec-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="cfeec-116">http&#8209;cache</span></span> | <span data-ttu-id="cfeec-117">Le Gestionnaire de Package de Visual Studio (NuGet 3.x+) et l’outil `dotnet` stockent une copie des packages téléchargés dans ce cache (sous la forme de fichiers `.dat`), dans un sous-dossier par source de package.</span><span class="sxs-lookup"><span data-stu-id="cfeec-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="cfeec-118">Les packages ne sont pas développés, et le cache a un délai d’expiration de 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="cfeec-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="cfeec-119">Windows : `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="cfeec-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="cfeec-120">Mac/Linux : `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="cfeec-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="cfeec-121">Écrasez avec la variable d’environnement NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="cfeec-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="cfeec-122">temp</span><span class="sxs-lookup"><span data-stu-id="cfeec-122">temp</span></span> | <span data-ttu-id="cfeec-123">Il s’agit du dossier dans lequel NuGet stocke les fichiers temporaires pendant ses différentes opérations.</span><span class="sxs-lookup"><span data-stu-id="cfeec-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="cfeec-124">Windows : `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="cfeec-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="cfeec-125">Mac/Linux : `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="cfeec-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="cfeec-126">plugins-cache **4.8+**</span><span class="sxs-lookup"><span data-stu-id="cfeec-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="cfeec-127">Il s’agit du dossier dans lequel NuGet stocke les résultats de la demande de revendications de l’opération.</span><span class="sxs-lookup"><span data-stu-id="cfeec-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="cfeec-128">Windows : `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="cfeec-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="cfeec-129">Mac/Linux : `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="cfeec-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="cfeec-130">Remplacez par la variable d’environnement NUGET_PLUGINS_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="cfeec-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="cfeec-131">NuGet 3.5 et les versions antérieures utilisent *packages-cache* au lieu de *http-cache*, qui se trouve dans `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="cfeec-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="cfeec-132">Les dossiers *global-packages* et cache dispensent en général NuGet de télécharger des packages déjà présents sur l’ordinateur, ce qui améliore les performances d’installation, de mise à jour et de restauration.</span><span class="sxs-lookup"><span data-stu-id="cfeec-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="cfeec-133">Avec PackageReference, le dossier *global-packages* évite également de conserver les packages téléchargés à l’intérieur des dossiers du projet, où ils pourraient être ajoutés par inadvertance au contrôle de code source, et réduit l’impact global de NuGet sur le stockage de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cfeec-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="cfeec-134">Pour récupérer un package, NuGet commence par regarder dans le dossier *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="cfeec-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="cfeec-135">Si la version exacte du package n’y figure pas, il vérifie toutes les sources de packages non HTTP.</span><span class="sxs-lookup"><span data-stu-id="cfeec-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="cfeec-136">S’il ne trouve toujours pas le package, il le recherche dans *http-cache*, sauf si vous spécifiez `--no-cache` avec des commandes `dotnet.exe` ou `-NoCache` avec des commandes `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="cfeec-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="cfeec-137">Si le package ne se trouve pas dans le cache ou que le cache n’est pas utilisé, NuGet le récupère sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="cfeec-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="cfeec-138">Pour plus d’informations, consultez [Processus d’installation d’un package](../concepts/package-installation-process.md).</span><span class="sxs-lookup"><span data-stu-id="cfeec-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="cfeec-139">Afficher l’emplacement des dossiers</span><span class="sxs-lookup"><span data-stu-id="cfeec-139">Viewing folder locations</span></span>

<span data-ttu-id="cfeec-140">Vous pouvez voir les emplacements avec la [commande nuget locals](../reference/cli-reference/cli-ref-locals.md) :</span><span class="sxs-lookup"><span data-stu-id="cfeec-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="cfeec-141">Sortie classique (Windows ; « user1 » est le nom d’utilisateur actuel) :</span><span class="sxs-lookup"><span data-stu-id="cfeec-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="cfeec-142">(`package-cache` est utilisé dans NuGet 2.x et apparaît avec NuGet 3.5 et les versions antérieures.)</span><span class="sxs-lookup"><span data-stu-id="cfeec-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="cfeec-143">Vous pouvez aussi voir l’emplacement des dossiers avec la [commande dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) :</span><span class="sxs-lookup"><span data-stu-id="cfeec-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```dotnetcli
dotnet nuget locals all --list
```

<span data-ttu-id="cfeec-144">Sortie classique (Mac/Linux ; « user1 » est le nom d’utilisateur actuel) :</span><span class="sxs-lookup"><span data-stu-id="cfeec-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="cfeec-145">Pour afficher l’emplacement d’un seul dossier, utilisez `http-cache`, `global-packages`, `temp` ou `plugins-cache` au lieu de `all`.</span><span class="sxs-lookup"><span data-stu-id="cfeec-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="cfeec-146">Effacer les dossiers locaux</span><span class="sxs-lookup"><span data-stu-id="cfeec-146">Clearing local folders</span></span>

<span data-ttu-id="cfeec-147">Si vous rencontrez des problèmes d’installation de package ou que vous voulez vous assurer de l’installer à partir d’une galerie à distance, utilisez l’option `locals --clear` (dotnet.exe) ou `locals -clear` (nuget.exe), en spécifiant le dossier à effacer, ou `all` pour tous les effacer :</span><span class="sxs-lookup"><span data-stu-id="cfeec-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="cfeec-148">Les packages utilisés par des projets actuellement ouverts dans Visual Studio ne sont pas effacés du dossier *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="cfeec-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="cfeec-149">À compter de Visual Studio 2017, utilisez la commande de menu **Outils > Gestionnaire de package NuGet > Paramètres du Gestionnaire de package**, puis sélectionnez **Effacer tous les caches NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cfeec-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="cfeec-150">À l’heure actuelle, la gestion du cache n’est pas disponible avec la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="cfeec-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="cfeec-151">Dans Visual Studio 2015, utilisez plutôt les commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="cfeec-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Commande d’option NuGet pour effacer les caches](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="cfeec-153">Dépannage des erreurs</span><span class="sxs-lookup"><span data-stu-id="cfeec-153">Troubleshooting errors</span></span>

<span data-ttu-id="cfeec-154">Les erreurs suivantes risquent de se produire avec `nuget locals` ou `dotnet nuget locals` :</span><span class="sxs-lookup"><span data-stu-id="cfeec-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="cfeec-155">*Erreur : Le processus ne peut pas accéder au fichier <package>, car il est utilisé par un autre processus* ou *Échec de l’effacement des ressources locales : Suppression d’un ou plusieurs fichiers impossible*</span><span class="sxs-lookup"><span data-stu-id="cfeec-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="cfeec-156">Un ou plusieurs fichiers du dossier sont en cours d’utilisation par un autre processus ; par exemple, un projet Visual Studio faisant référence à des packages du dossier *global-packages* est ouvert.</span><span class="sxs-lookup"><span data-stu-id="cfeec-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="cfeec-157">Fermez ces processus, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="cfeec-157">Close those processes and try again.</span></span>

- <span data-ttu-id="cfeec-158">*Erreur : Accès au chemin <path> refusé* ou *Le répertoire n’est pas vide*</span><span class="sxs-lookup"><span data-stu-id="cfeec-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="cfeec-159">Vous n’avez pas l’autorisation de supprimer des fichiers du cache.</span><span class="sxs-lookup"><span data-stu-id="cfeec-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="cfeec-160">Modifiez les autorisations du dossier, si possible, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="cfeec-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="cfeec-161">Sinon, contactez votre administrateur système.</span><span class="sxs-lookup"><span data-stu-id="cfeec-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="cfeec-162">*Erreur : le chemin d’accès spécifié, le nom de fichier ou les deux sont trop longs. Le nom de fichier complet doit être inférieur à 260 caractères, et le nom du répertoire doit contenir moins de 248 caractères.*</span><span class="sxs-lookup"><span data-stu-id="cfeec-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="cfeec-163">Raccourcissez le nom des dossiers, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="cfeec-163">Shorten the folder names and try again.</span></span>
