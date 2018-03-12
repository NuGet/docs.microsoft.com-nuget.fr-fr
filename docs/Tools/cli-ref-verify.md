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
ms.openlocfilehash: 2747491eb35d8685a44e86fcc1b572013982c754
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="a3269-104">Vérifiez la commande (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a3269-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="a3269-105">**S’applique à :** package consommation &bullet; **versions prises en charge :** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="a3269-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="a3269-106">Vérifie un package.</span><span class="sxs-lookup"><span data-stu-id="a3269-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="a3269-107">Utilisation</span><span class="sxs-lookup"><span data-stu-id="a3269-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="a3269-108">où `<package(s)>` est un ou plusieurs `.nupkg` fichiers.</span><span class="sxs-lookup"><span data-stu-id="a3269-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="a3269-109">Options</span><span class="sxs-lookup"><span data-stu-id="a3269-109">Options</span></span>

| <span data-ttu-id="a3269-110">Option</span><span class="sxs-lookup"><span data-stu-id="a3269-110">Option</span></span> | <span data-ttu-id="a3269-111">Description</span><span class="sxs-lookup"><span data-stu-id="a3269-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3269-112">Tous</span><span class="sxs-lookup"><span data-stu-id="a3269-112">All</span></span> | <span data-ttu-id="a3269-113">Spécifie que toutes les vérifications possibles doivent être effectuées sur l’ou les packages.</span><span class="sxs-lookup"><span data-stu-id="a3269-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="a3269-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="a3269-114">CertificateFingerprint</span></span> | <span data-ttu-id="a3269-115">Spécifie un ou plusieurs des empreintes certificat SHA-256 de certificats (s), lesquelles packages signés doivent être signées avec.</span><span class="sxs-lookup"><span data-stu-id="a3269-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="a3269-116">Une empreinte de certificat SHA-256 est un hachage SHA-256 du certificat.</span><span class="sxs-lookup"><span data-stu-id="a3269-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="a3269-117">Plusieurs entrées doivent être séparées par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="a3269-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="a3269-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a3269-118">ConfigFile</span></span> | <span data-ttu-id="a3269-119">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="a3269-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a3269-120">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a3269-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a3269-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a3269-121">ForceEnglishOutput</span></span> | <span data-ttu-id="a3269-122">Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="a3269-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a3269-123">Help</span><span class="sxs-lookup"><span data-stu-id="a3269-123">Help</span></span> | <span data-ttu-id="a3269-124">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="a3269-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="a3269-125">Non interactif</span><span class="sxs-lookup"><span data-stu-id="a3269-125">NonInteractive</span></span> | <span data-ttu-id="a3269-126">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="a3269-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a3269-127">Signatures</span><span class="sxs-lookup"><span data-stu-id="a3269-127">Signatures</span></span> | <span data-ttu-id="a3269-128">Spécifie que la vérification des signatures de package doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="a3269-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="a3269-129">Commentaires</span><span class="sxs-lookup"><span data-stu-id="a3269-129">Verbosity</span></span> | <span data-ttu-id="a3269-130">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="a3269-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="a3269-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="a3269-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```