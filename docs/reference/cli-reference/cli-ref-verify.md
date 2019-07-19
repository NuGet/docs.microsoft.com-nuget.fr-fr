---
title: Commande de vérification de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327496"
---
# <a name="verify-command-nuget-cli"></a>verify (commande, NuGet CLI)

**S’applique à:** &bullet; **versions prises en charge par** la consommation des packages: 4.6 +

Vérifie un package.

La vérification des packages signés n’est pas encore prise en charge dans .NET Core, sous mono ou sur des plateformes non-Windows.

## <a name="usage"></a>Usage

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

où `<package(s)>` se trouve un ou `.nupkg` plusieurs fichiers.

## <a name="nuget-verify--all"></a>contrôle NuGet-tout

Spécifie que toutes les vérifications possibles doivent être effectuées sur le ou les packages.

## <a name="nuget-verify--signatures"></a>contrôle NuGet-signatures

Spécifie que la vérification de la signature du package doit être effectuée.

## <a name="options-for-verify--signatures"></a>Options pour «Verify-signatures»

| Option | Description |
| --- | --- |
| CertificateFingerprint | Spécifie un ou plusieurs empreintes de certificat SHA-256 de certificats dont les packages signés doivent être signés. Une empreinte de certificat SHA-256 est un hachage SHA-256 du certificat. Les entrées multiples doivent être séparées par des points-virgules. |

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais. |
| Aide | Affiche des informations d’aide pour la commande. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

## <a name="examples"></a>Exemples

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```