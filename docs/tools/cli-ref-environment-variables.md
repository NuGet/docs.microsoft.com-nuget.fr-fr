---
title: Variables d’environnement NuGet CLI
description: Informations de référence pour les variables d’environnement nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 50bf8b469eda423db7665323823a2daf3f3aa41d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817071"
---
# <a name="nuget-cli-environment-variables"></a>Variables d’environnement NuGet CLI

Le comportement de l’interface CLI de nuget.exe peut être configuré via un nombre de variables d’environnement, ce qui affecte nuget.exe sur l’ordinateur, utilisateur, ou le traitement des niveaux. Variables d’environnement toujours remplacent les paramètres de `NuGet.Config` fichiers, ce qui permet de générer des serveurs pour modifier les paramètres appropriés sans modifier les fichiers.

En général, les options spécifiées directement sur la ligne de commande ou dans les fichiers de configuration NuGet ont une priorité, mais il existe quelques exceptions telles que *FORCE_NUGET_EXE_INTERACTIVE*. Si vous trouvez que nuget.exe se comporte différemment entre des ordinateurs différents, une variable d’environnement peut être la cause. Par exemple, Azure Web Apps Kudu (utilisés pendant le déploiement) a *NUGET_XMLDOC_MODE* la valeur *ignorer* pour accélérer les performances de restauration de package et d’économiser l’espace disque.

| Variable | Description | Notes |
| --- | --- | --- |
| http_proxy | Serveur proxy HTTP utilisé pour les opérations de NuGet HTTP. | Cela serait spécifiée en tant que `http://<username>:<password>@proxy.com`. |
| no_proxy | Configure les domaines de contourner l’utilisation de proxy. | Spécifié en tant que domaines séparés par des virgules (,). |
| EnableNuGetPackageRestore | Indicateur signalant si NuGet doit implicitement donner leur consentement si requis par le package lors de la restauration. | Indicateur spécifié est traité comme *true* ou *1*, toute autre valeur traitée en tant qu’indicateur pas définie. |
| NUGET_EXE_NO_PROMPT | Empêche le fichier exe pour demander des informations d’identification. | Toute valeur sauf une chaîne null ou vide est considérée comme cela indicateur ensemble/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Variable d’environnement global pour forcer le mode interactif. | Toute valeur sauf une chaîne null ou vide est considérée comme cela indicateur ensemble/true. |
| NUGET_PACKAGES | Chemin d’accès à utiliser pour le *global-packages* dossier comme décrit dans [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Spécifié comme chemin d’accès absolu. |
| NUGET_FALLBACK_PACKAGES | Dossiers de packages de secours global. | Chemins d’accès du dossier absolu séparés par un point-virgule ( ;). |
| NUGET_HTTP_CACHE_PATH | Chemin d’accès à utiliser pour le *du cache http* dossier comme décrit dans [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Spécifié comme chemin d’accès absolu. |
| NUGET_PERSIST_DG | Indicateur précisant si les fichiers de groupe de distribution (les données collectées à partir de MSBuild) doivent être persistante. | Spécifié en tant que *true* ou *false* (par défaut), si la valeur pas NUGET_PERSIST_DG_PATH sera stocké dans le répertoire temporaire (dossier NuGetScratch dans le répertoire temp environnement actuel). |
| NUGET_PERSIST_DG_PATH | Chemin d’accès pour conserver les fichiers de groupe de distribution. | Spécifié en tant que chemin d’accès absolu, cette option est utilisée uniquement lorsque *NUGET_PERSIST_DG* est définie sur true. |
| NUGET_RESTORE_MSBUILD_ARGS | Définit les autres arguments MSBuild. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Définit le niveau de détail du journal MSBuild. | Valeur par défaut est *silencieux* (« / v : q »). Les valeurs possibles *q [uiet]*, *m [inimal]*, *n [ormal]*, *d [etailed]*, et *diag [nostic]*. |
| NUGET_SHOW_STACK | Détermine si l’exception complète (y compris la trace de la pile) doit être affichée à l’utilisateur. | Spécifié en tant que *true* ou *false* (par défaut). |
| NUGET_XMLDOC_MODE | Détermine comment l’extraction de fichier de documentation XML assemblys doit être gérée. | Modes pris en charge sont *ignorer* (ne pas extraire les fichiers de documentation XML), *compresser* (stocker les fichiers de document XML en tant qu’une archive zip) ou *aucun* (par défaut, traiter les fichiers de document XML comme normal fichiers). |
