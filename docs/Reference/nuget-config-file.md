---
title: "Informations de référence sur le fichier NuGet.Config | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informations de référence sur le fichier NuGet.Config, notamment les sections config, bindingRedirects, packageRestore, solution et packageSource."
keywords: "fichier NuGet.Config, référence de configuration NuGet, options de configuration NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a5be1ebcca0accafcdaf32f0b1b7ca66ec53425
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="nugetconfig-reference"></a>Informations de référence sur NuGet.Config

Le comportement de NuGet est contrôlé par des paramètres dans différents fichiers `NuGet.Config` comme décrit dans [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md).

`NuGet.Config` est un fichier XML contenant un nœud `<configuration>` de niveau supérieur qui comprend à son tour les éléments de section décrits dans cette rubrique. Chaque section contient zéro ou plusieurs éléments `<add>` avec des attributs `key` et `value`. Consultez [l’exemple de fichier config](#example-config-file). Les noms de paramètre ne respectent pas la casse et les valeurs peuvent utiliser des [variables d’environnement](#using-environment-variables).

Dans cette rubrique :

- [Section config](#config-section)
- [Section bindingRedirects](#bindingredirects-section)
- [Section packageRestore](#packagerestore-section)
- [Section solution](#solution-section)
- [Sections sur les sources de packages](#package-source-sections) :
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [Utilisation de variables d’environnement](#using-environment-variables)
- [Exemple de fichier config](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Section config

Contient des paramètres de configuration divers, qui peuvent être définis à l’aide de la [commande `nuget config`](../tools/cli-ref-config.md).

Remarque : `dependencyVersion` et `repositoryPath` s’appliquent uniquement aux projets utilisant `packages.config`. `globalPackagesFolder` s’applique uniquement aux projets en utilisant le format PackageReference.

| Touche | Value |
| --- | --- |
| dependencyVersion (`packages.config` uniquement) | Valeur `DependencyVersion` par défaut pour l’installation, la restauration et la mise à jour de package, quand le commutateur `-DependencyVersion` n’est pas spécifié directement. Cette valeur est également utilisée par l’interface utilisateur du Gestionnaire de package NuGet. Les valeurs sont `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (projets n’utilisant pas `packages.config`) | Emplacement du dossier de packages global par défaut. L’emplacement par défaut est `%USERPROFILE%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux). Un chemin relatif peut être utilisé dans les fichiers `Nuget.Config` spécifiques au projet. |
| repositoryPath (`packages.config` uniquement) | Emplacement dans lequel installer les packages NuGet au lieu du dossier `$(Solutiondir)/packages` par défaut. Un chemin relatif peut être utilisé dans les fichiers `Nuget.Config` spécifiques au projet. |
| defaultPushSource | Identifie l’URL ou le chemin de la source du package qui doit être utilisée comme valeur par défaut si aucune autre source de package n’est trouvée pour une opération. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Paramètres de proxy à utiliser lors de la connexion aux sources de packages ; `http_proxy` doit être au format `http://<username>:<password>@<domain>`. Les mots de passe sont chiffrés et ne peuvent pas être ajoutés manuellement. Pour `no_proxy`, la valeur est une liste de domaines séparés par des virgules qui ignorent le serveur proxy. Vous pouvez également utiliser les variables d’environnement http_proxy et no_proxy pour ces valeurs. Pour plus d’informations, consultez [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |

**Exemple** :

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a>Section bindingRedirects

Définit si NuGet effectue des redirections de liaisons automatiques quand un package est installé.

| Touche | Value |
| --- | --- |
| skip | Valeur booléenne indiquant s’il faut ignorer les redirections de liaisons automatiques. La valeur par défaut est false. |

**Exemple** :

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Section packageRestore

Contrôle la restauration de packages pendant les générations.

| Touche | Value |
| --- | --- |
| enabled | Valeur booléenne indiquant si NuGet peut effectuer une restauration automatique. Vous pouvez également définir la variable d’environnement `EnableNuGetPackageRestore` avec la valeur `True` au lieu de définir cette clé dans le fichier config. |
| automatique | Valeur booléenne indiquant si NuGet doit rechercher les packages manquants pendant une génération. |

**Exemple** :

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Section solution

Contrôle si le dossier `packages` d’une solution est inclus dans le contrôle de code source. Cette section fonctionne uniquement dans les fichiers `Nuget.Config` dans un dossier de solution.

| Touche | Value |
| --- | --- |
| disableSourceControlIntegration | Valeur booléenne indiquant s’il faut ignorer le dossier de packages lors de l’utilisation de contrôle de code source. La valeur par défaut est false. |

**Exemple** :

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Sections sur les sources de packages

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` et `disabledPackageSources` fonctionnent ensemble pour configurer la façon dont NuGet utilise les dépôts de packages pendant les opérations d’installation, de restauration et de mise à jour.

La [commande `nuget sources`](../tools/cli-ref-sources.md) est généralement utilisée pour gérer ces paramètres, à l’exception de `apikeys` qui est géré à l’aide de la [commande `nuget setapikey`](../tools/cli-ref-setapikey.md).

Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Répertorie toutes les sources de packages connues. L’ordre est ignoré pendant les opérations de restauration et aucun projet utilisant le format PackageReference. NuGet respecte l’ordre des sources pour installer et mettre à jour des opérations avec des projets à l’aide de `packages.config`.

| Touche | Value |
| --- | --- |
| (nom à assigner à la source du package) | Chemin ou URL de la source du package. |

**Exemple** :

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Stocke les noms d’utilisateur et mots de passe pour les sources, spécifiés en général en utilisant les commutateurs `-username` et `-password` avec `nuget sources`. Les mots de passe sont chiffrés par défaut, sauf si l’option `-storepasswordincleartext` est également utilisée.

| Touche | Value |
| --- | --- |
| Nom d’utilisateur | Nom d’utilisateur pour la source en texte brut. |
| mot de passe | Mot de passe chiffré pour la source. |
| cleartextpassword | Mot de passe non chiffré pour la source. |

**Exemple :**

Dans le fichier config, l’élément `<packageSourceCredentials>` contient des nœuds enfants pour chaque nom de source applicable (les espaces dans le nom sont remplacés par `_x0020_`). Autrement dit, pour les sources nommées « Contoso » et « Test Source », le fichier config contient les éléments suivants lors de l’utilisation de mots de passe chiffrés :

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

Lors de l’utilisation de mots de passe non chiffrés :

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

### <a name="apikeys"></a>apikeys

Stocke les clés pour les sources qui utilisent l’authentification de clé API, comme défini avec la [commande `nuget setapikey`](../tools/cli-ref-setapikey.md).

| Touche | Value |
| --- | --- |
| (URL source) | Clé API chiffrée. |

**Exemple** :

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Identifie les sources actuellement désactivées. Peut être vide.

| Touche | Value |
| --- | --- |
| (nom de source) | Valeur booléenne indiquant si la source est désactivée. |

**Exemple :**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(2.x uniquement ; déprécié dans 3.x+)*

Identifie la source actuellement active ou indique l’agrégat de toutes les sources.

| Touche | Value |
| --- | --- |
| (nom de source) ou `All` | Si la clé est le nom d’une source, la valeur est le chemin ou l’URL de la source. Si la clé est `All`, la valeur doit être `(Aggregate source)` pour combiner toutes les sources de packages qui ne sont pas autrement désactivées. |

**Exemple** :

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a>Utilisation de variables d’environnement

Vous pouvez utiliser des variables d’environnement dans les valeurs `NuGet.Config` (NuGet 3.4+) pour appliquer des paramètres au moment de l’exécution.

Par exemple, si la variable d’environnement `HOME` sur Windows a la valeur `c:\users\username`, la valeur `%HOME%\NuGetRepository` dans le fichier de configuration correspond à `c:\users\username\NuGetRepository`.

De même, si `HOME` sur Mac/Linux a la valeur `/home/myStuff`, `$HOME/NuGetRepository` dans le fichier de configuration correspond à `/home/myStuff/NuGetRepository`.

Si aucune variable d’environnement n’est trouvée, NuGet utilise la valeur littérale du fichier de configuration.

## <a name="example-config-file"></a>Exemple de fichier config

Voici un exemple de fichier `NuGet.Config` qui illustre un certain nombre de paramètres :

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
