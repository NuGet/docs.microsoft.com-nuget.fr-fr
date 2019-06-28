---
title: Notes de version 1.2 de NuGet
description: Notes de publication pour NuGet 1.2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426189"
---
# <a name="nuget-12-release-notes"></a>Notes de version 1.2 de NuGet

[Notes de publication de NuGet 1.0 et 1.1](../release-notes/nuget-1.1.md) | [Notes de publication de NuGet 1.3](../release-notes/nuget-1.3.md)

NuGet 1.2 a été publiée le 30 mars 2011.

## <a name="new-features"></a>Nouvelles fonctionnalités

### <a name="framework-profile-support"></a>Prise en charge du profil de Framework

À partir du début, NuGet pris en charge ayant bibliothèques ciblent différentes infrastructures. Mais maintenant les packages peuvent contenir des assemblys qui ciblent des profils spécifiques telles que le profil de Windows Phone. Pour cibler un profil d’un framework spécifique, ajoutez un tiret suivi par l’abréviation de profil. Par exemple, pour cibler SilverLight en cours d’exécution sur un Windows Phone (également appelé Windows Phone 7), vous pouvez placer un assembly dans le dossier sl3-wp, comme illustré dans la capture d’écran suivante.

![Disposition de dossier de profil de Framework](./media/framework-profile-support.png)

Vous vous demandez peut-être pourquoi nous n’avez pas choisi simplement à utiliser « wp7 » en tant que le moniker. En partie, nous attendons avec impatience que Windows Phone 7 peut exécuter une version plus récente de Silverlight à l’avenir, auquel cas vous devrez peut-être être plus précis sur l’infrastructure de profil vous êtes ciblé.

### <a name="automatically-add-binding-redirects"></a>Ajouter automatiquement les redirections de liaison

Lorsque vous installez un package avec les assemblys avec nom fort, NuGet peut désormais détecter les cas où le projet requiert des redirections à ajouter au fichier de configuration pour le projet compiler et de les ajouter automatiquement un ordre de liaison. Partie 3 de la série de publications de blog de David Ebbo sur le contrôle de version de NuGet intitulée «[Unification par le biais de liaison redirige](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)» décrit l’objectif de cette fonctionnalité dans plus de détails.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Spécification des références d’Assembly Framework (GAC)

Dans certains cas, un package peut dépendre d’un assembly qui se trouve dans le .NET Framework. À proprement parler, il n’est pas toujours nécessaire que le consommateur de votre package font référence à l’assembly framework. Mais dans certains cas, il est important, par exemple lorsque le développeur doit coder des types dans cet assembly pour pouvoir utiliser votre package. La nouvelle `frameworkAssemblies` élément, un élément enfant de l’élément de métadonnées, vous permet de spécifier un ensemble de `frameworkAssembly` éléments pointant vers un assembly de Framework dans le GAC. Notez l’accent sur l’assembly Framework.
Ces assemblys ne sont pas inclus dans votre package comme elles sont supposées pour se trouver sur chaque ordinateur en tant que partie du .NET Framework. Le tableau suivant répertorie les attributs de la `frameworkAssembly` élément.


|Attribut |Description|
|----------------|-----------|
|**assemblyName**|*Requis*. Nom de l’assembly comme `System.Net`.|
|**targetFramework**|*Facultatif*. Permet de spécifier un nom de framework et profil (ou alias) correspondant à cet assembly framework tels que « net40 » ou « sl4 ». Utilise le même format que celui décrit dans [prise en charge de plusieurs Frameworks cibles](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe est maintenant en mesure de stocker les informations d’identification de clé API

Lorsque vous utilisez l’outil de ligne de commande nuget.exe, vous pouvez maintenant utiliser la commande SetApiKey pour stocker votre clé API. De cette façon, vous ne devez spécifier chaque fois que vous envoyez un package. Pour plus d’informations sur l’enregistrement de votre clé API avec nuget.exe, [lire la documentation sur la publication d’un package](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Explorateur de package
Explorateur de package a été mis à jour pour prendre en charge NuGet 1.2. Pour plus d’informations, consultez le [notes de publication de l’Explorateur de Package](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Autres fonctionnalités/correctifs

La liste précédente ont été le plus notable de nombreuses fonctionnalités que nous avons implémenté et nous avons corrigé des bogues. En résumé, nous avons implémenté/résolu [59 des éléments de travail](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) dans cette version.

## <a name="known-issues"></a>Problèmes connus

* **1.2 incompatibilité du package**: Les packages créés avec la dernière version de l’outil de ligne de commande, nuget.exe (1.2 >) ne fonctionne pas avec les versions antérieures du complément Visual Studio NuGet (par exemple 1.1). Si vous rencontrez un message d’erreur indiquant que quelque chose sur le schéma incompatible, vous rencontrez cette erreur. Mettez à jour NuGet vers la dernière version.
* **Incompatibilité de le NuGet.Server**: Si vous hébergez un flux à l’aide du projet de le NuGet.Server de NuGet interne, vous devrez mettre à jour de ce projet avec la dernière version de le NuGet.Server.
* **Erreur d’incompatibilité de signature**: Si vous rencontrez une erreur pendant une mise à niveau avec un message sur une incompatibilité de Signature, vous devez d’abord désinstaller NuGet, puis installez-le. Il est indiqué dans notre [page problèmes connus](../release-notes/known-issues.md) qui fournit plus de détails. Le problème affecte ceux en cours d’exécution Visual Studio 2010 SP1 uniquement et une version de NuGet installé 1.0 qui ont été signées incorrectement. Cette version a été uniquement accessible depuis le site Web CodePlex pendant une brève période donc ce problème ne doivent pas affecter beaucoup de personnes.