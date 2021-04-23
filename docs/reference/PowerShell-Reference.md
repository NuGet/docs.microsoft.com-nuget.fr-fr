---
title: Informations de référence sur PowerShell NuGet
description: La référence complète aux commandes PowerShell disponibles dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 7bc0395a98e75fe006e048b91d84cb5c17220161
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901887"
---
# <a name="powershell-reference"></a>Référence sur PowerShell

La console du gestionnaire de package fournit une interface PowerShell dans Visual Studio sur Windows pour interagir avec NuGet via les commandes spécifiques listées ci-dessous. (La console n’est pas disponible actuellement dans Visual Studio pour Mac.) Pour obtenir un guide d’utilisation de la console, consultez la rubrique [installer et gérer des packages à l’aide](../consume-packages/install-use-packages-powershell.md) de la console du gestionnaire de package.

> [!Tip]
> Toutes les commandes PowerShell sont liées uniquement à la consommation des packages. Aucune commande PowerShell n’est liée à la création et à la publication de packages, sauf dans la mesure où un package peut également être un consommateur d’autres packages.

> [!Important]
> Les commandes répertoriées ici sont spécifiques à la console du gestionnaire de package dans Visual Studio, et diffèrent des [commandes du module Package Management](/powershell/module/packagemanagement) qui sont disponibles dans un environnement PowerShell général. Plus précisément, chaque environnement possède des commandes qui ne sont pas disponibles dans l’autre, et les commandes portant le même nom peuvent également différer dans leurs arguments spécifiques. Lorsque vous utilisez la console Package Management dans Visual Studio, les commandes et les arguments décrits dans cette rubrique s’appliquent.

| Commandes courantes | Description | Version de NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Installe un package et ses dépendances dans le projet. | Tous |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Met à jour un package et ses dépendances, ou tous les packages d’un projet. | Tous |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Recherche une source de package à l’aide d’un ID de package ou de mots clés. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Récupère la liste des packages installés dans le référentiel local, ou répertorie les packages disponibles à partir d’une source de package. | Tous |

| Commandes secondaires | Description | Version de NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Examine tous les assemblys dans le chemin de sortie d’un projet et ajoute des redirections de liaison au ou, le `app.config` `web.config` cas échéant. | Tous |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Affiche des informations sur le projet par défaut ou spécifié. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Lance le navigateur par défaut avec l’URL du projet, de la licence ou du rapport d’abus pour le package spécifié. | Déconseillé dans 3.0 + |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Inscrit un expansion de tabulation pour les paramètres d’une commande, ce qui vous permet de créer des expansions personnalisées pour les valeurs de paramètres couramment utilisées. | Tous |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Obtient la version du package installé à partir du projet spécifié et synchronise la version avec les autres projets de la solution. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Supprime un package d’un projet, en supprimant éventuellement ses dépendances. | Tous |

Pour obtenir une aide détaillée sur l’une de ces commandes dans la console, exécutez simplement la commande suivante avec le nom de commande en question :

```ps
Get-Help <command> -full
```

Toutes les commandes de la console du gestionnaire de package prennent en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants :

- Débogage
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Commentaires
- WarningAction
- WarningVariable

Pour plus d’informations, reportez-vous à [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) dans la documentation PowerShell.