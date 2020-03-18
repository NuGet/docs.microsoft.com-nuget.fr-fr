---
title: Notes de publication de NuGet 1,2
description: Notes de publication de NuGet 1,2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429086"
---
# <a name="nuget-12-release-notes"></a>Notes de publication de NuGet 1,2

[Notes de publication de nuget 1,0 et 1,1](../release-notes/nuget-1.1.md) | [notes de publication de NuGet 1,3](../release-notes/nuget-1.3.md)

NuGet 1,2 a été publié le 30 mars 2011.

## <a name="new-features"></a>Nouvelles fonctionnalités

### <a name="framework-profile-support"></a>Prise en charge des profils de Framework

Depuis le début, NuGet prenait en charge les bibliothèques qui ciblent différents frameworks. Mais maintenant, les packages peuvent contenir des assemblys qui ciblent des profils spécifiques tels que le profil de Windows Phone. Pour cibler un profil spécifique d’une infrastructure, ajoutez un tiret suivi de l’abréviation de profil. Par exemple, pour cibler SilverLight exécuté sur un Windows Phone (Windows Phone 7), vous pouvez placer un assembly dans le dossier SL3-WP, comme illustré dans la capture d’écran suivante.

![Disposition des dossiers du profil du Framework](./media/framework-profile-support.png)

Vous pouvez vous demander pourquoi nous n’avons pas simplement choisi d’utiliser « WP7 » comme moniker. En partie, nous anticipons que Windows Phone 7 peut exécuter une version plus récente de Silverlight à l’avenir. dans ce cas, vous devrez peut-être être plus précis sur le profil Framework que vous ciblez.

### <a name="automatically-add-binding-redirects"></a>Ajouter automatiquement des redirections de liaison

Lors de l’installation d’un package avec des assemblys avec nom fort, NuGet peut désormais détecter les cas où le projet requiert que les redirections de liaison soient ajoutées au fichier de configuration pour que le projet puisse être compilé et ajouté automatiquement. La partie 3 de la série de billets de blog de David Ebbo sur le contrôle de version NuGet intitulé «[unification via les redirections de liaison](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)» couvre l’objectif de cette fonctionnalité plus en détail.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Spécification des références d’assembly Framework (GAC)

Dans certains cas, un package peut dépendre d’un assembly qui se trouve dans le .NET Framework. Strictement parlant, il n’est pas toujours nécessaire que le consommateur de votre package référence l’assembly Framework. Toutefois, dans certains cas, il est important, par exemple quand le développeur a besoin de coder par rapport à des types dans cet assembly afin d’utiliser votre package. Le nouvel élément `frameworkAssemblies`, un élément enfant de l’élément Metadata, vous permet de spécifier un ensemble d’éléments `frameworkAssembly` qui pointent vers un assembly Framework dans le GAC. Notez l’importance de l’assembly de Framework.
Ces assemblys ne sont pas inclus dans votre package, car ils sont supposés se trouver sur chaque ordinateur dans le cadre de la .NET Framework. Le tableau suivant répertorie les attributs de l’élément `frameworkAssembly`.


|Attribut |Description|
|----------------|-----------|
|**assemblyName**|*Requis*. Nom de l’assembly, par exemple `System.Net`.|
|**targetFramework**|*Facultatif*. Permet de spécifier un Framework et un nom de profil (ou alias) auxquels cet assembly d’infrastructure s’applique, tel que « net40 » ou « SL4 ». Utilise le même format que celui décrit dans [prise en charge de plusieurs frameworks cibles](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet. exe est désormais en mesure de stocker les informations d’identification de clé API

Lorsque vous utilisez l’outil en ligne de commande NuGet. exe, vous pouvez maintenant utiliser la commande SetApiKey pour stocker votre clé API. De cette façon, vous n’aurez pas besoin de le spécifier chaque fois que vous envoyez un package. Pour plus d’informations sur l’enregistrement de votre clé API avec NuGet. exe, [consultez la documentation sur la publication d’un package](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Explorateur de package
L’Explorateur de package a été mis à jour pour prendre en charge NuGet 1,2. Pour plus d’informations, consultez les [notes de publication](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)de l’Explorateur de package.

## <a name="other-featuresfixes"></a>Autres fonctionnalités/correctifs

La liste précédente était la plus perceptible des nombreuses fonctionnalités que nous avons implémentées et des bogues résolus. En tout, nous avons implémenté/corrigé [59 éléments de travail](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) dans cette version.

## <a name="known-issues"></a>Problèmes connus

* **1,2 incompatibilité de package**: les packages générés avec la dernière version de l’outil en ligne de commande, NuGet. exe (> 1,2) ne fonctionneront pas avec les versions antérieures du complément NuGet vs (par exemple, 1,1). Si vous rencontrez un message d’erreur indiquant un schéma incompatible, vous exécutez cette erreur. Veuillez mettre à jour NuGet vers la dernière version.
* **Incompatibilité de NuGet. Server**: Si vous hébergez un flux NuGet interne à l’aide du projet NuGet. Server, vous devez mettre à jour ce projet avec la dernière version de NuGet. Server.
* **Erreur d’incompatibilité de signature**: Si vous rencontrez une erreur lors d’une mise à niveau avec un message relatif à une incompatibilité de signature, vous devez d’abord désinstaller NuGet, puis l’installer. Cela est répertorié dans la [page problèmes connus](../release-notes/known-issues.md) qui fournit plus de détails. Le problème affecte uniquement ceux qui exécutent Visual Studio 2010 SP1 et dont une version de NuGet 1,0 installée n’a pas été correctement signée. Cette version n’était disponible qu’à partir du site Web CodePlex pendant une courte période, ce problème ne devrait donc pas affecter trop de personnes.