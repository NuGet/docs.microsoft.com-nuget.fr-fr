---
title: Signature de packages NuGet
description: Explique comment utiliser des packages signés pour vérifier l’intégrité du contenu.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 0679b60179760d6626e7ce42bfdbdfa266677ce6
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2018
ms.locfileid: "42792934"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="25332-103">Signature de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="25332-103">Signing NuGet Packages</span></span>

<span data-ttu-id="25332-104">La signature d’un package est un processus qui garantit que le package n’a pas été modifié depuis sa création.</span><span class="sxs-lookup"><span data-stu-id="25332-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25332-105">Prérequis</span><span class="sxs-lookup"><span data-stu-id="25332-105">Prerequisites</span></span>

1. <span data-ttu-id="25332-106">Package (fichier `.nupkg`) à signer.</span><span class="sxs-lookup"><span data-stu-id="25332-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="25332-107">Consultez [Création d’un package](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="25332-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="25332-108">nuget.exe 4.6.0 ou ultérieur.</span><span class="sxs-lookup"><span data-stu-id="25332-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="25332-109">Découvrez comment [installer l’interface de ligne de commande NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="25332-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="25332-110">[Certificat de signature de code](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="25332-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="25332-111">Signer un package</span><span class="sxs-lookup"><span data-stu-id="25332-111">Sign a package</span></span>

<span data-ttu-id="25332-112">Pour signer un package, utilisez [nuget sign](../tools/cli-ref-sign.md) :</span><span class="sxs-lookup"><span data-stu-id="25332-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="25332-113">Comme décrit dans la référence des commandes, vous pouvez utiliser un certificat disponible dans le magasin de certificats ou utiliser un certificat à partir d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="25332-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="25332-114">Problèmes courants liés à la signature d’un package</span><span class="sxs-lookup"><span data-stu-id="25332-114">Common problems when signing a package</span></span>

- <span data-ttu-id="25332-115">Le certificat n’est pas valide pour la signature de code.</span><span class="sxs-lookup"><span data-stu-id="25332-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="25332-116">Vous devez vérifier que le certificat spécifié est associé à l’utilisation améliorée de la clé appropriée (1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="25332-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="25332-117">Le certificat ne satisfait pas aux exigences de base (par exemple : algorithme de signature RSA SHA-256, clé publique de 2 048 bits ou plus, etc.).</span><span class="sxs-lookup"><span data-stu-id="25332-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="25332-118">Le certificat a expiré ou a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="25332-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="25332-119">Le serveur d’horodatage ne répond pas aux exigences du certificat.</span><span class="sxs-lookup"><span data-stu-id="25332-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="25332-120">Les packages signés doivent inclure un horodatage pour vérifier que la signature est valide après expiration du certificat de signature.</span><span class="sxs-lookup"><span data-stu-id="25332-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="25332-121">L’opération de signature produit un [avertissement NU3002](../reference/errors-and-warnings/NU3002.md) en l’absence d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="25332-121">The sign operation produce a [warning NU3002](../reference/errors-and-warnings/NU3002.md) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="25332-122">Vérifier un package signé</span><span class="sxs-lookup"><span data-stu-id="25332-122">Verify a signed package</span></span>

<span data-ttu-id="25332-123">Utilisez [nuget verify](../tools/cli-ref-verify.md) pour afficher les détails de la signature d’un package donné :</span><span class="sxs-lookup"><span data-stu-id="25332-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="25332-124">Installer un package signé</span><span class="sxs-lookup"><span data-stu-id="25332-124">Install a signed package</span></span>

<span data-ttu-id="25332-125">L’installation de packages signés ne nécessite aucune action spécifique. Toutefois, si le contenu a été modifié après sa signature, l’installation est bloquée et produit une [erreur NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="25332-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked and produces an [error NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="25332-126">Les packages signés avec des certificats non approuvés sont considérés comme non signés et installés sans avertissements ni erreurs, comme n’importe quel package non signé.</span><span class="sxs-lookup"><span data-stu-id="25332-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="25332-127">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="25332-127">See also</span></span>

[<span data-ttu-id="25332-128">Informations de référence sur les packages signés</span><span class="sxs-lookup"><span data-stu-id="25332-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
