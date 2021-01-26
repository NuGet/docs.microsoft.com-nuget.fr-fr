---
title: Notes de publication de NuGet 2.6.1 pour WebMatrix
description: Notes de publication de NuGet 2.6.1 pour WebMatrix, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780420"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="35e0e-103">Notes de publication de NuGet 2.6.1 pour WebMatrix</span><span class="sxs-lookup"><span data-stu-id="35e0e-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="35e0e-104">Notes de publication de [NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Notes de publication de NuGet 2,7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="35e0e-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="35e0e-105">L’équipe NuGet a publié une extension du gestionnaire de package NuGet mise à jour pour WebMatrix le 26 mars 2014.</span><span class="sxs-lookup"><span data-stu-id="35e0e-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="35e0e-106">Cette mise à jour peut être installée à partir de la [Galerie d’extensions WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="35e0e-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="35e0e-107">Ouvrir WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="35e0e-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="35e0e-108">Cliquez sur l’icône extensions dans le ruban d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="35e0e-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="35e0e-109">Sélectionner l’onglet mises à jour</span><span class="sxs-lookup"><span data-stu-id="35e0e-109">Select the Updates tab</span></span>
1. <span data-ttu-id="35e0e-110">Cliquez pour mettre à jour le gestionnaire de package NuGet vers 2.6.1</span><span class="sxs-lookup"><span data-stu-id="35e0e-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="35e0e-111">Fermer et redémarrer WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="35e0e-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="35e0e-112">Modifications notables</span><span class="sxs-lookup"><span data-stu-id="35e0e-112">Notable Changes</span></span>

<span data-ttu-id="35e0e-113">Cette mise à jour d’extension résout deux des problèmes les plus importants que les utilisateurs ont dû confronter à l’utilisation de packages NuGet dans WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="35e0e-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="35e0e-114">La première était une erreur de version de schéma NuGet et la seconde était un bogue conduisant à des dll de zéro octet dans le `bin` dossier.</span><span class="sxs-lookup"><span data-stu-id="35e0e-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="35e0e-115">Erreur de version du schéma NuGet</span><span class="sxs-lookup"><span data-stu-id="35e0e-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="35e0e-116">Étant donné que WebMatrix 3 a été publié, de nouvelles fonctionnalités ont été introduites dans NuGet qui nécessitent une nouvelle version de schéma pour les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="35e0e-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="35e0e-117">Lorsque vous tentez de gérer vos packages NuGet sur votre site Web, ces nouveaux packages peuvent entraîner des erreurs que vous voyez dans WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="35e0e-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Une erreur est survenue.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="35e0e-121">Cette dernière version offre une compatibilité avec les packages NuGet les plus récents, ce qui empêche l’apparition de cette erreur.</span><span class="sxs-lookup"><span data-stu-id="35e0e-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="35e0e-122">Les nouvelles versions des packages, y compris Microsoft. AspNet. webpages, peuvent désormais être installées dans WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="35e0e-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="35e0e-123">Certains de ces packages utilisaient des fonctionnalités NuGet, telles que des [transformations de configuration xdt](../release-notes/nuget-2.6.md#xdt), qui n’étaient pas prises en charge dans WebMatrix jusqu’à présent.</span><span class="sxs-lookup"><span data-stu-id="35e0e-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="35e0e-124">Zero-Byte des dll dans le dossier bin</span><span class="sxs-lookup"><span data-stu-id="35e0e-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="35e0e-125">Certains utilisateurs ont signalé qu’après l’installation des packages NuGet dans WebMatrix qui incluent des dll copiées dans bin, les dll s’affichent dans le `bin` dossier en tant que fichiers de 0 octet.</span><span class="sxs-lookup"><span data-stu-id="35e0e-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="35e0e-126">Cela interrompt l’application au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="35e0e-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="35e0e-127">[Ce problème](https://nuget.codeplex.com/workitem/4060) a été résolu.</span><span class="sxs-lookup"><span data-stu-id="35e0e-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="35e0e-128">Autres améliorations récentes</span><span class="sxs-lookup"><span data-stu-id="35e0e-128">Other Recent Improvements</span></span>

<span data-ttu-id="35e0e-129">Quand le gestionnaire de package NuGet 2,8 a été publié pour Visual Studio, nous avons également publié le gestionnaire de package NuGet 2.5.0 pour WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="35e0e-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="35e0e-130">Bien que cela ait été mentionné dans les [notes de publication de NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nous n’avons pas mentionné les nouvelles fonctionnalités spécifiques mises à jour introduites.</span><span class="sxs-lookup"><span data-stu-id="35e0e-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="35e0e-131">Tout mettre à jour</span><span class="sxs-lookup"><span data-stu-id="35e0e-131">Update All</span></span>

<span data-ttu-id="35e0e-132">Vous pouvez maintenant mettre à jour tous les packages de votre site Web en une seule étape.</span><span class="sxs-lookup"><span data-stu-id="35e0e-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="35e0e-133">Lorsque vous ouvrez l’extension NuGet dans WebMatrix, vous voyez la liste de tous les packages dans la Galerie, ceux installés et ceux avec des mises à jour disponibles.</span><span class="sxs-lookup"><span data-stu-id="35e0e-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="35e0e-134">Auparavant, chaque package devait être mis à jour individuellement, mais il y a maintenant un bouton « mettre à jour tout » utile qui s’affiche sous l’onglet mises à jour.</span><span class="sxs-lookup"><span data-stu-id="35e0e-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Cliquez sur tout mettre à jour pour mettre à jour tous les packages avec les mises à jour disponibles](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="35e0e-136">Remplacer les fichiers existants</span><span class="sxs-lookup"><span data-stu-id="35e0e-136">Overwrite Existing Files</span></span>

<span data-ttu-id="35e0e-137">Lors de l’installation de packages contenant des fichiers qui existent déjà sur votre site Web, NuGet a toujours ignoré ces fichiers en mode silencieux (laissant uniquement vos fichiers existants).</span><span class="sxs-lookup"><span data-stu-id="35e0e-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="35e0e-138">Cela peut donner l’impression qu’un package a été installé ou mis à jour correctement en fait.</span><span class="sxs-lookup"><span data-stu-id="35e0e-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="35e0e-139">NuGet va maintenant demander que les fichiers soient remplacés.</span><span class="sxs-lookup"><span data-stu-id="35e0e-139">NuGet will now prompt for files to be overwritten.</span></span>

![Résolution des conflits de fichiers](./media/NuGet-2.8/webmatrix-overwrite-file.png)
