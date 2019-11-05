---
title: Tools. JSON pour la détection des versions de NuGet. exe
description: Le point de terminaison pour
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611029"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools. JSON pour la détection des versions de NuGet. exe

Aujourd’hui, il existe plusieurs façons d’obtenir la dernière version de NuGet. exe sur votre machine de manière scriptable. Par exemple, vous pouvez télécharger et extraire le package [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) à partir de NuGet.org. Cela a une certaine complexité, car elle nécessite que vous disposiez déjà de NuGet. exe (pour `nuget.exe install`) ou vous devez décompresser le fichier. nupkg à l’aide d’un outil de décompression de base et rechercher le binaire à l’intérieur de.

Si vous disposez déjà de NuGet. exe, vous pouvez également utiliser `nuget.exe update -self`, mais cela nécessite également une copie existante de NuGet. exe. Cette approche vous permet également de vous mettre à jour vers la dernière version. Elle n’autorise pas l’utilisation d’une version spécifique.

Le point de terminaison `tools.json` est disponible pour résoudre le problème d’amorçage et pour vous permettre de contrôler la version de NuGet. exe que vous téléchargez. Il peut être utilisé dans des environnements CI/CD ou dans des scripts personnalisés pour détecter et télécharger une version finale de NuGet. exe.

Le point de terminaison `tools.json` peut être extrait à l’aide d’une requête HTTP non authentifiée (par exemple, `Invoke-WebRequest` dans PowerShell ou `wget`). Il peut être analysé à l’aide d’un désérialiseur JSON et les URL de téléchargement NuGet. exe suivantes peuvent également être extraites à l’aide de requêtes HTTP non authentifiées.

Le point de terminaison peut être extrait à l’aide de la méthode `GET` :

    GET https://dist.nuget.org/tools.json

Le [schéma JSON](https://json-schema.org/) du point de terminaison est disponible ici :

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Réponse

La réponse est un document JSON contenant toutes les versions disponibles de NuGet. exe.

L’objet JSON racine a la propriété suivante :

Name      | Tapez             | Obligatoire
--------- | ---------------- | --------
nuget.exe | Tableau d’objets | oui

Chaque objet du tableau de `nuget.exe` a les propriétés suivantes :

Name     | Tapez   | Obligatoire | Notes
-------- | ------ | -------- | -----
version  | string | oui      | Chaîne SemVer 2.0.0
url      | string | oui      | Une URL absolue pour le téléchargement de cette version de NuGet. exe
Mode    | string | oui      | Chaîne d’énumération
Téléchargé | string | oui      | Horodatage ISO 8601 approximatif de la date de mise à disposition de la version

Les éléments du tableau sont triés dans l’ordre décroissant, SemVer 2.0.0. Cette garantie est destinée à réduire la charge d’un client qui est intéressé par le numéro de version le plus élevé. Toutefois, cela signifie que la liste n’est pas triée dans l’ordre chronologique. Par exemple, si une version principale inférieure est gérée à une date ultérieure à une version majeure supérieure, cette version en service n’apparaît pas en haut de la liste. Si vous souhaitez que la version la plus récente soit libérée par *horodateur*, il vous suffit de trier le tableau en `uploaded` chaîne. Cela fonctionne parce que le `uploaded` horodateur est au format [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) qui peut être trié par ordre chronologique à l’aide d’un tri lexicographique (c’est-à-dire un tri de chaîne simple).

La propriété `stage` indique le mode d’utilisation de cette version de l’outil. 

Étape              | Signification
------------------ | ------
EarlyAccessPreview | Pas encore visible sur la [page Web de téléchargement](https://www.nuget.org/downloads) et doit être validé par les partenaires
Final           | Disponible sur le site de téléchargement, mais n’est pas encore recommandée pour une consommation étendue
ReleasedAndBlessed | Disponible sur le site de téléchargement et est recommandé pour la consommation

Une approche simple pour disposer de la version la plus récente recommandée consiste à prendre la première version de la liste qui a la valeur `stage` de `ReleasedAndBlessed`. Cela fonctionne parce que les versions sont triées dans l’ordre SemVer 2.0.0.

Le package `NuGet.CommandLine` sur nuget.org est généralement mis à jour uniquement avec les versions de `ReleasedAndBlessed`.

### <a name="sample-request"></a>Exemple de demande

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [tools-json.json](./_data/tools-json.json)]
