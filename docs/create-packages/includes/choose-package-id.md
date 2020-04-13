---
ms.openlocfilehash: c92f6e0c34347ee8555d416140d95ea2df5a3fbb
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610550"
---
L’identificateur de package et le numéro de version sont les deux valeurs les plus importantes dans le projet, car ils identifient de façon unique le code exact contenu dans le package.

**Bonnes pratiques en matière d’identificateur de package :**

- **Unicité** : l’identificateur doit être unique sur nuget.org ou dans la galerie qui héberge le package, quelle qu’elle soit. Avant de déterminer un identificateur, faites une recherche dans la galerie applicable pour vérifier si le nom est déjà en cours d’utilisation. Pour éviter les conflits, utilisez le nom de votre société comme première partie de l’identificateur, par exemple `Contoso.`.
- **Noms comme les espaces de noms** : suivez un modèle similaire aux espaces de noms dans .NET, en utilisant la notation à points au lieu de traits d’union. Par exemple, utilisez `Contoso.Utility.UsefulStuff` plutôt que `Contoso-Utility-UsefulStuff` ou `Contoso_Utility_UsefulStuff`. Les consommateurs trouvent également pratique de faire correspondre l’identificateur du package aux espaces de noms utilisés dans le code.
- **Exemples de package** : si vous produisez un package d’exemple de code qui montre comment utiliser un autre package, attachez `.Sample` comme suffixe à l’identificateur, comme dans `Contoso.Utility.UsefulStuff.Sample`. (Le paquet d’échantillons dépendrait bien sûr de l’autre paquet.) Lors de la création `contentFiles` d’un paquet d’échantillons, utilisez la valeur en `<IncludeAssets>`. Dans le dossier `content`, réorganisez l’exemple de code dans un dossier appelé `\Samples\<identifier>` comme dans `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Bonnes pratiques en matière de version de package :**

- En général, définissez la version du package pour qu’elle corresponde au projet (ou à l’assembly), bien que cela ne soit pas strictement obligatoire. C’est simple lorsque vous limitez un package à un assembly unique. Globalement, n’oubliez pas que NuGet lui-même traire les versions de package lors de la résolution des dépendances, pas les versions d’assembly.
- Lorsque vous utilisez un schéma de version non standard, veillez à prendre en compte les règles de gestion de versions NuGet, comme expliqué dans [Gestion des versions de package](../../concepts/package-versioning.md). NuGet est la plupart du temps [conforme à SemVer 2](../../concepts/package-versioning.md#semantic-versioning-200).

> Pour plus d’informations sur la résolution des dépendances, consultez [Résolution des dépendances avec PackageReference](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference). Pour obtenir des informations plus anciennes qui peuvent également aider à mieux comprendre le contrôle de version, consultez cette série de billets de blog.
>
> - [Partie 1 : Affronter les difficultés liées aux DLL](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Partie 2 : L’algorithme principal](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Partie 3 : Unification par le biais de redirections de liaison](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)
