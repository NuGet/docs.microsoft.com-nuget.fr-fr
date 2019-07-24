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
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="88939-103">verify (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="88939-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="88939-104">**S’applique à:** &bullet; **versions prises en charge par** la consommation des packages: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="88939-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="88939-105">Vérifie un package.</span><span class="sxs-lookup"><span data-stu-id="88939-105">Verifies a package.</span></span>

<span data-ttu-id="88939-106">La vérification des packages signés n’est pas encore prise en charge dans .NET Core, sous mono ou sur des plateformes non-Windows.</span><span class="sxs-lookup"><span data-stu-id="88939-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="88939-107">Usage</span><span class="sxs-lookup"><span data-stu-id="88939-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="88939-108">où `<package(s)>` se trouve un ou `.nupkg` plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="88939-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="88939-109">contrôle NuGet-tout</span><span class="sxs-lookup"><span data-stu-id="88939-109">nuget verify -All</span></span>

<span data-ttu-id="88939-110">Spécifie que toutes les vérifications possibles doivent être effectuées sur le ou les packages.</span><span class="sxs-lookup"><span data-stu-id="88939-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="88939-111">contrôle NuGet-signatures</span><span class="sxs-lookup"><span data-stu-id="88939-111">nuget verify -Signatures</span></span>

<span data-ttu-id="88939-112">Spécifie que la vérification de la signature du package doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="88939-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="88939-113">Options pour «Verify-signatures»</span><span class="sxs-lookup"><span data-stu-id="88939-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="88939-114">Option</span><span class="sxs-lookup"><span data-stu-id="88939-114">Option</span></span> | <span data-ttu-id="88939-115">Description</span><span class="sxs-lookup"><span data-stu-id="88939-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88939-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="88939-116">CertificateFingerprint</span></span> | <span data-ttu-id="88939-117">Spécifie un ou plusieurs empreintes de certificat SHA-256 de certificats dont les packages signés doivent être signés.</span><span class="sxs-lookup"><span data-stu-id="88939-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="88939-118">Une empreinte de certificat SHA-256 est un hachage SHA-256 du certificat.</span><span class="sxs-lookup"><span data-stu-id="88939-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="88939-119">Les entrées multiples doivent être séparées par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="88939-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="88939-120">Options</span><span class="sxs-lookup"><span data-stu-id="88939-120">Options</span></span>

| <span data-ttu-id="88939-121">Option</span><span class="sxs-lookup"><span data-stu-id="88939-121">Option</span></span> | <span data-ttu-id="88939-122">Description</span><span class="sxs-lookup"><span data-stu-id="88939-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88939-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="88939-123">ConfigFile</span></span> | <span data-ttu-id="88939-124">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="88939-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="88939-125">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="88939-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="88939-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="88939-126">ForceEnglishOutput</span></span> | <span data-ttu-id="88939-127">Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais.</span><span class="sxs-lookup"><span data-stu-id="88939-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="88939-128">Aide</span><span class="sxs-lookup"><span data-stu-id="88939-128">Help</span></span> | <span data-ttu-id="88939-129">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="88939-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="88939-130">Commentaires</span><span class="sxs-lookup"><span data-stu-id="88939-130">Verbosity</span></span> | <span data-ttu-id="88939-131">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="88939-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="88939-132">Exemples</span><span class="sxs-lookup"><span data-stu-id="88939-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```