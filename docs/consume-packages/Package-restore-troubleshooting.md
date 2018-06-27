---
title: Résolution des problèmes de restauration de packages NuGet dans Visual Studio
description: Description des erreurs courantes liées à la restauration des packages NuGet dans Visual Studio et résolution de ces erreurs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 8e817b8e95c53d27120bf56db52b45b69a5ff973
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816968"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="0d78b-103">Résolution des erreurs de restauration des packages</span><span class="sxs-lookup"><span data-stu-id="0d78b-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="0d78b-104">Cet article aborde les erreurs rencontrées couramment pendant la restauration de packages, ainsi que les étapes de résolution.</span><span class="sxs-lookup"><span data-stu-id="0d78b-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="0d78b-105">Pour plus d’informations sur la restauration des packages, consultez [Restauration de packages](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="0d78b-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="0d78b-106">Si les instructions présentées ici ne fonctionnent pas, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions examiner plus attentivement votre situation.</span><span class="sxs-lookup"><span data-stu-id="0d78b-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="0d78b-107">N’utilisez pas le contrôle « Cette page est-elle utile ? »</span><span class="sxs-lookup"><span data-stu-id="0d78b-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="0d78b-108">qui peut apparaître dans cette page, car celui-ci ne nous permet pas de vous contacter pour obtenir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="0d78b-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="0d78b-109">Solution rapide pour les utilisateurs de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0d78b-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="0d78b-110">Si vous utilisez Visual Studio, commencez par activer la restauration des packages comme suit.</span><span class="sxs-lookup"><span data-stu-id="0d78b-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="0d78b-111">Sinon, passez aux autres sections de cet article.</span><span class="sxs-lookup"><span data-stu-id="0d78b-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="0d78b-112">Sélectionnez la commande de menu **Outils > Gestionnaire de package NuGet > Paramètres du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="0d78b-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="0d78b-113">Définissez les deux options sous **Restauration de package**.</span><span class="sxs-lookup"><span data-stu-id="0d78b-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="0d78b-114">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d78b-114">Select **OK**.</span></span>
1. <span data-ttu-id="0d78b-115">Regénérez votre projet.</span><span class="sxs-lookup"><span data-stu-id="0d78b-115">Build your project again.</span></span>

