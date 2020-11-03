---
title: Signature de packages NuGet
description: Explique comment utiliser des packages signés pour vérifier l’intégrité du contenu.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 81f8695d7b3cec73f3e18f90ddf38dfe6c3ecf4d
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237586"
---
# <a name="signing-nuget-packages"></a>Signature de packages NuGet

Les packages signés permettent les contrôles de vérification de l’intégrité du contenu, qui offrent une protection contre la falsification de contenu. La signature du package sert également de source unique de vérité sur l’origine réelle du package et renforce l’authenticité du package pour le consommateur. Ce guide part du principe que vous avez déjà [créé un package](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Obtenir un certificat de signature de code

Des certificats valides peuvent être obtenus auprès d’une autorité de certification publique telle que [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [certr](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. La liste complète des autorités de certification approuvées par Windows peut être obtenue à partir de [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .

Vous pouvez utiliser des certificats auto-émis à des fins de test. Toutefois, les packages signés à l’aide de certificats auto-émis ne sont pas acceptés par NuGet.org. En savoir plus sur [la création d’un certificat de test](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Exporter le fichier de certificat

* Vous pouvez exporter un certificat existant à un format DER binaire avec l’Assistant Exportation de certificat.

  ![Assistant Exportation de certificat](../reference/media/CertificateExportWizard.png)

* Vous pouvez également exporter le certificat avec la [commande PowerShell Export-Certificate](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Signer le package

> [!note]
> Requiert nuget.exe 4.6.0 ou version ultérieure. La prise en charge de dotnet.exe sera bientôt disponible : [#7939](https://github.com/NuGet/Home/issues/7939)

Signez le package avec [nuget sign](../reference/cli-reference/cli-ref-sign.md) :

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Le fournisseur de certificats fournit souvent l’URL d’un serveur d’horodatage que vous pouvez utiliser pour l’argument facultatif `Timestamper` indiqué ci-dessus. Consultez la documentation et/ou contactez le support de votre fournisseur pour obtenir cette URL de service.

* Vous pouvez utiliser un certificat disponible dans le magasin de certificats ou utiliser un certificat provenant d’un fichier. Consultez les informations de référence sur CLI pour [nuget sign](../reference/cli-reference/cli-ref-sign.md).
* Les packages signés doivent inclure un horodatage pour vérifier que la signature est valide après expiration du certificat de signature. Sinon, l’opération de signature produit un [avertissement](../reference/errors-and-warnings/NU3002.md).
* Vous pouvez voir les détails de la signature d’un package donné avec [nuget verify](../reference/cli-reference/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Inscrire le certificat sur NuGet.org

Pour publier un package signé, vous devez d’abord inscrire le certificat auprès de NuGet.org. Vous avez besoin du certificat en tant que `.cer` fichier au format der binaire.

1. [Connectez-vous](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) à NuGet.org.
1. Accédez à `Account settings` (ou à `Manage Organization` **>** `Edit Organziation` si vous voulez inscrire le certificat auprès d’un compte d’organisation).
1. Développez la section `Certificates`, puis sélectionnez `Register new`.
1. Accédez au fichier de certificat qui a été exporté précédemment.
  ![Certificats inscrits](../reference/media/registered-certs.png)

**Remarque**
* Un même utilisateur peut envoyer plusieurs certificats et le même certificat peut être inscrit par plusieurs utilisateurs.
* Une fois qu’un utilisateur a un certificat inscrit, tous les envois de package ultérieurs **doivent** être signés avec un des certificats. Consultez [Gérer les exigences de signature de votre package sur NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Les utilisateurs peuvent également supprimer du compte un certificat inscrit. Une fois qu’un certificat est supprimé, l’envoi de nouveaux packages signés avec ce certificat échoue. Les packages existants ne sont pas affectés.

## <a name="publish-the-package"></a>Publier le package

Vous êtes maintenant prêt à publier le package sur NuGet.org. Consultez [publication de packages](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Créer un certificat de test

Vous pouvez utiliser des certificats auto-émis à des fins de test. Pour créer un certificat auto-émis, utilisez la [commande PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).

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

Cette commande crée un certificat de test disponible dans le magasin de certificats personnel de l’utilisateur actuel. Vous pouvez ouvrir le magasin de certificats en exécutant `certmgr.msc` pour voir le certificat nouvellement créé.

> [!Warning]
> NuGet.org n’accepte pas les packages signés avec des certificats auto-émis.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Gérer les exigences de signature de votre package sur NuGet.org
1. [Connectez-vous](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) à NuGet.org.

1. Accédez à `Manage Packages` 
   ![Configurer des signataires de package](../reference/media/configure-package-signers.png)

* Si vous êtes l’unique propriétaire d’un package, vous êtes le signataire requis : vous pouvez utiliser un des certificats inscrits pour signer et publier vos packages sur NuGet.org.

* Si un package a plusieurs propriétaires, par défaut, les certificats du propriétaire « N’importe lequel » peuvent être utilisés pour signer le package. En tant que copropriétaire du package, vous pouvez remplacer « N’importe lequel » par vous-même ou par n’importe quel autre copropriétaire pour en faire le signataire obligatoire. Si vous déclarez un propriétaire qui n’a aucun certificat inscrit, les packages non signés sont autorisés. 

* De même, si l’option par défaut « N’importe lequel » est sélectionnée pour un package où un propriétaire a un certificat inscrit et où un autre propriétaire n’a aucun certificat inscrit, NuGet.org accepte un package signé avec une signature inscrite par un de ses propriétaires ou un package non signé (un des propriétaires n’ayant aucun certificat inscrit).

## <a name="related-articles"></a>Articles connexes

- [Gérer les limites d’approbation de package](../consume-packages/installing-signed-packages.md)
- [Informations de référence sur les packages signés](../reference/Signed-Packages-Reference.md)