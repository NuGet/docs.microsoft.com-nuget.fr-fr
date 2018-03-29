---
title: Informations de référence sur le fichier NuGet.Config | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informations de référence sur le fichier NuGet.Config, notamment les sections config, bindingRedirects, packageRestore, solution et packageSource.
keywords: fichier NuGet.Config, référence de configuration NuGet, options de configuration NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="d1eb6-104">Informations de référence sur NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="d1eb6-104">NuGet.Config reference</span></span>

<span data-ttu-id="d1eb6-105">Le comportement de NuGet est contrôlé par des paramètres dans différents fichiers `NuGet.Config` comme décrit dans [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="d1eb6-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="d1eb6-106">`NuGet.Config` est un fichier XML contenant un nœud `<configuration>` de niveau supérieur qui comprend à son tour les éléments de section décrits dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="d1eb6-107">Chaque section contient zéro ou plusieurs éléments `<add>` avec des attributs `key` et `value`.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="d1eb6-108">Consultez [l’exemple de fichier config](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="d1eb6-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="d1eb6-109">Les noms de paramètre ne respectent pas la casse et les valeurs peuvent utiliser des [variables d’environnement](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="d1eb6-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="d1eb6-110">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-110">In this topic:</span></span>

- [<span data-ttu-id="d1eb6-111">Section config</span><span class="sxs-lookup"><span data-stu-id="d1eb6-111">config section</span></span>](#config-section)
- [<span data-ttu-id="d1eb6-112">Section bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="d1eb6-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="d1eb6-113">Section packageRestore</span><span class="sxs-lookup"><span data-stu-id="d1eb6-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="d1eb6-114">Section solution</span><span class="sxs-lookup"><span data-stu-id="d1eb6-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="d1eb6-115">[Sections sur les sources de packages](#package-source-sections) :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="d1eb6-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="d1eb6-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="d1eb6-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="d1eb6-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="d1eb6-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="d1eb6-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="d1eb6-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="d1eb6-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="d1eb6-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="d1eb6-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="d1eb6-121">Utilisation de variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="d1eb6-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="d1eb6-122">Exemple de fichier config</span><span class="sxs-lookup"><span data-stu-id="d1eb6-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="d1eb6-123">Section config</span><span class="sxs-lookup"><span data-stu-id="d1eb6-123">config section</span></span>

<span data-ttu-id="d1eb6-124">Contient des paramètres de configuration divers, qui peuvent être définis à l’aide de la [commande `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="d1eb6-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="d1eb6-125">`dependencyVersion` et `repositoryPath` s’appliquent uniquement aux projets à l’aide de `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="d1eb6-126">`globalPackagesFolder` s’applique uniquement aux projets en utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="d1eb6-127">Touche</span><span class="sxs-lookup"><span data-stu-id="d1eb6-127">Key</span></span> | <span data-ttu-id="d1eb6-128">Value</span><span class="sxs-lookup"><span data-stu-id="d1eb6-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d1eb6-129">dependencyVersion (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="d1eb6-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="d1eb6-130">Valeur `DependencyVersion` par défaut pour l’installation, la restauration et la mise à jour de package, quand le commutateur `-DependencyVersion` n’est pas spécifié directement.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="d1eb6-131">Cette valeur est également utilisée par l’interface utilisateur du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="d1eb6-132">Les valeurs sont `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="d1eb6-133">globalPackagesFolder (projets à l’aide de PackageReference uniquement)</span><span class="sxs-lookup"><span data-stu-id="d1eb6-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="d1eb6-134">Emplacement du dossier de packages global par défaut.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-134">The location of the default global packages folder.</span></span> <span data-ttu-id="d1eb6-135">L’emplacement par défaut est `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="d1eb6-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="d1eb6-136">Un chemin relatif peut être utilisé dans les fichiers `Nuget.Config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="d1eb6-137">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="d1eb6-138">repositoryPath (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="d1eb6-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="d1eb6-139">Emplacement dans lequel installer les packages NuGet au lieu du dossier `$(Solutiondir)/packages` par défaut.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="d1eb6-140">Un chemin relatif peut être utilisé dans les fichiers `Nuget.Config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="d1eb6-141">Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="d1eb6-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="d1eb6-142">defaultPushSource</span></span> | <span data-ttu-id="d1eb6-143">Identifie l’URL ou le chemin de la source du package qui doit être utilisée comme valeur par défaut si aucune autre source de package n’est trouvée pour une opération.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="d1eb6-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="d1eb6-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="d1eb6-145">Paramètres de proxy à utiliser lors de la connexion aux sources de packages ; `http_proxy` doit être au format `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="d1eb6-146">Les mots de passe sont chiffrés et ne peuvent pas être ajoutés manuellement.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="d1eb6-147">Pour `no_proxy`, la valeur est une liste de domaines séparés par des virgules qui ignorent le serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="d1eb6-148">Vous pouvez également utiliser les variables d’environnement http_proxy et no_proxy pour ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="d1eb6-149">Pour plus d’informations, consultez [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="d1eb6-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="d1eb6-150">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="d1eb6-151">Section bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="d1eb6-151">bindingRedirects section</span></span>

<span data-ttu-id="d1eb6-152">Définit si NuGet effectue des redirections de liaisons automatiques quand un package est installé.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="d1eb6-153">Touche</span><span class="sxs-lookup"><span data-stu-id="d1eb6-153">Key</span></span> | <span data-ttu-id="d1eb6-154">Value</span><span class="sxs-lookup"><span data-stu-id="d1eb6-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d1eb6-155">skip</span><span class="sxs-lookup"><span data-stu-id="d1eb6-155">skip</span></span> | <span data-ttu-id="d1eb6-156">Valeur booléenne indiquant s’il faut ignorer les redirections de liaisons automatiques.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="d1eb6-157">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-157">The default is false.</span></span> |

<span data-ttu-id="d1eb6-158">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="d1eb6-159">Section packageRestore</span><span class="sxs-lookup"><span data-stu-id="d1eb6-159">packageRestore section</span></span>

<span data-ttu-id="d1eb6-160">Contrôle la restauration de packages pendant les générations.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="d1eb6-161">Touche</span><span class="sxs-lookup"><span data-stu-id="d1eb6-161">Key</span></span> | <span data-ttu-id="d1eb6-162">Value</span><span class="sxs-lookup"><span data-stu-id="d1eb6-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d1eb6-163">enabled</span><span class="sxs-lookup"><span data-stu-id="d1eb6-163">enabled</span></span> | <span data-ttu-id="d1eb6-164">Valeur booléenne indiquant si NuGet peut effectuer une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="d1eb6-165">Vous pouvez également définir la variable d’environnement `EnableNuGetPackageRestore` avec la valeur `True` au lieu de définir cette clé dans le fichier config.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="d1eb6-166">automatique</span><span class="sxs-lookup"><span data-stu-id="d1eb6-166">automatic</span></span> | <span data-ttu-id="d1eb6-167">Valeur booléenne indiquant si NuGet doit rechercher les packages manquants pendant une génération.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="d1eb6-168">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="d1eb6-169">Section solution</span><span class="sxs-lookup"><span data-stu-id="d1eb6-169">solution section</span></span>

<span data-ttu-id="d1eb6-170">Contrôle si le dossier `packages` d’une solution est inclus dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="d1eb6-171">Cette section fonctionne uniquement dans les fichiers `Nuget.Config` dans un dossier de solution.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="d1eb6-172">Touche</span><span class="sxs-lookup"><span data-stu-id="d1eb6-172">Key</span></span> | <span data-ttu-id="d1eb6-173">Value</span><span class="sxs-lookup"><span data-stu-id="d1eb6-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d1eb6-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="d1eb6-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="d1eb6-175">Valeur booléenne indiquant s’il faut ignorer le dossier de packages lors de l’utilisation de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="d1eb6-176">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-176">The default value is false.</span></span> |

<span data-ttu-id="d1eb6-177">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="d1eb6-178">Sections sur les sources de packages</span><span class="sxs-lookup"><span data-stu-id="d1eb6-178">Package source sections</span></span>

<span data-ttu-id="d1eb6-179">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` et `disabledPackageSources` fonctionnent ensemble pour configurer la façon dont NuGet utilise les dépôts de packages pendant les opérations d’installation, de restauration et de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="d1eb6-180">La [commande `nuget sources`](../tools/cli-ref-sources.md) est généralement utilisée pour gérer ces paramètres, à l’exception de `apikeys` qui est géré à l’aide de la [commande `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="d1eb6-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="d1eb6-181">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="d1eb6-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="d1eb6-182">packageSources</span></span>

<span data-ttu-id="d1eb6-183">Répertorie toutes les sources de packages connues.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-183">Lists all known package sources.</span></span> <span data-ttu-id="d1eb6-184">L’ordre est ignoré pendant les opérations de restauration et aucun projet utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="d1eb6-185">NuGet respecte l’ordre des sources pour installer et mettre à jour des opérations avec des projets à l’aide de `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="d1eb6-186">Touche</span><span class="sxs-lookup"><span data-stu-id="d1eb6-186">Key</span></span> | <span data-ttu-id="d1eb6-187">Value</span><span class="sxs-lookup"><span data-stu-id="d1eb6-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d1eb6-188">(nom à assigner à la source du package)</span><span class="sxs-lookup"><span data-stu-id="d1eb6-188">(name to assign to the package source)</span></span> | <span data-ttu-id="d1eb6-189">Chemin ou URL de la source du package.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="d1eb6-190">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="d1eb6-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="d1eb6-191">packageSourceCredentials</span></span>

<span data-ttu-id="d1eb6-192">Stocke les noms d’utilisateur et mots de passe pour les sources, spécifiés en général en utilisant les commutateurs `-username` et `-password` avec `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="d1eb6-193">Les mots de passe sont chiffrés par défaut, sauf si l’option `-storepasswordincleartext` est également utilisée.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="d1eb6-194">Touche</span><span class="sxs-lookup"><span data-stu-id="d1eb6-194">Key</span></span> | <span data-ttu-id="d1eb6-195">Value</span><span class="sxs-lookup"><span data-stu-id="d1eb6-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d1eb6-196">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d1eb6-196">username</span></span> | <span data-ttu-id="d1eb6-197">Nom d’utilisateur pour la source en texte brut.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="d1eb6-198">mot de passe</span><span class="sxs-lookup"><span data-stu-id="d1eb6-198">password</span></span> | <span data-ttu-id="d1eb6-199">Mot de passe chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="d1eb6-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="d1eb6-200">cleartextpassword</span></span> | <span data-ttu-id="d1eb6-201">Mot de passe non chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="d1eb6-202">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="d1eb6-202">**Example:**</span></span>

<span data-ttu-id="d1eb6-203">Dans le fichier config, l’élément `<packageSourceCredentials>` contient des nœuds enfants pour chaque nom de source applicable (les espaces dans le nom sont remplacés par `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="d1eb6-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="d1eb6-204">Autrement dit, pour les sources nommées « Contoso » et « Test Source », le fichier config contient les éléments suivants lors de l’utilisation de mots de passe chiffrés :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="d1eb6-205">Lors de l’utilisation de mots de passe non chiffrés :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-205">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="d1eb6-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="d1eb6-206">apikeys</span></span>

<span data-ttu-id="d1eb6-207">Stocke les clés pour les sources qui utilisent l’authentification de clé API, comme défini avec la [commande `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="d1eb6-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="d1eb6-208">Touche</span><span class="sxs-lookup"><span data-stu-id="d1eb6-208">Key</span></span> | <span data-ttu-id="d1eb6-209">Value</span><span class="sxs-lookup"><span data-stu-id="d1eb6-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d1eb6-210">(URL source)</span><span class="sxs-lookup"><span data-stu-id="d1eb6-210">(source URL)</span></span> | <span data-ttu-id="d1eb6-211">Clé API chiffrée.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-211">The encrypted API key.</span></span> |

<span data-ttu-id="d1eb6-212">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="d1eb6-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="d1eb6-213">disabledPackageSources</span></span>

<span data-ttu-id="d1eb6-214">Identifie les sources actuellement désactivées.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-214">Identified currently disabled sources.</span></span> <span data-ttu-id="d1eb6-215">Peut être vide.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-215">May be empty.</span></span>

| <span data-ttu-id="d1eb6-216">Touche</span><span class="sxs-lookup"><span data-stu-id="d1eb6-216">Key</span></span> | <span data-ttu-id="d1eb6-217">Value</span><span class="sxs-lookup"><span data-stu-id="d1eb6-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d1eb6-218">(nom de source)</span><span class="sxs-lookup"><span data-stu-id="d1eb6-218">(name of source)</span></span> | <span data-ttu-id="d1eb6-219">Valeur booléenne indiquant si la source est désactivée.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="d1eb6-220">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="d1eb6-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="d1eb6-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="d1eb6-221">activePackageSource</span></span>

<span data-ttu-id="d1eb6-222">*(2.x uniquement ; déprécié dans 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="d1eb6-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="d1eb6-223">Identifie la source actuellement active ou indique l’agrégat de toutes les sources.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="d1eb6-224">Touche</span><span class="sxs-lookup"><span data-stu-id="d1eb6-224">Key</span></span> | <span data-ttu-id="d1eb6-225">Value</span><span class="sxs-lookup"><span data-stu-id="d1eb6-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d1eb6-226">(nom de source) ou `All`</span><span class="sxs-lookup"><span data-stu-id="d1eb6-226">(name of source) or `All`</span></span> | <span data-ttu-id="d1eb6-227">Si la clé est le nom d’une source, la valeur est le chemin ou l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="d1eb6-228">Si la clé est `All`, la valeur doit être `(Aggregate source)` pour combiner toutes les sources de packages qui ne sont pas autrement désactivées.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="d1eb6-229">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="d1eb6-230">Utilisation de variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="d1eb6-230">Using environment variables</span></span>

<span data-ttu-id="d1eb6-231">Vous pouvez utiliser des variables d’environnement dans les valeurs `NuGet.Config` (NuGet 3.4+) pour appliquer des paramètres au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="d1eb6-232">Par exemple, si la variable d’environnement `HOME` sur Windows a la valeur `c:\users\username`, la valeur `%HOME%\NuGetRepository` dans le fichier de configuration correspond à `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="d1eb6-233">De même, si `HOME` sur Mac/Linux a la valeur `/home/myStuff`, `$HOME/NuGetRepository` dans le fichier de configuration correspond à `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="d1eb6-234">Si aucune variable d’environnement n’est trouvée, NuGet utilise la valeur littérale du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="d1eb6-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="d1eb6-235">Exemple de fichier config</span><span class="sxs-lookup"><span data-stu-id="d1eb6-235">Example config file</span></span>

<span data-ttu-id="d1eb6-236">Voici un exemple de fichier `NuGet.Config` qui illustre un certain nombre de paramètres :</span><span class="sxs-lookup"><span data-stu-id="d1eb6-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
</configuration>
```
