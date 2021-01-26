---
title: Notes de publication de NuGet 2,1
description: Notes de publication de NuGet 2,1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777030"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="9c948-103">Notes de publication de NuGet 2,1</span><span class="sxs-lookup"><span data-stu-id="9c948-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="9c948-104">Notes de publication de [NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Notes de publication de NuGet 2,2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="9c948-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="9c948-105">NuGet 2,1 a été publié le 4 octobre 2012.</span><span class="sxs-lookup"><span data-stu-id="9c948-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="9c948-106">Nuget.Config hiérarchique</span><span class="sxs-lookup"><span data-stu-id="9c948-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="9c948-107">NuGet 2,1 vous offre une plus grande flexibilité dans le contrôle des paramètres NuGet grâce à la redirection récursive de la structure de dossiers à la recherche de `NuGet.Config` fichiers, puis à la génération de la configuration à partir de l’ensemble de tous les fichiers trouvés.</span><span class="sxs-lookup"><span data-stu-id="9c948-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="9c948-108">Par exemple, considérez le scénario dans lequel une équipe a un référentiel de packages interne pour les builds d’intégration continue d’autres dépendances internes.</span><span class="sxs-lookup"><span data-stu-id="9c948-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="9c948-109">La structure de dossiers d’un projet individuel peut se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="9c948-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="9c948-110">En outre, si la restauration des packages est activée pour la solution, le dossier suivant existera également :</span><span class="sxs-lookup"><span data-stu-id="9c948-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="9c948-111">Pour que le référentiel de packages interne de l’équipe soit disponible pour tous les projets sur lesquels l’équipe travaille, sans qu’il soit disponible pour chaque projet sur l’ordinateur, nous pouvons créer un fichier Nuget.Config et le placer dans le dossier c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="9c948-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="9c948-112">Il n’existe aucun moyen de dénombrer un dossier de packages par projet.</span><span class="sxs-lookup"><span data-stu-id="9c948-112">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="9c948-113">Nous pouvons maintenant voir que la source a été ajoutée en exécutant la commande’sources de nuget.exe 'à partir de n’importe quel dossier sous c:\myteam, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9c948-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Sources de package de la configuration NuGet parente](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="9c948-115">`NuGet.Config` les fichiers sont recherchés dans l’ordre suivant :</span><span class="sxs-lookup"><span data-stu-id="9c948-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="9c948-116">Parcours récursif du dossier du projet vers la racine</span><span class="sxs-lookup"><span data-stu-id="9c948-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="9c948-117">Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="9c948-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="9c948-118">Les configurations sont appliquées dans l' *ordre inverse*, ce qui signifie qu’en fonction du classement ci-dessus, le Nuget.Config global est appliqué en premier, suivi des fichiers Nuget.Config détectés du dossier racine au dossier du projet, suivi de `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="9c948-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="9c948-119">Cela est particulièrement important si vous utilisez l' `<clear/>` élément pour supprimer un ensemble d’éléments de la configuration.</span><span class="sxs-lookup"><span data-stu-id="9c948-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="9c948-120">Spécifier l’emplacement du dossier « Packages »</span><span class="sxs-lookup"><span data-stu-id="9c948-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="9c948-121">Dans le passé, NuGet gérait les packages d’une solution à partir d’un dossier connu « packages » situé sous le dossier racine de la solution.</span><span class="sxs-lookup"><span data-stu-id="9c948-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="9c948-122">Pour les équipes de développement qui possèdent de nombreuses solutions pour lesquelles des packages NuGet sont installés, cela peut entraîner l’installation d’un même package à différents emplacements du système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="9c948-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="9c948-123">NuGet 2,1 fournit un contrôle plus granulaire sur l’emplacement du dossier Packages par le biais de l' `repositoryPath` élément dans le `NuGet.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="9c948-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="9c948-124">En s’appuyant sur l’exemple précédent de prise en charge de Nuget.Config hiérarchique, supposons que nous souhaitons que tous les projets sous C:\myteam\ partagent le même dossier de packages.</span><span class="sxs-lookup"><span data-stu-id="9c948-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="9c948-125">Pour ce faire, ajoutez simplement l’entrée suivante à `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="9c948-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="9c948-126">Dans cet exemple, le `Nuget.Config` fichier partagé spécifie un dossier de packages partagés pour chaque projet créé sous C:\myteam, quelle que soit sa profondeur.</span><span class="sxs-lookup"><span data-stu-id="9c948-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="9c948-127">Notez que si vous avez un dossier Packages existant sous la racine de votre solution, vous devez le supprimer pour que NuGet place les packages dans le nouvel emplacement.</span><span class="sxs-lookup"><span data-stu-id="9c948-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="9c948-128">Prise en charge des bibliothèques portables</span><span class="sxs-lookup"><span data-stu-id="9c948-128">Support for Portable Libraries</span></span>

<span data-ttu-id="9c948-129">Les [bibliothèques portables](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) sont une fonctionnalité introduite pour la première fois avec .net 4, qui vous permet de créer des assemblys qui peuvent fonctionner sans modification sur différentes plateformes Microsoft, des versions de The.NET Framework à Silverlight pour Windows Phone et même la Xbox 360 (à ce stade, NuGet ne prend pas en charge la cible de la bibliothèque portable Xbox).</span><span class="sxs-lookup"><span data-stu-id="9c948-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="9c948-130">En étendant les [conventions de package](../create-packages/supporting-multiple-target-frameworks.md) pour les versions et les profils du Framework, NuGet 2,1 prend désormais en charge les bibliothèques portables en vous permettant de créer des packages qui ont des dossiers d’infrastructure composée et de profil cible `lib` .</span><span class="sxs-lookup"><span data-stu-id="9c948-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="9c948-131">Par exemple, considérez les plateformes cibles disponibles suivantes de la bibliothèque de classes portable.</span><span class="sxs-lookup"><span data-stu-id="9c948-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Boîte de dialogue de création de bibliothèque portable](./media/releasenotes-21-plib.png)

<span data-ttu-id="9c948-133">Une fois la bibliothèque générée et la commande `nuget.exe pack MyPortableProject.csproj` exécutée, la nouvelle structure de dossiers de package de bibliothèque portable peut être consultée en examinant le contenu du package NuGet généré.</span><span class="sxs-lookup"><span data-stu-id="9c948-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Disposition de package de bibliothèque portable](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="9c948-135">Comme vous pouvez le voir, la Convention de nom de dossier de la bibliothèque portable suit le modèle « portable-{Framework 1} + {Framework n} », où les identificateurs de Framework suivent le [nom et les conventions de version](../reference/target-frameworks.md)existants de l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="9c948-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="9c948-136">Une exception aux conventions de nom et de version se trouve dans l’identificateur de Framework utilisé pour Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="9c948-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="9c948-137">Ce moniker doit utiliser le nom de Framework’WP' (WP7, wp71 ou wp8).</span><span class="sxs-lookup"><span data-stu-id="9c948-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="9c948-138">L’utilisation de’Silverlight-WP7 ', par exemple, génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="9c948-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="9c948-139">Lors de l’installation du package créé à partir de cette structure de dossiers, NuGet peut désormais appliquer ses règles d’infrastructure et de profil à plusieurs cibles, comme indiqué dans le nom du dossier.</span><span class="sxs-lookup"><span data-stu-id="9c948-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="9c948-140">Derrière les règles de correspondance de NuGet est le principe que les cibles « plus spécifiques » ont priorité sur les « moins spécifiques ».</span><span class="sxs-lookup"><span data-stu-id="9c948-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="9c948-141">Cela signifie que les monikers ciblant une plateforme spécifique sont toujours préférés aux ordinateurs portables s’ils sont tous les deux compatibles avec un projet.</span><span class="sxs-lookup"><span data-stu-id="9c948-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="9c948-142">En outre, si plusieurs cibles portables sont compatibles avec un projet, NuGet préfère celui où l’ensemble de plates-formes prises en charge est « le plus proche » du projet référençant le package.</span><span class="sxs-lookup"><span data-stu-id="9c948-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="9c948-143">Ciblage de projets Windows 8 et Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="9c948-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="9c948-144">Outre l’ajout de la prise en charge du ciblage des projets de bibliothèque portables, NuGet 2,1 fournit de nouveaux monikers de Framework pour les projets Windows 8 Store et Windows Phone 8, ainsi que certains nouveaux monikers généraux pour les projets Windows Store et Windows Phone qui seront plus faciles à gérer sur les futures versions des plateformes respectives.</span><span class="sxs-lookup"><span data-stu-id="9c948-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="9c948-145">Pour les applications du Windows Store de Windows 8, les identificateurs se présentent comme suit :</span><span class="sxs-lookup"><span data-stu-id="9c948-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="9c948-146">NuGet 2,0 et versions antérieures</span><span class="sxs-lookup"><span data-stu-id="9c948-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="9c948-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="9c948-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="9c948-148">winRT45,. NETCore45</span><span class="sxs-lookup"><span data-stu-id="9c948-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="9c948-149">Windows, Windows8, Win, WIN8</span><span class="sxs-lookup"><span data-stu-id="9c948-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="9c948-150">Pour les projets Windows Phone, les identificateurs se présentent comme suit :</span><span class="sxs-lookup"><span data-stu-id="9c948-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="9c948-151">SE téléphone</span><span class="sxs-lookup"><span data-stu-id="9c948-151">Phone OS</span></span> | <span data-ttu-id="9c948-152">NuGet 2,0 et versions antérieures</span><span class="sxs-lookup"><span data-stu-id="9c948-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="9c948-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="9c948-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c948-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="9c948-154">Windows Phone 7</span></span> | <span data-ttu-id="9c948-155">silverlight3-WP</span><span class="sxs-lookup"><span data-stu-id="9c948-155">silverlight3-wp</span></span> | <span data-ttu-id="9c948-156">WP, WP7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="9c948-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="9c948-157">Windows Phone 7,5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="9c948-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="9c948-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="9c948-158">silverlight4-wp71</span></span> | <span data-ttu-id="9c948-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="9c948-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="9c948-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="9c948-160">Windows Phone 8</span></span> | <span data-ttu-id="9c948-161">(non pris en charge)</span><span class="sxs-lookup"><span data-stu-id="9c948-161">(not supported)</span></span> | <span data-ttu-id="9c948-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="9c948-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="9c948-163">Dans toutes les modifications apportées ci-dessus, les anciens noms de Framework seront toujours entièrement pris en charge par NuGet 2,1.</span><span class="sxs-lookup"><span data-stu-id="9c948-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="9c948-164">À l’avenir, les nouveaux noms doivent être utilisés, car ils seront plus stables dans les futures versions des plateformes respectives.</span><span class="sxs-lookup"><span data-stu-id="9c948-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="9c948-165">Toutefois, les nouveaux noms ne seront *pas* pris en charge dans les versions de NuGet antérieures à 2,1. par conséquent, planifiez en conséquence le moment où le basculement doit être effectué.</span><span class="sxs-lookup"><span data-stu-id="9c948-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="9c948-166">Recherche améliorée dans la boîte de dialogue du gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="9c948-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="9c948-167">Au cours des différentes itérations, des modifications ont été introduites dans la galerie NuGet, ce qui a amélioré la vitesse et la pertinence des recherches dans les packages.</span><span class="sxs-lookup"><span data-stu-id="9c948-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="9c948-168">Toutefois, ces améliorations étaient limitées au site Web nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9c948-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="9c948-169">NuGet 2,1 rend l’expérience de recherche améliorée disponible par le biais de la boîte de dialogue Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="9c948-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="9c948-170">Par exemple, imaginez que vous souhaitiez trouver le package de la version préliminaire de Windows Azure Caching.</span><span class="sxs-lookup"><span data-stu-id="9c948-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="9c948-171">Une requête de recherche raisonnable pour ce package peut être « Azure cache ».</span><span class="sxs-lookup"><span data-stu-id="9c948-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="9c948-172">Dans les versions précédentes de la boîte de dialogue du gestionnaire de package, le package souhaité ne serait même pas listé sur la première page des résultats.</span><span class="sxs-lookup"><span data-stu-id="9c948-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="9c948-173">Toutefois, dans NuGet 2,1, le package souhaité s’affiche désormais en haut des résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="9c948-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Recherche de boîte de dialogue du gestionnaire de package](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="9c948-175">Forcer la mise à jour du package</span><span class="sxs-lookup"><span data-stu-id="9c948-175">Force Package Update</span></span>

<span data-ttu-id="9c948-176">Avant NuGet 2,1, NuGet ignorerait la mise à jour d’un package alors qu’il n’existait pas de numéro de version élevé.</span><span class="sxs-lookup"><span data-stu-id="9c948-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="9c948-177">Cela a introduit un frottement pour certains scénarios, en particulier dans le cas de scénarios de génération ou d’élément de configuration où l’équipe ne souhaitait pas incrémenter le numéro de version de package avec chaque Build.</span><span class="sxs-lookup"><span data-stu-id="9c948-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="9c948-178">Le comportement souhaité consistait à forcer une mise à jour, quelle que soit la valeur.</span><span class="sxs-lookup"><span data-stu-id="9c948-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="9c948-179">NuGet 2,1 traite ceci avec l’indicateur « REINSTALL ».</span><span class="sxs-lookup"><span data-stu-id="9c948-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="9c948-180">Par exemple, les versions précédentes de NuGet se traduiraient par les éléments suivants lors de la tentative de mise à jour d’un package qui ne disposait pas d’une version plus récente du package :</span><span class="sxs-lookup"><span data-stu-id="9c948-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="9c948-181">Avec l’indicateur de réinstallation, le package est mis à jour, qu’il y ait ou non une version plus récente.</span><span class="sxs-lookup"><span data-stu-id="9c948-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="9c948-182">Un autre scénario dans lequel l’indicateur de réinstallation s’avère bénéfique est le reciblage de Framework.</span><span class="sxs-lookup"><span data-stu-id="9c948-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="9c948-183">Lors de la modification de la version cible du .NET Framework d’un projet (par exemple, de .NET 4 vers .NET 4,5), Update-Package-REINSTALL peut mettre à jour les références aux assemblys corrects pour tous les packages NuGet installés dans le projet.</span><span class="sxs-lookup"><span data-stu-id="9c948-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="9c948-184">Modifier des sources de package dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9c948-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="9c948-185">Dans les versions précédentes de NuGet, la mise à jour d’une source de package à partir de la boîte de dialogue Options de Visual Studio nécessitait de supprimer et rajouter la source du package.</span><span class="sxs-lookup"><span data-stu-id="9c948-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="9c948-186">NuGet 2,1 améliore ce flux de travail en prenant en charge la mise à jour en tant que fonction de première classe de l’interface utilisateur de configuration.</span><span class="sxs-lookup"><span data-stu-id="9c948-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Boîte de dialogue de configuration du gestionnaire de package](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="9c948-188">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="9c948-188">Bug Fixes</span></span>

<span data-ttu-id="9c948-189">NuGet 2,1 comprend de nombreux correctifs de bogues.</span><span class="sxs-lookup"><span data-stu-id="9c948-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="9c948-190">Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2,0, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="9c948-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
