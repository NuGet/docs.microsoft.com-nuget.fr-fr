---
title: Packages signés
description: Configuration requise pour la signature de package NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 7384e8b30cb2ec5fe53ea0fe485858bc1f7b3c43
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231251"
---
# <a name="signed-packages"></a>Packages signés

*NuGet 4.6.0 + et Visual Studio 2017 version 15,6 et versions ultérieures*

Les packages NuGet peuvent inclure une signature numérique qui offre une protection contre le contenu falsifié. Cette signature est générée à partir d’un certificat X. 509 qui ajoute également des preuves d’authenticité à l’origine réelle du package.

Les packages signés fournissent la validation de bout en bout la plus puissante. Il existe deux types différents de signatures NuGet :
- **Signature**de l’auteur. Une signature d’auteur garantit que le package n’a pas été modifié depuis que l’auteur a signé le package, quel que soit le référentiel ou la méthode de transport que le package est remis. En outre, les packages signés par l’auteur fournissent un mécanisme d’authentification supplémentaire au pipeline de publication nuget.org, car le certificat de signature doit être enregistré à l’avance. Pour plus d’informations, consultez [inscrire des certificats](#signature-requirements-on-nugetorg).
- **Signature du référentiel**. Les signatures de référentiel fournissent une garantie d’intégrité pour **tous les** packages d’un référentiel, qu’ils soient signés ou non, même si ces packages sont obtenus à partir d’un emplacement différent de celui dans lequel ils ont été signés.   

Pour plus d’informations sur la création d’un package signé par l’auteur, consultez [signature de packages](../create-packages/Sign-a-package.md) et la [commande NuGet Sign](../reference/cli-reference/cli-ref-sign.md).

> [!Important]
> La signature du package n’est actuellement prise en charge que lors de l’utilisation de NuGet. exe sur Windows. La [vérification des packages signés n’est actuellement prise en charge que lors de l’utilisation de NuGet. exe](../reference/cli-reference/cli-ref-verify.md) ou de Visual Studio sur Windows.

## <a name="certificate-requirements"></a>Configuration requise des certificats

La signature de package requiert un certificat de signature de code, qui est un type spécial de certificat qui est valide pour le `id-kp-codeSigning` objectif [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. En outre, le certificat doit avoir une longueur de clé publique RSA de 2048 bits ou supérieure.

## <a name="timestamp-requirements"></a>Exigences relatives aux horodateurs

Les packages signés doivent inclure un horodateur RFC 3161 pour garantir la validité des signatures au-delà de la période de validité du certificat de signature du package. Le certificat utilisé pour signer l’horodateur doit être valide pour le `id-kp-timeStamping` objectif [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. En outre, le certificat doit avoir une longueur de clé publique RSA de 2048 bits ou supérieure.

Des détails techniques supplémentaires sont disponibles dans les [spécifications techniques des signatures de packages](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Spécifications de signature sur NuGet.org

nuget.org a des exigences supplémentaires pour accepter un package signé :

- La signature principale doit être une signature d’auteur.
- La signature principale doit avoir un seul horodateur valide.
- Les certificats X. 509 pour la signature de l’auteur et la signature d’horodatage :
  - Doit avoir une clé publique RSA 2048 bits ou une version ultérieure.
  - Doit être dans sa période de validité par heure UTC actuelle au moment de la validation du package sur nuget.org.
  - Doit être lié à une autorité racine approuvée qui est approuvée par défaut sur Windows. Les packages signés avec des certificats auto-émis sont rejetés.
  - Doit être valide dans son but : 
    - Le certificat de signature d’auteur doit être valide pour la signature de code.
    - Le certificat d’horodatage doit être valide pour l’horodatage.
  - Ne doit pas être révoqué au moment de la signature. (Cela peut ne pas être knowable au moment de l’envoi, de sorte que nuget.org revérifie régulièrement l’état de révocation).
  
  
## <a name="related-articles"></a>Articles connexes

- [Signature de packages NuGet](../create-packages/Sign-a-Package.md)
- [Gérer les limites d’approbation de package](../consume-packages/installing-signed-packages.md)
