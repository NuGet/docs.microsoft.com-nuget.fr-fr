---
title: Notes de publication de NuGet 4.7 RTM
description: Notes de publication de NuGet 4.7.0, avec notamment les problèmes connus, les résolutions de bogues, les fonctionnalités ajoutées et les DCR.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: f1397e2f42fd65c3a883c864bd430ba5892c12b2
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432524"
---
# <a name="nuget-47-release-notes"></a>Notes de publication de NuGet 4.7

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-470"></a>Résumé : Nouveautés de la version 4.7.0

* Nous avons complété la signature du package pour activer les [packages signés de référentiel](https://github.com/NuGet/Home/wiki/Repository-Signatures).

* Dans la version 15.7 de Visual Studio, nous avons introduit la possibilité de [migrer des projets existants du format packages.config à PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference).

## <a name="summary-whats-new-in-472"></a>Résumé : Nouveautés de la version 4.7.2

* Correctif de sécurité : Les autorisations sur les fichiers créés dans ~/.nuget sont trop ouvertes [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>Résumé : Nouveautés de la version 4.7.3

* Correctif de sécurité : Les fichiers dans les NUPKG peuvent avoir un chemin relatif au-dessus du répertoire NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Problèmes connus

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>L’option `Migrate packages.config to PackageReference...` n’est pas disponible dans le menu contextuel

#### <a name="issue"></a>Problème

À la première ouverture d’un projet, il peut arriver que NuGet ne s’initialise pas tant qu’aucune opération NuGet n’a été réalisée. Dans ce cas, l’option de migration ne s’affiche pas dans le menu contextuel sur `packages.config` ou `References`.

#### <a name="workaround"></a>Solution de contournement

Effectuez l’une des actions NuGet suivantes :
* Ouvrez l’interface utilisateur du Gestionnaire de package : cliquez avec le bouton droit sur `References` et sélectionnez `Manage NuGet Packages...`.
* Ouvrez la console du Gestionnaire de package : dans `Tools > NuGet Package Manager`, sélectionnez `Package Manager Console`.
* Exécutez la restauration NuGet : cliquez avec le bouton droit sur le nœud de la solution dans l’Explorateur de solutions, puis sélectionnez `Restore NuGet Packages`.
* Générez le projet qui déclenche également la restauration NuGet.

L’option de migration devrait apparaître. Notez qu’elle n’est pas prise en charge et ne s’affiche pas pour les types de projets ASP.NET et C++.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problèmes liés à .NET Standard 2.0 avec .NET Framework & NuGet

.NET Standard et ses outils ont été conçus de façon à ce que les projets qui ciblent le .NET Framework 4.6.1 puissent consommer les projets et les packages NuGet ciblant .NET Standard 2.0 ou antérieur. [Ce document](https://github.com/dotnet/standard/issues/481) récapitule les problèmes liés à ce scénario et propose des solutions de contournement que vous pouvez déployer avec les outils actuellement disponibles.

## <a name="top-issues-fixed-in-this-release"></a>Principaux problèmes résolus dans cette version

### <a name="bugs"></a>Bogues

* NuGet se bloque dans le système de projet .NET Core (nouvelle régression). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pack : PackagePath est construit de manière incorrecte si TfmSpecificPackageFile est utilisé avec des chemins d’accès avec utilisation des caractères génériques. – [#6726](https://github.com/NuGet/Home/issues/6726)
* Pack : Un projet d’API web ne peut pas créer de packages, sauf si ispackable est défini explicitement. - [#6156](https://github.com/NuGet/Home/issues/6156)
* L’interface utilisateur de VS et PMC mettent 30 minutes à voir un nouveau package (nuget.exe le repère immédiatement). – [#6657](https://github.com/NuGet/Home/issues/6657)
* Signature :  SignatureUtility.GetCertificateChain(...) ne vérifie pas tous les états de chaînes. – [#6565](https://github.com/NuGet/Home/issues/6565)
* Signature : Améliorer la gestion de GeneralizedTime DER. – [#6564](https://github.com/NuGet/Home/issues/6564)
* Signature : VS n’affiche pas d’erreur NU3002 lors de l’installation d’un package falsifié. – [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary respecte la casse. – [#6500](https://github.com/NuGet/Home/issues/6500)
* Le code de restauration installer/mettre à jour et les chemins d’accès du code de restauration ne sont pas cohérents. – [#3471](https://github.com/NuGet/Home/issues/3471)
* La solution PackageManager version ComboBox peut sélectionner un séparateur avec le clavier. – [#2606](https://github.com/NuGet/Home/issues/2606)
* Impossible de charger l’index de service pour la source `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException : Le code d’état de la réponse n’indique pas une réussite : 403 (Interdit) – [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCR

* Émettez l’en-tête X-NuGet-Session-Id pour mettre en corrélation les différentes demandes [proposition de fonctionnalité]. – [#5330](https://github.com/NuGet/Home/issues/5330)
* Trouvez un moyen d’attendre la fin de l’exécution de l’opération de restauration dans Visual Studio via les API IV. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe – NoServiceEndpoint permet d’éviter d’ajouter le suffixe d’URL du service. – [#6586](https://github.com/NuGet/Home/issues/6586)
* Ajoutez un hachage de validation à la version d’information. – [#6492](https://github.com/NuGet/Home/issues/6492)
* Signature : Autorisez la suppression de la signature/contre-signature de référentiel. – [#6646](https://github.com/NuGet/Home/issues/6646)
* Signature :  API pour enlever la signature/contre-signature de référentiel. – [#6589](https://github.com/NuGet/Home/issues/6589)
* Consignez les informations relatives à la source dans VS. – [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtrez /tools sur TFM et RID uniquement, afin que le XML de paramètres puisse être placé dans le dossier /tools – [#6197](https://github.com/NuGet/Home/issues/6197)
* Lancez un avertissement lorsque la commande Pack exclut un fichier qui commence par « . ».  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Liste de tous les problèmes résolus dans cette version](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
