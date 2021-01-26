---
title: tools.jspour la découverte de versions nuget.exe
description: Le point de terminaison pour
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773817"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>tools.jspour la découverte de versions nuget.exe

Aujourd’hui, il existe plusieurs façons d’obtenir la dernière version de nuget.exe sur votre machine de manière scriptable. Par exemple, vous pouvez télécharger et extraire le [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package à partir de NuGet.org. Cela a une certaine complexité, car elle nécessite que vous disposiez déjà d' nuget.exe (pour `nuget.exe install` ), ou vous devez décompresser le fichier. nupkg à l’aide d’un outil de décompression de base et rechercher le binaire à l’intérieur de.

Si vous avez déjà nuget.exe, vous pouvez également utiliser `nuget.exe update -self` , mais cela nécessite également une copie existante de nuget.exe. Cette approche vous permet également de vous mettre à jour vers la dernière version. Elle n’autorise pas l’utilisation d’une version spécifique.

Le `tools.json` point de terminaison est disponible pour résoudre le problème d’amorçage et pour vous permettre de contrôler la version de nuget.exe que vous téléchargez. Il peut être utilisé dans des environnements CI/CD ou dans des scripts personnalisés pour détecter et télécharger une version finale de nuget.exe.

Le `tools.json` point de terminaison peut être extrait à l’aide d’une requête HTTP non authentifiée (par exemple, `Invoke-WebRequest` dans PowerShell ou `wget` ). Elle peut être analysée à l’aide d’un désérialiseur JSON et les URL de téléchargement ultérieures nuget.exe peuvent également être extraites à l’aide de requêtes HTTP non authentifiées.

Le point de terminaison peut être extrait à l’aide de la `GET` méthode :

```
GET https://dist.nuget.org/tools.json
```

Le [schéma JSON](https://json-schema.org/) du point de terminaison est disponible ici :

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>response

La réponse est un document JSON contenant toutes les versions disponibles de nuget.exe.

L’objet JSON racine a la propriété suivante :

Nom      | Type             | Obligatoire
--------- | ---------------- | --------
nuget.exe | tableau d’objets | Oui

Chaque objet du `nuget.exe` tableau a les propriétés suivantes :

Nom     | Type   | Obligatoire | Notes
-------- | ------ | -------- | -----
version  | string | Oui      | Chaîne SemVer 2.0.0
url      | string | Oui      | Une URL absolue pour le téléchargement de cette version de nuget.exe
étape    | string | Oui      | Chaîne d’énumération
Téléchargé | string | Oui      | Horodatage ISO 8601 approximatif de la date de mise à disposition de la version

Les éléments du tableau sont triés dans l’ordre décroissant, SemVer 2.0.0. Cette garantie est destinée à réduire la charge d’un client qui est intéressé par le numéro de version le plus élevé. Toutefois, cela signifie que la liste n’est pas triée dans l’ordre chronologique. Par exemple, si une version principale inférieure est gérée à une date ultérieure à une version majeure supérieure, cette version en service n’apparaît pas en haut de la liste. Si vous souhaitez que la version la plus récente soit libérée par *horodateur*, il vous suffit de trier le tableau par la `uploaded` chaîne. Cela fonctionne parce que l' `uploaded` horodatage est au format [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) qui peut être trié par ordre chronologique à l’aide d’un tri lexicographique (par exemple, un tri de chaîne simple).

La `stage` propriété indique le degré de vérification de cette version de l’outil. 

Étape              | Signification
------------------ | ------
EarlyAccessPreview | Pas encore visible sur la [page Web de téléchargement](https://www.nuget.org/downloads) et doit être validé par les partenaires
Final           | Disponible sur le site de téléchargement, mais n’est pas encore recommandée pour une consommation étendue
ReleasedAndBlessed | Disponible sur le site de téléchargement et est recommandé pour la consommation

Une approche simple pour disposer de la version la plus récente recommandée consiste à prendre la première version de la liste qui a la `stage` valeur `ReleasedAndBlessed` . Cela fonctionne parce que les versions sont triées dans l’ordre SemVer 2.0.0.

Le `NuGet.CommandLine` package sur NuGet.org est généralement uniquement mis à jour avec des `ReleasedAndBlessed` versions.

### <a name="sample-request"></a>Exemple de requête

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [tools-json.json](./_data/tools-json.json)]
