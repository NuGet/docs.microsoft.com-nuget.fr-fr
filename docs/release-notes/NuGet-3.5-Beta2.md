---
title: 3.5 Notes de version Bêta2
description: Notes de publication pour NuGet 3.5 bêta 2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551989"
---
# <a name="nuget-35-beta2-release-notes"></a>Notes de publication de NuGet 3.5 bêta 2

[Notes de publication NuGet 3.5 Beta](../release-notes/nuget-3.5-Beta.md) | [Notes de publication NuGet 3.5-RC](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 bêta 2 RTM a été publiée le 27 juin 2016 pour Visual Studio 2013 et de nuget.exe

[Journal des modifications complet](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Liste des problèmes](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Correctifs de bogues

* Message d’erreur de mise à jour à un manque de prise en charge de decrpytion de mot de passe dans .NET Core pour les flux authentifiés - [#2942](https://github.com/NuGet/Home/issues/2942)

* Console du Gestionnaire de package Get-Package échoue si le projet .NET Core est ouvert - [#2932](https://github.com/NuGet/Home/issues/2932)

* Corriger une gestion incorrecte des 403 dans la commande NuGet push [#2910](https://github.com/NuGet/Home/issues/2910)

* Résoudre les problèmes de désinstallation des packages d’une solution liée au contrôle de code source TFS lorsque disableSourceControlIntegration est définie sur true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Corriger la mise à jour de package pour tenir les packages non cible compte - [#2724](https://github.com/NuGet/Home/issues/2724)

* Utiliser le niveau de détail MSBuild pour définir des actions d’interface utilisateur - niveau de journal pour le Gestionnaire de package Nuget [#2705](https://github.com/NuGet/Home/issues/2705)

* Configuration de correctif NuGet est une erreur non valide dans les projets de site Web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Résoudre les problèmes liés au pack de `.csproj` lorsque les fichiers de contenu sont inclus - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource dans `NuGetDefaults.Config` (`ProgramData\NuGet`) ne fonctionne pas - [#2653](https://github.com/NuGet/Home/issues/2653)

* Résoudre le problème dans la version de Nuget 3.4.3 - valeur ne peut pas être null lors de la création de package - [#2648](https://github.com/NuGet/Home/issues/2648)

* Restauration utilise les informations d’identification stockées à partir de Nuget.Config pour les flux VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* Performances - correctif les allocations excessives dans le code de comparaison de version - [#2632](https://github.com/NuGet/Home/issues/2632)

* Résoudre les problèmes lorsque plusieurs instances de nuget.exe tente d’installer le package même en parallèle, [#2628](https://github.com/NuGet/Home/issues/2628)

* Performances - informations de dépendance de Cache pour les opérations de plusieurs projets - [#2619](https://github.com/NuGet/Home/issues/2619)

* Corriger le problème où vous ne pouvez pas des sources de package être ajoutés à partir des paramètres lors de la liste de source est vide - [#2617](https://github.com/NuGet/Home/issues/2617)

* Corriger les erreur trompeurs lorsque vous tentez d’installer le package dépend au moment du design façades - [#2594](https://github.com/NuGet/Home/issues/2594)

* Installation d’un package à partir de la console PackageManager avec le paramètre « All » tente uniquement la première source - [#2557](https://github.com/NuGet/Home/issues/2557)

* Résoudre les problèmes avec les packages qui ont des fichiers avec des temps d’écriture dans le futur (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Afficher exception lorsqu’une défaillance des projets de recherche dans la commande update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Contenu du package n’est pas restauré correctement lors de l’installation d’un package à partir d’une version 3.3 nuget + flux avec l’argument - NoCache lorsque le package contient `.nupkg` fichiers - [#2354](https://github.com/NuGet/Home/issues/2354)

* Correction d’un problème avec le package Installer (toutes les Sources) lorsque le package est manquant à partir de la source de 1 - [#2322](https://github.com/NuGet/Home/issues/2322)

* Installer des blocs si une source unique refuse l’autorisation - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` version plage doit substituer IncludeReferencedProjects - version - [#1983](https://github.com/NuGet/Home/issues/1983)

* Mise à jour de NuGet 3.3.0 échoue avec «... une contrainte supplémentaire défini dans packages.config empêche cette opération. » - [#1816](https://github.com/NuGet/Home/issues/1816)

* mise à jour de NuGet.exe supprime le nom fort de l’assembly et l’attribut privé. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Résoudre les problèmes avec le chemin d’accès relatif pour « DefaultPushSource » - [#1746](https://github.com/NuGet/Home/issues/1746)

* Améliorer les messages de défaillance du programme de résolution de mise à jour - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Fonctionnalités et modifications de comportement

* push de NuGet.exe - paramètre de délai d’attente ne fonctionne pas - [#2785](https://github.com/NuGet/Home/issues/2785)

* restauration de NuGet.exe ne produit pas `.props` et `.targets` pour les fichiers `.nuproj` projets (régression dans v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Besoin d’extensibilité API pour comparer des infrastructures avec importations - [#2633](https://github.com/NuGet/Home/issues/2633)

* Masquer les options de dépendance lors de l’utilisation `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* En-tête de version de nuget.exe dans une sortie détaillée - imprimer [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet doit prendre en charge les /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)