---
title: Notes de publication NuGet 2.5 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c193f1e3-d114-427f-9425-9930cc8e4db3
description: "Notes de version de NuGet 2.5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 2.5 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8d3bebbbe550645fcffad078538134427103cf98
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="f3880-104">Notes de publication NuGet 2.5</span><span class="sxs-lookup"><span data-stu-id="f3880-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="f3880-105">[Notes de publication NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Notes de publication](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="f3880-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="f3880-106">NuGet 2.5 a été publiée le 25 avril 2013.</span><span class="sxs-lookup"><span data-stu-id="f3880-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="f3880-107">Cette version a été tellement volumineux, il nous semble tenus à ignorer les versions 2.3 et 2.4 !</span><span class="sxs-lookup"><span data-stu-id="f3880-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="f3880-108">La date de fin, il s’agit la plus grand version nous avons eu de NuGet, avec sur [160 des éléments de travail](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) dans la version.</span><span class="sxs-lookup"><span data-stu-id="f3880-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="f3880-109">Remerciements</span><span class="sxs-lookup"><span data-stu-id="f3880-109">Acknowledgements</span></span>

<span data-ttu-id="f3880-110">Nous aimerions remercier les collaborateurs externes suivantes pour leur contribution significative à NuGet 2.5 :</span><span class="sxs-lookup"><span data-stu-id="f3880-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="f3880-111">[Michel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="f3880-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="f3880-112">[#2847](https://nuget.codeplex.com/workitem/2847) -ajouter des MonoAndroid, MonoTouch et MonoMac à la liste des identificateurs de framework cible connus.</span><span class="sxs-lookup"><span data-stu-id="f3880-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="f3880-113">[Aragoneses de g. Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="f3880-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="f3880-114">[#2865](https://nuget.codeplex.com/workitem/2865) -Corrigez l’orthographe du `NuGet.targets` pour un système d’exploitation qui respecte la casse</span><span class="sxs-lookup"><span data-stu-id="f3880-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="f3880-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="f3880-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="f3880-116">Vérifiez la solution build sur Mono.</span><span class="sxs-lookup"><span data-stu-id="f3880-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="f3880-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="f3880-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="f3880-118">Corrigez les tests unitaires échoue sur Mono.</span><span class="sxs-lookup"><span data-stu-id="f3880-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="f3880-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="f3880-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="f3880-120">[#2920](https://nuget.codeplex.com/workitem/2920) -commande pack de nuget.exe ne propage pas de propriétés MSBuild</span><span class="sxs-lookup"><span data-stu-id="f3880-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="f3880-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="f3880-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="f3880-122">[#1511](https://nuget.codeplex.com/workitem/1511) - XML modifié la gestion du code pour conserver la mise en forme.</span><span class="sxs-lookup"><span data-stu-id="f3880-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="f3880-123">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="f3880-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="f3880-124">Mots reconnus ajoutés au dictionnaire personnalisé permettant de build.cmd réussisse.</span><span class="sxs-lookup"><span data-stu-id="f3880-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="f3880-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="f3880-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="f3880-126">Corrigez les tests unitaires lors de l’exécution dans Visual Studio localisée.</span><span class="sxs-lookup"><span data-stu-id="f3880-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="f3880-127">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="f3880-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="f3880-128">Interface extrait à partir de PackageService</span><span class="sxs-lookup"><span data-stu-id="f3880-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="f3880-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="f3880-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="f3880-130">[#936](https://nuget.codeplex.com/workitem/936) -gérer les dépendances du projet lors de la livraison</span><span class="sxs-lookup"><span data-stu-id="f3880-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="f3880-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="f3880-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="f3880-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -prise en charge clair texte mot de passe lorsque vous stockez des informations d’identification de source de package dans les fichiers de nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="f3880-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="f3880-133">[James effectifs](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="f3880-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="f3880-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -description d’aide de Get-Package corriger</span><span class="sxs-lookup"><span data-stu-id="f3880-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="f3880-135">Nous apprécions également aux personnes suivantes pour la recherche de bogues avec NuGet 2.5 bêta/RC qui ont été approuvées et résolus avant la version finale :</span><span class="sxs-lookup"><span data-stu-id="f3880-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="f3880-136">[Durée totale de Tony](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="f3880-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="f3880-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest rompue avec la dernière NuGet 2.4 et 2.5 versions</span><span class="sxs-lookup"><span data-stu-id="f3880-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

# <a name="notable-features-in-the-release"></a><span data-ttu-id="f3880-138">Fonctionnalités notables dans la version</span><span class="sxs-lookup"><span data-stu-id="f3880-138">Notable features in the release</span></span>

## <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="f3880-139">Autoriser les utilisateurs à remplacer les fichiers de contenu qui existent déjà</span><span class="sxs-lookup"><span data-stu-id="f3880-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="f3880-140">Une des fonctionnalités plus demandées du temps a été la possibilité de remplacer les fichiers de contenu qui existent déjà sur le disque lorsque inclus dans un package NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3880-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="f3880-141">À compter de NuGet 2.5, ces conflits sont identifiés et vous devrez remplacer les fichiers, alors que précédemment ces fichiers toujours ignorés.</span><span class="sxs-lookup"><span data-stu-id="f3880-141">Starting with NuGet 2.5, these conflicts are identified and you will be prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Remplacer les fichiers de contenu](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="f3880-143">« nuget.exe mise à jour » et « Install-Package' maintenant ont tous deux une nouvelle option '-FileConflictAction' pour définir une valeur par défaut pour les scénarios de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="f3880-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="f3880-144">Définir une action par défaut lorsqu’un fichier à partir d’un package existe déjà dans le projet cible.</span><span class="sxs-lookup"><span data-stu-id="f3880-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="f3880-145">Pour remplacer les fichiers toujours la valeur « Remplacer ».</span><span class="sxs-lookup"><span data-stu-id="f3880-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="f3880-146">Défini sur « Ignorer » pour ignorer les fichiers.</span><span class="sxs-lookup"><span data-stu-id="f3880-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="f3880-147">Si non spécifié, il invite pour chaque fichier en conflit.</span><span class="sxs-lookup"><span data-stu-id="f3880-147">If not specified, it will prompt for each conflicting file.</span></span>

## <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="f3880-148">Importation automatique de MSBuild cibles et des fichiers</span><span class="sxs-lookup"><span data-stu-id="f3880-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="f3880-149">Un nouveau dossier classique a été créé au niveau supérieur du package NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3880-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="f3880-150">En tant qu’homologue `\lib`, `\content`, et `\tools`, vous pouvez maintenant inclure un `\build` dossier dans votre package.</span><span class="sxs-lookup"><span data-stu-id="f3880-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="f3880-151">Sous ce dossier, vous pouvez placer les deux fichiers portant des noms fixes, `{packageid}.targets` ou `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="f3880-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="f3880-152">Ces deux fichiers peuvent être directement sous `build` ou dans des dossiers spécifiques à l’infrastructure tout comme les autres dossiers.</span><span class="sxs-lookup"><span data-stu-id="f3880-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="f3880-153">La règle pour le dossier framework mieux mise en correspondance de prélèvement est exactement le même que dans ceux.</span><span class="sxs-lookup"><span data-stu-id="f3880-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="f3880-154">Lorsque NuGet installe un package avec les fichiers \build, il ajoute un MSBuild `<Import>` élément dans le fichier projet pointant vers le `.targets` et `.props` fichiers.</span><span class="sxs-lookup"><span data-stu-id="f3880-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="f3880-155">Le `.props` fichier est ajouté en haut, tandis que le `.targets` fichier est ajouté à la fin.</span><span class="sxs-lookup"><span data-stu-id="f3880-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

## <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="f3880-156">Spécifier différentes références par à l’aide de la plateforme `<References/>` élément</span><span class="sxs-lookup"><span data-stu-id="f3880-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="f3880-157">Avant de 2.5, dans `.nuspec` fichier, utilisateur peut uniquement spécifier les fichiers de référence, à ajouter pour tous les framework.</span><span class="sxs-lookup"><span data-stu-id="f3880-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="f3880-158">Grâce à cette nouvelle fonctionnalité dans 2.5, peut créer un utilisateur à présent le `<reference/>` élément pour chaque de la plateforme prise en charge, par exemple :</span><span class="sxs-lookup"><span data-stu-id="f3880-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="f3880-159">Voici le flux pour comment NuGet ajoute des références à des projets basés sur le `.nuspec` fichier :</span><span class="sxs-lookup"><span data-stu-id="f3880-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="f3880-160">Rechercher les `lib` dossier qui est appropriée pour le framework cible et d’obtenir la liste des assemblys de ce dossier</span><span class="sxs-lookup"><span data-stu-id="f3880-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="f3880-161">Séparément de trouver le groupe de références qui convient pour le framework cible et obtenir la liste des assemblys à partir de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="f3880-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="f3880-162">Groupe de référence sans infrastructure cible spécifié est le groupe de secours.</span><span class="sxs-lookup"><span data-stu-id="f3880-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="f3880-163">Recherche l’intersection des deux listes et l’utiliser comme les références à ajouter</span><span class="sxs-lookup"><span data-stu-id="f3880-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="f3880-164">Cette nouvelle fonctionnalité permet aux auteurs de package à utiliser la fonctionnalité de références aux sous-ensembles d’assemblys à différentes infrastructures lorsqu’ils ont besoin dans le cas contraire transporter des assemblys en double dans plusieurs `lib` dossiers.</span><span class="sxs-lookup"><span data-stu-id="f3880-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="f3880-165">Remarque : vous devez actuellement utiliser pack de nuget.exe pour utiliser cette fonctionnalité ; Explorateur de Package NuGet ne pas encore en charge.</span><span class="sxs-lookup"><span data-stu-id="f3880-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

## <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="f3880-166">Bouton tout pour permettre la mise à jour de tous les packages à la fois de mettre à jour</span><span class="sxs-lookup"><span data-stu-id="f3880-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="f3880-167">Beaucoup d'entre vous savent sur l’applet de commande PowerShell de « Mise à jour de Package » pour mettre à jour tous vos packages ; Il existe désormais un moyen simple pour y parvenir via l’interface utilisateur également.</span><span class="sxs-lookup"><span data-stu-id="f3880-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="f3880-168">Pour essayer cette fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="f3880-168">To try this feature out:</span></span>

1. <span data-ttu-id="f3880-169">Créez une application ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f3880-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="f3880-170">Lancer la boîte de dialogue « Gérer les Packages NuGet »</span><span class="sxs-lookup"><span data-stu-id="f3880-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="f3880-171">Sélectionnez les mises à jour. »</span><span class="sxs-lookup"><span data-stu-id="f3880-171">Select 'Updates'</span></span>
1. <span data-ttu-id="f3880-172">Cliquez sur le bouton « Tout mettre à jour »</span><span class="sxs-lookup"><span data-stu-id="f3880-172">Click the 'Update All' button</span></span>

![Mettre à jour le bouton tout dans la boîte de dialogue](./media/NuGet-2.5/update-all.png)

## <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="f3880-174">Prise en charge de référence de projet améliorée pour le Pack de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f3880-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="f3880-175">Maintenant le processus de commande de pack de nuget.exe référencé projets avec les règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="f3880-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="f3880-176">Si le projet référencé a correspondant `.nuspec` de fichiers, par exemple, il existe un fichier appelé `proj1.nuspec` dans le même dossier que `proj1.csproj`, puis ce projet est ajouté en tant que dépendance pour le package, à l’aide de l’id et version lire à partir de la `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="f3880-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="f3880-177">Dans le cas contraire, les fichiers du projet référencé sont regroupés dans le package.</span><span class="sxs-lookup"><span data-stu-id="f3880-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="f3880-178">Puis projets référencés par ce projet sont traités à l’aide de l’Afficheur de manière récursive les règles.</span><span class="sxs-lookup"><span data-stu-id="f3880-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="f3880-179">Toutes les DLL, `.pdb`, et `.exe` fichiers sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="f3880-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="f3880-180">Tous les autres fichiers de contenu sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="f3880-180">All other content files are added.</span></span>
1. <span data-ttu-id="f3880-181">Toutes les dépendances sont fusionnées.</span><span class="sxs-lookup"><span data-stu-id="f3880-181">All dependencies are merged.</span></span>

<span data-ttu-id="f3880-182">Cela permet à un projet référencé est traitée comme une dépendance s’il existe un `.nuspec` de fichiers, dans le cas contraire, il devient partie intégrante du package.</span><span class="sxs-lookup"><span data-stu-id="f3880-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="f3880-183">Plus de détails ici : [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="f3880-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

## <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="f3880-184">Ajouter une propriété « NuGet Version Minimum » aux packages</span><span class="sxs-lookup"><span data-stu-id="f3880-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="f3880-185">Un nouvel attribut de métadonnées appelé « minClientVersion » peut indiquer maintenant la version du client NuGet minimale nécessaire pour utiliser un package.</span><span class="sxs-lookup"><span data-stu-id="f3880-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="f3880-186">Cette fonctionnalité vous aide à l’auteur du package pour spécifier qu’un package fonctionnera uniquement après une version particulière de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3880-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="f3880-187">En tant que nouveaux `.nuspec` fonctionnalités sont ajoutés après NuGet 2.5, packages seront en mesure de demander une version minimale de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3880-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="f3880-188">Si l’utilisateur a installée de NuGet 2.5 et un package est identifié comme nécessitant 2.6, signaux visuels seront accordée à l’utilisateur indiquant que le package ne sera pas installable.</span><span class="sxs-lookup"><span data-stu-id="f3880-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="f3880-189">L’utilisateur sera ensuite demandé à mettre à jour leur version de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3880-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="f3880-190">Cela améliorera l’expérience dans lequel les packages de commencent à installer mais d’échouer indiquant qu'une version de schéma non reconnu a été identifiée.</span><span class="sxs-lookup"><span data-stu-id="f3880-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

## <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="f3880-191">Dépendances sont n’est plus inutilement mis à jour lors de l’installation du package</span><span class="sxs-lookup"><span data-stu-id="f3880-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="f3880-192">Avant de NuGet 2.5, lorsqu’un package a été installé et que fondées sur un package déjà installé dans le projet, la dépendance sera actualisée dans le cadre de la nouvelle installation, même si la version existante satisfait la dépendance.</span><span class="sxs-lookup"><span data-stu-id="f3880-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="f3880-193">À partir de NuGet 2.5, si une version de la dépendance est déjà satisfaite, la dépendance se verra pas pendant les installations des autres packages.</span><span class="sxs-lookup"><span data-stu-id="f3880-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="f3880-194">**Le scénario :**</span><span class="sxs-lookup"><span data-stu-id="f3880-194">**The scenario:**</span></span>

1. <span data-ttu-id="f3880-195">Le référentiel source contient le package B avec la version 1.0.0 et la version 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="f3880-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="f3880-196">Il contient également le package A, qui a une dépendance sur B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="f3880-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="f3880-197">Supposons que le projet actif possède déjà la version du package B 1.0.0 installé.</span><span class="sxs-lookup"><span data-stu-id="f3880-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="f3880-198">Maintenant que vous souhaitez installer le package a</span><span class="sxs-lookup"><span data-stu-id="f3880-198">Now you want to install package A.</span></span>

<span data-ttu-id="f3880-199">**Dans NuGet, 2.2 et versions antérieure :**</span><span class="sxs-lookup"><span data-stu-id="f3880-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="f3880-200">Lorsque vous installez le package A, NuGet mettra automatiquement à jour B vers la version 1.0.2, même si la version existante 1.0.0 répond déjà à la contrainte de version de dépendance, qui est > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="f3880-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="f3880-201">**Dans NuGet 2.5 et les versions ultérieures :**</span><span class="sxs-lookup"><span data-stu-id="f3880-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="f3880-202">NuGet est plus mis à jour B, parce qu’il détecte que la version existante 1.0.0 conforme à la contrainte de version de dépendance.</span><span class="sxs-lookup"><span data-stu-id="f3880-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="f3880-203">Pour plus d’informations sur cette modification, lisez la section détaillée [élément de travail](http://nuget.codeplex.com/workitem/1681) , ainsi que les [de discussion](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="f3880-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

## <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="f3880-204">NuGet.exe génère des requêtes http avec des commentaires détaillés</span><span class="sxs-lookup"><span data-stu-id="f3880-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="f3880-205">Si vous dépannez nuget.exe ou obtenir des informations que les requêtes HTTP sont effectuées lors des opérations, le '-commentaires détaillés ' commutateur produira désormais des toutes les requêtes HTTP sont effectuées.</span><span class="sxs-lookup"><span data-stu-id="f3880-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Sortie HTTP à partir de nuget.exe](./media/NuGet-2.5/verbosity.png)

## <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="f3880-207">push de NuGet.exe prend désormais en charge les sources UNC et le dossier</span><span class="sxs-lookup"><span data-stu-id="f3880-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="f3880-208">Avant de NuGet 2.5, lorsque vous essayez d’exécuter 'push de nuget.exe' à une source de package basée sur un chemin d’accès UNC ou un dossier local, l’installation poussée du échouerait.</span><span class="sxs-lookup"><span data-stu-id="f3880-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="f3880-209">Avec la fonctionnalité de configuration hiérarchique récemment ajouté, il était devenu commun de nuget.exe besoin cibler une source/dossier UNC, ou dans une galerie NuGet basée sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="f3880-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="f3880-210">À partir de NuGet 2.5, si nuget.exe identifie une source/dossier UNC, elle effectue la copie du fichier à la source.</span><span class="sxs-lookup"><span data-stu-id="f3880-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="f3880-211">La commande suivante fonctionne à présent :</span><span class="sxs-lookup"><span data-stu-id="f3880-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

## <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="f3880-212">NuGet.exe prend en charge explicitement spécifié les fichiers de configuration</span><span class="sxs-lookup"><span data-stu-id="f3880-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="f3880-213">les commandes de NuGet.exe qui accèdent à présent de configuration (tous sauf « spécification » et « pack ») prend en charge un nouveau '-ConfigFile' option, qui force un fichier de configuration spécifiques à utiliser à la place le fichier de configuration par défaut dans % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="f3880-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="f3880-214">Exemple :</span><span class="sxs-lookup"><span data-stu-id="f3880-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

## <a name="support-for-native-projects"></a><span data-ttu-id="f3880-215">Prise en charge pour les projets natifs</span><span class="sxs-lookup"><span data-stu-id="f3880-215">Support for Native projects</span></span>

<span data-ttu-id="f3880-216">Avec NuGet 2.5, les outils de NuGet sont désormais disponible pour les projets natifs dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f3880-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="f3880-217">Nous prévoyons plus packages natifs utilisent la fonctionnalité d’importations MSBuild ci-dessus, à l’aide d’un outil créé par le [CoApp projet](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="f3880-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="f3880-218">Pour plus d’informations, consultez [les détails de l’outil](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) sur le site Web coapp.org.</span><span class="sxs-lookup"><span data-stu-id="f3880-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="f3880-219">Le nom d’infrastructure cible du « native » est introduit pour les packages inclure des fichiers \build \content et \tools lorsque le package est installé dans un projet natif.</span><span class="sxs-lookup"><span data-stu-id="f3880-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="f3880-220">Le \\`lib' dossier n’est pas utilisé pour les projets natifs.</span><span class="sxs-lookup"><span data-stu-id="f3880-220">The \`lib` folder is not used for native projects.</span></span>
