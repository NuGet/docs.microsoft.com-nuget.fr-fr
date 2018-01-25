---
title: Notes de publication NuGet 2.2.1 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet 2.2.1, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 2.2.1 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-221-release-notes"></a>Notes de version 2.2.1 de NuGet

[Notes de publication NuGet 2.2](../release-notes/nuget-2.2.md) | [NuGet 2.5 Notes de publication](../release-notes/nuget-2.5.md)

NuGet 2.2.1 a été publiée le 15 février 2013.  Le numéro de version Extension VS est 2.2.40116.9051.

## <a name="localization-refresh"></a>Actualisation de la localisation
Lors de l’expédition NuGet dans le cadre de Visual Studio 2012, elle a été entièrement localisée en anglais + 13 autres langues.  Depuis, NuGet 2.1 et 2.2 ont été expédiés mais la localisation n’avait pas été actualisée.  La version NuGet 2.2.1 actualise la localisation.

Interface utilisateur et la PowerShell Console de NuGet sont traduits dans les langues suivantes :

1. Chinois (simplifié)
1. Chinois (traditionnel)
1. Tchèque
1. Anglais
1. Français
1. Allemand
1. Italien
1. Japonais
1. Coréen
1. Polonais
1. Portugais (Brésil)
1. Russe
1. Espagnol
1. Turc

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Modèles Visual Studio prend en charge plusieurs référentiels Package préinstallé
Si vous produisez des modèles Visual Studio, vous pouvez utiliser NuGet pour [préinstaller les packages](../visual-studio-extensibility/visual-studio-templates.md) en tant que partie du modèle.  Jusqu'à présent, cette fonctionnalité avait une limitation que tous les packages doivent provenir de la même source.  Avec NuGet 2.2.1, vous pouvez avoir des packages installés à partir de plusieurs référentiels (dans le modèle, une extension VSIX ou un dossier sur le disque défini dans le Registre).

Le scénario principal de cette fonctionnalité est des modèles de projet ASP.NET personnalisés.  Les modèles ASP.NET intégrés utilisent les packages préinstallés, extraction de packages à partir du disque local.  Vous pouvez maintenant créer un modèle de projet ASP.NET personnalisé qui utilise les packages existants installés par ASP.NET et ajouter des packages NuGet supplémentaires dans votre modèle.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 2.2.1 comprend plusieurs correctifs de bogues ciblés. Pour obtenir la liste de travail éléments fixes dans NuGet 2.2.1, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problèmes connus

Si vous étendez des modèles de projet ASP.NET, tous les référentiels préinstallé package doivent utiliser la même valeur pour le `isPreunzipped` attribut.
