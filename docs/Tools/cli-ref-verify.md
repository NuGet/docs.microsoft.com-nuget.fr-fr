---
title: "Vérifier la commande NuGet CLI | Documents Microsoft"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informations de référence pour le nuget.exe vérifier la commande"
keywords: "vérifier la référence de NuGet, vérifiez la commande"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 096c79670267d9b602dd6ad30640e832441c31c5
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="3020c-104">Vérifiez la commande (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3020c-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="3020c-105">**S’applique à :** package consommation &bullet; **versions prises en charge :** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="3020c-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="3020c-106">Vérifie un package.</span><span class="sxs-lookup"><span data-stu-id="3020c-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="3020c-107">Utilisation</span><span class="sxs-lookup"><span data-stu-id="3020c-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="3020c-108">où `<package(s)>` est un ou plusieurs `.nupkg` fichiers.</span><span class="sxs-lookup"><span data-stu-id="3020c-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="3020c-109">Options</span><span class="sxs-lookup"><span data-stu-id="3020c-109">Options</span></span>

| <span data-ttu-id="3020c-110">Option</span><span class="sxs-lookup"><span data-stu-id="3020c-110">Option</span></span> | <span data-ttu-id="3020c-111">Description</span><span class="sxs-lookup"><span data-stu-id="3020c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3020c-112">Tous</span><span class="sxs-lookup"><span data-stu-id="3020c-112">All</span></span> | <span data-ttu-id="3020c-113">Spécifie que toutes les vérifications possibles doivent être effectuées sur l’ou les packages.</span><span class="sxs-lookup"><span data-stu-id="3020c-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="3020c-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="3020c-114">CertificateFingerprint</span></span> | <span data-ttu-id="3020c-115">Spécifie un ou plusieurs des empreintes certificat SHA-256 de certificats (s), lesquelles packages signés doivent être signées avec.</span><span class="sxs-lookup"><span data-stu-id="3020c-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="3020c-116">Une empreinte de certificat SHA-256 est un hachage SHA-256 du certificat.</span><span class="sxs-lookup"><span data-stu-id="3020c-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="3020c-117">Plusieurs entrées doivent être séparées par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="3020c-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="3020c-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3020c-118">ConfigFile</span></span> | <span data-ttu-id="3020c-119">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="3020c-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3020c-120">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="3020c-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3020c-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3020c-121">ForceEnglishOutput</span></span> | <span data-ttu-id="3020c-122">Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="3020c-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3020c-123">Help</span><span class="sxs-lookup"><span data-stu-id="3020c-123">Help</span></span> | <span data-ttu-id="3020c-124">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="3020c-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="3020c-125">Non interactif</span><span class="sxs-lookup"><span data-stu-id="3020c-125">NonInteractive</span></span> | <span data-ttu-id="3020c-126">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="3020c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3020c-127">Signatures</span><span class="sxs-lookup"><span data-stu-id="3020c-127">Signatures</span></span> | <span data-ttu-id="3020c-128">Spécifie que la vérification des signatures de package doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="3020c-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="3020c-129">Commentaires</span><span class="sxs-lookup"><span data-stu-id="3020c-129">Verbosity</span></span> | <span data-ttu-id="3020c-130">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="3020c-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="3020c-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="3020c-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```