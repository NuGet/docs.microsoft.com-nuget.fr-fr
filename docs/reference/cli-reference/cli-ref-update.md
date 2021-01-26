---
title: Commande de mise à jour de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: cfa7fdcc6af46fd5f4030ba424754291f697bc43
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779134"
---
# <a name="update-command-nuget-cli"></a>Update, commande (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge par** la consommation des packages : toutes

Mettez à jour tous les packages dans un projet (en utilisant `packages.config`) avec leurs dernières versions disponibles. Il est recommandé d’exécuter [« Restore »](cli-ref-restore.md) avant d’exécuter le `update` . (Pour mettre à jour un package individuel, utilisez [`nuget install`](cli-ref-install.md) sans spécifier de numéro de version, auquel cas NuGet installe la version la plus récente.)

Remarque : `update` ne fonctionne pas avec l’interface CLI s’exécutant sous mono (Mac OSX ou Linux) ou lors de l’utilisation du format PackageReference.

La `update` commande met également à jour les références d’assembly dans le fichier projet, à condition que ces références existent déjà. Si un package mis à jour a un assembly ajouté, une nouvelle référence n’est *pas* ajoutée. Les références d’assembly des nouvelles dépendances de package ne sont pas non plus ajoutées. Pour inclure ces opérations dans le cadre d’une mise à jour, mettez à jour le package dans Visual Studio à l’aide de l’interface utilisateur du gestionnaire de package ou de la console du gestionnaire de package.

Cette commande peut également être utilisée pour mettre à jour nuget.exe elle-même à l’aide de l’indicateur *-Self* .

## <a name="usage"></a>Utilisation

```cli
nuget update <configPath> [options]
```

où `<configPath>` identifie un `packages.config` fichier solution ou qui répertorie les dépendances du projet.

## <a name="options"></a>Options

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  Spécifie la version des packages de dépendance à utiliser, qui peut être l’une des suivantes :<br/><ul><li>La *plus basse* (par défaut) : la version la plus basse</li><li>*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</li><li>*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</li><li>La *plus élevée*: la version la plus élevée</li><li>*Ignorer*: aucun package de dépendances ne sera utilisé</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Spécifie l’action par défaut lorsqu’un fichier d’un package existe déjà dans le projet cible. Affectez la valeur `Overwrite` pour toujours remplacer les fichiers. Affectez la valeur `Ignore` pour ignorer les fichiers.

  L' `PromptUser` action, la valeur par défaut, demande à chaque fichier en conflit `OverwriteAll` , sauf si ou `IgnoreAll` est fourni, qui s’applique à tous les fichiers restants.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-Id`**

  Spécifie une liste d’ID de package à mettre à jour.

- **`-MSBuildPath`**

  *(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande, prioritaire sur `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande. Les valeurs prises en charge sont 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Par défaut, MSBuild dans votre chemin d’accès est choisi, sinon il s’agit par défaut de la version installée la plus récente de MSBuild.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-PreRelease`**

  Autorise la mise à jour vers les versions préliminaires. Cet indicateur n’est pas nécessaire lors de la mise à jour des packages de version préliminaire déjà installés.

- **`-RepositoryPath`**

  Spécifie le dossier local dans lequel les packages sont installés.

- **`-Safe`**

  Spécifie que seules les mises à jour dont la version la plus récente est disponible dans la même version principale et la version mineure que le package installé seront installées.

- **`-Self`**

  Met à jour nuget.exe vers la dernière version ; tous les autres arguments sont ignorés.

- **`-Source`**

  Spécifie la liste des sources de packages (sous forme d’URL) à utiliser pour les mises à jour. En cas d’omission, la commande utilise les sources fournies dans les fichiers de configuration, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

- **`-Version`**

  Lorsqu’il est utilisé avec un ID de package, spécifie la version du package à mettre à jour.

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
