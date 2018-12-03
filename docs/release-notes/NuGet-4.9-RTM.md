---
title: Notes de publication de NuGet 4.9 RTM
description: Notes de publication de NuGet 4.9, avec notamment les problèmes connus, les résolutions de bogues, les nouvelles fonctionnalités et les DCR.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453771"
---
# <a name="nuget-49-release-notes"></a>Notes de publication NuGet 4.9

[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec NuGet 4.9.0.


Des versions en ligne de commande offrant les mêmes fonctionnalités sont également disponibles :
* NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)
* dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-490"></a>Récapitulatif : Nouveautés de la version 4.9.0

* Signature : configure ClientPolicies pour exiger l’utilisation d’un groupe d’auteurs et de référentiels de confiance répertoriés dans NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)

* Création de fichiers « .snupkg » qui contiennent les symboles dans un pack ; push amélioré pour comprendre le protocole nuget afin d’accepter les fichiers snupkg pour le serveur de symboles - [#6878](https://github.com/NuGet/Home/issues/6878)

* Plug-in d’informations d’identification NuGet V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* Licence de packages NuGet autonomes - [#4628](https://github.com/NuGet/Home/issues/4628)

* Possibilité d’activer les métadonnées « GeneratePathProperty » sur un objet PackageReference pour générer une propriété MSBuild par pack dans le répertoire Foo.Bar\1.0\" - [#6949](https://github.com/NuGet/Home/issues/6949)

* Meilleure réussite des clients avec les opérations NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

* Les avertissements convertis en erreurs (via WarnAsErrors) déclenchés par PackageExtraction ne doivent jamais quitter le package extrait - [#7445](https://github.com/NuGet/Home/issues/7445)

* Les packages mal signés ne doivent pas finir dans le dossier des packages globaux - [#7423](https://github.com/NuGet/Home/issues/7423)

* La génération de la redirection de liaison ne doit pas ignorer les assemblys de façade - [#7393](https://github.com/NuGet/Home/issues/7393)

* L’opération VersionRange Equals ne compare pas plages flottante - [#7324](https://github.com/NuGet/Home/issues/7324)

* Restauration : régression des performances à l’aide de la nouvelle pile .NET Core 2.1 HTTP - [#7314](https://github.com/NuGet/Home/issues/7314)

* La mise à jour d’un package ne doit pas modifier la propriété PrivateAssets d’un objet PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)

* Signature : la signature doit échouer si un package contient trop d’entrées (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)

* Le chemin de code « dotnet nuget push » doit prendre en charge le nouveau fournisseur d’informations d’identification - [#7233](https://github.com/NuGet/Home/issues/7233)

* Prise en charge des plug-ins d’exécution avec la culture dite indifférente (comme dans docker) - [#7223](https://github.com/NuGet/Home/issues/7223)

* « nuget sources add » ne doit pas supprimer les informations d’identification de NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)

* L’installation d’un objet devDependency PackageReference doit utiliser par défaut excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)

* Correction de l’option migrator afin qu’elle s’affiche pour tous les projets et affiche une erreur si le projet est incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)

* « dotnet add package » doit valider la restauration effectuée dans le fichier de ressources - [#6928](https://github.com/NuGet/Home/issues/6928)

* Signature : amélioration des messages d’erreur associés à la signature - [#6906](https://github.com/NuGet/Home/issues/6906)

* [Échec de test] [zh-TW] La chaîne « Package Manager Console » n’est pas localisée sur la Console du Gestionnaire de package - [#6381](https://github.com/NuGet/Home/issues/6381)

* Le message d’erreur « Unable to find project information » (Impossible de trouver des informations sur le projet) doit être un peu plus spécifique dans VS - [#5350](https://github.com/NuGet/Home/issues/5350)

* Message d’erreur inutile lorsque vous utilisez incorrectement une balise de version nuspec d’un pack nuget - [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - signature : prise en charge du protocole NuGet : ressource RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR - Le fichier .nupkg.metadata sera créé au cours de l’extraction du package - contient « content-hash » - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - ignorer la vérification authenticode des plug-ins lors de l’exécution sur Mono - [#7222](https://github.com/NuGet/Home/issues/7222)

[Liste de tous les problèmes résolus dans cette version 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Récapitulatif : Nouveautés de la version 4.9.1

* Ajout de la prise en charge de la lecture d’une écriture dans le fichier nuget.config via une nouvelle commande trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

* Correction de la génération de lien de licence - [#7515](https://github.com/NuGet/Home/issues/7515)

* Régression des codes d’erreur pour la validation des signatures- [#7492](https://github.com/NuGet/Home/issues/7492)

* Le package NuGet.Build.Tasks.Pack ne contient pas d’informations de licence - [#7379](https://github.com/NuGet/Home/issues/7379)

[Liste de tous les problèmes résolus dans cette version 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a>Problèmes connus

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a>dotnet.exe/nuget.exe n’utilise pas les informations d’identification lorsque le nom de la source contient un blanc - [#7517](https://github.com/NuGet/Home/issues/7517)

#### <a name="issue"></a>Problème
Si le nom de la source contient un espace, nuget.exe affiche une erreur de type `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`

#### <a name="workaround"></a>Solution de contournement
Modifiez le nom de la source pour supprimer tout espace.

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive génère une erreur sur Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problème
L’argument `--interactive` n’est pas transféré par l’interface CLI dotnet et génère l’erreur `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Solution de contournement
Exécutez une autre commande dotnet avec l’option interactive, par exemple `dotnet restore --interactive` et identifiez-vous. L’authentification peut-être mise en cache par le fournisseur des informations d’identification. Exécutez ensuite `dotnet nuget push`.

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a>Problèmes d’accessibilité LicenseAcceptanceWindow et LicenseFileWindow - [#7452](https://github.com/NuGet/Home/issues/7452)

#### <a name="issue"></a>Problème
La fenêtre d’acceptation de la licence et la fenêtre du fichier de licence présentent des problèmes d’accessibilité avec la navigation au clavier et la narration avec le lecteur d’écran et JAWS.

#### <a name="workaround"></a>Solution de contournement
Aucune solution de contournement.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Les packages dans FallbackFolders ont été installés de façon personnalisée par le kit SDK .NET Core et la validation de la signature échoue. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problème
Si vous utilisez dotnet.exe 2.x pour restaurer un projet qui cible netcoreapp 1.x et netcoreapp 2.x, le dossier de secours est traité comme un flux de fichier. Cela signifie que, lors de la restauration, NuGet sélectionnera le package dans le dossier de secours et essaiera de l’installer dans le dossier de packages globaux, et la validation de signature habituelle échouera.

#### <a name="workaround"></a>Solution de contournement
Désactivez l’utilisation du dossier de secours en n’attribuant aucune valeur au paramètre `RestoreAdditionalProjectSources`. `<RestoreAdditionalProjectSources/>` Utilisez cette option avec précaution car cela entraînera le téléchargement d’un grand nombre de packages à partir de NuGet.org, qui sinon auraient été restaurés à partir du dossier de secours.
