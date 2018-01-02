---
title: Installation des outils clients NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Conseils sur l’installation des outils clients, de l’interface de ligne de commande (CLI) et du Gestionnaire de package pour Visual Studio."
keywords: CLI NuGet.exe, outils clients NuGet, gestionnaire de package NuGet, console du gestionnaire de package NuGet, NuGet pour Visual Studio, NuGet Beta Channel
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="563fd-104">Installation des outils clients NuGet</span><span class="sxs-lookup"><span data-stu-id="563fd-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="563fd-105">**Vous souhaitez installer un package ? Consultez [Démarrage rapide - Utiliser un package](../Quickstart/Use-a-Package.md).**</span><span class="sxs-lookup"><span data-stu-id="563fd-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="563fd-106">Il existe deux outils principaux pour créer, publier et consommer des packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="563fd-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="563fd-107">[**L’interface de ligne de commande NuGet**](#nuget-cli) est l’utilitaire en ligne de commande pour Windows qui fournit toutes les fonctionnalités NuGet ; il peut également être exécuté sur Mac OSX et Linux à l’aide de Mono ou via l’interface de ligne de commande .NET Core (`dotnet`).</span><span class="sxs-lookup"><span data-stu-id="563fd-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="563fd-108">Le [**Gestionnaire de package NuGet dans Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows uniquement) est un outil GUI pour la gestion des packages et inclut une console PowerShell par le biais de laquelle vous pouvez utiliser certaines commandes NuGet directement dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="563fd-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="563fd-109">La console et l’interface utilisateur du Gestionnaire de package sont inclus dans Visual Studio (sur Windows) versions 2012 et ultérieures et peuvent être installées manuellement pour les versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="563fd-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="563fd-110">Avec Visual Studio pour Mac, les fonctionnalités NuGet sont intégrées directement.</span><span class="sxs-lookup"><span data-stu-id="563fd-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="563fd-111">Consultez [Inclusion d’un package NuGet dans votre projet](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) pour une procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="563fd-111">See [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="563fd-112">À l’heure actuelle, Visual Studio Code n’a pas de prise en charge intégrée de NuGet.</span><span class="sxs-lookup"><span data-stu-id="563fd-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="563fd-113">Utilisez l’interface de ligne de commande NuGet ou [l’interface de ligne de commande dotnet](../Tools/dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="563fd-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="563fd-114">Le Gestionnaire de package et l’interface de ligne de commande NuGet prennent en charge les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="563fd-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="563fd-115">Rechercher des packages</span><span class="sxs-lookup"><span data-stu-id="563fd-115">Search packages</span></span>
- <span data-ttu-id="563fd-116">Installer des packages</span><span class="sxs-lookup"><span data-stu-id="563fd-116">Install packages</span></span>
- <span data-ttu-id="563fd-117">Mettre à jour des packages</span><span class="sxs-lookup"><span data-stu-id="563fd-117">Update packages</span></span>
- <span data-ttu-id="563fd-118">Désinstaller des packages</span><span class="sxs-lookup"><span data-stu-id="563fd-118">Uninstall packages</span></span>
- <span data-ttu-id="563fd-119">Restaurer des packages (interface utilisateur uniquement dans le Gestionnaire de package)</span><span class="sxs-lookup"><span data-stu-id="563fd-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="563fd-120">Gérer les sources NuGet</span><span class="sxs-lookup"><span data-stu-id="563fd-120">Manage NuGet sources</span></span>

<span data-ttu-id="563fd-121">Les fonctionnalités suivantes sont uniquement prises en charge dans l’interface de ligne de commande NuGet :</span><span class="sxs-lookup"><span data-stu-id="563fd-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="563fd-122">Gérer les packages (nuget.org ou flux privé)</span><span class="sxs-lookup"><span data-stu-id="563fd-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="563fd-123">Créer des packages</span><span class="sxs-lookup"><span data-stu-id="563fd-123">Create packages</span></span> 
- <span data-ttu-id="563fd-124">Publier des packages</span><span class="sxs-lookup"><span data-stu-id="563fd-124">Publish packages</span></span>
- <span data-ttu-id="563fd-125">Gérer Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="563fd-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="563fd-126">Gérer le cache NuGet</span><span class="sxs-lookup"><span data-stu-id="563fd-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="563fd-127">Répliquer un package</span><span class="sxs-lookup"><span data-stu-id="563fd-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="563fd-128">Un autre bon outil est [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), outil autonome open source permettant d’explorer, de créer et de modifier des packages NuGet visuellement.</span><span class="sxs-lookup"><span data-stu-id="563fd-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="563fd-129">Il est très utile, par exemple, pour apporter des modifications expérimentales à une structure de package sans avoir à reconstruire le package systématiquement.</span><span class="sxs-lookup"><span data-stu-id="563fd-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="563fd-130">La chaîne d’outils multiplateforme de [l’interface de ligne de commande .NET Core](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation), utilisée pour développer des applications .NET Core, prend en charge une série de commandes NuGet, telles que delete, locals, push, pack et restore.</span><span class="sxs-lookup"><span data-stu-id="563fd-130">The cross-platform [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="563fd-131">Interface de ligne de commande NuGet</span><span class="sxs-lookup"><span data-stu-id="563fd-131">NuGet CLI</span></span>

<span data-ttu-id="563fd-132">L’interface de ligne de commande NuGet fournit l’accès à toutes les fonctionnalités NuGet et peut être exécutée sur Windows, Mac OSX et Linux, comme décrit dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="563fd-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="563fd-133">Windows</span><span class="sxs-lookup"><span data-stu-id="563fd-133">Windows</span></span>

<span data-ttu-id="563fd-134">**Téléchargement direct :**</span><span class="sxs-lookup"><span data-stu-id="563fd-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="563fd-135">Avec NuGet 1.4+, vous pouvez utiliser `nuget update -self` pour mettre à jour votre nuget.exe existant vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="563fd-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="563fd-136">**Autres méthodes :**</span><span class="sxs-lookup"><span data-stu-id="563fd-136">**Other methods:**</span></span>

- <span data-ttu-id="563fd-137">**Chocolatey** : installez le package Chocolatey [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) à l’aide du client [Chocolatey](http://chocolatey.org).</span><span class="sxs-lookup"><span data-stu-id="563fd-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="563fd-138">**Visual Studio** : installez le package [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) à partir de la console du Gestionnaire de package dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="563fd-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="563fd-139">**Pour les utilisateurs de NuGet 2.x** : en raison de modifications avec rupture introduites dans NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) pointe vers la dernière version stable de NuGet 2.x pour empêcher les ruptures potentielles des systèmes d’intégration continue.</span><span class="sxs-lookup"><span data-stu-id="563fd-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="563fd-140">Mac OSX et Linux</span><span class="sxs-lookup"><span data-stu-id="563fd-140">Mac OSX and Linux</span></span>

<span data-ttu-id="563fd-141">Sur Mac OSX et Linux, il existe deux façons d’exécuter l’interface de ligne de commande NuGet :</span><span class="sxs-lookup"><span data-stu-id="563fd-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="563fd-142">Installez le [SDK .NET Core](https://www.microsoft.com/net/download/core), qui inclut les fonctionnalités principales de NuGet.</span><span class="sxs-lookup"><span data-stu-id="563fd-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="563fd-143">Des téléchargements sont également répertoriés dans la page [github.com/dotnet/cli](https://github.com/dotnet/cli).</span><span class="sxs-lookup"><span data-stu-id="563fd-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="563fd-144">Si vous avez besoin de fonctionnalités plus complètes, utilisez la deuxième option ci-dessous pour utiliser `nuget.exe` avec Mono.</span><span class="sxs-lookup"><span data-stu-id="563fd-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="563fd-145">Installez [Mono](http://www.mono-project.com/docs/getting-started/install/), puis utilisez l’exécutable en ligne de commande `nuget.exe` pour Windows (version 3.2 et ultérieures) à partir de [nuget.org/downloads](https://nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="563fd-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="563fd-146">L’exécution de NuGet sur Mono est soumise aux limitations suivantes :</span><span class="sxs-lookup"><span data-stu-id="563fd-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="563fd-147">Commandes dont le fonctionnement a été confirmé au moyen de tests :</span><span class="sxs-lookup"><span data-stu-id="563fd-147">Commands tested to work:</span></span>
        - <span data-ttu-id="563fd-148">config</span><span class="sxs-lookup"><span data-stu-id="563fd-148">config</span></span>
        - <span data-ttu-id="563fd-149">delete</span><span class="sxs-lookup"><span data-stu-id="563fd-149">delete</span></span>
        - <span data-ttu-id="563fd-150">help</span><span class="sxs-lookup"><span data-stu-id="563fd-150">help</span></span>
        - <span data-ttu-id="563fd-151">install</span><span class="sxs-lookup"><span data-stu-id="563fd-151">install</span></span>
        - <span data-ttu-id="563fd-152">list</span><span class="sxs-lookup"><span data-stu-id="563fd-152">list</span></span>
        - <span data-ttu-id="563fd-153">push</span><span class="sxs-lookup"><span data-stu-id="563fd-153">push</span></span>
        - <span data-ttu-id="563fd-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="563fd-154">setApiKey</span></span>
        - <span data-ttu-id="563fd-155">sources</span><span class="sxs-lookup"><span data-stu-id="563fd-155">sources</span></span>
        - <span data-ttu-id="563fd-156">spec</span><span class="sxs-lookup"><span data-stu-id="563fd-156">spec</span></span>

    - <span data-ttu-id="563fd-157">Commandes fonctionnant partiellement :</span><span class="sxs-lookup"><span data-stu-id="563fd-157">Partially-working commands:</span></span>
        - <span data-ttu-id="563fd-158">pack : fonctionne avec des fichiers `.nuspec`, mais pas avec des fichiers projet.</span><span class="sxs-lookup"><span data-stu-id="563fd-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="563fd-159">restore : fonctionne avec des fichiers `packages.config` et `project.json`, mais pas avec des fichiers solution (`.sln`).</span><span class="sxs-lookup"><span data-stu-id="563fd-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="563fd-160">Commandes qui ne fonctionnent pas :</span><span class="sxs-lookup"><span data-stu-id="563fd-160">Commands that do not work:</span></span>
        - <span data-ttu-id="563fd-161">update</span><span class="sxs-lookup"><span data-stu-id="563fd-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="563fd-162">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="563fd-162">Related topics</span></span>

- [<span data-ttu-id="563fd-163">Informations de référence sur l’interface de ligne de commande NuGet</span><span class="sxs-lookup"><span data-stu-id="563fd-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="563fd-164">Création d’un package</span><span class="sxs-lookup"><span data-stu-id="563fd-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="563fd-165">Publication d’un package</span><span class="sxs-lookup"><span data-stu-id="563fd-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="563fd-166">Gestionnaire de package NuGet dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="563fd-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="563fd-167">Le Gestionnaire de package NuGet est inclus dans toutes les éditions de Visual Studio sur Windows (versions 2012 et ultérieures).</span><span class="sxs-lookup"><span data-stu-id="563fd-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="563fd-168">Il inclut l’interface utilisateur du Gestionnaire de package ([référence](../tools/package-manager-ui.md)), ainsi que la console du Gestionnaire de package par le biais de laquelle vous pouvez accéder aux outils fournis avec certains packages ([référence](../tools/package-manager-console.md)).</span><span class="sxs-lookup"><span data-stu-id="563fd-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="563fd-169">Le programme d’installation de Visual Studio 2017 inclut le Gestionnaire de package NuGet avec toute charge de travail qui utilise .NET.</span><span class="sxs-lookup"><span data-stu-id="563fd-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="563fd-170">Pour effectuer une installation séparément, ou pour vérifier que le Gestionnaire de package est installé, exécutez le programme d’installation de Visual Studio 2017 et cochez l’option sous **Composants individuels > Outils de code > Gestionnaire de package NuGet**.</span><span class="sxs-lookup"><span data-stu-id="563fd-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="563fd-171">La console requiert [PowerShell 2.0](http://support.microsoft.com/kb/968929), déjà installé sur Windows 7 ou version ultérieure et Windows Server 2008 R2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="563fd-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="563fd-172">De plus, les commandes de la console du Gestionnaire de package fonctionnent uniquement dans Visual Studio sur Windows.</span><span class="sxs-lookup"><span data-stu-id="563fd-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="563fd-173">Utilisez l’interface de ligne de commande NuGet en dehors de cet environnement, y compris avec Visual Studio pour Mac et Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="563fd-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="563fd-174">Installation du Gestionnaire de package pour Visual Studio 2010 et antérieur</span><span class="sxs-lookup"><span data-stu-id="563fd-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="563fd-175">*Ces étapes ne sont pas nécessaires pour Visual Studio 2012 et ultérieur, qui incluent déjà le Gestionnaire de package.*</span><span class="sxs-lookup"><span data-stu-id="563fd-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="563fd-176">Dans Visual Studio 2010 et antérieur, cliquez sur **Outils > Extensions et mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="563fd-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="563fd-177">Accédez à **En ligne**, puis recherchez « Gestionnaire de package NuGet dans Visual Studio » et cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="563fd-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="563fd-178">Dans la boîte de dialogue du programme d’installation, cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="563fd-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="563fd-179">Une fois l’installation terminée, redémarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="563fd-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="563fd-180">Si vous ne pouvez pas utiliser la boîte de dialogue **Extensions et mises à jour** dans Visual Studio (par exemple, si elle est bloquée par un proxy), vous pouvez télécharger des extensions pour Visual Studio 2013 et 2015 directement depuis l’adresse [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="563fd-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="563fd-181">Mise à jour du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="563fd-181">Updating the Package Manager</span></span>

<span data-ttu-id="563fd-182">Pour Visual Studio 2015 Update 2 et ultérieur, le Gestionnaire de package est automatiquement mis à jour avec la dernière version stable.</span><span class="sxs-lookup"><span data-stu-id="563fd-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="563fd-183">Pour Visual Studio 2015 Update 1 ou antérieur, sélectionnez la commande **Outils > Extensions et mises à jour**, puis cliquez sur l’onglet **Mises à jour** pour voir si une nouvelle version du Gestionnaire de package est disponible.</span><span class="sxs-lookup"><span data-stu-id="563fd-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="563fd-184">Aperçus de NuGet</span><span class="sxs-lookup"><span data-stu-id="563fd-184">NuGet previews</span></span>

<span data-ttu-id="563fd-185">Si vous souhaitez avoir un aperçu des fonctionnalités NuGet à venir, installez [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), qui fonctionne côte à côte avec les versions stables de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="563fd-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="563fd-186">Notez que la version NuGet Beta Channel précédente (`https://dotnet.myget.org/F/nuget-beta/vsix/`) pour Visual Studio 2015 n’est plus utilisée.</span><span class="sxs-lookup"><span data-stu-id="563fd-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="563fd-187">Pour signaler des problèmes avec une version de NuGet ou pour partager des idées, ouvrez un sujet sur le [dépôt GitHub NuGet](https://github.com/Nuget/Home).</span><span class="sxs-lookup"><span data-stu-id="563fd-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="563fd-188">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="563fd-188">Related topics</span></span>

- [<span data-ttu-id="563fd-189">Informations de référence sur l’interface utilisateur du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="563fd-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="563fd-190">Informations de référence sur la console du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="563fd-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="563fd-191">Informations de référence sur la console du Gestionnaire de package (version PowerShell)</span><span class="sxs-lookup"><span data-stu-id="563fd-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)