---
title: "Questions fréquentes (FAQ) sur NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: "Questions courantes et réponses sur l’utilisation de NuGet depuis la ligne de commande et dans Visual Studio et sur l’utilisation de la galerie NuGet."
keywords: "Q&R sur NuGet, questions et réponses, problèmes courants, versions NuGet, versions de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d19a24a2d1955e996e18d44fee346865d36493f8
ms.sourcegitcommit: e5b7cf6675be9891341c196afe822cea6f71d60c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/08/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="30af0-104">Questions fréquentes (FAQ) sur NuGet</span><span class="sxs-lookup"><span data-stu-id="30af0-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="30af0-105">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="30af0-105">In this topic:</span></span>

- [<span data-ttu-id="30af0-106">Prise en main</span><span class="sxs-lookup"><span data-stu-id="30af0-106">Getting started</span></span>](#getting-started)
- [<span data-ttu-id="30af0-107">NuGet dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30af0-107">NuGet in Visual Studio</span></span>](#nuget-in-visual-studio)
- [<span data-ttu-id="30af0-108">Ligne de commande NuGet</span><span class="sxs-lookup"><span data-stu-id="30af0-108">NuGet command line</span></span>](#nuget-command-line)
- [<span data-ttu-id="30af0-109">Console du Gestionnaire de package NuGet</span><span class="sxs-lookup"><span data-stu-id="30af0-109">NuGet Package Manager Console</span></span>](#nuget-package-manager-console)
- [<span data-ttu-id="30af0-110">Création et publication de packages</span><span class="sxs-lookup"><span data-stu-id="30af0-110">Creating and publishing packages</span></span>](#creating-and-publishing-packages)
- [<span data-ttu-id="30af0-111">Utilisation des packages</span><span class="sxs-lookup"><span data-stu-id="30af0-111">Working with packages</span></span>](#working-with-packages)
- [<span data-ttu-id="30af0-112">Gestion des packages sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="30af0-112">Managing packages on nuget.org</span></span>](#managing-packages-on-nugetorg)
- [<span data-ttu-id="30af0-113">nuget.org inaccessible</span><span class="sxs-lookup"><span data-stu-id="30af0-113">nuget.org not accessible</span></span>](#nugetorg-not-accessible)

## <a name="getting-started"></a><span data-ttu-id="30af0-114">Bien démarrer</span><span class="sxs-lookup"><span data-stu-id="30af0-114">Getting started</span></span>

<span data-ttu-id="30af0-115">**Quels sont les éléments nécessaires pour exécuter NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-115">**What is required to run NuGet?**</span></span>

<span data-ttu-id="30af0-116">Toutes les informations relatives à l’interface utilisateur et aux outils en ligne de commande sont disponibles dans le [guide d’installation](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="30af0-116">All the information around both UI and command-line tools is available in the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="30af0-117">**NuGet prend-il en charge Mono ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-117">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="30af0-118">L’outil en ligne de commande, `nuget.exe`, génère et s’exécute sous Mono 3.2+ et peut créer des packages dans Mono.</span><span class="sxs-lookup"><span data-stu-id="30af0-118">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="30af0-119">Bien que `nuget.exe` fonctionne entièrement sur Windows, il existe des problèmes connus sur Linux et OS X. Consultez [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) (Problèmes Mono) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="30af0-119">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="30af0-120">Un [client graphique](https://github.com/mrward/monodevelop-nuget-addin) est disponible en guise de complément pour MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="30af0-120">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="30af0-121">**Comment puis-je déterminer ce que contient un package et s’il est stable et utile pour mon application ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-121">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="30af0-122">La principale source d’apprentissage sur un package est sa page d’annonce sur nuget.org (ou sur un autre flux privé).</span><span class="sxs-lookup"><span data-stu-id="30af0-122">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="30af0-123">Chaque page de package sur nuget.org inclut une description du package, son historique des versions et les statistiques d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="30af0-123">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="30af0-124">La section **Info** sur la page de package contient également un lien vers le site web du projet où vous trouvez généralement de nombreux exemples et autres documentations pour vous aider à découvrir comment le package est utilisé.</span><span class="sxs-lookup"><span data-stu-id="30af0-124">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="30af0-125">Pour plus d’informations, consultez [Recherche et sélection des packages](../Consume-Packages/Finding-and-Choosing-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="30af0-125">For more information, see [Finding and choosing packages](../Consume-Packages/Finding-and-Choosing-Packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="30af0-126">NuGet dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30af0-126">NuGet in Visual Studio</span></span>

<span data-ttu-id="30af0-127">**Comment NuGet est-il pris en charge dans les différents produits Visual Studio ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-127">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="30af0-128">Visual Studio sur Windows prend en charge [l’interface utilisateur du Gestionnaire de package](../tools/Package-Manager-UI.md) et la [console du Gestionnaire de package](../tools/Package-Manager-Console.md).</span><span class="sxs-lookup"><span data-stu-id="30af0-128">Visual Studio on Windows supports the [Package Manager UI](../tools/Package-Manager-UI.md) and the [Package Manager Console](../tools/Package-Manager-Console.md).</span></span>
- <span data-ttu-id="30af0-129">Visual Studio pour Mac offre des fonctionnalités NuGet intégrées, comme décrit dans [Inclusion d’un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="30af0-129">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="30af0-130">Visual Studio Code (toutes les plateformes) n’a pas d’intégration directe de NuGet.</span><span class="sxs-lookup"><span data-stu-id="30af0-130">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="30af0-131">Utilisez [l’interface de ligne de commande NuGet](../tools/nuget-exe-CLI-Reference.md) ou [l’interface de ligne de commande dotnet](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="30af0-131">Use the [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="30af0-132">Visual Studio Team Services fournit [une étape de génération pour restaurer les packages NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="30af0-132">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="30af0-133">Vous pouvez également [héberger les flux de package NuGet privés sur Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="30af0-133">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="30af0-134">**Comment vérifier la version exacte des outils NuGet qui sont installés ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-134">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="30af0-135">Dans Visual Studio, utilisez la commande **Aide > À propos de Microsoft Visual Studio** et examinez la version affichée en regard de **Gestionnaire de package NuGet**.</span><span class="sxs-lookup"><span data-stu-id="30af0-135">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="30af0-136">Vous pouvez également lancer la console du Gestionnaire de package (**Outils > Gestionnaire de package NuGet > Console du Gestionnaire de package**), puis entrer `$host` pour afficher des informations sur NuGet, notamment la version.</span><span class="sxs-lookup"><span data-stu-id="30af0-136">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="30af0-137">**Quels sont les langages de programmation pris en charge par NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-137">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="30af0-138">En règle générale, NuGet fonctionne pour les langages .NET et est conçu pour intégrer les bibliothèques .NET dans un projet.</span><span class="sxs-lookup"><span data-stu-id="30af0-138">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="30af0-139">Comme il prend également en charge MSBuild et Visual Studio Automation dans certains types de projets, il prend aussi en charge d’autres projets et langages à des degrés divers.</span><span class="sxs-lookup"><span data-stu-id="30af0-139">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="30af0-140">La version la plus récente de NuGet prend en charge C#, Visual Basic, F#, WiX et C++.</span><span class="sxs-lookup"><span data-stu-id="30af0-140">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="30af0-141">**Quels sont les modèles de projet pris en charge par NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-141">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="30af0-142">NuGet prend totalement en charge de nombreux modèles de projet tels que Windows, Web, Cloud, SharePoint, Wix, etc.</span><span class="sxs-lookup"><span data-stu-id="30af0-142">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="30af0-143">**Comment mettre à jour les packages qui font partie de modèles Visual Studio ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-143">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="30af0-144">Accédez à l’onglet **Mises à jour** dans l’interface utilisateur du Gestionnaire de package et sélectionnez **Mettre à jour tout**, ou utilisez la [commande `Update-Package`](../Tools/ps-ref-update-package.md) à partir de la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="30af0-144">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../Tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="30af0-145">Pour mettre à jour le modèle lui-même, vous devez mettre à jour manuellement le dépôt du modèle.</span><span class="sxs-lookup"><span data-stu-id="30af0-145">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="30af0-146">Consultez le [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="30af0-146">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="30af0-147">Notez que cette opération est effectuée à vos risques et périls, étant donné que les mises à jour manuelles peuvent endommager le modèle si les dernières versions de toutes les dépendances ne sont pas compatibles entre elles.</span><span class="sxs-lookup"><span data-stu-id="30af0-147">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="30af0-148">**Puis-je utiliser NuGet en dehors de Visual Studio ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-148">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="30af0-149">Oui, NuGet fonctionne directement à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="30af0-149">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="30af0-150">Consultez le [guide d’installation](../guides/install-nuget.md) et les [informations de référence sur l’interface de ligne de commande](../tools/nuget-exe-CLI-Reference.md).</span><span class="sxs-lookup"><span data-stu-id="30af0-150">See the [Install guide](../guides/install-nuget.md) and the [CLI reference](../tools/nuget-exe-CLI-Reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="30af0-151">Ligne de commande NuGet</span><span class="sxs-lookup"><span data-stu-id="30af0-151">NuGet command line</span></span>

<span data-ttu-id="30af0-152">**Comment obtenir la dernière version de l’outil en ligne de commande NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-152">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="30af0-153">Consultez le [guide d’installation](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="30af0-153">See the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="30af0-154">**Est-il possible d’étendre l’outil en ligne de commande NuGet ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-154">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="30af0-155">Oui, vous pouvez ajouter des commandes personnalisées à `nuget.exe`, comme le décrit le [billet de blog de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="30af0-155">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="30af0-156">Console du Gestionnaire de package NuGet (Visual Studio sur Windows)</span><span class="sxs-lookup"><span data-stu-id="30af0-156">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="30af0-157">**Comment accéder à l’objet DTE dans la console du Gestionnaire de package ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-157">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="30af0-158">L’objet de niveau supérieur dans le modèle objet automation Visual Studio est appelé objet DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="30af0-158">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="30af0-159">La console le fournit par le biais d’une variable nommée `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="30af0-159">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="30af0-160">Pour plus d’informations, consultez [Vue d’ensemble du modèle Automation](/visualstudio/extensibility/internals/automation-model-overview) dans la documentation de l’extensibilité de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30af0-160">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="30af0-161">**J’essaie de caster la variable $DTE en type DTE2, mais j’obtiens une erreur indiquant qu’il est impossible de convertir la valeur « EnvDTE.DTEClass » du type « EnvDTE.DTEClass » en type « EnvDTE80.DTE2 ». Quel est le problème ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-161">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="30af0-162">Il s’agit d’un problème connu lié à la façon dont PowerShell interagit avec un objet COM.</span><span class="sxs-lookup"><span data-stu-id="30af0-162">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="30af0-163">Essayez l’opération suivante :</span><span class="sxs-lookup"><span data-stu-id="30af0-163">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="30af0-164">`Get-Interface` est une fonction d’assistance ajoutée par l’hôte PowerShell NuGet.</span><span class="sxs-lookup"><span data-stu-id="30af0-164">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="30af0-165">Création et publication de packages</span><span class="sxs-lookup"><span data-stu-id="30af0-165">Creating and publishing packages</span></span>

<span data-ttu-id="30af0-166">**Comment répertorier mon package dans un flux ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-166">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="30af0-167">Consultez [Création et publication d’un package](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="30af0-167">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="30af0-168">**Plusieurs versions de ma bibliothèque ciblent des versions différentes du .NET Framework. Comment créer un package unique qui prend en charge ce cas de figure ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-168">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="30af0-169">Consultez [Prise en charge de plusieurs versions et profils du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="30af0-169">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="30af0-170">**Comment définir mon propre dépôt ou flux ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-170">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="30af0-171">Consultez la [vue d’ensemble de l’hébergement des packages](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="30af0-171">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="30af0-172">**Comment charger des packages sur mon flux NuGet en bloc ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-172">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="30af0-173">Consultez [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (Publication de packages NuGet en bloc) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="30af0-173">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="30af0-174">Utilisation des packages</span><span class="sxs-lookup"><span data-stu-id="30af0-174">Working with packages</span></span>

<span data-ttu-id="30af0-175">**Quelle est la différence entre un package au niveau du projet et un package au niveau de la solution ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-175">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="30af0-176">Un package au niveau de la solution (NuGet 3.x+) est installé une seule fois dans une solution, puis est disponible pour tous les projets de la solution.</span><span class="sxs-lookup"><span data-stu-id="30af0-176">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="30af0-177">Un package au niveau du projet est installé dans chaque projet qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="30af0-177">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="30af0-178">Un package au niveau de la solution peut également installer de nouvelles commandes qui peuvent être appelées à partir de la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="30af0-178">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="30af0-179">**Est-il possible d’installer des packages NuGet sans connexion Internet ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-179">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="30af0-180">Oui, consultez le billet de Blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="30af0-180">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="30af0-181">**Comment installer des packages dans un autre emplacement que le dossier de packages par défaut ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-181">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="30af0-182">Définissez le paramètre [`repositoryPath`](../Schema/nuget-config-file.md#config-section) dans `Nuget.Config` en utilisant `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="30af0-182">Set the [`repositoryPath`](../Schema/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="30af0-183">**Comment éviter d’ajouter le dossier de packages NuGet dans le contrôle de code source ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-183">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="30af0-184">Définissez [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) dans `Nuget.Config` sur `true`.</span><span class="sxs-lookup"><span data-stu-id="30af0-184">Set the [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="30af0-185">Cette clé, qui fonctionne au niveau de la solution, doit être ajoutée au fichier `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="30af0-185">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="30af0-186">L’activation de la restauration des packages à partir de Visual Studio crée ce fichier automatiquement.</span><span class="sxs-lookup"><span data-stu-id="30af0-186">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="30af0-187">**Comment désactiver la restauration des packages ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-187">**How do I turn off package restore?**</span></span>

<span data-ttu-id="30af0-188">Consultez [Activation et désactivation de la restauration des packages](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="30af0-188">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="30af0-189">**Quand j’installe un package local avec des dépendances distantes, j’obtiens un message indiquant qu’il est impossible de résoudre une erreur de dépendance. Pourquoi ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-189">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="30af0-190">Vous devez sélectionner la source **Tous** durant l’installation d’un package local dans le projet.</span><span class="sxs-lookup"><span data-stu-id="30af0-190">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="30af0-191">Cette option regroupe tous les flux au lieu d’en utiliser un seul.</span><span class="sxs-lookup"><span data-stu-id="30af0-191">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="30af0-192">Cette erreur est liée au fait que les utilisateurs d’un dépôt local souhaitent souvent éviter d’installer accidentellement un package distant en raison de stratégies d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="30af0-192">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="30af0-193">**J’ai plusieurs projets dans le même dossier ; comment utiliser des fichiers packages.config distincts pour chaque projet ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-193">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="30af0-194">Dans la plupart des projets où des projets distincts se trouvent dans des dossiers séparés, ce n’est pas un problème, car NuGet identifie les fichiers `packages.config` dans chaque projet.</span><span class="sxs-lookup"><span data-stu-id="30af0-194">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="30af0-195">Si vous utilisez NuGet 3.3+ et que plusieurs projets se trouvent dans le même dossier, vous pouvez insérer le nom du projet dans les noms de fichier `packages.config` et utiliser le modèle `packages.{project-name}.config` ; NuGet utilise alors ce fichier.</span><span class="sxs-lookup"><span data-stu-id="30af0-195">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="30af0-196">Cela n’est pas un problème si vous utilisez PackageReference, car chaque fichier de projet contient sa propre liste de dépendances.</span><span class="sxs-lookup"><span data-stu-id="30af0-196">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="30af0-197">**Je ne vois pas nuget.org dans la liste des dépôts ; comment le récupérer ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-197">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="30af0-198">Ajoutez `https://api.nuget.org/v3/index.json` à votre liste de sources, ou</span><span class="sxs-lookup"><span data-stu-id="30af0-198">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="30af0-199">Supprimez le `%appdata%\.nuget\NuGet.Config` et laissez NuGet le recréer.</span><span class="sxs-lookup"><span data-stu-id="30af0-199">Delete the `%appdata%\.nuget\NuGet.Config` and let NuGet re-create it.</span></span>

<span data-ttu-id="30af0-200">**Quels sont les termes du contrat de licence si un package ne fournit pas des informations de licence spécifiques ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-200">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="30af0-201">Chaque package est régi par les conditions qu’il inclut.</span><span class="sxs-lookup"><span data-stu-id="30af0-201">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="30af0-202">Vous devez examiner les conditions applicables avant d’accéder à des packages, d’en télécharger ou d’en acquérir.</span><span class="sxs-lookup"><span data-stu-id="30af0-202">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="30af0-203">Sur nuget.org, utilisez le lien **License Info** (Informations de licence) sur la page des packages.</span><span class="sxs-lookup"><span data-stu-id="30af0-203">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="30af0-204">Si un package ne spécifie pas les termes du contrat de licence, contactez le propriétaire du package directement à l’aide du lien **Contact owners** (Contacter les propriétaires) sur la page des packages nuget.org.</span><span class="sxs-lookup"><span data-stu-id="30af0-204">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="30af0-205">Microsoft ne vous concède aucune licence de propriété intellectuelle de fournisseurs de packages tiers et n’est pas responsable des informations fournies par des tiers.</span><span class="sxs-lookup"><span data-stu-id="30af0-205">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>


## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="30af0-206">Gestion des packages sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="30af0-206">Managing packages on nuget.org</span></span>

<span data-ttu-id="30af0-207">**Puis-je modifier les métadonnées d’un package après l’avoir chargé ? Pourquoi demandez-vous de modifier le fichier nuspec et de charger un nouveau package pour apporter des modifications aux métadonnées du package ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-207">**Can I edit package metadata after it's been uploaded? Why do you require editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="30af0-208">NuGet exige que tous les packages soient signés.</span><span class="sxs-lookup"><span data-stu-id="30af0-208">NuGet requires all packages to be signed.</span></span> <span data-ttu-id="30af0-209">Un principe de conception de la signature du package est que le contenu du package signé doit être immuable, ce qui comprend le fichier nuspec.</span><span class="sxs-lookup"><span data-stu-id="30af0-209">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="30af0-210">Modifier les métadonnées du package entraîne des modifications du fichier nuspec, invalidant les signatures existantes.</span><span class="sxs-lookup"><span data-stu-id="30af0-210">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="30af0-211">Nous vous recommandons de modifier les flux de travail existants de manière à ce qu’il ne soit pas nécessaire de modifier les métadonnées du package une fois ce dernier créé.</span><span class="sxs-lookup"><span data-stu-id="30af0-211">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="30af0-212">Notez que les dépendances répertoriées pour votre package sont générées automatiquement à partir du package lui-même et qu’elles ne peuvent pas être modifiées.</span><span class="sxs-lookup"><span data-stu-id="30af0-212">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="30af0-213">De plus, le chargement d’un package sur [staging.nuget.org](http://staging.nuget.org) est un excellent moyen de le tester et de le valider sans le mettre à disposition dans la galerie publique.</span><span class="sxs-lookup"><span data-stu-id="30af0-213">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="30af0-214">**Est-il possible de réserver des noms pour les packages destinés à être publiés ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-214">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="30af0-215">Oui.</span><span class="sxs-lookup"><span data-stu-id="30af0-215">Yes.</span></span> <span data-ttu-id="30af0-216">Vous pouvez réserver des ID pour les packages sur [nuget.org](https://www.nuget.org/) en demandant un préfixe d’ID de package pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="30af0-216">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="30af0-217">Pour demander un préfixe d’ID de package, envoyez un e-mail à account (at) nuget.org avec le nom complet du propriétaire du package et le préfixe d’ID de package demandé.</span><span class="sxs-lookup"><span data-stu-id="30af0-217">In order to request a package ID prefix, send mail to account (at) nuget.org with the package owner display name, and the requested package ID prefix.</span></span>  

<span data-ttu-id="30af0-218">**Comment revendiquer la propriété de packages ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-218">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="30af0-219">Consultez [Gestion des propriétaires de packages sur nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="30af0-219">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="30af0-220">**Comment négocier avec un propriétaire de package qui viole ma licence de logiciel ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-220">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="30af0-221">Nous invitons la communauté NuGet à collaborer afin de résoudre les litiges pouvant survenir entre les propriétaires de packages et les propriétaires d’autres logiciels.</span><span class="sxs-lookup"><span data-stu-id="30af0-221">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="30af0-222">Nous avons conçu un [processus de résolution des litiges](../policies/dispute-resolution.md) à suivre avant de demander aux administrateurs de nuget.org d’intervenir.</span><span class="sxs-lookup"><span data-stu-id="30af0-222">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="30af0-223">**Est-il recommandé de charger mes packages de test sur nuget.org ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-223">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="30af0-224">À des fins de test, vous pouvez utiliser [staging.nuget.org](http://staging.nuget.org), ou d’autres serveurs NuGet publics comme [myget.org](https://myget.org) ou [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="30af0-224">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="30af0-225">Notez que les packages chargés sur staging.nuget.org ne sont pas nécessairement conservés.</span><span class="sxs-lookup"><span data-stu-id="30af0-225">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="30af0-226">Consultez [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="30af0-226">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="30af0-227">**Quelle est la taille maximale des packages que je peux charger sur nuget.org ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-227">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="30af0-228">La taille maximale de package autorisée par nuget.org est de 250 Mo, mais nous vous recommandons de limiter la taille des packages à 1 Mo maximum si possible et de les lier à l’aide de dépendances.</span><span class="sxs-lookup"><span data-stu-id="30af0-228">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="30af0-229">En règle générale, les packages contiennent un seul assembly pour éviter les collisions.</span><span class="sxs-lookup"><span data-stu-id="30af0-229">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="30af0-230">NuGet utilisant HTTP pour télécharger les packages, l’installation d’un package risque d’autant plus d’échouer que celui-ci est volumineux.</span><span class="sxs-lookup"><span data-stu-id="30af0-230">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="30af0-231">Vous pouvez partager des dépendances entre plusieurs packages, pour réduire la taille totale du téléchargement pour les consommateurs de vos packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="30af0-231">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="30af0-232">Les dépendances sont principalement statiques et ne changent jamais.</span><span class="sxs-lookup"><span data-stu-id="30af0-232">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="30af0-233">Quand vous résolvez un bogue dans le code, il peut s’avérer superflu de mettre à jour les dépendances.</span><span class="sxs-lookup"><span data-stu-id="30af0-233">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="30af0-234">Si vous regroupez des dépendances, vous finissez systématiquement par relivrer des packages plus volumineux.</span><span class="sxs-lookup"><span data-stu-id="30af0-234">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="30af0-235">Si vous fractionnez les packages NuGet en dépendances connexes, les mises à niveau sont beaucoup plus précises pour les consommateurs de votre package.</span><span class="sxs-lookup"><span data-stu-id="30af0-235">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="30af0-236">nuget.org inaccessible</span><span class="sxs-lookup"><span data-stu-id="30af0-236">nuget.org not accessible</span></span>

<span data-ttu-id="30af0-237">**Pourquoi ne puis-je pas télécharger de packages à partir de nuget.org ou en y charger ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-237">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="30af0-238">Tout d’abord, veillez à utiliser les dernières versions de NuGet.</span><span class="sxs-lookup"><span data-stu-id="30af0-238">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="30af0-239">Si cette version continue à échouer, [contactez le support technique](https://www.nuget.org/policies/Contact) et fournissez des informations supplémentaires pour la résolution du problème de connexion, notamment les suivantes :</span><span class="sxs-lookup"><span data-stu-id="30af0-239">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="30af0-240">Version de NuGet que vous utilisez</span><span class="sxs-lookup"><span data-stu-id="30af0-240">The version of NuGet you're using</span></span>
- <span data-ttu-id="30af0-241">Sources de package que vous utilisez</span><span class="sxs-lookup"><span data-stu-id="30af0-241">The package sources you're using</span></span>
- <span data-ttu-id="30af0-242">Journal de restauration avec commentaires détaillés</span><span class="sxs-lookup"><span data-stu-id="30af0-242">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="30af0-243">MTR ou traces Fiddler (voir ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="30af0-243">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="30af0-244">Votre zone géographique</span><span class="sxs-lookup"><span data-stu-id="30af0-244">Your geographical area</span></span>
- <span data-ttu-id="30af0-245">Version de votre système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="30af0-245">Your operating system version</span></span>
- <span data-ttu-id="30af0-246">Configuration de la machine (processeur, réseau, disque dur)</span><span class="sxs-lookup"><span data-stu-id="30af0-246">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="30af0-247">Si votre machine se trouve derrière un pare-feu ou proxy</span><span class="sxs-lookup"><span data-stu-id="30af0-247">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="30af0-248">Versions de .NET installées sur la machine</span><span class="sxs-lookup"><span data-stu-id="30af0-248">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="30af0-249">Versions des outils multiplateformes telles que l’interface de ligne de commande .NET ou DNU que vous utilisez</span><span class="sxs-lookup"><span data-stu-id="30af0-249">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="30af0-250">*Pour capturer MTR :*</span><span class="sxs-lookup"><span data-stu-id="30af0-250">*To capture MTR:*</span></span>

- <span data-ttu-id="30af0-251">Téléchargez WinMTR à partir de [http://winmtr.net/download/](http://winmtr.net/).</span><span class="sxs-lookup"><span data-stu-id="30af0-251">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="30af0-252">Entrez `api.nuget.org` comme nom d’hôte et cliquez sur **Start** (Démarrer).</span><span class="sxs-lookup"><span data-stu-id="30af0-252">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="30af0-253">Attendez que la colonne **Sent** (Envoyé) soit supérieure ou égale à 100.</span><span class="sxs-lookup"><span data-stu-id="30af0-253">Wait until the **Sent** column is >= 100.</span></span>

    ![Capture de MTR](media/mtr.png)

- <span data-ttu-id="30af0-255">Copiez le texte dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="30af0-255">Copy text to clipboard.</span></span>

<span data-ttu-id="30af0-256">*Pour capturer Fiddler :*</span><span class="sxs-lookup"><span data-stu-id="30af0-256">*To capture Fiddler:*</span></span>

- <span data-ttu-id="30af0-257">Installez la version la plus récente de [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="30af0-257">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="30af0-258">Démarrez Fiddler et désactivez la capture du trafic à l’aide du menu **File > Capture Traffic** (Fichier > Capturer le trafic).</span><span class="sxs-lookup"><span data-stu-id="30af0-258">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="30af0-259">Supprimez toutes les sessions (sélectionnez tous les éléments de la liste, puis appuyez sur la touche **Supprimer**).</span><span class="sxs-lookup"><span data-stu-id="30af0-259">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="30af0-260">Configurez Fiddler pour capturer le trafic HTTPS en cochant **Decrypt HTTPS traffic** (Déchiffrer le trafic HTTPS) sous l’onglet **HTTPS** du menu **Tools > Fiddler Options...** (Outils > Options Fiddler...).</span><span class="sxs-lookup"><span data-stu-id="30af0-260">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="30af0-261">Fermez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30af0-261">Close Visual Studio.</span></span>
- <span data-ttu-id="30af0-262">Activez **l’option Capture Traffic (Capturer le trafic) dans le menu File (Fichier)**.</span><span class="sxs-lookup"><span data-stu-id="30af0-262">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="30af0-263">Démarrez Visual Studio ou nuget.exe et effectuez les actions qui ne fonctionnent pas.</span><span class="sxs-lookup"><span data-stu-id="30af0-263">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="30af0-264">Le trafic généré par ces actions doit s’afficher dans Fiddler.</span><span class="sxs-lookup"><span data-stu-id="30af0-264">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="30af0-265">Une fois les actions exécutées, utilisez **File > Save > All Sessions** (Fichier > Enregistrer > Toutes les sessions) pour stocker les sessions capturées.</span><span class="sxs-lookup"><span data-stu-id="30af0-265">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="30af0-266">Remarque : Il peut être nécessaire de définir la variable d’environnement `HTTP_PROXY` sur `http://127.0.0.1:8888` pour router le trafic NuGet via Fiddler.</span><span class="sxs-lookup"><span data-stu-id="30af0-266">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="30af0-267">Si cette opération échoue, essayez les [conseils mentionnés dans ce billet de StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="30af0-267">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="30af0-268">**Quels sont les points de terminaison d’API pour nuget.org ?**</span><span class="sxs-lookup"><span data-stu-id="30af0-268">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="30af0-269">V3 : `https://api.nuget.org/v3/index.json` V2 : `https://www.nuget.org/api/v2/` (Notez que l’API V2 est dépréciée et ne fonctionne pas avec NuGet 4+.)</span><span class="sxs-lookup"><span data-stu-id="30af0-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
