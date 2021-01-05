---
title: Résolution des problèmes de restauration de packages NuGet dans Visual Studio
description: Description des erreurs courantes liées à la restauration des packages NuGet dans Visual Studio et résolution de ces erreurs.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 9f680a714717d1bde0472f2e1266cacfd8bd4d5f
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699725"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="c9c0f-103">Résolution des erreurs de restauration des packages</span><span class="sxs-lookup"><span data-stu-id="c9c0f-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="c9c0f-104">Cet article aborde les erreurs rencontrées couramment pendant la restauration de packages, ainsi que les étapes de résolution.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="c9c0f-105">La restauration du package tente d’installer toutes les dépendances de package dans l’état correct correspondant aux références de votre fichier projet (*. csproj* ) ou de votre fichier *packages. config*.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="c9c0f-106">(Dans Visual Studio, les références s’affichent dans Explorateur de solutions sous le nœud **dépendances \ NuGet** ou **References** .) Pour suivre les étapes nécessaires à la restauration des packages, consultez [restaurer des packages](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="c9c0f-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="c9c0f-107">Si les références de package dans votre fichier projet (*.csproj*) ou votre fichier *packages.config* sont incorrectes (elles ne correspondent pas à l’état souhaité après la restauration du package), vous devez installer ou mettre à jour les packages au lieu d’utiliser la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="c9c0f-108">Si les instructions présentées ici ne fonctionnent pas, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions examiner plus attentivement votre situation.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="c9c0f-109">N’utilisez pas le contrôle « Cette page est-elle utile ? »</span><span class="sxs-lookup"><span data-stu-id="c9c0f-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="c9c0f-110">qui peut apparaître dans cette page, car celui-ci ne nous permet pas de vous contacter pour obtenir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="c9c0f-111">Solution rapide pour les utilisateurs de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9c0f-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="c9c0f-112">Si vous utilisez Visual Studio, commencez par activer la restauration des packages comme suit.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="c9c0f-113">Sinon, passez aux autres sections de cet article.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="c9c0f-114">Sélectionnez la commande de menu **Outils > Gestionnaire de package NuGet > Paramètres du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="c9c0f-115">Définissez les deux options sous **Restauration de package**.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="c9c0f-116">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-116">Select **OK**.</span></span>
1. <span data-ttu-id="c9c0f-117">Regénérez votre projet.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-117">Build your project again.</span></span>

![Activer la restauration des packages NuGet dans Outils/Options](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="c9c0f-119">Vous pouvez également changer ces paramètres dans votre fichier `NuGet.config` (consultez la section sur le [consentement](#consent)).</span><span class="sxs-lookup"><span data-stu-id="c9c0f-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="c9c0f-120">Si votre projet est un projet plus ancien qui utilise la restauration de packages intégrée à MSBuild, vous devrez peut-être [migrer](package-restore.md#migrate-to-automatic-package-restore-visual-studio) vers la restauration automatique des packages.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="c9c0f-121">Ce projet fait référence à un ou plusieurs packages NuGet qui ne figurent pas sur cet ordinateur</span><span class="sxs-lookup"><span data-stu-id="c9c0f-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="c9c0f-122">Message d’erreur complet :</span><span class="sxs-lookup"><span data-stu-id="c9c0f-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="c9c0f-123">Cette erreur se produit quand vous tentez de générer un projet contenant des références à un ou plusieurs packages NuGet qui ne sont pas installés sur l’ordinateur ou dans le projet.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="c9c0f-124">Lorsque vous utilisez le format de gestion [PackageReference](package-references-in-project-files.md) , cette erreur peut être un restes d’une packages.config à la migration de PackageReference et doit être [supprimée manuellement](../resources/NuGet-FAQ.md#working-with-packages) du fichier projet.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-124">When using the [PackageReference](package-references-in-project-files.md) management format, this error might be a leftover from a packages.config to PackageReference migration and needs to be [manually removed](../resources/NuGet-FAQ.md#working-with-packages) from the project file.</span></span>
- <span data-ttu-id="c9c0f-125">Si [ packages.config](../reference/packages-config.md) est utilisé, l’erreur signifie que le package n’est pas installé dans le dossier `packages` à la racine de la solution.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="c9c0f-126">Cette situation se produit souvent quand vous obtenez le code source d’un projet à partir du contrôle de code source ou d’un autre téléchargement.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="c9c0f-127">Les packages sont généralement omis du contrôle de code source ou des téléchargements car ils peuvent être restaurés à partir de flux de packages comme nuget.org. Pour plus d’informations, consultez [Packages et contrôle de code source](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="c9c0f-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="c9c0f-128">Leur inclusion engendrerait l’encombrement du dépôt ou la création inutile de fichiers .zip volumineux.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="c9c0f-129">L’erreur peut également se produire si votre fichier projet contient des chemins absolus vers des emplacements de package, et que vous déplacez le projet.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="c9c0f-130">Utilisez l’une des méthodes suivantes pour restaurer les packages :</span><span class="sxs-lookup"><span data-stu-id="c9c0f-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="c9c0f-131">Si vous avez déplacé le fichier projet, modifiez le fichier directement pour mettre à jour les références de package.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="c9c0f-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([restauration automatique](package-restore.md#restore-packages-automatically-using-visual-studio) ou [restauration manuelle](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="c9c0f-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="c9c0f-133">Interface CLI .NET</span><span class="sxs-lookup"><span data-stu-id="c9c0f-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="c9c0f-134">Interface CLI de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c9c0f-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="c9c0f-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="c9c0f-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="c9c0f-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="c9c0f-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="c9c0f-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="c9c0f-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="c9c0f-138">Après une restauration réussie, le package devrait être présent dans le dossier *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="c9c0f-139">Dans le cas des projets utilisant PackageReference, la restauration devrait recréer le fichier `obj/project.assets.json` ; en ce qui concerne les projets utilisant `packages.config`, le package devrait apparaître dans le dossier `packages` du projet.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="c9c0f-140">Le projet doit à présent être généré.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-140">The project should now build successfully.</span></span> <span data-ttu-id="c9c0f-141">Si ce n’est pas le cas, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions vous contacter.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="c9c0f-142">Le fichier de ressources project.assets.json est introuvable</span><span class="sxs-lookup"><span data-stu-id="c9c0f-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="c9c0f-143">Message d’erreur complet :</span><span class="sxs-lookup"><span data-stu-id="c9c0f-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="c9c0f-144">Le fichier `project.assets.json` conserve le graphique de dépendance d’un projet si le format de gestion PackageReference, qui permet de s’assurer que tous les packages nécessaires sont installés sur l’ordinateur, est utilisé.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="c9c0f-145">Ce fichier étant généré dynamiquement par la restauration de package, il n’est généralement pas ajouté au contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="c9c0f-146">Par conséquent, cette erreur se produit en cas de création d’un projet avec un outil comme `msbuild`, qui ne restaure pas automatiquement les packages.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="c9c0f-147">Dans ce cas, exécutez `msbuild -t:restore` suivi de `msbuild` ou utilisez `dotnet build` (qui restaure automatiquement les packages).</span><span class="sxs-lookup"><span data-stu-id="c9c0f-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="c9c0f-148">Vous pouvez également utiliser l’une des méthodes de restauration de package de la [section précédente](#missing).</span><span class="sxs-lookup"><span data-stu-id="c9c0f-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="c9c0f-149">Un ou plusieurs packages NuGet devant être restaurés ne l’ont pas été en raison d’une absence de consentement</span><span class="sxs-lookup"><span data-stu-id="c9c0f-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="c9c0f-150">Message d’erreur complet :</span><span class="sxs-lookup"><span data-stu-id="c9c0f-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="c9c0f-151">Cette erreur indique que la restauration des packages est désactivée dans votre configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="c9c0f-152">Vous pouvez changer les paramètres applicables dans Visual Studio comme décrit précédemment dans [Solution rapide pour les utilisateurs de Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="c9c0f-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="c9c0f-153">Vous pouvez également modifier ces paramètres dans le fichier `nuget.config` applicable (en général, `%AppData%\NuGet\NuGet.Config` sur Windows et `~/.nuget/NuGet/NuGet.Config` sur Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c9c0f-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="c9c0f-154">Vérifiez que les clés `enabled` et `automatic` sous `packageRestore` ont la valeur True :</span><span class="sxs-lookup"><span data-stu-id="c9c0f-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="c9c0f-155">Si vous modifiez les paramètres `packageRestore` directement dans `nuget.config`, redémarrez Visual Studio pour que la boîte de dialogue des options affiche les valeurs actuelles.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="c9c0f-156">Autres conditions potentielles</span><span class="sxs-lookup"><span data-stu-id="c9c0f-156">Other potential conditions</span></span>

- <span data-ttu-id="c9c0f-157">Vous pouvez rencontrer des erreurs de build en raison de fichiers manquants. Dans ce cas, vous recevez un message vous demandant d’utiliser la restauration NuGet pour les télécharger.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="c9c0f-158">Toutefois, l’exécution d’une restauration peut indiquer que tous les packages sont déjà installés et qu’il n’y a rien à restaurer.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="c9c0f-159">Dans ce cas, supprimez le dossier `packages` (si vous utilisez `packages.config`) ou le fichier `obj/project.assets.json` (si vous utilisez PackageReference), puis réexécutez la restauration.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="c9c0f-160">Si l’erreur persiste, utilisez `nuget locals all -clear` ou `dotnet nuget locals all --clear` en ligne de commande pour effacer les dossiers *global-packages* et cache, comme l’explique la page [Gérer les dossiers de packages globaux et de cache](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c9c0f-160">If the error still persists, use `nuget locals all -clear` or `dotnet nuget locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="c9c0f-161">Quand vous obtenez un projet à partir du contrôle de code source, les dossiers de votre projet peuvent être définis en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="c9c0f-162">Changez les autorisations des dossiers et réessayez de restaurer les packages.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="c9c0f-163">Vous utilisez peut-être une ancienne version de NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="c9c0f-164">Pour obtenir les dernières versions recommandées, accédez à [nuget.org/downloads](https://www.nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="c9c0f-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="c9c0f-165">Pour Visual Studio 2015, nous vous recommandons d’utiliser la version 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="c9c0f-166">Si vous rencontrez d’autres problèmes, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions obtenir plus d’informations de votre part.</span><span class="sxs-lookup"><span data-stu-id="c9c0f-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