![Activer la restauration des packages NuGet dans Outils/Options](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="0d78b-117">Vous pouvez également changer ces paramètres dans votre fichier `NuGet.config` (consultez la section sur le [consentement](#consent)).</span><span class="sxs-lookup"><span data-stu-id="0d78b-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="0d78b-118">Ce projet fait référence à un ou plusieurs packages NuGet qui ne figurent pas sur cet ordinateur</span><span class="sxs-lookup"><span data-stu-id="0d78b-118">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="0d78b-119">Message d’erreur complet :</span><span class="sxs-lookup"><span data-stu-id="0d78b-119">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="0d78b-120">Cette erreur se produit en cas de tentative de création d’un projet contenant des références à un ou plusieurs packages NuGet qui ne sont pas installés sur l’ordinateur ou dans le projet.</span><span class="sxs-lookup"><span data-stu-id="0d78b-120">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="0d78b-121">Si le format de gestion PackageReference est utilisé, l’erreur signifie que le package n’est pas installé dans le dossier *global-packages*, comme l’explique la page [Gérer les dossiers de packages globaux et de cache](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="0d78b-121">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="0d78b-122">Si `packages.config` est utilisé, l’erreur signifie que le package n’est pas installé dans le dossier `packages` à la racine de la solution.</span><span class="sxs-lookup"><span data-stu-id="0d78b-122">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="0d78b-123">Cette situation se produit souvent quand vous obtenez le code source d’un projet à partir du contrôle de code source ou d’un autre téléchargement.</span><span class="sxs-lookup"><span data-stu-id="0d78b-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="0d78b-124">Les packages sont généralement omis du contrôle de code source ou des téléchargements car ils peuvent être restaurés à partir de flux de packages comme nuget.org. Pour plus d’informations, consultez [Packages et contrôle de code source](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="0d78b-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="0d78b-125">Leur inclusion engendrerait l’encombrement du dépôt ou la création inutile de fichiers .zip volumineux.</span><span class="sxs-lookup"><span data-stu-id="0d78b-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="0d78b-126">L’erreur peut également se produire si votre fichier projet contient des chemins absolus vers des emplacements de package, et que vous déplacez le projet.</span><span class="sxs-lookup"><span data-stu-id="0d78b-126">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="0d78b-127">Utilisez l’une des méthodes suivantes pour restaurer les packages :</span><span class="sxs-lookup"><span data-stu-id="0d78b-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="0d78b-128">Si vous avez déplacé le fichier projet, modifiez le fichier directement pour mettre à jour les références de package.</span><span class="sxs-lookup"><span data-stu-id="0d78b-128">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="0d78b-129">Dans Visual Studio, activez la restauration des packages. Pour cela, sélectionnez la commande de menu **Outils > Gestionnaire de Package NuGet > Paramètres du Gestionnaire de package**, définissez les deux options sous **Restauration de package**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d78b-129">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="0d78b-130">Ensuite, regénérez la solution.</span><span class="sxs-lookup"><span data-stu-id="0d78b-130">Then build the solution again.</span></span>
- <span data-ttu-id="0d78b-131">Pour les projets .NET Core, exécutez `dotnet restore` ou `dotnet build` (qui exécute automatiquement la restauration).</span><span class="sxs-lookup"><span data-stu-id="0d78b-131">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="0d78b-132">Sur la ligne de commande, exécutez `nuget restore` (sauf pour les projets créés avec `dotnet` ; dans ce cas, utilisez `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="0d78b-132">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="0d78b-133">Sur la ligne de commande avec les projets utilisant le format PackageReference, exécutez `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="0d78b-133">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="0d78b-134">Après une restauration réussie, le package devrait être présent dans le dossier *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="0d78b-134">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="0d78b-135">Dans le cas des projets utilisant PackageReference, la restauration devrait recréer le fichier `obj/project.assets.json` ; en ce qui concerne les projets utilisant `packages.config`, le package devrait apparaître dans le dossier `packages` du projet.</span><span class="sxs-lookup"><span data-stu-id="0d78b-135">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="0d78b-136">Le projet doit à présent être généré.</span><span class="sxs-lookup"><span data-stu-id="0d78b-136">The project should now build successfully.</span></span> <span data-ttu-id="0d78b-137">Si ce n’est pas le cas, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions vous contacter.</span><span class="sxs-lookup"><span data-stu-id="0d78b-137">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="0d78b-138">Le fichier de ressources project.assets.json est introuvable</span><span class="sxs-lookup"><span data-stu-id="0d78b-138">Assets file project.assets.json not found</span></span>

<span data-ttu-id="0d78b-139">Message d’erreur complet :</span><span class="sxs-lookup"><span data-stu-id="0d78b-139">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="0d78b-140">Le fichier `project.assets.json` conserve le graphique de dépendance d’un projet si le format de gestion PackageReference, qui permet de s’assurer que tous les packages nécessaires sont installés sur l’ordinateur, est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0d78b-140">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="0d78b-141">Ce fichier étant généré dynamiquement par la restauration de package, il n’est généralement pas ajouté au contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="0d78b-141">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="0d78b-142">Par conséquent, cette erreur se produit en cas de création d’un projet avec un outil comme `msbuild`, qui ne restaure pas automatiquement les packages.</span><span class="sxs-lookup"><span data-stu-id="0d78b-142">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="0d78b-143">Dans ce cas, exécutez `msbuild /t:restore` suivi de `msbuild` ou utilisez `dotnet build` (qui restaure automatiquement les packages).</span><span class="sxs-lookup"><span data-stu-id="0d78b-143">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="0d78b-144">Vous pouvez également utiliser l’une des méthodes de restauration de package de la [section précédente](#missing).</span><span class="sxs-lookup"><span data-stu-id="0d78b-144">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="0d78b-145">Un ou plusieurs packages NuGet devant être restaurés ne l’ont pas été en raison d’une absence de consentement</span><span class="sxs-lookup"><span data-stu-id="0d78b-145">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="0d78b-146">Message d’erreur complet :</span><span class="sxs-lookup"><span data-stu-id="0d78b-146">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="0d78b-147">Cette erreur indique que la restauration des packages est désactivée dans votre configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="0d78b-147">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="0d78b-148">Vous pouvez changer les paramètres applicables dans Visual Studio comme décrit précédemment dans [Solution rapide pour les utilisateurs de Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="0d78b-148">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="0d78b-149">Vous pouvez également modifier ces paramètres dans le fichier `nuget.config` applicable (en général, `%AppData%\NuGet\NuGet.Config` sur Windows et `~/.nuget/NuGet/NuGet.Config` sur Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="0d78b-149">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="0d78b-150">Vérifiez que les clés `enabled` et `automatic` sous `packageRestore` ont la valeur True :</span><span class="sxs-lookup"><span data-stu-id="0d78b-150">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="0d78b-151">Si vous modifiez les paramètres `packageRestore` directement dans `nuget.config`, redémarrez Visual Studio pour que la boîte de dialogue des options affiche les valeurs actuelles.</span><span class="sxs-lookup"><span data-stu-id="0d78b-151">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="0d78b-152">Autres conditions potentielles</span><span class="sxs-lookup"><span data-stu-id="0d78b-152">Other potential conditions</span></span>

- <span data-ttu-id="0d78b-153">Vous pouvez rencontrer des erreurs de build en raison de fichiers manquants. Dans ce cas, vous recevez un message vous demandant d’utiliser la restauration NuGet pour les télécharger.</span><span class="sxs-lookup"><span data-stu-id="0d78b-153">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="0d78b-154">Toutefois, l’exécution d’une restauration peut indiquer que tous les packages sont déjà installés et qu’il n’y a rien à restaurer.</span><span class="sxs-lookup"><span data-stu-id="0d78b-154">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="0d78b-155">Dans ce cas, supprimez le dossier `packages` (si vous utilisez `packages.config`) ou le fichier `obj/project.assets.json` (si vous utilisez PackageReference), puis réexécutez la restauration.</span><span class="sxs-lookup"><span data-stu-id="0d78b-155">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="0d78b-156">Si l’erreur persiste, utilisez `nuget locals all -clear` ou `dotnet locals all --clear` en ligne de commande pour effacer les dossiers *global-packages* et cache, comme l’explique la page [Gérer les dossiers de packages globaux et de cache](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="0d78b-156">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="0d78b-157">Quand vous obtenez un projet à partir du contrôle de code source, les dossiers de votre projet peuvent être définis en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="0d78b-157">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="0d78b-158">Changez les autorisations des dossiers et réessayez de restaurer les packages.</span><span class="sxs-lookup"><span data-stu-id="0d78b-158">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="0d78b-159">Vous utilisez peut-être une ancienne version de NuGet.</span><span class="sxs-lookup"><span data-stu-id="0d78b-159">You may be using an old version of NuGet.</span></span> <span data-ttu-id="0d78b-160">Pour obtenir les dernières versions recommandées, accédez à [nuget.org/downloads](https://www.nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="0d78b-160">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="0d78b-161">Pour Visual Studio 2015, nous vous recommandons d’utiliser la version 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="0d78b-161">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="0d78b-162">Si vous rencontrez d’autres problèmes, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions obtenir plus d’informations de votre part.</span><span class="sxs-lookup"><span data-stu-id="0d78b-162">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>