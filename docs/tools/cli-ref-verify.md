---
title: Vérifier la commande CLI NuGet
description: Référence pour nuget.exe vérifier la commande
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545211"
---
# <a name="verify-command-nuget-cli"></a>verify (commande, NuGet CLI)

**S’applique à :** la consommation de package &bullet; **versions prises en charge :** 4.6 +

Vérifie un package.

Vérification des packages signés n’est pas encore pris en charge dans .NET Core, sous Mono, ou sur des plateformes non Windows.

## <a name="usage"></a>Utilisation

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

où `<package(s)>` comporte un ou plusieurs `.nupkg` fichiers.

## <a name="nuget-verify--all"></a>vérifier NuGet - tout

Spécifie que toutes les vérifications possibles doivent être effectuées sur l’ou les packages.

## <a name="nuget-verify--signatures"></a>vérification de NuGet - Signatures

Spécifie que la vérification de signature de package doit être effectuée.

## <a name="options-for-verify--signatures"></a>Options pour « vérifier - Signatures »

| Option | Description |
| --- | --- |
| CertificateFingerprint | Spécifie un ou plusieurs empreintes de certificat SHA-256 de quels packages signés doivent être signés avec des certificats (s). Une empreinte de certificat SHA-256 est un hachage SHA-256 du certificat. Plusieurs entrées doivent être séparées par des points-virgules. |

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

## <a name="examples"></a>Exemples

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```