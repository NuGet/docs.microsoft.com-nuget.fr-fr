---
title: Lisez-moi du package sur NuGet.org
description: Explication détaillée du rendu des fichiers Lisez-moi sur NuGet.org et de la procédure à suivre lorsque vous rencontrez des problèmes.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902247"
---
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="0f512-103">Lisez-moi du package sur NuGet.org</span><span class="sxs-lookup"><span data-stu-id="0f512-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="0f512-104">[Incluez un fichier Lisez-moi dans votre package NuGet](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) pour rendre les détails de votre package plus riches et plus instructifs pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0f512-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="0f512-105">Il s’agit probablement de l’un des premiers éléments que les utilisateurs verront lorsqu’ils affichent la page de détails de votre package sur NuGet.org et sont essentiels pour faire une bonne impression !</span><span class="sxs-lookup"><span data-stu-id="0f512-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f512-106">NuGet.org prend uniquement en charge les fichiers Lisez-moi dans la [démarque](https://daringfireball.net/projects/markdown/) et les images d’un ensemble limité de domaines.</span><span class="sxs-lookup"><span data-stu-id="0f512-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="0f512-107">Consultez nos [domaines autorisés pour les images](#allowed-domains-for-images-and-badges) et les [fonctionnalités prises en charge](#supported-markdown-features) pour vous assurer que votre fichier Lisez-moi est correctement rendu sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="0f512-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="0f512-108">Que dois-je inclure dans mon fichier Lisez-moi ?</span><span class="sxs-lookup"><span data-stu-id="0f512-108">What should my readme include?</span></span>

<span data-ttu-id="0f512-109">Pensez à inclure les éléments suivants dans votre fichier Lisez-moi :</span><span class="sxs-lookup"><span data-stu-id="0f512-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="0f512-110">Une introduction à ce que fait votre package et quels sont les problèmes qu’il peut résoudre ?</span><span class="sxs-lookup"><span data-stu-id="0f512-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="0f512-111">Comment prendre en main votre package-existe-t-il des exigences spécifiques ?</span><span class="sxs-lookup"><span data-stu-id="0f512-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="0f512-112">Liens vers une documentation plus complète s’il n’est pas inclus dans le fichier Lisez-moi lui-même.</span><span class="sxs-lookup"><span data-stu-id="0f512-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="0f512-113">Au moins quelques extraits de code/exemples ou images d’exemple.</span><span class="sxs-lookup"><span data-stu-id="0f512-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="0f512-114">Où et comment conserver des commentaires tels que le lien vers les problèmes de projet, Twitter, le suivi des bogues ou une autre plateforme.</span><span class="sxs-lookup"><span data-stu-id="0f512-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="0f512-115">Comment contribuer, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="0f512-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="0f512-116">Gardez à l’esprit que les fichiers Lisez-moi de haute qualité peuvent se trouver dans un large éventail de formats, de formes et de tailles !</span><span class="sxs-lookup"><span data-stu-id="0f512-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="0f512-117">Si vous disposez déjà d’un package sur NuGet.org, il est probable que vous disposiez déjà d’un `readme.md` fichier ou d’un autre fichier de documentation dans votre référentiel, ce qui constitue un excellent ajout à la page de détails de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="0f512-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="0f512-118">Afficher un aperçu de votre fichier Lisez-moi</span><span class="sxs-lookup"><span data-stu-id="0f512-118">Preview your readme</span></span>

<span data-ttu-id="0f512-119">Pour afficher un aperçu de votre fichier Lisez-moi avant qu’il ne soit en ligne sur NuGet.org, téléchargez votre package à l’aide du [portail Web Télécharger le package sur NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) et faites défiler jusqu’à la section « fichier Lisez-moi » de l’aperçu des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="0f512-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="0f512-120">Il doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f512-120">It should look something like this:</span></span>

![Aperçu du fichier Lisez-moi](media\readme-upload-preview.PNG)

<span data-ttu-id="0f512-122">Prenez le temps de passer en revue et d’afficher un aperçu de votre fichier Lisez-moi pour [la conformité des images](#allowed-domains-for-images-and-badges) et la [mise en forme prise en charge](#supported-markdown-features) pour vous assurer qu’il donne une bonne première impression aux utilisateurs potentiels.</span><span class="sxs-lookup"><span data-stu-id="0f512-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="0f512-123">Pour corriger les erreurs dans le fichier Lisez-moi du package une fois qu’il est publié sur NuGet.org, vous devez envoyer une version de package mise à jour avec le correctif.</span><span class="sxs-lookup"><span data-stu-id="0f512-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="0f512-124">S’assurer que tout semble correct à l’avance peut vous faire gagner du soucis.</span><span class="sxs-lookup"><span data-stu-id="0f512-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="0f512-125">Domaines autorisés pour les images et les badges</span><span class="sxs-lookup"><span data-stu-id="0f512-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="0f512-126">En raison des préoccupations en matière de sécurité et de confidentialité, NuGet.org restreint les domaines à partir desquels les images et les badges peuvent être rendus aux hôtes approuvés.</span><span class="sxs-lookup"><span data-stu-id="0f512-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="0f512-127">NuGet.org autorise le rendu de toutes les images, y compris les badges, à partir des domaines approuvés suivants :</span><span class="sxs-lookup"><span data-stu-id="0f512-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="0f512-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="0f512-128">api.bintray.com</span></span>
* <span data-ttu-id="0f512-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="0f512-129">api.codacy.com</span></span>
* <span data-ttu-id="0f512-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="0f512-130">api.codeclimate.com</span></span>
* <span data-ttu-id="0f512-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="0f512-131">api.dependabot.com</span></span>
* <span data-ttu-id="0f512-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="0f512-132">api.travis-ci.com</span></span>
* <span data-ttu-id="0f512-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="0f512-133">api.travis-ci.org</span></span>
* <span data-ttu-id="0f512-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="0f512-134">app.fossa.io</span></span>
* <span data-ttu-id="0f512-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="0f512-135">badge.fury.io</span></span>
* <span data-ttu-id="0f512-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="0f512-136">badgen.net</span></span>
* <span data-ttu-id="0f512-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="0f512-137">badges.gitter.im</span></span>
* <span data-ttu-id="0f512-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="0f512-138">bettercodehub.com</span></span>
* <span data-ttu-id="0f512-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="0f512-139">buildstats.info</span></span>
* <span data-ttu-id="0f512-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="0f512-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="0f512-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="0f512-141">ci.appveyor.com</span></span>
* <span data-ttu-id="0f512-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="0f512-142">circleci.com</span></span>
* <span data-ttu-id="0f512-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="0f512-143">codecov.io</span></span>
* <span data-ttu-id="0f512-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="0f512-144">codefactor.io</span></span>
* <span data-ttu-id="0f512-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="0f512-145">coveralls.io</span></span>
* <span data-ttu-id="0f512-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="0f512-146">dev.azure.com</span></span>
* <span data-ttu-id="0f512-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="0f512-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="0f512-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="0f512-148">gitlab.com</span></span>
* <span data-ttu-id="0f512-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="0f512-149">img.shields.io</span></span>
* <span data-ttu-id="0f512-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="0f512-150">isitmaintained.com</span></span>
* <span data-ttu-id="0f512-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="0f512-151">opencollective.com</span></span>
* <span data-ttu-id="0f512-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="0f512-152">raw.github.com</span></span>
* <span data-ttu-id="0f512-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="0f512-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="0f512-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="0f512-154">snyk.io</span></span>
* <span data-ttu-id="0f512-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="0f512-155">sonarcloud.io</span></span>
* <span data-ttu-id="0f512-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="0f512-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="0f512-157">Si vous pensez qu’un autre domaine doit être ajouté à la liste verte, n’hésitez pas à [Envoyer un problème](https://github.com/NuGet/NuGetGallery/issues) et il sera revu par notre équipe d’ingénierie pour la confidentialité et la conformité de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f512-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="0f512-158">Les images avec des chemins d’accès locaux relatifs et des images hébergées à partir de domaines non pris en charge ne sont pas rendues et génèrent un avertissement sur la page Aperçu du fichier Lisez-moi et Détails du package qui est uniquement visible par les propriétaires du package.</span><span class="sxs-lookup"><span data-stu-id="0f512-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="0f512-159">Fonctionnalités de démarque prises en charge</span><span class="sxs-lookup"><span data-stu-id="0f512-159">Supported Markdown features</span></span>
<span data-ttu-id="0f512-160">[Markdown](https://daringfireball.net/projects/markdown/) est un langage de balisage léger avec une syntaxe de mise en forme en texte brut.</span><span class="sxs-lookup"><span data-stu-id="0f512-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="0f512-161">Les fichiers Lisez-moi NuGet.org prennent en charge la démarque [CommonMark](https://commonmark.org/) avec le moteur d’analyse [Markdig](https://github.com/lunet-io/markdig) .</span><span class="sxs-lookup"><span data-stu-id="0f512-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="0f512-162">NuGet.org prend actuellement en charge les fonctionnalités de démarque suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f512-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="0f512-163">En-têtes</span><span class="sxs-lookup"><span data-stu-id="0f512-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="0f512-164">Images</span><span class="sxs-lookup"><span data-stu-id="0f512-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="0f512-165">Accentuation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="0f512-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="0f512-166">Listes</span><span class="sxs-lookup"><span data-stu-id="0f512-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="0f512-167">Liens</span><span class="sxs-lookup"><span data-stu-id="0f512-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="0f512-168">Citation</span><span class="sxs-lookup"><span data-stu-id="0f512-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="0f512-169">Barres obliques inverses</span><span class="sxs-lookup"><span data-stu-id="0f512-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="0f512-170">Étendues de code</span><span class="sxs-lookup"><span data-stu-id="0f512-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="0f512-171">Listes des tâches</span><span class="sxs-lookup"><span data-stu-id="0f512-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="0f512-172">Tables</span><span class="sxs-lookup"><span data-stu-id="0f512-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="0f512-173">Emojis</span><span class="sxs-lookup"><span data-stu-id="0f512-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="0f512-174">Liaisons automatiques</span><span class="sxs-lookup"><span data-stu-id="0f512-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

