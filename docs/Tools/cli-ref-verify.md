---
title: Vérifier la commande NuGet CLI | Documents Microsoft
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informations de référence pour le nuget.exe vérifier la commande
keywords: vérifier la référence de NuGet, vérifiez la commande
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4423e491e0ab5dc1e13982440db42bc9b0e85c38
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="verify-command-nuget-cli"></a>Vérifiez la commande (NuGet CLI)

**S’applique à :** package consommation &bullet; **versions prises en charge :** 4.6 +

Vérifie un package.

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