---
title: Notes de publication NuGet 1.4 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notes de version de NuGet 1.4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
keywords: Notes de publication NuGet 1.4, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1229cd7fddb826902478b69cfdbc16a8ed192b64
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-14-release-notes"></a>Notes de publication NuGet 1.4

[Notes de publication NuGet 1.3](../release-notes/nuget-1.3.md) | [NuGet 1.5 Notes de publication](../release-notes/nuget-1.5.md)

NuGet 1.4 a été publiée le 17 juin 2011.

## <a name="features"></a>Fonctionnalités

### <a name="update-package-improvements"></a>Améliorations du Package de mise à jour
NuGet 1.4 introduit de nombreuses améliorations apportées à la commande de Package de mise à jour, ce qui la rend plus facile à maintenir des packages à la même version sur plusieurs projets dans une solution. Par exemple, lors de la mise à niveau d’un package vers la version la plus récente, il est très courant de tous les projets avec ce package installé pour être mis à jour vers la même verision.

Le `Update-Package` commande maintenant facilite :

#### <a name="update-all-packages-in-a-single-project"></a>Mettre à jour tous les packages dans un seul projet

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Mettre à jour un package dans tous les projets

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Mettre à jour tous les packages dans tous les projets

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Effectuer une mise à jour « sécurisée » sur tous les packages
Le `-Safe` indicateur contraint les mises à niveau uniquement les versions avec le même composant de version mineure et majeure. Par exemple, si la version 1.0.0 d’un package est installée, et les versions 1.0.1, 1.0.2 et 1.1 sont disponibles dans le flux, le `-Safe` indicateur met à jour le package vers la version 1.0.2. La mise à niveau sans le `-Safe` indicateur serait de mettre à niveau le package vers la dernière version, 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Gestion des Packages au niveau de la Solution
NuGet 1.4, avant l’installation d’un package en plusieurs projets a été lourde à l’aide de la boîte de dialogue. Il nécessaire de lancer la boîte de dialogue une fois par projet.

NuGet 1.4 ajoute la prise en charge pour l’installation/désinstallation/mise à jour des packages dans plusieurs projets en même temps. Il vous suffit de lancer l’en cliquant avec le bouton droit sur la Solution et en sélectionnant le **gérer les Packages NuGet** option de menu.

![Boîte de dialogue Manage NuGet Packages au niveau solution](./media/manage-nuget-packages-solution-dialog.png)

Notez que le nom de la solution s’affiche dans la barre de titre de la boîte de dialogue, pas le nom d’un projet.
Opérations de package fournissent désormais une liste de cases à cocher à la liste de l’opération doit s’appliquer à des projets.

![Gérer la sélection de projet les Packages NuGet](./media/manage-nuget-packages-project-selection.png)

