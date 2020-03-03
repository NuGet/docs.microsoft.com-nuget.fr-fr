---
title: Notes de publication de NuGet 1,4
description: Notes de publication de NuGet 1,4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b31c02b9251d6d45d952fdf8b111493495d57ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230705"
---
# <a name="nuget-14-release-notes"></a>Notes de publication de NuGet 1,4

[Notes de publication de nuget 1,3](../release-notes/nuget-1.3.md) | [notes de publication de NuGet 1,5](../release-notes/nuget-1.5.md)

NuGet 1,4 a été publié le 17 juin 2011.

## <a name="features"></a>Fonctionnalités

### <a name="update-package-improvements"></a>Améliorations des packages de mise à jour
NuGet 1,4 introduit de nombreuses améliorations apportées à la commande Update-Package, ce qui simplifie la conservation des packages à la même version sur plusieurs projets d’une solution. Par exemple, lors de la mise à niveau d’un package vers la version la plus récente, il est très courant de faire en sorte que tous les projets sur lesquels ce package est installé soient mis à jour vers le même verision.

La commande `Update-Package` facilite désormais les opérations suivantes :

#### <a name="update-all-packages-in-a-single-project"></a>Mettre à jour tous les packages dans un projet unique

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Mettre à jour un package dans tous les projets

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Mettre à jour tous les packages dans tous les projets

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Effectuer une mise à jour « sécurisée » sur tous les packages
L’indicateur `-Safe` limite les mises à niveau à des versions avec les mêmes composants de version principale et mineure. Par exemple, si la version 1.0.0 d’un package est installée et que les versions 1.0.1, 1.0.2 et 1,1 sont disponibles dans le flux, l’indicateur `-Safe` met à jour le package vers 1.0.2. La mise à niveau sans l’indicateur `-Safe` mettre à niveau le package vers la version la plus récente, 1,1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Gestion des packages au niveau de la solution
Avant NuGet 1,4, l’installation d’un package dans plusieurs projets était fastidieuse à l’aide de la boîte de dialogue. Elle nécessitait le lancement de la boîte de dialogue une seule fois par projet.

NuGet 1,4 ajoute la prise en charge pour l’installation et la désinstallation/la mise à jour de packages dans plusieurs projets en même temps. Lancez simplement le en cliquant avec le bouton droit sur la solution et en sélectionnant l’option de menu **gérer les packages NuGet** .

![Boîte de dialogue gérer les packages NuGet au niveau de la solution](./media/manage-nuget-packages-solution-dialog.png)

Notez que dans la barre de titre de la boîte de dialogue, le nom de la solution s’affiche, et non le nom d’un projet.
Les opérations de package fournissent désormais une liste de cases à cocher avec la liste des projets auxquels l’opération doit s’appliquer.

![Gérer la sélection de projets de packages NuGet](./media/manage-nuget-packages-project-selection.png)

