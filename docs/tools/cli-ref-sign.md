---
title: Commande de connexion de CLI de NuGet
description: Référence de la commande de connexion de nuget.exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546361"
---
# <a name="sign-command-nuget-cli"></a>sign (commande, NuGet CLI)

**S’applique à :** la création de package &bullet; **versions prises en charge :** 4.6 +

Signe tous les packages de mise en correspondance le premier argument avec un certificat. Le certificat avec la clé privée peut être obtenu à partir d’un fichier ou d’un certificat installé dans un magasin de certificats en fournissant un nom d’objet ou une empreinte numérique.

La signature du package n’est pas encore pris en charge dans .NET Core, sous Mono, ou sur des plateformes non Windows.

## <a name="usage"></a>Utilisation

```cli
nuget sign <package(s)> [options]
```

où `<package(s)>` comporte un ou plusieurs `.nupkg` fichiers.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| CertificateFingerprint | Spécifie l’empreinte SHA-1 du certificat utilisé pour rechercher un magasin de certificats local pour le certificat. |
| CertificatePassword | Spécifie le mot de passe du certificat, si nécessaire. Si un certificat est protégé par mot de passe, mais aucun mot de passe n’est fourni, la commande vous demande un mot de passe en cours d’exécution, sauf si l’option - option non interactive est passée. |
| CertificatePath | Spécifie le chemin d’accès de fichier pour le certificat à utiliser pour signer le package. |
| CertificateStoreLocation | Spécifie le nom de l’utilisation du magasin de certificats X.509 pour rechercher le certificat. La valeur par défaut est « CurrentUser », le magasin de certificats X.509 utilisé par l’utilisateur actuel. Cette option doit être utilisée lorsque vous spécifiez le certificat par le biais des options CertificateSubjectName - ou - CertificateFingerprint. |
| CertificateStoreName | Spécifie le nom du magasin de certificats X.509 à utiliser pour rechercher le certificat. Valeur par défaut est « My », le magasin de certificats X.509 pour les certificats personnels. Cette option doit être utilisée lorsque vous spécifiez le certificat par le biais des options CertificateSubjectName - ou - CertificateFingerprint. |
| CertificateSubjectName | Spécifie le nom du sujet du certificat utilisé pour rechercher un magasin de certificats local pour le certificat.  La recherche est une comparaison de chaînes respectant la casse à l’aide de la valeur fournie, qui recherchera tous les certificats dont le nom de l’objet contenant cette chaîne, indépendamment des autres valeurs de l’objet.  Le magasin de certificats peut être spécifié par les options Nom_magasin_certificats - et - Emplacement_magasin_certificats. |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Élément HashAlgorithm Impossible | Algorithme de hachage à utiliser pour signer le package. La valeur par défaut est SHA256. |
| Help | Affiche l’aide de la commande. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| OutputDirectory | Spécifie le répertoire dans lequel le package signé doit être enregistré. Par défaut, le package d’origine est remplacé par le package signé. |
| Overwrite | Commutateur pour indiquer si la signature actuelle doit être remplacée. Par défaut, la commande échoue si le package a déjà une signature. |
| Timestamper | URL vers un serveur d’horodatage RFC 3161. |
| TimestampHashAlgorithm | Algorithme de hachage à utiliser par le serveur d’horodatage RFC 3161. La valeur par défaut est SHA256. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

## <a name="examples"></a>Exemples

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```