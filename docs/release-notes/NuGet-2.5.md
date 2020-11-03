---
title: Notes de publication de NuGet 2,5
description: Notes de publication de NuGet 2,5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237079"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="d1c93-103">Notes de publication de NuGet 2,5</span><span class="sxs-lookup"><span data-stu-id="d1c93-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="d1c93-104">Notes de publication de [NuGet 2.2.1](../release-notes/nuget-2.2.1.md)  |  [Notes de publication de NuGet 2,6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="d1c93-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="d1c93-105">NuGet 2,5 a été publié le 25 avril 2013.</span><span class="sxs-lookup"><span data-stu-id="d1c93-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="d1c93-106">Cette version était tellement importante, nous avons pensé à ignorer les versions 2,3 et 2,4 !</span><span class="sxs-lookup"><span data-stu-id="d1c93-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="d1c93-107">À ce jour, il s’agit de la plus grande version de NuGet, avec plus de [160 éléments de travail](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) dans la version.</span><span class="sxs-lookup"><span data-stu-id="d1c93-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="d1c93-108">Remerciements</span><span class="sxs-lookup"><span data-stu-id="d1c93-108">Acknowledgements</span></span>

<span data-ttu-id="d1c93-109">Nous aimerions remercier les contributeurs externes suivants pour leurs contributions significatives à NuGet 2,5 :</span><span class="sxs-lookup"><span data-stu-id="d1c93-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="d1c93-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ( [@dsplaisted](https://twitter.com/dsplaisted) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="d1c93-111">[#2847](https://nuget.codeplex.com/workitem/2847) -ajoutez monoandroid, unitouch et MonoMac à la liste des identificateurs de Framework cible connus.</span><span class="sxs-lookup"><span data-stu-id="d1c93-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="d1c93-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ( [@knocte](https://twitter.com/knocte) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="d1c93-113">[#2865](https://nuget.codeplex.com/workitem/2865) -corriger l’orthographe de `NuGet.targets` pour un système d’exploitation qui respecte la casse</span><span class="sxs-lookup"><span data-stu-id="d1c93-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="d1c93-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="d1c93-115">Rendez la génération de la solution sur mono.</span><span class="sxs-lookup"><span data-stu-id="d1c93-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="d1c93-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ( [@atheken](https://twitter.com/atheken) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="d1c93-117">Corriger les tests unitaires qui échouent sur mono.</span><span class="sxs-lookup"><span data-stu-id="d1c93-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="d1c93-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ( [@OliIsCool](https://twitter.com/oliiscool) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="d1c93-119">la commande [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack ne propage pas les propriétés à MSBuild</span><span class="sxs-lookup"><span data-stu-id="d1c93-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="d1c93-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ( [@bajtos](https://twitter.com/bajtos) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="d1c93-121">Code de gestion XML modifié par [#1511](https://nuget.codeplex.com/workitem/1511) pour préserver la mise en forme.</span><span class="sxs-lookup"><span data-stu-id="d1c93-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="d1c93-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="d1c93-123">Ajout de mots reconnus au dictionnaire personnalisé pour permettre à Build. cmd de s’effectuer correctement.</span><span class="sxs-lookup"><span data-stu-id="d1c93-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="d1c93-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="d1c93-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="d1c93-125">Corriger les tests unitaires lors de l’exécution dans les</span><span class="sxs-lookup"><span data-stu-id="d1c93-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="d1c93-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="d1c93-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="d1c93-127">Interface extraite de PackageService</span><span class="sxs-lookup"><span data-stu-id="d1c93-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="d1c93-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ( [@brugidou](https://twitter.com/brugidou) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="d1c93-129">[#936](https://nuget.codeplex.com/workitem/936) : gère les dépendances de projet lors de la compression</span><span class="sxs-lookup"><span data-stu-id="d1c93-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="d1c93-130">[Xavier DECHARGEUR](https://www.codeplex.com/site/users/view/XavierDecoster) ( [@XavierDecoster](https://twitter.com/xavierdecoster) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="d1c93-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -prendre en charge le mot de passe en texte clair lors du stockage des informations d’identification de la source du package dans les fichiers NuGet. cofig</span><span class="sxs-lookup"><span data-stu-id="d1c93-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="d1c93-132">[James Equipment](http://www.codeplex.com/site/users/view/jmanning) ( [@manningj](https://twitter.com/manningj) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="d1c93-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -corriger la description de l’aide Get-Package</span><span class="sxs-lookup"><span data-stu-id="d1c93-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="d1c93-134">Nous apprécions également les personnes suivantes pour trouver des bogues avec NuGet 2,5 Beta/RC qui ont été approuvés et résolus avant la version finale :</span><span class="sxs-lookup"><span data-stu-id="d1c93-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="d1c93-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ( [@CodeChief](https://twitter.com/codechief) )</span><span class="sxs-lookup"><span data-stu-id="d1c93-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="d1c93-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest endommagé avec les dernières builds NuGet 2,4 et 2,5</span><span class="sxs-lookup"><span data-stu-id="d1c93-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="d1c93-137">Fonctionnalités notables dans la version</span><span class="sxs-lookup"><span data-stu-id="d1c93-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="d1c93-138">Autoriser les utilisateurs à remplacer les fichiers de contenu qui existent déjà</span><span class="sxs-lookup"><span data-stu-id="d1c93-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="d1c93-139">L’une des fonctionnalités les plus demandées de tout le temps est la possibilité de remplacer les fichiers de contenu qui existent déjà sur le disque lorsqu’ils sont inclus dans un package NuGet.</span><span class="sxs-lookup"><span data-stu-id="d1c93-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="d1c93-140">À compter de NuGet 2,5, ces conflits sont identifiés et vous êtes invité à remplacer les fichiers, tandis que ces fichiers étaient toujours ignorés.</span><span class="sxs-lookup"><span data-stu-id="d1c93-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Remplacer les fichiers de contenu](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="d1c93-142">« nuget.exe Update » et « Install-Package » disposent désormais d’une nouvelle option « -FileConflictAction » pour définir des valeurs par défaut pour les scénarios de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d1c93-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="d1c93-143">Définissez une action par défaut lorsqu’un fichier d’un package existe déjà dans le projet cible.</span><span class="sxs-lookup"><span data-stu-id="d1c93-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="d1c93-144">Définissez sur « overwrite » pour toujours remplacer les fichiers.</span><span class="sxs-lookup"><span data-stu-id="d1c93-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="d1c93-145">Définissez sur « Ignorer » pour ignorer les fichiers.</span><span class="sxs-lookup"><span data-stu-id="d1c93-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="d1c93-146">S’il n’est pas spécifié, il demande à chaque fichier en conflit.</span><span class="sxs-lookup"><span data-stu-id="d1c93-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="d1c93-147">Importation automatique de cibles et de fichiers props MSBuild</span><span class="sxs-lookup"><span data-stu-id="d1c93-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="d1c93-148">Un nouveau dossier conventionnel a été créé au niveau supérieur du package NuGet.</span><span class="sxs-lookup"><span data-stu-id="d1c93-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="d1c93-149">En tant qu’homologue de `\lib` , `\content` et `\tools` , vous pouvez désormais inclure un `\build` dossier dans votre package.</span><span class="sxs-lookup"><span data-stu-id="d1c93-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="d1c93-150">Dans ce dossier, vous pouvez placer deux fichiers avec des noms fixes, `{packageid}.targets` ou `{packageid}.props` .</span><span class="sxs-lookup"><span data-stu-id="d1c93-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="d1c93-151">Ces deux fichiers peuvent être directement sous `build` ou sous des dossiers spécifiques à l’infrastructure, tout comme les autres dossiers.</span><span class="sxs-lookup"><span data-stu-id="d1c93-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="d1c93-152">La règle de sélection du dossier Framework le mieux adapté est exactement la même que celle de celles-ci.</span><span class="sxs-lookup"><span data-stu-id="d1c93-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="d1c93-153">Quand NuGet installe un package avec des fichiers \Build, il ajoute un `<Import>` élément MSBuild dans le fichier projet pointant vers `.targets` les `.props` fichiers et.</span><span class="sxs-lookup"><span data-stu-id="d1c93-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="d1c93-154">Le `.props` fichier est ajouté en haut, tandis que le `.targets` fichier est ajouté en bas.</span><span class="sxs-lookup"><span data-stu-id="d1c93-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="d1c93-155">Spécifier différentes références par plateforme à l’aide de l' `<References/>` élément</span><span class="sxs-lookup"><span data-stu-id="d1c93-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="d1c93-156">Avant le 2,5, dans le `.nuspec` fichier, l’utilisateur ne peut spécifier que les fichiers de référence, à ajouter pour tous les frameworks.</span><span class="sxs-lookup"><span data-stu-id="d1c93-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="d1c93-157">Désormais, avec cette nouvelle fonctionnalité dans 2,5, l’utilisateur peut créer l' `<reference/>` élément pour chacune des plateformes prises en charge, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1c93-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="d1c93-158">Voici le déroulement de la manière dont NuGet ajoute des références aux projets basés sur le `.nuspec` fichier :</span><span class="sxs-lookup"><span data-stu-id="d1c93-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="d1c93-159">Recherchez le `lib` dossier qui convient à la version cible de .NET Framework et obtenez la liste des assemblys de ce dossier</span><span class="sxs-lookup"><span data-stu-id="d1c93-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="d1c93-160">Recherchez séparément le groupe de références qui est approprié pour la version cible de .NET Framework et obtenez la liste des assemblys de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="d1c93-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="d1c93-161">Le groupe de référence sans Framework cible spécifié est le groupe de secours.</span><span class="sxs-lookup"><span data-stu-id="d1c93-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="d1c93-162">Recherchez l’intersection des deux listes et utilisez-la comme référence à ajouter</span><span class="sxs-lookup"><span data-stu-id="d1c93-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="d1c93-163">Cette nouvelle fonctionnalité permet aux créateurs de packages d’utiliser la fonctionnalité de références pour appliquer des sous-ensembles d’assemblys à différents frameworks lorsqu’ils doivent autrement transporter des assemblys en double dans plusieurs `lib` dossiers.</span><span class="sxs-lookup"><span data-stu-id="d1c93-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="d1c93-164">Remarque : vous devez actuellement utiliser nuget.exe Pack pour utiliser cette fonctionnalité. L’Explorateur de package NuGet ne le prend pas encore en charge.</span><span class="sxs-lookup"><span data-stu-id="d1c93-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="d1c93-165">Bouton mettre à jour tout pour autoriser la mise à jour de tous les packages à la fois</span><span class="sxs-lookup"><span data-stu-id="d1c93-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="d1c93-166">Un grand nombre d’entre vous en savent plus sur l’applet de commande PowerShell « Update-Package » pour mettre à jour tous vos packages. Il existe désormais un moyen simple de le faire via l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d1c93-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="d1c93-167">Pour essayer cette fonctionnalité, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d1c93-167">To try this feature out:</span></span>

1. <span data-ttu-id="d1c93-168">Créer une application ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="d1c93-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="d1c93-169">Lancer la boîte de dialogue « gérer les packages NuGet »</span><span class="sxs-lookup"><span data-stu-id="d1c93-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="d1c93-170">Sélectionner « mises à jour »</span><span class="sxs-lookup"><span data-stu-id="d1c93-170">Select 'Updates'</span></span>
1. <span data-ttu-id="d1c93-171">Cliquez sur le bouton « mettre à jour tout »</span><span class="sxs-lookup"><span data-stu-id="d1c93-171">Click the 'Update All' button</span></span>

![Bouton tout mettre à jour dans la boîte de dialogue](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="d1c93-173">Prise en charge améliorée de la référence de projet pour nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="d1c93-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="d1c93-174">Désormais nuget.exe commande Pack traite les projets référencés avec les règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="d1c93-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="d1c93-175">Si le projet référencé a le `.nuspec` fichier correspondant, par exemple s’il existe un fichier appelé `proj1.nuspec` dans le même dossier que `proj1.csproj` , ce projet est ajouté en tant que dépendance au package, à l’aide de l’ID et de la version lus à partir du `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="d1c93-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="d1c93-176">Dans le cas contraire, les fichiers du projet référencé sont regroupés dans le package.</span><span class="sxs-lookup"><span data-stu-id="d1c93-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="d1c93-177">Les projets référencés par ce projet seront ensuite traités à l’aide des règles SAMES de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="d1c93-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="d1c93-178">Tous les fichiers DLL, `.pdb` et `.exe` sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="d1c93-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="d1c93-179">Tous les autres fichiers de contenu sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="d1c93-179">All other content files are added.</span></span>
1. <span data-ttu-id="d1c93-180">Toutes les dépendances sont fusionnées.</span><span class="sxs-lookup"><span data-stu-id="d1c93-180">All dependencies are merged.</span></span>

<span data-ttu-id="d1c93-181">Cela permet à un projet référencé d’être traité comme une dépendance s’il existe un `.nuspec` fichier, sinon il devient une partie du package.</span><span class="sxs-lookup"><span data-stu-id="d1c93-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="d1c93-182">Plus de détails ici : [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="d1c93-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="d1c93-183">Ajouter une propriété’version minimale de NuGet’aux packages</span><span class="sxs-lookup"><span data-stu-id="d1c93-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="d1c93-184">Un nouvel attribut de métadonnées appelé « minClientVersion » peut maintenant indiquer la version minimale du client NuGet requise pour utiliser un package.</span><span class="sxs-lookup"><span data-stu-id="d1c93-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="d1c93-185">Cette fonctionnalité permet à l’auteur du package de spécifier qu’un package ne fonctionnera qu’après une version particulière de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d1c93-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="d1c93-186">À mesure que de nouvelles `.nuspec` fonctionnalités sont ajoutées après NuGet 2,5, les packages peuvent revendiquer une version minimale de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d1c93-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="d1c93-187">Si NuGet 2,5 est installé sur l’utilisateur et qu’un package est identifié comme nécessitant 2,6, des signaux visuels seront fournis à l’utilisateur pour indiquer que le package ne pourra pas être installé.</span><span class="sxs-lookup"><span data-stu-id="d1c93-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="d1c93-188">L’utilisateur sera ensuite guidé pour mettre à jour sa version de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d1c93-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="d1c93-189">Cela permet d’améliorer l’expérience existante où les packages commencent à s’installer, mais qui échouent, indiquant qu’une version de schéma non reconnue a été identifiée.</span><span class="sxs-lookup"><span data-stu-id="d1c93-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="d1c93-190">Les dépendances ne sont plus mises à jour inutilement lors de l’installation du package</span><span class="sxs-lookup"><span data-stu-id="d1c93-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="d1c93-191">Avant la version antérieure de NuGet 2,5, quand un package était installé et dépendait d’un package déjà installé dans le projet, la dépendance serait mise à jour dans le cadre de la nouvelle installation, même si la version existante satisfaisait la dépendance.</span><span class="sxs-lookup"><span data-stu-id="d1c93-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="d1c93-192">À compter de NuGet 2,5, si une version de dépendance est déjà satisfaite, la dépendance ne sera pas mise à jour lors des autres installations de package.</span><span class="sxs-lookup"><span data-stu-id="d1c93-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="d1c93-193">**Le scénario :**</span><span class="sxs-lookup"><span data-stu-id="d1c93-193">**The scenario:**</span></span>

1. <span data-ttu-id="d1c93-194">Le référentiel source contient le package B avec les versions 1.0.0 et 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="d1c93-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="d1c93-195">Il contient également le package A qui a une dépendance sur B (>= 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="d1c93-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="d1c93-196">Supposons que le projet actuel a déjà le package B version 1.0.0 installé.</span><span class="sxs-lookup"><span data-stu-id="d1c93-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="d1c93-197">Vous souhaitez maintenant installer le package A.</span><span class="sxs-lookup"><span data-stu-id="d1c93-197">Now you want to install package A.</span></span>

<span data-ttu-id="d1c93-198">**Dans NuGet 2,2 et les versions antérieures :**</span><span class="sxs-lookup"><span data-stu-id="d1c93-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="d1c93-199">Lors de l’installation du package A, NuGet met automatiquement à jour B vers 1.0.2, même si la version existante 1.0.0 satisfait déjà à la contrainte de version de dépendance, qui est >= 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d1c93-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="d1c93-200">**Dans NuGet 2,5 et versions ultérieures :**</span><span class="sxs-lookup"><span data-stu-id="d1c93-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="d1c93-201">NuGet ne mettra plus à jour B, car il détecte que la version existante 1.0.0 est conforme à la contrainte de version de dépendance.</span><span class="sxs-lookup"><span data-stu-id="d1c93-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="d1c93-202">Pour plus d’informations sur cette modification, consultez l' [élément de travail](http://nuget.codeplex.com/workitem/1681) détaillé ainsi que le [thread de discussion](http://nuget.codeplex.com/discussions/436712)associé.</span><span class="sxs-lookup"><span data-stu-id="d1c93-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="d1c93-203">nuget.exe génère des requêtes http avec un niveau de détail détaillé</span><span class="sxs-lookup"><span data-stu-id="d1c93-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="d1c93-204">Si vous dépannez nuget.exe ou que vous voulez simplement savoir quelles sont les requêtes HTTP effectuées au cours des opérations, le commutateur « -verbosity detailed » génère à présent toutes les requêtes HTTP effectuées.</span><span class="sxs-lookup"><span data-stu-id="d1c93-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Sortie HTTP de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="d1c93-206">nuget.exe Push prend désormais en charge les sources UNC et de dossier</span><span class="sxs-lookup"><span data-stu-id="d1c93-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="d1c93-207">Avant NuGet 2,5, si vous tentez d’exécuter « nuget.exe push » dans une source de package en fonction d’un chemin UNC ou d’un dossier local, l’envoi échoue.</span><span class="sxs-lookup"><span data-stu-id="d1c93-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="d1c93-208">Avec la fonctionnalité de configuration hiérarchique ajoutée récemment, il était courant pour nuget.exe de devoir cibler une source UNC/dossier ou une galerie NuGet basée sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="d1c93-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="d1c93-209">À compter de NuGet 2,5, si nuget.exe identifie une source UNC/de dossier, il effectue la copie de fichiers vers la source.</span><span class="sxs-lookup"><span data-stu-id="d1c93-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="d1c93-210">La commande suivante fonctionne désormais :</span><span class="sxs-lookup"><span data-stu-id="d1c93-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="d1c93-211">nuget.exe prend en charge les fichiers de configuration spécifiés explicitement</span><span class="sxs-lookup"><span data-stu-id="d1c93-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="d1c93-212">nuget.exe commandes qui accèdent à la configuration (toutes sauf « spec » et « Pack ») prennent désormais en charge une nouvelle option « -ConfigFile », qui force l’utilisation d’un fichier de configuration spécifique à la place du fichier de configuration par défaut à l’adresse% AppData% \nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="d1c93-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="d1c93-213">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d1c93-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="d1c93-214">Prise en charge des projets natifs</span><span class="sxs-lookup"><span data-stu-id="d1c93-214">Support for Native projects</span></span>

<span data-ttu-id="d1c93-215">Avec NuGet 2,5, les outils NuGet sont désormais disponibles pour les projets natifs dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1c93-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="d1c93-216">Nous pensons que la plupart des packages natifs utiliseront la fonctionnalité importations MSBuild ci-dessus, à l’aide d’un outil créé par le [projet CoApp](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="d1c93-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="d1c93-217">Pour plus d’informations, consultez les [Détails de l’outil](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) sur le site Web coapp.org.</span><span class="sxs-lookup"><span data-stu-id="d1c93-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="d1c93-218">Le nom du Framework cible « native » est introduit pour que les packages incluent les fichiers dans \Build, \Content et \Tools lorsque le package est installé dans un projet natif.</span><span class="sxs-lookup"><span data-stu-id="d1c93-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="d1c93-219">Le \` dossier lib n’est pas utilisé pour les projets natifs.</span><span class="sxs-lookup"><span data-stu-id="d1c93-219">The \`lib\` folder is not used for native projects.</span></span>
