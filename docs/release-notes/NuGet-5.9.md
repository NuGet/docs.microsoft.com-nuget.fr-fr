---
title: Notes de publication de NuGet 5,9
description: Notes de publication de NuGet 5,9, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 1152af99cf1421918a42d0d1faa33f1452f54a8f
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323880"
---
# <a name="nuget-59-release-notes"></a>Notes de publication de NuGet 5,9

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio | Disponible dans les SDK .NET |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> installé avec Visual Studio 2019 avec une charge de travail .net Core
  
> [!NOTE]
> Visual Studio 16,9, MSBuild 16,9 et .NET 5.0.200 + requièrent NuGet.exe 5,9 ou version ultérieure.

## <a name="summary-whats-new-in-59"></a>Résumé : nouveautés de 5,9

* Ajouter l’élément de menu contextuel « mettre à jour » pour les dépendances de package qui lance l’interface utilisateur du gestionnaire de package avec des packages présélectionnés à mettre à jour- [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Cliquez avec le bouton droit sur l’expérience « mise à jour » du package](media/releasenotes-59-update.png)

* Afficher la version demandée (y compris la version flottante ou la demande de plage de versions) dans la colonne « version » de la liste de projets dans l’interface utilisateur du gestionnaire de package au niveau de la solution- [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Version demandée dans l’interface utilisateur du gestionnaire de package au niveau de la solution](media/releasenotes-59-requested-version.png)

