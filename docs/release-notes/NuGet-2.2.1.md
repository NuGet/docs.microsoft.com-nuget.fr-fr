---
title: Notes de publication de NuGet 2.2.1
description: Notes de publication pour NuGet 2.2.1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776806"
---
# <a name="nuget-221-release-notes"></a>Notes de publication de NuGet 2.2.1

Notes de publication de [NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Notes de publication de NuGet 2,5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 a été publié le 15 février 2013.  Le numéro de version de l’extension VS est 2.2.40116.9051.

## <a name="localization-refresh"></a>Actualisation de la localisation
Lorsque NuGet est fourni avec Visual Studio 2012, il a été entièrement localisé en anglais + 13 autres langages.  Depuis, NuGet 2,1 et 2,2 ont été expédiés, mais la localisation n’a pas été actualisée.  La version 2.2.1 de NuGet actualise notre localisation.

L’interface utilisateur et la console PowerShell de NuGet sont localisées dans les langues suivantes :

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Les modèles Visual Studio prennent en charge plusieurs référentiels de packages préinstallés
Si vous produisez des modèles Visual Studio, vous pouvez utiliser NuGet pour [préinstaller les packages](../visual-studio-extensibility/visual-studio-templates.md) dans le cadre du modèle.  Jusqu’à présent, cette fonctionnalité avait une limitation que tous les packages devaient provenir de la même source.  Toutefois, avec NuGet 2.2.1, vous pouvez avoir des packages installés à partir de plusieurs référentiels (dans le modèle, un VSIX ou un dossier sur le disque défini dans le registre).

Le scénario principal de cette fonctionnalité est le modèle de projet ASP.NET personnalisé.  Les modèles ASP.NET intégrés utilisent des packages préinstallés, en extrayant des packages à partir du disque local.  Vous pouvez maintenant créer un modèle de projet ASP.NET personnalisé qui utilise les packages existants installés par ASP.NET, mais ajouter des packages NuGet supplémentaires à votre modèle.

## <a name="bug-fixes"></a>Résolutions de bogues
NuGet 2.2.1 comprend quelques correctifs de bogues ciblés. Pour obtenir la liste des éléments de travail corrigés dans NuGet 2.2.1, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problèmes connus

Si vous étendez des modèles de projet ASP.NET, tous les référentiels de packages préinstallés doivent utiliser la même valeur pour l' `isPreunzipped` attribut.
