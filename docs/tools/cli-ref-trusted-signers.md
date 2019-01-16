---
title: Commande de signataires approuvé de CLI de NuGet
description: Référence de la commande signataires approuvé de nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324706"
---
# <a name="trusted-signers-command-nuget-cli"></a>commande signataires approuvé (CLI NuGet)

**S’applique à :** la consommation de package &bullet; **versions prises en charge :** 4.9.1+

Obtient ou définit les signataires approuvés à la configuration de NuGet. Pour une utilisation supplémentaire, consultez [configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md). Pour plus d’informations sur la façon dont le schéma de nuget.config ressemble, reportez-vous à la [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Utilisation

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Si aucun des `list|add|remove|sync` est spécifié, la commande par défaut sera `list`.

## <a name="nuget-trusted-signers-list"></a>liste des signataires approuvé de NuGet

Répertorie tous les signataires approuvés dans la configuration. Cette option permet d’inclure tous les certificats (avec empreintes digitales et algorithme d’empreinte digitale) a chaque signataire. Si un certificat a précédente `[U]`, cela signifie qu’entrée de certificat a `allowUntrustedRoot` définir en tant que `true`.

Voici un exemple de sortie à partir de cette commande :

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>NuGet approuvé-signataires ajouter [options]

Ajoute un signataire approuvé avec le nom donné à la configuration. Cette option a des gestes différents pour ajouter un auteur approuvé ou un référentiel.

## <a name="options-for-add-based-on-a-package"></a>Options pour ajouter basé sur un package

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

où `<package(s)>` comporte un ou plusieurs `.nupkg` fichiers.

| Option | Description |
| --- | --- |
| Auteur | Spécifie que la signature de l’auteur du ou des modules doit être approuvée. |
| Référentiel | Spécifie que la signature de référentiel ou d’une contre-signature du ou des modules doit être approuvé. |
| AllowUntrustedRoot | Spécifie si le certificat pour le signataire approuvé doit être autorisé à la chaîne à une racine non approuvée. |
| Propriétaires | Liste séparés par des points-virgules des propriétaires approuvés pour restreindre davantage l’approbation d’un référentiel. Valide uniquement lorsque vous utilisez la `-Repository` option. |

En fournissant les deux `-Author` et `-Repository` en même temps n’est pas pris en charge.

## <a name="options-for-add-based-on-a-service-index"></a>Options pour ajouter basé sur un index de service

```cli
nuget trusted-signers add -Name <name> [options]
```

_Remarque_ : Cette option n’ajoute des référentiels approuvés. 

| Option | Description |
| --- | --- |
| ServiceIndex | Spécifie l’index de service V3 du référentiel d’être approuvés. Ce dépôt a prendre en charge de la ressource de signatures du référentiel. Si n’est fourni, la commande recherchera une source de package avec le même `-Name` et obtenir l’index de service à partir de là. |
| AllowUntrustedRoot | Spécifie si le certificat pour le signataire approuvé doit être autorisé à la chaîne à une racine non approuvée. |
| Propriétaires | Liste séparés par des points-virgules des propriétaires approuvés pour restreindre davantage l’approbation d’un référentiel. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Options pour ajouter selon les informations de certificat

```cli
nuget trusted-signers add -Name <name> [options]
```

_Remarque_ : Si un signataire approuvé portant le nom spécifié existe déjà, l’élément de certificat est ajouté pour que le signataire. Sinon, un auteur approuvé sera créé avec un élément de certificat à partir des informations de certificat spécifiées.

| Option | Description |
| --- | --- |
| CertificateFingerprint | Spécifie un certificat empreintes d’un certificat qui packages signés doivent être signées avec. Une empreinte de certificat est un hachage du certificat. Spécifie l’algorithme de hachage utilisé pour calculer ce hachage doit être le `FingerprintAlgorithm` option. |
| FingerprintAlgorithm | Spécifie l’algorithme de hachage utilisé pour calculer l’empreinte numérique du certificat. La valeur par défaut est `SHA256`. Valeurs prises en charge sont `SHA256`, `SHA384` et `SHA512` |
| AllowUntrustedRoot | Spécifie si le certificat pour le signataire approuvé doit être autorisé à la chaîne à une racine non approuvée. |

## <a name="nuget-trusted-signers-remove--name-name"></a>NuGet approuvé-signataires remove - nom <name>

Supprime les signataires approuvés qui correspondent au nom donné.

## <a name="nuget-trusted-signers-sync--name-name"></a>NuGet approuvé-signataires synchroniser - nom <name>

Demande la dernière liste des certificats utilisés dans un référentiel actuellement approuvé pour mettre à jour le la liste de certificats existants dans le signataire approuvé.

_Remarque_ : Ce mouvement supprime la liste actuelle des certificats et les remplacer par une liste à jour à partir du référentiel.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

## <a name="examples"></a>Exemples

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
