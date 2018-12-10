---
title: Signature de packages NuGet
description: Explique comment utiliser des packages signés pour vérifier l’intégrité du contenu.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e8955f9d46bab235c8755d5654814a4291d542d6
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977561"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="f3f2f-103">Signature de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="f3f2f-103">Signing NuGet Packages</span></span>

<span data-ttu-id="f3f2f-104">Les packages signés permettent les contrôles de vérification de l’intégrité du contenu, qui offrent une protection contre la falsification de contenu.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="f3f2f-105">La signature du package sert également de source unique de vérité sur l’origine réelle du package et renforce l’authenticité du package pour le consommateur.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="f3f2f-106">Ce guide part du principe que vous avez déjà [créé un package](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="f3f2f-107">Obtenir un certificat de signature de code</span><span class="sxs-lookup"><span data-stu-id="f3f2f-107">Get a code signing certificate</span></span>

<span data-ttu-id="f3f2f-108">Vous pouvez obtenir des certificats valides auprès d’une autorité de certification publique, comme [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. Vous pouvez obtenir la liste complète des autorités de certification approuvées par Windows sur [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="f3f2f-109">Vous pouvez utiliser des certificats auto-émis à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="f3f2f-110">Cependant, les packages signés avec des certificats auto-émis ne sont pas acceptés par NuGet.org. Découvrez plus d’informations sur la [création d’un certificat de test](#create-a-test-certificate).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="f3f2f-111">Exporter le fichier de certificat</span><span class="sxs-lookup"><span data-stu-id="f3f2f-111">Export the certificate file</span></span>

* <span data-ttu-id="f3f2f-112">Vous pouvez exporter un certificat existant à un format DER binaire avec l’Assistant Exportation de certificat.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Assistant Exportation de certificat](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="f3f2f-114">Vous pouvez également exporter le certificat avec la [commande PowerShell Export-Certificate](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="f3f2f-115">Signer le package</span><span class="sxs-lookup"><span data-stu-id="f3f2f-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="f3f2f-116">Nécessite nuget.exe 4.6.0 ou ultérieur</span><span class="sxs-lookup"><span data-stu-id="f3f2f-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="f3f2f-117">Signez le package avec [nuget sign](../tools/cli-ref-sign.md) :</span><span class="sxs-lookup"><span data-stu-id="f3f2f-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* <span data-ttu-id="f3f2f-118">Vous pouvez utiliser un certificat disponible dans le magasin de certificats ou utiliser un certificat provenant d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-118">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="f3f2f-119">Consultez les informations de référence sur CLI pour [nuget sign](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-119">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="f3f2f-120">Les packages signés doivent inclure un horodatage pour vérifier que la signature est valide après expiration du certificat de signature.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="f3f2f-121">Sinon, l’opération de signature produit un [avertissement](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-121">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="f3f2f-122">Vous pouvez voir les détails de la signature d’un package donné avec [nuget verify](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-122">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="f3f2f-123">Inscrire le certificat sur NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f3f2f-123">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="f3f2f-124">Pour publier un package signé, vous devez d’abord inscrire le certificat auprès de NuGet.org. Vous avez besoin du certificat sous forme de fichier `.cer` au format DER binaire.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-124">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="f3f2f-125">[Connectez-vous](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) à NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-125">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="f3f2f-126">Accédez à `Account settings` (ou à `Manage Organization` **>** `Edit Organziation` si vous voulez inscrire le certificat auprès d’un compte d’organisation).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-126">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="f3f2f-127">Développez la section `Certificates`, puis sélectionnez `Register new`.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-127">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="f3f2f-128">Accédez au fichier de certificat qui a été exporté précédemment.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-128">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="f3f2f-129">![Certificats inscrits](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="f3f2f-129">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="f3f2f-130">**Remarque**</span><span class="sxs-lookup"><span data-stu-id="f3f2f-130">**Note**</span></span>
* <span data-ttu-id="f3f2f-131">Un même utilisateur peut envoyer plusieurs certificats et le même certificat peut être inscrit par plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-131">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="f3f2f-132">Une fois qu’un utilisateur a un certificat inscrit, tous les envois de package ultérieurs **doivent** être signés avec un des certificats.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-132">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="f3f2f-133">Consultez [Gérer les exigences de signature de votre package sur NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="f3f2f-133">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="f3f2f-134">Les utilisateurs peuvent également supprimer du compte un certificat inscrit.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-134">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="f3f2f-135">Une fois qu’un certificat est supprimé, l’envoi de nouveaux packages signés avec ce certificat échoue.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-135">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="f3f2f-136">Les packages existants ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-136">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="f3f2f-137">Publier le package</span><span class="sxs-lookup"><span data-stu-id="f3f2f-137">Publish the package</span></span>

<span data-ttu-id="f3f2f-138">Vous êtes maintenant prêt à publier le package sur NuGet.org. Consultez [Publication de packages](Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-138">You are now ready to publish the package to NuGet.org. See [Publishing packages](Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="f3f2f-139">Créer un certificat de test</span><span class="sxs-lookup"><span data-stu-id="f3f2f-139">Create a test certificate</span></span>

<span data-ttu-id="f3f2f-140">Vous pouvez utiliser des certificats auto-émis à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-140">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="f3f2f-141">Pour créer un certificat auto-émis, utilisez la [commande PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-141">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="f3f2f-142">Cette commande crée un certificat de test disponible dans le magasin de certificats personnel de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-142">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="f3f2f-143">Vous pouvez ouvrir le magasin de certificats en exécutant `certmgr.msc` pour voir le certificat nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-143">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="f3f2f-144">NuGet.org n’accepte pas les packages signés avec des certificats auto-émis.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-144">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="f3f2f-145">Gérer les exigences de signature de votre package sur NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f3f2f-145">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="f3f2f-146">[Connectez-vous](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) à NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-146">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="f3f2f-147">Accédez à `Manage Packages` 
   ![Configurer des signataires de package](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="f3f2f-147">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="f3f2f-148">Si vous êtes l’unique propriétaire d’un package, vous êtes le signataire requis : vous pouvez utiliser un des certificats inscrits pour signer et publier vos packages sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-148">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="f3f2f-149">Si un package a plusieurs propriétaires, par défaut, les certificats du propriétaire « N’importe lequel » peuvent être utilisés pour signer le package.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-149">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="f3f2f-150">En tant que copropriétaire du package, vous pouvez remplacer « N’importe lequel » par vous-même ou par n’importe quel autre copropriétaire pour en faire le signataire obligatoire.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-150">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="f3f2f-151">Si vous déclarez un propriétaire qui n’a aucun certificat inscrit, les packages non signés sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-151">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="f3f2f-152">De même, si l’option par défaut « N’importe lequel » est sélectionnée pour un package où un propriétaire a un certificat inscrit et où un autre propriétaire n’a aucun certificat inscrit, NuGet.org accepte un package signé avec une signature inscrite par un de ses propriétaires ou un package non signé (un des propriétaires n’ayant aucun certificat inscrit).</span><span class="sxs-lookup"><span data-stu-id="f3f2f-152">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="f3f2f-153">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="f3f2f-153">Related articles</span></span>

- [<span data-ttu-id="f3f2f-154">Installation de packages signés</span><span class="sxs-lookup"><span data-stu-id="f3f2f-154">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="f3f2f-155">Informations de référence sur les packages signés</span><span class="sxs-lookup"><span data-stu-id="f3f2f-155">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
