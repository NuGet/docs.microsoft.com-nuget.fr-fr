---
title: Commande de connexion NuGet CLI | Documents Microsoft
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande de connexion de nuget.exe"
keywords: "référence de connexion NuGet, commande sign"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: f600a0830472703f40ef62f1b1538c53671703a9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="sign-command-nuget-cli"></a>commande de connexion (NuGet CLI)

**S’applique à :** la création de package &bullet; **versions prises en charge :** 4.6 +

Signe tous les packages de mise en correspondance le premier argument avec un certificat. Le certificat avec la clé privée peut être obtenu à partir d’un fichier ou à partir d’un certificat installé dans un magasin de certificats en fournissant un nom d’objet ou une empreinte numérique.

La signature du package n'est pas encore prise en charge sous Mono ou sur les plateformes non Windows.

## <a name="usage"></a>Utilisation

```cli
nuget sign <package(s)> [options]
```

où `<package(s)>` est un ou plusieurs `.nupkg` fichiers.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| CertificateFingerprint | Spécifie l’empreinte SHA-1 du certificat utilisé pour rechercher un magasin de certificats local pour le certificat. |
| CertificatePassword | Spécifie le mot de passe du certificat, si nécessaire. Si un certificat est protégé par mot de passe, mais aucun mot de passe n’est fourni, la commande vous demande un mot de passe au moment de l’exécution, à moins que l’option - option non interactif est passée. |
| CertificatePath | Spécifie le chemin d’accès de fichier pour le certificat à utiliser dans la signature du package. |
| CertificateStoreLocation | Spécifie le nom de l’utilisation du magasin de certificats X.509 pour rechercher le certificat. La valeur par défaut est « CurrentUser », le magasin de certificats X.509 utilisé par l’utilisateur actuel. Cette option doit être utilisée lorsque vous spécifiez le certificat via les options disponibles CertificateSubjectName - ou - CertificateFingerprint. |
| CertificateStoreName | Spécifie le nom du magasin de certificats X.509 à utiliser pour rechercher le certificat. Valeur par défaut est « My », le magasin de certificats X.509 pour les certificats personnels. Cette option doit être utilisée lorsque vous spécifiez le certificat via les options disponibles CertificateSubjectName - ou - CertificateFingerprint. |
| CertificateSubjectName | Spécifie le nom du sujet du certificat utilisé pour rechercher un magasin de certificats local pour le certificat.  La recherche est une comparaison de chaînes pas la casse à l’aide de la valeur fournie, qui recherche tous les certificats avec le nom d’objet contient cette chaîne, indépendamment des autres valeurs de l’objet.  Le magasin de certificats peut être spécifié par les options CertificateStoreName - et - CertificateStoreLocation. |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| HashAlgorithm | Algorithme de hachage à utiliser pour signer le package. La valeur par défaut est SHA256. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| OutputDirectory | Spécifie le répertoire où le package signé doit être enregistré. Par défaut, le package d’origine est remplacé par le package signé. |
| Overwrite | Commutateur pour indiquer si la signature en cours doit être remplacée. Par défaut, la commande échoue si le package possède déjà une signature. |
| Timestamper | URL vers un serveur d’horodatage RFC 3161. |
| TimestampHashAlgorithm | Algorithme de hachage à utiliser par le serveur d’horodatage RFC 3161. La valeur par défaut est SHA256. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

## <a name="examples"></a>Exemples

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```