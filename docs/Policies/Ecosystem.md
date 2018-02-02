---
title: "Vue d’ensemble de l’écosystème NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Ressources complètes dans l’écosystème NuGet, notamment des sources NuGet, des projets NuGet non-Microsoft, des utilitaires et des supports de formation NuGet."
keywords: "écosystème NuGet, projets NuGet non-Microsoft, open source NuGet, utilitaires NuGet, supports de formation NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c1e457c034f239fbea4e75f24851ea38182a294
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Vue d’ensemble de l’écosystème NuGet

Depuis son introduction en 2010, NuGet offre une opportunité exceptionnelle d’améliorer et d’automatiser différents aspects des processus de développement.

NuGet étant disponible en open source sous [licence Apache v2](http://choosealicense.com/licenses/apache/) permissive, les autres projets peuvent en tirer parti et les entreprises peuvent le prendre en charge dans leurs produits. Que ce soit pour des projets open source ou pour le développement d’applications d’entreprise, NuGet et les autres applications basées ou axées sur NuGet fournissent un vaste écosystème d’outils pour améliorer votre processus de développement logiciel.

Tous ces projets sont sources d’innovation grâce aux contributions des développeurs. De la même manière que vous contribuez à NuGet lui-même, vous pouvez contribuer à ces projets en signalant des défauts, en proposant de nouvelles fonctionnalités, en formulant des commentaires, en écrivant de la documentation et en contribuant au code quand cela est possible.

## <a name="net-foundation-projects"></a>Projets .NET Foundation

NuGet fournit un système de gestion de packages gratuit et open source pour la plateforme de développement Microsoft. Il se compose de quelques outils clients, ainsi que de l’ensemble des services qui constituent la [Galerie NuGet officielle](http://www.nuget.org). Combinés, ils forment le projet NuGet régi par la [.NET Foundation](http://www.dotnetfoundation.org/).

L’organisation NuGet contient plusieurs dépôts sur GitHub. [https://github.com/NuGet/Home](https://github.com/Nuget/Home) donne une vue d’ensemble de tous les dépôts et des emplacements des différents composants NuGet.

## <a name="microsoft-projects"></a>Projets Microsoft

Microsoft a contribué largement au développement de NuGet. Toutes les contributions apportées par les employés Microsoft sont également open source et sont données (droits d’auteur compris) à la .NET Foundation.

## <a name="non-microsoft-projects"></a>Projets non-Microsoft

De nombreuses autres personnes et entreprises ont apporté des contributions importantes à l’écosystème NuGet. La licence de chaque projet répertorié ici pouvant différer de celle des composants NuGet principaux, vérifiez que les termes du contrat de licence sont acceptables avant d’utiliser le produit concerné :

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (ou NuGet-as-a-service)](http://www.myget.org/)
- [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Server](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin et MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Autres utilitaires basés sur NuGet

Il s’agit d’outils et d’utilitaires reposant sur NuGet :

- [Extensions Glimpse](http://getglimpse.com/Packages) (les plug-ins sont des packages)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (les modules CMS sont extraits d’un flux NuGet v1 hébergé dans la galerie Orchard)
- [Implémentation Java de NuGet Server](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (robot Twitter tweetant de nouvelles publications package)
- [DefinitelyTyped](http://definitelytyped.org/) ([Définitions publiées sur NuGet](http://www.nuget.org/packages?q=DefinitelyTyped) de type TypeScript [automatique](https://github.com/DefinitelyTyped/NugetAutomation/))

## <a name="training-materials-and-references"></a>Références et supports de formation

L’utilisation d’un nouvel outil ou technologie est généralement assortie d’une courbe d’apprentissage. Heureusement, la courbe d’apprentissage de NuGet ne présente aucune difficulté ! En fait, toute personne peut [commencer à consommer des packages](../quickstart/use-a-package.md) rapidement.

Ceci dit, la création de packages, et particulièrement de packages de qualité, ainsi que l’adoption de NuGet dans les processus de génération et de déploiement automatisés, nécessitent de consacrer un peu plus de temps aux ressources suivantes :

- [Blog NuGet](http://blog.nuget.org/)
- [Équipe NuGet sur Twitter, @nuget](http://twitter.com/nuget)
- Livres :
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Documentation pour des packages individuels

[NuDoq](http://nudoq.org) fournit un accès simple aux packages NuGet, des mises à jour de ces derniers et de la documentation à leur sujet.

NuDoq interroge régulièrement le serveur de la galerie nuget.org pour récupérer les dernières mises à jour de package, décompresse et traite les fichiers de la documentation de la bibliothèque et met à jour le site en conséquence.

## <a name="adding-your-project"></a>Ajout de votre projet

Si vous avez un projet d’écosystème NuGet susceptible d’enrichir cette page, envoyez une demande de tirage (pull request) avec une modification de cette page.
