---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496063"
---
Les erreurs de la commande `push` signalent généralement le problème. Par exemple, vous avez peut-être oublié de mettre à jour le numéro de version de votre projet et, par conséquent, vous essayez de publier un package qui existe déjà.

Des erreurs s’affichent également lorsque vous tentez de publier un package à l’aide d’un identificateur qui existe déjà sur l’hôte. Le nom « AppLogger », par exemple, existe déjà. Dans ce cas, la commande `push` génère l’erreur suivante :

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Si vous utilisez une clé API valide que vous venez de créer, ce message indique un conflit d’affectation de nom, ce qui n’est pas évident dans la partie « autorisation » de l’erreur. Modifiez l’identificateur de package, régénérez le projet, recréez le fichier `.nupkg`, puis réexécutez la commande `push`.