---
title: Packages signés
description: Configuration requise pour la signature du package NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 992097281e21cd8cf37edf67fb1968b70c2b359b
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020511"
---
# <a name="signed-packages"></a><span data-ttu-id="d8879-103">Packages signés</span><span class="sxs-lookup"><span data-stu-id="d8879-103">Signed packages</span></span>

<span data-ttu-id="d8879-104">*4.6.0+ de NuGet et Visual Studio 2017 version 15.6 et versions ultérieure*</span><span class="sxs-lookup"><span data-stu-id="d8879-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="d8879-105">Les packages NuGet peuvent inclure une signature numérique qui fournit une protection contre le contenu falsifiée.</span><span class="sxs-lookup"><span data-stu-id="d8879-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="d8879-106">Cette signature est générée à partir d’un certificat X.509 qui ajoute également des preuves d’authenticité à l’origine réelle du package.</span><span class="sxs-lookup"><span data-stu-id="d8879-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="d8879-107">Les packages signés fournissent la validation de bout en bout plus forte.</span><span class="sxs-lookup"><span data-stu-id="d8879-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="d8879-108">Il existe deux types de signatures de NuGet :</span><span class="sxs-lookup"><span data-stu-id="d8879-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="d8879-109">**Créer la Signature**.</span><span class="sxs-lookup"><span data-stu-id="d8879-109">**Author Signature**.</span></span> <span data-ttu-id="d8879-110">Une signature de l’auteur garantit que le package n’a pas été modifié depuis l’auteur a signé le package, non quel que soit à partir de laquelle le dépôt ou ce que le package est remis de méthode de transport.</span><span class="sxs-lookup"><span data-stu-id="d8879-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="d8879-111">En outre, les packages signés par auteur fournissent un mécanisme d’authentification supplémentaire au pipeline de publication nuget.org, car le certificat de signature doit être inscrit à l’avance.</span><span class="sxs-lookup"><span data-stu-id="d8879-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="d8879-112">Pour plus d’informations, consultez [enregistrer des certificats](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="d8879-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="d8879-113">**Signature de référentiel**.</span><span class="sxs-lookup"><span data-stu-id="d8879-113">**Repository Signature**.</span></span> <span data-ttu-id="d8879-114">Les signatures de référentiel offrent la garantie d’intégrité pour **tous les** dans un référentiel de packages qu’ils soient auteur signé ou non, même si ces packages sont obtenues à partir d’un emplacement autre que le dépôt d’origine où ils se trouvaient signé.</span><span class="sxs-lookup"><span data-stu-id="d8879-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="d8879-115">Pour plus d’informations sur la création d’un package signé auteur, consultez [signature de Packages](../create-packages/Sign-a-package.md) et [commande de connexion nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="d8879-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="d8879-116">La signature du package est actuellement pris en charge uniquement à l’aide de nuget.exe sur Windows.</span><span class="sxs-lookup"><span data-stu-id="d8879-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="d8879-117">Vérification des packages signés est actuellement pris en charge uniquement lorsque vous utilisez nuget.exe ou Visual Studio sur Windows.</span><span class="sxs-lookup"><span data-stu-id="d8879-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="d8879-118">Conditions de certificat</span><span class="sxs-lookup"><span data-stu-id="d8879-118">Certificate requirements</span></span>

