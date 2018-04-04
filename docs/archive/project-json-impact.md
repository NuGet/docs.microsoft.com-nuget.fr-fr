---
title: Impact de project.json sur les auteurs de packages NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informations sur la façon dont l’implémentation de project.json dans NuGet 3.x affecte les auteurs de packages, notamment en termes de fonctionnalités, de contenu et de format de package non pris en charge.
keywords: NuGet et project.json, impact de project.json, considérations liées à la création de packages, fonctionnalités de project.json
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6e8af98504a2866106e84943989aeb91f2e9c1fb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="abe2e-104">Impact de project.json lors de la création de packages</span><span class="sxs-lookup"><span data-stu-id="abe2e-104">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="abe2e-105">Ce contenu est déconseillé.</span><span class="sxs-lookup"><span data-stu-id="abe2e-105">This content is deprecated.</span></span> <span data-ttu-id="abe2e-106">Les projets doivent utiliser soit le format `packages.config`, soit le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="abe2e-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="abe2e-107">Le système `project.json` utilisé dans NuGet 3+ affecte les auteurs de packages de plusieurs façons, comme décrit dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="abe2e-107">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="abe2e-108">Modifications affectant l’utilisation de packages existants</span><span class="sxs-lookup"><span data-stu-id="abe2e-108">Changes affecting existing packages usage</span></span>

<span data-ttu-id="abe2e-109">Les packages NuGet traditionnels prennent en charge un ensemble de fonctionnalités qui ne sont pas reportées dans le monde transitif.</span><span class="sxs-lookup"><span data-stu-id="abe2e-109">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="abe2e-110">Les scripts d’installation et de désinstallation sont ignorés</span><span class="sxs-lookup"><span data-stu-id="abe2e-110">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="abe2e-111">Le modèle de restauration transitif, décrit dans la [résolution des dépendances](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), n’a pas le concept d’« heure d’installation du package ».</span><span class="sxs-lookup"><span data-stu-id="abe2e-111">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="abe2e-112">Un package est soit présent, soit absent, mais il n’existe aucun processus cohérent qui se produit lorsqu’un package est installé.</span><span class="sxs-lookup"><span data-stu-id="abe2e-112">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="abe2e-113">De plus, les scripts d’installation étaient pris en charge uniquement dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abe2e-113">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="abe2e-114">Les environnements de développement intégrés (IDE) devaient simuler l’API d’extensibilité de Visual Studio pour essayer de prendre en charge de tels scripts, et aucune prise en charge n’était disponible dans les éditeurs courants et les outils en ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="abe2e-114">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="abe2e-115">Les transformations de contenu ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="abe2e-115">Content transforms are not supported</span></span>

<span data-ttu-id="abe2e-116">À l’instar des scripts d’installation, les transformations s’exécutent sur l’installation du package et ne sont généralement pas idempotentes.</span><span class="sxs-lookup"><span data-stu-id="abe2e-116">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="abe2e-117">Étant donné qu’il n’existe plus d’heure d’installation, XDT Transform et d’autres fonctionnalités similaires ne sont pas prises en charge et sont ignorées si un tel package est utilisé dans un scénario transitif.</span><span class="sxs-lookup"><span data-stu-id="abe2e-117">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="abe2e-118">Contenu</span><span class="sxs-lookup"><span data-stu-id="abe2e-118">Content</span></span>

<span data-ttu-id="abe2e-119">Les packages NuGet traditionnels fournissent des fichiers de contenu comme des fichiers de code source et de configuration.</span><span class="sxs-lookup"><span data-stu-id="abe2e-119">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="abe2e-120">Ils sont en général utilisés dans deux scénarios :</span><span class="sxs-lookup"><span data-stu-id="abe2e-120">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="abe2e-121">Les fichiers initiaux sont déposés dans le projet de sorte que l’utilisateur peut les modifier ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="abe2e-121">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="abe2e-122">Les fichiers de configuration par défaut en sont un exemple type.</span><span class="sxs-lookup"><span data-stu-id="abe2e-122">The common example is default configuration files.</span></span>

