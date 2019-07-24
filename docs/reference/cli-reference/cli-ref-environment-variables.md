---
title: Variables d’environnement de l’interface CLI NuGet
description: Informations de référence sur les variables d’environnement NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b04efaecce1d5bc892dfc48ae3e872d80aad209d
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327826"
---
# <a name="nuget-cli-environment-variables"></a>Variables d’environnement de l’interface CLI NuGet

Le comportement de l’interface CLI NuGet. exe peut être configuré à l’aide de plusieurs variables d’environnement, qui affectent NuGet. exe à l’ensemble des niveaux d’ordinateur, d’utilisateur ou de processus. Les variables d’environnement remplacent toujours tous `NuGet.Config` les paramètres dans les fichiers, ce qui permet aux serveurs de builds de modifier les paramètres appropriés sans modifier les fichiers.

En général, les options spécifiées directement sur la ligne de commande ou dans les fichiers de configuration NuGet ont la priorité, mais il existe quelques exceptions, telles que *FORCE_NUGET_EXE_INTERACTIVE*. Si vous constatez que NuGet. exe se comporte différemment entre différents ordinateurs, une variable d’environnement peut en être la cause. Par exemple, Azure Web Apps Kudu (utilisé pendant le déploiement) a *NUGET_XMLDOC_MODE* défini sur *Ignorer* pour accélérer les performances de restauration des packages et économiser de l’espace disque.

L’interface CLI NuGet utilise MSBuild pour lire les fichiers projet. Toutes les variables d’environnement sont disponibles en tant que [Propriétés](/visualstudio/msbuild/msbuild-command-line-reference) lors de l’évaluation MSBuild.
La liste des propriétés documentées dans [NuGet Pack et Restore en tant que cibles MSBuild](../msbuild-targets.md#restore-properties) peut également être définie en tant que variables d’environnement.

| Variable | Description | Notes |
| --- | --- | --- |
| http_proxy | Proxy HTTP utilisé pour les opérations NuGet HTTP. | Cela est spécifié en tant `http://<username>:<password>@proxy.com`que. |
| no_proxy | Configure les domaines pour qu’ils contournent de l’utilisation du proxy. | Spécifié en tant que domaines séparés par une virgule (,). |
| EnableNuGetPackageRestore | Indicateur pour si NuGet doit implicitement accorder le consentement si cela est requis par le package lors de la restauration. | L’indicateur spécifié est traité comme *true* ou *1*, toute autre valeur traitée comme Flag n’est pas définie. |
| NUGET_EXE_NO_PROMPT | Empêche l’exe de demander des informations d’identification. | Toute valeur, à l’exception de null ou d’une chaîne vide, est traitée comme cet indicateur SET/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Variable d’environnement globale pour forcer le mode interactif. | Toute valeur, à l’exception de null ou d’une chaîne vide, est traitée comme cet indicateur SET/true. |
| NUGET_PACKAGES | Chemin à utiliser pour le dossier *Global-packages* , comme décrit dans [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Spécifié comme chemin d’accès absolu. |
| NUGET_FALLBACK_PACKAGES | Dossiers de packages de secours globaux. | Chemins d’accès absolus au dossier séparés par un point-virgule (;). |
| NUGET_HTTP_CACHE_PATH | Chemin à utiliser pour le dossier *http-cache* , comme décrit dans [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Spécifié comme chemin d’accès absolu. |
| NUGET_PERSIST_DG | Indicateur qui spécifie si les fichiers DG (données collectées à partir de MSBuild) doivent être persistants. | Spécifié comme *true* ou *false* (valeur par défaut), si NUGET_PERSIST_DG_PATH n’est pas défini, est stocké dans le répertoire temporaire (dossier NuGetScratch dans le répertoire Temp de l’environnement actuel). |
| NUGET_PERSIST_DG_PATH | Chemin d’accès pour conserver les fichiers DG. | Spécifié comme chemin absolu, cette option est utilisée uniquement lorsque *NUGET_PERSIST_DG* a la valeur true. |
| NUGET_RESTORE_MSBUILD_ARGS | Définit des arguments MSBuild supplémentaires. | Transmettez les arguments de la même façon que vous les transmettez à MSBuild. exe. Voici un exemple de définition d’une propriété de projet foo à partir de la ligne de commande vers la barre de valeurs:/p: foo = bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Définit le niveau de détail du journal MSBuild. | La valeur par défaut est *Quiet* ("/v: q"). Les valeurs possibles sont *q [uiet]* , *m [inimal]* , *n [ormal]* , *d [etailed]* et *diag [Nostic]* . |
| NUGET_SHOW_STACK | Détermine si l’exception complète (y compris la trace de la pile) doit être affichée à l’utilisateur. | Spécifié comme *true* ou *false* (valeur par défaut). |
| NUGET_XMLDOC_MODE | Détermine le mode de gestion de l’extraction des fichiers de documentation XML des assemblys. | Les modes pris en charge sont *Skip* (ne pas extraire les fichiers de documentation XML), compresser (stocker les fichiers de document XML en tant qu’archive zip) ou *aucun* (par défaut, traiter les fichiers de document XML comme des fichiers standard). |
| NUGET_CERT_REVOCATION_MODE | Détermine la façon dont la vérification de l’état de révocation du certificat utilisé pour signer un package est effectuée lors de l’installation ou de la restauration d’un package signé. Si la valeur n’est pas définie `online`, la valeur par défaut est.| Valeurs possibles *en ligne* (par défaut), *hors connexion*.  En rapport avec [NU3028](../errors-and-warnings/NU3028.md) |

