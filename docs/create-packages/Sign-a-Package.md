---
title: Signature de packages NuGet
description: Explique comment utiliser des packages signés pour vérifier l’intégrité du contenu.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429002"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="33042-103">Signature de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="33042-103">Signing NuGet Packages</span></span>

<span data-ttu-id="33042-104">Les packages signés permettent les contrôles de vérification de l’intégrité du contenu, qui offrent une protection contre la falsification de contenu.</span><span class="sxs-lookup"><span data-stu-id="33042-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="33042-105">La signature du package sert également de source unique de vérité sur l’origine réelle du package et renforce l’authenticité du package pour le consommateur.</span><span class="sxs-lookup"><span data-stu-id="33042-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="33042-106">Ce guide part du principe que vous avez déjà [créé un package](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="33042-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="33042-107">Obtenir un certificat de signature de code</span><span class="sxs-lookup"><span data-stu-id="33042-107">Get a code signing certificate</span></span>

<span data-ttu-id="33042-108">Des certificats valides peuvent être obtenus auprès d’une autorité de certification publique telle que [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [certr](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. La liste complète des autorités de certification approuvées par Windows peut être obtenue à partir de [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="33042-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="33042-109">Vous pouvez utiliser des certificats auto-émis à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="33042-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="33042-110">Toutefois, les packages signés à l’aide de certificats auto-émis ne sont pas acceptés par NuGet.org. En savoir plus sur [la création d’un certificat de test](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="33042-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="33042-111">Exporter le fichier de certificat</span><span class="sxs-lookup"><span data-stu-id="33042-111">Export the certificate file</span></span>

* <span data-ttu-id="33042-112">Vous pouvez exporter un certificat existant à un format DER binaire avec l’Assistant Exportation de certificat.</span><span class="sxs-lookup"><span data-stu-id="33042-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Assistant Exportation de certificat](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="33042-114">Vous pouvez également exporter le certificat avec la [commande PowerShell Export-Certificate](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="33042-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="33042-115">Signer le package</span><span class="sxs-lookup"><span data-stu-id="33042-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="33042-116">Requiert NuGet. exe 4.6.0 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="33042-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="33042-117">la prise en charge de dotnet. exe sera bientôt [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="33042-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="33042-118">Signez le package avec [nuget sign](../reference/cli-reference/cli-ref-sign.md) :</span><span class="sxs-lookup"><span data-stu-id="33042-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="33042-119">Le fournisseur de certificats fournit souvent l’URL d’un serveur d’horodatage que vous pouvez utiliser pour l’argument facultatif `Timestamper` indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="33042-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="33042-120">Consultez la documentation et/ou contactez le support de votre fournisseur pour obtenir cette URL de service.</span><span class="sxs-lookup"><span data-stu-id="33042-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="33042-121">Vous pouvez utiliser un certificat disponible dans le magasin de certificats ou utiliser un certificat provenant d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="33042-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="33042-122">Consultez les informations de référence sur CLI pour [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="33042-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="33042-123">Les packages signés doivent inclure un horodatage pour vérifier que la signature est valide après expiration du certificat de signature.</span><span class="sxs-lookup"><span data-stu-id="33042-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="33042-124">Sinon, l’opération de signature produit un [avertissement](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="33042-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="33042-125">Vous pouvez voir les détails de la signature d’un package donné avec [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="33042-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="33042-126">Inscrire le certificat sur NuGet.org</span><span class="sxs-lookup"><span data-stu-id="33042-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="33042-127">Pour publier un package signé, vous devez d’abord inscrire le certificat auprès de NuGet.org. Vous avez besoin du certificat en tant que fichier `.cer` dans un format DER binaire.</span><span class="sxs-lookup"><span data-stu-id="33042-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="33042-128">[Connectez-vous](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) à NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="33042-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="33042-129">Accédez à `Account settings` (ou `Manage Organization` **>** `Edit Organziation` si vous souhaitez inscrire le certificat auprès d’un compte d’organisation).</span><span class="sxs-lookup"><span data-stu-id="33042-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="33042-130">Développez la section `Certificates`, puis sélectionnez `Register new`.</span><span class="sxs-lookup"><span data-stu-id="33042-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="33042-131">Accédez au fichier de certificat qui a été exporté précédemment.</span><span class="sxs-lookup"><span data-stu-id="33042-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="33042-132">![Certificats inscrits](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="33042-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="33042-133">**Remarque**</span><span class="sxs-lookup"><span data-stu-id="33042-133">**Note**</span></span>
* <span data-ttu-id="33042-134">Un même utilisateur peut envoyer plusieurs certificats et le même certificat peut être inscrit par plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="33042-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="33042-135">Une fois qu’un utilisateur a un certificat inscrit, tous les envois de package ultérieurs **doivent** être signés avec un des certificats.</span><span class="sxs-lookup"><span data-stu-id="33042-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="33042-136">Consultez [Gérer les exigences de signature de votre package sur NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="33042-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="33042-137">Les utilisateurs peuvent également supprimer du compte un certificat inscrit.</span><span class="sxs-lookup"><span data-stu-id="33042-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="33042-138">Une fois qu’un certificat est supprimé, l’envoi de nouveaux packages signés avec ce certificat échoue.</span><span class="sxs-lookup"><span data-stu-id="33042-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="33042-139">Les packages existants ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="33042-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="33042-140">Publier le package</span><span class="sxs-lookup"><span data-stu-id="33042-140">Publish the package</span></span>

<span data-ttu-id="33042-141">Vous êtes maintenant prêt à publier le package sur NuGet.org. Consultez [publication de packages](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="33042-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="33042-142">Créer un certificat de test</span><span class="sxs-lookup"><span data-stu-id="33042-142">Create a test certificate</span></span>

<span data-ttu-id="33042-143">Vous pouvez utiliser des certificats auto-émis à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="33042-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="33042-144">Pour créer un certificat auto-émis, utilisez la [commande PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="33042-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="33042-145">Cette commande crée un certificat de test disponible dans le magasin de certificats personnel de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="33042-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="33042-146">Vous pouvez ouvrir le magasin de certificats en exécutant `certmgr.msc` pour voir le certificat nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="33042-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="33042-147">NuGet.org n’accepte pas les packages signés avec des certificats auto-émis.</span><span class="sxs-lookup"><span data-stu-id="33042-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="33042-148">Gérer les exigences de signature de votre package sur NuGet.org</span><span class="sxs-lookup"><span data-stu-id="33042-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="33042-149">[Connectez-vous](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) à NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="33042-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="33042-150">Accédez à `Manage Packages` 
   ![Configurer des signataires de package](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="33042-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="33042-151">Si vous êtes l’unique propriétaire d’un package, vous êtes le signataire requis : vous pouvez utiliser un des certificats inscrits pour signer et publier vos packages sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="33042-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="33042-152">Si un package a plusieurs propriétaires, par défaut, les certificats du propriétaire « N’importe lequel » peuvent être utilisés pour signer le package.</span><span class="sxs-lookup"><span data-stu-id="33042-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="33042-153">En tant que copropriétaire du package, vous pouvez remplacer « N’importe lequel » par vous-même ou par n’importe quel autre copropriétaire pour en faire le signataire obligatoire.</span><span class="sxs-lookup"><span data-stu-id="33042-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="33042-154">Si vous déclarez un propriétaire qui n’a aucun certificat inscrit, les packages non signés sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="33042-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="33042-155">De même, si l’option par défaut « N’importe lequel » est sélectionnée pour un package où un propriétaire a un certificat inscrit et où un autre propriétaire n’a aucun certificat inscrit, NuGet.org accepte un package signé avec une signature inscrite par un de ses propriétaires ou un package non signé (un des propriétaires n’ayant aucun certificat inscrit).</span><span class="sxs-lookup"><span data-stu-id="33042-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="33042-156">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="33042-156">Related articles</span></span>

- [<span data-ttu-id="33042-157">Gérer les limites d’approbation de package</span><span class="sxs-lookup"><span data-stu-id="33042-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="33042-158">Informations de référence sur les packages signés</span><span class="sxs-lookup"><span data-stu-id="33042-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
