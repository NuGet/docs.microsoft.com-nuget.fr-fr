---
title: Notes de publication de NuGet 2.2.1
description: Notes de publication pour NuGet 2.2.1 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550696"
---
# <a name="nuget-221-release-notes"></a>Notes de publication de NuGet 2.2.1

[Notes de publication de NuGet 2.2](../release-notes/nuget-2.2.md) | [Notes de publication de NuGet 2.5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 a été publiée le 15 février 2013.  Le numéro de version d’Extension VS est 2.2.40116.9051.

## <a name="localization-refresh"></a>Actualisation de la localisation
Lorsque NuGet partie intégrante de Visual Studio 2012, elle a été entièrement localisée en anglais + 13 autres langues.  Depuis lors, NuGet 2.1 et 2.2 ont été renvoyés, mais la localisation n’avait pas été actualisée.  La version de NuGet 2.2.1 actualise la localisation.

L’interface utilisateur de NuGet et la PowerShell Console sont traduits dans les langues suivantes :

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Modèles Visual Studio prend en charge plusieurs référentiels de packages préinstallés
Si vous produisez des modèles Visual Studio, vous pouvez utiliser NuGet pour [préinstaller les packages](../visual-studio-extensibility/visual-studio-templates.md) en tant que partie du modèle.  Jusqu'à présent, cette fonctionnalité était une limitation que tous les packages nécessaires à venir de la même source.  Avec NuGet 2.2.1 Cependant, vous pouvez avoir des packages installés à partir de plusieurs référentiels (dans le modèle, une extension VSIX ou dans un dossier sur le disque défini dans le Registre).

Le scénario principal de cette fonctionnalité est des modèles de projet ASP.NET personnalisés.  Les modèles d’ASP.NET intégrés utilisent des packages préinstallés, extraction de packages à partir du disque local.  Vous pouvez maintenant créer un modèle de projet ASP.NET personnalisé qui utilise les packages existants installés par ASP.NET et ajouter les packages NuGet supplémentaires dans votre modèle.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 2.2.1 comprend quelques correctifs de bogues ciblés. Pour obtenir la liste de travail éléments résolus dans NuGet 2.2.1, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problèmes connus

Si vous étendez des modèles de projet ASP.NET, tous les référentiels de packages préinstallés doivent utiliser la même valeur pour le `isPreunzipped` attribut.
