---
title: Commande de vérification de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622601"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="1d135-103">Verify, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="1d135-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="1d135-104">**S’applique à :** &bullet; **versions prises en charge par** la consommation des packages : 4.6 +</span><span class="sxs-lookup"><span data-stu-id="1d135-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="1d135-105">Vérifie un package.</span><span class="sxs-lookup"><span data-stu-id="1d135-105">Verifies a package.</span></span>

<span data-ttu-id="1d135-106">La vérification des packages signés n’est pas encore prise en charge dans .NET Core, sous mono ou sur des plateformes non-Windows.</span><span class="sxs-lookup"><span data-stu-id="1d135-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="1d135-107">Usage</span><span class="sxs-lookup"><span data-stu-id="1d135-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="1d135-108">où `<package(s)>` se trouve un ou plusieurs `.nupkg` fichiers.</span><span class="sxs-lookup"><span data-stu-id="1d135-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="1d135-109">contrôle NuGet-tout</span><span class="sxs-lookup"><span data-stu-id="1d135-109">nuget verify -All</span></span>

<span data-ttu-id="1d135-110">Spécifie que toutes les vérifications possibles doivent être effectuées sur le ou les packages.</span><span class="sxs-lookup"><span data-stu-id="1d135-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="1d135-111">contrôle NuGet-signatures</span><span class="sxs-lookup"><span data-stu-id="1d135-111">nuget verify -Signatures</span></span>

<span data-ttu-id="1d135-112">Spécifie que la vérification de la signature du package doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="1d135-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="1d135-113">Options pour « Verify-signatures »</span><span class="sxs-lookup"><span data-stu-id="1d135-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="1d135-114">Spécifie un ou plusieurs empreintes de certificat SHA-256 de certificats dont les packages signés doivent être signés.</span><span class="sxs-lookup"><span data-stu-id="1d135-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="1d135-115">Une empreinte de certificat SHA-256 est un hachage SHA-256 du certificat.</span><span class="sxs-lookup"><span data-stu-id="1d135-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="1d135-116">Les entrées multiples doivent être séparées par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="1d135-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="1d135-117">Options</span><span class="sxs-lookup"><span data-stu-id="1d135-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="1d135-118">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="1d135-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1d135-119">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="1d135-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="1d135-120">Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="1d135-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="1d135-121">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="1d135-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="1d135-122">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1d135-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="1d135-123">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="1d135-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="1d135-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="1d135-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```