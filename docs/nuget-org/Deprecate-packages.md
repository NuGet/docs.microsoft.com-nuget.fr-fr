---
title: Dépréciation de packages sur nuget.org
description: Description détaillée du processus d’obsolescence des packages et de la façon dont les clients affichent ces informations
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 120b463fda856fe9dd407b6eba32d60e0918f763
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248896"
---
# <a name="deprecating-packages"></a><span data-ttu-id="7100b-103">Dépréciation des packages</span><span class="sxs-lookup"><span data-stu-id="7100b-103">Deprecating packages</span></span>

<span data-ttu-id="7100b-104">Vous pouvez déconseiller un package si vous ne gérez plus un package ou si vous souhaitez inciter les consommateurs de votre package à le déplacer vers un autre package.</span><span class="sxs-lookup"><span data-stu-id="7100b-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="7100b-105">La désapprobation de package est différente de la **liste** de votre package, comme expliqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7100b-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="7100b-106">Le fait de ne pas **répertorier** un package empêche sa détection, car il est masqué dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="7100b-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="7100b-107">La **dépréciation** d’un package permet aux consommateurs existants de votre package de déterminer s’ils sont installés ou utilisés dans leurs projets.</span><span class="sxs-lookup"><span data-stu-id="7100b-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="7100b-108">Elle leur permet également de connaître la raison de la désapprobation et un autre package recommandé tel que spécifié par vous (l’éditeur du package).</span><span class="sxs-lookup"><span data-stu-id="7100b-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="7100b-109">La désapprobation d’un package ne déliste pas le package.</span><span class="sxs-lookup"><span data-stu-id="7100b-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="7100b-110">En tant que serveur de publication, vous pouvez choisir de ne pas répertorier et de déprécier les packages.</span><span class="sxs-lookup"><span data-stu-id="7100b-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="7100b-111">Flux de travail de désapprobation</span><span class="sxs-lookup"><span data-stu-id="7100b-111">Deprecation workflow</span></span>
1. <span data-ttu-id="7100b-112">Pour déprécier un package, accédez à **gérer les packages** et sélectionnez **dépréciation**:</span><span class="sxs-lookup"><span data-stu-id="7100b-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Accéder à l’option déprécier le package](media/deprecation-select-option.png)

2. <span data-ttu-id="7100b-114">Sélectionnez la version que vous souhaitez déprécier.</span><span class="sxs-lookup"><span data-stu-id="7100b-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="7100b-115">Si vous souhaitez déprécier toute la version, choisissez l’option **Sélectionner toutes les versions** .</span><span class="sxs-lookup"><span data-stu-id="7100b-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Sélectionner les versions de package à déprécier](media/deprecation-select-version.png)

3. <span data-ttu-id="7100b-117">Choisissez un motif d’obsolescence.</span><span class="sxs-lookup"><span data-stu-id="7100b-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="7100b-118">Si le package n’est plus conservé, choisissez l’option **hérité** .</span><span class="sxs-lookup"><span data-stu-id="7100b-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="7100b-119">Si la version spécifique présente un bogue critique, choisissez l’option **a des bogues critiques** .</span><span class="sxs-lookup"><span data-stu-id="7100b-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="7100b-120">Pour toute autre raison, sélectionnez **autre**.</span><span class="sxs-lookup"><span data-stu-id="7100b-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="7100b-121">Vous pouvez toujours spécifier un autre package recommandé (et la même version) et un message personnalisé destiné aux propriétaires.</span><span class="sxs-lookup"><span data-stu-id="7100b-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Sélectionner les raisons de la recommandation du package de substitution et un message personnalisé](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="7100b-123">Le message personnalisé s’affiche uniquement sur nuget.org, mais pas sur les clients.</span><span class="sxs-lookup"><span data-stu-id="7100b-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="7100b-124">Actuellement, les clients tels `dotnet.exe` que et le gestionnaire de package NuGet n’affichent pas le message personnalisé.</span><span class="sxs-lookup"><span data-stu-id="7100b-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="7100b-125">Expérience client pour les packages déconseillés</span><span class="sxs-lookup"><span data-stu-id="7100b-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="7100b-126">Une fois qu’un package est déconseillé, ses consommateurs en sont informés de la façon suivante (selon le client utilisé).</span><span class="sxs-lookup"><span data-stu-id="7100b-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="7100b-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7100b-127">Visual Studio</span></span> 
<span data-ttu-id="7100b-128">*Disponible à partir de Visual Studio 2019 version 16,3*</span><span class="sxs-lookup"><span data-stu-id="7100b-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="7100b-129">Visual Studio vous avertit de l’utilisation d’un package déconseillé sous `Installed` l’onglet. Elle vous dirigera vers le package et ses informations d’obsolescence (notamment la raison pour laquelle elle a été dépréciée et le package de remplacement à utiliser à la place, le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="7100b-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab.It will lead you to the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Packages déconseillés sur Visual Studio onglet installé du gestionnaire de package](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="7100b-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="7100b-131">dotnet.exe</span></span>
<span data-ttu-id="7100b-132">*Disponible à partir du kit de développement logiciel (SDK) .NET 3,0*</span><span class="sxs-lookup"><span data-stu-id="7100b-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="7100b-133">Si vous utilisez dotnet. exe, vous pouvez exécuter la commande `dotnet list package --deprecated` sur le dossier de la solution ou du projet pour obtenir la liste des packages déconseillés, ainsi que les informations de désapprobation :</span><span class="sxs-lookup"><span data-stu-id="7100b-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
