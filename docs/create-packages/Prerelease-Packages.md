---
title: Préversions dans les packages NuGet
description: Instructions pour la génération de packages en préversion
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: ae6628efa6d97ff5ba2c4c359b9565a3214cb346
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774662"
---
# <a name="building-pre-release-packages"></a>Génération de packages en préversion

Chaque fois que vous publiez un package mis à jour avec un nouveau numéro de version, NuGet le considère comme la « dernière version stable », comme indiqué par exemple dans l’interface utilisateur du gestionnaire de package dans Visual Studio :

![Interface utilisateur du gestionnaire de package montrant la dernière version stable](media/Prerelease_01-LatestStable.png)

Une version stable est une version considérée comme suffisamment fiable pour être utilisée en production. La dernière version stable est également celle qui est installée sous forme de mise à jour de package ou pendant une restauration de package (conformément aux contraintes décrites dans [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md)).

Pour prendre en charge le cycle de vie de publication du logiciel, NuGet 1.6 et ultérieur permet de distribuer des packages en préversion, où le numéro de version inclut un suffixe de gestion des versions sémantique comme `-alpha`, `-beta` ou `-rc`. Pour plus d’informations, consultez [Gestion des versions de package](../concepts/package-versioning.md#pre-release-versions).

Vous pouvez spécifier ces versions en utilisant l’une des manières suivantes :

- **Si votre projet utilise [`PackageReference`](../consume-packages/package-references-in-project-files.md)**  : incluez le suffixe de version sémantique dans l’élément [`PackageVersion`](/dotnet/core/tools/csproj#packageversion) du fichier `.csproj` :

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Si votre projet utilise un fichier [`packages.config`](../reference/packages-config.md)**  : incluez le suffixe de version sémantique dans l’élément [`version`](../reference/nuspec.md#version) du fichier [`.nuspec`](../reference/nuspec.md) :

    ```xml
    <version>1.0.1-alpha</version>
    ```

Lorsque vous êtes prêt à publier une version stable, supprimez simplement le suffixe et le package est prioritaire sur toutes les préversions. Là encore, consultez [Gestion des versions de package](../concepts/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Installation et mise à jour des packages en préversion

Par défaut, NuGet n’inclut pas de préversions dans le cadre de l’utilisation de packages, mais vous pouvez modifier ce comportement comme suit :

- **Interface utilisateur du gestionnaire de package dans Visual Studio** : dans l’interface utilisateur **Gérer les packages NuGet**, cochez la case **Inclure la préversion** :

    ![Case à cocher Inclure la préversion dans Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Le fait de cocher ou décocher cette case actualise l’interface utilisateur du gestionnaire de package et la liste des versions disponibles que vous pouvez installer.

- **Console du gestionnaire de package**: utilisez le `-IncludePrerelease` commutateur avec les `Find-Package` commandes,, `Get-Package` `Install-Package` , `Sync-Package` et `Update-Package` . Reportez-vous à [Informations de référence sur PowerShell](../reference/powershell-reference.md).

- **Interface CLI NuGet**: utilisez le `-prerelease` commutateur avec `install` les `update` commandes,, `delete` et `mirror` . Reportez-vous à [Informations de référence sur l’interface de ligne de commande NuGet](../reference/nuget-exe-cli-reference.md).

## <a name="semantic-versioning"></a>Gestion sémantique de version

La [gestion sémantique de version ou convention SemVer](https://semver.org/spec/v1.0.0.html) décrit la manière d’utiliser des chaînes dans les numéros de version pour qu’elles indiquent la signification du code sous-jacent.

Dans cette convention, chaque version se compose de trois parties, `Major.Minor.Patch`, avec la signification suivante :

- `Major` : Modifications avec rupture
- `Minor` : Nouvelles fonctionnalités, offrant néanmoins une compatibilité descendante
- `Patch` : Correctifs de bogues à compatibilité descendante uniquement

Les préversions sont alors signalées par l’ajout d’un trait d’union et d’une chaîne après le numéro du correctif. Techniquement parlant, vous pouvez utiliser *n’importe quelle* chaîne après le trait d’union pour que NuGet traite le package comme une préversion. NuGet affiche alors le numéro de version complet dans l’interface utilisateur applicable, en laissant les consommateurs interpréter la signification pour eux-mêmes.

En sachant cela, il est généralement judicieux de suivre les conventions de nommage reconnues comme les suivantes :

- `-alpha` : version alpha, généralement utilisée pour les travaux en cours et les expérimentations.
- `-beta`: version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.
- `-rc` : version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.

> [!Note]
> NuGet 4.3.0+ prend en charge la [gestion sémantique de version 2.0.0](https://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de pré-livraison utilisant la notation à points (par exemple, `1.0.1-build.23`). La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0. Dans les versions antérieures de NuGet, vous pouviez utiliser un format similaire à `1.0.1-build23`, mais celui-ci est toujours considéré comme une version de pré-livraison.

Quels que soient les suffixes que vous utilisez, toutefois, NuGet leur donne la priorité dans l’ordre alphabétique inverse :

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta.12
1.0.1-beta.5
1.0.1-beta
1.0.1-alpha.2
1.0.1-alpha
```

Comme indiqué, la version sans aucun suffixe est toujours prioritaire par rapport aux préversions.

Les zéros de début ne sont pas nécessaires avec semver2, mais ils le sont avec l’ancien schéma de version. Si vous utilisez des suffixes numériques avec des balises en version préliminaire susceptibles d’utiliser des nombres à deux chiffres (ou plus), utilisez des zéros non significatifs comme dans beta.01 et beta.05 pour pouvoir les trier correctement quand ces numéros s’allongent. Cette recommandation s’applique uniquement à l’ancien schéma de version.
