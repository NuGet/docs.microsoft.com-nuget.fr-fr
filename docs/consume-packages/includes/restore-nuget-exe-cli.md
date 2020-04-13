---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860579"
---
Utilisez la commande [restore](../../reference/cli-reference/cli-ref-restore.md), qui télécharge et installe tous les packages manquants dans le dossier *packages*.

Pour les projets migrés vers PackageReference, utilisez [msbuild-t:restore](../package-restore.md#restore-using-msbuild) à la place pour restaurer les packages.

La commande `restore` ajoute seulement les packages sur le disque, sans changer les dépendances du projet. Pour restaurer les dépendances du projet, modifiez `packages.config`, puis utilisez la commande `restore`.

Comme avec les autres commandes CLI `nuget.exe`, ouvrez d’abord une ligne de commande et accédez au répertoire contenant votre fichier projet.

Pour restaurer un package à l’aide de la commande `restore` :

```cli
nuget restore MySolution.sln
```