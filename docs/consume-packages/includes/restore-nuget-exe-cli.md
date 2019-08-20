---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2019
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