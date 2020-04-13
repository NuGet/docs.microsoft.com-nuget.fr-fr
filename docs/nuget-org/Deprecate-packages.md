---
title: Déprécier les paquets sur nuget.org
description: Description détaillée du processus de dépréciation des paquets et de la façon dont les clients affichent ces informations
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096883"
---
# <a name="deprecating-packages"></a><span data-ttu-id="dde8d-103">Déprécier les paquets</span><span class="sxs-lookup"><span data-stu-id="dde8d-103">Deprecating packages</span></span>

<span data-ttu-id="dde8d-104">Vous pouvez déprécier un forfait si vous ne conservez plus un forfait ou si vous souhaitez encourager les consommateurs de votre forfait à passer à un autre forfait.</span><span class="sxs-lookup"><span data-stu-id="dde8d-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="dde8d-105">La dépréciation du paquet est différente de la **non-cotation de** votre colis comme expliqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="dde8d-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="dde8d-106">**Le déballage d’un** paquet empêche sa découverte parce qu’il est caché dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="dde8d-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="dde8d-107">**La dépréciation d’un** paquet permet aux consommateurs existants de votre colis de savoir s’ils l’ont installé ou utilisé dans leurs projets.</span><span class="sxs-lookup"><span data-stu-id="dde8d-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="dde8d-108">Il leur permet également de connaître la raison de la dépréciation et un autre paquet recommandé tel que spécifié par vous (l’éditeur de paquets).</span><span class="sxs-lookup"><span data-stu-id="dde8d-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="dde8d-109">Déprécier un paquet ne désiste pas le paquet.</span><span class="sxs-lookup"><span data-stu-id="dde8d-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="dde8d-110">En tant qu’éditeur, vous pouvez choisir de non-liste ainsi que de déprécier les paquets.</span><span class="sxs-lookup"><span data-stu-id="dde8d-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="dde8d-111">Flux de travail de dépréciation</span><span class="sxs-lookup"><span data-stu-id="dde8d-111">Deprecation workflow</span></span>
1. <span data-ttu-id="dde8d-112">Pour déprécier un forfait, **rendez-vous** sur Gérer les forfaits et sélectionnez **Déprécation**:</span><span class="sxs-lookup"><span data-stu-id="dde8d-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Aller à déprécier l’option paquet](media/deprecation-select-option.png)

2. <span data-ttu-id="dde8d-114">Sélectionnez la version que vous souhaitez déprécier.</span><span class="sxs-lookup"><span data-stu-id="dde8d-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="dde8d-115">Si vous souhaitez déprécier toutes les **versions, choisissez Sélectionnez toutes les versions** option.</span><span class="sxs-lookup"><span data-stu-id="dde8d-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Sélectionnez des versions de paquet pour déprécier](media/deprecation-select-version.png)

3. <span data-ttu-id="dde8d-117">Choisissez une raison de dépréciation.</span><span class="sxs-lookup"><span data-stu-id="dde8d-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="dde8d-118">Si le paquet n’est plus maintenu, choisissez l’option **Legacy.**</span><span class="sxs-lookup"><span data-stu-id="dde8d-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="dde8d-119">Si la version spécifique a un bogue critique, choisissez **l’option des bogues critiques.**</span><span class="sxs-lookup"><span data-stu-id="dde8d-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="dde8d-120">Pour toute autre raison, sélectionnez **Autre**.</span><span class="sxs-lookup"><span data-stu-id="dde8d-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="dde8d-121">Vous pouvez toujours spécifier un autre paquet recommandé (et la version) et un message personnalisé aux propriétaires.</span><span class="sxs-lookup"><span data-stu-id="dde8d-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Sélectionnez des raisons de recommandation de paquet alternative et de message personnalisé](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="dde8d-123">Le message personnalisé n’est affiché que sur nuget.org mais pas auprès des clients.</span><span class="sxs-lookup"><span data-stu-id="dde8d-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="dde8d-124">Actuellement, les `dotnet.exe` clients tels que et le gestionnaire de paquets NuGet ne montrent pas le message personnalisé.</span><span class="sxs-lookup"><span data-stu-id="dde8d-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="dde8d-125">Expérience client pour les forfaits dépréciés</span><span class="sxs-lookup"><span data-stu-id="dde8d-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="dde8d-126">Une fois qu’un colis a été déprécié, ses consommateurs en sont informés de la façon suivante (selon le client utilisé).</span><span class="sxs-lookup"><span data-stu-id="dde8d-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="dde8d-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dde8d-127">Visual Studio</span></span> 
<span data-ttu-id="dde8d-128">*Disponible à partir de Visual Studio 2019 version 16.3*</span><span class="sxs-lookup"><span data-stu-id="dde8d-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="dde8d-129">Visual Studio met en garde contre l’utilisation `Installed` d’un paquet déprécié sur l’onglet. Il montrera un avertissement pour le paquet et ses informations de dépréciation (y compris la raison pour laquelle il a été déprécié et le paquet alternatif à utiliser à la place, si présent).</span><span class="sxs-lookup"><span data-stu-id="dde8d-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Paquets dépréciés sur Visual Studio onglet installé de gestionnaire de paquets](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="dde8d-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="dde8d-131">dotnet.exe</span></span>
<span data-ttu-id="dde8d-132">*Disponible en commençant par .NET SDK 3.0*</span><span class="sxs-lookup"><span data-stu-id="dde8d-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="dde8d-133">Si vous utilisez dotnet.exe, vous `dotnet list package --deprecated` pouvez exécuter la commande sur la solution ou le dossier de projet pour obtenir une liste de paquets dépréciés ainsi que les informations de dépréciation:</span><span class="sxs-lookup"><span data-stu-id="dde8d-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
