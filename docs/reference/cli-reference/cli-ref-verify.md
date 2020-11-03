---
title: Commande de vérification de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238138"
---
# <a name="verify-command-nuget-cli"></a>Verify, commande (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge par** la consommation des packages : 4.6 +

Vérifie un package.

La vérification des packages signés n’est pas encore prise en charge sous mono.

## <a name="usage"></a>Utilisation

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

où `<package(s)>` se trouve un ou plusieurs `.nupkg` fichiers.

## <a name="nuget-verify--all"></a>contrôle NuGet-tout

Spécifie que toutes les vérifications possibles doivent être effectuées sur le ou les packages.

## <a name="nuget-verify--signatures"></a>contrôle NuGet-signatures

Spécifie que la vérification de la signature du package doit être effectuée.

## <a name="options-for-verify--signatures"></a>Options pour « Verify-signatures »

- **`-CertificateFingerprint`**

  Spécifie un ou plusieurs empreintes de certificat SHA-256 de certificats dont les packages signés doivent être signés. Une empreinte de certificat SHA-256 est un hachage SHA-256 du certificat. Les entrées multiples doivent être séparées par des points-virgules.

## <a name="options"></a>Options

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

## <a name="examples"></a>Exemples

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```