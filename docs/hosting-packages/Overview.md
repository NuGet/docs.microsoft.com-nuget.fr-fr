---
title: Vue d’ensemble de l’hébergement de vos propres flux NuGet
description: Vue d’ensemble des possibilités d’hébergement de vos propres galeries ou flux de packages NuGet localement ou à distance.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 81acf15ac69d78d39d2784e77c18ba38bfea126d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385540"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hébergement de vos propres flux NuGet

Plutôt que de mettre les packages à la disposition de tous, vous pouvez les réserver à un public limité, tel que votre organisation ou groupe de travail. De plus, certaines sociétés peuvent souhaiter restreindre les bibliothèques tierces que sont susceptibles d’utiliser leurs développeurs en leur demandant de puiser dans une source de packages limitée plutôt que dans nuget.org.

À ces fins, NuGet prend en charge la configuration de sources de packages privées des façons suivantes :

- Flux local : les packages sont simplement placés sur un partage de fichiers réseau approprié, dans l’idéal, en utilisant `nuget init` et `nuget add` pour créer une structure de dossiers hiérarchique (NuGet 3.3+). Pour plus d’informations, consultez [Flux locaux](../hosting-packages/local-feeds.md).
- NuGet.Server : les packages sont accessibles via un serveur HTTP local. Pour plus d’informations, consultez [NuGet.Server](../hosting-packages/nuget-server.md).
- Galerie NuGet : les packages sont hébergés sur un serveur Internet à l’aide du [projet de Galerie NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). Avec la Galerie NuGet, gérez les utilisateurs et profitez de fonctionnalités telles qu’une interface utilisateur web complète qui permet de rechercher et d’explorer les packages à partir du navigateur, comme nuget.org.

Il existe également plusieurs autres produits d’hébergement NuGet, tels que [Azure artifacts](https://www.visualstudio.com/docs/package/nuget/publish) et le [Registre de packages GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) qui prennent en charge les flux privés distants. Vous trouverez ci-dessous une liste de ces produits :

- [Artifactory](https://www.jfrog.com/artifactory/) de JFrog
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), qui est également disponible sur Team Foundation Server 2017 et ultérieur.
- [BaGet](https://github.com/loic-sharma/BaGet), implémentation open source du serveur NuGet V3 reposant sur ASP.NET Core
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), un Saas entièrement géré pour la gestion des packages
- [Registre de package GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), une implémentation open source du serveur NuGet V2 qui s’exécute sur Kestrel dans Docker
- [MyGet](https://myget.org)
- [OSS du référentiel](https://www.sonatype.com/nexus-repository-oss) de la réversion de Sonatype.
- [NuGet Server (Open Source)](https://github.com/svenkle/nuget-server) : implémentation open source similaire à NuGet Server d’Inedo
- [NuGet Server](http://nugetserver.net/) : projet communautaire d’Inedo
- [ProGet](https://inedo.com/proget) d’Inedo
- [Sleet](https://github.com/emgarten/sleet), un générateur de flux statique NuGet V3 open source
- [TeamCity](https://www.jetbrains.com/teamcity/) de JetBrains

Quelle que soit la façon dont les packages sont hébergés, vous y accédez en les ajoutant à la liste des sources disponibles dans `NuGet.Config`. Vous pouvez effectuer cette opération dans Visual Studio, comme décrit dans [Sources de packages](../consume-packages/install-use-packages-visual-studio.md#package-sources), ou à partir de la ligne de commande à l’aide de [`nuget sources`](../reference/cli-reference/cli-ref-sources.md). Le chemin d’une source peut être le chemin d’un dossier local, le nom d’un réseau ou une URL.
