---
title: Commande des signataires approuvés de l’interface CLI NuGet
description: Informations de référence sur la commande NuGet. exe Trusted-Signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327536"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="f1b61-103">commande des signataires approuvés (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="f1b61-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="f1b61-104">**S’applique à:** &bullet; **versions prises en charge par** la consommation des packages: 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="f1b61-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="f1b61-105">Obtient ou définit des signataires approuvés pour la configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1b61-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="f1b61-106">Pour une utilisation supplémentaire, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f1b61-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="f1b61-107">Pour plus d’informations sur l’apparence du schéma NuGet. config, reportez-vous à la [Référence du fichier de configuration NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="f1b61-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f1b61-108">Usage</span><span class="sxs-lookup"><span data-stu-id="f1b61-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="f1b61-109">Si aucun de `list|add|remove|sync` n’est spécifié, la commande prend `list`par défaut la valeur.</span><span class="sxs-lookup"><span data-stu-id="f1b61-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="f1b61-110">Liste des signataires approuvés NuGet</span><span class="sxs-lookup"><span data-stu-id="f1b61-110">nuget trusted-signers list</span></span>

<span data-ttu-id="f1b61-111">Répertorie tous les signataires approuvés dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="f1b61-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="f1b61-112">Cette option inclut tous les certificats (avec l’algorithme d’empreinte digitale et l’algorithme d’empreinte digitale) de chaque signataire.</span><span class="sxs-lookup"><span data-stu-id="f1b61-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="f1b61-113">Si un certificat est précédé `[U]`d’un, cela signifie que l’entrée du certificat a `allowUntrustedRoot` la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="f1b61-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="f1b61-114">Voici un exemple de sortie de cette commande:</span><span class="sxs-lookup"><span data-stu-id="f1b61-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="f1b61-115">les signataires approuvés NuGet Add [options]</span><span class="sxs-lookup"><span data-stu-id="f1b61-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="f1b61-116">Ajoute un signataire approuvé portant le nom donné à la configuration. Cette option a des gestes différents pour ajouter un auteur ou un dépôt approuvé.</span><span class="sxs-lookup"><span data-stu-id="f1b61-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="f1b61-117">Options d’ajout basés sur un package</span><span class="sxs-lookup"><span data-stu-id="f1b61-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="f1b61-118">où `<package(s)>` se trouve un ou `.nupkg` plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="f1b61-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="f1b61-119">Option</span><span class="sxs-lookup"><span data-stu-id="f1b61-119">Option</span></span> | <span data-ttu-id="f1b61-120">Description</span><span class="sxs-lookup"><span data-stu-id="f1b61-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1b61-121">Auteur</span><span class="sxs-lookup"><span data-stu-id="f1b61-121">Author</span></span> | <span data-ttu-id="f1b61-122">Spécifie que la signature de l’auteur du ou des packages doit être approuvée.</span><span class="sxs-lookup"><span data-stu-id="f1b61-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="f1b61-123">Référentiel</span><span class="sxs-lookup"><span data-stu-id="f1b61-123">Repository</span></span> | <span data-ttu-id="f1b61-124">Spécifie que la signature du référentiel ou la contre-signature du ou des packages doit être approuvée.</span><span class="sxs-lookup"><span data-stu-id="f1b61-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="f1b61-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="f1b61-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="f1b61-126">Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée.</span><span class="sxs-lookup"><span data-stu-id="f1b61-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="f1b61-127">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="f1b61-127">Owners</span></span> | <span data-ttu-id="f1b61-128">Liste de propriétaires approuvés séparés par des points-virgules pour restreindre davantage l’approbation d’un référentiel.</span><span class="sxs-lookup"><span data-stu-id="f1b61-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="f1b61-129">Valide uniquement lors de l' `-Repository` utilisation de l’option.</span><span class="sxs-lookup"><span data-stu-id="f1b61-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="f1b61-130">Le fait de `-Repository` fournir à la fois etenmêmetempsn’estpasprisencharge.`-Author`</span><span class="sxs-lookup"><span data-stu-id="f1b61-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="f1b61-131">Options d’ajout basés sur un index de service</span><span class="sxs-lookup"><span data-stu-id="f1b61-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="f1b61-132">_Remarque_: Cette option permet d’ajouter uniquement des référentiels approuvés.</span><span class="sxs-lookup"><span data-stu-id="f1b61-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="f1b61-133">Option</span><span class="sxs-lookup"><span data-stu-id="f1b61-133">Option</span></span> | <span data-ttu-id="f1b61-134">Description</span><span class="sxs-lookup"><span data-stu-id="f1b61-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1b61-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="f1b61-135">ServiceIndex</span></span> | <span data-ttu-id="f1b61-136">Spécifie l’index de service v3 du référentiel à approuver.</span><span class="sxs-lookup"><span data-stu-id="f1b61-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="f1b61-137">Ce dépôt doit prendre en charge la ressource de signatures de référentiel.</span><span class="sxs-lookup"><span data-stu-id="f1b61-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="f1b61-138">S’il n’est pas fourni, la commande recherche une source de package avec `-Name` le même et obtient l’index de service à partir de là.</span><span class="sxs-lookup"><span data-stu-id="f1b61-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="f1b61-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="f1b61-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="f1b61-140">Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée.</span><span class="sxs-lookup"><span data-stu-id="f1b61-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="f1b61-141">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="f1b61-141">Owners</span></span> | <span data-ttu-id="f1b61-142">Liste de propriétaires approuvés séparés par des points-virgules pour restreindre davantage l’approbation d’un référentiel.</span><span class="sxs-lookup"><span data-stu-id="f1b61-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="f1b61-143">Options d’ajout en fonction des informations de certificat</span><span class="sxs-lookup"><span data-stu-id="f1b61-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="f1b61-144">_Remarque_: Si un signataire approuvé portant le même nom existe déjà, l’élément de certificat est ajouté à ce signataire.</span><span class="sxs-lookup"><span data-stu-id="f1b61-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="f1b61-145">Dans le cas contraire, un auteur approuvé sera créé avec un élément de certificat à partir des informations de certificat données.</span><span class="sxs-lookup"><span data-stu-id="f1b61-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="f1b61-146">Option</span><span class="sxs-lookup"><span data-stu-id="f1b61-146">Option</span></span> | <span data-ttu-id="f1b61-147">Description</span><span class="sxs-lookup"><span data-stu-id="f1b61-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1b61-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="f1b61-148">CertificateFingerprint</span></span> | <span data-ttu-id="f1b61-149">Spécifie les empreintes de certificat d’un certificat avec lequel les packages signés doivent être signés.</span><span class="sxs-lookup"><span data-stu-id="f1b61-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="f1b61-150">Une empreinte de certificat est un hachage du certificat.</span><span class="sxs-lookup"><span data-stu-id="f1b61-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="f1b61-151">L’algorithme de hachage utilisé pour le calcul de ce hachage doit `FingerprintAlgorithm` être défini dans l’option.</span><span class="sxs-lookup"><span data-stu-id="f1b61-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="f1b61-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="f1b61-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="f1b61-153">Spécifie l’algorithme de hachage utilisé pour calculer l’empreinte digitale du certificat.</span><span class="sxs-lookup"><span data-stu-id="f1b61-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="f1b61-154">La valeur par défaut est `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="f1b61-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="f1b61-155">Les valeurs prises `SHA256`en `SHA384` charge sont, et`SHA512`</span><span class="sxs-lookup"><span data-stu-id="f1b61-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="f1b61-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="f1b61-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="f1b61-157">Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée.</span><span class="sxs-lookup"><span data-stu-id="f1b61-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="f1b61-158">suppression des signataires approuvés NuGet-nom<name></span><span class="sxs-lookup"><span data-stu-id="f1b61-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="f1b61-159">Supprime tous les signataires approuvés qui correspondent au nom donné.</span><span class="sxs-lookup"><span data-stu-id="f1b61-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="f1b61-160">Nom de synchronisation des signataires approuvés NuGet<name></span><span class="sxs-lookup"><span data-stu-id="f1b61-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="f1b61-161">Demande la liste la plus récente des certificats utilisés dans un référentiel actuellement approuvé pour mettre à jour la liste des certificats existants dans le signataire approuvé.</span><span class="sxs-lookup"><span data-stu-id="f1b61-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="f1b61-162">_Remarque_: Ce geste supprimera la liste actuelle des certificats et les remplacera par une liste à jour du référentiel.</span><span class="sxs-lookup"><span data-stu-id="f1b61-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="f1b61-163">Options</span><span class="sxs-lookup"><span data-stu-id="f1b61-163">Options</span></span>

| <span data-ttu-id="f1b61-164">Option</span><span class="sxs-lookup"><span data-stu-id="f1b61-164">Option</span></span> | <span data-ttu-id="f1b61-165">Description</span><span class="sxs-lookup"><span data-stu-id="f1b61-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1b61-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f1b61-166">ConfigFile</span></span> | <span data-ttu-id="f1b61-167">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="f1b61-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f1b61-168">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="f1b61-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f1b61-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f1b61-169">ForceEnglishOutput</span></span> | <span data-ttu-id="f1b61-170">Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais.</span><span class="sxs-lookup"><span data-stu-id="f1b61-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f1b61-171">Aide</span><span class="sxs-lookup"><span data-stu-id="f1b61-171">Help</span></span> | <span data-ttu-id="f1b61-172">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="f1b61-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="f1b61-173">Commentaires</span><span class="sxs-lookup"><span data-stu-id="f1b61-173">Verbosity</span></span> | <span data-ttu-id="f1b61-174">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="f1b61-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="f1b61-175">Exemples</span><span class="sxs-lookup"><span data-stu-id="f1b61-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
