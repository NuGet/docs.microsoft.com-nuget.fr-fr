---
title: Notes de publication de 3,5 beta2
description: Notes de publication de NuGet 3,5 Beta 2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776393"
---
# <a name="nuget-35-beta2-release-notes"></a>Notes de publication de NuGet 3,5 beta2

Notes de publication [de NuGet 3,5-Beta](../release-notes/nuget-3.5-Beta.md)  |  [Notes de publication de NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)

La version RTM de NuGet 3,5 bêta 2 a été publiée le 27 juin 2016 pour Visual Studio 2013 et nuget.exe

[Journal des modifications complet](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Liste des problèmes](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Résolutions de bogues

* Mise à jour du message d’erreur en absence de prise en charge du mot de passe decrpytion dans .NET Core pour les flux authentifiés- [#2942](https://github.com/NuGet/Home/issues/2942)

* La console du gestionnaire de package Get-Package échoue si le projet .NET Core est ouvert- [#2932](https://github.com/NuGet/Home/issues/2932)

* Correction de la gestion incorrecte de 403 dans la commande NuGet Push [#2910](https://github.com/NuGet/Home/issues/2910)

* Résoudre les problèmes de désinstallation des packages dans une solution liée au contrôle de code source TFS quand disableSourceControlIntegration a la valeur true- [#2739](https://github.com/NuGet/Home/issues/2739)

* Corriger la mise à jour du package pour prendre en compte les packages non cibles- [#2724](https://github.com/NuGet/Home/issues/2724)

* Utiliser le niveau de détail MSBuild pour définir le niveau de journalisation pour les actions d’interface utilisateur du gestionnaire de package NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)

* Corriger la configuration NuGet n’est pas une erreur dans les projets de site Web-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* Corriger les problèmes de package à partir du `.csproj` moment où les fichiers de contenu sont inclus- [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource dans `NuGetDefaults.Config` ( `ProgramData\NuGet` ) ne fonctionne pas- [#2653](https://github.com/NuGet/Home/issues/2653)

* Résoudre le problème dans NuGet 3.4.3 Release-la valeur ne peut pas être null lors de la création du package- [#2648](https://github.com/NuGet/Home/issues/2648)

* La restauration utilise les informations d’identification stockées à partir de Nuget.Config pour les flux VSTS, [#2647](https://github.com/NuGet/Home/issues/2647)

* Performances-corriger des allocations excessives dans le code de la version d’analyse de version- [#2632](https://github.com/NuGet/Home/issues/2632)

* Résoudre les problèmes lorsque plusieurs instances de nuget.exe essaient d’installer le même package en parallèle [#2628](https://github.com/NuGet/Home/issues/2628)

* Performances-mettre en cache les informations de dépendance pour les opérations de projets multiples- [#2619](https://github.com/NuGet/Home/issues/2619)

* Résoudre le problème où les sources de package ne sont pas ajoutées à partir des paramètres lorsque la liste source est vide- [#2617](https://github.com/NuGet/Home/issues/2617)

* Corriger l’erreur trompeuse lors de la tentative d’installation du package qui dépend des façades au moment de la conception- [#2594](https://github.com/NuGet/Home/issues/2594)

* L’installation d’un package à partir de la console PackageManager avec le paramètre « All » essaie uniquement la première source [#2557](https://github.com/NuGet/Home/issues/2557)

* Résoudre les problèmes liés aux packages dont les fichiers ont des temps d’écriture à l’avenir (mono)- [#2518](https://github.com/NuGet/Home/issues/2518)

* Afficher une exception en cas d’échec lors de la recherche de projets dans la commande de mise à jour [#2418](https://github.com/NuGet/Home/issues/2418)

* Le contenu du package n’est pas restauré correctement lors de l’installation d’un package à partir d’un flux NuGet v 3.3 + avec l’argument-NoCache quand le package contient `.nupkg` des fichiers- [#2354](https://github.com/NuGet/Home/issues/2354)

* Résoudre le problème d’installation du package (toutes les sources) quand le package est manquant dans 1 [#2322](https://github.com/NuGet/Home/issues/2322) source

* Installer les blocs si une seule source ne parvient pas à obtenir l’autorisation- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` la plage de versions doit remplacer-IncludeReferencedProjects version- [#1983](https://github.com/NuGet/Home/issues/1983)

* La mise à jour NuGet 3.3.0 échoue avec «une contrainte supplémentaire... défini dans packages.config empêche cette opération.» - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe mise à jour supprime le nom fort et l’attribut privé de l’assembly. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Résoudre les problèmes liés au chemin de fichier relatif pour « DefaultPushSource »- [#1746](https://github.com/NuGet/Home/issues/1746)

* Améliorer les messages d’échec du programme de résolution des mises à jour- [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Fonctionnalités et changements de comportement

* Le paramètre nuget.exe Push-Timeout ne fonctionne pas- [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe restauration ne produit pas les `.props` `.targets` fichiers et pour les `.nuproj` projets (régression dans v 3.4.3.855)- [#2711](https://github.com/NuGet/Home/issues/2711)

* Nécessite une API d’extensibilité pour comparer des frameworks à des importations- [#2633](https://github.com/NuGet/Home/issues/2633)

* Masquer les options de dépendance lors de l’utilisation de `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Imprimer l’en-tête de version nuget.exe dans la sortie détaillée- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet doit ajouter la prise en charge de/runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)