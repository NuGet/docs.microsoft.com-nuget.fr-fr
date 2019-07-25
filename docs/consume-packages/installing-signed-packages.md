---
title: Gérer les limites d’approbation de package
description: Décrit le processus d’installation de packages NuGet signés et de configuration des paramètres d’approbation des signatures de package.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 7b92d07d19a2e9073ecc38ed37b4ee2491080443
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317769"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="548d9-103">Gérer les limites d’approbation de package</span><span class="sxs-lookup"><span data-stu-id="548d9-103">Manage package trust boundaries</span></span>

<span data-ttu-id="548d9-104">L’installation de packages signés ne nécessite aucune action spécifique. Cependant, si le contenu a été modifié après sa signature, l’installation est bloquée avec une erreur [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="548d9-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="548d9-105">Les packages signés avec des certificats non approuvés sont considérés comme non signés et installés sans avertissements ni erreurs, comme n’importe quel package non signé.</span><span class="sxs-lookup"><span data-stu-id="548d9-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="548d9-106">Configurer les exigences de signature de package</span><span class="sxs-lookup"><span data-stu-id="548d9-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="548d9-107">Nécessite NuGet 4.9.0+ et Visual Studio version 15.9 et ultérieure sur Windows</span><span class="sxs-lookup"><span data-stu-id="548d9-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="548d9-108">Vous pouvez configurer la façon dont les clients NuGet valident les signatures de package en définissant `signatureValidationMode` sur `require` dans le fichier [nuget.config](../reference/nuget-config-file.md) avec la commande [`nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="548d9-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="548d9-109">Ce mode vérifie que tous les packages sont signés par un des certificats approuvés dans le fichier `nuget.config`.</span><span class="sxs-lookup"><span data-stu-id="548d9-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="548d9-110">Ce fichier vous permet de spécifier les auteurs et/ou les dépôts qui sont approuvés en fonction de l’empreinte du certificat.</span><span class="sxs-lookup"><span data-stu-id="548d9-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="548d9-111">Approuver un auteur de package</span><span class="sxs-lookup"><span data-stu-id="548d9-111">Trust package author</span></span>

<span data-ttu-id="548d9-112">Pour approuver des packages en fonction de la signature de l’auteur, utilisez la commande [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) pour définir la propriété `author` dans le fichier nuget.config.</span><span class="sxs-lookup"><span data-stu-id="548d9-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
><span data-ttu-id="548d9-113">Utilisez la [commande verify](../reference/cli-reference/cli-ref-verify.md) de `nuget.exe` pour obtenir la valeur `SHA256` de l’empreinte du certificat.</span><span class="sxs-lookup"><span data-stu-id="548d9-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="548d9-114">Approuver tous les packages d’un dépôt</span><span class="sxs-lookup"><span data-stu-id="548d9-114">Trust all packages from a repository</span></span>

<span data-ttu-id="548d9-115">Pour approuver des packages en fonction de la signature du dépôt, utilisez l’élément `repository` :</span><span class="sxs-lookup"><span data-stu-id="548d9-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="548d9-116">Approuver des propriétaires de package</span><span class="sxs-lookup"><span data-stu-id="548d9-116">Trust Package Owners</span></span>

<span data-ttu-id="548d9-117">Les signatures de dépôt incluent des métadonnées supplémentaires pour déterminer les propriétaires du package au moment de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="548d9-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="548d9-118">Vous pouvez restreindre les packages d’un dépôt en fonction d’une liste de propriétaires :</span><span class="sxs-lookup"><span data-stu-id="548d9-118">You can restrict packages from a repository based on a list of owners:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

<span data-ttu-id="548d9-119">Si un package a plusieurs propriétaires et que l’un de ces propriétaires est dans la liste approuvée, l’installation du package réussit.</span><span class="sxs-lookup"><span data-stu-id="548d9-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="548d9-120">Certificats racines non approuvés</span><span class="sxs-lookup"><span data-stu-id="548d9-120">Untrusted Root certificates</span></span>

<span data-ttu-id="548d9-121">Dans certaines situations, vous souhaitez activer la vérification avec des certificats qui ne sont pas chaînés à une racine approuvée dans la machine locale.</span><span class="sxs-lookup"><span data-stu-id="548d9-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="548d9-122">Vous pouvez utiliser l’attribut `allowUntrustedRoot` pour personnaliser ce comportement.</span><span class="sxs-lookup"><span data-stu-id="548d9-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="548d9-123">Synchroniser des certificats de dépôt</span><span class="sxs-lookup"><span data-stu-id="548d9-123">Sync repository certificates</span></span>

<span data-ttu-id="548d9-124">Les dépôts de packages doivent annoncer les certificats qu’ils utilisent dans leur [index des services](../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="548d9-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="548d9-125">Au final, le dépôt met à jour ces certificats, par exemple quand un certificat expire.</span><span class="sxs-lookup"><span data-stu-id="548d9-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="548d9-126">Quand cela se produit, les clients avec des stratégies spécifiques demandent une mise à jour de la configuration pour inclure le certificat nouvellement ajouté.</span><span class="sxs-lookup"><span data-stu-id="548d9-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="548d9-127">Vous pouvez facilement mettre à niveau les signataires approuvés associés à un dépôt avec la [commande trusted-signers sync](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-) de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="548d9-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="548d9-128">Informations de référence sur le schéma</span><span class="sxs-lookup"><span data-stu-id="548d9-128">Schema reference</span></span>

<span data-ttu-id="548d9-129">Vous trouverez les informations de référence complètes sur le schéma pour les stratégies clientes dans les [informations de référence sur nuget.config](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="548d9-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="548d9-130">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="548d9-130">Related articles</span></span>

- [<span data-ttu-id="548d9-131">Signature de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="548d9-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="548d9-132">Informations de référence sur les packages signés</span><span class="sxs-lookup"><span data-stu-id="548d9-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
