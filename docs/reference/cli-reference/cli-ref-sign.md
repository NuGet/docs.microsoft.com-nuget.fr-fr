---
title: Commande de signature de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622770"
---
# <a name="sign-command-nuget-cli"></a>Sign, commande (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge** pour la création de package : 4.6 +

Signe tous les packages correspondant au premier argument avec un certificat. Le certificat avec la clé privée peut être obtenu à partir d’un fichier ou d’un certificat installé dans un magasin de certificats en fournissant un nom d’objet ou une empreinte numérique.

> [!Note]
> La signature du package n’est pas encore prise en charge dans .NET Core, sous mono ou sur des plateformes non-Windows.

## <a name="usage"></a>Usage

```cli
nuget sign <package(s)> [options]
```

où `<package(s)>` se trouve un ou plusieurs `.nupkg` fichiers.

## <a name="options"></a>Options

- **`-CertificateFingerprint`**

  Spécifie l’empreinte SHA-1 du certificat utilisé pour rechercher le certificat dans un magasin de certificats local.

- **`-CertificatePassword`**

  Spécifie le mot de passe du certificat, si nécessaire. Si un certificat est protégé par un mot de passe mais qu’aucun mot de passe n’est fourni, la commande vous invite à entrer un mot de passe au moment de l’exécution, sauf si l' `-NonInteractive` option est passée.

- **`-CertificatePath`**

  Spécifie le chemin d’accès au certificat à utiliser pour signer le package.

- **`-CertificateStoreLocation`**

  Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat. La valeur par défaut est « CurrentUser », le magasin de certificats X. 509 utilisé par l’utilisateur actuel. Cette option doit être utilisée lors de la spécification du certificat via les `-CertificateSubjectName` `-CertificateFingerprint` options ou.

- **`-CertificateStoreName`**

  Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat. La valeur par défaut est « My », le magasin de certificats X. 509 pour les certificats personnels. Cette option doit être utilisée lors de la spécification du certificat via les `-CertificateSubjectName` `-CertificateFingerprint` options ou.

- **`-CertificateSubjectName`**

  Spécifie le nom du sujet du certificat utilisé pour rechercher le certificat dans un magasin de certificats local.  La recherche est une comparaison de chaînes ne respectant pas la casse à l’aide de la valeur fournie, qui recherchera tous les certificats dont le nom d’objet contient cette chaîne, indépendamment des autres valeurs d’objet.  Le magasin de certificats peut être spécifié par les `-CertificateStoreName` `-CertificateStoreLocation` options et.

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-HashAlgorithm`**

  Algorithme de hachage à utiliser pour signer le package. La valeur par défaut est SHA256. Les valeurs possibles sont SHA256, SHA384 et SHA512.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-OutputDirectory`**

  Spécifie le répertoire dans lequel le package signé doit être enregistré. Par défaut, le package d’origine est remplacé par le package signé.

- **`-Overwrite`**

  Basculez pour indiquer si la signature actuelle doit être remplacée. Par défaut, la commande échoue si le package a déjà une signature.

- **`-Timestamper`**

  URL vers un serveur d’horodatage RFC 3161.

- **`-TimestampHashAlgorithm`**

  Algorithme de hachage à utiliser par le serveur d’horodatage RFC 3161. La valeur par défaut est SHA256.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

## <a name="examples"></a>Exemples

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
