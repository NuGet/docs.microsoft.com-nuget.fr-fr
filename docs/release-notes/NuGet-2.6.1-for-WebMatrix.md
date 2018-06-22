---
title: NuGet 2.6.1 pour les Notes de publication WebMatrix
description: Notes de publication pour NuGet 2.6.1 pour WebMatrix, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3d767788d348553cbb5cb82c6f70aac1894628c3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818403"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 pour les Notes de publication WebMatrix

[Notes de publication NuGet 2.6](../release-notes/nuget-2.6.md) | [NuGet 2.7 Notes de publication](../release-notes/nuget-2.7.md)

L’équipe NuGet a publié une extension de gestionnaire de Package NuGet de mise à jour pour WebMatrix 26 mars 2014.  Cette mise à jour peut être installé à partir de la [Galerie d’extensions WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) en procédant comme suit :

1. Ouvrez WebMatrix 3
1. Cliquez sur l’icône des Extensions dans le ruban Accueil
1. Sélectionnez l’onglet mises à jour
1. Cliquez pour mettre à jour le Gestionnaire de Package NuGet pour 2.6.1
1. Fermez et redémarrez WebMatrix 3

## <a name="notable-changes"></a>Modifications importantes

Cette extension mise à jour concerne deux des problèmes majeurs à vos utilisateurs ont dû faire face les packages NuGet consommation dans WebMatrix.  La première était une erreur de version de schéma de NuGet et le deuxième un bogue conduisant à la DLL de zéro octet dans le `bin` dossier.

### <a name="nuget-schema-version-error"></a>Erreur de Version du schéma de NuGet

Depuis la publication de WebMatrix 3, les nouvelles fonctionnalités ont été introduites dans NuGet qui nécessitent une nouvelle version de schéma pour les packages NuGet.  Lorsque vous tentez de gérer vos packages NuGet dans votre site web, ces nouveaux packages peuvent entraîner des erreurs que vous voyez dans WebMatrix.

![Une erreur s'est produite. La version du schéma est incompatible. Mettez à niveau NuGet vers la dernière version.](./media/NuGet-2.8/webmatrix-schema-version.png)

Cette nouvelle version assure la compatibilité avec les packages NuGet les plus récents, empêcher cette erreur ne se produise. Nouvelles versions des packages, y compris Microsoft.AspNet.WebPages peuvent désormais être installées dans WebMatrix.  Certaines de ces packages ont été à l’aide des fonctionnalités de NuGet comme [XDT config transforme](../release-notes/nuget-2.6.md#xdt), qui n’a pas été pris en charge dans WebMatrix jusqu'à présent.

### <a name="zero-byte-dlls-in-bin-folder"></a>DLL de zéro octet dans l’emplacement de dossier

Certains utilisateurs ont indiqué qu’une fois l’installation de NuGet empaquette dans WebMatrix qui incluent des DLL qui sont copiés à l’emplacement que l’émission de la DLL dans le `bin` dossier en tant que fichiers de 0 octet.  Cela arrête l’application lors de l’exécution.

[Ce problème](https://nuget.codeplex.com/workitem/4060) a maintenant été corrigé.

## <a name="other-recent-improvements"></a>Autres améliorations récentes

Lorsque le Gestionnaire de Package NuGet 2.8 a été lancé pour Visual Studio, nous avons publié également le Gestionnaire de Package NuGet 2.5.0 pour WebMatrix.  Alors que cela a été mentionné dans le [notes de mise à jour de NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nous n’a pas de mentionner les nouvelles fonctionnalités spécifiques cette mise à jour introduit.

### <a name="update-all"></a>Tout mettre à jour

Vous pouvez maintenant mettre à jour tous les packages de votre site web en une seule étape !  Lorsque vous ouvrez l’extension NuGet dans WebMatrix, vous consultez la liste de tous les packages dans la galerie, ces derniers sont installés et celles avec les mises à jour disponibles.  Auparavant, chaque package devra être mis à jour individuellement, mais il existe désormais un bouton « Mise à jour toutes les » utile qui s’affiche sous l’onglet mises à jour.

![Cliquez sur tout mettre à jour pour mettre à jour tous les packages de mises à jour disponibles](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Remplacer les fichiers existants

Lors de l’installation des packages qui contiennent les fichiers qui existent déjà dans votre site web, NuGet a toujours uniquement en mode silencieux les fichiers ignorés (toucher vos fichiers existants).  Cela peut entraîner l’impression qu’un package a été installé ou mis à jour correctement lorsque en fait qu’il n’a pas été.  NuGet va maintenant demander pour les fichiers doivent être remplacées.

![Résolution des conflits de fichier](./media/NuGet-2.8/webmatrix-overwrite-file.png)
