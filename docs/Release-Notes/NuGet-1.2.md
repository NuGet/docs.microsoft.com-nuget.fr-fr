---
title: Notes de publication NuGet 1.2 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet 1.2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 1.2, les correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cb9eb1cb8fc3a77fc297e04ce73aaf8e24fc557a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-12-release-notes"></a>Notes de version 1.2 de NuGet

[Notes de version 1.0 et 1.1 de NuGet](../release-notes/nuget-1.1.md) | [NuGet 1.3 Notes de publication](../release-notes/nuget-1.3.md)

NuGet 1.2 a été publiée le 30 mars 2011.

## <a name="new-features"></a>Nouvelles fonctionnalités

### <a name="framework-profile-support"></a>Prise en charge du profil de Framework

À partir du début, NuGet pris en charge avec les bibliothèques ciblent différentes infrastructures. Mais maintenant les packages peuvent contenir des assemblys qui ciblent des profils spécifiques telles que le profil de Windows Phone. Pour cibler un profil spécifique d’une infrastructure, ajoutez un tiret, suivi de l’abréviation de profil. Par exemple, pour cibler SilverLight en cours d’exécution sur un Windows Phone (également appelé Windows Phone 7), vous pouvez placer un assembly dans le dossier sl3-wp, comme illustré dans la capture d’écran suivante.

![Disposition de dossier de profil de Framework](./media/framework-profile-support.png)

Vous vous demandez peut-être pourquoi nous n’avez pas choisi simplement utiliser « wp7 » en tant que moniker. En partie, nous allons anticipation que Windows Phone 7 peut exécuter une version plus récente de Silverlight dans le futur, auquel cas vous devrez peut-être plus spécifiques sur l’infrastructure de profil vous êtes ciblé.

### <a name="automatically-add-binding-redirects"></a>Ajouter automatiquement les redirections de liaison

Lorsque vous installez un package avec les assemblys avec nom fort, NuGet peut désormais détecter les cas où le projet requiert des redirections à ajouter au fichier de configuration pour le projet compiler et les ajouter automatiquement un ordre de liaison. Partie 3 de la série de billet de blog de David Ebbo sur le contrôle de version de NuGet intitulée «[Unification par redirections de liaison](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)» décrit l’objectif de cette fonctionnalité dans plus de détails.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Spécification des références d’Assembly Framework (GAC)

Dans certains cas, un package peut dépendre d’un assembly qui est dans le .NET Framework. En principe, il n’est pas toujours nécessaire que le consommateur de votre package de référence l’assembly framework. Mais dans certains cas, il est important, par exemple lorsque le développeur doit coder des types dans cet assembly pour pouvoir utiliser votre package. La nouvelle `frameworkAssemblies` élément, un élément enfant de l’élément de métadonnées, vous permet de spécifier un ensemble de `frameworkAssembly` éléments pointant vers un assembly de Framework dans le GAC. Notez l’accent sur l’assembly Framework.
Ces assemblys ne sont pas inclus dans votre package comme elles sont supposées se pour trouver sur chaque ordinateur dans le cadre du .NET Framework. Le tableau suivant répertorie les attributs de la `frameworkAssembly` élément.


|Attribut |Description|
|----------------|-----------|
|**assemblyName**|*Requise*. Nom de l’assembly comme `System.Net`.|
|**targetFramework**|*Facultatif*. Permet de spécifier un nom de profil et le framework (ou alias) correspondant à cet assembly framework tels que « net40 » ou « sl4 ». Utilise le même format que celui décrit dans [prenant en charge plusieurs infrastructures de cible](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe est désormais en mesure de stocker les informations d’identification de la clé d’API

Lorsque vous utilisez l’outil de ligne de commande nuget.exe, vous pouvez désormais utiliser la commande SetApiKey pour stocker votre clé API. De cette façon, vous n’aurez pas à spécifier chaque fois que vous effectuez un push un package. Pour plus d’informations sur l’enregistrement de votre clé API avec nuget.exe, [lire la documentation sur la publication d’un package](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Explorateur de package
Explorateur de package a été mis à jour pour prendre en charge NuGet 1.2. Pour plus d’informations, consultez la [notes de version de l’Explorateur de Package](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Autres fonctionnalités/correctifs

La liste précédente a été le plus notable des nombreuses fonctionnalités que nous avons implémenté et nous corrigés. Dans l’ensemble, nous avons implémenté/fixe [59 des éléments de travail](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) dans cette version.

## <a name="known-issues"></a>Problèmes connus

* **1.2 incompatibilité du package**: Packages générés avec la version la plus récente de l’outil de ligne de commande, de nuget.exe (1.2 >) ne fonctionne pas avec les versions antérieures du complément Visual Studio de NuGet (par exemple 1.1). Si vous rencontrez un message d’erreur indiquant que des informations sur le schéma incompatible, vous rencontrez cette erreur. Mettez à jour NuGet vers la dernière version.
* **Incompatibilité de NuGet.Server**: Si vous hébergez un flux à l’aide du projet NuGet.Server de NuGet interne, vous devez mettre à jour de ce projet avec la version la plus récente de NuGet.Server.
* **Erreur d’incompatibilité de signature**: Si vous rencontrez une erreur pendant une mise à niveau avec un message sur une incompatibilité de Signature, vous devez d’abord désinstaller NuGet, puis installez-le. Cette information est répertoriée dans notre [page problèmes connus](../release-notes/Known-Issues.md) qui fournit plus de détails. Le problème affecte ceux exécutant Visual Studio 2010 SP1 uniquement et disposez d’une version 1.0 de NuGet installés qui ont été signées incorrectement. Cette version a été uniquement accessibles depuis le site Web CodePlex pendant une brève période afin de ce problème ne devrait pas affecter trop d’utilisateurs.