---
title: Commande d’installation de l’interface CLI NuGet
description: Référence pour la commande nuget.exe install
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779264"
---
# <a name="install-command-nuget-cli"></a>commande Install (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge par** la consommation des packages : toutes

Télécharge et installe un package dans un projet, en utilisant par défaut le dossier actif, à l’aide des sources de package spécifiées.

> [!Tip]
> Pour télécharger un package directement en dehors du contexte d’un projet, accédez à la page du package sur [NuGet.org](https://www.nuget.org) et sélectionnez le lien de **Téléchargement** .

Si aucune source n’est spécifiée, celles répertoriées dans le fichier de configuration global `%appdata%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) sont utilisées. Pour plus d’informations, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md) .

Si aucun package spécifique n’est spécifié, `install` installe tous les packages répertoriés dans le fichier du projet `packages.config` , en le rendant similaire à [`restore`](cli-ref-restore.md) .

La `install` commande ne modifie pas un fichier projet ou `packages.config` . de cette façon, elle est semblable à dans le sens `restore` où elle ajoute uniquement des packages sur le disque, mais ne modifie pas les dépendances d’un projet.

Pour ajouter une dépendance, ajoutez un package par le biais de l’interface utilisateur ou de la console du gestionnaire de package dans Visual Studio, ou modifiez, `packages.config` puis exécutez `install` ou `restore` .

## <a name="usage"></a>Utilisation

```cli
nuget install <packageID | configFilePath> [options]
```

où `<packageID>` nomme le package à installer (à l’aide de la version la plus récente) ou `<configFilePath>` identifie le `packages.config` fichier qui répertorie les packages à installer. Vous pouvez indiquer une version spécifique avec l' `-Version` option.

## <a name="options"></a>Options

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-DependencyVersion`**

  *(4.4 +)* Version des packages de dépendance à utiliser, qui peut être l’une des suivantes :<br/><ul><li>La *plus basse* (par défaut) : la version la plus basse</li><li>*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</li><li>*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</li><li>La *plus élevée*: la version la plus élevée</li><li>*Ignorer*: aucun package de dépendances ne sera utilisé</li></ul>

- **`-DirectDownload`**

  Téléchargez directement sans remplir de caches avec des métadonnées ou des binaires.

- **`-DisableParallelProcessing`**

  Désactive l’installation de plusieurs packages en parallèle.

- **`-x|-ExcludeVersion`**

  Installe le package dans un dossier nommé avec uniquement le nom du package et non le numéro de version.

- **`-FallbackSource`**

  *(3.2 +)* Liste de sources de packages à utiliser comme secours si le package est introuvable dans la source principale ou par défaut.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-Framework`**

  *(4.4 +)* Framework cible utilisé pour la sélection des dépendances. La valeur par défaut est « any » s’il n’est pas spécifié.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-NoCache`**

  Empêche NuGet d’utiliser les packages mis en cache. Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-OutputDirectory`**

  Spécifie le dossier dans lequel les packages sont installés. Si aucun dossier n’est spécifié, le dossier actif est utilisé.

- **`-PackageSaveMode`**

  Spécifie les types de fichiers à enregistrer après l’installation du package : l’un des éléments `nuspec` , `nupkg` ou `nuspec;nupkg` .

- **`-PreRelease`**

  Autorise l’installation des packages de version préliminaire. Cet indicateur n’est pas requis lors de la restauration de packages avec `packages.config` .

- **`-RequireConsent`**

  Vérifie que la restauration des packages est activée avant de télécharger et d’installer les packages. Pour plus d’informations, consultez [restauration de packages](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Spécifie le dossier racine de la solution pour laquelle restaurer les packages.

- **`-Source`**

   Spécifie la liste des sources de packages (sous forme d’URL) à utiliser. En cas d’omission, la commande utilise les sources fournies dans les fichiers de configuration, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

- **`-Version`**

  Spécifie la version du package à installer.

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
