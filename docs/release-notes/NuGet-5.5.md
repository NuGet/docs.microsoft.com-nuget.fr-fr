---
title: Notes de publication de NuGet 5,5
description: Notes de publication de NuGet 5,5, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780109"
---
# <a name="nuget-55-release-notes"></a>Notes de publication de NuGet 5,5

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio| Disponible dans les SDK .NET|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core

## <a name="summary-whats-new-in-55"></a>Résumé : nouveautés de 5,5

* Amélioration de l’accessibilité et du lecteur d’écran pour l’interface utilisateur du gestionnaire de package NuGet dans Visual Studio
    * Problèmes d’accessibilité dans l’expérience du lecteur d’écran, altText et nom accessible manquants pour la zone de texte installée, etc.,- [#9059](https://github.com/NuGet/Home/issues/9059)
    * Problèmes d’accessibilité dans les expériences de lecteur d’écran dans la liste des packages- [#9077](https://github.com/NuGet/Home/issues/9077)
    * Problèmes d’accessibilité dans les environnements de lecteur d’écran liés aux onglets « parcourir », « installer », « mettre à jour »- [#9078](https://github.com/NuGet/Home/issues/9078)
    * Le narrateur n’annonce pas « vide », « aucune Dependencies","NuGet. org », étiquette de lien « MIT » [#9157](https://github.com/NuGet/Home/issues/9157)

* Prise en charge de l’apprentissage des icônes autonomes dans l’interface utilisateur du gestionnaire de package Visual Studio pour les packages hébergés sur des flux locaux- [#8189](https://github.com/NuGet/Home/issues/8189)

* Amélioration significative des performances de restauration sans opération utilisant pour `RestoreUseStaticGraphEvaluation` accélérer les évaluations en appelant les API Graph statiques MSBuild- [8791](https://github.com/NuGet/Home/issues/8791)

* Amélioration de la fiabilité des dotnet.exe avec les plug-ins d’authentification multiplateforme
    * échec de dotnet restore avec TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)
    * Plug-in : « une tâche a été annulée »-problème avec l’authentification ADO en raison de cette erreur. - [#8528](https://github.com/NuGet/Home/issues/8528)

* Ajouter `dotnet nuget <add|remove|update|disable|enable|list> source` une [#4126](https://github.com/NuGet/Home/issues/4126) de commande

* La `--skip-duplicate`  diffusion pour l’utilisation de dotnet NuGet Push- [#8778](https://github.com/NuGet/Home/issues/8778)

* Prise en charge `packages.config` de MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Bogues**

* Réutiliser les Self-Updater avec des API V3- [#4197](https://github.com/NuGet/Home/issues/4197)

* Version de dépendance de package incorrecte si la version de dépendance de package est définie sur « * »- [#6697](https://github.com/NuGet/Home/issues/6697)

* Le message d’erreur ErrorUnsafePackageEntry ne pointe pas vers la source du problème- [#7505](https://github.com/NuGet/Home/issues/7505)

* Le fichier de verrouillage n’est pas respecté dans les scénarios « * »- [#8073](https://github.com/NuGet/Home/issues/8073)

* NuGet.exe ne correspond pas à la version la plus récente d’un package lors de l’utilisation de * dans PackageReference (MSBuild/dotnet/VS Restore do)- [#8432](https://github.com/NuGet/Home/issues/8432)

* package de liste dotnet avec multi-ciblage de projets WPF- [#8463](https://github.com/NuGet/Home/issues/8463)

* Améliorer les ConcurrencyUtilities (réduire l’utilisation de l’UC)- [#8653](https://github.com/NuGet/Home/issues/8653)

* Les spécifications de la DG pour les scénarios de projets déchargés ne doivent pas être écrites dans les restaurations d’aperçu- [#8793](https://github.com/NuGet/Home/issues/8793)

* Les packages NuGet de Visual Studio (RestoreManagerPackage) doivent être chargés automatiquement sur les événements de build de solution- [#8796](https://github.com/NuGet/Home/issues/8796)

* Blocage dans VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)

* La boîte à outils de VisualStudio n’est pas remplie à partir d’un package NuGet si un projet est placé dans un dossier de solution- [#8868](https://github.com/NuGet/Home/issues/8868)

* VS : la restauration de solution a échoué en raison d’une condition de concurrence critique [#8881](https://github.com/NuGet/Home/issues/8881)

* Constante « chargement en cours.. » sur l’onglet installé et «recherche <term>..» sous l’onglet mises à jour- [#8890](https://github.com/NuGet/Home/issues/8890)

* Icônes incorporées manquantes dans l’interface utilisateur de VS PM après expiration du cache- [#9069](https://github.com/NuGet/Home/issues/9069)

* Démarrage de l’interface utilisateur FireAndForget PM- [#9112](https://github.com/NuGet/Home/issues/9112)

* Restauration : l’implémentation de IncludeExcludeFiles. Equals (...) est incorrecte- [#9167](https://github.com/NuGet/Home/issues/9167)

* Restauration : PackageSpec. Clone () crée une [#9211](https://github.com/NuGet/Home/issues/9211) de clonage inégale

* Liste d’erreurs affichée bien que « toujours afficher Liste d’erreurs si la génération se termine avec des erreurs » n’est pas vérifiée- [#8190](https://github.com/NuGet/Home/issues/8190)

* La restauration du graphique statique ne doit pas passer un SolutionPath vide- [#9061](https://github.com/NuGet/Home/issues/9061)

* Restauration : fermeture calculée pour chaque projet 4 fois- [#9042](https://github.com/NuGet/Home/issues/9042)

* Restauration : DependencyGraphSpec. Load (...) n’a pas besoin de JObject- [#9040](https://github.com/NuGet/Home/issues/9040)

* Restauration : chaînes volumineuses créées sur le tas d’objets volumineux (LOH)- [#9031](https://github.com/NuGet/Home/issues/9031)

* Une nuget.exe personnalisée sur un mono plus récent peut s’interrompre en raison du programme de résolution du SDK MSBuild- [8848](https://github.com/NuGet/Home/issues/8848)

* la restauration échoue quand nuget.dgspec.jsest « utilisé par un autre processus »- [8692](https://github.com/NuGet/Home/issues/8692)

**DCR**

* La logique de _GetRestoreProjectStyle doit se trouver dans une tâche [#8804](https://github.com/NuGet/Home/issues/8804)

* Ajoutez les informations d’obsolescence par défaut sous l’onglet installé- [#8541](https://github.com/NuGet/Home/issues/8541)

**[Liste de tous les problèmes résolus dans cette version-5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
