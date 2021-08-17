---
title: lisez-moi du Package sur NuGet. org
description: explication détaillée de la façon dont les fichiers lisez-moi dans NuGet. org sont rendus et que faire lorsque vous rencontrez des problèmes.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: ac0e89c1f5ef9eb19c29646bcc76bcb0b460c5cd
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209941"
---
# <a name="package-readme-on-nugetorg"></a>lisez-moi du Package sur NuGet. org

[ajoutez un fichier lisez-moi dans votre package NuGet](/nuget/reference/msbuild-targets#packagereadmefile) pour rendre les détails de votre package plus riches et plus instructifs pour vos utilisateurs.

il s’agit probablement de l’un des premiers éléments que les utilisateurs voient lorsqu’ils affichent la page de détails de votre package sur NuGet. org et qui est essentiel pour une bonne impression !

> [!IMPORTANT]
> NuGet. org prend uniquement en charge les fichiers lisez-moi dans la [démarque](https://daringfireball.net/projects/markdown/) et les images d’un ensemble limité de domaines. consultez nos [domaines autorisés pour les images](#allowed-domains-for-images-and-badges) et les [fonctionnalités prises en charge](#supported-markdown-features) pour vous assurer que votre fichier lisez-moi est correctement rendu sur NuGet. org.

## <a name="what-should-my-readme-include"></a>Que dois-je inclure dans mon fichier Lisez-moi ?

Pensez à inclure les éléments suivants dans votre fichier Lisez-moi :
* Une introduction à ce que fait votre package et quels sont les problèmes qu’il peut résoudre ?
* Comment prendre en main votre package-existe-t-il des exigences spécifiques ?
* Liens vers une documentation plus complète s’il n’est pas inclus dans le fichier Lisez-moi lui-même.
* Au moins quelques extraits de code/exemples ou images d’exemple.
* Où et comment conserver des commentaires tels que le lien vers les problèmes de projet, Twitter, le suivi des bogues ou une autre plateforme.
* Comment contribuer, le cas échéant.

Gardez à l’esprit que les fichiers Lisez-moi de haute qualité peuvent se trouver dans un large éventail de formats, de formes et de tailles ! si vous disposez déjà d’un package sur NuGet. org, il est probable que vous disposiez déjà d’un `readme.md` fichier ou d’un autre fichier de documentation dans votre référentiel, ce qui constitue un excellent ajout à la page de détails de NuGet. org.

## <a name="preview-your-readme"></a>Afficher un aperçu de votre fichier Lisez-moi

pour afficher un aperçu de votre fichier lisez-moi avant qu’il ne soit en ligne sur NuGet. org, téléchargez votre package à l’aide du [portail web du package Télécharger sur NuGet. org](/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) et faites défiler jusqu’à la section « fichier lisez-moi » de l’aperçu des métadonnées. Il doit se présenter comme suit :

![Aperçu du fichier Lisez-moi](media\readme-upload-preview.PNG)

Prenez le temps de passer en revue et d’afficher un aperçu de votre fichier Lisez-moi pour [la conformité des images](#allowed-domains-for-images-and-badges) et la [mise en forme prise en charge](#supported-markdown-features) pour vous assurer qu’il donne une bonne première impression aux utilisateurs potentiels. pour corriger les erreurs dans le fichier lisez-moi du package une fois qu’il est publié dans NuGet. org, vous devez transmettre une version de package mise à jour avec le correctif. S’assurer que tout semble correct à l’avance peut vous faire gagner du soucis.
## <a name="allowed-domains-for-images-and-badges"></a>Domaines autorisés pour les images et les badges

en raison des préoccupations en matière de sécurité et de confidentialité, NuGet. org limite les domaines à partir desquels les images et les badges peuvent être rendus aux hôtes approuvés. 

NuGet. org autorise le rendu de toutes les images, y compris les badges, à partir des domaines approuvés suivants :
* api.bintray.com
* api.codacy.com
* app.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* cdn.jsdelivr.net
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* i.imgur.com
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Si vous pensez qu’un autre domaine doit être ajouté à la liste verte, n’hésitez pas à [Envoyer un problème](https://github.com/NuGet/NuGetGallery/issues) et il sera revu par notre équipe d’ingénierie pour la confidentialité et la conformité de la sécurité. Les images avec des chemins d’accès locaux relatifs et des images hébergées à partir de domaines non pris en charge ne sont pas rendues et génèrent un avertissement sur la page Aperçu du fichier Lisez-moi et Détails du package qui est uniquement visible par les propriétaires du package.

## <a name="supported-markdown-features"></a>Fonctionnalités de démarque prises en charge
[Markdown](https://daringfireball.net/projects/markdown/) est un langage de balisage léger avec une syntaxe de mise en forme en texte brut. NuGet. les fichiers lisez-moi de l’org prennent en charge la démarque conforme à [CommonMark](https://commonmark.org/) via le moteur d’analyse [Markdig](https://github.com/lunet-io/markdig) .

NuGet. org prend actuellement en charge les fonctionnalités de démarque suivantes :
* [En-têtes](https://spec.commonmark.org/0.29/#atx-headings)
* [Images](https://spec.commonmark.org/0.29/#images)
* [Accentuation supplémentaire](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Listes](https://spec.commonmark.org/0.29/#lists)
* [Liens](https://spec.commonmark.org/0.29/#links)
* [Citation](https://spec.commonmark.org/0.29/#block-quotes)
* [Barres obliques inverses](https://spec.commonmark.org/0.29/#backslash-escapes)
* [Étendues de code](https://spec.commonmark.org/0.29/#code-spans)
* [Listes des tâches](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Tables](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Emojis](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Liaisons automatiques](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

