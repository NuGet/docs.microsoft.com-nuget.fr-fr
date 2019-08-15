---
title: informations de référence sur le fichier NuGet. config
description: Informations de référence sur le fichier NuGet.Config, notamment les sections config, bindingRedirects, packageRestore, solution et packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: a2955617b899bfadab42d1ae98dd20c8fc6ddca9
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020050"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="f7a7c-103">informations de référence sur NuGet. config</span><span class="sxs-lookup"><span data-stu-id="f7a7c-103">nuget.config reference</span></span>

<span data-ttu-id="f7a7c-104">Le comportement de NuGet est contrôlé par des `NuGet.Config` paramètres dans des fichiers différents, comme décrit dans [configurations courantes de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="f7a7c-105">`nuget.config` est un fichier XML contenant un nœud `<configuration>` de niveau supérieur qui comprend à son tour les éléments de section décrits dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="f7a7c-106">Chaque section contient zéro ou plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-106">Each section contains zero or more items.</span></span> <span data-ttu-id="f7a7c-107">Consultez [l’exemple de fichier config](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="f7a7c-108">Les noms de paramètre ne respectent pas la casse et les valeurs peuvent utiliser des [variables d’environnement](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="f7a7c-109">Section config</span><span class="sxs-lookup"><span data-stu-id="f7a7c-109">config section</span></span>

<span data-ttu-id="f7a7c-110">Contient des paramètres de configuration divers, qui peuvent être définis à l’aide de la [commande `nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="f7a7c-111">`dependencyVersion`et `repositoryPath` s’appliquent uniquement aux `packages.config`projets à l’aide de.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="f7a7c-112">`globalPackagesFolder`s’applique uniquement aux projets utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="f7a7c-113">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-113">Key</span></span> | <span data-ttu-id="f7a7c-114">Valeur</span><span class="sxs-lookup"><span data-stu-id="f7a7c-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-115">dependencyVersion (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="f7a7c-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="f7a7c-116">Valeur `DependencyVersion` par défaut pour l’installation, la restauration et la mise à jour de package, quand le commutateur `-DependencyVersion` n’est pas spécifié directement.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="f7a7c-117">Cette valeur est également utilisée par l’interface utilisateur du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="f7a7c-118">Les valeurs sont `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="f7a7c-119">globalPackagesFolder (projets utilisant PackageReference uniquement)</span><span class="sxs-lookup"><span data-stu-id="f7a7c-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="f7a7c-120">Emplacement du dossier de packages global par défaut.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-120">The location of the default global packages folder.</span></span> <span data-ttu-id="f7a7c-121">L’emplacement par défaut est `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="f7a7c-122">Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="f7a7c-123">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="f7a7c-124">repositoryPath (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="f7a7c-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="f7a7c-125">Emplacement dans lequel installer les packages NuGet au lieu du dossier `$(Solutiondir)/packages` par défaut.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="f7a7c-126">Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="f7a7c-127">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="f7a7c-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="f7a7c-128">defaultPushSource</span></span> | <span data-ttu-id="f7a7c-129">Identifie l’URL ou le chemin de la source du package qui doit être utilisée comme valeur par défaut si aucune autre source de package n’est trouvée pour une opération.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="f7a7c-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="f7a7c-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="f7a7c-131">Paramètres de proxy à utiliser lors de la connexion aux sources de packages ; `http_proxy` doit être au format `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="f7a7c-132">Les mots de passe sont chiffrés et ne peuvent pas être ajoutés manuellement.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="f7a7c-133">Pour `no_proxy`, la valeur est une liste de domaines séparés par des virgules qui ignorent le serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="f7a7c-134">Vous pouvez également utiliser les variables d’environnement http_proxy et no_proxy pour ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="f7a7c-135">Pour plus d’informations, consultez [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="f7a7c-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="f7a7c-136">signatureValidationMode</span></span> | <span data-ttu-id="f7a7c-137">Spécifie le mode de validation utilisé pour vérifier les signatures de package pour l’installation du package et la restauration.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="f7a7c-138">Les valeurs `accept`sont `require`,.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="f7a7c-139">La valeur par défaut est `accept`.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-139">Defaults to `accept`.</span></span>

<span data-ttu-id="f7a7c-140">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="f7a7c-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="f7a7c-141">Section bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="f7a7c-141">bindingRedirects section</span></span>

<span data-ttu-id="f7a7c-142">Définit si NuGet effectue des redirections de liaisons automatiques quand un package est installé.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="f7a7c-143">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-143">Key</span></span> | <span data-ttu-id="f7a7c-144">Valeur</span><span class="sxs-lookup"><span data-stu-id="f7a7c-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-145">skip</span><span class="sxs-lookup"><span data-stu-id="f7a7c-145">skip</span></span> | <span data-ttu-id="f7a7c-146">Valeur booléenne indiquant s’il faut ignorer les redirections de liaisons automatiques.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="f7a7c-147">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-147">The default is false.</span></span> |

<span data-ttu-id="f7a7c-148">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="f7a7c-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="f7a7c-149">Section packageRestore</span><span class="sxs-lookup"><span data-stu-id="f7a7c-149">packageRestore section</span></span>

<span data-ttu-id="f7a7c-150">Contrôle la restauration de packages pendant les générations.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="f7a7c-151">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-151">Key</span></span> | <span data-ttu-id="f7a7c-152">Valeur</span><span class="sxs-lookup"><span data-stu-id="f7a7c-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-153">enabled</span><span class="sxs-lookup"><span data-stu-id="f7a7c-153">enabled</span></span> | <span data-ttu-id="f7a7c-154">Valeur booléenne indiquant si NuGet peut effectuer une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="f7a7c-155">Vous pouvez également définir la variable d’environnement `EnableNuGetPackageRestore` avec la valeur `True` au lieu de définir cette clé dans le fichier config.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="f7a7c-156">automatique</span><span class="sxs-lookup"><span data-stu-id="f7a7c-156">automatic</span></span> | <span data-ttu-id="f7a7c-157">Valeur booléenne indiquant si NuGet doit rechercher les packages manquants pendant une génération.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="f7a7c-158">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="f7a7c-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="f7a7c-159">Section solution</span><span class="sxs-lookup"><span data-stu-id="f7a7c-159">solution section</span></span>

<span data-ttu-id="f7a7c-160">Contrôle si le dossier `packages` d’une solution est inclus dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="f7a7c-161">Cette section fonctionne uniquement dans les fichiers `nuget.config` dans un dossier de solution.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="f7a7c-162">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-162">Key</span></span> | <span data-ttu-id="f7a7c-163">Valeur</span><span class="sxs-lookup"><span data-stu-id="f7a7c-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="f7a7c-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="f7a7c-165">Valeur booléenne indiquant s’il faut ignorer le dossier de packages lors de l’utilisation de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="f7a7c-166">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-166">The default value is false.</span></span> |

<span data-ttu-id="f7a7c-167">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="f7a7c-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="f7a7c-168">Sections sur les sources de packages</span><span class="sxs-lookup"><span data-stu-id="f7a7c-168">Package source sections</span></span>

<span data-ttu-id="f7a7c-169">Les `packageSources`fonctions `packageSourceCredentials`,, `apikeys`, etfonctionnentensemblepour`disabledPackageSources` configurer la façon dont NuGet fonctionne avec les référentiels de packages pendant les opérations d’installation, de restauration et de mise à jour. `trustedSigners` `activePackageSource`</span><span class="sxs-lookup"><span data-stu-id="f7a7c-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="f7a7c-170">La `apikeys` `trustedSigners` [ `nuget sources` commande](../reference/cli-reference/cli-ref-sources.md) est généralement utilisée pour gérer ces paramètres, à l’exception de qui est géré à l’aide de la [ `nuget setapikey` commande](../reference/cli-reference/cli-ref-setapikey.md)et qui est gérée à l’aide de la [ `nuget trusted-signers` commande](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="f7a7c-171">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="f7a7c-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="f7a7c-172">packageSources</span></span>

<span data-ttu-id="f7a7c-173">Répertorie toutes les sources de packages connues.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-173">Lists all known package sources.</span></span> <span data-ttu-id="f7a7c-174">L’ordre est ignoré pendant les opérations de restauration et avec n’importe quel projet utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="f7a7c-175">NuGet respecte l’ordre des sources pour les opérations d’installation et de mise `packages.config`à jour des projets à l’aide de.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="f7a7c-176">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-176">Key</span></span> | <span data-ttu-id="f7a7c-177">Valeur</span><span class="sxs-lookup"><span data-stu-id="f7a7c-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-178">(nom à assigner à la source du package)</span><span class="sxs-lookup"><span data-stu-id="f7a7c-178">(name to assign to the package source)</span></span> | <span data-ttu-id="f7a7c-179">Chemin ou URL de la source du package.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="f7a7c-180">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="f7a7c-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="f7a7c-181">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="f7a7c-181">packageSourceCredentials</span></span>

<span data-ttu-id="f7a7c-182">Stocke les noms d’utilisateur et mots de passe pour les sources, spécifiés en général en utilisant les commutateurs `-username` et `-password` avec `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-182">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="f7a7c-183">Les mots de passe sont chiffrés par défaut, sauf si l’option `-storepasswordincleartext` est également utilisée.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-183">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="f7a7c-184">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-184">Key</span></span> | <span data-ttu-id="f7a7c-185">`Value`</span><span class="sxs-lookup"><span data-stu-id="f7a7c-185">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-186">username</span><span class="sxs-lookup"><span data-stu-id="f7a7c-186">username</span></span> | <span data-ttu-id="f7a7c-187">Nom d’utilisateur pour la source en texte brut.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-187">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="f7a7c-188">password</span><span class="sxs-lookup"><span data-stu-id="f7a7c-188">password</span></span> | <span data-ttu-id="f7a7c-189">Mot de passe chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-189">The encrypted password for the source.</span></span> |
| <span data-ttu-id="f7a7c-190">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="f7a7c-190">cleartextpassword</span></span> | <span data-ttu-id="f7a7c-191">Mot de passe non chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-191">The unencrypted password for the source.</span></span> |

<span data-ttu-id="f7a7c-192">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="f7a7c-192">**Example:**</span></span>

<span data-ttu-id="f7a7c-193">Dans le fichier config, l’élément `<packageSourceCredentials>` contient des nœuds enfants pour chaque nom de source applicable (les espaces dans le nom sont remplacés par `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-193">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="f7a7c-194">Autrement dit, pour les sources nommées « Contoso » et « Test Source », le fichier config contient les éléments suivants lors de l’utilisation de mots de passe chiffrés :</span><span class="sxs-lookup"><span data-stu-id="f7a7c-194">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="f7a7c-195">Lors de l’utilisation de mots de passe non chiffrés :</span><span class="sxs-lookup"><span data-stu-id="f7a7c-195">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="f7a7c-196">apikeys</span><span class="sxs-lookup"><span data-stu-id="f7a7c-196">apikeys</span></span>

<span data-ttu-id="f7a7c-197">Stocke les clés pour les sources qui utilisent l’authentification de clé API, comme défini avec la [commande `nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-197">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="f7a7c-198">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-198">Key</span></span> | <span data-ttu-id="f7a7c-199">Valeur</span><span class="sxs-lookup"><span data-stu-id="f7a7c-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-200">(URL source)</span><span class="sxs-lookup"><span data-stu-id="f7a7c-200">(source URL)</span></span> | <span data-ttu-id="f7a7c-201">Clé API chiffrée.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-201">The encrypted API key.</span></span> |

<span data-ttu-id="f7a7c-202">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="f7a7c-202">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="f7a7c-203">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="f7a7c-203">disabledPackageSources</span></span>

<span data-ttu-id="f7a7c-204">Identifie les sources actuellement désactivées.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-204">Identified currently disabled sources.</span></span> <span data-ttu-id="f7a7c-205">Peut être vide.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-205">May be empty.</span></span>

| <span data-ttu-id="f7a7c-206">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-206">Key</span></span> | <span data-ttu-id="f7a7c-207">Valeur</span><span class="sxs-lookup"><span data-stu-id="f7a7c-207">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-208">(nom de source)</span><span class="sxs-lookup"><span data-stu-id="f7a7c-208">(name of source)</span></span> | <span data-ttu-id="f7a7c-209">Valeur booléenne indiquant si la source est désactivée.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-209">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="f7a7c-210">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="f7a7c-210">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="f7a7c-211">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="f7a7c-211">activePackageSource</span></span>

<span data-ttu-id="f7a7c-212">*(2.x uniquement ; déprécié dans 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="f7a7c-212">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="f7a7c-213">Identifie la source actuellement active ou indique l’agrégat de toutes les sources.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-213">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="f7a7c-214">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-214">Key</span></span> | <span data-ttu-id="f7a7c-215">Valeur</span><span class="sxs-lookup"><span data-stu-id="f7a7c-215">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-216">(nom de source) ou `All`</span><span class="sxs-lookup"><span data-stu-id="f7a7c-216">(name of source) or `All`</span></span> | <span data-ttu-id="f7a7c-217">Si la clé est le nom d’une source, la valeur est le chemin ou l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-217">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="f7a7c-218">Si la clé est `All`, la valeur doit être `(Aggregate source)` pour combiner toutes les sources de packages qui ne sont pas autrement désactivées.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-218">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="f7a7c-219">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="f7a7c-219">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="f7a7c-220">section trustedSigners</span><span class="sxs-lookup"><span data-stu-id="f7a7c-220">trustedSigners section</span></span>

<span data-ttu-id="f7a7c-221">Stocke les signataires approuvés utilisés pour autoriser le package lors de l’installation ou de la restauration.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-221">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="f7a7c-222">Cette liste ne peut pas être vide lorsque l' `signatureValidationMode` utilisateur `require`affecte à la valeur.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-222">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="f7a7c-223">Cette section peut être mise à jour à l’aide de la [ `nuget trusted-signers` commande](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="f7a7c-223">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="f7a7c-224">**Schéma** :</span><span class="sxs-lookup"><span data-stu-id="f7a7c-224">**Schema**:</span></span>

<span data-ttu-id="f7a7c-225">Un signataire approuvé contient une collection d' `certificate` éléments qui inscrivent tous les certificats qui identifient un signataire donné.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-225">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="f7a7c-226">Un signataire approuvé peut être `Author` un ou un. `Repository`</span><span class="sxs-lookup"><span data-stu-id="f7a7c-226">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="f7a7c-227">Un *référentiel* approuvé spécifie également le `serviceIndex` pour le référentiel (qui doit être un URI valide `https` ) et peut éventuellement spécifier une liste délimitée par des `owners` points-virgules pour limiter encore plus la confiance de ce référentiel.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-227">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="f7a7c-228">Les algorithmes de hachage pris en charge utilisés pour une `SHA256`empreinte `SHA384` digitale `SHA512`de certificat sont, et.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-228">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="f7a7c-229">Si un `certificate` `allowUntrustedRoot` spécifie `true` en tant que certificat donné, il est autorisé à effectuer une chaîne sur une racine non approuvée lors de la génération de la chaîne de certificats dans le cadre de la vérification de la signature.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-229">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="f7a7c-230">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="f7a7c-230">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="f7a7c-231">section fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="f7a7c-231">fallbackPackageFolders section</span></span>

<span data-ttu-id="f7a7c-232">*(3.5 +)* Fournit un moyen de préinstaller des packages afin qu’aucun travail ne doive être effectué si le package se trouve dans les dossiers de secours.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-232">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="f7a7c-233">Les dossiers de package de secours ont exactement la même structure de dossiers et de fichiers que le dossier de package global: *. nupkg* est présent et tous les fichiers sont extraits.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-233">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="f7a7c-234">La logique de recherche pour cette configuration est la suivante:</span><span class="sxs-lookup"><span data-stu-id="f7a7c-234">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="f7a7c-235">Recherchez dans le dossier de package global pour voir si le package/la version est déjà téléchargé.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-235">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="f7a7c-236">Recherchez dans les dossiers de secours un package/version correspondant.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-236">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="f7a7c-237">Si une recherche est réussie, aucun téléchargement n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-237">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="f7a7c-238">Si aucune correspondance n’est trouvée, NuGet vérifie les sources de fichiers, puis les sources http, puis télécharge les packages.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-238">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="f7a7c-239">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-239">Key</span></span> | <span data-ttu-id="f7a7c-240">Valeur</span><span class="sxs-lookup"><span data-stu-id="f7a7c-240">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-241">(nom du dossier de secours)</span><span class="sxs-lookup"><span data-stu-id="f7a7c-241">(name of fallback folder)</span></span> | <span data-ttu-id="f7a7c-242">Chemin d’accès au dossier de secours.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-242">Path to fallback folder.</span></span> |

<span data-ttu-id="f7a7c-243">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="f7a7c-243">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="f7a7c-244">packageManagement (section)</span><span class="sxs-lookup"><span data-stu-id="f7a7c-244">packageManagement section</span></span>

<span data-ttu-id="f7a7c-245">Définit le format de gestion de package par défaut, *packages. config* ou PackageReference.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-245">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="f7a7c-246">Les projets de style SDK utilisent toujours PackageReference.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-246">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="f7a7c-247">Clé</span><span class="sxs-lookup"><span data-stu-id="f7a7c-247">Key</span></span> | <span data-ttu-id="f7a7c-248">`Value`</span><span class="sxs-lookup"><span data-stu-id="f7a7c-248">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f7a7c-249">format</span><span class="sxs-lookup"><span data-stu-id="f7a7c-249">format</span></span> | <span data-ttu-id="f7a7c-250">Valeur booléenne qui indique le format de gestion des packages par défaut.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-250">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="f7a7c-251">Si `1`, format est PackageReference.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-251">If `1`, format is PackageReference.</span></span> <span data-ttu-id="f7a7c-252">Si `0`la forme est, le format est *packages. config*.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-252">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="f7a7c-253">désactivés</span><span class="sxs-lookup"><span data-stu-id="f7a7c-253">disabled</span></span> | <span data-ttu-id="f7a7c-254">Valeur booléenne indiquant s’il faut afficher l’invite de sélection d’un format de package par défaut lors de la première installation de package.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-254">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="f7a7c-255">`False`masque l’invite.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-255">`False` hides the prompt.</span></span> |

<span data-ttu-id="f7a7c-256">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="f7a7c-256">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="f7a7c-257">Utilisation de variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="f7a7c-257">Using environment variables</span></span>

<span data-ttu-id="f7a7c-258">Vous pouvez utiliser des variables d’environnement dans les valeurs `nuget.config` (NuGet 3.4+) pour appliquer des paramètres au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-258">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="f7a7c-259">Par exemple, si la variable d’environnement `HOME` sur Windows a la valeur `c:\users\username`, la valeur `%HOME%\NuGetRepository` dans le fichier de configuration correspond à `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-259">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="f7a7c-260">De même, si `HOME` sur Mac/Linux a la valeur `/home/myStuff`, `%HOME%/NuGetRepository` dans le fichier de configuration correspond à `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-260">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="f7a7c-261">Si aucune variable d’environnement n’est trouvée, NuGet utilise la valeur littérale du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="f7a7c-261">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="f7a7c-262">Exemple de fichier config</span><span class="sxs-lookup"><span data-stu-id="f7a7c-262">Example config file</span></span>

<span data-ttu-id="f7a7c-263">Voici un exemple de fichier `nuget.config` qui illustre un certain nombre de paramètres :</span><span class="sxs-lookup"><span data-stu-id="f7a7c-263">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
