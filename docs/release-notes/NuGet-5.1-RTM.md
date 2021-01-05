---
title: Notes de publication de NuGet 5,1 RTM
description: Notes de publication de NuGet 5,1, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699865"
---
# <a name="nuget-51-release-notes"></a>Notes de publication de NuGet 5,1

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio| Disponible dans les SDK .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core 

<sup>2</sup> Disponible en tant qu’installation facultative avec Visual Studio 2019 avec la charge de travail .NET Core

## <a name="summary-whats-new-in-51"></a>Résumé : nouveautés de 5,1

* Prise en charge pour ignorer un push de package s’il existe déjà pour permettre une meilleure intégration avec les flux de travail CI/CD- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio fournit maintenant un lien pratique vers la page de la Galerie nuget.org du package- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Prise en charge des nouvelles ressources .NET Core 3,0, telles que le [ciblage de packs](https://github.com/dotnet/cli/issues/10006) et les [packs d’exécution](https://github.com/dotnet/cli/issues/10007)
  * Prise en charge du Pack et de la restauration NuGet pour FrameworkReferences pour activer le ciblage et les références de package d’exécution- [#7342](https://github.com/NuGet/Home/issues/7342)
  * Prise en charge du scénario de package « Télécharger uniquement » avec PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * Exclure le runtime et les packs de ciblage des résultats de la recherche & Restore Graph à l’aide de PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Bogues**

* Plug-ins : détails de l’exception perdus pendant la création du plug-in- [#8057](https://github.com/NuGet/Home/issues/8057)

* La plage PackageReference avec limite inférieure exclusive ne fonctionne pas si la limite inférieure est présente dans l’une des sources. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Améliorer les messages IsPackableFalseError- [#8021](https://github.com/NuGet/Home/issues/8021)

* Packages verrouiller les fichiers-régénérer le fichier de verrouillage lorsque le graphique du projet change- [#8019](https://github.com/NuGet/Home/issues/8019)

* Bogue ProjectSystem : packages NuGet en cours de suppression automatique- [#8017](https://github.com/NuGet/Home/issues/8017)

* Ajoutez une cible pour retourner le FrameworkReference similaire à CollectPackageDownloads et CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* Cache HTTP : la ressource RepositoryResources n’est pas mise en cache dans une méthode avec version [#7997](https://github.com/NuGet/Home/issues/7997)

* Journalisation : les piles d’exception ne sont pas signalés avec un niveau de détail détaillé- [#7955](https://github.com/NuGet/Home/issues/7955)

* Modifiez toutes les URL des documents NuGet pour utiliser le protocole HTTPs- [#7950](https://github.com/NuGet/Home/issues/7950)

* Améliorer le message d’avertissement NU3024- [#7933](https://github.com/NuGet/Home/issues/7933)

* verrouillage du fichier qui n’est pas mis à jour quand packagereference a été supprimé- [#7930](https://github.com/NuGet/Home/issues/7930)

* Améliorer la gestion des cas d’erreur lors de la validation de licenseUrl et de l’élément de licence dans NuSpec- [#7915](https://github.com/NuGet/Home/issues/7915)

* Interface utilisateur PM-cliquer avec le bouton droit sur l’en-tête de l’onglet et cliquer sur « Ouvrir l’emplacement du fichier » génère une erreur- [#7913](https://github.com/NuGet/Home/issues/7913)

* Plug-ins : journal lorsque le processus de plug-in se termine- [#7907](https://github.com/NuGet/Home/issues/7907)

* Plug-ins : taux de collision élevé dans la journalisation des valeurs DateTime- [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest. ReadFrom échoue sur n’importe quel NuSpec avec LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode : NU1004 inattendu quand ProjectReference fait référence à un projet avec un [#7889](https://github.com/NuGet/Home/issues/7889) AssemblyName personnalisé

* Meilleur message d’erreur lorsque le démarrage du plug-in échoue avec une exception- [#7857](https://github.com/NuGet/Home/issues/7857)

* Lorsque vous procédez à une restauration NoOp, évitez * .dgspec.jsen écriture dans le répertoire obj- [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true ne parvient pas à générer la propriété en cas d’incompatibilité de cas- [#7843](https://github.com/NuGet/Home/issues/7843)

* Paramètres : un caractère non conforme dans le chemin source du package peut se bloquer et [#7820](https://github.com/NuGet/Home/issues/7820)

* Si le fichier de verrouillage est supprimé, la restauration ne génère pas de fichier de verrouillage sur NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)

* L’URL et la licence de la licence provoquent une erreur de lecture avec les métadonnées- [#7547](https://github.com/NuGet/Home/issues/7547)

* Exceptions non gérées dans V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe retourne le code de sortie zéro pour les arguments non valides- [#7178](https://github.com/NuGet/Home/issues/7178)

* Mettre à jour les erreurs et les documents d’avertissement pour refléter les scénarios liés à la signature- [#6498](https://github.com/NuGet/Home/issues/6498)

* Le fichier de ressources doit utiliser des chemins d’accès relatifs pour faciliter le déplacement des projets [#4582](https://github.com/NuGet/Home/issues/4582)

**DCR**

* Plug-ins : activer la journalisation des diagnostics- [#7859](https://github.com/NuGet/Home/issues/7859)

* Faire correspondre Tizen 6 à netstandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[Liste de tous les problèmes résolus dans cette version-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
