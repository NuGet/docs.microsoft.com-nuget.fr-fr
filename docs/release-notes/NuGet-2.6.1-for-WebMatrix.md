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
# <a name="nuget-261-for-webmatrix-release-notes"></a>Notes de publication de NuGet 2.6.1 pour WebMatrix

Notes de publication de [NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Notes de publication de NuGet 2,7](../release-notes/nuget-2.7.md)

L’équipe NuGet a publié une extension du gestionnaire de package NuGet mise à jour pour WebMatrix le 26 mars 2014.  Cette mise à jour peut être installée à partir de la [Galerie d’extensions WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) en procédant comme suit :

1. Ouvrir WebMatrix 3
1. Cliquez sur l’icône extensions dans le ruban d’hébergement.
1. Sélectionner l’onglet mises à jour
1. Cliquez pour mettre à jour le gestionnaire de package NuGet vers 2.6.1
1. Fermer et redémarrer WebMatrix 3

## <a name="notable-changes"></a>Modifications notables

Cette mise à jour d’extension résout deux des problèmes les plus importants que les utilisateurs ont dû confronter à l’utilisation de packages NuGet dans WebMatrix.  La première était une erreur de version de schéma NuGet et la seconde était un bogue conduisant à des dll de zéro octet dans le `bin` dossier.

### <a name="nuget-schema-version-error"></a>Erreur de version du schéma NuGet

Étant donné que WebMatrix 3 a été publié, de nouvelles fonctionnalités ont été introduites dans NuGet qui nécessitent une nouvelle version de schéma pour les packages NuGet.  Lorsque vous tentez de gérer vos packages NuGet sur votre site Web, ces nouveaux packages peuvent entraîner des erreurs que vous voyez dans WebMatrix.

![Une erreur est survenue. La version du schéma n’est pas compatible. Mettez à niveau NuGet vers la dernière version.](./media/NuGet-2.8/webmatrix-schema-version.png)

Cette dernière version offre une compatibilité avec les packages NuGet les plus récents, ce qui empêche l’apparition de cette erreur. Les nouvelles versions des packages, y compris Microsoft. AspNet. webpages, peuvent désormais être installées dans WebMatrix.  Certains de ces packages utilisaient des fonctionnalités NuGet, telles que des [transformations de configuration xdt](../release-notes/nuget-2.6.md#xdt), qui n’étaient pas prises en charge dans WebMatrix jusqu’à présent.

### <a name="zero-byte-dlls-in-bin-folder"></a>Zero-Byte des dll dans le dossier bin

Certains utilisateurs ont signalé qu’après l’installation des packages NuGet dans WebMatrix qui incluent des dll copiées dans bin, les dll s’affichent dans le `bin` dossier en tant que fichiers de 0 octet.  Cela interrompt l’application au moment de l’exécution.

[Ce problème](https://nuget.codeplex.com/workitem/4060) a été résolu.

## <a name="other-recent-improvements"></a>Autres améliorations récentes

Quand le gestionnaire de package NuGet 2,8 a été publié pour Visual Studio, nous avons également publié le gestionnaire de package NuGet 2.5.0 pour WebMatrix.  Bien que cela ait été mentionné dans les [notes de publication de NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nous n’avons pas mentionné les nouvelles fonctionnalités spécifiques mises à jour introduites.

### <a name="update-all"></a>Tout mettre à jour

Vous pouvez maintenant mettre à jour tous les packages de votre site Web en une seule étape.  Lorsque vous ouvrez l’extension NuGet dans WebMatrix, vous voyez la liste de tous les packages dans la Galerie, ceux installés et ceux avec des mises à jour disponibles.  Auparavant, chaque package devait être mis à jour individuellement, mais il y a maintenant un bouton « mettre à jour tout » utile qui s’affiche sous l’onglet mises à jour.

![Cliquez sur tout mettre à jour pour mettre à jour tous les packages avec les mises à jour disponibles](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Remplacer les fichiers existants

Lors de l’installation de packages contenant des fichiers qui existent déjà sur votre site Web, NuGet a toujours ignoré ces fichiers en mode silencieux (laissant uniquement vos fichiers existants).  Cela peut donner l’impression qu’un package a été installé ou mis à jour correctement en fait.  NuGet va maintenant demander que les fichiers soient remplacés.

![Résolution des conflits de fichiers](./media/NuGet-2.8/webmatrix-overwrite-file.png)
