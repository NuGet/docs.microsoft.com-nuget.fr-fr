---
title: "Résolution des problèmes de restauration de packages NuGet dans Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Description des erreurs courantes liées à la restauration des packages NuGet dans Visual Studio et résolution de ces erreurs."
keywords: "Restauration des packages NuGet, restauration des packages, résolution des problèmes, résoudre les problèmes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="6087b-104">Résolution des erreurs de restauration des packages</span><span class="sxs-lookup"><span data-stu-id="6087b-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="6087b-105">Cet article aborde les erreurs rencontrées couramment pendant la restauration de packages, ainsi que les étapes de résolution.</span><span class="sxs-lookup"><span data-stu-id="6087b-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="6087b-106">Pour plus d’informations sur la restauration des packages, consultez [Restauration de packages](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="6087b-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="6087b-107">Si les instructions présentées ici ne fonctionnent pas, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions examiner plus attentivement votre situation.</span><span class="sxs-lookup"><span data-stu-id="6087b-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="6087b-108">N’utilisez pas le contrôle « Cette page est-elle utile ? »</span><span class="sxs-lookup"><span data-stu-id="6087b-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="6087b-109">qui peut apparaître dans cette page, car celui-ci ne nous permet pas de vous contacter pour obtenir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6087b-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="6087b-110">Solution rapide pour les utilisateurs de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6087b-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="6087b-111">Si vous utilisez Visual Studio, commencez par activer la restauration des packages comme suit.</span><span class="sxs-lookup"><span data-stu-id="6087b-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="6087b-112">Sinon, passez aux autres sections de cet article.</span><span class="sxs-lookup"><span data-stu-id="6087b-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="6087b-113">Sélectionnez la commande de menu **Outils > Gestionnaire de package NuGet > Paramètres du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="6087b-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="6087b-114">Définissez les deux options sous **Restauration de package**.</span><span class="sxs-lookup"><span data-stu-id="6087b-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="6087b-115">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="6087b-115">Select **OK**.</span></span>
1. <span data-ttu-id="6087b-116">Regénérez votre projet.</span><span class="sxs-lookup"><span data-stu-id="6087b-116">Build your project again.</span></span>

