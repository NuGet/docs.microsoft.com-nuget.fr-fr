---
title: Variables d’environnement CLI NuGet
description: Référence pour les variables d’environnement nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: ac1bf2b65ab6ec4e8cf864810181fc661236262a
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931980"
---
# <a name="nuget-cli-environment-variables"></a>Variables d’environnement CLI NuGet

Le comportement de l’interface CLI de nuget.exe peut être configuré via un nombre de variables d’environnement, qui affectent nuget.exe sur l’ordinateur, utilisateur ou le traitement des niveaux. Variables d’environnement remplacent toujours les paramètres dans `NuGet.Config` fichiers, ce qui permet des serveurs pour modifier les paramètres appropriés sans modifier tous les fichiers de builds.

En règle générale, les options spécifiées directement sur la ligne de commande ou dans les fichiers de configuration NuGet ont une priorité, mais il existe quelques exceptions comme *FORCE_NUGET_EXE_INTERACTIVE*. Si vous trouvez que nuget.exe se comporte différemment entre différents ordinateurs, une variable d’environnement peut être la cause. Par exemple, Azure Web Apps Kudu (utilisé au cours du déploiement) a *NUGET_XMLDOC_MODE* définie sur *ignorer* pour accélérer les performances de restauration de package et d’économiser l’espace disque.

La CLI NuGet utilise MSBuild pour lire les fichiers de projet. Toutes les variables d’environnement sont disponibles en tant que [propriétés](/visualstudio/msbuild/msbuild-command-line-reference) lors de l’évaluation de MSBuild.
La liste de propriétés présentée dans [NuGet pack et restore en tant que cibles de MSBuild](../reference/msbuild-targets.md#restore-properties) peut également être définie en tant que variables d’environnement.

| Variable | Description | Notes |
| --- | --- | --- |
| http_proxy | Proxy HTTP utilisé pour les opérations HTTP de NuGet. | Cela serait spécifiée en tant que `http://<username>:<password>@proxy.com`. |
| no_proxy | Configure les domaines de contourner l’utilisation de proxy. | Spécifié en tant que domaines séparés par des virgules (,). |
| EnableNuGetPackageRestore | Indicateur pour si NuGet doit implicitement donner son consentement si requis par le package lors de la restauration. | Indicateur spécifié est traité comme *true* ou *1*, toute autre valeur traitée en tant qu’indicateur pas définie. |
| NUGET_EXE_NO_PROMPT | Empêche le fichier exe pour demander des informations d’identification. | N’importe quelle valeur sauf une chaîne null ou vide est considérée comme cet indicateur ensemble/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Variable d’environnement global pour forcer le mode interactif. | N’importe quelle valeur sauf une chaîne null ou vide est considérée comme cet indicateur ensemble/true. |
| NUGET_PACKAGES | Chemin d’accès à utiliser pour le *global-packages* dossier comme décrit sur [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Spécifié en tant que chemin d’accès absolu. |
| NUGET_FALLBACK_PACKAGES | Dossiers de packages de secours globaux. | Chemins d’accès du dossier absolu séparées par des points-virgules ( ;). |
| NUGET_HTTP_CACHE_PATH | Chemin d’accès à utiliser pour le *http-cache* dossier comme décrit sur [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Spécifié en tant que chemin d’accès absolu. |
| NUGET_PERSIST_DG | Indicateur spécifiant si les fichiers de groupe de distribution (données collectées à partir de MSBuild) doivent être rendue persistante. | Spécifié en tant que *true* ou *false* (valeur par défaut), si la valeur pas NUGET_PERSIST_DG_PATH est stockée dans le répertoire temporaire (dossier NuGetScratch dans le répertoire temp de l’environnement actuel). |
| NUGET_PERSIST_DG_PATH | Chemin d’accès pour conserver les fichiers de groupe de distribution. | Spécifié en tant que chemin d’accès absolu, cette option est utilisée uniquement lorsque *NUGET_PERSIST_DG* est définie sur true. |
| NUGET_RESTORE_MSBUILD_ARGS | Définit les autres arguments MSBuild. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Définit le niveau de détail du journal MSBuild. | Valeur par défaut est *silencieux* (« / v : q »). Les valeurs possibles *q [uiet]*, *m [inimal]*, *n [ormal]*, *d [etailed]*, et *diag [nostic]*. |
| NUGET_SHOW_STACK | Détermine si l’exception complète (y compris la trace de pile) doit être affichée à l’utilisateur. | Spécifié en tant que *true* ou *false* (valeur par défaut). |
| NUGET_XMLDOC_MODE | Détermine comment l’extraction du fichier assemblys XML documentation doit être gérée. | Modes pris en charge sont *ignorer* (ne pas extraire les fichiers de documentation XML), *compresser* (stocker les fichiers de document XML comme une archive zip) ou *aucun* (par défaut, traiter des fichiers de document XML comme standard fichiers). |
| NUGET_CERT_REVOCATION_MODE | Détermine comment pour vérifier l’état de révocation du certificat utilisé pour signer un package, est effectuée lorsqu’un package signé est installé ou restauré. Si ne pas la valeur, valeur par défaut est `online`.| Les valeurs possibles *online* (valeur par défaut), *hors connexion*.  Associées à [NU3028](../reference/errors-and-warnings/NU3028.md) |

