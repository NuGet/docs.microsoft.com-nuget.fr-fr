---
title: Commande d’installation de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Référence de la commande d’installation de nuget.exe
keywords: NuGet installer référence, la commande de package d’installation
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 121d7b50767f1d466d6d0d8494f324b02d8ff6f1
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="install-command-nuget-cli"></a>installation de commande (CLI NuGet)

**S’applique à :** package consommation &bullet; **versions prises en charge :** toutes les

Télécharge et installe un package dans un projet, par défaut dans le dossier actif, l’utilisation de sources de package spécifié.

> [!Tip]
> Pour télécharger un package directement à l’extérieur du contexte d’un projet, visitez la page de du package sur [nuget.org](https://www.nuget.org) et sélectionnez le **télécharger** lien.

Si aucune source n’est spécifiées, ceux répertoriés dans le fichier de configuration globale, `%appdata%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Linux/Mac), sont utilisés. Consultez [NuGet de configuration de comportement](../consume-packages/configuring-nuget-behavior.md) pour plus d’informations.

Si aucun des packages spécifiques ne sont spécifiés, `install` installe tous les packages répertoriés dans le fichier `packages.config` fichier semblable à [ `restore` ](cli-ref-restore.md).

Le `install` commande ne modifie pas un fichier projet ou `packages.config`; de cette façon, il est similaire à `restore` dans la mesure où il uniquement ajoute des packages sur le disque, mais ne modifie pas les dépendances d’un projet.

Pour ajouter une dépendance, ajoutez un projet via l’interface utilisateur du Gestionnaire de Package ou de la Console dans Visual Studio, ou modifier `packages.config` , puis exécutez soit `install` ou `restore`.

## <a name="usage"></a>Utilisation

```cli
nuget install <packageID | configFilePath> [options]
```

où `<packageID>` le package à installer (à l’aide de la version la plus récente), les noms ou `<configFilePath>` identifie les `packages.config` fichier qui répertorie les packages à installer. Vous pouvez indiquer une version spécifique avec la `-Version` option.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| DependencyVersion | *(4.4 +)*  Spécifie une version spécifique, la substitution du comportement de résolution de dépendance par défaut. |
| DisableParallelProcessing | Désactive l’installation de plusieurs packages en parallèle. |
| ExcludeVersion | Installe le package dans un dossier nommé avec uniquement le nom du package et pas le numéro de version. |
| FallbackSource | *(3.2 +)*  Une liste des sources de package à utiliser comme secours au cas où le package n’est pas trouvé dans le serveur principal ou source par défaut. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Framework | *(4.4 +)*  Framework cible utilisé pour la sélection des dépendances. Par défaut, 'Any' Si non spécifié. |
| Help | Affiche l’aide de la commande. |
| NoCache | NuGet empêche l’utilisation de packages de mise en cache. Consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| OutputDirectory | Spécifie le dossier dans lequel les packages sont installés. Si aucun dossier n’est spécifié, le dossier actif est utilisé. |
| PackageSaveMode | Spécifie les types de fichiers à enregistrer après l’installation du package : un des `nuspec`, `nupkg`, ou `nuspec;nupkg`. |
| Version préliminaire | Permet de versions préliminaires des packages à installer. Cet indicateur n’est pas requis lors de la restauration des packages avec `packages.config`. |
| RequireConsent | Vérifie que la restauration des packages est activé avant de télécharger et installer les packages. Pour plus d’informations, consultez [restauration des packages](../consume-packages/package-restore.md). |
| SolutionDirectory | Spécifie le dossier racine de la solution pour lequel restaurer les packages. |
| Source | Spécifie la liste des sources de package (en tant qu’URL) pour utiliser. Si omis, la commande utilise les sources fournies dans les fichiers de configuration, consultez [NuGet de configuration de comportement](../consume-packages/configuring-nuget-behavior.md). |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |
| Version | Spécifie la version du package à installer. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