1. <span data-ttu-id="abe2e-123">Les fichiers de contenu sont utilisés comme compléments des assemblys installés dans le projet.</span><span class="sxs-lookup"><span data-stu-id="abe2e-123">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="abe2e-124">Une image de logo utilisée par un assembly en serait un exemple.</span><span class="sxs-lookup"><span data-stu-id="abe2e-124">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="abe2e-125">La prise en charge du contenu est actuellement désactivée pour des raisons similaires à celle des scripts et transformations, mais nous sommes en train de la concevoir.</span><span class="sxs-lookup"><span data-stu-id="abe2e-125">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="abe2e-126">Les fichiers de contenu peuvent toujours être déplacés à l’intérieur des packages, même s’ils sont ignorés actuellement, mais l’utilisateur final peut toujours les copier au bon endroit.</span><span class="sxs-lookup"><span data-stu-id="abe2e-126">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="abe2e-127">Vous trouverez une des propositions de réintégration des fichiers de contenu et pourrez suivre sa progression ici : [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="abe2e-127">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="abe2e-128">Impact pour les auteurs de packages</span><span class="sxs-lookup"><span data-stu-id="abe2e-128">Impact for package authors</span></span>

<span data-ttu-id="abe2e-129">Les packages qui utilisent les fonctionnalités ci-dessus doivent utiliser un autre mécanisme.</span><span class="sxs-lookup"><span data-stu-id="abe2e-129">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="abe2e-130">Le plus couramment utilisé des mécanismes implique les cibles/propriétés MSBuild qui continuent d’être entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="abe2e-130">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="abe2e-131">Le système de génération peut choisir d’autres conventions dans le package.</span><span class="sxs-lookup"><span data-stu-id="abe2e-131">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="abe2e-132">C’est de cette façon que les cibles MSBuild sont prises en charge, ainsi que les analyseurs Roslyn.</span><span class="sxs-lookup"><span data-stu-id="abe2e-132">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="abe2e-133">Il est possible de générer des packages qui prennent en charge des cibles et des analyseurs pour les scénarios `packages.config` et `project.json`.</span><span class="sxs-lookup"><span data-stu-id="abe2e-133">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="abe2e-134">Les packages qui essaient de modifier le projet pour en faciliter le démarrage fonctionnent généralement dans un ensemble très limité de scénarios et doivent plutôt fournir un fichier Lisez-moi ou des instructions d’utilisation du package.</span><span class="sxs-lookup"><span data-stu-id="abe2e-134">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="abe2e-135">La plupart des packages existants n’ont pas besoin d’utiliser le format de package décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="abe2e-135">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="abe2e-136">Le format active le contenu natif en tant que scénario de première classe.</span><span class="sxs-lookup"><span data-stu-id="abe2e-136">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="abe2e-137">Cela signifie que les assemblys managés qui dépendent d’implémentations matérielles fournissent des implémentations binaires en même temps que les assemblys managés en fonction de la plateforme cible.</span><span class="sxs-lookup"><span data-stu-id="abe2e-137">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="abe2e-138">Par exemple, le package System.IO.Compression utilise cette technologie.</span><span class="sxs-lookup"><span data-stu-id="abe2e-138">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="abe2e-139">En résumé, si la fonctionnalité ci-dessus n’est pas indispensable, nous vous recommandons de continuer à utiliser le format de package existant, puisque le format décrit ici est pris en charge uniquement par NuGet 3.x+.</span><span class="sxs-lookup"><span data-stu-id="abe2e-139">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="abe2e-140">Il est possible de générer des packages utilisables pour les scénarios `packages.config` et `project.json` par ajustement, cependant il est souvent plus simple de structurer uniquement les packages de manière traditionnelle, sans les fonctionnalités dépréciées mentionnées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="abe2e-140">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="abe2e-141">Format de package 3.x</span><span class="sxs-lookup"><span data-stu-id="abe2e-141">3.x package format</span></span>

<span data-ttu-id="abe2e-142">Le format de package 3.x permet plusieurs fonctionnalités supplémentaires au-delà de NuGet 2.x :</span><span class="sxs-lookup"><span data-stu-id="abe2e-142">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="abe2e-143">Définition d’un assembly de référence utilisé pour la compilation et d’un jeu d’assemblys d’implémentation utilisé pour le runtime sur différents appareils/plateformes.</span><span class="sxs-lookup"><span data-stu-id="abe2e-143">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="abe2e-144">Ceci vous permet d’exploiter les API propres à la plateforme tout en fournissant une surface d’exposition commune à vos consommateurs.</span><span class="sxs-lookup"><span data-stu-id="abe2e-144">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="abe2e-145">Plus précisément, cela facilite l’écriture de bibliothèques portables intermédiaires.</span><span class="sxs-lookup"><span data-stu-id="abe2e-145">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="abe2e-146">Permet aux packages de tourner sur les plateformes, par exemple les systèmes d’exploitation ou l’architecture UC.</span><span class="sxs-lookup"><span data-stu-id="abe2e-146">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="abe2e-147">Permet de séparer les implémentations spécifiques de plateforme des packages complémentaires.</span><span class="sxs-lookup"><span data-stu-id="abe2e-147">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="abe2e-148">Prise en charge des dépendances natives en tant que citoyen de première classe.</span><span class="sxs-lookup"><span data-stu-id="abe2e-148">Support Native dependencies as a first class citizen.</span></span>
