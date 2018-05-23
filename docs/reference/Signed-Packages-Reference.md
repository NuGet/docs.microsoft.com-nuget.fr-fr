---
title: Packages signés
description: Configuration requise pour la signature du package NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a><span data-ttu-id="47966-103">Packages signés</span><span class="sxs-lookup"><span data-stu-id="47966-103">Signed packages</span></span>

<span data-ttu-id="47966-104">*NuGet 4.6.0+ et Visual Studio 2017 15,6 et versions ultérieures*</span><span class="sxs-lookup"><span data-stu-id="47966-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="47966-105">Les packages NuGet peuvent inclure une signature numérique qui assure la protection de contenu falsifié.</span><span class="sxs-lookup"><span data-stu-id="47966-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="47966-106">Cette signature est générée à partir d’un certificat X.509 qui ajoute également des preuves d’authenticité à l’origine réelle du package.</span><span class="sxs-lookup"><span data-stu-id="47966-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="47966-107">Les packages signés fournissent la validation de bout en bout pour les plus fortes.</span><span class="sxs-lookup"><span data-stu-id="47966-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="47966-108">Une signature de l’auteur garantit que le package n’a pas été modifié depuis l’auteur de signature du package, sans quel que soit à partir de laquelle référentiel ou que le package est remis (méthode) de transport.</span><span class="sxs-lookup"><span data-stu-id="47966-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="47966-109">En outre, signées par l’auteur de packages fournissent un mécanisme d’authentification supplémentaire pour le pipeline de publication nuget.org car le certificat de signature doit être enregistré à l’avance.</span><span class="sxs-lookup"><span data-stu-id="47966-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="47966-110">Pour plus d’informations, consultez [enregistrer des certificats](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="47966-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="47966-111">Pour plus d’informations sur la création d’un package signé, consultez [de signature de Packages](../create-packages/Sign-a-package.md) et [commande de connexion nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="47966-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="47966-112">La signature du package est actuellement pris en charge uniquement sur Windows à l’aide de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="47966-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="47966-113">Vérification des packages signés est actuellement pris en charge uniquement sur Windows à l’aide de nuget.exe ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47966-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="47966-114">Conditions de certificat</span><span class="sxs-lookup"><span data-stu-id="47966-114">Certificate requirements</span></span>

<span data-ttu-id="47966-115">La signature du package nécessite un code de signature de certificat, qui est un type particulier de certificat valide pour le `id-kp-codeSigning` objectif [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="47966-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="47966-116">En outre, le certificat doit avoir une publique longueur de clé RSA ou plus de 2 048 bits.</span><span class="sxs-lookup"><span data-stu-id="47966-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="47966-117">Obtenir un certificat de signature de code</span><span class="sxs-lookup"><span data-stu-id="47966-117">Get a code signing certificate</span></span>

<span data-ttu-id="47966-118">Certificats valides peuvent être obtenues à partir d’une autorité de certification publique comme :</span><span class="sxs-lookup"><span data-stu-id="47966-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="47966-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="47966-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="47966-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="47966-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="47966-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="47966-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="47966-122">Signe global</span><span class="sxs-lookup"><span data-stu-id="47966-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="47966-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="47966-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="47966-124">Certum</span><span class="sxs-lookup"><span data-stu-id="47966-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="47966-125">La liste complète des autorités de certification approuvées par Windows peut être obtenue à partir de [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="47966-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="47966-126">Créer un certificat de test</span><span class="sxs-lookup"><span data-stu-id="47966-126">Create a test certificate</span></span>

<span data-ttu-id="47966-127">Vous pouvez utiliser les certificats auto-émis à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="47966-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="47966-128">Pour créer un certificat auto-émis, utilisez le [commande New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="47966-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="47966-129">Cette commande crée un certificat de test disponible dans le magasin de certificats personnel de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="47966-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="47966-130">Vous pouvez ouvrir le magasin de certificats en exécutant `certmgr.msc` pour afficher le certificat nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="47966-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="47966-131">NuGet.org n’accepte pas les packages signés avec les certificats auto-émis.</span><span class="sxs-lookup"><span data-stu-id="47966-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="47966-132">Configuration requise d’horodatage</span><span class="sxs-lookup"><span data-stu-id="47966-132">Timestamp requirements</span></span>

<span data-ttu-id="47966-133">Les packages signés doivent inclure un horodatage RFC 3161 pour garantir la validité de signature au-delà de la période de validité du certificat de signature de packages.</span><span class="sxs-lookup"><span data-stu-id="47966-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="47966-134">Le certificat utilisé pour signer l’horodateur doit être valide pour le `id-kp-timeStamping` objectif [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="47966-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="47966-135">En outre, le certificat doit avoir une publique longueur de clé RSA ou plus de 2 048 bits.</span><span class="sxs-lookup"><span data-stu-id="47966-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="47966-136">Vous trouverez des informations techniques dans le [les spécifications techniques de signature du package](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="47966-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="47966-137">Spécifications de signature sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="47966-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="47966-138">NuGet.org a des exigences supplémentaires pour l’acceptation d’un package signé :</span><span class="sxs-lookup"><span data-stu-id="47966-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="47966-139">La signature principale doit être une signature de l’auteur.</span><span class="sxs-lookup"><span data-stu-id="47966-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="47966-140">La signature principale doit avoir un seul horodateur valid.</span><span class="sxs-lookup"><span data-stu-id="47966-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="47966-141">Les certificats X.509 pour la signature de l’auteur et sa signature horodateur :</span><span class="sxs-lookup"><span data-stu-id="47966-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="47966-142">Doit avoir une clé publique de RSA 2 048 bits ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="47966-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="47966-143">Doit être dans sa période de validité par heure UTC actuelle au moment de la validation du package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="47966-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="47966-144">Doit être chaîné à une autorité racine approuvée qui est approuvée par défaut sur Windows.</span><span class="sxs-lookup"><span data-stu-id="47966-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="47966-145">Les packages signés avec les certificats auto-émis sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="47966-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="47966-146">Doit être valide pour son objectif :</span><span class="sxs-lookup"><span data-stu-id="47966-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="47966-147">L’auteur du certificat de signature doit être valide pour la signature de code.</span><span class="sxs-lookup"><span data-stu-id="47966-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="47966-148">Le certificat de l’horodatage doit être valide pour le service d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="47966-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="47966-149">Ne doit pas être révoqué à l’heure de signature.</span><span class="sxs-lookup"><span data-stu-id="47966-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="47966-150">(Il ne peut pas être qui peuvent être connue au moment de l’envoi, donc nuget.org vérifie périodiquement l’état de révocation).</span><span class="sxs-lookup"><span data-stu-id="47966-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="47966-151">Enregistrer un certificat sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="47966-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="47966-152">Pour envoyer un package signé, vous devez d’abord inscrire le certificat dans nuget.org. Vous devez installer le certificat en tant qu’un `.cer` fichier dans un format DER binaire.</span><span class="sxs-lookup"><span data-stu-id="47966-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="47966-153">Vous pouvez exporter un certificat existant dans un format DER binaire à l’aide de l’Assistant Exportation de certificat.</span><span class="sxs-lookup"><span data-stu-id="47966-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Assistant Exportation de certificat](media/CertificateExportWizard.png)

<span data-ttu-id="47966-155">Les utilisateurs expérimentés peuvent exporter le certificat à l’aide de la [commande PowerShell de certificat d’exportation](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="47966-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="47966-156">Pour inscrire le certificat avec nuget.org, accédez à `Certificates` section `Account settings` page (ou page de paramètres de l’organisation) et sélectionnez `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="47966-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certificats inscrits](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="47966-158">Un utilisateur peut soumettre que plusieurs certificats et le même certificat peuvent être inscrit par plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="47966-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="47966-159">Une fois qu’un utilisateur a un certificat enregistré, toutes les soumissions futures **doit** être signées avec un des certificats.</span><span class="sxs-lookup"><span data-stu-id="47966-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="47966-160">Les utilisateurs peuvent également supprimer un certificat enregistré à partir du compte.</span><span class="sxs-lookup"><span data-stu-id="47966-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="47966-161">Une fois qu’un certificat est supprimé, les packages signés avec ce certificat échouent au dépôt.</span><span class="sxs-lookup"><span data-stu-id="47966-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="47966-162">Les packages existants ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="47966-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="47966-163">Configurer les exigences de signature de packages</span><span class="sxs-lookup"><span data-stu-id="47966-163">Configure package signing requirements</span></span>

<span data-ttu-id="47966-164">Si vous êtes l’unique propriétaire d’un package, vous êtes le signataire obligatoire.</span><span class="sxs-lookup"><span data-stu-id="47966-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="47966-165">Autrement dit, vous pouvez utiliser un des certificats inscrits pour signer vos packages et les soumettre à nuget.org.</span><span class="sxs-lookup"><span data-stu-id="47966-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="47966-166">Si un package contient plusieurs propriétaires, par défaut, les certificats du « Tout » propriétaire peuvent être utilisés pour signer le package.</span><span class="sxs-lookup"><span data-stu-id="47966-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="47966-167">En tant que copropriétaire du package, vous pouvez remplacer « Tout » avec vous-même ou n’importe quel autre copropriétaire soit le signataire obligatoire.</span><span class="sxs-lookup"><span data-stu-id="47966-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="47966-168">Si vous effectuez un propriétaire qui ne dispose pas de n’importe quel certificat inscrit, puis packages non signés seront autorisés.</span><span class="sxs-lookup"><span data-stu-id="47966-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="47966-169">De même, si la valeur par défaut est « Any » sélectionnée pour un package dans lequel un seul propriétaire a un certificat inscrit et un autre propriétaire n’a pas de n’importe quel certificat inscrit, puis nuget.org accepte un package signé avec une signature inscrite par un de ses propriétaires ou non signée (étant donné qu’un des propriétaires n’a pas de n’importe quel certificat enregistré) du package.</span><span class="sxs-lookup"><span data-stu-id="47966-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Configurer signataires de package](media/configure-package-signers.png)
