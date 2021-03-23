---
ms.openlocfilehash: 585537c5e3c7b27e0c7c312db19723d952421ce3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859557"
---
Aucune contribution n’est trop grande ou trop petite.

1. Accédez à la page à modifier sur [docs.Microsoft.com/NuGet](https://docs.microsoft.com/nuget/), puis cliquez sur le bouton **modifier** en haut à droite. Cela vous amène à la page de démarque appropriée dans le référentiel.
1. Modifiez la démarque :
    1. Si vous incluez des images (utilisez des fichiers PNG, en général), placez-les dans le dossier du média qui se trouve dans le dossier de la rubrique. Les liens sont alors `media/<image_name>.png` .
    1. Les liens relatifs vers d’autres pages de ce docset doivent se présenter sous la forme `../<folder>/<topic-file>.md` , y compris la formation `.md` . Si vous établissez un lien vers une autre rubrique dans le même dossier, vous `../<folder>/` pouvez l’omettre. Quand vous utilisez des ancres, pensez toujours à inclure le `.md` avant le `#` .
    1. Lorsque vous utilisez des liens externes, en particulier pour docs.microsoft.com (ou msdn.microsoft.com pour tout contenu plus ancien), omettez toute balise de langue comme « en-US » afin qu’un lecteur dans une autre langue se trouve sur une page cible dans la même langue si elle est disponible.
1. Lorsque vous avez terminé, entrez un message de validation ci-dessous, puis cliquez sur **proposer une modification de fichier**.
1. Envoyez une demande de tirage (pull request) pour votre modification. Nous examinons la variable PRs régulièrement.
1. Merci !

Si vous créez une nouvelle rubrique, gardez également à l’esprit les points suivants :

1. Placez toujours la nouvelle rubrique dans un sous-dossier approprié et suivez les conventions pour les noms de fichiers, car vous les voyez utilisées ici.
1. Vous devez inclure un bloc de métadonnées comme vous pouvez le voir dans d’autres rubriques. Les valeurs par défaut standard (par exemple, pour ms. Workload et ms. Reviewer) sont définies dans docs/docjx.js. vous n’avez donc besoin de modifier que les éléments suivants :

  - titre : titre qui apparaît dans les résultats de la recherche. Pour SEO, cet idéal n’est pas le même que le # (H1) de niveau supérieur de l’article.
  - Description : Résumé de l’article qui apparaît dans les résultats de la recherche.
  - Auteur : ID GitHub de l’auteur auquel les fichiers de problèmes de cet article sont affectés.
  - ms. Author : si l’auteur est un employé de Microsoft, il s’agit de l’alias Microsoft. Utilisé pour la création de rapports et le transfert de commentaires à partir d’autres canaux.
  - Manager : alias Microsoft du responsable de l’auteur, le cas échéant.
  - ms. Date : date de la dernière révision ou révision de l’article au format mm/jj/aaaa (utilisez des zéros non significatifs). Il s’agit d’une communication avec le lecteur à propos de l’actualisation. il n’est donc pas mis à jour pour des modifications mineures, uniquement pour des révisions plus importantes ou lorsque l’article a été revérifié, même si aucune modification n’est apportée.
  - ms. topic : permet de catégoriser l’article dans les rapports. Consultez le tableau ci-dessous. La plupart des articles sont « conceptuels ». 
1. Outre l’ajout de votre page, modifiez docs/TOC. MD pour ajouter un lien vers cette page.
1. Si vous ajoutez un nœud de niveau supérieur à la table des matières, créez également une entrée pour celui-ci dans docs/index. MD.

| ms. Topic (catégorie) | Description |
| --- | --- |
| conceptuel | Utilisez pour tout contenu qui ne fait pas partie d’un autre. Cette valeur est définie par défaut dans docfx.js. |
| vue d'ensemble | À utiliser pour les Articles de présentation ou de guide de l’utilisateur, en général uniquement ceux qui résident sous un nœud « vue d’ensemble » dans la table des matières. |
| démarrage rapide | Tout ce qui se trouve sous le nœud « démarrage rapide » dans la table des matières créée conformément aux instructions de démarrage rapide. |
| didacticiel | Tout ce qui se trouve sous le nœud « didacticiel » de la table des matières est créé conformément aux instructions du didacticiel. |
| reference | Tout article de type référence qui n’est pas généré automatiquement. |
| article | À utiliser pour le contenu fourni par la Communauté (c’est-à-dire tout ce qui provient de l’extérieur de l’équipe d’ingénierie ou de l’équipe de documentation de Microsoft). |
