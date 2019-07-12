---
title: Notes de version 5.1 RTM de NuGet
description: Notes de publication pour 5.1 NuGet, y compris les nouvelles fonctionnalités, les correctifs de bogues et les dcr.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842577"
---
# <a name="nuget-51-release-notes"></a>Notes de publication NuGet 5.1

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio| Disponible dans les SDK .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>installées avec Visual Studio 2019 par charge de travail .NET Core 

<sup>2</sup>disponible en tant qu’option installation avec Visual Studio 2019 avec la charge de travail .NET Core

## <a name="summary-whats-new-in-51"></a>Résumé : Quelles sont les nouveautés dans 5.1

* Prise en charge pour ignorer un push de package s’il existe déjà pour permettre une meilleure intégration avec les flux de travail CI/CD - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio fournit désormais un lien pratique vers la page du package de la galerie nuget.org - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Prise en charge de nouvelles ressources .NET Core 3.0 comme [Pack de ciblage](https://github.com/dotnet/cli/issues/10006) et [Packs de Runtime](https://github.com/dotnet/cli/issues/10007)
  * La prise en charge de NuGet pack et restore pour FrameworkReferences activer les références de package de ciblage et exécution - [#7342](https://github.com/NuGet/Home/issues/7342)
  * Prise en charge « télécharger uniquement » package scénario avec PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)
  * À l’aide du graphique Exlcude runtime et les packs à partir des résultats de recherche et de restauration de ciblage PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Bogues**

* Plug-ins : détails de l’exception perdu lors de la création de plug-in - [#8057](https://github.com/NuGet/Home/issues/8057)

* Plage de PackageReference avec une limite inférieure exclusive ne fonctionne pas si la limite inférieure est présente sur une des sources. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Améliorer IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)

* Fichier de verrouillage - fichier de verrouillage régénérer lors de changements dans le graphique de projet - les packages [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem bogue : Les Packages NuGet obtention automatique supprimé - [#8017](https://github.com/NuGet/Home/issues/8017)

* Ajouter une cible pour retourner le FrameworkReference similaires aux CollectPackageDownloads et CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)

* Cache HTTP :  RepositoryResources ressource n’est pas mis en cache d’une manière avec version - [#7997](https://github.com/NuGet/Home/issues/7997)

* Journalisation : pile des appels d’exception ne sont pas signalés avec des commentaires détaillés - [#7955](https://github.com/NuGet/Home/issues/7955)

* Modifiez toutes les URL de Docs de NuGet afin d’utiliser le protocole HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)

* Améliorer le message d’avertissement NU3024 - [#7933](https://github.com/NuGet/Home/issues/7933)

* fichier de verrouillage ne pas mis à jour lorsque packagereference supprimé - [#7930](https://github.com/NuGet/Home/issues/7930)

* Améliorer la gestion de cas d’erreur lors de la validation d’un élément licenseurl et licence dans nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)

* PM UI - un clic droit sur l’en-tête d’onglet et en cliquant sur « Ouvrir l’emplacement du fichier » entraîne l’erreur - [#7913](https://github.com/NuGet/Home/issues/7913)

* Plug-ins : consigner les lors de la sortie du processus de plug-in - [#7907](https://github.com/NuGet/Home/issues/7907)

* Plug-ins : taux de collision élevé dans les valeurs de date/heure de journalisation - [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom échoue sur n’importe quel fichier nuspec avec LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode : NU1004 inattendu lorsque ProjectReference fait référence à un projet avec AssemblyName personnalisé - [#7889](https://github.com/NuGet/Home/issues/7889)

* Meilleur message d’erreur lorsque le démarrage de plug-in échoue avec une exception - [#7857](https://github.com/NuGet/Home/issues/7857)

* Lorsque vous effectuez une restauration NoOp, éviter *. écriture dgspec.json dans le répertoire obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = trues ne peut pas générer la propriété sur le non-respect de la casse - [#7843](https://github.com/NuGet/Home/issues/7843)

* Paramètres : caractère non conforme dans le chemin source du package peut se bloquer VS - [#7820](https://github.com/NuGet/Home/issues/7820)

* Si le fichier de verrouillage est supprimé, restauration ne génère pas de fichier de verrouillage sur NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)

* URL de licence et les causes de licence lire erreur avec des métadonnées - [#7547](https://github.com/NuGet/Home/issues/7547)

* Exceptions non gérées dans V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)

* NuGet.exe retourne le code de sortie zéro pour les arguments non valides - [#7178](https://github.com/NuGet/Home/issues/7178)

* Mettre à jour des erreurs et des documents de l’avertissement pour refléter des scénarios connexes signatures - [#6498](https://github.com/NuGet/Home/issues/6498)

* Fichier de ressources doit utiliser des chemins d’accès relatifs pour activer le déplacement de projets plus facilement - [#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* Plug-ins : activer la journalisation des diagnostics - [#7859](https://github.com/NuGet/Home/issues/7859)

* Mappage de Tizen 6 Vérifiez à la version 2.1 de NetStandard - [#7773](https://github.com/NuGet/Home/issues/7773)

**[Liste de tous les problèmes résolus dans cette version - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
