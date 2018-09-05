---
title: Commande d’installation NuGet CLI
description: Référence pour la commande d’installation nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8261cdb83af72d9d9379124f4c446c7cd2a50299
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549134"
---
# <a name="install-command-nuget-cli"></a>install (commande, NuGet CLI)

**S’applique à :** la consommation de package &bullet; **versions prises en charge :** toutes les

Télécharge et installe un package dans un projet, par défaut le dossier actuel, à l’aide de sources de package spécifié.

> [!Tip]
> Pour télécharger un package directement à l’extérieur du contexte d’un projet, visitez la page du package sur [nuget.org](https://www.nuget.org) et sélectionnez le **télécharger** lien.

Si aucune source n’est spécifiées, ceux répertoriés dans le fichier de configuration globale, `%appdata%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), sont utilisés. Consultez [du comportement de NuGet configuration](../consume-packages/configuring-nuget-behavior.md) pour plus d’informations.

Si aucun des packages spécifiques ne sont spécifiés, `install` installe tous les packages répertoriés dans le projet `packages.config` fichier, rendant similaire à [ `restore` ](cli-ref-restore.md).

Le `install` commande ne modifie pas un fichier projet ou `packages.config`; de cette façon, elle est similaire à `restore` car il uniquement ajoute des packages sur le disque, mais ne modifie pas les dépendances d’un projet.

Pour ajouter une dépendance, soit ajouter un package via l’interface utilisateur du Gestionnaire de Package ou de la Console dans Visual Studio ou de modifier `packages.config` , puis exécutez soit `install` ou `restore`.

## <a name="usage"></a>Utilisation

```cli
nuget install <packageID | configFilePath> [options]
```

où `<packageID>` désigne le package à installer (à l’aide de la dernière version), ou `<configFilePath>` identifie le `packages.config` fichier qui répertorie les packages à installer. Vous pouvez indiquer une version spécifique avec la `-Version` option.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| DependencyVersion | *(4.4 +)*  La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :<br/><ul><li>*La plus basse* (valeur par défaut) : la version la plus basse</li><li>*HighestPatch*: la version du correctif plus bas majeure, mineure la plus basse, le plus élevé</li><li>*HighestMinor*: la version avec le plus bas principales, des correctifs mineurs, la plus élevée le plus élevé</li><li>*La plus élevée*: la version la plus récente</li></ul> |
| DisableParallelProcessing | Désactive l’installation de plusieurs packages en parallèle. |
| ExcludeVersion | Installe le package dans un dossier nommé avec uniquement le nom du package et pas le numéro de version. |
| FallbackSource | *(3.2 +)*  Une liste des sources de package à utiliser comme solutions de secours dans le cas où le package n’est pas trouvé dans le réplica principal ou source par défaut. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Framework | *(4.4 +)*  Framework cible utilisé pour sélectionner les dépendances. Valeur par défaut est 'Any' Si non spécifié. |
| Help | Affiche l’aide de la commande. |
| NoCache | Empêche NuGet d’utiliser les packages mis en cache. Consultez [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| OutputDirectory | Spécifie le dossier dans lequel les packages sont installés. Si aucun dossier n’est spécifié, le dossier actif est utilisé. |
| PackageSaveMode | Spécifie les types de fichiers à enregistrer après l’installation de package : un des `nuspec`, `nupkg`, ou `nuspec;nupkg`. |
| Version préliminaire | Permet à installer des packages de version préliminaire. Cet indicateur n’est pas requis lors de la restauration des packages avec `packages.config`. |
| RequireConsent | Vérifie que la restauration des packages est activé avant de télécharger et installer les packages. Pour plus d’informations, consultez [la restauration des packages](../consume-packages/package-restore.md). |
| SolutionDirectory | Spécifie le dossier racine de la solution pour lequel restaurer les packages. |
| Source | Spécifie la liste des sources de package (en tant qu’URL) pour utiliser. Si omis, la commande utilise les sources fournies dans les fichiers de configuration, consultez [du comportement de NuGet configuration](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |
| Version | Spécifie la version du package à installer. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
