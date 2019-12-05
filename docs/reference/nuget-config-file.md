---
title: informations de référence sur le fichier NuGet. config
description: Informations de référence sur le fichier NuGet.Config, notamment les sections config, bindingRedirects, packageRestore, solution et packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 0b052bd03625172f1b941c365cbedf7629809d6f
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825189"
---
# <a name="nugetconfig-reference"></a>informations de référence sur NuGet. config

Le comportement de NuGet est contrôlé par des paramètres dans différents fichiers `NuGet.Config` ou `nuget.config`, comme décrit dans [configurations NuGet courantes](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` est un fichier XML contenant un nœud `<configuration>` de niveau supérieur qui comprend à son tour les éléments de section décrits dans cette rubrique. Chaque section contient zéro ou plusieurs éléments. Consultez [l’exemple de fichier config](#example-config-file). Les noms de paramètre ne respectent pas la casse et les valeurs peuvent utiliser des [variables d’environnement](#using-environment-variables).

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Section config

Contient des paramètres de configuration divers, qui peuvent être définis à l’aide de la [commande `nuget config`](../reference/cli-reference/cli-ref-config.md).

`dependencyVersion` et `repositoryPath` s’appliquent uniquement aux projets utilisant `packages.config`. `globalPackagesFolder` s’applique uniquement aux projets utilisant le format PackageReference.

| Clé | Value |
| --- | --- |
| dependencyVersion (`packages.config` uniquement) | Valeur `DependencyVersion` par défaut pour l’installation, la restauration et la mise à jour de package, quand le commutateur `-DependencyVersion` n’est pas spécifié directement. Cette valeur est également utilisée par l’interface utilisateur du Gestionnaire de package NuGet. Les valeurs sont `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (projets utilisant PackageReference uniquement) | Emplacement du dossier de packages global par défaut. L’emplacement par défaut est `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux). Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet. Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire. |
| repositoryPath (`packages.config` uniquement) | Emplacement dans lequel installer les packages NuGet au lieu du dossier `$(Solutiondir)/packages` par défaut. Un chemin relatif peut être utilisé dans les fichiers `nuget.config` spécifiques au projet. Ce paramètre est remplacé par la variable d’environnement NUGET_PACKAGES, qui est prioritaire. |
| defaultPushSource | Identifie l’URL ou le chemin de la source du package qui doit être utilisée comme valeur par défaut si aucune autre source de package n’est trouvée pour une opération. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Paramètres de proxy à utiliser lors de la connexion aux sources de packages ; `http_proxy` doit être au format `http://<username>:<password>@<domain>`. Les mots de passe sont chiffrés et ne peuvent pas être ajoutés manuellement. Pour `no_proxy`, la valeur est une liste de domaines séparés par des virgules qui ignorent le serveur proxy. Vous pouvez également utiliser les variables d’environnement http_proxy et no_proxy pour ces valeurs. Pour plus d’informations, consultez [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Spécifie le mode de validation utilisé pour vérifier les signatures de package pour l’installation du package et la restauration. Les valeurs sont `accept`, `require`. La valeur par défaut est `accept`.

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

| Clé | Value |
| --- | --- |
| skip | Valeur booléenne indiquant s’il faut ignorer les redirections de liaisons automatiques. La valeur par défaut est False. |

**Exemple** :

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Section packageRestore

Contrôle la restauration de packages pendant les générations.

| Clé | Value |
| --- | --- |
| activé | Valeur booléenne indiquant si NuGet peut effectuer une restauration automatique. Vous pouvez également définir la variable d’environnement `EnableNuGetPackageRestore` avec la valeur `True` au lieu de définir cette clé dans le fichier config. |
| automatic | Valeur booléenne indiquant si NuGet doit rechercher les packages manquants pendant une génération. |

**Exemple** :

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Section solution

Contrôle si le dossier `packages` d’une solution est inclus dans le contrôle de code source. Cette section fonctionne uniquement dans les fichiers `nuget.config` dans un dossier de solution.

| Clé | Value |
| --- | --- |
| disableSourceControlIntegration | Valeur booléenne indiquant s’il faut ignorer le dossier de packages lors de l’utilisation de contrôle de code source. La valeur par défaut est false. |

**Exemple** :

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Sections sur les sources de packages

Les `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` et `trustedSigners` fonctionnent ensemble pour configurer la façon dont NuGet fonctionne avec les dépôts de packages pendant les opérations d’installation, de restauration et de mise à jour.

La [commande`nuget sources`](../reference/cli-reference/cli-ref-sources.md) est généralement utilisée pour gérer ces paramètres, à l’exception de `apikeys` qui est gérée à l’aide de la [commande`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md)et `trustedSigners` qui est gérée à l’aide de la [commande`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).

Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Répertorie toutes les sources de packages connues. L’ordre est ignoré pendant les opérations de restauration et avec n’importe quel projet utilisant le format PackageReference. NuGet respecte l’ordre des sources pour les opérations d’installation et de mise à jour des projets à l’aide de `packages.config`.

| Clé | Value |
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

| Clé | Value |
| --- | --- |
| nom_utilisateur | Nom d’utilisateur pour la source en texte brut. |
| mot de passe du . | Mot de passe chiffré pour la source. |
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

Stocke les clés pour les sources qui utilisent l’authentification de clé API, comme défini avec la [commande `nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).

| Clé | Value |
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

| Clé | Value |
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

| Clé | Value |
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

## <a name="trustedsigners-section"></a>section trustedSigners

Stocke les signataires approuvés utilisés pour autoriser le package lors de l’installation ou de la restauration. Cette liste ne peut pas être vide lorsque l’utilisateur définit `signatureValidationMode` sur `require`. 

Cette section peut être mise à jour à l’aide de la [commande`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).

**Schéma** :

Un signataire approuvé contient une collection d’éléments `certificate` qui inscrivent tous les certificats qui identifient un signataire donné. Un signataire approuvé peut être un `Author` ou un `Repository`.

Un *référentiel* approuvé spécifie également les `serviceIndex` pour le dépôt (qui doit être un URI `https` valide) et peut éventuellement spécifier une liste de `owners` délimitée par des points-virgules pour limiter encore plus les personnes autorisées à partir de ce référentiel spécifique.

Les algorithmes de hachage pris en charge utilisés pour une empreinte digitale de certificat sont `SHA256`, `SHA384` et `SHA512`.

Si un `certificate` spécifie `allowUntrustedRoot` comme `true` le certificat donné est autorisé à se lier à une racine non approuvée lors de la génération de la chaîne de certificats dans le cadre de la vérification de la signature.

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

## <a name="fallbackpackagefolders-section"></a>section fallbackPackageFolders

*(3.5 +)* Fournit un moyen de préinstaller des packages afin qu’aucun travail ne doive être effectué si le package se trouve dans les dossiers de secours. Les dossiers de package de secours ont exactement la même structure de dossiers et de fichiers que le dossier de package global : *. nupkg* est présent et tous les fichiers sont extraits.

La logique de recherche pour cette configuration est la suivante :

- Recherchez dans le dossier de package global pour voir si le package/la version est déjà téléchargé.

- Recherchez dans les dossiers de secours un package/version correspondant.

Si une recherche est réussie, aucun téléchargement n’est nécessaire.

Si aucune correspondance n’est trouvée, NuGet vérifie les sources de fichiers, puis les sources http, puis télécharge les packages.

| Clé | Value |
| --- | --- |
| (nom du dossier de secours) | Chemin d’accès au dossier de secours. |

**Exemple** :

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>packageManagement (section)

Définit le format de gestion de package par défaut, *packages. config* ou PackageReference. Les projets de style SDK utilisent toujours PackageReference.

| Clé | Value |
| --- | --- |
| format | Valeur booléenne qui indique le format de gestion des packages par défaut. Si `1`, le format est PackageReference. Si `0`, le format est *packages. config*. |
| désactivés | Valeur booléenne indiquant s’il faut afficher l’invite de sélection d’un format de package par défaut lors de la première installation de package. `False` masque l’invite. |

**Exemple** :

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
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
