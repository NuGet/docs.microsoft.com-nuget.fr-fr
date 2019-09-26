---
title: Questions fréquentes (FAQ) sur NuGet
description: Questions courantes et réponses sur l’utilisation de NuGet sur la ligne de commande et dans Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8cc990e0c9eed07c59c8dffb04d104be47051736
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999939"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="59b75-103">Questions fréquentes (FAQ) sur NuGet</span><span class="sxs-lookup"><span data-stu-id="59b75-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="59b75-104">Pour parcourir les questions fréquemment posées à propos de NuGet.org, notamment les questions relatives aux comptes NuGet.org, consultez [Questions fréquentes (FAQ) sur NuGet.org](../nuget-org/nuget-org-faq.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-104">For frequently-asked questions pertaining to NuGet.org, such as NuGet.org account questions, see [NuGet.org frequently-asked questions](../nuget-org/nuget-org-faq.md).</span></span>

<span data-ttu-id="59b75-105">**Quels sont les éléments nécessaires pour exécuter NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="59b75-106">Toutes les informations relatives à l’interface utilisateur et aux outils en ligne de commande sont disponibles dans le [guide d’installation](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="59b75-107">**NuGet prend-il en charge Mono ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="59b75-108">L’outil en ligne de commande, `nuget.exe`, génère et s’exécute sous Mono 3.2+ et peut créer des packages dans Mono.</span><span class="sxs-lookup"><span data-stu-id="59b75-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="59b75-109">Bien que `nuget.exe` fonctionne entièrement sur Windows, il existe des problèmes connus sur Linux et OS X. Consultez [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) (Problèmes Mono) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="59b75-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="59b75-110">Un [client graphique](https://github.com/mrward/monodevelop-nuget-addin) est disponible en guise de complément pour MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="59b75-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="59b75-111">**Comment puis-je déterminer ce que contient un package et s’il est stable et utile pour mon application ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="59b75-112">La principale source d’apprentissage sur un package est sa page d’annonce sur nuget.org (ou sur un autre flux privé).</span><span class="sxs-lookup"><span data-stu-id="59b75-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="59b75-113">Chaque page de package sur nuget.org inclut une description du package, son historique des versions et les statistiques d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="59b75-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="59b75-114">La section **Info** sur la page de package contient également un lien vers le site web du projet où vous trouvez généralement de nombreux exemples et autres documentations pour vous aider à découvrir comment le package est utilisé.</span><span class="sxs-lookup"><span data-stu-id="59b75-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="59b75-115">Pour plus d’informations, consultez [Recherche et sélection des packages](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="59b75-116">NuGet dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59b75-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="59b75-117">**Comment NuGet est-il pris en charge dans les différents produits Visual Studio ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="59b75-118">Visual Studio sur Windows prend en charge [l’interface utilisateur du Gestionnaire de package](../consume-packages/install-use-packages-visual-studio.md) et la [console du Gestionnaire de package](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-118">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="59b75-119">Visual Studio pour Mac offre des fonctionnalités NuGet intégrées, comme décrit dans [Inclusion d’un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="59b75-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="59b75-120">Visual Studio Code (toutes les plateformes) n’a pas d’intégration directe de NuGet.</span><span class="sxs-lookup"><span data-stu-id="59b75-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="59b75-121">Utilisez [l’interface de ligne de commande NuGet](../reference/nuget-exe-cli-reference.md) ou [l’interface de ligne de commande dotnet](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-121">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="59b75-122">Azure DevOps fournit [une étape de la génération pour restaurer des packages NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="59b75-122">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="59b75-123">Vous pouvez également [héberger des flux de packages NuGet privés sur Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="59b75-123">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="59b75-124">**Comment vérifier la version exacte des outils NuGet qui sont installés ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="59b75-125">Dans Visual Studio, utilisez la commande **Aide > À propos de Microsoft Visual Studio** et examinez la version affichée en regard de **Gestionnaire de package NuGet**.</span><span class="sxs-lookup"><span data-stu-id="59b75-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="59b75-126">Vous pouvez également lancer la console du Gestionnaire de package (**Outils > Gestionnaire de package NuGet > Console du Gestionnaire de package**), puis entrer `$host` pour afficher des informations sur NuGet, notamment la version.</span><span class="sxs-lookup"><span data-stu-id="59b75-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="59b75-127">**Quels sont les langages de programmation pris en charge par NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="59b75-128">En règle générale, NuGet fonctionne pour les langages .NET et est conçu pour intégrer les bibliothèques .NET dans un projet.</span><span class="sxs-lookup"><span data-stu-id="59b75-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="59b75-129">Comme il prend également en charge MSBuild et Visual Studio Automation dans certains types de projets, il prend aussi en charge d’autres projets et langages à des degrés divers.</span><span class="sxs-lookup"><span data-stu-id="59b75-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="59b75-130">La version la plus récente de NuGet prend en charge C#, Visual Basic, F#, WiX et C++.</span><span class="sxs-lookup"><span data-stu-id="59b75-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="59b75-131">**Quels sont les modèles de projet pris en charge par NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="59b75-132">NuGet prend totalement en charge de nombreux modèles de projet tels que Windows, Web, Cloud, SharePoint, Wix, etc.</span><span class="sxs-lookup"><span data-stu-id="59b75-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="59b75-133">**Comment mettre à jour les packages qui font partie de modèles Visual Studio ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="59b75-134">Accédez à l’onglet **Mises à jour** dans l’interface utilisateur du Gestionnaire de package et sélectionnez **Mettre à jour tout**, ou utilisez la [commande `Update-Package`](../reference/ps-reference/ps-ref-update-package.md) à partir de la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="59b75-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="59b75-135">Pour mettre à jour le modèle lui-même, vous devez mettre à jour manuellement le dépôt du modèle.</span><span class="sxs-lookup"><span data-stu-id="59b75-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="59b75-136">Consultez le [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="59b75-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="59b75-137">Notez que cette opération est effectuée à vos risques et périls, étant donné que les mises à jour manuelles peuvent endommager le modèle si les dernières versions de toutes les dépendances ne sont pas compatibles entre elles.</span><span class="sxs-lookup"><span data-stu-id="59b75-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="59b75-138">**Puis-je utiliser NuGet en dehors de Visual Studio ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="59b75-139">Oui, NuGet fonctionne directement à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="59b75-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="59b75-140">Consultez le [guide d’installation](../install-nuget-client-tools.md) et les [informations de référence sur l’interface de ligne de commande](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="59b75-141">Ligne de commande NuGet</span><span class="sxs-lookup"><span data-stu-id="59b75-141">NuGet command line</span></span>

<span data-ttu-id="59b75-142">**Comment obtenir la dernière version de l’outil en ligne de commande NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="59b75-143">Consultez le [guide d’installation](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-143">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="59b75-144">Pour vérifier la version actuelle installée de l'outil, utilisez `nuget help`.</span><span class="sxs-lookup"><span data-stu-id="59b75-144">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="59b75-145">**Quelle est la licence pour nuget.exe ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-145">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="59b75-146">Vous êtes autorisé à redistribuer nuget.exe selon les termes de la licence du MIT.</span><span class="sxs-lookup"><span data-stu-id="59b75-146">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="59b75-147">Vous êtes responsable de la mise à jour et de la maintenance de toutes les copies de nuget.exe que vous souhaitez redistribuer.</span><span class="sxs-lookup"><span data-stu-id="59b75-147">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="59b75-148">**Est-il possible d’étendre l’outil en ligne de commande NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-148">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="59b75-149">Oui, vous pouvez ajouter des commandes personnalisées à `nuget.exe`, comme le décrit le [billet de blog de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="59b75-149">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="59b75-150">Console du Gestionnaire de package NuGet (Visual Studio sur Windows)</span><span class="sxs-lookup"><span data-stu-id="59b75-150">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="59b75-151">**Comment accéder à l’objet DTE dans la console du Gestionnaire de package ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-151">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="59b75-152">L’objet de niveau supérieur dans le modèle objet automation Visual Studio est appelé objet DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="59b75-152">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="59b75-153">La console le fournit par le biais d’une variable nommée `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="59b75-153">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="59b75-154">Pour plus d’informations, consultez [Vue d’ensemble du modèle Automation](/visualstudio/extensibility/internals/automation-model-overview) dans la documentation de l’extensibilité de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59b75-154">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="59b75-155">**J’essaie d’effectuer un cast de la variable $DTE en type DTE2, mais j’obtiens une erreur : Impossible de convertir la valeur « EnvDTE.DTEClass » de type « EnvDTE.DTEClass » en type « EnvDTE80.DTE2 ». Quel est le problème ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-155">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="59b75-156">Il s’agit d’un problème connu lié à la façon dont PowerShell interagit avec un objet COM.</span><span class="sxs-lookup"><span data-stu-id="59b75-156">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="59b75-157">Essayez l’opération suivante :</span><span class="sxs-lookup"><span data-stu-id="59b75-157">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="59b75-158">`Get-Interface` est une fonction d’assistance ajoutée par l’hôte PowerShell NuGet.</span><span class="sxs-lookup"><span data-stu-id="59b75-158">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="59b75-159">Création et publication de packages</span><span class="sxs-lookup"><span data-stu-id="59b75-159">Creating and publishing packages</span></span>

<span data-ttu-id="59b75-160">**Comment répertorier mon package dans un flux ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-160">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="59b75-161">Consultez [Création et publication d’un package](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-161">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="59b75-162">**Plusieurs versions de ma bibliothèque ciblent des versions différentes du .NET Framework. Comment créer un package unique qui prend en charge ce cas de figure ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-162">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="59b75-163">Consultez [Prise en charge de plusieurs versions et profils du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-163">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="59b75-164">**Comment définir mon propre dépôt ou flux ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-164">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="59b75-165">Consultez la [vue d’ensemble de l’hébergement des packages](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="59b75-165">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="59b75-166">**Comment charger des packages sur mon flux NuGet en bloc ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-166">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="59b75-167">Consultez [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (Publication de packages NuGet en bloc) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="59b75-167">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="59b75-168">Utilisation des packages</span><span class="sxs-lookup"><span data-stu-id="59b75-168">Working with packages</span></span>

<span data-ttu-id="59b75-169">**Quelle est la différence entre un package au niveau du projet et un package au niveau de la solution ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-169">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="59b75-170">Un package au niveau de la solution (NuGet 3.x+) est installé une seule fois dans une solution, puis est disponible pour tous les projets de la solution.</span><span class="sxs-lookup"><span data-stu-id="59b75-170">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="59b75-171">Un package au niveau du projet est installé dans chaque projet qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="59b75-171">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="59b75-172">Un package au niveau de la solution peut également installer de nouvelles commandes qui peuvent être appelées à partir de la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="59b75-172">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="59b75-173">**Est-il possible d’installer des packages NuGet sans connexion Internet ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-173">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="59b75-174">Oui, consultez le billet de Blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="59b75-174">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="59b75-175">**Comment installer des packages dans un autre emplacement que le dossier de packages par défaut ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-175">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="59b75-176">Définissez le paramètre [`repositoryPath`](../reference/nuget-config-file.md#config-section) dans `Nuget.Config` en utilisant `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="59b75-176">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="59b75-177">**Comment éviter d’ajouter le dossier de packages NuGet dans le contrôle de code source ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-177">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="59b75-178">Définissez [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) dans `Nuget.Config` sur `true`.</span><span class="sxs-lookup"><span data-stu-id="59b75-178">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="59b75-179">Cette clé, qui fonctionne au niveau de la solution, doit être ajoutée au fichier `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="59b75-179">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="59b75-180">L’activation de la restauration des packages à partir de Visual Studio crée ce fichier automatiquement.</span><span class="sxs-lookup"><span data-stu-id="59b75-180">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="59b75-181">**Comment désactiver la restauration des packages ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-181">**How do I turn off package restore?**</span></span>

<span data-ttu-id="59b75-182">Consultez [Activation et désactivation de la restauration des packages](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="59b75-182">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="59b75-183">**Quand j’installe un package local avec des dépendances distantes, j’obtiens un message indiquant qu’il est impossible de résoudre une erreur de dépendance. Pourquoi ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-183">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="59b75-184">Vous devez sélectionner la source **Tous** durant l’installation d’un package local dans le projet.</span><span class="sxs-lookup"><span data-stu-id="59b75-184">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="59b75-185">Cette option regroupe tous les flux au lieu d’en utiliser un seul.</span><span class="sxs-lookup"><span data-stu-id="59b75-185">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="59b75-186">Cette erreur est liée au fait que les utilisateurs d’un dépôt local souhaitent souvent éviter d’installer accidentellement un package distant en raison de stratégies d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="59b75-186">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="59b75-187">**J’ai plusieurs projets dans le même dossier ; comment utiliser des fichiers packages.config distincts pour chaque projet ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-187">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="59b75-188">Dans la plupart des projets où des projets distincts se trouvent dans des dossiers séparés, ce n’est pas un problème, car NuGet identifie les fichiers `packages.config` dans chaque projet.</span><span class="sxs-lookup"><span data-stu-id="59b75-188">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="59b75-189">Si vous utilisez NuGet 3.3+ et que plusieurs projets se trouvent dans le même dossier, vous pouvez insérer le nom du projet dans les noms de fichier `packages.config` et utiliser le modèle `packages.{project-name}.config` ; NuGet utilise alors ce fichier.</span><span class="sxs-lookup"><span data-stu-id="59b75-189">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="59b75-190">Cela n’est pas un problème si vous utilisez PackageReference, car chaque fichier de projet contient sa propre liste de dépendances.</span><span class="sxs-lookup"><span data-stu-id="59b75-190">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="59b75-191">**Je ne vois pas nuget.org dans la liste des dépôts ; comment le récupérer ?**</span><span class="sxs-lookup"><span data-stu-id="59b75-191">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="59b75-192">Ajoutez `https://api.nuget.org/v3/index.json` à votre liste de sources, ou</span><span class="sxs-lookup"><span data-stu-id="59b75-192">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="59b75-193">Supprimez `%appdata%\.nuget\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) et laissez NuGet le recréer.</span><span class="sxs-lookup"><span data-stu-id="59b75-193">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>