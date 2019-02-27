---
title: Tools.JSON de détection des versions de nuget.exe
description: Le point de terminaison
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852531"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools.JSON de détection des versions de nuget.exe

Aujourd'hui, il existe plusieurs façons d’obtenir la dernière version de nuget.exe sur votre ordinateur de manière scriptable. Par exemple, vous pouvez télécharger et extraire le [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) package à partir de nuget.org. Cela a une certaine complexité car elle requiert soit que vous avez déjà nuget.exe (pour `nuget.exe install`) ou vous devez décompresser le fichier .nupkg à l’aide d’un outil de décompression de base et de trouver le binaire à l’intérieur.

Si vous avez déjà nuget.exe, vous pouvez également utiliser `nuget.exe update -self`, mais cela nécessite également avoir une copie existante de nuget.exe. Cette approche met également à jour vous vers la dernière version. Il n’autorise pas l’utilisation d’une version spécifique.

Le `tools.json` point de terminaison est disponible pour les deux résoudre le problème de démarrage et à laisser le contrôle de la version de nuget.exe que vous téléchargez. Cela peut servir dans des environnements CI/CD ou dans des scripts personnalisés pour détecter et de télécharger n’importe quelle version publiée de nuget.exe.

Le `tools.json` point de terminaison peut être extraites à l’aide d’une requête HTTP non authentifiée (par exemple, `Invoke-WebRequest` dans PowerShell ou `wget`). Il peut être analysée à l’aide d’un désérialiseur JSON et télécharger nuget.exe suivantes de qu'url peuvent également être extraites à l’aide non authentifiée de requêtes HTTP.

Le point de terminaison peut être extraites à l’aide de la `GET` méthode :

    GET https://dist.nuget.org/tools.json

Le [schéma JSON](http://json-schema.org/) pour le point de terminaison est disponible ici :

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Réponse

La réponse est un document JSON contenant toutes les versions disponibles de nuget.exe.

L’objet JSON racine a la propriété suivante :

Name      | Type             | Obligatoire
--------- | ---------------- | --------
nuget.exe | tableau d’objets | oui

Chaque objet dans le `nuget.exe` tableau présente les propriétés suivantes :

Name     | Type   | Obligatoire | Notes
-------- | ------ | -------- | -----
version  | string | oui      | Une chaîne de SemVer 2.0.0
url      | string | oui      | Une URL absolue pour le téléchargement de cette version de nuget.exe
Étape    | string | oui      | Une chaîne d’enum
uploaded | string | oui      | Un horodatage ISO 8601 approximatif de lorsque la version mise à disposition

Les éléments dans le tableau doit être triées, SemVer 2.0.0 par ordre décroissant. Cette garantie est destinée à réduire la charge d’un client qui s’intéresse à un numéro de version le plus élevé. Toutefois, cela ne signifie que la liste n’est pas triée dans l’ordre chronologique. Par exemple, si une version majeure inférieur est pris en charge à une date ultérieure à une version majeure supérieure, cette version pris en charge n’apparaîtra pas en haut de la liste. Si vous souhaitez que la dernière version publiée par *timestamp*, il suffit de trier le tableau par le `uploaded` chaîne. Cela fonctionne parce que le `uploaded` timestamp est exprimé en le [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format qui peut être trié par ordre chronologique à l’aide d’un tri lexicographique (autrement dit, un tri simple chaîne).

Le `stage` propriété indique maintenant comment cette version de l’outil. 

Étape              | Signification
------------------ | ------
EarlyAccessPreview | Pas encore visible sur le [web page de téléchargement](https://www.nuget.org/downloads) et doivent être validés par les partenaires
Final           | Disponible sur le site de téléchargement, mais n’est pas encore recommandé pour la consommation généralisée
ReleasedAndBlessed | Disponible sur le site de téléchargement et est recommandée pour la consommation

Une approche simple pour avoir la dernière version, la version recommandée est à prendre la première version dans la liste qui possède le `stage` valeur `ReleasedAndBlessed`. Cela fonctionne car les versions sont triées par ordre de SemVer 2.0.0.

Le `NuGet.CommandLine` package sur nuget.org est généralement uniquement mis à jour avec `ReleasedAndBlessed` versions.

### <a name="sample-request"></a>Exemple de demande

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [tools-json.json](./_data/tools-json.json)]
