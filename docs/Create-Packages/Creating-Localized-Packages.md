---
title: "Guide pratique pour créer un package NuGet localisé | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informations sur les deux façons de créer des packages NuGet localisés, soit en incluant tous les assemblys dans un package unique, soit en publiant des assemblys séparés."
keywords: "Localisation de packages NuGet, assemblys satellites NuGet, création de packages localisés, conventions de localisation NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1ce8cff07bf629fcdeeaace901a185f2446b077a
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2018
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="5e706-104">Création de packages NuGet localisés</span><span class="sxs-lookup"><span data-stu-id="5e706-104">Creating localized NuGet packages</span></span>

<span data-ttu-id="5e706-105">Il existe deux façons de créer des versions localisées d’une bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="5e706-105">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="5e706-106">Incluez tous les assemblys de ressources localisés dans un package unique.</span><span class="sxs-lookup"><span data-stu-id="5e706-106">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="5e706-107">Créez des packages satellites localisés distincts (NuGet 1.8 et version ultérieure), en suivant un ensemble strict de conventions.</span><span class="sxs-lookup"><span data-stu-id="5e706-107">Create separate localized satellite packages (NuGet 1.8 and later), by following a strict set of conventions.</span></span>

<span data-ttu-id="5e706-108">Les deux méthodes ont leurs avantages et leurs inconvénients, comme décrit dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="5e706-108">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="5e706-109">Assemblys de ressources localisés dans un package unique</span><span class="sxs-lookup"><span data-stu-id="5e706-109">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="5e706-110">L’inclusion des assemblys de ressources localisés dans un package unique constitue généralement l’approche la plus simple.</span><span class="sxs-lookup"><span data-stu-id="5e706-110">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="5e706-111">Pour cela, créez des dossiers dans `lib` pour la langue prise en charge autre que celle par défaut du package (supposée être en-us).</span><span class="sxs-lookup"><span data-stu-id="5e706-111">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="5e706-112">Dans ces dossiers, vous pouvez placer des assemblys de ressources et des fichiers XML IntelliSense localisés.</span><span class="sxs-lookup"><span data-stu-id="5e706-112">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="5e706-113">Par exemple, la structure de dossiers suivante prend en charge l’allemand (de), l’italien (it), le japonais (ja), le russe (ru), le chinois simplifié (zh-Hans) et le chinois traditionnel (zh-Hant) :</span><span class="sxs-lookup"><span data-stu-id="5e706-113">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="5e706-114">Vous pouvez voir que les langues sont toutes répertoriées sous le dossier de la version cible de .Net Framework `net40`.</span><span class="sxs-lookup"><span data-stu-id="5e706-114">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="5e706-115">Si vous [prenez en charge plusieurs versions](../create-packages/supporting-multiple-target-frameworks.md), vous avez un dossier sous `lib` pour chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="5e706-115">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="5e706-116">Une fois ces dossiers en place, vous pouvez référencer tous les fichiers dans votre `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="5e706-116">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="5e706-117">[Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0) est un exemple de package qui utilise cette approche.</span><span class="sxs-lookup"><span data-stu-id="5e706-117">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="5e706-118">Avantages et inconvénients (assemblies de ressources localisées)</span><span class="sxs-lookup"><span data-stu-id="5e706-118">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="5e706-119">Le regroupement de toutes les langues dans un package unique présente quelques inconvénients :</span><span class="sxs-lookup"><span data-stu-id="5e706-119">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="5e706-120">**Métadonnées partagées** : étant donné qu’un package NuGet peut uniquement contenir un seul fichier `.nuspec`, vous pouvez fournir les métadonnées d’une seule langue.</span><span class="sxs-lookup"><span data-stu-id="5e706-120">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="5e706-121">Autrement dit, NuGet ne prend pas encore en charge les métadonnées localisées.</span><span class="sxs-lookup"><span data-stu-id="5e706-121">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="5e706-122">**Taille du package** : selon le nombre de langues que vous prenez en charge, la bibliothèque peut devenir très volumineuse, ce qui ralentit l’installation et la restauration du package.</span><span class="sxs-lookup"><span data-stu-id="5e706-122">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="5e706-123">**Versions simultanées** : le regroupement des fichiers localisés dans un package unique exige la publication simultanée de toutes les ressources dans ce package, au lieu de la publication de chaque localisation séparément.</span><span class="sxs-lookup"><span data-stu-id="5e706-123">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="5e706-124">De plus, toute mise à jour d’une localisation exige une nouvelle version de la totalité du package.</span><span class="sxs-lookup"><span data-stu-id="5e706-124">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="5e706-125">Toutefois, il a également quelques avantages :</span><span class="sxs-lookup"><span data-stu-id="5e706-125">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="5e706-126">**Simplicité** : les consommateurs du package obtiennent toutes les langues prises en charge dans une installation unique, au lieu de devoir installer chaque langue séparément.</span><span class="sxs-lookup"><span data-stu-id="5e706-126">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="5e706-127">Un package unique est également plus facile à trouver sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5e706-127">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="5e706-128">**Versions couplées** : étant donné que tous les assemblys de ressources se trouvent dans le même package que l’assembly principal, ils partagent tous le même numéro de version et ne courent pas le risque d’être découplés par erreur.</span><span class="sxs-lookup"><span data-stu-id="5e706-128">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="5e706-129">Packages satellites localisés</span><span class="sxs-lookup"><span data-stu-id="5e706-129">Localized satellite packages</span></span>

<span data-ttu-id="5e706-130">Semblable à la manière dont .NET Framework prend en charge les assemblys satellites, cette méthode sépare les ressources localisées et les fichiers XML IntelliSense dans des packages satellites.</span><span class="sxs-lookup"><span data-stu-id="5e706-130">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="5e706-131">Pour cela, votre package principal utilise la convention de nommage `{identifier}.{version}.nupkg` et contient l’assembly de la langue par défaut (par exemple, en-US).</span><span class="sxs-lookup"><span data-stu-id="5e706-131">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="5e706-132">Par exemple, `ContosoUtilities.1.0.0.nupkg` contiendrait la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="5e706-132">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="5e706-133">Un assembly satellite utilise alors la convention de nommage `{identifier}.{language}.{version}.nupkg`, comme `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="5e706-133">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="5e706-134">L’identificateur **doit** correspondre exactement à celui du package principal.</span><span class="sxs-lookup"><span data-stu-id="5e706-134">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="5e706-135">Comme il s’agit d’un package distinct, il possède son propre fichier `.nuspec` qui contient des métadonnées localisées.</span><span class="sxs-lookup"><span data-stu-id="5e706-135">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="5e706-136">N’oubliez pas que la langue dans le fichier `.nuspec` **doit** correspond à celle utilisée dans le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="5e706-136">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="5e706-137">L’assembly satellite **doit** également déclarer une version exacte du package principal en tant que dépendance, à l’aide de la notation de version [] \(consultez [Gestion des versions de package](../reference/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="5e706-137">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="5e706-138">Par exemple, `ContosoUtilities.de.1.0.0.nupkg` doit déclarer une dépendance vis-à-vis de `ContosoUtilities.1.0.0.nupkg` à l’aide de la notation `[1.0.0]`.</span><span class="sxs-lookup"><span data-stu-id="5e706-138">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="5e706-139">Le package satellite peut, bien entendu, avoir un numéro de version différent de celui du package principal.</span><span class="sxs-lookup"><span data-stu-id="5e706-139">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="5e706-140">La structure du package satellite doit alors inclure l’assembly de ressources et le fichier XML IntelliSense dans un sous-dossier qui correspond à `{language}` dans le nom de fichier du package :</span><span class="sxs-lookup"><span data-stu-id="5e706-140">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="5e706-141">**Remarque** : sauf si des sous-cultures spécifiques comme `ja-JP` sont nécessaires, utilisez toujours l’identificateur de langue le plus général, comme `ja`.</span><span class="sxs-lookup"><span data-stu-id="5e706-141">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="5e706-142">Dans un assembly satellite, NuGet reconnaît **uniquement** les fichiers inclus dans le dossier qui correspond à `{language}` dans le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="5e706-142">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="5e706-143">Tous les autres sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="5e706-143">All others are ignored.</span></span>

<span data-ttu-id="5e706-144">Lorsque toutes ces conventions sont respectées, NuGet reconnaît le package en tant que package satellite et installe les fichiers localisés dans le dossier `lib` du package principal, comme s’ils avaient été regroupés à l’origine.</span><span class="sxs-lookup"><span data-stu-id="5e706-144">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="5e706-145">La désinstallation du package satellite permet de supprimer ses fichiers de ce même dossier.</span><span class="sxs-lookup"><span data-stu-id="5e706-145">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="5e706-146">Vous créez d’autres assemblys satellites de la même façon pour chaque langue prise en charge.</span><span class="sxs-lookup"><span data-stu-id="5e706-146">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="5e706-147">Pour obtenir un exemple, examinez l’ensemble de packages MVC ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="5e706-147">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="5e706-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (anglais principal)</span><span class="sxs-lookup"><span data-stu-id="5e706-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="5e706-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (allemand)</span><span class="sxs-lookup"><span data-stu-id="5e706-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="5e706-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonais)</span><span class="sxs-lookup"><span data-stu-id="5e706-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="5e706-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chinois (simplifié))</span><span class="sxs-lookup"><span data-stu-id="5e706-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="5e706-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chinois (traditionnel))</span><span class="sxs-lookup"><span data-stu-id="5e706-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="5e706-153">Résumé des conventions obligatoires</span><span class="sxs-lookup"><span data-stu-id="5e706-153">Summary of required conventions</span></span>

- <span data-ttu-id="5e706-154">Le package principal doit être nommé `{identifier}.{version}.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="5e706-154">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="5e706-155">Un package satellite doit être nommé `{identifier}.{language}.{version}.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="5e706-155">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="5e706-156">Le fichier `.nuspec` d’un package satellite doit spécifier sa langue pour correspondre au nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="5e706-156">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="5e706-157">Un package satellite doit déclarer une dépendance vis-à-vis d’une version exacte du package principal à l’aide de la notation [] dans son fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5e706-157">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="5e706-158">Les plages ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="5e706-158">Ranges are not supported.</span></span>
- <span data-ttu-id="5e706-159">Un package satellite doit placer des fichiers dans le dossier `lib\[{framework}\]{language}` qui correspondent exactement à `{language}` dans le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="5e706-159">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="5e706-160">Avantages et inconvénients (packages satellites)</span><span class="sxs-lookup"><span data-stu-id="5e706-160">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="5e706-161">L’utilisation de packages satellites présente quelques avantages :</span><span class="sxs-lookup"><span data-stu-id="5e706-161">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="5e706-162">**Taille du package** : l’encombrement global du package principal est réduit et les consommateurs payent uniquement les coûts de chaque langue qu’ils souhaitent utiliser.</span><span class="sxs-lookup"><span data-stu-id="5e706-162">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="5e706-163">**Métadonnées distinctes** : chaque package satellite possède son propre fichier `.nuspec` et, par conséquent, ses propres métadonnées localisées.</span><span class="sxs-lookup"><span data-stu-id="5e706-163">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="5e706-164">Cela peut permettre à certains consommateurs de trouver plus facilement des packages sur nuget.org en utilisant des termes localisés.</span><span class="sxs-lookup"><span data-stu-id="5e706-164">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="5e706-165">**Versions découplées** : il est possible de publier les assemblys satellites progressivement, plutôt que tous en même temps, ce qui vous permet d’étaler vos efforts de localisation.</span><span class="sxs-lookup"><span data-stu-id="5e706-165">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="5e706-166">Néanmois, les packages satellites présentent aussi quelques inconvénients :</span><span class="sxs-lookup"><span data-stu-id="5e706-166">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="5e706-167">**Multiplicité** : au lieu d’un package unique, vous avez de nombreux packages pouvant engendrer des résultats de recherche confus sur nuget.org et une longue liste de références dans un projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5e706-167">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="5e706-168">**Conventions strictes**.</span><span class="sxs-lookup"><span data-stu-id="5e706-168">**Strict conventions**.</span></span> <span data-ttu-id="5e706-169">Les packages satellites doivent suivre les conventions à la lettre sans quoi les versions localisées ne sont pas correctement sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="5e706-169">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="5e706-170">**Gestion de versions** : chaque package satellite doit avoir une dépendance de version exacte vis-à-vis du package principal.</span><span class="sxs-lookup"><span data-stu-id="5e706-170">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="5e706-171">Cela signifie que la mise à jour du package principal peut nécessiter celle de tous les packages satellites également, même si les ressources n’ont pas changé.</span><span class="sxs-lookup"><span data-stu-id="5e706-171">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
