---
title: Référence du fichier NuGet.config
description: Informations de référence sur le fichier NuGet.Config, notamment les sections config, bindingRedirects, packageRestore, solution et packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 2eceb6e94a353cb29b83aea114c6cea2acbac266
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426144"
---
# <a name="nugetconfig-reference"></a>nuget.config reference

Comportement de NuGet est contrôlé par les paramètres dans différents `NuGet.Config` comme décrit dans les fichiers [les configurations courantes NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` est un fichier XML contenant un nœud `<configuration>` de niveau supérieur qui comprend à son tour les éléments de section décrits dans cette rubrique. Chaque section contient zéro ou plusieurs éléments. Consultez [l’exemple de fichier config](#example-config-file). Les noms de paramètre ne respectent pas la casse et les valeurs peuvent utiliser des [variables d’environnement](#using-environment-variables).

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
- [section de trustedSigners](#trustedsigners-section)
- [Utilisation de variables d’environnement](#using-environment-variables)
- [Exemple de fichier config](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Section config

Contient des paramètres de configuration divers, qui peuvent être définis à l’aide de la [commande `nuget config`](../tools/cli-ref-config.md).

`dependencyVersion` et `repositoryPath` s’appliquent uniquement aux projets utilisant `packages.config`. `globalPackagesFolder` s’applique uniquement aux projets utilisant le format PackageReference.

| Touche | Value |
| --- | --- |
| dependencyVersion (`packages.config` uniquement) | Valeur `DependencyVersion` par défaut pour l’installation, la restauration et la mise à jour de package, quand le commutateur `-DependencyVersion` n’est pas spécifié directement. Cette valeur est également utilisée par l’interface utilisateur du Gestionnaire de package NuGet. Les valeurs sont `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (projets à l’aide de PackageReference uniquement) | Emplacement du dossier de packages global par défaut. L’emplacement par défaut est `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux). Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet. Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire. |
| repositoryPath (`packages.config` uniquement) | Emplacement dans lequel installer les packages NuGet au lieu du dossier `$(Solutiondir)/packages` par défaut. Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet. Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire. |
| defaultPushSource | Identifie l’URL ou le chemin de la source du package qui doit être utilisée comme valeur par défaut si aucune autre source de package n’est trouvée pour une opération. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Paramètres de proxy à utiliser lors de la connexion aux sources de packages ; `http_proxy` doit être au format `http://<username>:<password>@<domain>`. Les mots de passe sont chiffrés et ne peuvent pas être ajoutés manuellement. Pour `no_proxy`, la valeur est une liste de domaines séparés par des virgules qui ignorent le serveur proxy. Vous pouvez également utiliser les variables d’environnement http_proxy et no_proxy pour ces valeurs. Pour plus d’informations, consultez [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Spécifie le mode de validation utilisé pour vérifier les signatures de package pour l’installation du package et de restauration. Les valeurs sont `accept`, `require`. La valeur par défaut est `accept`.

**Exemple** :

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
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

Contrôle si le dossier `packages` d’une solution est inclus dans le contrôle de code source. Cette section fonctionne uniquement dans les fichiers `nuget.config` dans un dossier de solution.

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

Le `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` et `trustedSigners` fonctionnent ensemble pour configurer le fonctionne de NuGet avec les référentiels de package pendant l’installation, la restauration et les opérations de mise à jour.

Le [ `nuget sources` commande](../tools/cli-ref-sources.md) est généralement utilisée pour gérer ces paramètres, à l’exception de `apikeys` qui est gérée à l’aide de la [ `nuget setapikey` commande](../tools/cli-ref-setapikey.md), et `trustedSigners` qui est gérée à l’aide de la [ `nuget trusted-signers` commande](../tools/cli-ref-trusted-signers.md).

Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Répertorie toutes les sources de packages connues. L’ordre est ignoré pendant les opérations de restauration et avec n’importe quel projet en utilisant le format PackageReference. NuGet respecte l’ordre des sources pour installer et mettre à jour des opérations avec des projets à l’aide de `packages.config`.

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
## <a name="trustedsigners-section"></a>section de trustedSigners

Magasins approuvé utilisés pour permettre de package lors de l’installation ou la restauration des signataires. Cette liste ne peut pas être vide lorsque l’utilisateur définit `signatureValidationMode` à `require`. 

Cette section peut être mis à jour avec la [ `nuget trusted-signers` commande](../tools/cli-ref-trusted-signers.md).

**Schéma**:

Un signataire approuvé possède une collection de `certificate` éléments inscrire tous les certificats qui identifient un signataire donné. Un signataire approuvé peut être un `Author` ou un `Repository`.

Approuvé *référentiel* spécifie également le `serviceIndex` pour le dépôt (qui doit être valide `https` uri) et vous pouvez éventuellement spécifier une liste délimitée par des points-virgules de `owners` pour limiter encore plus qui est approuvé à partir de ce référentiel spécifique.

Les algorithmes de hachage pris en charge utilisés pour une empreinte de certificat sont `SHA256`, `SHA384` et `SHA512`.

Si un `certificate` spécifie `allowUntrustedRoot` comme `true` le certificat donné est autorisé à la chaîne à une racine non approuvée pendant la génération de la chaîne de certificats dans le cadre de la vérification de signature.

**Exemple** :

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

## <a name="using-environment-variables"></a>Utilisation de variables d’environnement

Vous pouvez utiliser des variables d’environnement dans les valeurs `nuget.config` (NuGet 3.4+) pour appliquer des paramètres au moment de l’exécution.

Par exemple, si la variable d’environnement `HOME` sur Windows a la valeur `c:\users\username`, la valeur `%HOME%\NuGetRepository` dans le fichier de configuration correspond à `c:\users\username\NuGetRepository`.

De même, si `HOME` sur Mac/Linux a la valeur `/home/myStuff`, `%HOME%/NuGetRepository` dans le fichier de configuration correspond à `/home/myStuff/NuGetRepository`.

Si aucune variable d’environnement n’est trouvée, NuGet utilise la valeur littérale du fichier de configuration.

## <a name="example-config-file"></a>Exemple de fichier config

Voici un exemple de fichier `nuget.config` qui illustre un certain nombre de paramètres :

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
