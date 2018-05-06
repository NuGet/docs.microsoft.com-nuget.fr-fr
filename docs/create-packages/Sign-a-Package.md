---
title: Signature de packages NuGet
description: Explique comment utiliser des packages signés pour vérifier l’intégrité du contenu.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a469cbdd218a0e9c18950bb0d36faf4dbcb42a01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="signing-nuget-packages"></a>Signature de packages NuGet

La signature d’un package est un processus qui garantit que le package n’a pas été modifié depuis sa création.

## <a name="prerequisites"></a>Prérequis

1. Package (fichier `.nupkg`) à signer. Consultez [Création d’un package](creating-a-package.md).

1. nuget.exe 4.6.0 ou ultérieur. Découvrez comment [installer l’interface de ligne de commande NuGet](../install-nuget-client-tools.md#nugetexe-cli).

1. [Certificat de signature de code](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

> [!Warning]
> nuget.org n’accepte pas actuellement les packages signés. Vous pouvez signer des packages pour les publier dans des flux personnalisés.

## <a name="sign-a-package"></a>Signer un package

Pour signer un package, utilisez [nuget sign](../tools/cli-ref-sign.md) :

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Comme décrit dans la référence des commandes, vous pouvez utiliser un certificat disponible dans le magasin de certificats ou utiliser un certificat à partir d’un fichier.

### <a name="common-problems-when-signing-a-package"></a>Problèmes courants liés à la signature d’un package

- Le certificat n’est pas valide pour la signature de code. Vous devez vérifier que le certificat spécifié est associé à l’utilisation améliorée de la clé appropriée (1.3.6.1.5.5.7.3.3).
- Le certificat ne satisfait pas aux exigences de base (par exemple : algorithme de signature RSA SHA-256, clé publique de 2 048 bits ou plus, etc.).
- Le certificat a expiré ou a été révoqué.
- Le serveur d’horodatage ne répond pas aux exigences du certificat.

> [!Note]
> Les packages signés doivent inclure un horodatage pour vérifier que la signature est valide après expiration du certificat de signature. L’opération de signature produit un [avertissement NU3002](../reference/Errors-and-Warnings.md#nu3002) en l’absence d’horodatage.

## <a name="verify-a-signed-package"></a>Vérifier un package signé

Utilisez [nuget verify](../tools/cli-ref-verify.md) pour afficher les détails de la signature d’un package donné :

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Installer un package signé

L’installation de packages signés ne nécessite aucune action spécifique. Toutefois, si le contenu a été modifié après sa signature, l’installation est bloquée et produit une [erreur NU3008](../reference/Errors-and-Warnings.md#nu3008).

> [!Warning]
> Les packages signés avec des certificats non approuvés sont considérés comme non signés et installés sans avertissements ni erreurs, comme n’importe quel package non signé.

## <a name="see-also"></a>Voir aussi

[Informations de référence sur les packages signés](../reference/Signed-Packages-Reference.md)
