---
title: Référence des Packages NuGet de signé
description: Configuration requise pour la signature du package NuGet.
author: rido-min
ms.author: rido-min
manager: unnir
ms.date: 04/24/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 751a8ff14bdc3a647985da4f908ad1a0fd0def9a
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2018
---
# <a name="signed-packages"></a>Packages signés

*NuGet 4.6.0+ et Visual Studio 2017 15,6 et versions ultérieures*

Les packages NuGet peuvent inclure une signature numérique qui assure la protection de contenu falsifié. Cette signature est générée à partir d’un certificat X.509 qui ajoute également des preuves d’authenticité à l’origine réelle du package.

Les packages signés fournissent la validation de bout en bout pour les plus fortes. Une signature de l’auteur garantit que le package n’a pas été modifié depuis l’auteur de signature du package, sans quel que soit à partir de laquelle référentiel ou que le package est remis (méthode) de transport.

Les consommateurs qui exigent un environnement verrouillé peuvent nécessiter des packages signés avec un certificat de l’auteur spécifique.

En outre, signées par l’auteur de packages fournissent un mécanisme d’authentification supplémentaire pour le pipeline de publication nuget.org car le certificat de signature doit être enregistré à l’avance.

Pour plus d’informations sur la création d’un package signé, consultez [de signature de Packages](../create-packages/Sign-a-package.md) et [commande de connexion nuget](../tools/cli-ref-sign.md).

> [!Important]
> actuellement, NuGet.org n’accepte pas les packages signés. Vous pouvez signer des packages pour les publier dans des flux personnalisés.

> [!Important]
> La signature du package est actuellement pris en charge uniquement sur Windows à l’aide de nuget.exe. Vérification des packages signés est actuellement pris en charge uniquement sur Windows à l’aide de nuget.exe ou Visual Studio.

## <a name="certificate-requirements"></a>Conditions de certificat

La signature du package nécessite un code de signature de certificat, qui est un type particulier de certificat valide pour le `id-kp-codeSigning` objectif [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. En outre, le certificat doit avoir une publique longueur de clé RSA ou plus de 2 048 bits.

## <a name="get-a-code-signing-certificate"></a>Obtenir un certificat de signature de code

Les certificats valides peuvent être obtenues à partir des autorités de certification publique comme :

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Signe global](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

La liste complète des autorités de certification approuvées par Windows peut être obtenue à partir de [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Créer un certificat de test

Vous pouvez utiliser les certificats auto-émis à des fins de test. Pour créer un certificat auto-émis, utilisez le [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) commande PowerShell.

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

Cette commande crée un certificat de test disponible dans le magasin de certificats personnel de l’utilisateur actuel. Vous pouvez ouvrir le magasin de certificats en exécutant `certmgr.msc` pour afficher le certificat nouvellement créé.

## <a name="timestamp-requirements"></a>Configuration requise d’horodatage

Les packages signés doivent inclure un horodatage RFC 3161 pour garantir la validité de signature au-delà de la période de validité du certificat de signature de packages. Le certificat utilisé pour signer l’horodateur doit être valide pour le `id-kp-timeStamping` objectif [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. En outre, le certificat doit avoir une publique longueur de clé RSA ou plus de 2 048 bits.

Vous trouverez des informations techniques dans le [les spécifications techniques de signature du package](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).
