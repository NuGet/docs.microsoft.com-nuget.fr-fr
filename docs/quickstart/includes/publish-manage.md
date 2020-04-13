---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495941"
---
À partir de votre profil sur nuget.org, sélectionnez **Manage Packages** (Gérer les packages) pour voir celui que vous venez de publier. Vous recevrez aussi un e-mail de confirmation. Notez que l’indexation de votre package et son apparition dans les résultats de la recherche peuvent prendre un certain temps. Pendant ce temps, la page de votre package contient le message ci-dessous :

![This package has not been indexed yet. (Ce package n’a pas encore été indexé.) It will appear in search results and will be available for install/restore after indexing is complete. (Il apparaîtra dans les résultats de la recherche et sera disponible pour l’installation/restauration une fois l’indexation terminée.)](../media/QS_Create-03-NotIndexed.png)

Et le tour est joué ! Vous venez de publier votre premier package NuGet sur nuget.org. D’autres développeurs peuvent maintenant l’utiliser dans leurs propres projets.

Si, dans cette procédure pas à pas, vous avez créé un package qui n’est pas réellement utile (par exemple, un package créé avec une bibliothèque de classes vide), vous devez *retirer de la liste* le package pour le masquer dans les résultats de la recherche :

1. Sur nuget.org, choisissez votre nom d’utilisateur (en haut à droite de la page), puis sélectionnez **Gérer les packages**.

1. Recherchez le package que vous souhaitez retirer de la liste sous **Publié** puis sélectionnez l’icône Corbeille à droite :

    ![Icône Corbeille affichée pour un package répertorié sur nuget.org](../media/qs_create-vs-03-trash-can.png)

1. Sur la page suivante, désactivez la case **Liste (nom du package) dans les résultats de la recherche** puis sélectionnez **Enregistrer** :

    ![Désactivation de la case à cocher Liste pour un package sur nuget.org](../media/qs_create-vs-04-unlist.png)