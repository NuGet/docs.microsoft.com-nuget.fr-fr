---
title: Notes de publication de NuGet 5,3
description: Notes de publication de NuGet 5,3, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 009a219139a767ee6453305be68ccce478b0ec75
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780123"
---
# <a name="nuget-53-release-notes"></a>Notes de publication de NuGet 5,3

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio| Disponible dans les SDK .NET|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,3](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |
| [**5.3.1**](https://nuget.org/downloads) | [Version 16.3.6 de Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) | [Version future : 3.0.101](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core

## <a name="summary-whats-new-in-53"></a>Résumé : nouveautés de 5,3

* [L’icône de package peut être incorporée dans le package](../reference/msbuild-targets.md#packing-an-icon-image-file), au lieu d’avoir besoin d’une URL externe. - [#352](https://github.com/NuGet/Home/issues/352)

* Sécurité améliorée avec suivi et mise en application SHA pour Packages.Config- [#7281](https://github.com/NuGet/Home/issues/7281)

* Activer la désapprobation des packages NuGet obsolètes/hérités [#2867](https://github.com/NuGet/Home/issues/2867)  |  [](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/)  |  [documents](../nuget-org/deprecate-packages.md) du billet de blog

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Bogues**

* Les packages NuGet produits avec le kit de développement logiciel (SDK) 3.0.100-preview9 ne peuvent pas être utilisés par les utilisateurs du SDK 2,2... en fonction de votre fuseau horaire [#8603](https://github.com/NuGet/Home/issues/8603)

* Guillemets dans le chemin d’accès, la cause de l’erreur « caractères illégaux dans le chemin d’accès » dans `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)

* VS : les assemblys sont entièrement Ngen-Ed non partiellement Ngen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)

* Réduire l’utilisation de la mémoire (se désabonner des événements)- [#8471](https://github.com/NuGet/Home/issues/8471)

* Le message « Error_UnableToFindProjectInfo » n’est pas correct par programmation- [#8441](https://github.com/NuGet/Home/issues/8441)

* Améliorations apportées à NU1403-valider tous les packages, inclure les valeurs SHA attendues/réelles- [#8424](https://github.com/NuGet/Home/issues/8424)

* Énumération multiple dans `NuGetPackageManager.PreviewUpdatePackagesAsync`  -  [#8401](https://github.com/NuGet/Home/issues/8401)

* Restauration de la modification « public-> Internal » dans PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider. GetSources (...) a un comportement d’exception mal défini- [#8383](https://github.com/NuGet/Home/issues/8383)

* Rendre publique le constructeur PluginManager- [#8379](https://github.com/NuGet/Home/issues/8379)

* Mesures permettant de suivre la fréquence d’actualisation de l’interface utilisateur PM- [#8369](https://github.com/NuGet/Home/issues/8369)

* Réduire le nombre d’actualisations de l’interface utilisateur lors de l’installation par le biais de l’interface utilisateur du gestionnaire de package- [#8358](https://github.com/NuGet/Home/issues/8358)

* Télémétrie : les valeurs DateTime utilisent des formats spécifiques à la culture- [#8351](https://github.com/NuGet/Home/issues/8351)

* Réduire les actualisations de l’interface utilisateur sous l’onglet Parcourir de l’interface utilisateur du gestionnaire de package #6570- [#8339](https://github.com/NuGet/Home/issues/8339)

* [Échec du test] Le message « Impossible d’analyser le fichier de configuration » s’affiche à deux reprises [#8320](https://github.com/NuGet/Home/issues/8320)

* Déclencher une erreur NU5037 avec une bonne page de documentation qui explique les correctifs du client (le fichier NuSpec requis est manquant dans le package)- [#8291](https://github.com/NuGet/Home/issues/8291)

* La restauration en mode verrouillé échoue quand le RuntimeIdentifier d’un projet est modifié- [#8260](https://github.com/NuGet/Home/issues/8260)

* Rendre les paramètres lus dans VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)

* La régression dans `Nuget sources add` amène le caractère «  : », la valeur hexadécimale 0x3A, ne peut pas être inclus dans un nom «Errors- [#7948](https://github.com/NuGet/Home/issues/7948)

* Fournisseurs d’informations d’identification du plug-in NuGet-masquer la fenêtre de processus- [#7511](https://github.com/NuGet/Home/issues/7511)

* L’application de PackagePathResolver est un chemin d’accès absolu- [#7349](https://github.com/NuGet/Home/issues/7349)

* Réduire les actualisations de l’interface utilisateur dans les onglets installer et mettre à jour de l’interface utilisateur du gestionnaire de package- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR :**

* Mettre à jour les frameworks Xamarin pour les mapper à netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Activer la copie du contenu de la « fenêtre d’aperçu » du gestionnaire de package pour l’installation/la mise à jour- [#8324](https://github.com/NuGet/Home/issues/8324)

* Activer la restauration sur les fichiers. proj- [#8212](https://github.com/NuGet/Home/issues/8212)

* Introduire `NUGET_NETFX_PLUGIN_PATHS` et `NUGET_NETCORE_PLUGIN_PATHS` pour prendre en charge la configuration des deux en même temps [#8151](https://github.com/NuGet/Home/issues/8151)

* Activer plusieurs versions pour un PackageDownload via l’attribut de version- [#8074](https://github.com/NuGet/Home/issues/8074)

* Options Add-SolutionDirectory et-PackageDirectory pour nuget.exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)

**[Liste de tous les problèmes résolus dans cette version-5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**

## <a name="summary-whats-new-in-531"></a>Résumé : nouveautés de la procédure 5.3.1

* Plug-in : une tâche a été annulée-ne laissez pas les annulations affecter l’instanciation du plug-in- [#8648](https://github.com/NuGet/Home/issues/8648)

* La tâche de restauration ne peut pas être exécutée deux fois en toute sécurité dans un même processus (lorsque des fournisseurs d’informations d’identification sont utilisés)- [#8688](https://github.com/NuGet/Home/issues/8688)
