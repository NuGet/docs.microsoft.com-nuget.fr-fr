---
title: Commande de signature de l’interface CLI NuGet
description: Référence pour la commande de signature NuGet. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327586"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="1f204-103">sign (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1f204-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="1f204-104">**S’applique à:** &bullet; **versions prises en charge** pour la création de package: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="1f204-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="1f204-105">Signe tous les packages correspondant au premier argument avec un certificat.</span><span class="sxs-lookup"><span data-stu-id="1f204-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="1f204-106">Le certificat avec la clé privée peut être obtenu à partir d’un fichier ou d’un certificat installé dans un magasin de certificats en fournissant un nom d’objet ou une empreinte numérique.</span><span class="sxs-lookup"><span data-stu-id="1f204-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="1f204-107">La signature du package n’est pas encore prise en charge dans .NET Core, sous mono ou sur des plateformes non-Windows.</span><span class="sxs-lookup"><span data-stu-id="1f204-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="1f204-108">Usage</span><span class="sxs-lookup"><span data-stu-id="1f204-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="1f204-109">où `<package(s)>` se trouve un ou `.nupkg` plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="1f204-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="1f204-110">Options</span><span class="sxs-lookup"><span data-stu-id="1f204-110">Options</span></span>

| <span data-ttu-id="1f204-111">Option</span><span class="sxs-lookup"><span data-stu-id="1f204-111">Option</span></span> | <span data-ttu-id="1f204-112">Description</span><span class="sxs-lookup"><span data-stu-id="1f204-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1f204-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="1f204-113">CertificateFingerprint</span></span> | <span data-ttu-id="1f204-114">Spécifie l’empreinte SHA-1 du certificat utilisé pour rechercher le certificat dans un magasin de certificats local.</span><span class="sxs-lookup"><span data-stu-id="1f204-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="1f204-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="1f204-115">CertificatePassword</span></span> | <span data-ttu-id="1f204-116">Spécifie le mot de passe du certificat, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1f204-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="1f204-117">Si un certificat est protégé par un mot de passe mais qu’aucun mot de passe n’est fourni, la commande vous invite à entrer un mot de passe au moment de l’exécution, sauf si l’option-non interactive est passée.</span><span class="sxs-lookup"><span data-stu-id="1f204-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="1f204-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="1f204-118">CertificatePath</span></span> | <span data-ttu-id="1f204-119">Spécifie le chemin d’accès au certificat à utiliser pour signer le package.</span><span class="sxs-lookup"><span data-stu-id="1f204-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="1f204-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="1f204-120">CertificateStoreLocation</span></span> | <span data-ttu-id="1f204-121">Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat.</span><span class="sxs-lookup"><span data-stu-id="1f204-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="1f204-122">La valeur par défaut est «CurrentUser», le magasin de certificats X. 509 utilisé par l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="1f204-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="1f204-123">Cette option doit être utilisée lors de la spécification du certificat via les options-CertificateSubjectName ou-CertificateFingerprint.</span><span class="sxs-lookup"><span data-stu-id="1f204-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="1f204-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="1f204-124">CertificateStoreName</span></span> | <span data-ttu-id="1f204-125">Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat.</span><span class="sxs-lookup"><span data-stu-id="1f204-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="1f204-126">La valeur par défaut est «My», le magasin de certificats X. 509 pour les certificats personnels.</span><span class="sxs-lookup"><span data-stu-id="1f204-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="1f204-127">Cette option doit être utilisée lors de la spécification du certificat via les options-CertificateSubjectName ou-CertificateFingerprint.</span><span class="sxs-lookup"><span data-stu-id="1f204-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="1f204-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="1f204-128">CertificateSubjectName</span></span> | <span data-ttu-id="1f204-129">Spécifie le nom du sujet du certificat utilisé pour rechercher le certificat dans un magasin de certificats local.</span><span class="sxs-lookup"><span data-stu-id="1f204-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="1f204-130">La recherche est une comparaison de chaînes ne respectant pas la casse à l’aide de la valeur fournie, qui recherchera tous les certificats dont le nom d’objet contient cette chaîne, indépendamment des autres valeurs d’objet.</span><span class="sxs-lookup"><span data-stu-id="1f204-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="1f204-131">Le magasin de certificats peut être spécifié par les options-CertificateStoreName et-CertificateStoreLocation.</span><span class="sxs-lookup"><span data-stu-id="1f204-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="1f204-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1f204-132">ConfigFile</span></span> | <span data-ttu-id="1f204-133">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="1f204-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1f204-134">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="1f204-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1f204-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1f204-135">ForceEnglishOutput</span></span> | <span data-ttu-id="1f204-136">Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais.</span><span class="sxs-lookup"><span data-stu-id="1f204-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1f204-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="1f204-137">HashAlgorithm</span></span> | <span data-ttu-id="1f204-138">Algorithme de hachage à utiliser pour signer le package.</span><span class="sxs-lookup"><span data-stu-id="1f204-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="1f204-139">La valeur par défaut est SHA256.</span><span class="sxs-lookup"><span data-stu-id="1f204-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="1f204-140">Aide</span><span class="sxs-lookup"><span data-stu-id="1f204-140">Help</span></span> | <span data-ttu-id="1f204-141">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="1f204-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="1f204-142">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1f204-142">NonInteractive</span></span> | <span data-ttu-id="1f204-143">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1f204-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1f204-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="1f204-144">OutputDirectory</span></span> | <span data-ttu-id="1f204-145">Spécifie le répertoire dans lequel le package signé doit être enregistré.</span><span class="sxs-lookup"><span data-stu-id="1f204-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="1f204-146">Par défaut, le package d’origine est remplacé par le package signé.</span><span class="sxs-lookup"><span data-stu-id="1f204-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="1f204-147">Overwrite</span><span class="sxs-lookup"><span data-stu-id="1f204-147">Overwrite</span></span> | <span data-ttu-id="1f204-148">Basculez pour indiquer si la signature actuelle doit être remplacée.</span><span class="sxs-lookup"><span data-stu-id="1f204-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="1f204-149">Par défaut, la commande échoue si le package a déjà une signature.</span><span class="sxs-lookup"><span data-stu-id="1f204-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="1f204-150">Timestamper</span><span class="sxs-lookup"><span data-stu-id="1f204-150">Timestamper</span></span> | <span data-ttu-id="1f204-151">URL vers un serveur d’horodatage RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="1f204-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="1f204-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="1f204-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="1f204-153">Algorithme de hachage à utiliser par le serveur d’horodatage RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="1f204-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="1f204-154">La valeur par défaut est SHA256.</span><span class="sxs-lookup"><span data-stu-id="1f204-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="1f204-155">Commentaires</span><span class="sxs-lookup"><span data-stu-id="1f204-155">Verbosity</span></span> | <span data-ttu-id="1f204-156">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="1f204-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="1f204-157">Exemples</span><span class="sxs-lookup"><span data-stu-id="1f204-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```