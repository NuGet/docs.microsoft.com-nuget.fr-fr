---
title: Commande de signataires approuvé de CLI de NuGet
description: Référence de la commande signataires approuvé de nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324706"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="63086-103">commande signataires approuvé (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="63086-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="63086-104">**S’applique à :** la consommation de package &bullet; **versions prises en charge :** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="63086-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="63086-105">Obtient ou définit les signataires approuvés à la configuration de NuGet.</span><span class="sxs-lookup"><span data-stu-id="63086-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="63086-106">Pour une utilisation supplémentaire, consultez [configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="63086-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="63086-107">Pour plus d’informations sur la façon dont le schéma de nuget.config ressemble, reportez-vous à la [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="63086-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="63086-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="63086-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="63086-109">Si aucun des `list|add|remove|sync` est spécifié, la commande par défaut sera `list`.</span><span class="sxs-lookup"><span data-stu-id="63086-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="63086-110">liste des signataires approuvé de NuGet</span><span class="sxs-lookup"><span data-stu-id="63086-110">nuget trusted-signers list</span></span>

<span data-ttu-id="63086-111">Répertorie tous les signataires approuvés dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="63086-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="63086-112">Cette option permet d’inclure tous les certificats (avec empreintes digitales et algorithme d’empreinte digitale) a chaque signataire.</span><span class="sxs-lookup"><span data-stu-id="63086-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="63086-113">Si un certificat a précédente `[U]`, cela signifie qu’entrée de certificat a `allowUntrustedRoot` définir en tant que `true`.</span><span class="sxs-lookup"><span data-stu-id="63086-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="63086-114">Voici un exemple de sortie à partir de cette commande :</span><span class="sxs-lookup"><span data-stu-id="63086-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="63086-115">NuGet approuvé-signataires ajouter [options]</span><span class="sxs-lookup"><span data-stu-id="63086-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="63086-116">Ajoute un signataire approuvé avec le nom donné à la configuration. Cette option a des gestes différents pour ajouter un auteur approuvé ou un référentiel.</span><span class="sxs-lookup"><span data-stu-id="63086-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="63086-117">Options pour ajouter basé sur un package</span><span class="sxs-lookup"><span data-stu-id="63086-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="63086-118">où `<package(s)>` comporte un ou plusieurs `.nupkg` fichiers.</span><span class="sxs-lookup"><span data-stu-id="63086-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="63086-119">Option</span><span class="sxs-lookup"><span data-stu-id="63086-119">Option</span></span> | <span data-ttu-id="63086-120">Description</span><span class="sxs-lookup"><span data-stu-id="63086-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63086-121">Auteur</span><span class="sxs-lookup"><span data-stu-id="63086-121">Author</span></span> | <span data-ttu-id="63086-122">Spécifie que la signature de l’auteur du ou des modules doit être approuvée.</span><span class="sxs-lookup"><span data-stu-id="63086-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="63086-123">Référentiel</span><span class="sxs-lookup"><span data-stu-id="63086-123">Repository</span></span> | <span data-ttu-id="63086-124">Spécifie que la signature de référentiel ou d’une contre-signature du ou des modules doit être approuvé.</span><span class="sxs-lookup"><span data-stu-id="63086-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="63086-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="63086-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="63086-126">Spécifie si le certificat pour le signataire approuvé doit être autorisé à la chaîne à une racine non approuvée.</span><span class="sxs-lookup"><span data-stu-id="63086-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="63086-127">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="63086-127">Owners</span></span> | <span data-ttu-id="63086-128">Liste séparés par des points-virgules des propriétaires approuvés pour restreindre davantage l’approbation d’un référentiel.</span><span class="sxs-lookup"><span data-stu-id="63086-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="63086-129">Valide uniquement lorsque vous utilisez la `-Repository` option.</span><span class="sxs-lookup"><span data-stu-id="63086-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="63086-130">En fournissant les deux `-Author` et `-Repository` en même temps n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="63086-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="63086-131">Options pour ajouter basé sur un index de service</span><span class="sxs-lookup"><span data-stu-id="63086-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="63086-132">_Remarque_ : Cette option n’ajoute des référentiels approuvés.</span><span class="sxs-lookup"><span data-stu-id="63086-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="63086-133">Option</span><span class="sxs-lookup"><span data-stu-id="63086-133">Option</span></span> | <span data-ttu-id="63086-134">Description</span><span class="sxs-lookup"><span data-stu-id="63086-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63086-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="63086-135">ServiceIndex</span></span> | <span data-ttu-id="63086-136">Spécifie l’index de service V3 du référentiel d’être approuvés.</span><span class="sxs-lookup"><span data-stu-id="63086-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="63086-137">Ce dépôt a prendre en charge de la ressource de signatures du référentiel.</span><span class="sxs-lookup"><span data-stu-id="63086-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="63086-138">Si n’est fourni, la commande recherchera une source de package avec le même `-Name` et obtenir l’index de service à partir de là.</span><span class="sxs-lookup"><span data-stu-id="63086-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="63086-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="63086-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="63086-140">Spécifie si le certificat pour le signataire approuvé doit être autorisé à la chaîne à une racine non approuvée.</span><span class="sxs-lookup"><span data-stu-id="63086-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="63086-141">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="63086-141">Owners</span></span> | <span data-ttu-id="63086-142">Liste séparés par des points-virgules des propriétaires approuvés pour restreindre davantage l’approbation d’un référentiel.</span><span class="sxs-lookup"><span data-stu-id="63086-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="63086-143">Options pour ajouter selon les informations de certificat</span><span class="sxs-lookup"><span data-stu-id="63086-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="63086-144">_Remarque_ : Si un signataire approuvé portant le nom spécifié existe déjà, l’élément de certificat est ajouté pour que le signataire.</span><span class="sxs-lookup"><span data-stu-id="63086-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="63086-145">Sinon, un auteur approuvé sera créé avec un élément de certificat à partir des informations de certificat spécifiées.</span><span class="sxs-lookup"><span data-stu-id="63086-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="63086-146">Option</span><span class="sxs-lookup"><span data-stu-id="63086-146">Option</span></span> | <span data-ttu-id="63086-147">Description</span><span class="sxs-lookup"><span data-stu-id="63086-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63086-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="63086-148">CertificateFingerprint</span></span> | <span data-ttu-id="63086-149">Spécifie un certificat empreintes d’un certificat qui packages signés doivent être signées avec.</span><span class="sxs-lookup"><span data-stu-id="63086-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="63086-150">Une empreinte de certificat est un hachage du certificat.</span><span class="sxs-lookup"><span data-stu-id="63086-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="63086-151">Spécifie l’algorithme de hachage utilisé pour calculer ce hachage doit être le `FingerprintAlgorithm` option.</span><span class="sxs-lookup"><span data-stu-id="63086-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="63086-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="63086-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="63086-153">Spécifie l’algorithme de hachage utilisé pour calculer l’empreinte numérique du certificat.</span><span class="sxs-lookup"><span data-stu-id="63086-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="63086-154">La valeur par défaut est `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="63086-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="63086-155">Valeurs prises en charge sont `SHA256`, `SHA384` et `SHA512`</span><span class="sxs-lookup"><span data-stu-id="63086-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="63086-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="63086-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="63086-157">Spécifie si le certificat pour le signataire approuvé doit être autorisé à la chaîne à une racine non approuvée.</span><span class="sxs-lookup"><span data-stu-id="63086-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="63086-158">NuGet approuvé-signataires remove - nom <name></span><span class="sxs-lookup"><span data-stu-id="63086-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="63086-159">Supprime les signataires approuvés qui correspondent au nom donné.</span><span class="sxs-lookup"><span data-stu-id="63086-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="63086-160">NuGet approuvé-signataires synchroniser - nom <name></span><span class="sxs-lookup"><span data-stu-id="63086-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="63086-161">Demande la dernière liste des certificats utilisés dans un référentiel actuellement approuvé pour mettre à jour le la liste de certificats existants dans le signataire approuvé.</span><span class="sxs-lookup"><span data-stu-id="63086-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="63086-162">_Remarque_ : Ce mouvement supprime la liste actuelle des certificats et les remplacer par une liste à jour à partir du référentiel.</span><span class="sxs-lookup"><span data-stu-id="63086-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="63086-163">Options</span><span class="sxs-lookup"><span data-stu-id="63086-163">Options</span></span>

| <span data-ttu-id="63086-164">Option</span><span class="sxs-lookup"><span data-stu-id="63086-164">Option</span></span> | <span data-ttu-id="63086-165">Description</span><span class="sxs-lookup"><span data-stu-id="63086-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63086-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="63086-166">ConfigFile</span></span> | <span data-ttu-id="63086-167">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="63086-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="63086-168">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="63086-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="63086-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="63086-169">ForceEnglishOutput</span></span> | <span data-ttu-id="63086-170">Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="63086-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="63086-171">Help</span><span class="sxs-lookup"><span data-stu-id="63086-171">Help</span></span> | <span data-ttu-id="63086-172">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="63086-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="63086-173">Verbosity</span><span class="sxs-lookup"><span data-stu-id="63086-173">Verbosity</span></span> | <span data-ttu-id="63086-174">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="63086-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="63086-175">Exemples</span><span class="sxs-lookup"><span data-stu-id="63086-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
