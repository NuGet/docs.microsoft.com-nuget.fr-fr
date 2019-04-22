---
title: Référence du fichier NuGet.config
description: Informations de référence sur le fichier NuGet.Config, notamment les sections config, bindingRedirects, packageRestore, solution et packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911086"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="27b95-103">nuget.config reference</span><span class="sxs-lookup"><span data-stu-id="27b95-103">nuget.config reference</span></span>

<span data-ttu-id="27b95-104">Le comportement de NuGet est contrôlé par des paramètres dans différents fichiers `NuGet.Config` comme décrit dans [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="27b95-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="27b95-105">`nuget.config` est un fichier XML contenant un nœud `<configuration>` de niveau supérieur qui comprend à son tour les éléments de section décrits dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="27b95-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="27b95-106">Chaque section contient zéro ou plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="27b95-106">Each section contains zero or more items.</span></span> <span data-ttu-id="27b95-107">Consultez [l’exemple de fichier config](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="27b95-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="27b95-108">Les noms de paramètre ne respectent pas la casse et les valeurs peuvent utiliser des [variables d’environnement](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="27b95-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="27b95-109">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="27b95-109">In this topic:</span></span>

- [<span data-ttu-id="27b95-110">Section config</span><span class="sxs-lookup"><span data-stu-id="27b95-110">config section</span></span>](#config-section)
- [<span data-ttu-id="27b95-111">Section bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="27b95-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="27b95-112">Section packageRestore</span><span class="sxs-lookup"><span data-stu-id="27b95-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="27b95-113">Section solution</span><span class="sxs-lookup"><span data-stu-id="27b95-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="27b95-114">[Sections sur les sources de packages](#package-source-sections) :</span><span class="sxs-lookup"><span data-stu-id="27b95-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="27b95-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="27b95-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="27b95-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="27b95-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="27b95-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="27b95-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="27b95-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="27b95-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="27b95-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="27b95-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="27b95-120">section de trustedSigners</span><span class="sxs-lookup"><span data-stu-id="27b95-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="27b95-121">Utilisation de variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="27b95-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="27b95-122">Exemple de fichier config</span><span class="sxs-lookup"><span data-stu-id="27b95-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="27b95-123">Section config</span><span class="sxs-lookup"><span data-stu-id="27b95-123">config section</span></span>

<span data-ttu-id="27b95-124">Contient des paramètres de configuration divers, qui peuvent être définis à l’aide de la [commande `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="27b95-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="27b95-125">`dependencyVersion` et `repositoryPath` s’appliquent uniquement aux projets utilisant `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="27b95-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="27b95-126">`globalPackagesFolder` s’applique uniquement aux projets utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="27b95-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="27b95-127">Touche</span><span class="sxs-lookup"><span data-stu-id="27b95-127">Key</span></span> | <span data-ttu-id="27b95-128">Value</span><span class="sxs-lookup"><span data-stu-id="27b95-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="27b95-129">dependencyVersion (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="27b95-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="27b95-130">Valeur `DependencyVersion` par défaut pour l’installation, la restauration et la mise à jour de package, quand le commutateur `-DependencyVersion` n’est pas spécifié directement.</span><span class="sxs-lookup"><span data-stu-id="27b95-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="27b95-131">Cette valeur est également utilisée par l’interface utilisateur du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="27b95-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="27b95-132">Les valeurs sont `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="27b95-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="27b95-133">globalPackagesFolder (projets à l’aide de PackageReference uniquement)</span><span class="sxs-lookup"><span data-stu-id="27b95-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="27b95-134">Emplacement du dossier de packages global par défaut.</span><span class="sxs-lookup"><span data-stu-id="27b95-134">The location of the default global packages folder.</span></span> <span data-ttu-id="27b95-135">L’emplacement par défaut est `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="27b95-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="27b95-136">Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="27b95-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="27b95-137">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="27b95-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="27b95-138">repositoryPath (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="27b95-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="27b95-139">Emplacement dans lequel installer les packages NuGet au lieu du dossier `$(Solutiondir)/packages` par défaut.</span><span class="sxs-lookup"><span data-stu-id="27b95-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="27b95-140">Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="27b95-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="27b95-141">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="27b95-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="27b95-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="27b95-142">defaultPushSource</span></span> | <span data-ttu-id="27b95-143">Identifie l’URL ou le chemin de la source du package qui doit être utilisée comme valeur par défaut si aucune autre source de package n’est trouvée pour une opération.</span><span class="sxs-lookup"><span data-stu-id="27b95-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="27b95-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="27b95-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="27b95-145">Paramètres de proxy à utiliser lors de la connexion aux sources de packages ; `http_proxy` doit être au format `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="27b95-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="27b95-146">Les mots de passe sont chiffrés et ne peuvent pas être ajoutés manuellement.</span><span class="sxs-lookup"><span data-stu-id="27b95-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="27b95-147">Pour `no_proxy`, la valeur est une liste de domaines séparés par des virgules qui ignorent le serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="27b95-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="27b95-148">Vous pouvez également utiliser les variables d’environnement http_proxy et no_proxy pour ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="27b95-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="27b95-149">Pour plus d’informations, consultez [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="27b95-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="27b95-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="27b95-150">signatureValidationMode</span></span> | <span data-ttu-id="27b95-151">Spécifie le mode de validation utilisé pour vérifier les signatures de package pour l’installation du package et de restauration.</span><span class="sxs-lookup"><span data-stu-id="27b95-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="27b95-152">Les valeurs sont `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="27b95-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="27b95-153">La valeur par défaut est `accept`.</span><span class="sxs-lookup"><span data-stu-id="27b95-153">Defaults to `accept`.</span></span>

<span data-ttu-id="27b95-154">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="27b95-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="27b95-155">Section bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="27b95-155">bindingRedirects section</span></span>

<span data-ttu-id="27b95-156">Définit si NuGet effectue des redirections de liaisons automatiques quand un package est installé.</span><span class="sxs-lookup"><span data-stu-id="27b95-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="27b95-157">Touche</span><span class="sxs-lookup"><span data-stu-id="27b95-157">Key</span></span> | <span data-ttu-id="27b95-158">Value</span><span class="sxs-lookup"><span data-stu-id="27b95-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="27b95-159">skip</span><span class="sxs-lookup"><span data-stu-id="27b95-159">skip</span></span> | <span data-ttu-id="27b95-160">Valeur booléenne indiquant s’il faut ignorer les redirections de liaisons automatiques.</span><span class="sxs-lookup"><span data-stu-id="27b95-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="27b95-161">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="27b95-161">The default is false.</span></span> |

<span data-ttu-id="27b95-162">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="27b95-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="27b95-163">Section packageRestore</span><span class="sxs-lookup"><span data-stu-id="27b95-163">packageRestore section</span></span>

<span data-ttu-id="27b95-164">Contrôle la restauration de packages pendant les générations.</span><span class="sxs-lookup"><span data-stu-id="27b95-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="27b95-165">Touche</span><span class="sxs-lookup"><span data-stu-id="27b95-165">Key</span></span> | <span data-ttu-id="27b95-166">Value</span><span class="sxs-lookup"><span data-stu-id="27b95-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="27b95-167">enabled</span><span class="sxs-lookup"><span data-stu-id="27b95-167">enabled</span></span> | <span data-ttu-id="27b95-168">Valeur booléenne indiquant si NuGet peut effectuer une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="27b95-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="27b95-169">Vous pouvez également définir la variable d’environnement `EnableNuGetPackageRestore` avec la valeur `True` au lieu de définir cette clé dans le fichier config.</span><span class="sxs-lookup"><span data-stu-id="27b95-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="27b95-170">automatique</span><span class="sxs-lookup"><span data-stu-id="27b95-170">automatic</span></span> | <span data-ttu-id="27b95-171">Valeur booléenne indiquant si NuGet doit rechercher les packages manquants pendant une génération.</span><span class="sxs-lookup"><span data-stu-id="27b95-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="27b95-172">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="27b95-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="27b95-173">Section solution</span><span class="sxs-lookup"><span data-stu-id="27b95-173">solution section</span></span>

<span data-ttu-id="27b95-174">Contrôle si le dossier `packages` d’une solution est inclus dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="27b95-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="27b95-175">Cette section fonctionne uniquement dans les fichiers `nuget.config` dans un dossier de solution.</span><span class="sxs-lookup"><span data-stu-id="27b95-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="27b95-176">Touche</span><span class="sxs-lookup"><span data-stu-id="27b95-176">Key</span></span> | <span data-ttu-id="27b95-177">Value</span><span class="sxs-lookup"><span data-stu-id="27b95-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="27b95-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="27b95-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="27b95-179">Valeur booléenne indiquant s’il faut ignorer le dossier de packages lors de l’utilisation de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="27b95-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="27b95-180">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="27b95-180">The default value is false.</span></span> |

<span data-ttu-id="27b95-181">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="27b95-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="27b95-182">Sections sur les sources de packages</span><span class="sxs-lookup"><span data-stu-id="27b95-182">Package source sections</span></span>

<span data-ttu-id="27b95-183">Le `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` et `trustedSigners` fonctionnent ensemble pour configurer le fonctionne de NuGet avec les référentiels de package pendant l’installation, la restauration et les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="27b95-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="27b95-184">Le [ `nuget sources` commande](../tools/cli-ref-sources.md) est généralement utilisée pour gérer ces paramètres, à l’exception de `apikeys` qui est gérée à l’aide de la [ `nuget setapikey` commande](../tools/cli-ref-setapikey.md), et `trustedSigners` qui est gérée à l’aide de la [ `nuget trusted-signers` commande](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="27b95-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="27b95-185">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="27b95-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="27b95-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="27b95-186">packageSources</span></span>

<span data-ttu-id="27b95-187">Répertorie toutes les sources de packages connues.</span><span class="sxs-lookup"><span data-stu-id="27b95-187">Lists all known package sources.</span></span> <span data-ttu-id="27b95-188">L’ordre est ignoré pendant les opérations de restauration et avec n’importe quel projet en utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="27b95-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="27b95-189">NuGet respecte l’ordre des sources pour installer et mettre à jour des opérations avec des projets à l’aide de `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="27b95-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="27b95-190">Touche</span><span class="sxs-lookup"><span data-stu-id="27b95-190">Key</span></span> | <span data-ttu-id="27b95-191">Value</span><span class="sxs-lookup"><span data-stu-id="27b95-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="27b95-192">(nom à assigner à la source du package)</span><span class="sxs-lookup"><span data-stu-id="27b95-192">(name to assign to the package source)</span></span> | <span data-ttu-id="27b95-193">Chemin ou URL de la source du package.</span><span class="sxs-lookup"><span data-stu-id="27b95-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="27b95-194">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="27b95-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="27b95-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="27b95-195">packageSourceCredentials</span></span>

<span data-ttu-id="27b95-196">Stocke les noms d’utilisateur et mots de passe pour les sources, spécifiés en général en utilisant les commutateurs `-username` et `-password` avec `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="27b95-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="27b95-197">Les mots de passe sont chiffrés par défaut, sauf si l’option `-storepasswordincleartext` est également utilisée.</span><span class="sxs-lookup"><span data-stu-id="27b95-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="27b95-198">Touche</span><span class="sxs-lookup"><span data-stu-id="27b95-198">Key</span></span> | <span data-ttu-id="27b95-199">Value</span><span class="sxs-lookup"><span data-stu-id="27b95-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="27b95-200">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="27b95-200">username</span></span> | <span data-ttu-id="27b95-201">Nom d’utilisateur pour la source en texte brut.</span><span class="sxs-lookup"><span data-stu-id="27b95-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="27b95-202">mot de passe</span><span class="sxs-lookup"><span data-stu-id="27b95-202">password</span></span> | <span data-ttu-id="27b95-203">Mot de passe chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="27b95-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="27b95-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="27b95-204">cleartextpassword</span></span> | <span data-ttu-id="27b95-205">Mot de passe non chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="27b95-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="27b95-206">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="27b95-206">**Example:**</span></span>

<span data-ttu-id="27b95-207">Dans le fichier config, l’élément `<packageSourceCredentials>` contient des nœuds enfants pour chaque nom de source applicable (les espaces dans le nom sont remplacés par `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="27b95-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="27b95-208">Autrement dit, pour les sources nommées « Contoso » et « Test Source », le fichier config contient les éléments suivants lors de l’utilisation de mots de passe chiffrés :</span><span class="sxs-lookup"><span data-stu-id="27b95-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="27b95-209">Lors de l’utilisation de mots de passe non chiffrés :</span><span class="sxs-lookup"><span data-stu-id="27b95-209">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="27b95-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="27b95-210">apikeys</span></span>

<span data-ttu-id="27b95-211">Stocke les clés pour les sources qui utilisent l’authentification de clé API, comme défini avec la [commande `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="27b95-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="27b95-212">Touche</span><span class="sxs-lookup"><span data-stu-id="27b95-212">Key</span></span> | <span data-ttu-id="27b95-213">Value</span><span class="sxs-lookup"><span data-stu-id="27b95-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="27b95-214">(URL source)</span><span class="sxs-lookup"><span data-stu-id="27b95-214">(source URL)</span></span> | <span data-ttu-id="27b95-215">Clé API chiffrée.</span><span class="sxs-lookup"><span data-stu-id="27b95-215">The encrypted API key.</span></span> |

<span data-ttu-id="27b95-216">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="27b95-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="27b95-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="27b95-217">disabledPackageSources</span></span>

<span data-ttu-id="27b95-218">Identifie les sources actuellement désactivées.</span><span class="sxs-lookup"><span data-stu-id="27b95-218">Identified currently disabled sources.</span></span> <span data-ttu-id="27b95-219">Peut être vide.</span><span class="sxs-lookup"><span data-stu-id="27b95-219">May be empty.</span></span>

| <span data-ttu-id="27b95-220">Touche</span><span class="sxs-lookup"><span data-stu-id="27b95-220">Key</span></span> | <span data-ttu-id="27b95-221">Value</span><span class="sxs-lookup"><span data-stu-id="27b95-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="27b95-222">(nom de source)</span><span class="sxs-lookup"><span data-stu-id="27b95-222">(name of source)</span></span> | <span data-ttu-id="27b95-223">Valeur booléenne indiquant si la source est désactivée.</span><span class="sxs-lookup"><span data-stu-id="27b95-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="27b95-224">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="27b95-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="27b95-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="27b95-225">activePackageSource</span></span>

<span data-ttu-id="27b95-226">*(2.x uniquement ; déprécié dans 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="27b95-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="27b95-227">Identifie la source actuellement active ou indique l’agrégat de toutes les sources.</span><span class="sxs-lookup"><span data-stu-id="27b95-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="27b95-228">Touche</span><span class="sxs-lookup"><span data-stu-id="27b95-228">Key</span></span> | <span data-ttu-id="27b95-229">Value</span><span class="sxs-lookup"><span data-stu-id="27b95-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="27b95-230">(nom de source) ou `All`</span><span class="sxs-lookup"><span data-stu-id="27b95-230">(name of source) or `All`</span></span> | <span data-ttu-id="27b95-231">Si la clé est le nom d’une source, la valeur est le chemin ou l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="27b95-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="27b95-232">Si la clé est `All`, la valeur doit être `(Aggregate source)` pour combiner toutes les sources de packages qui ne sont pas autrement désactivées.</span><span class="sxs-lookup"><span data-stu-id="27b95-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="27b95-233">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="27b95-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="27b95-234">section de trustedSigners</span><span class="sxs-lookup"><span data-stu-id="27b95-234">trustedSigners section</span></span>

<span data-ttu-id="27b95-235">Magasins approuvé utilisés pour permettre de package lors de l’installation ou la restauration des signataires.</span><span class="sxs-lookup"><span data-stu-id="27b95-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="27b95-236">Cette liste ne peut pas être vide lorsque l’utilisateur définit `signatureValidationMode` à `require`.</span><span class="sxs-lookup"><span data-stu-id="27b95-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="27b95-237">Cette section peut être mis à jour avec la [ `nuget trusted-signers` commande](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="27b95-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="27b95-238">**Schéma**:</span><span class="sxs-lookup"><span data-stu-id="27b95-238">**Schema**:</span></span>

<span data-ttu-id="27b95-239">Un signataire approuvé possède une collection de `certificate` éléments inscrire tous les certificats qui identifient un signataire donné.</span><span class="sxs-lookup"><span data-stu-id="27b95-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="27b95-240">Un signataire approuvé peut être un `Author` ou un `Repository`.</span><span class="sxs-lookup"><span data-stu-id="27b95-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="27b95-241">Approuvé *référentiel* spécifie également le `serviceIndex` pour le dépôt (qui doit être valide `https` uri) et vous pouvez éventuellement spécifier une liste délimitée par des points-virgules de `owners` pour limiter encore plus qui est approuvé à partir de ce référentiel spécifique.</span><span class="sxs-lookup"><span data-stu-id="27b95-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="27b95-242">Les algorithmes de hachage pris en charge utilisés pour une empreinte de certificat sont `SHA256`, `SHA384` et `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="27b95-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="27b95-243">Si un `certificate` spécifie `allowUntrustedRoot` comme `true` le certificat donné est autorisé à la chaîne à une racine non approuvée pendant la génération de la chaîne de certificats dans le cadre de la vérification de signature.</span><span class="sxs-lookup"><span data-stu-id="27b95-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="27b95-244">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="27b95-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="27b95-245">Utilisation de variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="27b95-245">Using environment variables</span></span>

<span data-ttu-id="27b95-246">Vous pouvez utiliser des variables d’environnement dans les valeurs `nuget.config` (NuGet 3.4+) pour appliquer des paramètres au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="27b95-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="27b95-247">Par exemple, si la variable d’environnement `HOME` sur Windows a la valeur `c:\users\username`, la valeur `%HOME%\NuGetRepository` dans le fichier de configuration correspond à `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="27b95-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="27b95-248">De même, si `HOME` sur Mac/Linux a la valeur `/home/myStuff`, `%HOME%/NuGetRepository` dans le fichier de configuration correspond à `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="27b95-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="27b95-249">Si aucune variable d’environnement n’est trouvée, NuGet utilise la valeur littérale du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="27b95-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="27b95-250">Exemple de fichier config</span><span class="sxs-lookup"><span data-stu-id="27b95-250">Example config file</span></span>

<span data-ttu-id="27b95-251">Voici un exemple de fichier `nuget.config` qui illustre un certain nombre de paramètres :</span><span class="sxs-lookup"><span data-stu-id="27b95-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
