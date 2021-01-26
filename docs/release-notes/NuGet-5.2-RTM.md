---
title: Notes de publication de NuGet 5,2 RTM
description: Notes de publication de NuGet 5,2, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776206"
---
# <a name="nuget-52-release-notes"></a>Notes de publication de NuGet 5,2

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio| Disponible dans les SDK .NET|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core 

<sup>2</sup> Disponible en tant qu’installation facultative avec Visual Studio 2019 avec la charge de travail .NET Core

## <a name="summary-whats-new-in-52"></a>Résumé : nouveautés de 5,2

* Correction d’un bogue critique qui provoquait occasionnellement des échecs d’opération NuGet en raison de problèmes de chemin sur Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)

* Amélioration de la réactivité de l’interface utilisateur lors de l’exploration des packages à l’aide de l’interface utilisateur du gestionnaire de package NuGet dans Visual Studio, particulièrement pour les sources lentes- [#8039](https://github.com/NuGet/Home/issues/8039)

* Tonnes de correctifs de fiabilité pour le fichier de verrouillage ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) et le plug-in d’authentification ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210)[, #8198,](https://github.com/NuGet/Home/issues/8198)[#7845](https://github.com/NuGet/Home/issues/7845))

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Bogues**

* Perf : console du gestionnaire de package : mise à jour différée de l’interface utilisateur « projet par défaut », valeur sélectionnée de la liste modifiable- [#8235](https://github.com/NuGet/Home/issues/8235)

* Performances : améliorations des performances dans l’interface utilisateur PM- [#8039](https://github.com/NuGet/Home/issues/8039)

* Perf : délai d’attente de l’interface utilisateur lors de la lecture du projet par défaut dans PMC- [#6824](https://github.com/NuGet/Home/issues/6824)

* Perf : [vsfeedback] l’onglet de mise à jour NuGet se fige pour une source de package locale- [#6470](https://github.com/NuGet/Home/issues/6470)

* Plug-ins : NuGet attend le délai d’expiration de la négociation complète si le plug-in ne parvient pas à démarrer ou à se terminer [#8300](https://github.com/NuGet/Home/issues/8300)

* Plug-ins : améliorer la diagnostic de l’échec de lancement du plug-in- [#8271](https://github.com/NuGet/Home/issues/8271)

* Plug-ins : problème avec nuget.exe découverte de plug-ins intégrés- [#8269](https://github.com/NuGet/Home/issues/8269)

* Plug-ins : le fichier cache n’est jamais en lecture [#8210](https://github.com/NuGet/Home/issues/8210)

* Plug-ins : « une tâche a été annulée. » erreurs avec le plug-in d’authentification lors de la restauration- [#8198](https://github.com/NuGet/Home/issues/8198)

* Cache de plug-ins non détectable par intermittence sur les plateformes Linux- [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile : avec ATF, le NU1004 est faux en raison d’une vérification de l’égalité de la version cible du .NET Framework incorrecte- [#8187](https://github.com/NuGet/Home/issues/8187)

* LockFile : indicateur de restauration'--Locked-Mode’non respecté si le fichier de verrouillage est vide ou incorrect [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile : pas de projets en minuscules avec des noms d’assemblys personnalisés dans les packages verrouiller les fichiers- [#8114](https://github.com/NuGet/Home/issues/8114)

* LockFile : mettre la référence du projet en minuscules dans le fichier de verrouillage- [#7840](https://github.com/NuGet/Home/issues/7840)

* Restauration : l’installation d’un package avec signature falsifiée entraîne l’échec de plusieurs tentatives d’installation (avec une sortie répétée)- [#8175](https://github.com/NuGet/Home/issues/8175)

* VS : les options utilisateur de solution ne sont pas désérialisées après la mise à jour NuGet- [#8166](https://github.com/NuGet/Home/issues/8166)

* dotnet-List-package dans un projet UnitTest retourne une erreur : [#8154](https://github.com/NuGet/Home/issues/8154)

* Créer un groupe de packages NuGet pour le programme d’installation de VS-correction de certains problèmes d’installation VSIX- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild ne doit pas définir nobuild. - [#7801](https://github.com/NuGet/Home/issues/7801)

* La nouvelle option « -SymbolPackageFormat snupkg » génère une erreur lorsque le fichier. NuSpec contient un élément de référence d’assembly explicite- [#7638](https://github.com/NuGet/Home/issues/7638)

* NuGet. targets (498, 5) : erreur : impossible de trouver une partie du chemin d’accès'/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)

**DCR :**

* Ajoutez une propriété MSBuild qui indique que PackageDownload est pris en charge- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference supprimer le workflow de dépendance via FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* Mécanisme permettant de fournir des runtime.jsà l’extérieur d’un package- [#7351](https://github.com/NuGet/Home/issues/7351)

**[Liste de tous les problèmes résolus dans cette version-5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


