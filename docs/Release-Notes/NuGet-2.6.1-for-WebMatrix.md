---
title: NuGet 2.6.1 pour les Notes de publication WebMatrix | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Notes de publication pour NuGet 2.6.1 pour WebMatrix, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 2.6.1 pour les notes de publication WebMatrix, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f859fd8ef74f3246d997790e40f70ad25aadeb71
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="f8e5a-104">NuGet 2.6.1 pour les Notes de publication WebMatrix</span><span class="sxs-lookup"><span data-stu-id="f8e5a-104">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="f8e5a-105">[Notes de publication NuGet 2.6](../release-notes/nuget-2.6.md) | [NuGet 2.7 Notes de publication](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="f8e5a-105">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="f8e5a-106">L’équipe NuGet a publié une extension de gestionnaire de Package NuGet de mise à jour pour WebMatrix 26 mars 2014.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-106">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="f8e5a-107">Cette mise à jour peut être installé à partir de la [Galerie d’extensions WebMatrix](http://extensions.webmatrix.com/packages/NuGetPackageManager/) en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="f8e5a-107">This update can be installed from the [WebMatrix Extension Gallery](http://extensions.webmatrix.com/packages/NuGetPackageManager/) using the following steps:</span></span>

1. <span data-ttu-id="f8e5a-108">Ouvrez WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="f8e5a-108">Open WebMatrix 3</span></span>
2. <span data-ttu-id="f8e5a-109">Cliquez sur l’icône des Extensions dans le ruban Accueil</span><span class="sxs-lookup"><span data-stu-id="f8e5a-109">Click the Extensions icon in the Home ribbon</span></span>
3. <span data-ttu-id="f8e5a-110">Sélectionnez l’onglet mises à jour</span><span class="sxs-lookup"><span data-stu-id="f8e5a-110">Select the Updates tab</span></span>
4. <span data-ttu-id="f8e5a-111">Cliquez pour mettre à jour le Gestionnaire de Package NuGet pour 2.6.1</span><span class="sxs-lookup"><span data-stu-id="f8e5a-111">Click to update NuGet Package Manager to 2.6.1</span></span>
6. <span data-ttu-id="f8e5a-112">Fermez et redémarrez WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="f8e5a-112">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="f8e5a-113">Modifications importantes</span><span class="sxs-lookup"><span data-stu-id="f8e5a-113">Notable Changes</span></span>

<span data-ttu-id="f8e5a-114">Cette extension mise à jour concerne deux des problèmes majeurs à vos utilisateurs ont dû faire face les packages NuGet consommation dans WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-114">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="f8e5a-115">La première était une erreur de version de schéma de NuGet et le deuxième un bogue conduisant à la DLL de zéro octet dans le `bin` dossier.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-115">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="f8e5a-116">Erreur de Version du schéma de NuGet</span><span class="sxs-lookup"><span data-stu-id="f8e5a-116">NuGet Schema Version Error</span></span>

<span data-ttu-id="f8e5a-117">Depuis la publication de WebMatrix 3, les nouvelles fonctionnalités ont été introduites dans NuGet qui nécessitent une nouvelle version de schéma pour les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-117">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="f8e5a-118">Lorsque vous tentez de gérer vos packages NuGet dans votre site web, ces nouveaux packages peuvent entraîner des erreurs qui s’affiche dans WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-118">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you'll see in WebMatrix.</span></span>

![Une erreur s'est produite.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="f8e5a-122">Cette nouvelle version assure la compatibilité avec les packages NuGet les plus récents, empêcher cette erreur ne se produise.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-122">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="f8e5a-123">Nouvelles versions des packages, y compris Microsoft.AspNet.WebPages peuvent désormais être installées dans WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-123">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="f8e5a-124">Certaines de ces packages ont été à l’aide des fonctionnalités de NuGet comme [XDT config transforme](../release-notes/nuget-2.6.md#xdt), qui n’a pas été pris en charge dans WebMatrix jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-124">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="f8e5a-125">DLL de zéro octet dans l’emplacement de dossier</span><span class="sxs-lookup"><span data-stu-id="f8e5a-125">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="f8e5a-126">Certains utilisateurs ont indiqué qu’une fois l’installation de NuGet empaquette dans WebMatrix qui incluent des DLL qui sont copiés à l’emplacement que l’émission de la DLL dans le `bin` dossier en tant que fichiers de 0 octet.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-126">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="f8e5a-127">Cela arrête l’application lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-127">This breaks the application at runtime.</span></span>

<span data-ttu-id="f8e5a-128">[Ce problème](https://nuget.codeplex.com/workitem/4060) a maintenant été corrigé.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-128">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="f8e5a-129">Autres améliorations récentes</span><span class="sxs-lookup"><span data-stu-id="f8e5a-129">Other Recent Improvements</span></span>

<span data-ttu-id="f8e5a-130">Lorsque le Gestionnaire de Package NuGet 2.8 a été lancé pour Visual Studio, nous avons publié également le Gestionnaire de Package NuGet 2.5.0 pour WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-130">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="f8e5a-131">Alors que cela a été mentionné dans le [notes de mise à jour de NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nous n’a pas de mentionner les nouvelles fonctionnalités spécifiques cette mise à jour introduit.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-131">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="f8e5a-132">Tout mettre à jour</span><span class="sxs-lookup"><span data-stu-id="f8e5a-132">Update All</span></span>

<span data-ttu-id="f8e5a-133">Vous pouvez maintenant mettre à jour tous les packages de votre site web en une seule étape !</span><span class="sxs-lookup"><span data-stu-id="f8e5a-133">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="f8e5a-134">Lorsque vous ouvrez l’extension NuGet dans WebMatrix, vous consultez la liste de tous les packages dans la galerie, ces derniers sont installés et celles avec les mises à jour disponibles.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-134">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="f8e5a-135">Auparavant, chaque package devra être mis à jour individuellement, mais il existe désormais un bouton « Mise à jour toutes les » utile qui s’affiche sous l’onglet mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-135">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Cliquez sur tout mettre à jour pour mettre à jour tous les packages de mises à jour disponibles](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="f8e5a-137">Remplacer les fichiers existants</span><span class="sxs-lookup"><span data-stu-id="f8e5a-137">Overwrite Existing Files</span></span>

<span data-ttu-id="f8e5a-138">Lors de l’installation des packages qui contiennent les fichiers qui existent déjà dans votre site web, NuGet a toujours uniquement en mode silencieux les fichiers ignorés (toucher vos fichiers existants).</span><span class="sxs-lookup"><span data-stu-id="f8e5a-138">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="f8e5a-139">Cela peut entraîner l’impression qu’un package a été installé ou mis à jour correctement lorsque en fait qu’il n’a pas été.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-139">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="f8e5a-140">NuGet va maintenant demander pour les fichiers doivent être remplacées.</span><span class="sxs-lookup"><span data-stu-id="f8e5a-140">NuGet will now prompt for files to be overwritten.</span></span>

![Résolution des conflits de fichier](./media/NuGet-2.8/webmatrix-overwrite-file.png)
