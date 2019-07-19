---
title: Commande des signataires approuvés de l’interface CLI NuGet
description: Informations de référence sur la commande NuGet. exe Trusted-Signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327536"
---
# <a name="trusted-signers-command-nuget-cli"></a>commande des signataires approuvés (interface CLI NuGet)

**S’applique à:** &bullet; **versions prises en charge par** la consommation des packages: 4.9.1 +

Obtient ou définit des signataires approuvés pour la configuration NuGet. Pour une utilisation supplémentaire, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md). Pour plus d’informations sur l’apparence du schéma NuGet. config, reportez-vous à la [Référence du fichier de configuration NuGet](../nuget-config-file.md).

## <a name="usage"></a>Usage

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Si aucun de `list|add|remove|sync` n’est spécifié, la commande prend `list`par défaut la valeur.

## <a name="nuget-trusted-signers-list"></a>Liste des signataires approuvés NuGet

Répertorie tous les signataires approuvés dans la configuration. Cette option inclut tous les certificats (avec l’algorithme d’empreinte digitale et l’algorithme d’empreinte digitale) de chaque signataire. Si un certificat est précédé `[U]`d’un, cela signifie que l’entrée du certificat a `allowUntrustedRoot` la valeur `true`.

Voici un exemple de sortie de cette commande:

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

## <a name="nuget-trusted-signers-add-options"></a>les signataires approuvés NuGet Add [options]

Ajoute un signataire approuvé portant le nom donné à la configuration. Cette option a des gestes différents pour ajouter un auteur ou un dépôt approuvé.

## <a name="options-for-add-based-on-a-package"></a>Options d’ajout basés sur un package

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

où `<package(s)>` se trouve un ou `.nupkg` plusieurs fichiers.

| Option | Description |
| --- | --- |
| Auteur | Spécifie que la signature de l’auteur du ou des packages doit être approuvée. |
| Référentiel | Spécifie que la signature du référentiel ou la contre-signature du ou des packages doit être approuvée. |
| AllowUntrustedRoot | Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée. |
| Propriétaires | Liste de propriétaires approuvés séparés par des points-virgules pour restreindre davantage l’approbation d’un référentiel. Valide uniquement lors de l' `-Repository` utilisation de l’option. |

Le fait de `-Repository` fournir à la fois etenmêmetempsn’estpasprisencharge.`-Author`

## <a name="options-for-add-based-on-a-service-index"></a>Options d’ajout basés sur un index de service

```cli
nuget trusted-signers add -Name <name> [options]
```

_Remarque_: Cette option permet d’ajouter uniquement des référentiels approuvés. 

| Option | Description |
| --- | --- |
| ServiceIndex | Spécifie l’index de service v3 du référentiel à approuver. Ce dépôt doit prendre en charge la ressource de signatures de référentiel. S’il n’est pas fourni, la commande recherche une source de package avec `-Name` le même et obtient l’index de service à partir de là. |
| AllowUntrustedRoot | Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée. |
| Propriétaires | Liste de propriétaires approuvés séparés par des points-virgules pour restreindre davantage l’approbation d’un référentiel. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Options d’ajout en fonction des informations de certificat

```cli
nuget trusted-signers add -Name <name> [options]
```

_Remarque_: Si un signataire approuvé portant le même nom existe déjà, l’élément de certificat est ajouté à ce signataire. Dans le cas contraire, un auteur approuvé sera créé avec un élément de certificat à partir des informations de certificat données.

| Option | Description |
| --- | --- |
| CertificateFingerprint | Spécifie les empreintes de certificat d’un certificat avec lequel les packages signés doivent être signés. Une empreinte de certificat est un hachage du certificat. L’algorithme de hachage utilisé pour le calcul de ce hachage doit `FingerprintAlgorithm` être défini dans l’option. |
| FingerprintAlgorithm | Spécifie l’algorithme de hachage utilisé pour calculer l’empreinte digitale du certificat. La valeur par défaut est `SHA256`. Les valeurs prises `SHA256`en `SHA384` charge sont, et`SHA512` |
| AllowUntrustedRoot | Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée. |

## <a name="nuget-trusted-signers-remove--name-name"></a>suppression des signataires approuvés NuGet-nom<name>

Supprime tous les signataires approuvés qui correspondent au nom donné.

## <a name="nuget-trusted-signers-sync--name-name"></a>Nom de synchronisation des signataires approuvés NuGet<name>

Demande la liste la plus récente des certificats utilisés dans un référentiel actuellement approuvé pour mettre à jour la liste des certificats existants dans le signataire approuvé.

_Remarque_: Ce geste supprimera la liste actuelle des certificats et les remplacera par une liste à jour du référentiel.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais. |
| Aide | Affiche des informations d’aide pour la commande. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

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
