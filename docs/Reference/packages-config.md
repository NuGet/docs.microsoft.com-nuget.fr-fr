---
title: Informations de référence sur le fichier packages.config NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Dans certains types de projets, packages.config gère la liste des packages NuGet utilisés dans le projet.
keywords: fichier packages.config NuGet, références de package NuGet, dépendances NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 38d4724d25476d372a936cb8ebf08e2b53fcf9f4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="packagesconfig-reference"></a>Informations de référence sur packages.config

Le fichier `packages.config` est utilisé dans certains types de projets pour gérer la liste des packages référencés par le projet. Cela permet à NuGet de restaurer facilement les dépendances du projet quand le projet doit être acheminé vers un autre ordinateur, tel qu’un serveur de builds, sans tous ces packages.

## <a name="schema"></a>Schéma

Le schéma est simple : l’en-tête XML standard est suivi d’un seul nœud `<packages>` qui contient un ou plusieurs éléments `<package>`, un pour chaque référence. Chaque élément `<package>` peut avoir les attributs suivants :

| Attribut | Obligatoire | Description |
| --- | --- | --- |
| ID | Oui | Identificateur du package, tel que Newtonsoft.json ou Microsoft.AspNet.Mvc. | 
| version | Oui | Version exacte du package à installer, comme 3.1.1 ou la version bêta 4.2.5.11. Une chaîne de version doit avoir au moins trois chiffres ; un quatrième est facultatif, comme un suffixe de préversion. Les plages ne sont pas autorisées. | 
| targetFramework | Non | [Moniker du Framework cible (TFM)](target-frameworks.md) à appliquer lors de l’installation du package. Cet attribut est initialement défini sur la cible du projet quand un package est installé. Par conséquent, différents éléments `<package>` peuvent avoir différents monikers TFM. Par exemple, si vous créez un projet ciblant .NET 4.5.2, les packages installés à ce stade utilisent le moniker TFM net452. Si vous reciblez ultérieurement le projet vers .NET 4.6 et ajoutez d’autres packages, ceux-ci utilisent le moniker TFM net46. Une incompatibilité entre la cible du projet et les attributs `targetFramework` génère des avertissements, auquel cas vous pouvez réinstaller les packages concernés. | 
| allowedVersions | Non | Plage de versions autorisées pour ce package appliquée au cours de la mise à jour du package (consultez [Limitation des versions de mise à niveau](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)). Cet attribut n’affecte *pas* le package installé pendant une opération d’installation ou de restauration. Consultez [Gestion de versions des packages](../reference/package-versioning.md#version-ranges-and-wildcards) pour connaître la syntaxe. L’interface utilisateur du Gestionnaire de package désactive également toutes les versions en dehors de la plage autorisée. | 
| developmentDependency | Non | Si le projet de consommation lui-même crée un package NuGet, l’affectation de la valeur `true` à cet attribut pour une dépendance empêche l’ajout de ce package quand le package de consommation est créé. La valeur par défaut est `false`. | 

## <a name="examples"></a>Exemples

L’élément `packages.config` suivant fait référence à deux dépendances :

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

L’élément`packages.config` suivant fait référence à neuf packages, mais `Microsoft.Net.Compilers` n’est pas inclus lors de la création du package de consommation en raison de l’attribut `developmentDependency`. La référence à Newtonsoft.Json restreint également les mises à jour des versions 8.x et 9.x uniquement.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
