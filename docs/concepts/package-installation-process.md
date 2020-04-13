---
title: Processus d’installation d’un package
description: Informations détaillées sur le processus d’installation d’un package
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 1ae030c308b14b8884fb608c1683c8c46000b0bd
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "77036901"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Processus d’installation d’un package NuGet

En termes simples, les différents outils NuGet créent généralement une référence à un package dans le fichier projet ou `packages.config`, puis effectuent une restauration de package, ce qui installe le package proprement dit. `nuget install` fait figure d’exception : il développe simplement le package dans un dossier `packages`, sans modifier les autres fichiers.

Le processus général se décompose ainsi :

1. (Tous les outils à l’exception de `nuget.exe`) Enregistrez la version et l’identificateur du package dans le fichier projet ou `packages.config`.

   Si l’outil d’installation est Visual Studio ou l’interface CLI dotnet, l’outil essaie d’abord d’installer le package. S’il est incompatible, le package n’est pas ajouté au fichier projet ou `packages.config`.

2. Acquérir le package :
   - Déterminez si le package (en fonction du numéro de version et de l’identificateur précis) est déjà installé dans le dossier *global-packages*, comme l’explique la page [Gérer les dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Si le paquet n’est pas dans le dossier *global-paquets,* essayez de le récupérer à partir des sources énumérées dans les [fichiers de configuration](../consume-packages/Configuring-NuGet-Behavior.md). Pour les sources en ligne, tentez tout d’abord de récupérer le package du cache HTTP, sauf si vous avez spécifié `-NoCache` avec des commandes de `nuget.exe`, ou spécifié `--no-cache` avec la commande `dotnet restore`. (Visual Studio `dotnet add package` et toujours utiliser le cache.) Si un paquet est utilisé à partir du cache, "CACHE" apparaît dans la sortie. Le cache a un délai d’expiration de 30 minutes.

   - Si le package ne se trouve pas dans le cache HTTP, tentez de le télécharger parmi les sources listées dans la configuration. Si un package est téléchargé, « GET » et « OK » apparaissent en sortie. NuGet journalise le trafic HTTP avec le niveau de commentaires normal.

   - Si aucune source ne permet de récupérer le package, l’installation échoue à ce stade, avec une erreur du type [NU1103](../reference/errors-and-warnings/NU1103.md). Notez que les erreurs des commandes `nuget.exe` affichent uniquement la dernière source vérifiée, mais implique que le package n’était disponible dans aucune source.

   Lors de l’acquisition du package, l’ordre des sources de la configuration NuGet peut s’appliquer :

   - NuGet consulte les partages réseau et le dossier local de sources avant de parcourir les sources HTTP.

3. Enregistrez une copie du package et d’autres informations dans le dossier *http-cache*, comme cela est expliqué dans [Gérer les dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. S’il a été téléchargé, installez le package dans le dossier *global-packages* de l’utilisateur. NuGet crée un sous-dossier par identificateur de package, puis un sous-dossier par version installée du package.

5. NuGet installe les dépendances de package nécessaires. Ce processus est susceptible de mettre à jour les versions de package, comme l’explique la page [Résolution de dépendances](../concepts/dependency-resolution.md).

6. Mettez à jour les dossiers et les fichiers projet :

    - Pour les projets qui utilisent PackageReference, mettez à jour le graphique de dépendance de package stocké dans `obj/project.assets.json`. Le contenu des packages proprement dits n’est copié dans aucun dossier du projet.
    - Mettez à jour `app.config` et/ou `web.config` si le package utilise des [transformations de fichiers config et source](../create-packages/source-and-config-file-transformations.md).

7. (Visual Studio uniquement) Affichez le fichier Lisez-moi du package, le cas échéant, dans une fenêtre Visual Studio.

Bénéficiez d’un codage productif avec les packages NuGet !
