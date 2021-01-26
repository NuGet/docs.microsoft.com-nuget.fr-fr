---
title: Notes de publication de NuGet 1,4
description: Notes de publication de NuGet 1,4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777151"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="88635-103">Notes de publication de NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="88635-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="88635-104">Notes de publication de [NuGet 1,3](../release-notes/nuget-1.3.md)  |  [Notes de publication de NuGet 1,5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="88635-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="88635-105">NuGet 1,4 a été publié le 17 juin 2011.</span><span class="sxs-lookup"><span data-stu-id="88635-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="88635-106">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="88635-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="88635-107">Améliorations de la Update-Package</span><span class="sxs-lookup"><span data-stu-id="88635-107">Update-Package improvements</span></span>
<span data-ttu-id="88635-108">NuGet 1,4 introduit de nombreuses améliorations apportées à la commande Update-Package, ce qui facilite la conservation des packages à la même version sur plusieurs projets d’une solution.</span><span class="sxs-lookup"><span data-stu-id="88635-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="88635-109">Par exemple, lors de la mise à niveau d’un package vers la version la plus récente, il est très courant de faire en sorte que tous les projets sur lesquels ce package est installé soient mis à jour vers le même verision.</span><span class="sxs-lookup"><span data-stu-id="88635-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="88635-110">La `Update-Package` commande vous permet désormais d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="88635-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="88635-111">Mettre à jour tous les packages dans un projet unique</span><span class="sxs-lookup"><span data-stu-id="88635-111">Update all packages in a single project</span></span>

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="88635-112">Mettre à jour un package dans tous les projets</span><span class="sxs-lookup"><span data-stu-id="88635-112">Update a package in all projects</span></span>

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="88635-113">Mettre à jour tous les packages dans tous les projets</span><span class="sxs-lookup"><span data-stu-id="88635-113">Update all packages in all projects</span></span>

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="88635-114">Effectuer une mise à jour « sécurisée » sur tous les packages</span><span class="sxs-lookup"><span data-stu-id="88635-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="88635-115">L' `-Safe` indicateur limite les mises à niveau à des versions avec les mêmes composants de version majeure et mineure.</span><span class="sxs-lookup"><span data-stu-id="88635-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="88635-116">Par exemple, si la version 1.0.0 d’un package est installée et que les versions 1.0.1, 1.0.2 et 1,1 sont disponibles dans le flux, l' `-Safe` indicateur met à jour le package avec la valeur 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="88635-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="88635-117">Si vous effectuez une mise à niveau sans l' `-Safe` indicateur, le package est mis à niveau vers la version la plus récente, 1,1.</span><span class="sxs-lookup"><span data-stu-id="88635-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="88635-118">Gestion des packages au niveau de la solution</span><span class="sxs-lookup"><span data-stu-id="88635-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="88635-119">Avant NuGet 1,4, l’installation d’un package dans plusieurs projets était fastidieuse à l’aide de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="88635-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="88635-120">Elle nécessitait le lancement de la boîte de dialogue une seule fois par projet.</span><span class="sxs-lookup"><span data-stu-id="88635-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="88635-121">NuGet 1,4 ajoute la prise en charge pour l’installation et la désinstallation/la mise à jour de packages dans plusieurs projets en même temps.</span><span class="sxs-lookup"><span data-stu-id="88635-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="88635-122">Lancez simplement le en cliquant avec le bouton droit sur la solution et en sélectionnant l’option de menu **gérer les packages NuGet** .</span><span class="sxs-lookup"><span data-stu-id="88635-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Boîte de dialogue gérer les packages NuGet au niveau de la solution](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="88635-124">Notez que dans la barre de titre de la boîte de dialogue, le nom de la solution s’affiche, et non le nom d’un projet.</span><span class="sxs-lookup"><span data-stu-id="88635-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="88635-125">Les opérations de package fournissent désormais une liste de cases à cocher avec la liste des projets auxquels l’opération doit s’appliquer.</span><span class="sxs-lookup"><span data-stu-id="88635-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Gérer la sélection de projets de packages NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="88635-127">Pour plus d’informations, consultez la rubrique relative à la [gestion des packages pour la solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="88635-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="88635-128">Restriction des mises à niveau vers les versions autorisées</span><span class="sxs-lookup"><span data-stu-id="88635-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="88635-129">Par défaut, lorsque vous exécutez la `Update-Package` commande sur un package (ou mettez à jour le package à l’aide de la boîte de dialogue), elle est mise à jour vers la version la plus récente dans le flux.</span><span class="sxs-lookup"><span data-stu-id="88635-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="88635-130">Avec la nouvelle prise en charge de la mise à jour de tous les packages, il peut arriver que vous souhaitiez verrouiller un package à une plage de versions spécifique.</span><span class="sxs-lookup"><span data-stu-id="88635-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="88635-131">Par exemple, vous savez peut-être à l’avance que votre application ne fonctionnera qu’avec la version 2. \* d’un package, mais pas avec 3,0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="88635-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="88635-132">Afin d’éviter la mise à jour accidentelle du package vers 3, NuGet 1,4 ajoute la prise en charge de la limitation de la plage de versions vers laquelle les packages peuvent être mis à niveau, en modifiant manuellement le `packages.config` fichier à l’aide du nouvel `allowedVersions` attribut.</span><span class="sxs-lookup"><span data-stu-id="88635-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="88635-133">Par exemple, l’exemple suivant montre comment verrouiller le `SomePackage` package dans la plage de versions 2,0-3,0 (exclusive).</span><span class="sxs-lookup"><span data-stu-id="88635-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="88635-134">L' `allowedVersions` attribut accepte des valeurs à l’aide du [format de plage de versions](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="88635-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="88635-135">Notez que dans 1,4, le verrouillage d’un package à une plage de versions spécifique doit être modifié manuellement.</span><span class="sxs-lookup"><span data-stu-id="88635-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="88635-136">Dans NuGet 1,5, nous prévoyons d’ajouter la prise en charge de la mise en place de cette plage à l’aide de la `Install-Package` commande.</span><span class="sxs-lookup"><span data-stu-id="88635-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="88635-137">Visualiseur de package</span><span class="sxs-lookup"><span data-stu-id="88635-137">Package Visualizer</span></span>
<span data-ttu-id="88635-138">Le nouveau visualiseur de package, lancé via l’option de menu du visualiseur de package du gestionnaire de package d' **Outils**  ->    ->   , vous permet de visualiser facilement tous les projets et leurs dépendances de package au sein d’une solution.</span><span class="sxs-lookup"><span data-stu-id="88635-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="88635-139">_**Remarque importante :** Cette fonctionnalité tire parti de la prise en charge de DGML dans Visual Studio. La création de la visualisation est uniquement prise en charge dans Visual Studio Ultimate. L’affichage d’un diagramme DGML est pris en charge uniquement dans Visual Studio Premium ou une version ultérieure._</span><span class="sxs-lookup"><span data-stu-id="88635-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Visualiseur de package](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="88635-141">Vérification de la mise à jour automatique pour la boîte de dialogue NuGet</span><span class="sxs-lookup"><span data-stu-id="88635-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="88635-142">Certaines versions de NuGet introduisent de nouvelles fonctionnalités exprimées par le biais du `.nuspec` fichier qui ne sont pas comprises par les versions antérieures de la boîte de dialogue NuGet.</span><span class="sxs-lookup"><span data-stu-id="88635-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="88635-143">Un exemple est l’introduction de NuGet 1,4 pour la [spécification d’assemblys Framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="88635-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="88635-144">Pour cette raison, il est important d’utiliser la dernière version de NuGet pour vous assurer que vous pouvez utiliser les packages en tirant parti des fonctionnalités les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="88635-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="88635-145">Pour rendre les mises à jour de NuGet plus visibles, la boîte de dialogue NuGet contient une logique pour mettre en évidence quand une version plus récente est disponible.</span><span class="sxs-lookup"><span data-stu-id="88635-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="88635-146">_**Remarque**: la vérification est effectuée uniquement si l’onglet **en ligne** a été sélectionné dans la session active._</span><span class="sxs-lookup"><span data-stu-id="88635-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Boîte de dialogue gérer les packages NuGet avec une nouvelle version disponible](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="88635-148">Pour désactiver la vérification automatique des mises à jour, accédez à la boîte de dialogue Paramètres NuGet et décochez la **case Rechercher automatiquement les mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="88635-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Paramètres NuGet](./media/nuget-settings.png)

<span data-ttu-id="88635-150">Cette fonctionnalité a été ajoutée dans NuGet 1,3, mais elle n’est pas visible, bien sûr, jusqu’à ce qu’une mise à jour de 1,3, telle que NuGet 1,4, soit disponible.</span><span class="sxs-lookup"><span data-stu-id="88635-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="88635-151">Améliorations de la boîte de dialogue du gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="88635-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="88635-152">**Amélioration des noms de menu**: les options de menu pour lancer la boîte de dialogue ont été renommées pour plus de clarté.</span><span class="sxs-lookup"><span data-stu-id="88635-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="88635-153">L’option de menu gère désormais les **packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="88635-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="88635-154">Le **volet d’informations affiche la dernière date de mise à jour**: la boîte de dialogue NuGet affiche la date de la dernière mise à jour dans le volet d’informations d’un package lorsque l’onglet **en ligne** ou **mises à jour** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="88635-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="88635-155">**Liste des balises affichées**: la boîte de dialogue NuGet affiche des balises.</span><span class="sxs-lookup"><span data-stu-id="88635-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="88635-156">Améliorations de PowerShell</span><span class="sxs-lookup"><span data-stu-id="88635-156">Powershell Improvements</span></span>
* <span data-ttu-id="88635-157">**Scripts PowerShell signés**: NuGet comprend des scripts PowerShell signés permettant l’utilisation dans des environnements plus restrictifs.</span><span class="sxs-lookup"><span data-stu-id="88635-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="88635-158">**Demande de support**: la console du gestionnaire de package prend désormais en charge l’invite via les `$host.ui.Prompt` `$host.ui.PromptForChoice` commandes et.</span><span class="sxs-lookup"><span data-stu-id="88635-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="88635-159">**Noms des sources du package**: le fait de fournir le nom d’une source de package est pris en charge lors de la spécification d’une source de package à l’aide de l' `-Source` indicateur.</span><span class="sxs-lookup"><span data-stu-id="88635-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="88635-160">nuget.exe les améliorations de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="88635-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="88635-161">**Commandes personnalisées NuGet**: nuget.exe est extensible par le biais de commandes personnalisées à l’aide de MEF.</span><span class="sxs-lookup"><span data-stu-id="88635-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="88635-162">**Simplification du flux de travail pour la création de packages de symboles**: l' `-Symbols` indicateur peut être appliqué à une structure de dossiers basée sur une convention normale qui crée un package de symboles en incluant uniquement la source et les `.pdb` fichiers dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="88635-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="88635-163">**Spécification de plusieurs sources**: la `NuGet install` commande prend en charge la spécification de plusieurs sources à l’aide de points-virgules comme délimiteurs ou en spécifiant `-Source` plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="88635-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="88635-164">**Prise en charge de l’authentification proxy**: NuGet 1,4 ajoute la prise en charge pour demander les informations d’identification de l’utilisateur lors de l’utilisation de NuGet derrière un proxy qui requiert une authentification.</span><span class="sxs-lookup"><span data-stu-id="88635-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="88635-165">**nuget.exe modification avec rupture de la mise à jour**: l' `-Self` indicateur est désormais requis pour que nuget.exe se met à jour.</span><span class="sxs-lookup"><span data-stu-id="88635-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="88635-166">`nuget.exe Update` prend maintenant le chemin d’accès au `packages.config` fichier et tente de mettre à jour les packages.</span><span class="sxs-lookup"><span data-stu-id="88635-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="88635-167">Notez que cette mise à jour est limitée en ce qu’elle ne peut pas : \* \* mettre à jour, ajouter et supprimer du contenu dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="88635-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="88635-168">\* \* Exécutez les scripts PowerShell dans le package.</span><span class="sxs-lookup"><span data-stu-id="88635-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="88635-169">Prise en charge du serveur NuGet pour l’envoi de packages à l’aide de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="88635-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="88635-170">NuGet comprend un moyen simple d’héberger un [référentiel NuGet basé sur le Web](../hosting-packages/nuget-server.md) à l’aide du `NuGet.Server` package NuGet.</span><span class="sxs-lookup"><span data-stu-id="88635-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="88635-171">Avec NuGet 1,4, le serveur léger prend en charge l’envoi et la suppression de packages à l’aide de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="88635-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="88635-172">La dernière version de `NuGet.Server` ajoute un nouveau `appSetting` , nommé `apiKey` .</span><span class="sxs-lookup"><span data-stu-id="88635-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="88635-173">Lorsque la clé est omise ou laissée vide, le push des packages vers le flux est désactivé.</span><span class="sxs-lookup"><span data-stu-id="88635-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="88635-174">La définition de apiKey sur une valeur (idéalement un mot de passe fort) permet de pousser des packages à l’aide d' nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="88635-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="88635-175">Prise en charge de l’édition de Windows Phone Tools Mango</span><span class="sxs-lookup"><span data-stu-id="88635-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="88635-176">NuGet est désormais pris en charge dans la version Release candidate de Windows Phone Tools pour Mango.</span><span class="sxs-lookup"><span data-stu-id="88635-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="88635-177">Actuellement, Windows Phone Tools ne prend pas en charge le gestionnaire d’extensions de Visual Studio. ainsi, pour installer NuGet pour les outils de Windows Phone, vous devrez peut-être télécharger et exécuter le VSIX manuellement.</span><span class="sxs-lookup"><span data-stu-id="88635-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="88635-178">Pour désinstaller NuGet pour les outils Windows Phone, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="88635-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a><span data-ttu-id="88635-179">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="88635-179">Bug Fixes</span></span>
<span data-ttu-id="88635-180">NuGet 1,4 avait un total de 88 éléments de travail corrigés.</span><span class="sxs-lookup"><span data-stu-id="88635-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="88635-181">71 de ceux-ci ont été marqués comme des bogues.</span><span class="sxs-lookup"><span data-stu-id="88635-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="88635-182">Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 1,4, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="88635-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="88635-183">Les correctifs de bogues méritent d’être notés :</span><span class="sxs-lookup"><span data-stu-id="88635-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="88635-184">[Problème 603](http://nuget.codeplex.com/workitem/603): les dépendances de package dans différents référentiels sont résolues correctement lors de la spécification d’une source de package spécifique.</span><span class="sxs-lookup"><span data-stu-id="88635-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="88635-185">[Problème 1036](http://nuget.codeplex.com/workitem/1036): `NuGet Pack SomeProject.csproj` l’ajout à l’événement après génération n’entraîne plus une boucle infinie.</span><span class="sxs-lookup"><span data-stu-id="88635-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="88635-186">[Problème 961](http://nuget.codeplex.com/workitem/961): l' `-Source` indicateur prend en charge les chemins d’accès relatifs.</span><span class="sxs-lookup"><span data-stu-id="88635-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="88635-187">Mise à jour NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="88635-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="88635-188">Peu après la publication de NuGet 1,4, nous avons trouvé quelques problèmes importants à résoudre.</span><span class="sxs-lookup"><span data-stu-id="88635-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="88635-189">Le numéro de version spécifique de cette mise à jour de 1,4 est 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="88635-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="88635-190">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="88635-190">Bug Fixes</span></span>
* <span data-ttu-id="88635-191">[Problème 1220](http://nuget.codeplex.com/workitem/1220): Update-Package ne s’exécute pas `install.ps1` / `uninstall.ps1` dans tous les projets lorsqu’il y a plusieurs projets</span><span class="sxs-lookup"><span data-stu-id="88635-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="88635-192">[Problème 1156](http://nuget.codeplex.com/workitem/1156): le gestionnaire de package est bloqué sur le SP2/XP (lorsque PowerShell 2 n’est pas installé)</span><span class="sxs-lookup"><span data-stu-id="88635-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
