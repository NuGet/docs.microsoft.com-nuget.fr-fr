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
ms.locfileid: "34449589"
---
# <a name="signed-packages"></a>Packages signés

*NuGet 4.6.0+ et Visual Studio 2017 15,6 et versions ultérieures*

Les packages NuGet peuvent inclure une signature numérique qui assure la protection de contenu falsifié. Cette signature est générée à partir d’un certificat X.509 qui ajoute également des preuves d’authenticité à l’origine réelle du package.

Les packages signés fournissent la validation de bout en bout pour les plus fortes. Une signature de l’auteur garantit que le package n’a pas été modifié depuis l’auteur de signature du package, sans quel que soit à partir de laquelle référentiel ou que le package est remis (méthode) de transport.

En outre, signées par l’auteur de packages fournissent un mécanisme d’authentification supplémentaire pour le pipeline de publication nuget.org car le certificat de signature doit être enregistré à l’avance. Pour plus d’informations, consultez [enregistrer des certificats](#register-certificate-on-nugetorg).

Pour plus d’informations sur la création d’un package signé, consultez [de signature de Packages](../create-packages/Sign-a-package.md) et [commande de connexion nuget](../tools/cli-ref-sign.md).

> [!Important]
> La signature du package est actuellement pris en charge uniquement sur Windows à l’aide de nuget.exe. Vérification des packages signés est actuellement pris en charge uniquement sur Windows à l’aide de nuget.exe ou Visual Studio.

## <a name="certificate-requirements"></a>Conditions de certificat

La signature du package nécessite un code de signature de certificat, qui est un type particulier de certificat valide pour le `id-kp-codeSigning` objectif [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. En outre, le certificat doit avoir une publique longueur de clé RSA ou plus de 2 048 bits.

## <a name="get-a-code-signing-certificate"></a>Obtenir un certificat de signature de code

Certificats valides peuvent être obtenues à partir d’une autorité de certification publique comme :

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Signe global](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

La liste complète des autorités de certification approuvées par Windows peut être obtenue à partir de [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Créer un certificat de test

Vous pouvez utiliser les certificats auto-émis à des fins de test. Pour créer un certificat auto-émis, utilisez le [commande New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

> [!Warning]
> NuGet.org n’accepte pas les packages signés avec les certificats auto-émis.

## <a name="timestamp-requirements"></a>Configuration requise d’horodatage

Les packages signés doivent inclure un horodatage RFC 3161 pour garantir la validité de signature au-delà de la période de validité du certificat de signature de packages. Le certificat utilisé pour signer l’horodateur doit être valide pour le `id-kp-timeStamping` objectif [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. En outre, le certificat doit avoir une publique longueur de clé RSA ou plus de 2 048 bits.

Vous trouverez des informations techniques dans le [les spécifications techniques de signature du package](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Spécifications de signature sur nuget.org

NuGet.org a des exigences supplémentaires pour l’acceptation d’un package signé :

- La signature principale doit être une signature de l’auteur.
- La signature principale doit avoir un seul horodateur valid.
- Les certificats X.509 pour la signature de l’auteur et sa signature horodateur :
  - Doit avoir une clé publique de RSA 2 048 bits ou supérieur.
  - Doit être dans sa période de validité par heure UTC actuelle au moment de la validation du package sur nuget.org.
  - Doit être chaîné à une autorité racine approuvée qui est approuvée par défaut sur Windows. Les packages signés avec les certificats auto-émis sont rejetées.
  - Doit être valide pour son objectif : 
    - L’auteur du certificat de signature doit être valide pour la signature de code.
    - Le certificat de l’horodatage doit être valide pour le service d’horodatage.
  - Ne doit pas être révoqué à l’heure de signature. (Il ne peut pas être qui peuvent être connue au moment de l’envoi, donc nuget.org vérifie périodiquement l’état de révocation).

## <a name="register-certificate-on-nugetorg"></a>Enregistrer un certificat sur nuget.org

Pour envoyer un package signé, vous devez d’abord inscrire le certificat dans nuget.org. Vous devez installer le certificat en tant qu’un `.cer` fichier dans un format DER binaire. Vous pouvez exporter un certificat existant dans un format DER binaire à l’aide de l’Assistant Exportation de certificat.

![Assistant Exportation de certificat](media/CertificateExportWizard.png)

Les utilisateurs expérimentés peuvent exporter le certificat à l’aide de la [commande PowerShell de certificat d’exportation](/powershell/module/pkiclient/export-certificate.md).

Pour inscrire le certificat avec nuget.org, accédez à `Certificates` section `Account settings` page (ou page de paramètres de l’organisation) et sélectionnez `Register new certificate`.

![Certificats inscrits](media/registered-certs.png)

> [!Tip]
> Un utilisateur peut soumettre que plusieurs certificats et le même certificat peuvent être inscrit par plusieurs utilisateurs.

Une fois qu’un utilisateur a un certificat enregistré, toutes les soumissions futures **doit** être signées avec un des certificats.

Les utilisateurs peuvent également supprimer un certificat enregistré à partir du compte. Une fois qu’un certificat est supprimé, les packages signés avec ce certificat échouent au dépôt. Les packages existants ne sont pas affectés.

## <a name="configure-package-signing-requirements"></a>Configurer les exigences de signature de packages

Si vous êtes l’unique propriétaire d’un package, vous êtes le signataire obligatoire. Autrement dit, vous pouvez utiliser un des certificats inscrits pour signer vos packages et les soumettre à nuget.org.

Si un package contient plusieurs propriétaires, par défaut, les certificats du « Tout » propriétaire peuvent être utilisés pour signer le package. En tant que copropriétaire du package, vous pouvez remplacer « Tout » avec vous-même ou n’importe quel autre copropriétaire soit le signataire obligatoire. Si vous effectuez un propriétaire qui ne dispose pas de n’importe quel certificat inscrit, puis packages non signés seront autorisés. 

De même, si la valeur par défaut est « Any » sélectionnée pour un package dans lequel un seul propriétaire a un certificat inscrit et un autre propriétaire n’a pas de n’importe quel certificat inscrit, puis nuget.org accepte un package signé avec une signature inscrite par un de ses propriétaires ou non signée (étant donné qu’un des propriétaires n’a pas de n’importe quel certificat enregistré) du package.

![Configurer signataires de package](media/configure-package-signers.png)
