---
title: Référence PowerShell de NuGet
description: La référence complète de commandes PowerShell disponibles dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 425ba736eba4609ebd6b5185ae3f1f976ab07a67
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842567"
---
# <a name="powershell-reference"></a>Informations de référence sur PowerShell

La Console du Gestionnaire de Package fournit une interface de PowerShell dans Visual Studio sur Windows pour interagir avec NuGet via les commandes spécifiques répertoriées ci-dessous. (La console n’est pas actuellement disponible dans Visual Studio pour Mac.) Pour un guide d’utilisation de la console, consultez [installer et gérer des packages à l’aide de la Console du Gestionnaire de Package](../tools/package-manager-console.md) rubrique.

> [!Tip]
> Toutes les commandes PowerShell se rapportent uniquement à la consommation de package. Aucune commande PowerShell sont liées à la création et publication de packages à l’exception dans la mesure où un package peut également être un consommateur d’autres packages.

> [!Important]
> Les commandes répertoriées ici sont spécifiques à la Console du Gestionnaire de Package dans Visual Studio et diffère le [les commandes de module de gestion des packages](/powershell/module/packagemanagement/?view=powershell-6) qui sont disponibles dans un environnement PowerShell général. Plus précisément, chaque environnement possède des commandes qui ne sont pas disponibles dans l’autre, et commandes portant le même nom peuvent également différer dans leurs arguments spécifiques. Lorsque vous utilisez la Console de gestion de Package dans Visual Studio, les commandes et les arguments documentées dans cette rubrique s’appliquent.

| Commandes courantes | Description | Version de NuGet |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Installe un package et ses dépendances dans le projet. | Tous |
| [Update-Package](ps-ref-update-package.md) | Met à jour un package et ses dépendances ou tous les packages dans un projet. | Tous |
| [Find-Package](ps-ref-find-package.md) | Recherche dans une source de package à l’aide d’un ID de package ou des mots clés. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Récupère la liste des packages installés dans le référentiel local, ou répertorie les packages disponibles à partir d’une source de package. | Tous |

| Commandes secondaires | Description | Version de NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Examine tous les assemblys dans le chemin de sortie pour un projet et ajoute des redirections de liaison à la `app.config` ou `web.config` lorsque cela est nécessaire. | Tous |
| [Get-Project](ps-ref-get-project.md) | Affiche des informations sur la valeur par défaut ou le projet spécifié. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Lance le navigateur par défaut avec le projet, une licence ou une URL d’abus de rapport pour le package spécifié. | Déconseillé dans 3.0 + |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Inscrit une tabulation pour les paramètres d’une commande, ce qui vous permet de créer des expansions personnalisées pour les valeurs de paramètres couramment utilisés. | Tous |
| [Sync-Package](ps-ref-sync-package.md) | Obtenir la version installée de package à partir spécifié du projet et synchronise la version pour le reste des projets de la solution. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Supprime un package à partir d’un projet, éventuellement de supprimer ses dépendances. | Tous |

Pour une aide complète et détaillée sur un de ces commandes dans la console, exécutez simplement la commande suivante avec le nom de la commande en question :

```ps
Get-Help <command> -full
```

Toutes les commandes de Console du Gestionnaire de Package prennent en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216):

- Débogage
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Détaillé
- WarningAction
- WarningVariable

Pour plus d’informations, reportez-vous à [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) dans la documentation de PowerShell.
