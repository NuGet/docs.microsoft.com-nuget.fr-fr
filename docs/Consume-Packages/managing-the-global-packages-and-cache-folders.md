---
title: Gérer les dossiers de packages globaux, les dossiers de cache et les dossiers temporaires dans NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Guide pratique pour gérer le dossier d’installation des packages globaux, le cache de package et les dossiers temporaires présents sur un ordinateur et utilisés lors de l’installation, la restauration et la mise à jour de packages.
keywords: Dossier de packages globaux NuGet, cache de package NuGet, mise en cache de package, dossier d’installation de package, caches NuGet, gérer les caches, cache NuGet local, cache NuGet global, commande nuget locals, effacer le cache
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e9f4383a3f1700b96e3d6fe9ea4c0a7c24daa45a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Gérer les dossiers de packages globaux, les dossiers de cache et les dossiers temporaires

Chaque fois que vous installez, mettez à jour ou restaurez un package, NuGet gère les packages et les informations associées dans plusieurs dossiers extérieurs à la structure de votre projet :

| Name | Description et emplacement (par utilisateur)|
| --- | --- |
| global&#8209;packages | C’est dans le dossier *global-packages* que NuGet installe les packages téléchargés. Chaque package est entièrement développé dans un sous-dossier qui correspond à son identificateur et à son numéro de version. Les projets au format PackageReference utilisent toujours les packages directement dans ce dossier. Si `packages.config` est utilisé, les packages sont installés dans le dossier *global-packages*, puis copiés dans le dossier `packages` du projet.<br/><ul><li>Windows : `%userprofile%\.nuget\packages`</li><li>Mac/Linux : `~/.nuget/packages`</li><li>Écrasez avec la variable d’environnement NUGET_PACKAGES, les [paramètres de configuration](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` ou `repositoryPath` (respectivement pour PackageReference et `packages.config`) ou la propriété MSBuild `RestorePackagesPath` (MSBuild uniquement). La variable d’environnement a la priorité sur le paramètre de configuration.</li></ul> |
| http&#8209;cache | Le Gestionnaire de Package de Visual Studio (NuGet 3.x+) et l’outil `dotnet` stockent une copie des packages téléchargés dans ce cache (sous la forme de fichiers `.dat`), dans un sous-dossier par source de package. Les packages ne sont pas développés, et le cache a un délai d’expiration de 30 minutes.<br/><ul><li>Windows : `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux : `~/.local/share/NuGet/v3-cache`</li><li>Écrasez avec la variable d’environnement NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Il s’agit du dossier dans lequel NuGet stocke les fichiers temporaires pendant ses différentes opérations.<br/><li>Windows : `%temp%\NuGetScratch`</li><li>Mac/Linux : `/tmp/NuGetScratch`</li></ul> |

> [!Note]
> NuGet 3.5 et les versions antérieures utilisent *packages-cache* au lieu de *http-cache*, qui se trouve dans `%localappdata%\NuGet\Cache`.

Les dossiers *global-packages* et cache dispensent en général NuGet de télécharger des packages déjà présents sur l’ordinateur, ce qui améliore les performances d’installation, de mise à jour et de restauration. Avec PackageReference, le dossier *global-packages* évite également de conserver les packages téléchargés à l’intérieur des dossiers du projet, où ils pourraient être ajoutés par inadvertance au contrôle de code source, et réduit l’impact global de NuGet sur le stockage de l’ordinateur.

Pour récupérer un package, NuGet commence par regarder dans le dossier *global-packages*. Si la version exacte du package n’y figure pas, il vérifie toutes les sources de packages non HTTP. S’il ne trouve toujours pas le package, il le recherche dans *http-cache*, sauf si vous spécifiez `--no-cache` avec des commandes `dotnet.exe` ou `-NoCache` avec des commandes `nuget.exe`. Si le package ne se trouve pas dans le cache ou que le cache n’est pas utilisé, NuGet le récupère sur HTTP.

Pour plus d’informations, consultez la section [Processus d’installation d’un package](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).

## <a name="viewing-folder-locations"></a>Afficher l’emplacement des dossiers

Vous pouvez afficher l’emplacement des dossiers avec la [commande dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) :

```cli
dotnet nuget locals all --list
```

Sortie classique (Mac/Linux ; « user1 » est le nom d’utilisateur actuel) :

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

Pour afficher l’emplacement d’un seul dossier, utilisez `http-cache`, `global-packages` ou `temp` au lieu de `all`. 

Vous affichez également afficher les emplacements avec la [commande nuget locals](../tools/cli-ref-locals.md) :

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

Sortie classique (Windows ; « user1 » est le nom d’utilisateur actuel) :

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

(`package-cache` est utilisé dans NuGet 2.x et apparaît avec NuGet 3.5 et les versions antérieures.)

## <a name="clearing-local-folders"></a>Effacer les dossiers locaux

Si vous rencontrez des problèmes d’installation de package ou que vous voulez vous assurer de l’installer à partir d’une galerie à distance, utilisez l’option `locals --clear` (dotnet.exe) ou `locals -clear` (nuget.exe), en spécifiant le dossier à effacer, ou `all` pour tous les effacer :

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

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Les packages utilisés par des projets actuellement ouverts dans Visual Studio ne sont pas effacés du dossier *global-packages*.

Dans Visual Studio, utilisez la commande de menu **Outils > Gestionnaire de package NuGet > Paramètres du Gestionnaire de package**, puis sélectionnez **Effacer tous les caches NuGet**. À l’heure actuelle, la gestion du cache n’est pas disponible avec la console du Gestionnaire de package.

![Commande d’option NuGet pour effacer les caches](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Résoudre les erreurs

Les erreurs suivantes risquent de se produire avec `nuget locals` ou `dotnet nuget locals` :

- *Erreur : Le processus ne peut pas accéder au fichier <package>, car il est utilisé par un autre processus* ou *Échec de l’effacement des ressources locales : Suppression d’un ou plusieurs fichiers impossible*

    Un ou plusieurs fichiers du dossier sont en cours d’utilisation par un autre processus ; par exemple, un projet Visual Studio faisant référence à des packages du dossier *global-packages* est ouvert. Fermez ces processus, puis réessayez.

- *Erreur : Accès au chemin <path> refusé* ou *Le répertoire n’est pas vide*

    Vous n’avez pas l’autorisation de supprimer des fichiers du cache. Modifiez les autorisations du dossier, si possible, puis réessayez. Sinon, contactez votre administrateur système.

- *Erreur : Le chemin d’accès ou le nom de fichier spécifié est trop long. Le nom complet du fichier doit être inférieur à 260 caractères, et le nom du répertoire à 248 caractères.*

    Raccourcissez le nom des dossiers, puis réessayez.