* Suggestions de packages IntelliCode dans l’onglet Parcourir de l’interface utilisateur du gestionnaire de package publiée en tant que test A/B- [#10053](https://github.com/NuGet/Home/issues/10053)

* Étendez le `.nupkg.metadata` fichier pour inclure la source d’installation [#10354](https://github.com/NuGet/Home/issues/10354)

* Introduire une nouvelle propriété MSBuild pour exclure la sortie de génération pour des TFM spécifiques pendant la tâche de Pack- [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**DCR (demande de modification de la conception) :**

* L’icône d’icône de verrouillage lorsque la dernière version de package est installée n’est pas intuitive. L’ancien cycle vert était parfait- [#9789](https://github.com/NuGet/Home/issues/9789)

* Le niveau de détail de débogage NuGet doit indiquer l’origine d’un package : [#3055](https://github.com/NuGet/Home/issues/3055)

* Le Pack NuGet doit détecter les omissions incorrectes du point dans les numéros de version- [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Désactiver l’épinglage des dépendances transitives centrales- [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM : génère une erreur en cas d’absence de TPV- [#9441](https://github.com/NuGet/Home/issues/9441)

* Journaliser les contenthash de package lors de la restauration de la journalisation (pendant l’extraction)- [#10384](https://github.com/NuGet/Home/issues/10384)

* Implémentez un mécanisme de pré-inscription pour les projets de demande de tirage hérités qui appellent la restauration à la solution Open- [#9986](https://github.com/NuGet/Home/issues/9986)

* Le conseiller de package NuGet doit fonctionner quand plusieurs sources sont sélectionnées dans le gestionnaire de package- [#10433](https://github.com/NuGet/Home/issues/10433)

* Lors de la restauration à un niveau de détail normal, consignez la source à partir de laquelle un package est restauré- [#10461](https://github.com/NuGet/Home/issues/10461)

**Corrigé**

* INuGetPackageFileService-extraire des images et des licences incorporées pour Codespaces-Connected et standalone- [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE : IProjectMetadataContextInfo Formatter manquant- [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-perf] Réduisez les informations écrites dans centralTransitiveDependencyGroups- [#10002](https://github.com/NuGet/Home/issues/10002)

* Les opérations de restauration qui lèvent une exception en raison d’un projet qui n’est pas chargé sont signalées comme `NoOp` dans la télémétrie- [#9985](https://github.com/NuGet/Home/issues/9985)

* Les icônes avec certaines palettes de couleurs entraînent le blocage de l’interface utilisateur PM VS [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-perf] Réduire le clone PackageSpec lors de l’ajout des informations CPVM- [#10003](https://github.com/NuGet/Home/issues/10003)

* IU PM-asyncify icône chargement- [#10009](https://github.com/NuGet/Home/issues/10009)

* Délai de l’interface utilisateur lors du chargement des URL d’icône dans l’interface utilisateur PM- [#8505](https://github.com/NuGet/Home/issues/8505)

* Affinité de thread dans BitmapSource et les threads d’interface utilisateur WPF- [#9161](https://github.com/NuGet/Home/issues/9161)

* Avertissement pour l’avertissement NU5128 quand packastool avec l’alias TargetFramework- [#10097](https://github.com/NuGet/Home/issues/10097)

* La logique OutputPath des cibles de Pack dans une build personnalisée ne fonctionne pas correctement- [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE : mettre en cache l’instance IServiceBroker sur le client [#10141](https://github.com/NuGet/Home/issues/10141)

* Créer NuGetProjectActions pour la désinstallation de l’interface utilisateur PM une opération parallèle- [#9956](https://github.com/NuGet/Home/issues/9956)

* Performances : réduire UIDelays dans GetPackageSpecsAsync pour les projets hérités et les projets non-PR- [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` n’envoie pas plus d’un fichier- [#4393](https://github.com/NuGet/Home/issues/4393)

* La sortie est encapsulée sur 80 caractères sur macOS lors de la redirection- [#10198](https://github.com/NuGet/Home/issues/10198)

* La restauration échoue avec la <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406) source

* netcoreapp 5.0-Windows n’effectue pas d’aller-retour et n’analyse pas les informations de la plateforme- [#10177](https://github.com/NuGet/Home/issues/10177)

* Les projets CPS personnalisés requièrent la fonctionnalité de projet AssemblyReferences pour pouvoir être restaurés. - [#8071](https://github.com/NuGet/Home/issues/8071)

* La vérification de l’existence du fichier d’icône et de licence doit toujours utiliser une comparaison sensible à la casse- [#9817](https://github.com/NuGet/Home/issues/9817)

* Les restaurations DotnetCLiToolReference rendent difficile la raison des projets non-op Count/uptodateprojectscount- [#10038](https://github.com/NuGet/Home/issues/10038)

* Difficile de voir la zone de ligne en pointillés du format de package lors de la navigation par tabulation via la boîte de dialogue « choisir le format du gestionnaire de package NuGet » dans le thème sombre- [#9729](https://github.com/NuGet/Home/issues/9729)

* Exclure les références d’infrastructure transitives de `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* Les propriétés statiques du comparateur doivent être idempotent- [#10339](https://github.com/NuGet/Home/issues/10339)

* résoudre le chargement d’assembly de contrats internes (Fix RPS ou recevoir une exception)- [#9919](https://github.com/NuGet/Home/issues/9919)

* Remplacez GetService par GetServiceAsync dans NuGet. clients, part 1- [#10362](https://github.com/NuGet/Home/issues/10362)

* Les installations de l’interface de commande ne doivent pas installer les packages non répertoriés- [#7466](https://github.com/NuGet/Home/issues/7466)

* Restauration statique du graphique MSBuild-unnnecessary à propos de MSBuildStartupDirectory- [#10335](https://github.com/NuGet/Home/issues/10335)

* Les dépendances de projet de références marquées comme PrivateAssets ne doivent pas être incluses dans le fichier de verrouillage à jour, [#8565](https://github.com/NuGet/Home/issues/8565)

* Les projets SDK avec des données incorrectes n’indiquent pas les erreurs de restauration dans VS- [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 lors de la restauration d’une solution qui a des projets mixtes hérités et netstandard2 à partir de la ligne de commande avec LockedMode- [#9623](https://github.com/NuGet/Home/issues/9623)

* Pack comprend le contenu remis via des packages de dépendances dans le package du projet actuel (projets basés sur le kit de développement logiciel (SDK) uniquement)- [#8867](https://github.com/NuGet/Home/issues/8867)

* Ajouter des données de télémétrie pour les erreurs de l’API d’extensibilité VS de NuGet- [#10062](https://github.com/NuGet/Home/issues/10062)

* Ajoutez GenerateRestoreGraphFile dans la restauration de graphiques statiques pour améliorer la débogage.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Impossible d’ouvrir le gestionnaire de package NuGet- [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Narrator ne lit pas l’étiquette « licence » pour le lien « Apache-2,0 »- [#10425](https://github.com/NuGet/Home/issues/10425)

* Le message de la barre d’état de mise à jour n’est pas parfait dans VS- [#9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.jssur utilise un Framework cible incorrect [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces : corriger la télémétrie à partir de https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* L’erreur NU1004 disparaît lors de la génération de la solution après l’activation de « RestoreLockedMode »- [#8973](https://github.com/NuGet/Home/issues/8973)

* La tabulation par PMUI dans le sens inverse devrait être la direction de la transmission en miroir- [#10234](https://github.com/NuGet/Home/issues/10234)

* Le débogage de PMUI dans une instance expérimentale lève parfois une exception InvalidCastException de SolutionView à ProjectView- [#10416](https://github.com/NuGet/Home/issues/10416)

* La version par défaut est null après avoir cliqué sur un package déconseillé dans l’onglet Parcourir- [#10380](https://github.com/NuGet/Home/issues/10380)

* Le gestionnaire NuGet dans Visual Studio se recharge lorsque le focus est récupéré- [#4176](https://github.com/NuGet/Home/issues/4176)

* Supprimer IPackageSourceProvider2 et les types associés- [#10098](https://github.com/NuGet/Home/issues/10098)

* Le package « NameOfPackage » n’est pas compatible avec les infrastructures « tout » dans le projet- [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync n’effectue pas de comparaisons NuGetVersion, [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet. client doit remplacer l’utilisation de ManagedImageMonikers par KnownMonikers- [#9977](https://github.com/NuGet/Home/issues/9977)

* L’icône dépréciée chevauche la version du package déconseillé dans l’onglet Parcourir- [#10452](https://github.com/NuGet/Home/issues/10452)

* La gestion des erreurs PackageReference NU1604 est différente entre VS et la ligne de commande (Restore & Package Manager UI)- [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces : formateurs nécessaires non inscrits- [#10467](https://github.com/NuGet/Home/issues/10467)

* Supprimez Net45 comme Framework cible de NuGet. frameworks- [#10470](https://github.com/NuGet/Home/issues/10470)

* Implémentation : ajoutez de nouveaux télémétrie pour suivre les événements liés à PMC et à l’utilisation de PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Un seul package s’affiche dans la fenêtre Aperçu des modifications quand plusieurs packages sont disponibles pour la mise à jour dans l’interface utilisateur du gestionnaire de package- [#10483](https://github.com/NuGet/Home/issues/10483)

* Des groupes frameworkReferences vides doivent être générés lors de l’empaquetage de projets multiciblés- [#10218](https://github.com/NuGet/Home/issues/10218)

* Il est difficile d’afficher la case à cocher du package dans l’onglet « mises à jour » avec une zone de lignes en pointillés lorsque vous accédez à l’onglet en bleu/bleu (contraste supplémentaire) Thèmes/Light- [#8963](https://github.com/NuGet/Home/issues/8963)

* Les cases à cocher des onglets de mise à jour ne fonctionnent pas correctement avec les lecteurs d’écran- [#10449](https://github.com/NuGet/Home/issues/10449)

* La mise à jour dans PMUI provoque une référence d’objet non définie sur une instance d’un objet [#9882](https://github.com/NuGet/Home/issues/9882)

* Implémentation : ajoutez de nouveaux télémétrie pour suivre les événements liés à PMC et à l’utilisation de PowerShell suivi. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Erreur de copie/collage dans V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)

* NuGetPackageFileService Fix-utilisation de pour MemoryStream- [#10503](https://github.com/NuGet/Home/issues/10503) jetable

**[Liste de tous les problèmes résolus dans cette version-5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Liste des validations dans cette version-5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Contributions de la communauté

Merci à tous les contributeurs qui ont aidé à rendre cette version de NuGet extraordinaire !

|Qui|Tirage|Problèmes|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Erreur de copie/collage dans V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Tests manquants pour le cas où les packages sont référencés avec l’attribut PrivateAssets = "All"- [#10397](https://github.com/NuGet/Home/issues/10397)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Ajout de la prise en charge de l’envoi de plusieurs packages- [#4393](https://github.com/NuGet/Home/issues/4393)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | La génération de bibliothèques NuGet est rompue lorsque la signature d’assembly est désactivée- [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Nettoyez les documents de contribution- [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | La vérification de l’existence du fichier d’icône et de licence doit toujours utiliser une comparaison sensible à la casse- [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Utilisez BitmapCreateOptions. IgnoreColorProfile pour résoudre le problème WPF lors de l’utilisation de DecodePixelWidth- [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Le lien SDK Windows 10 est rompu dans NuGet. Guide de contribution client- [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Les liens relatifs sont rompus dans NuGet. Guide de débogage du client- [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Améliorez les contextes de test et les [#9996](https://github.com/NuGet/Home/issues/9996) de code associés
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | La sortie est encapsulée sur 80 caractères sur macOS lors de la redirection- [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Rendre NuGet. PackageManagement disponible en tant que package .NET Standard- [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Introduire une nouvelle propriété MSBuild pour exclure la sortie de génération pour des TFM spécifiques pendant la tâche de Pack- [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>Résumé : nouveautés de 5.9.1

* « dotnet NuGet Remove source nuget.org » ne fonctionne pas la première fois- [#10745](https://github.com/NuGet/Home/issues/10745)
* Désactivation de la validation par défaut sur Linux, mais activée par défaut sur Windows- [#10713](https://github.com/NuGet/Home/issues/10713)

**[Liste de tous les problèmes résolus dans cette version-5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Liste des validations dans cette version-5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="known-issues"></a>Problèmes connus

### <a name="nuget-59-pack-raises-null-reference-exception---10685"></a>le Pack NuGet 5,9 déclenche une `Null Reference` exception. - [#10685](https://github.com/NuGet/Home/issues/10685)

#### <a name="issue"></a>Problème
Quand String `pack` utilise un `.nuspec` fichier, la `NuGet 5.9` version lève une `null reference` exception si des [références d’assembly explicites](../reference/nuspec.md#explicit-assembly-references) sont spécifiées sans ajouter `reference groups` de pour les projets qui ciblent `multiple frameworks` .

#### <a name="workaround"></a>Solution de contournement
Utilisez `nuget.exe` [5.8.1](https://dist.nuget.org/win-x86-commandline/v5.8.1/nuget.exe)  ou la version la plus récente que `5.9.1` .

## <a name="feedback-welcome"></a>Commentaires

Vos commentaires sont très importants pour nous.  En cas de problème avec cette version, consultez nos [problèmes GitHub](https://github.com/NuGet/Home/issues) et la [communauté de développeurs Visual Studio](https://developercommunity.visualstudio.com/) pour les problèmes existants.  Pour les nouveaux problèmes dans NuGet, signalez un [problème GitHub](https://github.com/NuGet/Home/issues/new).
Pour les problèmes généraux d’expérience NuGet, faites-le nous savoir par le biais de l’option [signaler un problème](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) trouvée dans votre IDE favori sous **aide > signaler un problème**.
