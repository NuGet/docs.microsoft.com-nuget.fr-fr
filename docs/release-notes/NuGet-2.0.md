---
title: Notes de publication de NuGet 2,0
description: Notes de publication de NuGet 2,0, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776994"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="91140-103">Notes de publication de NuGet 2,0</span><span class="sxs-lookup"><span data-stu-id="91140-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="91140-104">Notes de publication de [NuGet 1,8](../release-notes/nuget-1.8.md)  |  [Notes de publication de NuGet 2,1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="91140-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="91140-105">NuGet 2,0 a été publié le 19 juin 2012.</span><span class="sxs-lookup"><span data-stu-id="91140-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="91140-106">Problème d’installation connu</span><span class="sxs-lookup"><span data-stu-id="91140-106">Known Installation Issue</span></span>
<span data-ttu-id="91140-107">Si vous exécutez VS 2010 SP1, vous pouvez rencontrer une erreur d’installation lors de la tentative de mise à niveau de NuGet si une version antérieure est installée.</span><span class="sxs-lookup"><span data-stu-id="91140-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="91140-108">La solution consiste à désinstaller simplement NuGet, puis à l’installer à partir de la Galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91140-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="91140-109"><https://support.microsoft.com/kb/2581019>Pour plus d’informations, consultez pour plus d’informations ou [accédez directement au correctif vs](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="91140-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="91140-110">Remarque : si Visual Studio ne vous permet pas de désinstaller l’extension (le bouton désinstaller est désactivé), vous devrez probablement redémarrer Visual Studio à l’aide de « exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="91140-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="91140-111">Le consentement de la restauration du package est maintenant actif</span><span class="sxs-lookup"><span data-stu-id="91140-111">Package restore consent is now active</span></span>

<span data-ttu-id="91140-112">Comme décrit dans cette [publication sur le consentement de la restauration des packages](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 requiert désormais que le consentement soit donné pour activer la restauration du package en ligne et télécharger les packages.</span><span class="sxs-lookup"><span data-stu-id="91140-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="91140-113">Vérifiez que vous avez fourni un consentement via la boîte de dialogue de configuration du gestionnaire de package ou la variable d’environnement EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="91140-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="91140-114">Grouper les dépendances par frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="91140-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="91140-115">À partir de la version 2,0, les dépendances de package peuvent varier en fonction du profil du Framework du projet cible.</span><span class="sxs-lookup"><span data-stu-id="91140-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="91140-116">Cela s’effectue à l’aide d’un schéma mis à jour `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="91140-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="91140-117">L' `<dependencies>` élément peut maintenant contenir un ensemble d' `<group>` éléments.</span><span class="sxs-lookup"><span data-stu-id="91140-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="91140-118">Chaque groupe contient zéro `<dependency>` élément, un ou plusieurs éléments et un `targetFramework` attribut.</span><span class="sxs-lookup"><span data-stu-id="91140-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="91140-119">Toutes les dépendances à l’intérieur d’un groupe sont installées ensemble si le Framework cible est compatible avec le profil de l’infrastructure de projet cible.</span><span class="sxs-lookup"><span data-stu-id="91140-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="91140-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="91140-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="91140-121">Notez qu’un groupe peut contenir **zéro** dépendance.</span><span class="sxs-lookup"><span data-stu-id="91140-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="91140-122">Dans l’exemple ci-dessus, si le package est installé dans un projet qui cible Silverlight 3,0 ou une version ultérieure, aucune dépendance n’est installée.</span><span class="sxs-lookup"><span data-stu-id="91140-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="91140-123">Si le package est installé dans un projet qui cible .NET 4,0 ou une version ultérieure, deux dépendances, jQuery et webactivateur, seront installées.</span><span class="sxs-lookup"><span data-stu-id="91140-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="91140-124">Si le package est installé dans un projet qui cible une version antérieure de ces 2 frameworks, ou de tout autre Framework, RouteMagic 1.1.0 sera installé.</span><span class="sxs-lookup"><span data-stu-id="91140-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="91140-125">Il n’y a pas d’héritage entre les groupes.</span><span class="sxs-lookup"><span data-stu-id="91140-125">There is no inheritance between groups.</span></span> <span data-ttu-id="91140-126">Si la version cible de .NET Framework d’un projet correspond à l' `targetFramework` attribut d’un groupe, seules les dépendances au sein de ce groupe seront installées.</span><span class="sxs-lookup"><span data-stu-id="91140-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="91140-127">Un package peut spécifier des dépendances de package dans l’un des deux formats suivants : l’ancien format d’une liste plate d' `<dependency>` éléments ou de groupes.</span><span class="sxs-lookup"><span data-stu-id="91140-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="91140-128">Si le `<group>` format est utilisé, le package ne peut pas être installé dans les versions de NuGet antérieures à 2,0.</span><span class="sxs-lookup"><span data-stu-id="91140-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="91140-129">Notez que le mélange des deux formats n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="91140-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="91140-130">Par exemple, l’extrait de code suivant n’est **pas valide** et sera rejeté par NuGet.</span><span class="sxs-lookup"><span data-stu-id="91140-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="91140-131">Regroupement de fichiers de contenu et de scripts PowerShell par le Framework cible</span><span class="sxs-lookup"><span data-stu-id="91140-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="91140-132">Outre les références d’assembly, les fichiers de contenu et les scripts PowerShell peuvent également être regroupés par Framework cible.</span><span class="sxs-lookup"><span data-stu-id="91140-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="91140-133">La même structure de dossiers trouvée dans le dossier pour la spécification de la version `lib` cible de .NET Framework peut désormais être appliquée de la même façon aux `content` `tools` dossiers et.</span><span class="sxs-lookup"><span data-stu-id="91140-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="91140-134">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="91140-134">For example:</span></span>

```
\content
    \net11
        \MyContent.txt
    \net20
        \MyContent20.txt
    \net40
    \sl40
        \MySilverlightContent.html

\tools
    \init.ps1
    \net40
        \install.ps1
        \uninstall.ps1
    \sl40
        \install.ps1
        \uninstall.ps1
```

<span data-ttu-id="91140-135">**Remarque**: étant donné que `init.ps1` est exécuté au niveau de la solution et qu’il n’est pas dépendant d’un projet individuel, il doit être placé directement sous le `tools` dossier.</span><span class="sxs-lookup"><span data-stu-id="91140-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="91140-136">S’il est placé dans un dossier spécifique à l’infrastructure, il sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="91140-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="91140-137">En outre, une nouvelle fonctionnalité de NuGet 2,0 est qu’un dossier Framework peut être *vide*, auquel cas NuGet n’ajoute pas de références d’assembly, n’ajoute pas de fichiers de contenu ou n’exécute pas de scripts PowerShell pour la version de Framework particulière.</span><span class="sxs-lookup"><span data-stu-id="91140-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="91140-138">Dans l’exemple ci-dessus, le dossier `content\net40` est vide.</span><span class="sxs-lookup"><span data-stu-id="91140-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="91140-139">Amélioration des performances de la saisie semi-automatique par tabulation</span><span class="sxs-lookup"><span data-stu-id="91140-139">Improved tab completion performance</span></span>
<span data-ttu-id="91140-140">La fonctionnalité de saisie semi-automatique par tabulation dans la console du gestionnaire de package NuGet a été mise à jour pour améliorer les performances de manière significative.</span><span class="sxs-lookup"><span data-stu-id="91140-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="91140-141">Il y aura bien moins de temps à partir du moment où la touche Tab est enfoncée jusqu’à ce que la liste déroulante de suggestions apparaisse.</span><span class="sxs-lookup"><span data-stu-id="91140-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="91140-142">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="91140-142">Bug Fixes</span></span>
<span data-ttu-id="91140-143">NuGet 2,0 comprend de nombreux correctifs de bogues, en mettant l’accent sur le consentement et les performances de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="91140-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="91140-144">Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2,0, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="91140-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
