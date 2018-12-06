---
title: Packages signés
description: Configuration requise pour la signature du package NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977509"
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

## <a name="timestamp-requirements"></a>Configuration requise d’horodatage

Packages signés doivent inclure un horodatage RFC 3161 pour garantir la validité de signature au-delà de la période de validité du certificat de signature du package. Le certificat utilisé pour signer l’horodateur doit être valide pour le `id-kp-timeStamping` usage [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. En outre, le certificat doit avoir une publique longueur de clé RSA de 2 048 bits ou une version ultérieure.

Vous trouverez des informations techniques dans le [les spécifications techniques de signature du package](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Exigences de signature sur NuGet.org

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
  
  
## <a name="related-articles"></a>Articles connexes

- [Signature de Packages NuGet](../create-packages/Sign-a-Package.md)
- [L’installation de packages signés](../consume-packages/installing-signed-packages.md)
