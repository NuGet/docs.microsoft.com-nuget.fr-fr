---
title: Commande de signature de l’interface CLI NuGet
description: Référence pour la commande de signature NuGet. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e596fd5eb3de8ca4802d9b7b8e7cb623568e3dcb
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231121"
---
# <a name="sign-command-nuget-cli"></a>sign (commande, NuGet CLI)

**S’applique à : création de** package &bullet; **versions prises en charge :** 4.6 +

Signe tous les packages correspondant au premier argument avec un certificat. Le certificat avec la clé privée peut être obtenu à partir d’un fichier ou d’un certificat installé dans un magasin de certificats en fournissant un nom d’objet ou une empreinte numérique.

> [!Note]
> La signature du package n’est pas encore prise en charge dans .NET Core, sous mono ou sur des plateformes non-Windows.

## <a name="usage"></a>Usage

```cli
nuget sign <package(s)> [options]
```

où `<package(s)>` est un ou plusieurs fichiers `.nupkg`.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| CertificateFingerprint | Spécifie l’empreinte SHA-1 du certificat utilisé pour rechercher le certificat dans un magasin de certificats local. |
| CertificatePassword | Spécifie le mot de passe du certificat, si nécessaire. Si un certificat est protégé par un mot de passe mais qu’aucun mot de passe n’est fourni, la commande vous invite à entrer un mot de passe au moment de l’exécution, sauf si l’option-non interactive est passée. |
| CertificatePath | Spécifie le chemin d’accès au certificat à utiliser pour signer le package. |
| CertificateStoreLocation | Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat. La valeur par défaut est « CurrentUser », le magasin de certificats X. 509 utilisé par l’utilisateur actuel. Cette option doit être utilisée lors de la spécification du certificat via les options-CertificateSubjectName ou-CertificateFingerprint. |
| CertificateStoreName | Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat. La valeur par défaut est « My », le magasin de certificats X. 509 pour les certificats personnels. Cette option doit être utilisée lors de la spécification du certificat via les options-CertificateSubjectName ou-CertificateFingerprint. |
| CertificateSubjectName | Spécifie le nom du sujet du certificat utilisé pour rechercher le certificat dans un magasin de certificats local.  La recherche est une comparaison de chaînes ne respectant pas la casse à l’aide de la valeur fournie, qui recherchera tous les certificats dont le nom d’objet contient cette chaîne, indépendamment des autres valeurs d’objet.  Le magasin de certificats peut être spécifié par les options-CertificateStoreName et-CertificateStoreLocation. |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais. |
| HashAlgorithm | Algorithme de hachage à utiliser pour signer le package. La valeur par défaut est SHA256. Les valeurs possibles sont SHA256, SHA384 et SHA512. |
| Aide | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| OutputDirectory | Spécifie le répertoire dans lequel le package signé doit être enregistré. Par défaut, le package d’origine est remplacé par le package signé. |
| Remplacer | Basculez pour indiquer si la signature actuelle doit être remplacée. Par défaut, la commande échoue si le package a déjà une signature. |
| Timestamper | URL vers un serveur d’horodatage RFC 3161. |
| TimestampHashAlgorithm | Algorithme de hachage à utiliser par le serveur d’horodatage RFC 3161. La valeur par défaut est SHA256. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie : *normal*, *Quiet*, *detailed*. |

## <a name="examples"></a>Exemples

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
