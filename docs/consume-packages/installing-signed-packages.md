---
title: Installer un package NuGet signé
description: Décrit le processus d’installation de packages NuGet signés et de configuration des paramètres d’approbation des signatures de package.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977833"
---
# <a name="install-a-signed-package"></a><span data-ttu-id="5fa47-103">Installer un package signé</span><span class="sxs-lookup"><span data-stu-id="5fa47-103">Install a signed package</span></span>

<span data-ttu-id="5fa47-104">L’installation de packages signés ne nécessite aucune action spécifique. Cependant, si le contenu a été modifié après sa signature, l’installation est bloquée avec une erreur [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="5fa47-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="5fa47-105">Les packages signés avec des certificats non approuvés sont considérés comme non signés et installés sans avertissements ni erreurs, comme n’importe quel package non signé.</span><span class="sxs-lookup"><span data-stu-id="5fa47-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="5fa47-106">Configurer les exigences de signature de package</span><span class="sxs-lookup"><span data-stu-id="5fa47-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="5fa47-107">Nécessite NuGet 4.9.0+ et Visual Studio version 15.9 et ultérieure sur Windows</span><span class="sxs-lookup"><span data-stu-id="5fa47-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="5fa47-108">Vous pouvez configurer la façon dont les clients NuGet valident les signatures de package en définissant `signatureValidationMode` sur `require` dans le fichier [nuget.config](../reference/nuget-config-file) avec la commande [`nuget config`](../tools/cli-ref-config).</span><span class="sxs-lookup"><span data-stu-id="5fa47-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="5fa47-109">Ce mode vérifie que tous les packages sont signés par un des certificats approuvés dans le fichier `nuget.config`.</span><span class="sxs-lookup"><span data-stu-id="5fa47-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="5fa47-110">Ce fichier vous permet de spécifier les auteurs et/ou les dépôts qui sont approuvés en fonction de l’empreinte du certificat.</span><span class="sxs-lookup"><span data-stu-id="5fa47-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="5fa47-111">Approuver un auteur de package</span><span class="sxs-lookup"><span data-stu-id="5fa47-111">Trust package author</span></span>

<span data-ttu-id="5fa47-112">Pour approuver des packages en fonction de la signature de l’auteur, utilisez la commande [`trusted-signers`](..tools/cli-ref-trusted-signers) pour définir la propriété `author` dans le fichier nuget.config.</span><span class="sxs-lookup"><span data-stu-id="5fa47-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="5fa47-113">Utilisez la [commande verify](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) de `nuget.exe` pour obtenir la valeur `SHA256` de l’empreinte du certificat.</span><span class="sxs-lookup"><span data-stu-id="5fa47-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="5fa47-114">Approuver tous les packages d’un dépôt</span><span class="sxs-lookup"><span data-stu-id="5fa47-114">Trust all packages from a repository</span></span>

<span data-ttu-id="5fa47-115">Pour approuver des packages en fonction de la signature du dépôt, utilisez l’élément `repository` :</span><span class="sxs-lookup"><span data-stu-id="5fa47-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="5fa47-116">Approuver des propriétaires de package</span><span class="sxs-lookup"><span data-stu-id="5fa47-116">Trust Package Owners</span></span>

<span data-ttu-id="5fa47-117">Les signatures de dépôt incluent des métadonnées supplémentaires pour déterminer les propriétaires du package au moment de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="5fa47-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="5fa47-118">Vous pouvez restreindre les packages d’un dépôt en fonction d’une liste de propriétaires :</span><span class="sxs-lookup"><span data-stu-id="5fa47-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="5fa47-119">Si un package a plusieurs propriétaires et que l’un de ces propriétaires est dans la liste approuvée, l’installation du package réussit.</span><span class="sxs-lookup"><span data-stu-id="5fa47-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="5fa47-120">Certificats racines non approuvés</span><span class="sxs-lookup"><span data-stu-id="5fa47-120">Untrusted Root certificates</span></span>

<span data-ttu-id="5fa47-121">Dans certaines situations, vous souhaitez activer la vérification avec des certificats qui ne sont pas chaînés à une racine approuvée dans la machine locale.</span><span class="sxs-lookup"><span data-stu-id="5fa47-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="5fa47-122">Vous pouvez utiliser l’attribut `allowUntrustedRoot` pour personnaliser ce comportement.</span><span class="sxs-lookup"><span data-stu-id="5fa47-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="5fa47-123">Synchroniser des certificats de dépôt</span><span class="sxs-lookup"><span data-stu-id="5fa47-123">Sync repository certificates</span></span>

<span data-ttu-id="5fa47-124">Les dépôts de packages doivent annoncer les certificats qu’ils utilisent dans leur [index des services](https://docs.microsoft.com/en-us/nuget/api/service-index).</span><span class="sxs-lookup"><span data-stu-id="5fa47-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="5fa47-125">Au final, le dépôt met à jour ces certificats, par exemple quand un certificat expire.</span><span class="sxs-lookup"><span data-stu-id="5fa47-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="5fa47-126">Quand cela se produit, les clients avec des stratégies spécifiques demandent une mise à jour de la configuration pour inclure le certificat nouvellement ajouté.</span><span class="sxs-lookup"><span data-stu-id="5fa47-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="5fa47-127">Vous pouvez facilement mettre à niveau les signataires approuvés associés à un dépôt avec la [commande trusted-signers sync](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-) de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="5fa47-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="5fa47-128">Informations de référence sur le schéma</span><span class="sxs-lookup"><span data-stu-id="5fa47-128">Schema reference</span></span>

<span data-ttu-id="5fa47-129">Vous trouverez les informations de référence complètes sur le schéma pour les stratégies clientes dans les [informations de référence sur nuget.config](/nuget/reference/nuget-config-file#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="5fa47-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="5fa47-130">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="5fa47-130">Related articles</span></span>

- [<span data-ttu-id="5fa47-131">Les différentes façons d’installer un package NuGet</span><span class="sxs-lookup"><span data-stu-id="5fa47-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="5fa47-132">Signature de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="5fa47-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="5fa47-133">Informations de référence sur les packages signés</span><span class="sxs-lookup"><span data-stu-id="5fa47-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