Pour plus d’informations, consultez la rubrique sur [la gestion des Packages pour la Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>En limitant met à niveau autorisé de Versions
Par défaut, lorsque vous exécutez le `Update-Package` commande sur un package (ou mise à jour le package à l’aide de la boîte de dialogue), il sera mis à jour vers la dernière version dans le flux. Avec la nouvelle prise en charge de tous les packages de mise à jour, il peut arriver dans lequel vous souhaitez verrouiller un package à une plage de versions spécifiques. Par exemple, vous savez peut-être à l’avance que votre application fonctionne uniquement avec 2.* de version d’un package, mais pas 3.0 et versions ultérieures. Afin d’éviter l’accidentellement mise à jour le package à 3, NuGet 1.4 ajoute la prise en charge de la plage de versions des packages peuvent être mis à niveau en modifiant de main en limitant le `packages.config` de fichiers à l’aide de la nouvelle `allowedVersions` attribut.

Par exemple, l’exemple suivant montre comment verrouiller le `SomePackage` la version de package de plage (exclusif) 2.0 3.0.
Le `allowedVersions` attribut accepte les valeurs à l’aide de la [format de plage de version](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Notez que dans 1.4, verrouillage d’un lot à une plage de version spécifique doit être modifié manuellement. Dans la version 1.5 de NuGet nous prévoyons d’ajouter la prise en charge pour la sélection élective de cette plage via la `Install-Package` commande.

### <a name="package-visualizer"></a>Visualiseur de package
Le visualiseur de package nouvelle, lancé via le **outils** -> **Gestionnaire de Package de bibliothèque** -> **Package visualiseur** option de menu, vous permet de facilement visualiser tous les projets et leurs dépendances de package dans une solution.

_**Remarque importante :** cette fonctionnalité tire parti de la prise en charge le langage DGML dans Visual Studio. Création de la visualisation est uniquement pris en charge dans Visual Studio Ultimate. Affichage d’un diagramme DGML est uniquement pris en charge dans Visual Studio Premium ou supérieur._

![Visualiseur de package](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Vérification de mise à jour automatique de la boîte de dialogue NuGet
Certaines versions de NuGet introduisent de nouvelles fonctionnalités exprimées par les `.nuspec` fichier qui ne sont pas compris par les versions antérieures de la boîte de dialogue NuGet.
Par exemple, l’introduction de NuGet 1.4 pour [spécifiant des assemblys de framework](../release-notes/nuget-1.2.md#framework-assembly-refs).
Pour cette raison, il est important d’utiliser la version la plus récente de NuGet pour vous assurer que vous pouvez tirer parti des fonctionnalités plus récentes des packages.
Pour mettre à jour NuGet plus visible, la boîte de dialogue NuGet contient la logique pour mettre en surbrillance quand une version plus récente est disponible.

_**Remarque**: la vérification est effectuée uniquement si le **Online** onglet a été sélectionné dans la session active._

![Gérer la boîte de dialogue de Packages NuGet avec la nouvelle version disponible](./media/manage-nuget-packages-update-notification.png)

Pour désactiver la vérification automatique des mises à jour, accédez à la boîte de dialogue Paramètres NuGet et décochez la case **rechercher automatiquement les mises à jour**.

![Paramètres de NuGet](./media/nuget-settings.png)

Cette fonctionnalité a été ajoutée dans NuGet 1.3, mais ne serait pas visible, bien entendu, jusqu'à ce que la mise à jour 1.3, telles que NuGet 1.4, a été effectuée disponible.

### <a name="package-manager-dialog-improvements"></a>Améliorations de la boîte de dialogue Gestionnaire de package
* **Les noms des menus améliorée**: options de Menu pour ouvrir la boîte de dialogue ont été renommées pour plus de clarté. L’option de menu est désormais **gérer les Packages NuGet**.
* **Volet d’informations affiche la dernière date de mise à jour**: NuGet de la boîte de dialogue affiche la date de la dernière mise à jour dans le volet de détails pour un package lorsque le **Online** ou **met à jour** onglet est sélectionné.
* **Liste des balises affichées**: Nuget de la boîte de dialogue affiche des balises.

### <a name="powershell-improvements"></a>Améliorations de PowerShell
* **Signature des scripts PowerShell**: NuGet inclut des scripts Powershell signés l’activation de l’utilisation dans les environnements plus restrictifs.
* **Prise en charge de solliciter**: la Console du Gestionnaire de Package prend désormais en charge la demande le `$host.ui.Prompt` et `$host.ui.PromptForChoice` commandes.
* **Les noms de Source de package**: le nom d’une source de package est pris en charge lorsque vous spécifiez une source de package à l’aide la `-Source` indicateur.

### <a name="nugetexe-command-line-improvements"></a>améliorations de la ligne de commande NuGet.exe
* **Des commandes personnalisées NuGet**: nuget.exe est extensible via des commandes personnalisées à l’aide de MEF.
* **Plus simple le flux de travail pour la création de packages de symboles**: le `-Symbols` indicateur peut être appliqué à une structure de dossiers basé sur une convention normaux création d’un package de symboles en incluant uniquement de la source et `.pdb` fichiers au sein du dossier.
* **Spécification de plusieurs Sources**: le `NuGet install` commande prend en charge la spécification de plusieurs sources à l’aide de points-virgules comme un séparateur ou en spécifiant `-Source` plusieurs fois.
* **Prend en charge de l’authentification proxy**: NuGet 1.4 ajoute la prise en charge de la demande d’informations d’identification de l’utilisateur lors de l’utilisation de NuGet derrière un proxy qui nécessite une authentification.
* **mettre à jour les modifications avec rupture de NuGet.exe**: le `-Self` indicateur est désormais requis pour nuget.exe mettre à jour automatiquement. `nuget.exe Update` prend désormais en un chemin d’accès à la `packages.config` de fichiers et tente de mettre à jour les packages. Notez que cette mise à jour est limité, il ne sera pas : ** mettre à jour, ajouter, supprimer du contenu dans le fichier projet.
** D’exécution des scripts Powershell dans le package.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Prise en charge du serveur NuGet pour les Packages de distribution à l’aide de nuget.exe
NuGet inclut une méthode simple pour héberger un [sur le web léger référentiel NuGet](../hosting-packages/nuget-server.md) via la `NuGet.Server` package NuGet. Avec NuGet 1.4, le serveur léger prend en charge l’envoi et la suppression de packages à l’aide de nuget.exe.
La dernière version de `NuGet.Server` ajoute un nouveau `appSetting`, nommé `apiKey`. Lorsque la clé est omise ou est vide, en exécutant un push de packages pour le flux est désactivé. Affecter l’apiKey une valeur (dans l’idéal, un mot de passe fort) permet de push des packages à l’aide de nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Prise en charge pour l’édition de Mango outils Windows Phone
NuGet est maintenant pris en charge dans la version release candidate des outils de Windows Phone pour Mango.
Actuellement, les outils de Windows Phone n’a pas de prise en charge pour le Gestionnaire de l’Extension Visual Studio Installer NuGet pour les outils Windows Phone, vous devrez peut-être télécharger et exécuter l’extension VSIX manuellement.

Pour désinstaller les outils de NuGet pour Windows Phone, exécutez la commande suivante.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1.4 comportait 88 fixe des éléments de travail. 71 d'entre eux ont été marquées en tant que bogues.

Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.4, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correctifs de bogues à noter :

* [Problème 603](http://nuget.codeplex.com/workitem/603): dépendances de Package dans différents espaces de stockage résout correctement lors de la spécification d’une source de package spécifique.
* [Problème 1036](http://nuget.codeplex.com/workitem/1036): ajout de `NuGet Pack SomeProject.csproj` à l’événement après génération n’est plus provoque une boucle infinie.
* [Problème 961](http://nuget.codeplex.com/workitem/961): `-Source` indicateur prend en charge les chemins d’accès relatifs.

## <a name="nuget-14-update"></a>Mise à jour de NuGet 1.4
Peu après la publication de NuGet 1.4, nous avons trouvé quelques problèmes qui ont été important de le corriger.
Le numéro de version spécifique de cette mise à jour 1.4 est 1.4.20615.9020.

### <a name="bug-fixes"></a>Correctifs de bogues
* [Problème 1220](http://nuget.codeplex.com/workitem/1220): Package de mise à jour n’exécute pas `install.ps1` / `uninstall.ps1` dans tous les projets lorsqu’il existe plusieurs projets
* [Problème 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Console bloqués sur W2K3/XP (lorsque Powershell 2 n’est pas installé)