Pour plus d’informations, consultez la rubrique relative à la [gestion des packages pour la solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Restriction des mises à niveau vers les versions autorisées
Par défaut, lors de l’exécution de la commande `Update-Package` sur un package (ou la mise à jour du package à l’aide de la boîte de dialogue), elle est mise à jour vers la version la plus récente dans le flux. Avec la nouvelle prise en charge de la mise à jour de tous les packages, il peut arriver que vous souhaitiez verrouiller un package à une plage de versions spécifique. Par exemple, vous savez peut-être à l’avance que votre application ne fonctionnera qu’avec la version 2. * d’un package, mais pas avec 3,0 et versions ultérieures. Pour empêcher la mise à jour accidentelle du package vers 3, NuGet 1,4 ajoute la prise en charge de la limitation de la plage de versions vers laquelle les packages peuvent être mis à niveau pour modifier manuellement le fichier `packages.config` à l’aide du nouvel attribut `allowedVersions`.

Par exemple, l’exemple suivant montre comment verrouiller le package `SomePackage` la plage de versions 2,0-3,0 (exclusive).
L’attribut `allowedVersions` accepte des valeurs à l’aide du [format de plage de versions](../concepts/package-versioning.md#version-ranges).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Notez que dans 1,4, le verrouillage d’un package à une plage de versions spécifique doit être modifié manuellement. Dans NuGet 1,5, nous prévoyons d’ajouter la prise en charge de la mise en place de cette plage via la commande `Install-Package`.

### <a name="package-visualizer"></a>Visualiseur de package
Le nouveau visualiseur de package, lancé via l’option de menu **outils** -> **bibliothèque gestionnaire de package** -> **visualiseur de package** , vous permet de visualiser facilement tous les projets et leurs dépendances de package au sein d’une solution.

_**Remarque importante :** Cette fonctionnalité tire parti de la prise en charge de DGML dans Visual Studio. La création de la visualisation est uniquement prise en charge dans Visual Studio Ultimate. L’affichage d’un diagramme DGML est pris en charge uniquement dans Visual Studio Premium ou une version ultérieure._

![Visualiseur de package](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Vérification de la mise à jour automatique pour la boîte de dialogue NuGet
Certaines versions de NuGet introduisent de nouvelles fonctionnalités exprimées par le biais du fichier `.nuspec` qui ne sont pas comprises par les versions antérieures de la boîte de dialogue NuGet.
Un exemple est l’introduction de NuGet 1,4 pour la [spécification d’assemblys Framework](../release-notes/nuget-1.2.md#framework-assembly-refs).
Pour cette raison, il est important d’utiliser la dernière version de NuGet pour vous assurer que vous pouvez utiliser les packages en tirant parti des fonctionnalités les plus récentes.
Pour rendre les mises à jour de NuGet plus visibles, la boîte de dialogue NuGet contient une logique pour mettre en évidence quand une version plus récente est disponible.

_**Remarque**: la vérification est effectuée uniquement si l’onglet **en ligne** a été sélectionné dans la session active._

![Boîte de dialogue gérer les packages NuGet avec une nouvelle version disponible](./media/manage-nuget-packages-update-notification.png)

Pour désactiver la vérification automatique des mises à jour, accédez à la boîte de dialogue Paramètres NuGet et décochez la **case Rechercher automatiquement les mises à jour**.

![Paramètres NuGet](./media/nuget-settings.png)

Cette fonctionnalité a été ajoutée dans NuGet 1,3, mais elle n’est pas visible, bien sûr, jusqu’à ce qu’une mise à jour de 1,3, telle que NuGet 1,4, soit disponible.

### <a name="package-manager-dialog-improvements"></a>Améliorations de la boîte de dialogue du gestionnaire de package
* **Amélioration des noms de menu**: les options de menu pour lancer la boîte de dialogue ont été renommées pour plus de clarté. L’option de menu gère désormais les **packages NuGet**.
* Le **volet d’informations affiche la dernière date de mise à jour**: la boîte de dialogue NuGet affiche la date de la dernière mise à jour dans le volet d’informations d’un package lorsque l’onglet **en ligne** ou **mises à jour** est sélectionné.
* **Liste des balises affichées**: la boîte de dialogue NuGet affiche des balises.

### <a name="powershell-improvements"></a>Améliorations de PowerShell
* **Scripts PowerShell signés**: NuGet comprend des scripts PowerShell signés permettant l’utilisation dans des environnements plus restrictifs.
* **Demande de support**: la console du gestionnaire de package prend désormais en charge l’invite via les commandes `$host.ui.Prompt` et `$host.ui.PromptForChoice`.
* **Noms des sources du package**: le fait de fournir le nom d’une source de package est pris en charge lors de la spécification d’une source de package à l’aide de l’indicateur `-Source`.

### <a name="nugetexe-command-line-improvements"></a>améliorations de la ligne de commande NuGet. exe
* **Commandes personnalisées NuGet**: NuGet. exe est extensible par le biais de commandes personnalisées à l’aide de MEF.
* **Simplification du flux de travail pour la création de packages de symboles**: l’indicateur `-Symbols` peut être appliqué à une structure de dossiers basée sur une convention normale créant un package de symboles en incluant uniquement les fichiers source et `.pdb` dans le dossier.
* **Spécification de plusieurs sources**: la commande `NuGet install` prend en charge la spécification de plusieurs sources en utilisant des points-virgules comme délimiteurs ou en spécifiant des `-Source` plusieurs fois.
* **Prise en charge de l’authentification proxy**: NuGet 1,4 ajoute la prise en charge pour demander les informations d’identification de l’utilisateur lors de l’utilisation de NuGet derrière un proxy qui requiert une authentification.
* **modification avec rupture de la mise à jour de NuGet. exe**: l’indicateur `-Self` est désormais requis pour que NuGet. exe se met à jour lui-même. `nuget.exe Update` prend maintenant le chemin d’accès au fichier `packages.config` et tente de mettre à jour les packages. Notez que cette mise à jour est limitée en ce qu’elle ne peut pas : * * mettre à jour, ajouter et supprimer du contenu dans le fichier projet.
* * Exécutez les scripts PowerShell dans le package.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Prise en charge du serveur NuGet pour l’envoi de packages Push à l’aide de NuGet. exe
NuGet comprend un moyen simple d’héberger un [référentiel NuGet basé sur le Web](../hosting-packages/nuget-server.md) via le package NuGet `NuGet.Server`. Avec NuGet 1,4, le serveur léger prend en charge l’envoi et la suppression de packages à l’aide de NuGet. exe.
La dernière version de `NuGet.Server` ajoute un nouveau `appSetting`, nommé `apiKey`. Lorsque la clé est omise ou laissée vide, le push des packages vers le flux est désactivé. La définition de apiKey sur une valeur (idéalement un mot de passe fort) permet de pousser des packages à l’aide de NuGet. exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Prise en charge de l’édition de Windows Phone Tools Mango
NuGet est désormais pris en charge dans la version Release candidate de Windows Phone Tools pour Mango.
Actuellement, Windows Phone Tools ne prend pas en charge le gestionnaire d’extensions de Visual Studio. ainsi, pour installer NuGet pour les outils de Windows Phone, vous devrez peut-être télécharger et exécuter le VSIX manuellement.

Pour désinstaller NuGet pour les outils Windows Phone, exécutez la commande suivante.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1,4 avait un total de 88 éléments de travail corrigés. 71 de ceux-ci ont été marqués comme des bogues.

Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 1,4, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Les correctifs de bogues méritent d’être notés :

* [Problème 603](http://nuget.codeplex.com/workitem/603): les dépendances de package dans différents référentiels sont résolues correctement lors de la spécification d’une source de package spécifique.
* [Problème 1036](http://nuget.codeplex.com/workitem/1036): l’ajout d' `NuGet Pack SomeProject.csproj` à l’événement après génération n’entraîne plus une boucle infinie.
* [Problème 961](http://nuget.codeplex.com/workitem/961): l’indicateur `-Source` prend en charge les chemins d’accès relatifs.

## <a name="nuget-14-update"></a>Mise à jour NuGet 1,4
Peu après la publication de NuGet 1,4, nous avons trouvé quelques problèmes importants à résoudre.
Le numéro de version spécifique de cette mise à jour de 1,4 est 1.4.20615.9020.

### <a name="bug-fixes"></a>Correctifs de bogues
* [Problème 1220](http://nuget.codeplex.com/workitem/1220): Update-Package ne s’exécute pas `install.ps1`/`uninstall.ps1` dans tous les projets lorsqu’il y a plusieurs projets
* [Problème 1156](http://nuget.codeplex.com/workitem/1156): le gestionnaire de package est bloqué sur le SP2/XP (lorsque PowerShell 2 n’est pas installé)
