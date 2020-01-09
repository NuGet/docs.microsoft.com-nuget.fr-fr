---
title: informations de référence sur le fichier NuGet. config
description: Informations de référence sur le fichier NuGet.Config, notamment les sections config, bindingRedirects, packageRestore, solution et packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: d6cad228eb052563fe57ea635bff0ea548cedc1f
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383562"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="6f115-103">informations de référence sur NuGet. config</span><span class="sxs-lookup"><span data-stu-id="6f115-103">nuget.config reference</span></span>

<span data-ttu-id="6f115-104">Le comportement de NuGet est contrôlé par des paramètres dans différents fichiers `NuGet.Config` ou `nuget.config`, comme décrit dans [configurations NuGet courantes](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6f115-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="6f115-105">`nuget.config` est un fichier XML contenant un nœud `<configuration>` de niveau supérieur qui comprend à son tour les éléments de section décrits dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="6f115-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="6f115-106">Chaque section contient zéro ou plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="6f115-106">Each section contains zero or more items.</span></span> <span data-ttu-id="6f115-107">Consultez [l’exemple de fichier config](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="6f115-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="6f115-108">Les noms de paramètre ne respectent pas la casse et les valeurs peuvent utiliser des [variables d’environnement](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="6f115-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="6f115-109">Section config</span><span class="sxs-lookup"><span data-stu-id="6f115-109">config section</span></span>

<span data-ttu-id="6f115-110">Contient des paramètres de configuration divers, qui peuvent être définis à l’aide de la [commande `nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="6f115-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="6f115-111">`dependencyVersion` et `repositoryPath` s’appliquent uniquement aux projets utilisant `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="6f115-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="6f115-112">`globalPackagesFolder` s’applique uniquement aux projets utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6f115-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="6f115-113">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-113">Key</span></span> | <span data-ttu-id="6f115-114">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-115">dependencyVersion (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="6f115-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="6f115-116">Valeur `DependencyVersion` par défaut pour l’installation, la restauration et la mise à jour de package, quand le commutateur `-DependencyVersion` n’est pas spécifié directement.</span><span class="sxs-lookup"><span data-stu-id="6f115-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="6f115-117">Cette valeur est également utilisée par l’interface utilisateur du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="6f115-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="6f115-118">Les valeurs sont `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="6f115-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="6f115-119">globalPackagesFolder (projets utilisant PackageReference uniquement)</span><span class="sxs-lookup"><span data-stu-id="6f115-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="6f115-120">Emplacement du dossier de packages global par défaut.</span><span class="sxs-lookup"><span data-stu-id="6f115-120">The location of the default global packages folder.</span></span> <span data-ttu-id="6f115-121">L’emplacement par défaut est `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6f115-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="6f115-122">Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="6f115-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6f115-123">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="6f115-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6f115-124">repositoryPath (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="6f115-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="6f115-125">Emplacement dans lequel installer les packages NuGet au lieu du dossier `$(Solutiondir)/packages` par défaut.</span><span class="sxs-lookup"><span data-stu-id="6f115-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="6f115-126">Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="6f115-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6f115-127">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="6f115-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6f115-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="6f115-128">defaultPushSource</span></span> | <span data-ttu-id="6f115-129">Identifie l’URL ou le chemin de la source du package qui doit être utilisée comme valeur par défaut si aucune autre source de package n’est trouvée pour une opération.</span><span class="sxs-lookup"><span data-stu-id="6f115-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="6f115-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="6f115-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="6f115-131">Paramètres de proxy à utiliser lors de la connexion aux sources de packages ; `http_proxy` doit être au format `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="6f115-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="6f115-132">Les mots de passe sont chiffrés et ne peuvent pas être ajoutés manuellement.</span><span class="sxs-lookup"><span data-stu-id="6f115-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="6f115-133">Pour `no_proxy`, la valeur est une liste de domaines séparés par des virgules qui ignorent le serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="6f115-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="6f115-134">Vous pouvez également utiliser les variables d’environnement http_proxy et no_proxy pour ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="6f115-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="6f115-135">Pour plus d’informations, consultez [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="6f115-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="6f115-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="6f115-136">signatureValidationMode</span></span> | <span data-ttu-id="6f115-137">Spécifie le mode de validation utilisé pour vérifier les signatures de package pour l’installation du package et la restauration.</span><span class="sxs-lookup"><span data-stu-id="6f115-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="6f115-138">Les valeurs sont `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="6f115-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="6f115-139">La valeur par défaut est `accept`.</span><span class="sxs-lookup"><span data-stu-id="6f115-139">Defaults to `accept`.</span></span>

<span data-ttu-id="6f115-140">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="6f115-141">Section bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="6f115-141">bindingRedirects section</span></span>

<span data-ttu-id="6f115-142">Définit si NuGet effectue des redirections de liaisons automatiques quand un package est installé.</span><span class="sxs-lookup"><span data-stu-id="6f115-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="6f115-143">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-143">Key</span></span> | <span data-ttu-id="6f115-144">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-145">skip</span><span class="sxs-lookup"><span data-stu-id="6f115-145">skip</span></span> | <span data-ttu-id="6f115-146">Valeur booléenne indiquant s’il faut ignorer les redirections de liaisons automatiques.</span><span class="sxs-lookup"><span data-stu-id="6f115-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="6f115-147">La valeur par défaut est False.</span><span class="sxs-lookup"><span data-stu-id="6f115-147">The default is false.</span></span> |

<span data-ttu-id="6f115-148">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="6f115-149">Section packageRestore</span><span class="sxs-lookup"><span data-stu-id="6f115-149">packageRestore section</span></span>

<span data-ttu-id="6f115-150">Contrôle la restauration de packages pendant les générations.</span><span class="sxs-lookup"><span data-stu-id="6f115-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="6f115-151">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-151">Key</span></span> | <span data-ttu-id="6f115-152">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-153">activé</span><span class="sxs-lookup"><span data-stu-id="6f115-153">enabled</span></span> | <span data-ttu-id="6f115-154">Valeur booléenne indiquant si NuGet peut effectuer une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="6f115-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="6f115-155">Vous pouvez également définir la variable d’environnement `EnableNuGetPackageRestore` avec la valeur `True` au lieu de définir cette clé dans le fichier config.</span><span class="sxs-lookup"><span data-stu-id="6f115-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="6f115-156">automatic</span><span class="sxs-lookup"><span data-stu-id="6f115-156">automatic</span></span> | <span data-ttu-id="6f115-157">Valeur booléenne indiquant si NuGet doit rechercher les packages manquants pendant une génération.</span><span class="sxs-lookup"><span data-stu-id="6f115-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="6f115-158">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="6f115-159">Section solution</span><span class="sxs-lookup"><span data-stu-id="6f115-159">solution section</span></span>

<span data-ttu-id="6f115-160">Contrôle si le dossier `packages` d’une solution est inclus dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="6f115-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="6f115-161">Cette section fonctionne uniquement dans les fichiers `nuget.config` dans un dossier de solution.</span><span class="sxs-lookup"><span data-stu-id="6f115-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="6f115-162">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-162">Key</span></span> | <span data-ttu-id="6f115-163">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="6f115-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="6f115-165">Valeur booléenne indiquant s’il faut ignorer le dossier de packages lors de l’utilisation de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="6f115-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="6f115-166">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="6f115-166">The default value is false.</span></span> |

<span data-ttu-id="6f115-167">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="6f115-168">Sections sur les sources de packages</span><span class="sxs-lookup"><span data-stu-id="6f115-168">Package source sections</span></span>

<span data-ttu-id="6f115-169">Les `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` et `trustedSigners` fonctionnent ensemble pour configurer la façon dont NuGet fonctionne avec les dépôts de packages pendant les opérations d’installation, de restauration et de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="6f115-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="6f115-170">La [commande`nuget sources`](../reference/cli-reference/cli-ref-sources.md) est généralement utilisée pour gérer ces paramètres, à l’exception de `apikeys` qui est gérée à l’aide de la [commande`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md)et `trustedSigners` qui est gérée à l’aide de la [commande`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="6f115-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="6f115-171">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="6f115-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="6f115-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="6f115-172">packageSources</span></span>

<span data-ttu-id="6f115-173">Répertorie toutes les sources de packages connues.</span><span class="sxs-lookup"><span data-stu-id="6f115-173">Lists all known package sources.</span></span> <span data-ttu-id="6f115-174">L’ordre est ignoré pendant les opérations de restauration et avec n’importe quel projet utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6f115-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="6f115-175">NuGet respecte l’ordre des sources pour les opérations d’installation et de mise à jour des projets à l’aide de `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="6f115-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="6f115-176">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-176">Key</span></span> | <span data-ttu-id="6f115-177">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-178">(nom à assigner à la source du package)</span><span class="sxs-lookup"><span data-stu-id="6f115-178">(name to assign to the package source)</span></span> | <span data-ttu-id="6f115-179">Chemin ou URL de la source du package.</span><span class="sxs-lookup"><span data-stu-id="6f115-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="6f115-180">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="6f115-181">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="6f115-181">packageSourceCredentials</span></span>

<span data-ttu-id="6f115-182">Stocke les noms d’utilisateur et mots de passe pour les sources, spécifiés en général en utilisant les commutateurs `-username` et `-password` avec `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="6f115-182">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="6f115-183">Les mots de passe sont chiffrés par défaut, sauf si l’option `-storepasswordincleartext` est également utilisée.</span><span class="sxs-lookup"><span data-stu-id="6f115-183">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="6f115-184">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-184">Key</span></span> | <span data-ttu-id="6f115-185">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-185">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-186">nom_utilisateur</span><span class="sxs-lookup"><span data-stu-id="6f115-186">username</span></span> | <span data-ttu-id="6f115-187">Nom d’utilisateur pour la source en texte brut.</span><span class="sxs-lookup"><span data-stu-id="6f115-187">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="6f115-188">mot de passe du .</span><span class="sxs-lookup"><span data-stu-id="6f115-188">password</span></span> | <span data-ttu-id="6f115-189">Mot de passe chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="6f115-189">The encrypted password for the source.</span></span> |
| <span data-ttu-id="6f115-190">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="6f115-190">cleartextpassword</span></span> | <span data-ttu-id="6f115-191">Mot de passe non chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="6f115-191">The unencrypted password for the source.</span></span> |

<span data-ttu-id="6f115-192">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="6f115-192">**Example:**</span></span>

<span data-ttu-id="6f115-193">Dans le fichier config, l’élément `<packageSourceCredentials>` contient des nœuds enfants pour chaque nom de source applicable (les espaces dans le nom sont remplacés par `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="6f115-193">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="6f115-194">Autrement dit, pour les sources nommées « Contoso » et « Test Source », le fichier config contient les éléments suivants lors de l’utilisation de mots de passe chiffrés :</span><span class="sxs-lookup"><span data-stu-id="6f115-194">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="6f115-195">Lors de l’utilisation de mots de passe non chiffrés :</span><span class="sxs-lookup"><span data-stu-id="6f115-195">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="6f115-196">apikeys</span><span class="sxs-lookup"><span data-stu-id="6f115-196">apikeys</span></span>

<span data-ttu-id="6f115-197">Stocke les clés pour les sources qui utilisent l’authentification de clé API, comme défini avec la [commande `nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="6f115-197">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="6f115-198">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-198">Key</span></span> | <span data-ttu-id="6f115-199">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-200">(URL source)</span><span class="sxs-lookup"><span data-stu-id="6f115-200">(source URL)</span></span> | <span data-ttu-id="6f115-201">Clé API chiffrée.</span><span class="sxs-lookup"><span data-stu-id="6f115-201">The encrypted API key.</span></span> |

<span data-ttu-id="6f115-202">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-202">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="6f115-203">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="6f115-203">disabledPackageSources</span></span>

<span data-ttu-id="6f115-204">Identifie les sources actuellement désactivées.</span><span class="sxs-lookup"><span data-stu-id="6f115-204">Identified currently disabled sources.</span></span> <span data-ttu-id="6f115-205">Peut être vide.</span><span class="sxs-lookup"><span data-stu-id="6f115-205">May be empty.</span></span>

| <span data-ttu-id="6f115-206">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-206">Key</span></span> | <span data-ttu-id="6f115-207">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-207">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-208">(nom de source)</span><span class="sxs-lookup"><span data-stu-id="6f115-208">(name of source)</span></span> | <span data-ttu-id="6f115-209">Valeur booléenne indiquant si la source est désactivée.</span><span class="sxs-lookup"><span data-stu-id="6f115-209">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="6f115-210">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="6f115-210">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="6f115-211">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="6f115-211">activePackageSource</span></span>

<span data-ttu-id="6f115-212">*(2.x uniquement ; déprécié dans 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="6f115-212">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="6f115-213">Identifie la source actuellement active ou indique l’agrégat de toutes les sources.</span><span class="sxs-lookup"><span data-stu-id="6f115-213">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="6f115-214">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-214">Key</span></span> | <span data-ttu-id="6f115-215">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-215">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-216">(nom de source) ou `All`</span><span class="sxs-lookup"><span data-stu-id="6f115-216">(name of source) or `All`</span></span> | <span data-ttu-id="6f115-217">Si la clé est le nom d’une source, la valeur est le chemin ou l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="6f115-217">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="6f115-218">Si la clé est `All`, la valeur doit être `(Aggregate source)` pour combiner toutes les sources de packages qui ne sont pas autrement désactivées.</span><span class="sxs-lookup"><span data-stu-id="6f115-218">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="6f115-219">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-219">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="6f115-220">section trustedSigners</span><span class="sxs-lookup"><span data-stu-id="6f115-220">trustedSigners section</span></span>

<span data-ttu-id="6f115-221">Stocke les signataires approuvés utilisés pour autoriser le package lors de l’installation ou de la restauration.</span><span class="sxs-lookup"><span data-stu-id="6f115-221">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="6f115-222">Cette liste ne peut pas être vide lorsque l’utilisateur définit `signatureValidationMode` sur `require`.</span><span class="sxs-lookup"><span data-stu-id="6f115-222">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="6f115-223">Cette section peut être mise à jour à l’aide de la [commande`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="6f115-223">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="6f115-224">**Schéma** :</span><span class="sxs-lookup"><span data-stu-id="6f115-224">**Schema**:</span></span>

<span data-ttu-id="6f115-225">Un signataire approuvé contient une collection d’éléments `certificate` qui inscrivent tous les certificats qui identifient un signataire donné.</span><span class="sxs-lookup"><span data-stu-id="6f115-225">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="6f115-226">Un signataire approuvé peut être un `Author` ou un `Repository`.</span><span class="sxs-lookup"><span data-stu-id="6f115-226">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="6f115-227">Un *référentiel* approuvé spécifie également les `serviceIndex` pour le dépôt (qui doit être un URI `https` valide) et peut éventuellement spécifier une liste de `owners` délimitée par des points-virgules pour limiter encore plus les personnes autorisées à partir de ce référentiel spécifique.</span><span class="sxs-lookup"><span data-stu-id="6f115-227">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="6f115-228">Les algorithmes de hachage pris en charge utilisés pour une empreinte digitale de certificat sont `SHA256`, `SHA384` et `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="6f115-228">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="6f115-229">Si un `certificate` spécifie `allowUntrustedRoot` comme `true` le certificat donné est autorisé à se lier à une racine non approuvée lors de la génération de la chaîne de certificats dans le cadre de la vérification de la signature.</span><span class="sxs-lookup"><span data-stu-id="6f115-229">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="6f115-230">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-230">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="6f115-231">section fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="6f115-231">fallbackPackageFolders section</span></span>

<span data-ttu-id="6f115-232">*(3.5 +)* Fournit un moyen de préinstaller des packages afin qu’aucun travail ne doive être effectué si le package se trouve dans les dossiers de secours.</span><span class="sxs-lookup"><span data-stu-id="6f115-232">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="6f115-233">Les dossiers de package de secours ont exactement la même structure de dossiers et de fichiers que le dossier de package global : *. nupkg* est présent et tous les fichiers sont extraits.</span><span class="sxs-lookup"><span data-stu-id="6f115-233">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="6f115-234">La logique de recherche pour cette configuration est la suivante :</span><span class="sxs-lookup"><span data-stu-id="6f115-234">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="6f115-235">Recherchez dans le dossier de package global pour voir si le package/la version est déjà téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6f115-235">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="6f115-236">Recherchez dans les dossiers de secours un package/version correspondant.</span><span class="sxs-lookup"><span data-stu-id="6f115-236">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="6f115-237">Si une recherche est réussie, aucun téléchargement n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6f115-237">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="6f115-238">Si aucune correspondance n’est trouvée, NuGet vérifie les sources de fichiers, puis les sources http, puis télécharge les packages.</span><span class="sxs-lookup"><span data-stu-id="6f115-238">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="6f115-239">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-239">Key</span></span> | <span data-ttu-id="6f115-240">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-240">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-241">(nom du dossier de secours)</span><span class="sxs-lookup"><span data-stu-id="6f115-241">(name of fallback folder)</span></span> | <span data-ttu-id="6f115-242">Chemin d’accès au dossier de secours.</span><span class="sxs-lookup"><span data-stu-id="6f115-242">Path to fallback folder.</span></span> |

<span data-ttu-id="6f115-243">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-243">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="6f115-244">packageManagement (section)</span><span class="sxs-lookup"><span data-stu-id="6f115-244">packageManagement section</span></span>

<span data-ttu-id="6f115-245">Définit le format de gestion de package par défaut, *packages. config* ou PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6f115-245">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="6f115-246">Les projets de style SDK utilisent toujours PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6f115-246">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="6f115-247">Clé</span><span class="sxs-lookup"><span data-stu-id="6f115-247">Key</span></span> | <span data-ttu-id="6f115-248">Value</span><span class="sxs-lookup"><span data-stu-id="6f115-248">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f115-249">format</span><span class="sxs-lookup"><span data-stu-id="6f115-249">format</span></span> | <span data-ttu-id="6f115-250">Valeur booléenne qui indique le format de gestion des packages par défaut.</span><span class="sxs-lookup"><span data-stu-id="6f115-250">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="6f115-251">Si `1`, le format est PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6f115-251">If `1`, format is PackageReference.</span></span> <span data-ttu-id="6f115-252">Si `0`, le format est *packages. config*.</span><span class="sxs-lookup"><span data-stu-id="6f115-252">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="6f115-253">désactivés</span><span class="sxs-lookup"><span data-stu-id="6f115-253">disabled</span></span> | <span data-ttu-id="6f115-254">Valeur booléenne indiquant s’il faut afficher l’invite de sélection d’un format de package par défaut lors de la première installation de package.</span><span class="sxs-lookup"><span data-stu-id="6f115-254">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="6f115-255">`False` masque l’invite.</span><span class="sxs-lookup"><span data-stu-id="6f115-255">`False` hides the prompt.</span></span> |

<span data-ttu-id="6f115-256">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="6f115-256">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="6f115-257">Utilisation de variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="6f115-257">Using environment variables</span></span>

<span data-ttu-id="6f115-258">Vous pouvez utiliser des variables d’environnement dans les valeurs `nuget.config` (NuGet 3.4+) pour appliquer des paramètres au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6f115-258">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="6f115-259">Par exemple, si la variable d’environnement `HOME` sur Windows a la valeur `c:\users\username`, la valeur `%HOME%\NuGetRepository` dans le fichier de configuration correspond à `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="6f115-259">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="6f115-260">De même, si `HOME` sur Mac/Linux a la valeur `/home/myStuff`, `$HOME/NuGetRepository` dans le fichier de configuration correspond à `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="6f115-260">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="6f115-261">Si aucune variable d’environnement n’est trouvée, NuGet utilise la valeur littérale du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="6f115-261">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="6f115-262">Exemple de fichier config</span><span class="sxs-lookup"><span data-stu-id="6f115-262">Example config file</span></span>

<span data-ttu-id="6f115-263">Voici un exemple de fichier `nuget.config` qui illustre un certain nombre de paramètres :</span><span class="sxs-lookup"><span data-stu-id="6f115-263">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
