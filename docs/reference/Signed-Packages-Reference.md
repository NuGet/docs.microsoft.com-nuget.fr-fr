---
title: Packages signés
description: Configuration requise pour la signature du package NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550419"
---
# <a name="signed-packages"></a>Packages signés

*4.6.0+ de NuGet et Visual Studio 2017 version 15.6 et versions ultérieure*

Les packages NuGet peuvent inclure une signature numérique qui fournit une protection contre le contenu falsifiée. Cette signature est générée à partir d’un certificat X.509 qui ajoute également des preuves d’authenticité à l’origine réelle du package.

Les packages signés fournissent la validation de bout en bout plus forte. Il existe deux types de signatures de NuGet :
- **Créer la Signature**. Une signature de l’auteur garantit que le package n’a pas été modifié depuis l’auteur a signé le package, non quel que soit à partir de laquelle le dépôt ou ce que le package est remis de méthode de transport. En outre, les packages signés par auteur fournissent un mécanisme d’authentification supplémentaire au pipeline de publication nuget.org, car le certificat de signature doit être inscrit à l’avance. Pour plus d’informations, consultez [enregistrer des certificats](#register-certificate-on-nugetorg).
- **Signature de référentiel**. Les signatures de référentiel offrent la garantie d’intégrité pour **tous les** dans un référentiel de packages qu’ils soient auteur signé ou non, même si ces packages sont obtenues à partir d’un emplacement autre que le dépôt d’origine où ils se trouvaient signé.   

Pour plus d’informations sur la création d’un package signé auteur, consultez [signature de Packages](../create-packages/Sign-a-package.md) et [commande de connexion nuget](../tools/cli-ref-sign.md).

> [!Important]
> La signature du package est actuellement pris en charge uniquement à l’aide de nuget.exe sur Windows. Vérification des packages signés est actuellement pris en charge uniquement lorsque vous utilisez nuget.exe ou Visual Studio sur Windows.

## <a name="certificate-requirements"></a>Conditions de certificat

La signature du package nécessite un code de signature de certificat, qui est un type spécial de certificat est valide pour le `id-kp-codeSigning` usage [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. En outre, le certificat doit avoir une publique longueur de clé RSA de 2 048 bits ou une version ultérieure.

## <a name="get-a-code-signing-certificate"></a>Obtenir un certificat de signature de code

Certificats valides peuvent être obtenus à partir d’une autorité de certification publique, comme :

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Connexion globale](https://www.globalsign.com/en/code-signing-certificate/)
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

Packages signés doivent inclure un horodatage RFC 3161 pour garantir la validité de signature au-delà de la période de validité du certificat de signature du package. Le certificat utilisé pour signer l’horodateur doit être valide pour le `id-kp-timeStamping` usage [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. En outre, le certificat doit avoir une publique longueur de clé RSA de 2 048 bits ou une version ultérieure.

Vous trouverez des informations techniques dans le [les spécifications techniques de signature du package](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Exigences de signature sur nuget.org

NuGet.org a des exigences supplémentaires pour l’acceptation d’un package signé :

- La signature principale doit être une signature de l’auteur.
- La signature principale doit avoir un seul horodateur valid.
- Les certificats X.509 pour la signature de l’auteur et sa signature d’horodatage :
  - Doit avoir une clé publique de RSA 2 048 bits ou supérieur.
  - Doit être au sein de sa période de validité par heure UTC actuelle au moment de la validation du package sur nuget.org.
  - Doit être lié à une autorité racine approuvée qui est approuvée par défaut sur Windows. Les packages signés avec les certificats auto-émis sont rejetées.
  - Doit être valide pour sa fonction : 
    - L’auteur du certificat de signature doit être valide pour la signature de code.
    - Le certificat d’horodatage doit être valide pour le service d’horodatage.
  - Il ne doit pas être révoqué à l’heure de signature. (Cela ne peut pas être qui peuvent être connue au moment de l’envoi, donc nuget.org vérifie périodiquement l’état de révocation).

## <a name="register-certificate-on-nugetorg"></a>Inscrire le certificat sur nuget.org

Pour envoyer un package signé, vous devez tout d’abord inscrire le certificat auprès de nuget.org. Vous avez besoin du certificat en tant qu’un `.cer` fichier dans un format DER binaire. Vous pouvez exporter un certificat existant dans un format DER binaire à l’aide de l’Assistant Exportation de certificat.

![Assistant Exportation de certificat](media/CertificateExportWizard.png)

Les utilisateurs expérimentés peuvent exporter le certificat à l’aide de la [commande Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate.md).

Pour demander le certificat auprès de nuget.org, accédez à `Certificates` section `Account settings` page (ou page de paramètres de l’organisation) et sélectionnez `Register new certificate`.

![Certificats inscrits](media/registered-certs.png)

> [!Tip]
> Un utilisateur peut soumettre que plusieurs certificats et le même certificat peuvent être inscrit par plusieurs utilisateurs.

Une fois qu’un utilisateur a un certificat enregistré, toutes les soumissions ultérieures du package **doit** être signé avec un des certificats.

Les utilisateurs peuvent également supprimer un certificat enregistré à partir du compte. Une fois qu’un certificat est supprimé, les packages signés avec ce certificat échouent au dépôt. Les packages existants ne sont pas affectés.

## <a name="configure-package-signing-requirements"></a>Configurer les exigences de signature du package

Si vous êtes l’unique propriétaire d’un package, vous êtes le signataire requis. Autrement dit, vous pouvez utiliser un des certificats inscrits pour signer vos packages et soumettre sur nuget.org.

Si un package contient plusieurs propriétaires, par défaut, les certificats du propriétaire de la « Any » peuvent être utilisés pour signer le package. En tant que copropriétaire du package, vous pouvez remplacer « Tout » avec vous-même ou n’importe quel autre copropriétaire pour être le signataire requis. Si vous apportez un propriétaire qui ne dispose pas de n’importe quel certificat inscrit, puis packages non signés pourront. 

De même, si la valeur par défaut « Tout » est sélectionnée pour un package où un seul propriétaire a un certificat enregistré et un autre propriétaire n’a pas de n’importe quel certificat inscrit, puis nuget.org accepte un package signé avec une signature inscrite par un de ses propriétaires ou non signée (étant donné qu’un des propriétaires n’a pas de n’importe quel certificat enregistré) du package.

![Configurer des signataires de package](media/configure-package-signers.png)