<span data-ttu-id="d8879-119">La signature du package nécessite un code de signature de certificat, qui est un type spécial de certificat est valide pour le `id-kp-codeSigning` usage [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="d8879-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="d8879-120">En outre, le certificat doit avoir une publique longueur de clé RSA de 2 048 bits ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d8879-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="d8879-121">Obtenir un certificat de signature de code</span><span class="sxs-lookup"><span data-stu-id="d8879-121">Get a code signing certificate</span></span>

<span data-ttu-id="d8879-122">Certificats valides peuvent être obtenus à partir d’une autorité de certification publique, comme :</span><span class="sxs-lookup"><span data-stu-id="d8879-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="d8879-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="d8879-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="d8879-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="d8879-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="d8879-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="d8879-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="d8879-126">Connexion globale</span><span class="sxs-lookup"><span data-stu-id="d8879-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="d8879-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="d8879-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="d8879-128">Certum</span><span class="sxs-lookup"><span data-stu-id="d8879-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="d8879-129">La liste complète des autorités de certification approuvées par Windows peut être obtenue à partir de [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="d8879-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="d8879-130">Créer un certificat de test</span><span class="sxs-lookup"><span data-stu-id="d8879-130">Create a test certificate</span></span>

<span data-ttu-id="d8879-131">Vous pouvez utiliser les certificats auto-émis à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="d8879-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="d8879-132">Pour créer un certificat auto-émis, utilisez le [commande New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="d8879-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="d8879-133">Cette commande crée un certificat de test disponible dans le magasin de certificats personnel de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="d8879-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="d8879-134">Vous pouvez ouvrir le magasin de certificats en exécutant `certmgr.msc` pour afficher le certificat nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="d8879-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="d8879-135">NuGet.org n’accepte pas les packages signés avec les certificats auto-émis.</span><span class="sxs-lookup"><span data-stu-id="d8879-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="d8879-136">Configuration requise d’horodatage</span><span class="sxs-lookup"><span data-stu-id="d8879-136">Timestamp requirements</span></span>

<span data-ttu-id="d8879-137">Packages signés doivent inclure un horodatage RFC 3161 pour garantir la validité de signature au-delà de la période de validité du certificat de signature du package.</span><span class="sxs-lookup"><span data-stu-id="d8879-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="d8879-138">Le certificat utilisé pour signer l’horodateur doit être valide pour le `id-kp-timeStamping` usage [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="d8879-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="d8879-139">En outre, le certificat doit avoir une publique longueur de clé RSA de 2 048 bits ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d8879-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="d8879-140">Vous trouverez des informations techniques dans le [les spécifications techniques de signature du package](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="d8879-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="d8879-141">Exigences de signature sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="d8879-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="d8879-142">NuGet.org a des exigences supplémentaires pour l’acceptation d’un package signé :</span><span class="sxs-lookup"><span data-stu-id="d8879-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="d8879-143">La signature principale doit être une signature de l’auteur.</span><span class="sxs-lookup"><span data-stu-id="d8879-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="d8879-144">La signature principale doit avoir un seul horodateur valid.</span><span class="sxs-lookup"><span data-stu-id="d8879-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="d8879-145">Les certificats X.509 pour la signature de l’auteur et sa signature d’horodatage :</span><span class="sxs-lookup"><span data-stu-id="d8879-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="d8879-146">Doit avoir une clé publique de RSA 2 048 bits ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="d8879-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="d8879-147">Doit être au sein de sa période de validité par heure UTC actuelle au moment de la validation du package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d8879-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="d8879-148">Doit être lié à une autorité racine approuvée qui est approuvée par défaut sur Windows.</span><span class="sxs-lookup"><span data-stu-id="d8879-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="d8879-149">Les packages signés avec les certificats auto-émis sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="d8879-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="d8879-150">Doit être valide pour sa fonction :</span><span class="sxs-lookup"><span data-stu-id="d8879-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="d8879-151">L’auteur du certificat de signature doit être valide pour la signature de code.</span><span class="sxs-lookup"><span data-stu-id="d8879-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="d8879-152">Le certificat d’horodatage doit être valide pour le service d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="d8879-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="d8879-153">Il ne doit pas être révoqué à l’heure de signature.</span><span class="sxs-lookup"><span data-stu-id="d8879-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="d8879-154">(Cela ne peut pas être qui peuvent être connue au moment de l’envoi, donc nuget.org vérifie périodiquement l’état de révocation).</span><span class="sxs-lookup"><span data-stu-id="d8879-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="d8879-155">Inscrire le certificat sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="d8879-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="d8879-156">Pour envoyer un package signé, vous devez tout d’abord inscrire le certificat auprès de nuget.org. Vous avez besoin du certificat en tant qu’un `.cer` fichier dans un format DER binaire.</span><span class="sxs-lookup"><span data-stu-id="d8879-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="d8879-157">Vous pouvez exporter un certificat existant dans un format DER binaire à l’aide de l’Assistant Exportation de certificat.</span><span class="sxs-lookup"><span data-stu-id="d8879-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Assistant Exportation de certificat](media/CertificateExportWizard.png)

<span data-ttu-id="d8879-159">Les utilisateurs expérimentés peuvent exporter le certificat à l’aide de la [commande Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="d8879-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="d8879-160">Pour demander le certificat auprès de nuget.org, accédez à `Certificates` section `Account settings` page (ou page de paramètres de l’organisation) et sélectionnez `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="d8879-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certificats inscrits](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="d8879-162">Un utilisateur peut soumettre que plusieurs certificats et le même certificat peuvent être inscrit par plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d8879-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="d8879-163">Une fois qu’un utilisateur a un certificat enregistré, toutes les soumissions ultérieures du package **doit** être signé avec un des certificats.</span><span class="sxs-lookup"><span data-stu-id="d8879-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="d8879-164">Les utilisateurs peuvent également supprimer un certificat enregistré à partir du compte.</span><span class="sxs-lookup"><span data-stu-id="d8879-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="d8879-165">Une fois qu’un certificat est supprimé, les packages signés avec ce certificat échouent au dépôt.</span><span class="sxs-lookup"><span data-stu-id="d8879-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="d8879-166">Les packages existants ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="d8879-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="d8879-167">Configurer les exigences de signature du package</span><span class="sxs-lookup"><span data-stu-id="d8879-167">Configure package signing requirements</span></span>

<span data-ttu-id="d8879-168">Si vous êtes l’unique propriétaire d’un package, vous êtes le signataire requis.</span><span class="sxs-lookup"><span data-stu-id="d8879-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="d8879-169">Autrement dit, vous pouvez utiliser un des certificats inscrits pour signer vos packages et soumettre sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d8879-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="d8879-170">Si un package contient plusieurs propriétaires, par défaut, les certificats du propriétaire de la « Any » peuvent être utilisés pour signer le package.</span><span class="sxs-lookup"><span data-stu-id="d8879-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="d8879-171">En tant que copropriétaire du package, vous pouvez remplacer « Tout » avec vous-même ou n’importe quel autre copropriétaire pour être le signataire requis.</span><span class="sxs-lookup"><span data-stu-id="d8879-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="d8879-172">Si vous apportez un propriétaire qui ne dispose pas de n’importe quel certificat inscrit, puis packages non signés pourront.</span><span class="sxs-lookup"><span data-stu-id="d8879-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="d8879-173">De même, si la valeur par défaut « Tout » est sélectionnée pour un package où un seul propriétaire a un certificat enregistré et un autre propriétaire n’a pas de n’importe quel certificat inscrit, puis nuget.org accepte un package signé avec une signature inscrite par un de ses propriétaires ou non signée (étant donné qu’un des propriétaires n’a pas de n’importe quel certificat enregistré) du package.</span><span class="sxs-lookup"><span data-stu-id="d8879-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Configurer des signataires de package](media/configure-package-signers.png)
