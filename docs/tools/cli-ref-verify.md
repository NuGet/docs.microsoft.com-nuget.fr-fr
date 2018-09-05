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
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="4e114-103">verify (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4e114-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="4e114-104">**S’applique à :** la consommation de package &bullet; **versions prises en charge :** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="4e114-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="4e114-105">Vérifie un package.</span><span class="sxs-lookup"><span data-stu-id="4e114-105">Verifies a package.</span></span>

<span data-ttu-id="4e114-106">Vérification des packages signés n’est pas encore pris en charge dans .NET Core, sous Mono, ou sur des plateformes non Windows.</span><span class="sxs-lookup"><span data-stu-id="4e114-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="4e114-107">Utilisation</span><span class="sxs-lookup"><span data-stu-id="4e114-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="4e114-108">où `<package(s)>` comporte un ou plusieurs `.nupkg` fichiers.</span><span class="sxs-lookup"><span data-stu-id="4e114-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="4e114-109">vérifier NuGet - tout</span><span class="sxs-lookup"><span data-stu-id="4e114-109">nuget verify -All</span></span>

<span data-ttu-id="4e114-110">Spécifie que toutes les vérifications possibles doivent être effectuées sur l’ou les packages.</span><span class="sxs-lookup"><span data-stu-id="4e114-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="4e114-111">vérification de NuGet - Signatures</span><span class="sxs-lookup"><span data-stu-id="4e114-111">nuget verify -Signatures</span></span>

<span data-ttu-id="4e114-112">Spécifie que la vérification de signature de package doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="4e114-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="4e114-113">Options pour « vérifier - Signatures »</span><span class="sxs-lookup"><span data-stu-id="4e114-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="4e114-114">Option</span><span class="sxs-lookup"><span data-stu-id="4e114-114">Option</span></span> | <span data-ttu-id="4e114-115">Description</span><span class="sxs-lookup"><span data-stu-id="4e114-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e114-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="4e114-116">CertificateFingerprint</span></span> | <span data-ttu-id="4e114-117">Spécifie un ou plusieurs empreintes de certificat SHA-256 de quels packages signés doivent être signés avec des certificats (s).</span><span class="sxs-lookup"><span data-stu-id="4e114-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="4e114-118">Une empreinte de certificat SHA-256 est un hachage SHA-256 du certificat.</span><span class="sxs-lookup"><span data-stu-id="4e114-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="4e114-119">Plusieurs entrées doivent être séparées par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="4e114-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="4e114-120">Options</span><span class="sxs-lookup"><span data-stu-id="4e114-120">Options</span></span>

| <span data-ttu-id="4e114-121">Option</span><span class="sxs-lookup"><span data-stu-id="4e114-121">Option</span></span> | <span data-ttu-id="4e114-122">Description</span><span class="sxs-lookup"><span data-stu-id="4e114-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e114-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4e114-123">ConfigFile</span></span> | <span data-ttu-id="4e114-124">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="4e114-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4e114-125">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="4e114-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4e114-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4e114-126">ForceEnglishOutput</span></span> | <span data-ttu-id="4e114-127">Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="4e114-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4e114-128">Help</span><span class="sxs-lookup"><span data-stu-id="4e114-128">Help</span></span> | <span data-ttu-id="4e114-129">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="4e114-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="4e114-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="4e114-130">Verbosity</span></span> | <span data-ttu-id="4e114-131">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="4e114-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="4e114-132">Exemples</span><span class="sxs-lookup"><span data-stu-id="4e114-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```