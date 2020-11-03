---
title: Commande des signataires approuvés de l’interface CLI NuGet
description: Référence pour la commande nuget.exe des signataires approuvés
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238151"
---
# <a name="trusted-signers-command-nuget-cli"></a>commande des signataires approuvés (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge par** la consommation de packages : 4.9.1 +

Obtient ou définit des signataires approuvés pour la configuration NuGet. Pour une utilisation supplémentaire, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md). Pour plus d’informations sur l’apparence du schéma nuget.config, consultez la [Référence du fichier de configuration NuGet](../nuget-config-file.md).

## <a name="usage"></a>Utilisation

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Si aucun de `list|add|remove|sync` n’est spécifié, la commande prend par défaut la valeur `list` .

## <a name="nuget-trusted-signers-list"></a>Liste des signataires approuvés NuGet

Répertorie tous les signataires approuvés dans la configuration. Cette option inclut tous les certificats (avec l’algorithme d’empreinte digitale et l’algorithme d’empreinte digitale) de chaque signataire. Si un certificat est précédé d’un `[U]` , cela signifie que l’entrée du certificat a la `allowUntrustedRoot` valeur `true` .

Voici un exemple de sortie de cette commande :

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
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

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

où `<package(s)>` se trouve un ou plusieurs `.nupkg` fichiers.

- **`-Author`**

  Spécifie que la signature de l’auteur du ou des packages doit être approuvée.

- **`-AllowUntrustedRoot`**

  Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée.

- **`-Owners`**

  Liste de propriétaires approuvés séparés par des points-virgules pour restreindre davantage l’approbation d’un référentiel. Valide uniquement lors de l’utilisation de l' `-Repository` option.

- **`-Repository`**

  Spécifie que la signature du référentiel ou la contre-signature du ou des packages doit être approuvée.

`-Author` `-Repository` Le fait de fournir à la fois et en même temps n’est pas pris en charge.

## <a name="options-for-add-based-on-a-service-index"></a>Options d’ajout basés sur un index de service

```cli
nuget trusted-signers add -Name <name> [options]
```

_Remarque_ : cette option ajoute uniquement des référentiels approuvés. 

- **`-AllowUntrustedRoot`**

  Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée.

- **`-Owners`**

  Liste de propriétaires approuvés séparés par des points-virgules pour restreindre davantage l’approbation d’un référentiel.

- **`-ServiceIndex`**

  Spécifie l’index de service v3 du référentiel à approuver. Ce dépôt doit prendre en charge la ressource de signatures de référentiel. S’il n’est pas fourni, la commande recherche une source de package avec le même `-Name` et obtient l’index de service à partir de là.

## <a name="options-for-add-based-on-the-certificate-information"></a>Options d’ajout en fonction des informations de certificat

```cli
nuget trusted-signers add -Name <name> [options]
```

_Remarque_ : si un signataire approuvé portant le même nom existe déjà, l’élément de certificat sera ajouté à ce signataire. Dans le cas contraire, un auteur approuvé sera créé avec un élément de certificat à partir des informations de certificat données.


- **`-AllowUntrustedRoot`**

  Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée.

- **`-CertificateFingerprint`**

  Spécifie les empreintes de certificat d’un certificat avec lequel les packages signés doivent être signés. Une empreinte de certificat est un hachage du certificat. L’algorithme de hachage utilisé pour le calcul de ce hachage doit être défini dans l' `FingerprintAlgorithm` option.

- **`-FingerprintAlgorithm`**

  Spécifie l’algorithme de hachage utilisé pour calculer l’empreinte digitale du certificat. La valeur par défaut est `SHA256`. Les valeurs prises en charge sont `SHA256` , `SHA384` et `SHA512` .

## <a name="nuget-trusted-signers-remove--name-name"></a>suppression des signataires approuvés NuGet-nom \<name\>

Supprime tous les signataires approuvés qui correspondent au nom donné.

## <a name="nuget-trusted-signers-sync--name-name"></a>Nom de synchronisation des signataires approuvés NuGet \<name\>

Demande la liste la plus récente des certificats utilisés dans un référentiel actuellement approuvé pour mettre à jour la liste des certificats existants dans le signataire approuvé.

_Remarque_ : ce geste supprimera la liste actuelle des certificats et les remplacera par une liste à jour du référentiel.

## <a name="options"></a>Options

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-Name`**

  Nom du signataire approuvé.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .


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
