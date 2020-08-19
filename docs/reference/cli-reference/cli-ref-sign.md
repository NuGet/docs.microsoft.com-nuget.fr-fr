---
title: Commande de signature de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622770"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="b17f3-103">Sign, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="b17f3-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="b17f3-104">**S’applique à :** &bullet; **versions prises en charge** pour la création de package : 4.6 +</span><span class="sxs-lookup"><span data-stu-id="b17f3-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="b17f3-105">Signe tous les packages correspondant au premier argument avec un certificat.</span><span class="sxs-lookup"><span data-stu-id="b17f3-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="b17f3-106">Le certificat avec la clé privée peut être obtenu à partir d’un fichier ou d’un certificat installé dans un magasin de certificats en fournissant un nom d’objet ou une empreinte numérique.</span><span class="sxs-lookup"><span data-stu-id="b17f3-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="b17f3-107">La signature du package n’est pas encore prise en charge dans .NET Core, sous mono ou sur des plateformes non-Windows.</span><span class="sxs-lookup"><span data-stu-id="b17f3-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="b17f3-108">Usage</span><span class="sxs-lookup"><span data-stu-id="b17f3-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="b17f3-109">où `<package(s)>` se trouve un ou plusieurs `.nupkg` fichiers.</span><span class="sxs-lookup"><span data-stu-id="b17f3-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="b17f3-110">Options</span><span class="sxs-lookup"><span data-stu-id="b17f3-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="b17f3-111">Spécifie l’empreinte SHA-1 du certificat utilisé pour rechercher le certificat dans un magasin de certificats local.</span><span class="sxs-lookup"><span data-stu-id="b17f3-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="b17f3-112">Spécifie le mot de passe du certificat, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b17f3-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="b17f3-113">Si un certificat est protégé par un mot de passe mais qu’aucun mot de passe n’est fourni, la commande vous invite à entrer un mot de passe au moment de l’exécution, sauf si l' `-NonInteractive` option est passée.</span><span class="sxs-lookup"><span data-stu-id="b17f3-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="b17f3-114">Spécifie le chemin d’accès au certificat à utiliser pour signer le package.</span><span class="sxs-lookup"><span data-stu-id="b17f3-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="b17f3-115">Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat.</span><span class="sxs-lookup"><span data-stu-id="b17f3-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="b17f3-116">La valeur par défaut est « CurrentUser », le magasin de certificats X. 509 utilisé par l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="b17f3-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="b17f3-117">Cette option doit être utilisée lors de la spécification du certificat via les `-CertificateSubjectName` `-CertificateFingerprint` options ou.</span><span class="sxs-lookup"><span data-stu-id="b17f3-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="b17f3-118">Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat.</span><span class="sxs-lookup"><span data-stu-id="b17f3-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="b17f3-119">La valeur par défaut est « My », le magasin de certificats X. 509 pour les certificats personnels.</span><span class="sxs-lookup"><span data-stu-id="b17f3-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="b17f3-120">Cette option doit être utilisée lors de la spécification du certificat via les `-CertificateSubjectName` `-CertificateFingerprint` options ou.</span><span class="sxs-lookup"><span data-stu-id="b17f3-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="b17f3-121">Spécifie le nom du sujet du certificat utilisé pour rechercher le certificat dans un magasin de certificats local.</span><span class="sxs-lookup"><span data-stu-id="b17f3-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="b17f3-122">La recherche est une comparaison de chaînes ne respectant pas la casse à l’aide de la valeur fournie, qui recherchera tous les certificats dont le nom d’objet contient cette chaîne, indépendamment des autres valeurs d’objet.</span><span class="sxs-lookup"><span data-stu-id="b17f3-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="b17f3-123">Le magasin de certificats peut être spécifié par les `-CertificateStoreName` `-CertificateStoreLocation` options et.</span><span class="sxs-lookup"><span data-stu-id="b17f3-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b17f3-124">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="b17f3-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b17f3-125">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="b17f3-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b17f3-126">Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="b17f3-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="b17f3-127">Algorithme de hachage à utiliser pour signer le package.</span><span class="sxs-lookup"><span data-stu-id="b17f3-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="b17f3-128">La valeur par défaut est SHA256.</span><span class="sxs-lookup"><span data-stu-id="b17f3-128">Defaults to SHA256.</span></span> <span data-ttu-id="b17f3-129">Les valeurs possibles sont SHA256, SHA384 et SHA512.</span><span class="sxs-lookup"><span data-stu-id="b17f3-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b17f3-130">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="b17f3-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b17f3-131">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b17f3-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="b17f3-132">Spécifie le répertoire dans lequel le package signé doit être enregistré.</span><span class="sxs-lookup"><span data-stu-id="b17f3-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="b17f3-133">Par défaut, le package d’origine est remplacé par le package signé.</span><span class="sxs-lookup"><span data-stu-id="b17f3-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="b17f3-134">Basculez pour indiquer si la signature actuelle doit être remplacée.</span><span class="sxs-lookup"><span data-stu-id="b17f3-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="b17f3-135">Par défaut, la commande échoue si le package a déjà une signature.</span><span class="sxs-lookup"><span data-stu-id="b17f3-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="b17f3-136">URL vers un serveur d’horodatage RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="b17f3-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="b17f3-137">Algorithme de hachage à utiliser par le serveur d’horodatage RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="b17f3-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="b17f3-138">La valeur par défaut est SHA256.</span><span class="sxs-lookup"><span data-stu-id="b17f3-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b17f3-139">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="b17f3-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="b17f3-140">Exemples</span><span class="sxs-lookup"><span data-stu-id="b17f3-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
