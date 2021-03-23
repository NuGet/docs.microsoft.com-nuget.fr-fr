---
ms.openlocfilehash: 585537c5e3c7b27e0c7c312db19723d952421ce3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859557"
---
<span data-ttu-id="434e7-101">Aucune contribution n’est trop grande ou trop petite.</span><span class="sxs-lookup"><span data-stu-id="434e7-101">No contribution is too big or too small.</span></span>

1. <span data-ttu-id="434e7-102">Accédez à la page à modifier sur [docs.Microsoft.com/NuGet](https://docs.microsoft.com/nuget/), puis cliquez sur le bouton **modifier** en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="434e7-102">Visit the page to edit on [docs.microsoft.com/nuget](https://docs.microsoft.com/nuget/), then click the **Edit** button on the top right.</span></span> <span data-ttu-id="434e7-103">Cela vous amène à la page de démarque appropriée dans le référentiel.</span><span class="sxs-lookup"><span data-stu-id="434e7-103">This brings you to the appropriate markdown page in the repo.</span></span>
1. <span data-ttu-id="434e7-104">Modifiez la démarque :</span><span class="sxs-lookup"><span data-stu-id="434e7-104">Edit the markdown:</span></span>
    1. <span data-ttu-id="434e7-105">Si vous incluez des images (utilisez des fichiers PNG, en général), placez-les dans le dossier du média qui se trouve dans le dossier de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="434e7-105">If you're including images (use PNGs, generally), place them in the media folder that's in the topic's folder.</span></span> <span data-ttu-id="434e7-106">Les liens sont alors `media/<image_name>.png` .</span><span class="sxs-lookup"><span data-stu-id="434e7-106">Links are then `media/<image_name>.png`.</span></span>
    1. <span data-ttu-id="434e7-107">Les liens relatifs vers d’autres pages de ce docset doivent se présenter sous la forme `../<folder>/<topic-file>.md` , y compris la formation `.md` .</span><span class="sxs-lookup"><span data-stu-id="434e7-107">Relative links to other pages in this docset should be in the form `../<folder>/<topic-file>.md` including the training `.md`.</span></span> <span data-ttu-id="434e7-108">Si vous établissez un lien vers une autre rubrique dans le même dossier, vous `../<folder>/` pouvez l’omettre.</span><span class="sxs-lookup"><span data-stu-id="434e7-108">If you're linking to another topic in the same folder, then `../<folder>/` can be omitted.</span></span> <span data-ttu-id="434e7-109">Quand vous utilisez des ancres, pensez toujours à inclure le `.md` avant le `#` .</span><span class="sxs-lookup"><span data-stu-id="434e7-109">When using anchors, always remember to include the `.md` before the `#`.</span></span>
    1. <span data-ttu-id="434e7-110">Lorsque vous utilisez des liens externes, en particulier pour docs.microsoft.com (ou msdn.microsoft.com pour tout contenu plus ancien), omettez toute balise de langue comme « en-US » afin qu’un lecteur dans une autre langue se trouve sur une page cible dans la même langue si elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="434e7-110">When using external links, especially to docs.microsoft.com (or msdn.microsoft.com for any older content), omit any language tag like "en-us" so that a reader in another language lands on a target page in that same language if it's available.</span></span>
1. <span data-ttu-id="434e7-111">Lorsque vous avez terminé, entrez un message de validation ci-dessous, puis cliquez sur **proposer une modification de fichier**.</span><span class="sxs-lookup"><span data-stu-id="434e7-111">When you're done, enter a commit message below, and click **Propose file change**.</span></span>
1. <span data-ttu-id="434e7-112">Envoyez une demande de tirage (pull request) pour votre modification.</span><span class="sxs-lookup"><span data-stu-id="434e7-112">Send a pull request for your change.</span></span> <span data-ttu-id="434e7-113">Nous examinons la variable PRs régulièrement.</span><span class="sxs-lookup"><span data-stu-id="434e7-113">We review PRs on a regular basis.</span></span>
1. <span data-ttu-id="434e7-114">Merci !</span><span class="sxs-lookup"><span data-stu-id="434e7-114">Thank you!</span></span>

<span data-ttu-id="434e7-115">Si vous créez une nouvelle rubrique, gardez également à l’esprit les points suivants :</span><span class="sxs-lookup"><span data-stu-id="434e7-115">If you're creating a new topic, keep the following in mind as well:</span></span>

1. <span data-ttu-id="434e7-116">Placez toujours la nouvelle rubrique dans un sous-dossier approprié et suivez les conventions pour les noms de fichiers, car vous les voyez utilisées ici.</span><span class="sxs-lookup"><span data-stu-id="434e7-116">Always place the new topic in an appropriate subfolder, and follow the conventions for filenames as you see them used here.</span></span>
1. <span data-ttu-id="434e7-117">Vous devez inclure un bloc de métadonnées comme vous pouvez le voir dans d’autres rubriques.</span><span class="sxs-lookup"><span data-stu-id="434e7-117">You must include a metadata block as you see on other topics.</span></span> <span data-ttu-id="434e7-118">Les valeurs par défaut standard (par exemple, pour ms. Workload et ms. Reviewer) sont définies dans docs/docjx.js. vous n’avez donc besoin de modifier que les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="434e7-118">Typical defaults (such as for ms.workload and ms.reviewer) are set within docs/docjx.json, so you need only change the following:</span></span>

  - <span data-ttu-id="434e7-119">titre : titre qui apparaît dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="434e7-119">title: The title that appears in search results.</span></span> <span data-ttu-id="434e7-120">Pour SEO, cet idéal n’est pas le même que le # (H1) de niveau supérieur de l’article.</span><span class="sxs-lookup"><span data-stu-id="434e7-120">For SEO, this ideally isn't the same as the top-level # (H1) of the article.</span></span>
  - <span data-ttu-id="434e7-121">Description : Résumé de l’article qui apparaît dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="434e7-121">description: The abstract of the article that appears in search results.</span></span>
  - <span data-ttu-id="434e7-122">Auteur : ID GitHub de l’auteur auquel les fichiers de problèmes de cet article sont affectés.</span><span class="sxs-lookup"><span data-stu-id="434e7-122">author: the author's GitHub ID, to which issues files for this article are assigned.</span></span>
  - <span data-ttu-id="434e7-123">ms. Author : si l’auteur est un employé de Microsoft, il s’agit de l’alias Microsoft.</span><span class="sxs-lookup"><span data-stu-id="434e7-123">ms.author: if the author is a Microsoft employee, this is the Microsoft alias.</span></span> <span data-ttu-id="434e7-124">Utilisé pour la création de rapports et le transfert de commentaires à partir d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="434e7-124">Used for reporting and forwarding feedback from other channels.</span></span>
  - <span data-ttu-id="434e7-125">Manager : alias Microsoft du responsable de l’auteur, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="434e7-125">manager: Microsoft alias of the author's manager, if applicable.</span></span>
  - <span data-ttu-id="434e7-126">ms. Date : date de la dernière révision ou révision de l’article au format mm/jj/aaaa (utilisez des zéros non significatifs).</span><span class="sxs-lookup"><span data-stu-id="434e7-126">ms.date: the date of the last revision or review of the article in mm/dd/yyyy format (use leading zeros).</span></span> <span data-ttu-id="434e7-127">Il s’agit d’une communication avec le lecteur à propos de l’actualisation. il n’est donc pas mis à jour pour des modifications mineures, uniquement pour des révisions plus importantes ou lorsque l’article a été revérifié, même si aucune modification n’est apportée.</span><span class="sxs-lookup"><span data-stu-id="434e7-127">This is a communication to the reader about freshness, so it's not updated for minor changes, only for more significant revisions OR when the article has reverified even if there are no changes.</span></span>
  - <span data-ttu-id="434e7-128">ms. topic : permet de catégoriser l’article dans les rapports.</span><span class="sxs-lookup"><span data-stu-id="434e7-128">ms.topic: used to categorize the article in reports.</span></span> <span data-ttu-id="434e7-129">Consultez le tableau ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="434e7-129">See table below.</span></span> <span data-ttu-id="434e7-130">La plupart des articles sont « conceptuels ».</span><span class="sxs-lookup"><span data-stu-id="434e7-130">Most articles are "conceptual".</span></span> 
1. <span data-ttu-id="434e7-131">Outre l’ajout de votre page, modifiez docs/TOC. MD pour ajouter un lien vers cette page.</span><span class="sxs-lookup"><span data-stu-id="434e7-131">In addition to adding your page, edit docs/TOC.md to add a link to that page.</span></span>
1. <span data-ttu-id="434e7-132">Si vous ajoutez un nœud de niveau supérieur à la table des matières, créez également une entrée pour celui-ci dans docs/index. MD.</span><span class="sxs-lookup"><span data-stu-id="434e7-132">If you're adding a top-level node to the TOC, also make an entry for it in docs/index.md.</span></span>

| <span data-ttu-id="434e7-133">ms. Topic (catégorie)</span><span class="sxs-lookup"><span data-stu-id="434e7-133">ms.topic category</span></span> | <span data-ttu-id="434e7-134">Description</span><span class="sxs-lookup"><span data-stu-id="434e7-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="434e7-135">conceptuel</span><span class="sxs-lookup"><span data-stu-id="434e7-135">conceptual</span></span> | <span data-ttu-id="434e7-136">Utilisez pour tout contenu qui ne fait pas partie d’un autre.</span><span class="sxs-lookup"><span data-stu-id="434e7-136">Use for any content that doesn't fall into another.</span></span> <span data-ttu-id="434e7-137">Cette valeur est définie par défaut dans docfx.js.</span><span class="sxs-lookup"><span data-stu-id="434e7-137">This is set as the default in docfx.json.</span></span> |
| <span data-ttu-id="434e7-138">vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="434e7-138">overview</span></span> | <span data-ttu-id="434e7-139">À utiliser pour les Articles de présentation ou de guide de l’utilisateur, en général uniquement ceux qui résident sous un nœud « vue d’ensemble » dans la table des matières.</span><span class="sxs-lookup"><span data-stu-id="434e7-139">Use for any overview or user-guide articles, typically only those that live under an "Overview" node in the TOC.</span></span> |
| <span data-ttu-id="434e7-140">démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="434e7-140">quickstart</span></span> | <span data-ttu-id="434e7-141">Tout ce qui se trouve sous le nœud « démarrage rapide » dans la table des matières créée conformément aux instructions de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="434e7-141">Anything under the "Quickstart" node in the TOC that's authored according to Quickstart guidelines.</span></span> |
| <span data-ttu-id="434e7-142">didacticiel</span><span class="sxs-lookup"><span data-stu-id="434e7-142">tutorial</span></span> | <span data-ttu-id="434e7-143">Tout ce qui se trouve sous le nœud « didacticiel » de la table des matières est créé conformément aux instructions du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="434e7-143">Anything under the "Tutorial" node in the TOC that's authored according to Tutorial guidelines.</span></span> |
| <span data-ttu-id="434e7-144">reference</span><span class="sxs-lookup"><span data-stu-id="434e7-144">reference</span></span> | <span data-ttu-id="434e7-145">Tout article de type référence qui n’est pas généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="434e7-145">Any reference-type article that isn't auto-generated.</span></span> |
| <span data-ttu-id="434e7-146">article</span><span class="sxs-lookup"><span data-stu-id="434e7-146">article</span></span> | <span data-ttu-id="434e7-147">À utiliser pour le contenu fourni par la Communauté (c’est-à-dire tout ce qui provient de l’extérieur de l’équipe d’ingénierie ou de l’équipe de documentation de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="434e7-147">Use for community-contributed content (that is, anything from outside the engineering team or the docs team at Microsoft.</span></span> |