![Activer la restauration des packages NuGet dans Outils/Options](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="6087b-118">Vous pouvez également changer ces paramètres dans votre fichier `NuGet.config` (consultez la section sur le [consentement](#consent)).</span><span class="sxs-lookup"><span data-stu-id="6087b-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="6087b-119">Ce projet fait référence à un ou plusieurs packages NuGet qui ne figurent pas sur cet ordinateur</span><span class="sxs-lookup"><span data-stu-id="6087b-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="6087b-120">Message d’erreur complet :</span><span class="sxs-lookup"><span data-stu-id="6087b-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="6087b-121">Cette erreur se produit quand vous essayez de générer un projet qui contient des références à un ou plusieurs packages NuGet, mais que ces derniers ne sont pas actuellement mis en cache dans le projet.</span><span class="sxs-lookup"><span data-stu-id="6087b-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="6087b-122">(Les packages sont mis en cache dans un dossier `packages` à la racine de la solution si le projet utilise `packages.config`, ou dans le fichier `obj/project.assets.json` si le projet utilise le format PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="6087b-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="6087b-123">Cette situation se produit souvent quand vous obtenez le code source d’un projet à partir du contrôle de code source ou d’un autre téléchargement.</span><span class="sxs-lookup"><span data-stu-id="6087b-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="6087b-124">Les packages sont généralement omis du contrôle de code source ou des téléchargements car ils peuvent être restaurés à partir de flux de packages comme nuget.org. Pour plus d’informations, consultez [Packages et contrôle de code source](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="6087b-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="6087b-125">Leur inclusion engendrerait l’encombrement du dépôt ou la création inutile de fichiers .zip volumineux.</span><span class="sxs-lookup"><span data-stu-id="6087b-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="6087b-126">Utilisez l’une des méthodes suivantes pour restaurer les packages :</span><span class="sxs-lookup"><span data-stu-id="6087b-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="6087b-127">Dans Visual Studio, activez la restauration des packages. Pour cela, sélectionnez la commande de menu **Outils > Gestionnaire de Package NuGet > Paramètres du Gestionnaire de package**, définissez les deux options sous **Restauration de package**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="6087b-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="6087b-128">Ensuite, regénérez la solution.</span><span class="sxs-lookup"><span data-stu-id="6087b-128">Then build the solution again.</span></span>
- <span data-ttu-id="6087b-129">Pour les projets .NET Core, exécutez `dotnet restore` ou `dotnet build` (qui exécute automatiquement la restauration).</span><span class="sxs-lookup"><span data-stu-id="6087b-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="6087b-130">Sur la ligne de commande, exécutez `nuget restore` (sauf pour les projets créés avec `dotnet` ; dans ce cas, utilisez `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="6087b-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="6087b-131">Sur la ligne de commande avec les projets utilisant le format PackageReference, exécutez `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="6087b-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="6087b-132">Après une restauration réussie, vous devriez voir soit un dossier `packages` (si vous utilisez `packages.config`), soit le fichier `obj/project.assets.json` (si vous utilisez PackageReference).</span><span class="sxs-lookup"><span data-stu-id="6087b-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="6087b-133">Le projet doit à présent être généré.</span><span class="sxs-lookup"><span data-stu-id="6087b-133">The project should now build successfully.</span></span> <span data-ttu-id="6087b-134">Si ce n’est pas le cas, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions vous contacter.</span><span class="sxs-lookup"><span data-stu-id="6087b-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="6087b-135">Le fichier de ressources project.assets.json est introuvable</span><span class="sxs-lookup"><span data-stu-id="6087b-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="6087b-136">Message d’erreur complet :</span><span class="sxs-lookup"><span data-stu-id="6087b-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="6087b-137">Cette erreur se produit pour les mêmes raisons que celles décrites dans la [section précédente](#missing). Les solutions à adopter sont aussi les mêmes.</span><span class="sxs-lookup"><span data-stu-id="6087b-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="6087b-138">Par exemple, l’exécution de `msbuild` sur un projet .NET Core obtenu à partir du contrôle de code source ne restaure pas automatiquement les packages.</span><span class="sxs-lookup"><span data-stu-id="6087b-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="6087b-139">Dans ce cas, exécutez `msbuild /t:restore` suivi de `msbuild` ou utilisez `dotnet build` (qui restaure automatiquement les packages).</span><span class="sxs-lookup"><span data-stu-id="6087b-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="6087b-140">Un ou plusieurs packages NuGet devant être restaurés ne l’ont pas été en raison d’une absence de consentement</span><span class="sxs-lookup"><span data-stu-id="6087b-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="6087b-141">Message d’erreur complet :</span><span class="sxs-lookup"><span data-stu-id="6087b-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="6087b-142">Cette erreur indique que la restauration des packages est désactivée dans votre configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="6087b-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="6087b-143">Vous pouvez changer les paramètres applicables dans Visual Studio comme décrit précédemment dans [Solution rapide pour les utilisateurs de Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="6087b-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="6087b-144">Vous pouvez également modifier ces paramètres dans le fichier `nuget.config` applicable (en général, `%AppData%\NuGet\NuGet.Config` sur Windows et `~/.nuget/NuGet/NuGet.Config` sur Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6087b-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="6087b-145">Vérifiez que les clés `enabled` et `automatic` sous `packageRestore` ont la valeur True :</span><span class="sxs-lookup"><span data-stu-id="6087b-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="6087b-146">Si vous modifiez les paramètres `packageRestore` directement dans `nuget.config`, redémarrez Visual Studio pour que la boîte de dialogue des options affiche les valeurs actuelles.</span><span class="sxs-lookup"><span data-stu-id="6087b-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="6087b-147">Autres conditions potentielles</span><span class="sxs-lookup"><span data-stu-id="6087b-147">Other potential conditions</span></span>

- <span data-ttu-id="6087b-148">Vous pouvez rencontrer des erreurs de build en raison de fichiers manquants. Dans ce cas, vous recevez un message vous demandant d’utiliser la restauration NuGet pour les télécharger.</span><span class="sxs-lookup"><span data-stu-id="6087b-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="6087b-149">Toutefois, l’exécution d’une restauration peut indiquer que tous les packages sont déjà installés et qu’il n’y a rien à restaurer.</span><span class="sxs-lookup"><span data-stu-id="6087b-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="6087b-150">Dans ce cas, supprimez le dossier `packages` (si vous utilisez `packages.config`) ou le fichier `obj/project.assets.json` (si vous utilisez PackageReference), puis réexécutez la restauration.</span><span class="sxs-lookup"><span data-stu-id="6087b-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="6087b-151">Quand vous obtenez un projet à partir du contrôle de code source, les dossiers de votre projet peuvent être définis en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="6087b-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="6087b-152">Changez les autorisations des dossiers et réessayez de restaurer les packages.</span><span class="sxs-lookup"><span data-stu-id="6087b-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="6087b-153">Vous utilisez peut-être une ancienne version de NuGet.</span><span class="sxs-lookup"><span data-stu-id="6087b-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="6087b-154">Pour obtenir les dernières versions recommandées, accédez à [nuget.org/downloads](https://www.nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="6087b-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="6087b-155">Pour Visual Studio 2015, nous vous recommandons d’utiliser la version 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="6087b-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="6087b-156">Si vous rencontrez d’autres problèmes, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions obtenir plus d’informations de votre part.</span><span class="sxs-lookup"><span data-stu-id="6087b-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>