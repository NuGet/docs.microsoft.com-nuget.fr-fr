---
title: "Informations de référence sur le fichier NuGet.Config | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: fbf31530-3bf4-478c-b26c-c2b24dd3406d
description: "Informations de référence sur le fichier NuGet.Config, notamment les sections config, bindingRedirects, packageRestore, solution et packageSource."
keywords: "fichier NuGet.Config, référence de configuration NuGet, options de configuration NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 830c622f622b894a228b18dfdb3a790bccfde8a3
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="b7ea4-104">Informations de référence sur NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="b7ea4-104">NuGet.Config reference</span></span>

<span data-ttu-id="b7ea4-105">Le comportement de NuGet est contrôlé par des paramètres dans différents fichiers `NuGet.Config` comme décrit dans [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="b7ea4-106">`NuGet.Config` est un fichier XML contenant un nœud `<configuration>` de niveau supérieur qui comprend à son tour les éléments de section décrits dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="b7ea4-107">Chaque section contient zéro ou plusieurs éléments `<add>` avec des attributs `key` et `value`.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="b7ea4-108">Consultez [l’exemple de fichier config](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="b7ea4-109">Les noms de paramètre ne respectent pas la casse et les valeurs peuvent utiliser des [variables d’environnement](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="b7ea4-110">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-110">In this topic:</span></span>

- [<span data-ttu-id="b7ea4-111">Section config</span><span class="sxs-lookup"><span data-stu-id="b7ea4-111">config section</span></span>](#config-section)
- [<span data-ttu-id="b7ea4-112">Section bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="b7ea4-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="b7ea4-113">Section packageRestore</span><span class="sxs-lookup"><span data-stu-id="b7ea4-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="b7ea4-114">Section solution</span><span class="sxs-lookup"><span data-stu-id="b7ea4-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="b7ea4-115">[Sections sur les sources de packages](#package-source-sections)- :[packageSources](#packagesources)</span><span class="sxs-lookup"><span data-stu-id="b7ea4-115">[Package source sections](#package-source-sections): -[packageSources](#packagesources)</span></span>
  - [<span data-ttu-id="b7ea4-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="b7ea4-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="b7ea4-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="b7ea4-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="b7ea4-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="b7ea4-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="b7ea4-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="b7ea4-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="b7ea4-120">Utilisation de variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="b7ea4-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="b7ea4-121">Exemple de fichier config</span><span class="sxs-lookup"><span data-stu-id="b7ea4-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="b7ea4-122">Section config</span><span class="sxs-lookup"><span data-stu-id="b7ea4-122">config section</span></span>

<span data-ttu-id="b7ea4-123">Contient des paramètres de configuration divers, qui peuvent être définis à l’aide de la [commande `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="b7ea4-124">Remarque : `dependencyVersion` et `repositoryPath` s’appliquent uniquement aux projets utilisant `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-124">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="b7ea4-125">`globalPackagesFolder` s’applique uniquement aux projets utilisant `project.json` et les formats PackageReference.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-125">`globalPackagesFolder` applies only to projects using `project.json` and PackageReference formats.</span></span>

| <span data-ttu-id="b7ea4-126">Touche</span><span class="sxs-lookup"><span data-stu-id="b7ea4-126">Key</span></span> | <span data-ttu-id="b7ea4-127">Value</span><span class="sxs-lookup"><span data-stu-id="b7ea4-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b7ea4-128">dependencyVersion (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="b7ea4-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="b7ea4-129">Valeur `DependencyVersion` par défaut pour l’installation, la restauration et la mise à jour de package, quand le commutateur `-DependencyVersion` n’est pas spécifié directement.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="b7ea4-130">Cette valeur est également utilisée par l’interface utilisateur du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="b7ea4-131">Les valeurs sont `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="b7ea4-132">globalPackagesFolder (projets n’utilisant pas `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="b7ea4-132">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="b7ea4-133">Emplacement du dossier de packages global par défaut.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-133">The location of the default global packages folder.</span></span> <span data-ttu-id="b7ea4-134">L’emplacement par défaut est `%USERPROFILE%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-134">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="b7ea4-135">Un chemin relatif peut être utilisé dans les fichiers `Nuget.Config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-135">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="b7ea4-136">repositoryPath (`packages.config` uniquement)</span><span class="sxs-lookup"><span data-stu-id="b7ea4-136">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="b7ea4-137">Emplacement dans lequel installer les packages NuGet au lieu du dossier `$(Solutiondir)/packages` par défaut.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-137">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="b7ea4-138">Un chemin relatif peut être utilisé dans les fichiers `Nuget.Config` spécifiques au projet.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-138">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="b7ea4-139">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="b7ea4-139">defaultPushSource</span></span> | <span data-ttu-id="b7ea4-140">Identifie l’URL ou le chemin de la source du package qui doit être utilisée comme valeur par défaut si aucune autre source de package n’est trouvée pour une opération.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-140">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="b7ea4-141">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="b7ea4-141">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="b7ea4-142">Paramètres de proxy à utiliser lors de la connexion aux sources de packages ; `http_proxy` doit être au format `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-142">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="b7ea4-143">Les mots de passe sont chiffrés et ne peuvent pas être ajoutés manuellement.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-143">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="b7ea4-144">Pour `no_proxy`, la valeur est une liste de domaines séparés par des virgules qui ignorent le serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-144">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="b7ea4-145">Vous pouvez également utiliser les variables d’environnement http_proxy et no_proxy pour ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-145">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="b7ea4-146">Pour plus d’informations, consultez [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-146">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="b7ea4-147">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-147">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="b7ea4-148">Section bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="b7ea4-148">bindingRedirects section</span></span>

<span data-ttu-id="b7ea4-149">Définit si NuGet effectue des redirections de liaisons automatiques quand un package est installé.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-149">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="b7ea4-150">Touche</span><span class="sxs-lookup"><span data-stu-id="b7ea4-150">Key</span></span> | <span data-ttu-id="b7ea4-151">Value</span><span class="sxs-lookup"><span data-stu-id="b7ea4-151">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b7ea4-152">skip</span><span class="sxs-lookup"><span data-stu-id="b7ea4-152">skip</span></span> | <span data-ttu-id="b7ea4-153">Valeur booléenne indiquant s’il faut ignorer les redirections de liaisons automatiques.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-153">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="b7ea4-154">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-154">The default is false.</span></span> |

<span data-ttu-id="b7ea4-155">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-155">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="b7ea4-156">Section packageRestore</span><span class="sxs-lookup"><span data-stu-id="b7ea4-156">packageRestore section</span></span>

<span data-ttu-id="b7ea4-157">*Ignorée dans 2.7+*</span><span class="sxs-lookup"><span data-stu-id="b7ea4-157">*Ignored in 2.7+*</span></span>

<span data-ttu-id="b7ea4-158">Contrôle la restauration de packages pendant les générations.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-158">Controls package restore during builds.</span></span>

| <span data-ttu-id="b7ea4-159">Touche</span><span class="sxs-lookup"><span data-stu-id="b7ea4-159">Key</span></span> | <span data-ttu-id="b7ea4-160">Value</span><span class="sxs-lookup"><span data-stu-id="b7ea4-160">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b7ea4-161">enabled</span><span class="sxs-lookup"><span data-stu-id="b7ea4-161">enabled</span></span> | <span data-ttu-id="b7ea4-162">Valeur booléenne indiquant si NuGet peut effectuer une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-162">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="b7ea4-163">Vous pouvez également définir la variable d’environnement `EnableNuGetPackageRestore` avec la valeur `True` au lieu de définir cette clé dans le fichier config.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-163">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="b7ea4-164">automatique</span><span class="sxs-lookup"><span data-stu-id="b7ea4-164">automatic</span></span> | <span data-ttu-id="b7ea4-165">Valeur booléenne indiquant si NuGet doit rechercher les packages manquants pendant une génération.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-165">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="b7ea4-166">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-166">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="b7ea4-167">Section solution</span><span class="sxs-lookup"><span data-stu-id="b7ea4-167">solution section</span></span>

<span data-ttu-id="b7ea4-168">Contrôle si le dossier `packages` d’une solution est inclus dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-168">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="b7ea4-169">Cette section fonctionne uniquement dans les fichiers `Nuget.Config` dans un dossier de solution.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-169">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="b7ea4-170">Touche</span><span class="sxs-lookup"><span data-stu-id="b7ea4-170">Key</span></span> | <span data-ttu-id="b7ea4-171">Value</span><span class="sxs-lookup"><span data-stu-id="b7ea4-171">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b7ea4-172">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="b7ea4-172">disableSourceControlIntegration</span></span> | <span data-ttu-id="b7ea4-173">Valeur booléenne indiquant s’il faut ignorer le dossier de packages lors de l’utilisation de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-173">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="b7ea4-174">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-174">The default value is false.</span></span> |

<span data-ttu-id="b7ea4-175">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-175">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="b7ea4-176">Sections sur les sources de packages</span><span class="sxs-lookup"><span data-stu-id="b7ea4-176">Package source sections</span></span>

<span data-ttu-id="b7ea4-177">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` et `disabledPackageSources` fonctionnent ensemble pour configurer la façon dont NuGet utilise les dépôts de packages pendant les opérations d’installation, de restauration et de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-177">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="b7ea4-178">La [commande `nuget sources`](../tools/cli-ref-sources.md) est généralement utilisée pour gérer ces paramètres, à l’exception de `apikeys` qui est géré à l’aide de la [commande `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-178">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="b7ea4-179">Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-179">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="b7ea4-180">packageSources</span><span class="sxs-lookup"><span data-stu-id="b7ea4-180">packageSources</span></span>

<span data-ttu-id="b7ea4-181">Répertorie toutes les sources de packages connues.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-181">Lists all known package sources.</span></span>

| <span data-ttu-id="b7ea4-182">Touche</span><span class="sxs-lookup"><span data-stu-id="b7ea4-182">Key</span></span> | <span data-ttu-id="b7ea4-183">Value</span><span class="sxs-lookup"><span data-stu-id="b7ea4-183">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b7ea4-184">(nom à assigner à la source du package)</span><span class="sxs-lookup"><span data-stu-id="b7ea4-184">(name to assign to the package source)</span></span> | <span data-ttu-id="b7ea4-185">Chemin ou URL de la source du package.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-185">The path or URL of the package source.</span></span> |

<span data-ttu-id="b7ea4-186">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-186">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="b7ea4-187">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="b7ea4-187">packageSourceCredentials</span></span>

<span data-ttu-id="b7ea4-188">Stocke les noms d’utilisateur et mots de passe pour les sources, spécifiés en général en utilisant les commutateurs `-username` et `-password` avec `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-188">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="b7ea4-189">Les mots de passe sont chiffrés par défaut, sauf si l’option `-storepasswordincleartext` est également utilisée.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-189">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="b7ea4-190">Touche</span><span class="sxs-lookup"><span data-stu-id="b7ea4-190">Key</span></span> | <span data-ttu-id="b7ea4-191">Value</span><span class="sxs-lookup"><span data-stu-id="b7ea4-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b7ea4-192">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b7ea4-192">username</span></span> | <span data-ttu-id="b7ea4-193">Nom d’utilisateur pour la source en texte brut.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-193">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="b7ea4-194">mot de passe</span><span class="sxs-lookup"><span data-stu-id="b7ea4-194">password</span></span> | <span data-ttu-id="b7ea4-195">Mot de passe chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-195">The encrypted password for the source.</span></span> |
| <span data-ttu-id="b7ea4-196">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="b7ea4-196">cleartextpassword</span></span> | <span data-ttu-id="b7ea4-197">Mot de passe non chiffré pour la source.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-197">The unencrypted password for the source.</span></span> |

<span data-ttu-id="b7ea4-198">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="b7ea4-198">**Example:**</span></span>

<span data-ttu-id="b7ea4-199">Dans le fichier config, l’élément `<packageSourceCredentials>` contient des nœuds enfants pour chaque nom de source applicable (les espaces dans le nom sont remplacés par `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-199">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="b7ea4-200">Autrement dit, pour les sources nommées « Contoso » et « Test Source », le fichier config contient les éléments suivants lors de l’utilisation de mots de passe chiffrés :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-200">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="b7ea4-201">Lors de l’utilisation de mots de passe non chiffrés :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-201">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="b7ea4-202">apikeys</span><span class="sxs-lookup"><span data-stu-id="b7ea4-202">apikeys</span></span>

<span data-ttu-id="b7ea4-203">Stocke les clés pour les sources qui utilisent l’authentification de clé API, comme défini avec la [commande `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-203">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="b7ea4-204">Touche</span><span class="sxs-lookup"><span data-stu-id="b7ea4-204">Key</span></span> | <span data-ttu-id="b7ea4-205">Value</span><span class="sxs-lookup"><span data-stu-id="b7ea4-205">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b7ea4-206">(URL source)</span><span class="sxs-lookup"><span data-stu-id="b7ea4-206">(source URL)</span></span> | <span data-ttu-id="b7ea4-207">Clé API chiffrée.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-207">The encrypted API key.</span></span> |

<span data-ttu-id="b7ea4-208">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-208">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="b7ea4-209">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="b7ea4-209">disabledPackageSources</span></span>

<span data-ttu-id="b7ea4-210">Identifie les sources actuellement désactivées.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-210">Identified currently disabled sources.</span></span> <span data-ttu-id="b7ea4-211">Peut être vide.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-211">May be empty.</span></span>

| <span data-ttu-id="b7ea4-212">Touche</span><span class="sxs-lookup"><span data-stu-id="b7ea4-212">Key</span></span> | <span data-ttu-id="b7ea4-213">Value</span><span class="sxs-lookup"><span data-stu-id="b7ea4-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b7ea4-214">(nom de source)</span><span class="sxs-lookup"><span data-stu-id="b7ea4-214">(name of source)</span></span> | <span data-ttu-id="b7ea4-215">Valeur booléenne indiquant si la source est désactivée.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-215">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="b7ea4-216">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="b7ea4-216">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="b7ea4-217">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="b7ea4-217">activePackageSource</span></span>

<span data-ttu-id="b7ea4-218">*(2.x uniquement ; déprécié dans 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="b7ea4-218">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="b7ea4-219">Identifie la source actuellement active ou indique l’agrégat de toutes les sources.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-219">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="b7ea4-220">Touche</span><span class="sxs-lookup"><span data-stu-id="b7ea4-220">Key</span></span> | <span data-ttu-id="b7ea4-221">Value</span><span class="sxs-lookup"><span data-stu-id="b7ea4-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b7ea4-222">(nom de source) ou `All`</span><span class="sxs-lookup"><span data-stu-id="b7ea4-222">(name of source) or `All`</span></span> | <span data-ttu-id="b7ea4-223">Si la clé est le nom d’une source, la valeur est le chemin ou l’URL de la source.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-223">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="b7ea4-224">Si la clé est `All`, la valeur doit être `(Aggregate source)` pour combiner toutes les sources de packages qui ne sont pas autrement désactivées.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-224">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="b7ea4-225">**Exemple** :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-225">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="b7ea4-226">Utilisation de variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="b7ea4-226">Using environment variables</span></span>

<span data-ttu-id="b7ea4-227">Vous pouvez utiliser des variables d’environnement dans les valeurs `NuGet.Config` (NuGet 3.4+) pour appliquer des paramètres au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-227">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="b7ea4-228">Par exemple, si la variable d’environnement `HOME` sur Windows a la valeur `c:\users\username`, la valeur `%HOME%\NuGetRepository` dans le fichier de configuration correspond à `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-228">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="b7ea4-229">De même, si `HOME` sur Mac/Linux a la valeur `/home/myStuff`, `$HOME/NuGetRepository` dans le fichier de configuration correspond à `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-229">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="b7ea4-230">Si aucune variable d’environnement n’est trouvée, NuGet utilise la valeur littérale du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-230">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="b7ea4-231">Exemple de fichier config</span><span class="sxs-lookup"><span data-stu-id="b7ea4-231">Example config file</span></span>

<span data-ttu-id="b7ea4-232">Voici un exemple de fichier `NuGet.Config` qui illustre un certain nombre de paramètres :</span><span class="sxs-lookup"><span data-stu-id="b7ea4-232">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
