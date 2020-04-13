---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496063"
---
<span data-ttu-id="662be-101">Les erreurs de la commande `push` signalent généralement le problème.</span><span class="sxs-lookup"><span data-stu-id="662be-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="662be-102">Par exemple, vous avez peut-être oublié de mettre à jour le numéro de version de votre projet et, par conséquent, vous essayez de publier un package qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="662be-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="662be-103">Des erreurs s’affichent également lorsque vous tentez de publier un package à l’aide d’un identificateur qui existe déjà sur l’hôte.</span><span class="sxs-lookup"><span data-stu-id="662be-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="662be-104">Le nom « AppLogger », par exemple, existe déjà.</span><span class="sxs-lookup"><span data-stu-id="662be-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="662be-105">Dans ce cas, la commande `push` génère l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="662be-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="662be-106">Si vous utilisez une clé API valide que vous venez de créer, ce message indique un conflit d’affectation de nom, ce qui n’est pas évident dans la partie « autorisation » de l’erreur.</span><span class="sxs-lookup"><span data-stu-id="662be-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="662be-107">Modifiez l’identificateur de package, régénérez le projet, recréez le fichier `.nupkg`, puis réexécutez la commande `push`.</span><span class="sxs-lookup"><span data-stu-id="662be-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>