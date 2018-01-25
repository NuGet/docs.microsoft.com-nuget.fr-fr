---
title: Notes de publication NuGet 1.4 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de version de NuGet 1.4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 1.4, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a69f4f5c7172817d711fa5e995cf6db3875c4810
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="4c297-104">Notes de publication NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="4c297-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="4c297-105">[Notes de publication NuGet 1.3](../release-notes/nuget-1.3.md) | [NuGet 1.5 Notes de publication](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="4c297-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="4c297-106">NuGet 1.4 a été publiée le 17 juin 2011.</span><span class="sxs-lookup"><span data-stu-id="4c297-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="4c297-107">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="4c297-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="4c297-108">Améliorations du Package de mise à jour</span><span class="sxs-lookup"><span data-stu-id="4c297-108">Update-Package improvements</span></span>
<span data-ttu-id="4c297-109">NuGet 1.4 introduit de nombreuses améliorations apportées à la commande de Package de mise à jour, ce qui la rend plus facile à maintenir des packages à la même version sur plusieurs projets dans une solution.</span><span class="sxs-lookup"><span data-stu-id="4c297-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="4c297-110">Par exemple, lors de la mise à niveau d’un package vers la version la plus récente, il est très courant de tous les projets avec ce package installé pour être mis à jour vers la même verision.</span><span class="sxs-lookup"><span data-stu-id="4c297-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="4c297-111">Le `Update-Package` commande maintenant facilite :</span><span class="sxs-lookup"><span data-stu-id="4c297-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="4c297-112">Mettre à jour tous les packages dans un seul projet</span><span class="sxs-lookup"><span data-stu-id="4c297-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="4c297-113">Mettre à jour un package dans tous les projets</span><span class="sxs-lookup"><span data-stu-id="4c297-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="4c297-114">Mettre à jour tous les packages dans tous les projets</span><span class="sxs-lookup"><span data-stu-id="4c297-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="4c297-115">Effectuer une mise à jour « sécurisée » sur tous les packages</span><span class="sxs-lookup"><span data-stu-id="4c297-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="4c297-116">Le `-Safe` indicateur contraint les mises à niveau uniquement les versions avec le même composant de version mineure et majeure.</span><span class="sxs-lookup"><span data-stu-id="4c297-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="4c297-117">Par exemple, si la version 1.0.0 d’un package est installée, et les versions 1.0.1, 1.0.2 et 1.1 sont disponibles dans le flux, le `-Safe` indicateur met à jour le package vers la version 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="4c297-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="4c297-118">La mise à niveau sans le `-Safe` indicateur serait de mettre à niveau le package vers la dernière version, 1.1.</span><span class="sxs-lookup"><span data-stu-id="4c297-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="4c297-119">Gestion des Packages au niveau de la Solution</span><span class="sxs-lookup"><span data-stu-id="4c297-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="4c297-120">NuGet 1.4, avant l’installation d’un package en plusieurs projets a été lourde à l’aide de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4c297-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="4c297-121">Il nécessaire de lancer la boîte de dialogue une fois par projet.</span><span class="sxs-lookup"><span data-stu-id="4c297-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="4c297-122">NuGet 1.4 ajoute la prise en charge pour l’installation/désinstallation/mise à jour des packages dans plusieurs projets en même temps.</span><span class="sxs-lookup"><span data-stu-id="4c297-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="4c297-123">Il vous suffit de lancer l’en cliquant avec le bouton droit sur la Solution et en sélectionnant le **gérer les Packages NuGet** option de menu.</span><span class="sxs-lookup"><span data-stu-id="4c297-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Boîte de dialogue Manage NuGet Packages au niveau solution](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="4c297-125">Notez que le nom de la solution s’affiche dans la barre de titre de la boîte de dialogue, pas le nom d’un projet.</span><span class="sxs-lookup"><span data-stu-id="4c297-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="4c297-126">Opérations de package fournissent désormais une liste de cases à cocher à la liste de l’opération doit s’appliquer à des projets.</span><span class="sxs-lookup"><span data-stu-id="4c297-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Gérer la sélection de projet les Packages NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="4c297-128">Pour plus d’informations, consultez la rubrique sur [la gestion des Packages pour la Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="4c297-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="4c297-129">En limitant met à niveau autorisé de Versions</span><span class="sxs-lookup"><span data-stu-id="4c297-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="4c297-130">Par défaut, lorsque vous exécutez le `Update-Package` commande sur un package (ou mise à jour le package à l’aide de la boîte de dialogue), il sera mis à jour vers la dernière version dans le flux.</span><span class="sxs-lookup"><span data-stu-id="4c297-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="4c297-131">Avec la nouvelle prise en charge de tous les packages de mise à jour, il peut arriver dans lequel vous souhaitez verrouiller un package à une plage de versions spécifiques.</span><span class="sxs-lookup"><span data-stu-id="4c297-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="4c297-132">Par exemple, vous savez peut-être à l’avance que votre application fonctionne uniquement avec 2.\* de version d’un package, mais pas 3.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="4c297-132">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="4c297-133">Afin d’éviter l’accidentellement mise à jour le package à 3, NuGet 1.4 ajoute la prise en charge de la plage de versions des packages peuvent être mis à niveau en modifiant de main en limitant le `packages.config` de fichiers à l’aide de la nouvelle `allowedVersions` attribut.</span><span class="sxs-lookup"><span data-stu-id="4c297-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="4c297-134">Par exemple, l’exemple suivant montre comment verrouiller le `SomePackage` la version de package de plage (exclusif) 2.0 3.0.</span><span class="sxs-lookup"><span data-stu-id="4c297-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="4c297-135">Le `allowedVersions` attribut accepte les valeurs à l’aide de la [format de plage de version](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="4c297-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="4c297-136">Notez que dans 1.4, verrouillage d’un lot à une plage de version spécifique doit être modifié manuellement.</span><span class="sxs-lookup"><span data-stu-id="4c297-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="4c297-137">Dans la version 1.5 de NuGet nous prévoyons d’ajouter la prise en charge pour la sélection élective de cette plage via la `Install-Package` commande.</span><span class="sxs-lookup"><span data-stu-id="4c297-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="4c297-138">Visualiseur de package</span><span class="sxs-lookup"><span data-stu-id="4c297-138">Package Visualizer</span></span>
<span data-ttu-id="4c297-139">Le visualiseur de package nouvelle, lancé via le **outils** -> **Gestionnaire de Package de bibliothèque** -> **Package visualiseur** option de menu, vous permet de facilement visualiser tous les projets et leurs dépendances de package dans une solution.</span><span class="sxs-lookup"><span data-stu-id="4c297-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="4c297-140">_**Remarque importante :** cette fonctionnalité tire parti de la prise en charge le langage DGML dans Visual Studio. Création de la visualisation est uniquement pris en charge dans Visual Studio Ultimate. Affichage d’un diagramme DGML est uniquement pris en charge dans Visual Studio Premium ou supérieur._</span><span class="sxs-lookup"><span data-stu-id="4c297-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Visualiseur de package](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="4c297-142">Vérification de mise à jour automatique de la boîte de dialogue NuGet</span><span class="sxs-lookup"><span data-stu-id="4c297-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="4c297-143">Certaines versions de NuGet introduisent de nouvelles fonctionnalités exprimées par les `.nuspec` fichier qui ne sont pas compris par les versions antérieures de la boîte de dialogue NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c297-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="4c297-144">Par exemple, l’introduction de NuGet 1.4 pour [spécifiant des assemblys de framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="4c297-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="4c297-145">Pour cette raison, il est important d’utiliser la version la plus récente de NuGet pour vous assurer que vous pouvez tirer parti des fonctionnalités plus récentes des packages.</span><span class="sxs-lookup"><span data-stu-id="4c297-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="4c297-146">Pour mettre à jour NuGet plus visible, la boîte de dialogue NuGet contient la logique pour mettre en surbrillance quand une version plus récente est disponible.</span><span class="sxs-lookup"><span data-stu-id="4c297-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="4c297-147">_**Remarque**: la vérification est effectuée uniquement si le **Online** onglet a été sélectionné dans la session active._</span><span class="sxs-lookup"><span data-stu-id="4c297-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Gérer la boîte de dialogue de Packages NuGet avec la nouvelle version disponible](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="4c297-149">Pour désactiver la vérification automatique des mises à jour, accédez à la boîte de dialogue Paramètres NuGet et décochez la case **rechercher automatiquement les mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="4c297-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Paramètres de NuGet](./media/nuget-settings.png)

<span data-ttu-id="4c297-151">Cette fonctionnalité a été ajoutée dans NuGet 1.3, mais ne serait pas visible, bien entendu, jusqu'à ce que la mise à jour 1.3, telles que NuGet 1.4, a été effectuée disponible.</span><span class="sxs-lookup"><span data-stu-id="4c297-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="4c297-152">Améliorations de la boîte de dialogue Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="4c297-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="4c297-153">**Les noms des menus améliorée**: options de Menu pour ouvrir la boîte de dialogue ont été renommées pour plus de clarté.</span><span class="sxs-lookup"><span data-stu-id="4c297-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="4c297-154">L’option de menu est désormais **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4c297-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="4c297-155">**Volet d’informations affiche la dernière date de mise à jour**: NuGet de la boîte de dialogue affiche la date de la dernière mise à jour dans le volet de détails pour un package lorsque le **Online** ou **met à jour** onglet est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="4c297-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="4c297-156">**Liste des balises affichées**: Nuget de la boîte de dialogue affiche des balises.</span><span class="sxs-lookup"><span data-stu-id="4c297-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="4c297-157">Améliorations de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c297-157">Powershell Improvements</span></span>
* <span data-ttu-id="4c297-158">**Signature des scripts PowerShell**: NuGet inclut des scripts Powershell signés l’activation de l’utilisation dans les environnements plus restrictifs.</span><span class="sxs-lookup"><span data-stu-id="4c297-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="4c297-159">**Prise en charge de solliciter**: la Console du Gestionnaire de Package prend désormais en charge la demande le `$host.ui.Prompt` et `$host.ui.PromptForChoice` commandes.</span><span class="sxs-lookup"><span data-stu-id="4c297-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="4c297-160">**Les noms de Source de package**: le nom d’une source de package est pris en charge lorsque vous spécifiez une source de package à l’aide la `-Source` indicateur.</span><span class="sxs-lookup"><span data-stu-id="4c297-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="4c297-161">améliorations de la ligne de commande NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="4c297-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="4c297-162">**Des commandes personnalisées NuGet**: nuget.exe est extensible via des commandes personnalisées à l’aide de MEF.</span><span class="sxs-lookup"><span data-stu-id="4c297-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="4c297-163">**Plus simple le flux de travail pour la création de packages de symboles**: le `-Symbols` indicateur peut être appliqué à une structure de dossiers basé sur une convention normaux création d’un package de symboles en incluant uniquement de la source et `.pdb` fichiers au sein du dossier.</span><span class="sxs-lookup"><span data-stu-id="4c297-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="4c297-164">**Spécification de plusieurs Sources**: le `NuGet install` commande prend en charge la spécification de plusieurs sources à l’aide de points-virgules comme un séparateur ou en spécifiant `-Source` plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="4c297-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="4c297-165">**Prend en charge de l’authentification proxy**: NuGet 1.4 ajoute la prise en charge de la demande d’informations d’identification de l’utilisateur lors de l’utilisation de NuGet derrière un proxy qui nécessite une authentification.</span><span class="sxs-lookup"><span data-stu-id="4c297-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="4c297-166">**mettre à jour les modifications avec rupture de NuGet.exe**: le `-Self` indicateur est désormais requis pour nuget.exe mettre à jour automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4c297-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="4c297-167">`nuget.exe Update`prend désormais en un chemin d’accès à la `packages.config` de fichiers et tente de mettre à jour les packages.</span><span class="sxs-lookup"><span data-stu-id="4c297-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="4c297-168">Notez que cette mise à jour est limité, il ne sera pas : ** mettre à jour, ajouter, supprimer du contenu dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="4c297-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="4c297-169">** D’exécution des scripts Powershell dans le package.</span><span class="sxs-lookup"><span data-stu-id="4c297-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="4c297-170">Prise en charge du serveur NuGet pour les Packages de distribution à l’aide de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4c297-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="4c297-171">NuGet inclut une méthode simple pour héberger un [sur le web léger référentiel NuGet](../hosting-packages/NuGet-Server.md) via la `NuGet.Server` package NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c297-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/NuGet-Server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="4c297-172">Avec NuGet 1.4, le serveur léger prend en charge l’envoi et la suppression de packages à l’aide de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="4c297-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="4c297-173">La dernière version de `NuGet.Server` ajoute un nouveau `appSetting`, nommé `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="4c297-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="4c297-174">Lorsque la clé est omise ou est vide, en exécutant un push de packages pour le flux est désactivé.</span><span class="sxs-lookup"><span data-stu-id="4c297-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="4c297-175">Affecter l’apiKey une valeur (dans l’idéal, un mot de passe fort) permet de push des packages à l’aide de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="4c297-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="4c297-176">Prise en charge pour l’édition de Mango outils Windows Phone</span><span class="sxs-lookup"><span data-stu-id="4c297-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="4c297-177">NuGet est maintenant pris en charge dans la version release candidate des outils de Windows Phone pour Mango.</span><span class="sxs-lookup"><span data-stu-id="4c297-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="4c297-178">Actuellement, les outils de Windows Phone n’a pas de prise en charge pour le Gestionnaire de l’Extension Visual Studio Installer NuGet pour les outils Windows Phone, vous devrez peut-être télécharger et exécuter l’extension VSIX manuellement.</span><span class="sxs-lookup"><span data-stu-id="4c297-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="4c297-179">Pour désinstaller les outils de NuGet pour Windows Phone, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="4c297-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="4c297-180">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="4c297-180">Bug Fixes</span></span>
<span data-ttu-id="4c297-181">NuGet 1.4 comportait 88 fixe des éléments de travail.</span><span class="sxs-lookup"><span data-stu-id="4c297-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="4c297-182">71 d'entre eux ont été marquées en tant que bogues.</span><span class="sxs-lookup"><span data-stu-id="4c297-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="4c297-183">Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.4, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="4c297-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="4c297-184">Correctifs de bogues à noter :</span><span class="sxs-lookup"><span data-stu-id="4c297-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="4c297-185">[Problème 603](http://nuget.codeplex.com/workitem/603): dépendances de Package dans différents espaces de stockage résout correctement lors de la spécification d’une source de package spécifique.</span><span class="sxs-lookup"><span data-stu-id="4c297-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="4c297-186">[Problème 1036](http://nuget.codeplex.com/workitem/1036): ajout de `NuGet Pack SomeProject.csproj` à l’événement après génération n’est plus provoque une boucle infinie.</span><span class="sxs-lookup"><span data-stu-id="4c297-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="4c297-187">[Problème 961](http://nuget.codeplex.com/workitem/961): `-Source` indicateur prend en charge les chemins d’accès relatifs.</span><span class="sxs-lookup"><span data-stu-id="4c297-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="4c297-188">Mise à jour de NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="4c297-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="4c297-189">Peu après la publication de NuGet 1.4, nous avons trouvé quelques problèmes qui ont été important de le corriger.</span><span class="sxs-lookup"><span data-stu-id="4c297-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="4c297-190">Le numéro de version spécifique de cette mise à jour 1.4 est 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="4c297-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="4c297-191">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="4c297-191">Bug Fixes</span></span>
* <span data-ttu-id="4c297-192">[Problème 1220](http://nuget.codeplex.com/workitem/1220): Package de mise à jour n’exécute pas `install.ps1` / `uninstall.ps1` dans tous les projets lorsqu’il existe plusieurs projets</span><span class="sxs-lookup"><span data-stu-id="4c297-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="4c297-193">[Problème 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Console bloqués sur W2K3/XP (lorsque Powershell 2 n’est pas installé)</span><span class="sxs-lookup"><span data-stu-id="4c297-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
