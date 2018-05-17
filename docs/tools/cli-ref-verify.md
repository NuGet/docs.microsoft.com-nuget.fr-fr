---
title: Vérifier la commande NuGet CLI
description: Informations de référence pour le nuget.exe vérifier la commande
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c2c31b71358bc50a1fb9aab8905c279cd1235b07
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2018
---
# <a name="verify-command-nuget-cli"></a>verify (commande, NuGet CLI)

**S’applique à :** package consommation &bullet; **versions prises en charge :** 4.6 +

Vérifie un package.

Vérification des packages signés n’est pas encore pris en charge dans .NET Core, sous Mono, ou sur les plateformes non Windows.

## <a name="usage"></a>Utilisation

```cli
nuget verify <package(s)> [options]
```

où `<package(s)>` est un ou plusieurs `.nupkg` fichiers.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| Tous | Spécifie que toutes les vérifications possibles doivent être effectuées sur l’ou les packages. |
| CertificateFingerprint | Spécifie un ou plusieurs des empreintes certificat SHA-256 de certificats (s), lesquelles packages signés doivent être signées avec. Une empreinte de certificat SHA-256 est un hachage SHA-256 du certificat. Plusieurs entrées doivent être séparées par des points-virgules. |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Signatures | Spécifie que la vérification des signatures de package doit être effectuée. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

## <a name="examples"></a>Exemples

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```