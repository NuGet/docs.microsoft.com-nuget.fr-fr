---
title: 3.5 Notes de version bêta 2 de
description: Notes de publication pour NuGet 3.5 bêta 2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08bbae00a3e63c2a1ff42d5cc04981eb02966850
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822342"
---
# <a name="nuget-35-beta2-release-notes"></a>Notes de mise à jour de NuGet 3.5 bêta 2

[Notes de version bêta de 3.5 NuGet](../release-notes/nuget-3.5-Beta.md) | [Notes 3.5 RC de NuGet](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 bêta 2 RTM publiée le 27 juin 2016 pour Visual Studio 2013 et nuget.exe

[Journal complet](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Liste des problèmes](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Correctifs de bogues

* Message d’erreur de mise à jour à un manque de prise en charge de decrpytion de mot de passe dans le .NET Core pour les flux authentifiés - [#2942](https://github.com/NuGet/Home/issues/2942)

* Get-Package la Console Gestionnaire de package échoue si les projets .NET Core sont open - [#2932](https://github.com/NuGet/Home/issues/2932)

* Corriger une gestion incorrecte des 403 dans une commande NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Résoudre les problèmes lors de la désinstallation des packages dans une solution liée au contrôle de code source TFS lorsque disableSourceControlIntegration a la valeur true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Corriger la mise à jour de package pour tenir les packages non cibles compte - [#2724](https://github.com/NuGet/Home/issues/2724)

* Utiliser le niveau de détail de MSBuild pour définir des actions d’interface utilisateur - niveau de journal pour le Gestionnaire de package Nuget [#2705](https://github.com/NuGet/Home/issues/2705)

* Corrigez la configuration NuGet est une erreur non valide dans les projets de site Web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Résoudre les problèmes de pack de `.csproj` lorsque les fichiers de contenu sont inclus - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource dans `NuGetDefaults.Config` (`ProgramData\NuGet`) ne fonctionne pas - [#2653](https://github.com/NuGet/Home/issues/2653)

* Corrigez le problème dans la version Nuget 3.4.3 - la valeur ne peut pas être null lors de la création de package - [#2648](https://github.com/NuGet/Home/issues/2648)

* L’instruction RESTORE utilise les informations d’identification stockées à partir de Nuget.Config pour les flux VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* Performances - correctif les allocations excessives dans le code de comparaison de version - [#2632](https://github.com/NuGet/Home/issues/2632)

* Résoudre les problèmes lorsque plusieurs instances de nuget.exe tente d’installer le même package en parallèle - [#2628](https://github.com/NuGet/Home/issues/2628)

* Performances - informations de dépendance de Cache pour les opérations de plusieurs projets - [#2619](https://github.com/NuGet/Home/issues/2619)

* Corrigez le problème où vous ne pouvez pas les sources de package ajoutées à partir de paramètres lors de la liste source est vide - [#2617](https://github.com/NuGet/Home/issues/2617)

* Corrigez trompeurs erreur lorsque vous tentez d’installer le package dépend au moment du design façades - [#2594](https://github.com/NuGet/Home/issues/2594)

* Installation d’un package à partir de la console PackageManager avec le paramètre « All » tente uniquement de première source - [#2557](https://github.com/NuGet/Home/issues/2557)

* Résoudre les problèmes avec les packages qui ont des fichiers avec des temps d’écriture dans le futur (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Afficher l’exception lors d’un échec des projets de recherche dans la commande update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Contenu du package n’est pas restauré correctement lors de l’installation d’un package à partir d’un v3.3 nuget + flux avec l’argument - NoCache lorsque le package contient `.nupkg` fichiers - [#2354](https://github.com/NuGet/Home/issues/2354)

* Problème de correctif avec package Installer (toutes les Sources) lorsque le package est manquant à partir de la source de 1 - [#2322](https://github.com/NuGet/Home/issues/2322)

* Installer des blocs si une seule source échoue autorisation - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` version plage doit substituer IncludeReferencedProjects - version - [#1983](https://github.com/NuGet/Home/issues/1983)

* Échec de la mise à jour de NuGet 3.3.0 avec ' une contrainte supplémentaire... défini dans packages.config empêche cette opération. » - [#1816](https://github.com/NuGet/Home/issues/1816)

* mise à jour de NuGet.exe supprime le nom fort d’assembly et l’attribut privé. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Résoudre les problèmes avec le chemin d’accès relatif pour « DefaultPushSource » - [#1746](https://github.com/NuGet/Home/issues/1746)

* Améliorer les messages de défaillance de programme de résolution de mise à jour - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Fonctionnalités et modifications de comportement

* push de NuGet.exe - paramètre de délai d’attente ne fonctionne pas - [#2785](https://github.com/NuGet/Home/issues/2785)

* restauration de NuGet.exe ne produit pas `.props` et `.targets` pour les fichiers `.nuproj` projets (régression dans v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Besoin d’extensibilité API pour comparer des infrastructures des importations - [#2633](https://github.com/NuGet/Home/issues/2633)

* Masquer les options de dépendance lors de l’utilisation `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Impression nuget.exe en-tête de version dans une sortie détaillée - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet doit prendre en charge pour /runtimes/ {rid} /nativeassets/ {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)