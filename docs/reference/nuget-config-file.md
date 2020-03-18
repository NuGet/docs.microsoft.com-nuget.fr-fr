---
title: informations de référence sur le fichier NuGet. config
description: Informations de référence sur le fichier NuGet.Config, notamment les sections config, bindingRedirects, packageRestore, solution et packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429128"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="3aab2-103">informations de référence sur NuGet. config</span><span class="sxs-lookup"><span data-stu-id="3aab2-103">nuget.config reference</span></span>

<span data-ttu-id="3aab2-104">Le comportement de NuGet est contrôlé par des paramètres dans différents fichiers `NuGet.Config` ou `nuget.config`, comme décrit dans [configurations NuGet courantes](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3aab2-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="3aab2-105">`nuget.config` est un fichier XML contenant un nœud `<configuration>` de niveau supérieur qui comprend à son tour les éléments de section décrits dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="3aab2-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="3aab2-106">Chaque section contient zéro ou plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="3aab2-106">Each section contains zero or more items.</span></span> <span data-ttu-id="3aab2-107">Consultez [l’exemple de fichier config](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="3aab2-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="3aab2-108">Les noms de paramètre ne respectent pas la casse et les valeurs peuvent utiliser des [variables d’environnement](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="3aab2-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="3aab2-109">Section config</span><span class="sxs-lookup"><span data-stu-id="3aab2-109">config section</span></span>

<span data-ttu-id="3aab2-110">Contient des paramètres de configuration divers, qui peuvent être définis à l’aide de la [commande `nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="3aab2-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="3aab2-111">`dependencyVersion` et `repositoryPath` s’appliquent uniquement aux projets utilisant `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="3aab2-112">`globalPackagesFolder` s’applique uniquement aux projets utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3aab2-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="3aab2-113">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-113">Key</span></span> | <span data-ttu-id="3aab2-114">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-115">dependencyVersion (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="3aab2-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="3aab2-116">Valeur `DependencyVersion` par défaut pour l’installation, la restauration et la mise à jour de package, quand le commutateur `-DependencyVersion` n’est pas spécifié directement.</span><span class="sxs-lookup"><span data-stu-id="3aab2-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="3aab2-117">Cette valeur est également utilisée par l’interface utilisateur du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="3aab2-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="3aab2-118">Les valeurs sont `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="3aab2-119">globalPackagesFolder (projets utilisant PackageReference uniquement)</span><span class="sxs-lookup"><span data-stu-id="3aab2-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="3aab2-120">Emplacement du dossier de packages global par défaut.</span><span class="sxs-lookup"><span data-stu-id="3aab2-120">The location of the default global packages folder.</span></span> <span data-ttu-id="3aab2-121">L’emplacement par défaut est `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="3aab2-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="3aab2-122">Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="3aab2-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3aab2-123">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="3aab2-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3aab2-124">repositoryPath (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="3aab2-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="3aab2-125">Emplacement dans lequel installer les packages NuGet au lieu du dossier `$(Solutiondir)/packages` par défaut.</span><span class="sxs-lookup"><span data-stu-id="3aab2-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="3aab2-126">Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="3aab2-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3aab2-127">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="3aab2-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3aab2-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="3aab2-128">defaultPushSource</span></span> | <span data-ttu-id="3aab2-129">Identifie l’URL ou le chemin de la source du package qui doit être utilisée comme valeur par défaut si aucune autre source de package n’est trouvée pour une opération.</span><span class="sxs-lookup"><span data-stu-id="3aab2-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="3aab2-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="3aab2-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="3aab2-131">Paramètres de proxy à utiliser lors de la connexion aux sources de packages ; `http_proxy` doit être au format `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="3aab2-132">Les mots de passe sont chiffrés et ne peuvent pas être ajoutés manuellement.</span><span class="sxs-lookup"><span data-stu-id="3aab2-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="3aab2-133">Pour `no_proxy`, la valeur est une liste de domaines séparés par des virgules qui ignorent le serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="3aab2-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="3aab2-134">Vous pouvez également utiliser les variables d’environnement http_proxy et no_proxy pour ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="3aab2-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="3aab2-135">Pour plus d’informations, consultez [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="3aab2-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="3aab2-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="3aab2-136">signatureValidationMode</span></span> | <span data-ttu-id="3aab2-137">Spécifie le mode de validation utilisé pour vérifier les signatures de package pour l’installation du package et la restauration.</span><span class="sxs-lookup"><span data-stu-id="3aab2-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="3aab2-138">Les valeurs sont `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="3aab2-139">La valeur par défaut est `accept`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-139">Defaults to `accept`.</span></span>

<span data-ttu-id="3aab2-140">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="3aab2-141">Section bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="3aab2-141">bindingRedirects section</span></span>

<span data-ttu-id="3aab2-142">Définit si NuGet effectue des redirections de liaisons automatiques quand un package est installé.</span><span class="sxs-lookup"><span data-stu-id="3aab2-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="3aab2-143">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-143">Key</span></span> | <span data-ttu-id="3aab2-144">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-145">skip</span><span class="sxs-lookup"><span data-stu-id="3aab2-145">skip</span></span> | <span data-ttu-id="3aab2-146">Valeur booléenne indiquant s’il faut ignorer les redirections de liaisons automatiques.</span><span class="sxs-lookup"><span data-stu-id="3aab2-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="3aab2-147">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="3aab2-147">The default is false.</span></span> |

<span data-ttu-id="3aab2-148">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="3aab2-149">Section packageRestore</span><span class="sxs-lookup"><span data-stu-id="3aab2-149">packageRestore section</span></span>

<span data-ttu-id="3aab2-150">Contrôle la restauration de packages pendant les générations.</span><span class="sxs-lookup"><span data-stu-id="3aab2-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="3aab2-151">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-151">Key</span></span> | <span data-ttu-id="3aab2-152">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-153">enabled</span><span class="sxs-lookup"><span data-stu-id="3aab2-153">enabled</span></span> | <span data-ttu-id="3aab2-154">Valeur booléenne indiquant si NuGet peut effectuer une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="3aab2-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="3aab2-155">Vous pouvez également définir la variable d’environnement `EnableNuGetPackageRestore` avec la valeur `True` au lieu de définir cette clé dans le fichier config.</span><span class="sxs-lookup"><span data-stu-id="3aab2-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="3aab2-156">automatique</span><span class="sxs-lookup"><span data-stu-id="3aab2-156">automatic</span></span> | <span data-ttu-id="3aab2-157">Valeur booléenne indiquant si NuGet doit rechercher les packages manquants pendant une génération.</span><span class="sxs-lookup"><span data-stu-id="3aab2-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="3aab2-158">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="3aab2-159">Section solution</span><span class="sxs-lookup"><span data-stu-id="3aab2-159">solution section</span></span>

<span data-ttu-id="3aab2-160">Contrôle si le dossier `packages` d’une solution est inclus dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="3aab2-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="3aab2-161">Cette section fonctionne uniquement dans les fichiers `nuget.config` dans un dossier de solution.</span><span class="sxs-lookup"><span data-stu-id="3aab2-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="3aab2-162">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-162">Key</span></span> | <span data-ttu-id="3aab2-163">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="3aab2-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="3aab2-165">Valeur booléenne indiquant s’il faut ignorer le dossier de packages lors de l’utilisation de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="3aab2-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="3aab2-166">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="3aab2-166">The default value is false.</span></span> |

<span data-ttu-id="3aab2-167">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="3aab2-168">Sections sur les sources de packages</span><span class="sxs-lookup"><span data-stu-id="3aab2-168">Package source sections</span></span>

<span data-ttu-id="3aab2-169">Les `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` et `trustedSigners` fonctionnent ensemble pour configurer la façon dont NuGet fonctionne avec les dépôts de packages pendant les opérations d’installation, de restauration et de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="3aab2-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="3aab2-170">La [commande`nuget sources`](../reference/cli-reference/cli-ref-sources.md) est généralement utilisée pour gérer ces paramètres, à l’exception de `apikeys` qui est gérée à l’aide de la [commande`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md)et `trustedSigners` qui est gérée à l’aide de la [commande`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="3aab2-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="3aab2-171">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="3aab2-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="3aab2-172">packageSources</span></span>

<span data-ttu-id="3aab2-173">Répertorie toutes les sources de packages connues.</span><span class="sxs-lookup"><span data-stu-id="3aab2-173">Lists all known package sources.</span></span> <span data-ttu-id="3aab2-174">L’ordre est ignoré pendant les opérations de restauration et avec n’importe quel projet utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3aab2-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="3aab2-175">NuGet respecte l’ordre des sources pour les opérations d’installation et de mise à jour des projets à l’aide de `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="3aab2-176">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-176">Key</span></span> | <span data-ttu-id="3aab2-177">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-178">(nom à assigner à la source du package)</span><span class="sxs-lookup"><span data-stu-id="3aab2-178">(name to assign to the package source)</span></span> | <span data-ttu-id="3aab2-179">Chemin ou URL de la source du package.</span><span class="sxs-lookup"><span data-stu-id="3aab2-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="3aab2-180">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="3aab2-181">Lorsque `<clear />` est présent pour un nœud donné, NuGet ignore les valeurs de configuration définies précédemment pour ce nœud.</span><span class="sxs-lookup"><span data-stu-id="3aab2-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="3aab2-182">[En savoir plus sur la façon dont les paramètres sont appliqués](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="3aab2-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="3aab2-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="3aab2-183">packageSourceCredentials</span></span>

<span data-ttu-id="3aab2-184">Stocke les noms d’utilisateur et mots de passe pour les sources, spécifiés en général en utilisant les commutateurs `-username` et `-password` avec `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="3aab2-185">Les mots de passe sont chiffrés par défaut, sauf si l’option `-storepasswordincleartext` est également utilisée.</span><span class="sxs-lookup"><span data-stu-id="3aab2-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="3aab2-186">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-186">Key</span></span> | <span data-ttu-id="3aab2-187">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-188">username</span><span class="sxs-lookup"><span data-stu-id="3aab2-188">username</span></span> | <span data-ttu-id="3aab2-189">Nom d’utilisateur pour la source en texte brut.</span><span class="sxs-lookup"><span data-stu-id="3aab2-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="3aab2-190">password</span><span class="sxs-lookup"><span data-stu-id="3aab2-190">password</span></span> | <span data-ttu-id="3aab2-191">Mot de passe chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="3aab2-191">The encrypted password for the source.</span></span> |
| <span data-ttu-id="3aab2-192">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="3aab2-192">cleartextpassword</span></span> | <span data-ttu-id="3aab2-193">Mot de passe non chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="3aab2-193">The unencrypted password for the source.</span></span> |

<span data-ttu-id="3aab2-194">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="3aab2-194">**Example:**</span></span>

<span data-ttu-id="3aab2-195">Dans le fichier config, l’élément `<packageSourceCredentials>` contient des nœuds enfants pour chaque nom de source applicable (les espaces dans le nom sont remplacés par `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="3aab2-195">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="3aab2-196">Autrement dit, pour les sources nommées « Contoso » et « Test Source », le fichier config contient les éléments suivants lors de l’utilisation de mots de passe chiffrés :</span><span class="sxs-lookup"><span data-stu-id="3aab2-196">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="3aab2-197">Lors de l’utilisation de mots de passe non chiffrés :</span><span class="sxs-lookup"><span data-stu-id="3aab2-197">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="3aab2-198">apikeys</span><span class="sxs-lookup"><span data-stu-id="3aab2-198">apikeys</span></span>

<span data-ttu-id="3aab2-199">Stocke les clés pour les sources qui utilisent l’authentification de clé API, comme défini avec la [commande `nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="3aab2-199">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="3aab2-200">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-200">Key</span></span> | <span data-ttu-id="3aab2-201">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-201">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-202">(URL source)</span><span class="sxs-lookup"><span data-stu-id="3aab2-202">(source URL)</span></span> | <span data-ttu-id="3aab2-203">Clé API chiffrée.</span><span class="sxs-lookup"><span data-stu-id="3aab2-203">The encrypted API key.</span></span> |

<span data-ttu-id="3aab2-204">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-204">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="3aab2-205">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="3aab2-205">disabledPackageSources</span></span>

<span data-ttu-id="3aab2-206">Identifie les sources actuellement désactivées.</span><span class="sxs-lookup"><span data-stu-id="3aab2-206">Identified currently disabled sources.</span></span> <span data-ttu-id="3aab2-207">Peut être vide.</span><span class="sxs-lookup"><span data-stu-id="3aab2-207">May be empty.</span></span>

| <span data-ttu-id="3aab2-208">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-208">Key</span></span> | <span data-ttu-id="3aab2-209">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-210">(nom de source)</span><span class="sxs-lookup"><span data-stu-id="3aab2-210">(name of source)</span></span> | <span data-ttu-id="3aab2-211">Valeur booléenne indiquant si la source est désactivée.</span><span class="sxs-lookup"><span data-stu-id="3aab2-211">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="3aab2-212">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="3aab2-212">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="3aab2-213">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="3aab2-213">activePackageSource</span></span>

<span data-ttu-id="3aab2-214">*(2.x uniquement ; déprécié dans 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="3aab2-214">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="3aab2-215">Identifie la source actuellement active ou indique l’agrégat de toutes les sources.</span><span class="sxs-lookup"><span data-stu-id="3aab2-215">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="3aab2-216">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-216">Key</span></span> | <span data-ttu-id="3aab2-217">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-218">(nom de source) ou `All`</span><span class="sxs-lookup"><span data-stu-id="3aab2-218">(name of source) or `All`</span></span> | <span data-ttu-id="3aab2-219">Si la clé est le nom d’une source, la valeur est le chemin ou l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="3aab2-219">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="3aab2-220">Si la clé est `All`, la valeur doit être `(Aggregate source)` pour combiner toutes les sources de packages qui ne sont pas autrement désactivées.</span><span class="sxs-lookup"><span data-stu-id="3aab2-220">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="3aab2-221">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-221">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="3aab2-222">section trustedSigners</span><span class="sxs-lookup"><span data-stu-id="3aab2-222">trustedSigners section</span></span>

<span data-ttu-id="3aab2-223">Stocke les signataires approuvés utilisés pour autoriser le package lors de l’installation ou de la restauration.</span><span class="sxs-lookup"><span data-stu-id="3aab2-223">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="3aab2-224">Cette liste ne peut pas être vide lorsque l’utilisateur définit `signatureValidationMode` sur `require`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-224">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="3aab2-225">Cette section peut être mise à jour à l’aide de la [commande`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="3aab2-225">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="3aab2-226">**Schéma** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-226">**Schema**:</span></span>

<span data-ttu-id="3aab2-227">Un signataire approuvé contient une collection d’éléments `certificate` qui inscrivent tous les certificats qui identifient un signataire donné.</span><span class="sxs-lookup"><span data-stu-id="3aab2-227">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="3aab2-228">Un signataire approuvé peut être un `Author` ou un `Repository`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-228">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="3aab2-229">Un *référentiel* approuvé spécifie également les `serviceIndex` pour le dépôt (qui doit être un URI `https` valide) et peut éventuellement spécifier une liste de `owners` délimitée par des points-virgules pour limiter encore plus les personnes autorisées à partir de ce référentiel spécifique.</span><span class="sxs-lookup"><span data-stu-id="3aab2-229">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="3aab2-230">Les algorithmes de hachage pris en charge utilisés pour une empreinte digitale de certificat sont `SHA256`, `SHA384` et `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-230">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="3aab2-231">Si un `certificate` spécifie `allowUntrustedRoot` comme `true` le certificat donné est autorisé à se lier à une racine non approuvée lors de la génération de la chaîne de certificats dans le cadre de la vérification de la signature.</span><span class="sxs-lookup"><span data-stu-id="3aab2-231">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="3aab2-232">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-232">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="3aab2-233">section fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="3aab2-233">fallbackPackageFolders section</span></span>

<span data-ttu-id="3aab2-234">*(3.5 +)* Fournit un moyen de préinstaller des packages afin qu’aucun travail ne doive être effectué si le package se trouve dans les dossiers de secours.</span><span class="sxs-lookup"><span data-stu-id="3aab2-234">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="3aab2-235">Les dossiers de package de secours ont exactement la même structure de dossiers et de fichiers que le dossier de package global : *. nupkg* est présent et tous les fichiers sont extraits.</span><span class="sxs-lookup"><span data-stu-id="3aab2-235">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="3aab2-236">La logique de recherche pour cette configuration est la suivante :</span><span class="sxs-lookup"><span data-stu-id="3aab2-236">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="3aab2-237">Recherchez dans le dossier de package global pour voir si le package/la version est déjà téléchargé.</span><span class="sxs-lookup"><span data-stu-id="3aab2-237">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="3aab2-238">Recherchez dans les dossiers de secours un package/version correspondant.</span><span class="sxs-lookup"><span data-stu-id="3aab2-238">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="3aab2-239">Si une recherche est réussie, aucun téléchargement n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3aab2-239">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="3aab2-240">Si aucune correspondance n’est trouvée, NuGet vérifie les sources de fichiers, puis les sources http, puis télécharge les packages.</span><span class="sxs-lookup"><span data-stu-id="3aab2-240">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="3aab2-241">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-241">Key</span></span> | <span data-ttu-id="3aab2-242">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-242">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-243">(nom du dossier de secours)</span><span class="sxs-lookup"><span data-stu-id="3aab2-243">(name of fallback folder)</span></span> | <span data-ttu-id="3aab2-244">Chemin d’accès au dossier de secours.</span><span class="sxs-lookup"><span data-stu-id="3aab2-244">Path to fallback folder.</span></span> |

<span data-ttu-id="3aab2-245">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-245">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="3aab2-246">packageManagement (section)</span><span class="sxs-lookup"><span data-stu-id="3aab2-246">packageManagement section</span></span>

<span data-ttu-id="3aab2-247">Définit le format de gestion de package par défaut, *packages. config* ou PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3aab2-247">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="3aab2-248">Les projets de style SDK utilisent toujours PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3aab2-248">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="3aab2-249">Clé</span><span class="sxs-lookup"><span data-stu-id="3aab2-249">Key</span></span> | <span data-ttu-id="3aab2-250">Valeur</span><span class="sxs-lookup"><span data-stu-id="3aab2-250">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3aab2-251">format</span><span class="sxs-lookup"><span data-stu-id="3aab2-251">format</span></span> | <span data-ttu-id="3aab2-252">Valeur booléenne qui indique le format de gestion des packages par défaut.</span><span class="sxs-lookup"><span data-stu-id="3aab2-252">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="3aab2-253">Si `1`, le format est PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3aab2-253">If `1`, format is PackageReference.</span></span> <span data-ttu-id="3aab2-254">Si `0`, le format est *packages. config*.</span><span class="sxs-lookup"><span data-stu-id="3aab2-254">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="3aab2-255">disabled</span><span class="sxs-lookup"><span data-stu-id="3aab2-255">disabled</span></span> | <span data-ttu-id="3aab2-256">Valeur booléenne indiquant s’il faut afficher l’invite de sélection d’un format de package par défaut lors de la première installation de package.</span><span class="sxs-lookup"><span data-stu-id="3aab2-256">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="3aab2-257">`False` masque l’invite.</span><span class="sxs-lookup"><span data-stu-id="3aab2-257">`False` hides the prompt.</span></span> |

<span data-ttu-id="3aab2-258">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="3aab2-258">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="3aab2-259">Utilisation de variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="3aab2-259">Using environment variables</span></span>

<span data-ttu-id="3aab2-260">Vous pouvez utiliser des variables d’environnement dans les valeurs `nuget.config` (NuGet 3.4+) pour appliquer des paramètres au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="3aab2-260">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="3aab2-261">Par exemple, si la variable d’environnement `HOME` sur Windows a la valeur `c:\users\username`, la valeur `%HOME%\NuGetRepository` dans le fichier de configuration correspond à `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-261">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="3aab2-262">Notez que vous devez utiliser des variables d’environnement de style Windows (commence et se termine par%) même sur Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="3aab2-262">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="3aab2-263">Le fait d’avoir `$HOME/NuGetRepository` dans un fichier de configuration ne sera pas résolu.</span><span class="sxs-lookup"><span data-stu-id="3aab2-263">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="3aab2-264">Sur Mac/Linux, la valeur de `%HOME%\NuGetRepository` est résolue en `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="3aab2-264">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="3aab2-265">Si aucune variable d’environnement n’est trouvée, NuGet utilise la valeur littérale du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="3aab2-265">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="3aab2-266">Exemple de fichier config</span><span class="sxs-lookup"><span data-stu-id="3aab2-266">Example config file</span></span>

<span data-ttu-id="3aab2-267">Vous trouverez ci-dessous un exemple de `nuget.config` fichier qui illustre un certain nombre de paramètres, notamment ceux qui sont facultatifs :</span><span class="sxs-lookup"><span data-stu-id="3aab2-267">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
