---
title: Commande des signataires approuvés de l’interface CLI NuGet
description: Référence pour la commande nuget.exe des signataires approuvés
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323588"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="a90fa-103">commande des signataires approuvés (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="a90fa-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="a90fa-104">**S’applique à :** &bullet; **versions prises en charge par** la consommation de packages : 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="a90fa-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="a90fa-105">Obtient ou définit des signataires approuvés pour la configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="a90fa-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="a90fa-106">Pour une utilisation supplémentaire, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a90fa-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="a90fa-107">Pour plus d’informations sur l’apparence du schéma nuget.config, consultez la [Référence du fichier de configuration NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="a90fa-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a90fa-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="a90fa-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="a90fa-109">Si aucun de `list|add|remove|sync` n’est spécifié, la commande prend par défaut la valeur `list` .</span><span class="sxs-lookup"><span data-stu-id="a90fa-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="a90fa-110">Liste des signataires approuvés NuGet</span><span class="sxs-lookup"><span data-stu-id="a90fa-110">nuget trusted-signers list</span></span>

<span data-ttu-id="a90fa-111">Répertorie tous les signataires approuvés dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="a90fa-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="a90fa-112">Cette option inclut tous les certificats (avec l’algorithme d’empreinte digitale et l’algorithme d’empreinte digitale) de chaque signataire.</span><span class="sxs-lookup"><span data-stu-id="a90fa-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="a90fa-113">Si un certificat est précédé d’un `[U]` , cela signifie que l’entrée du certificat a la `allowUntrustedRoot` valeur `true` .</span><span class="sxs-lookup"><span data-stu-id="a90fa-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="a90fa-114">Voici un exemple de sortie de cette commande :</span><span class="sxs-lookup"><span data-stu-id="a90fa-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="a90fa-115">les signataires approuvés NuGet Add [options]</span><span class="sxs-lookup"><span data-stu-id="a90fa-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="a90fa-116">Ajoute un signataire approuvé portant le nom donné à la configuration. Cette option a des gestes différents pour ajouter un auteur ou un dépôt approuvé.</span><span class="sxs-lookup"><span data-stu-id="a90fa-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="a90fa-117">Options d’ajout basés sur un package</span><span class="sxs-lookup"><span data-stu-id="a90fa-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

<span data-ttu-id="a90fa-118">où `<package>` est un `.nupkg` fichier signé.</span><span class="sxs-lookup"><span data-stu-id="a90fa-118">where `<package>` is one signed `.nupkg` file.</span></span>

- **`-Author`**

  <span data-ttu-id="a90fa-119">Spécifie que la signature de l’auteur du package signé doit être approuvée.</span><span class="sxs-lookup"><span data-stu-id="a90fa-119">Specifies that the author signature of the signed package should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="a90fa-120">Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée.</span><span class="sxs-lookup"><span data-stu-id="a90fa-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="a90fa-121">Liste de propriétaires approuvés séparés par des points-virgules pour restreindre davantage l’approbation d’un référentiel.</span><span class="sxs-lookup"><span data-stu-id="a90fa-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="a90fa-122">Valide uniquement lors de l’utilisation de l' `-Repository` option.</span><span class="sxs-lookup"><span data-stu-id="a90fa-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="a90fa-123">Spécifie que la signature de référentiel ou la contre-signature du package signé doit être approuvée.</span><span class="sxs-lookup"><span data-stu-id="a90fa-123">Specifies that the repository signature or countersignature of the signed package should be trusted.</span></span>

<span data-ttu-id="a90fa-124">`-Author` `-Repository` Le fait de fournir à la fois et en même temps n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a90fa-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="a90fa-125">Options d’ajout basés sur un index de service</span><span class="sxs-lookup"><span data-stu-id="a90fa-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="a90fa-126">_Remarque_: cette option ajoute uniquement des référentiels approuvés.</span><span class="sxs-lookup"><span data-stu-id="a90fa-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="a90fa-127">Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée.</span><span class="sxs-lookup"><span data-stu-id="a90fa-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="a90fa-128">Liste de propriétaires approuvés séparés par des points-virgules pour restreindre davantage l’approbation d’un référentiel.</span><span class="sxs-lookup"><span data-stu-id="a90fa-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="a90fa-129">Spécifie l’index de service v3 du référentiel à approuver.</span><span class="sxs-lookup"><span data-stu-id="a90fa-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="a90fa-130">Ce dépôt doit prendre en charge la ressource de signatures de référentiel.</span><span class="sxs-lookup"><span data-stu-id="a90fa-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="a90fa-131">S’il n’est pas fourni, la commande recherche une source de package avec le même `-Name` et obtient l’index de service à partir de là.</span><span class="sxs-lookup"><span data-stu-id="a90fa-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="a90fa-132">Options d’ajout en fonction des informations de certificat</span><span class="sxs-lookup"><span data-stu-id="a90fa-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="a90fa-133">_Remarque_: si un signataire approuvé portant le même nom existe déjà, l’élément de certificat sera ajouté à ce signataire.</span><span class="sxs-lookup"><span data-stu-id="a90fa-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="a90fa-134">Dans le cas contraire, un auteur approuvé sera créé avec un élément de certificat à partir des informations de certificat données.</span><span class="sxs-lookup"><span data-stu-id="a90fa-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="a90fa-135">Spécifie si le certificat du signataire approuvé doit être autorisé à se lier à une racine non approuvée.</span><span class="sxs-lookup"><span data-stu-id="a90fa-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="a90fa-136">Spécifie les empreintes de certificat d’un certificat avec lequel les packages signés doivent être signés.</span><span class="sxs-lookup"><span data-stu-id="a90fa-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="a90fa-137">Une empreinte de certificat est un hachage du certificat.</span><span class="sxs-lookup"><span data-stu-id="a90fa-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="a90fa-138">L’algorithme de hachage utilisé pour le calcul de ce hachage doit être défini dans l' `FingerprintAlgorithm` option.</span><span class="sxs-lookup"><span data-stu-id="a90fa-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="a90fa-139">Spécifie l’algorithme de hachage utilisé pour calculer l’empreinte digitale du certificat.</span><span class="sxs-lookup"><span data-stu-id="a90fa-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="a90fa-140">La valeur par défaut est `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="a90fa-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="a90fa-141">Les valeurs prises en charge sont `SHA256` , `SHA384` et `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="a90fa-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="a90fa-142">suppression des signataires approuvés NuGet-nom \<name\></span><span class="sxs-lookup"><span data-stu-id="a90fa-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="a90fa-143">Supprime tous les signataires approuvés qui correspondent au nom donné.</span><span class="sxs-lookup"><span data-stu-id="a90fa-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="a90fa-144">Nom de synchronisation des signataires approuvés NuGet \<name\></span><span class="sxs-lookup"><span data-stu-id="a90fa-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="a90fa-145">Demande la liste la plus récente des certificats utilisés dans un référentiel actuellement approuvé pour mettre à jour la liste des certificats existants dans le signataire approuvé.</span><span class="sxs-lookup"><span data-stu-id="a90fa-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="a90fa-146">_Remarque_: ce geste supprimera la liste actuelle des certificats et les remplacera par une liste à jour du référentiel.</span><span class="sxs-lookup"><span data-stu-id="a90fa-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="a90fa-147">Options</span><span class="sxs-lookup"><span data-stu-id="a90fa-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a90fa-148">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="a90fa-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a90fa-149">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a90fa-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a90fa-150">Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="a90fa-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a90fa-151">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="a90fa-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="a90fa-152">Nom du signataire approuvé.</span><span class="sxs-lookup"><span data-stu-id="a90fa-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a90fa-153">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a90fa-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a90fa-154">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a90fa-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="a90fa-155">Exemples</span><span class="sxs-lookup"><span data-stu-id="a90fa-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
