---
title: "Résolution des problèmes de restauration de packages NuGet dans Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Description des erreurs courantes liées à la restauration des packages NuGet dans Visual Studio et résolution de ces erreurs."
keywords: "Restauration des packages NuGet, restauration des packages, résolution des problèmes, résoudre les problèmes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a>Résolution des erreurs de restauration des packages

Cet article aborde les erreurs rencontrées couramment pendant la restauration de packages, ainsi que les étapes de résolution. Pour plus d’informations sur la restauration des packages, consultez [Restauration de packages](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Si les instructions présentées ici ne fonctionnent pas, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions examiner plus attentivement votre situation. N’utilisez pas le contrôle « Cette page est-elle utile ? » qui peut apparaître dans cette page, car celui-ci ne nous permet pas de vous contacter pour obtenir plus d’informations.

## <a name="quick-solution-for-visual-studio-users"></a>Solution rapide pour les utilisateurs de Visual Studio

Si vous utilisez Visual Studio, commencez par activer la restauration des packages comme suit. Sinon, passez aux autres sections de cet article.

1. Sélectionnez la commande de menu **Outils > Gestionnaire de package NuGet > Paramètres du Gestionnaire de package**.
1. Définissez les deux options sous **Restauration de package**.
1. Sélectionnez **OK**.
1. Regénérez votre projet.

![Activer la restauration des packages NuGet dans Outils/Options](../consume-packages/media/restore-01-autorestoreoptions.png)

Vous pouvez également changer ces paramètres dans votre fichier `NuGet.config` (consultez la section sur le [consentement](#consent)).

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Ce projet fait référence à un ou plusieurs packages NuGet qui ne figurent pas sur cet ordinateur

Message d’erreur complet :

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Cette erreur se produit quand vous essayez de générer un projet qui contient des références à un ou plusieurs packages NuGet, mais que ces derniers ne sont pas actuellement mis en cache dans le projet. (Les packages sont mis en cache dans un dossier `packages` à la racine de la solution si le projet utilise `packages.config`, ou dans le fichier `obj/project.assets.json` si le projet utilise le format PackageReference.)

Cette situation se produit souvent quand vous obtenez le code source d’un projet à partir du contrôle de code source ou d’un autre téléchargement. Les packages sont généralement omis du contrôle de code source ou des téléchargements car ils peuvent être restaurés à partir de flux de packages comme nuget.org. Pour plus d’informations, consultez [Packages et contrôle de code source](Packages-and-Source-Control.md)). Leur inclusion engendrerait l’encombrement du dépôt ou la création inutile de fichiers .zip volumineux.

Utilisez l’une des méthodes suivantes pour restaurer les packages :

- Dans Visual Studio, activez la restauration des packages. Pour cela, sélectionnez la commande de menu **Outils > Gestionnaire de Package NuGet > Paramètres du Gestionnaire de package**, définissez les deux options sous **Restauration de package**, puis sélectionnez **OK**. Ensuite, regénérez la solution.
- Pour les projets .NET Core, exécutez `dotnet restore` ou `dotnet build` (qui exécute automatiquement la restauration).
- Sur la ligne de commande, exécutez `nuget restore` (sauf pour les projets créés avec `dotnet` ; dans ce cas, utilisez `dotnet restore`).
- Sur la ligne de commande avec les projets utilisant le format PackageReference, exécutez `msbuild /t:restore`.

Après une restauration réussie, vous devriez voir soit un dossier `packages` (si vous utilisez `packages.config`), soit le fichier `obj/project.assets.json` (si vous utilisez PackageReference). Le projet doit à présent être généré. Si ce n’est pas le cas, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions vous contacter.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Le fichier de ressources project.assets.json est introuvable

Message d’erreur complet :

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Cette erreur se produit pour les mêmes raisons que celles décrites dans la [section précédente](#missing). Les solutions à adopter sont aussi les mêmes. Par exemple, l’exécution de `msbuild` sur un projet .NET Core obtenu à partir du contrôle de code source ne restaure pas automatiquement les packages. Dans ce cas, exécutez `msbuild /t:restore` suivi de `msbuild` ou utilisez `dotnet build` (qui restaure automatiquement les packages).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Un ou plusieurs packages NuGet devant être restaurés ne l’ont pas été en raison d’une absence de consentement

Message d’erreur complet :

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Cette erreur indique que la restauration des packages est désactivée dans votre configuration NuGet.

Vous pouvez changer les paramètres applicables dans Visual Studio comme décrit précédemment dans [Solution rapide pour les utilisateurs de Visual Studio](#quick-solution-for-visual-studio-users).

Vous pouvez également modifier ces paramètres dans le fichier `nuget.config` applicable (en général, `%AppData%\NuGet\NuGet.Config` sur Windows et `~/.nuget/NuGet/NuGet.Config` sur Mac/Linux). Vérifiez que les clés `enabled` et `automatic` sous `packageRestore` ont la valeur True :

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

Si vous modifiez les paramètres `packageRestore` directement dans `nuget.config`, redémarrez Visual Studio pour que la boîte de dialogue des options affiche les valeurs actuelles.

## <a name="other-potential-conditions"></a>Autres conditions potentielles

- Vous pouvez rencontrer des erreurs de build en raison de fichiers manquants. Dans ce cas, vous recevez un message vous demandant d’utiliser la restauration NuGet pour les télécharger. Toutefois, l’exécution d’une restauration peut indiquer que tous les packages sont déjà installés et qu’il n’y a rien à restaurer. Dans ce cas, supprimez le dossier `packages` (si vous utilisez `packages.config`) ou le fichier `obj/project.assets.json` (si vous utilisez PackageReference), puis réexécutez la restauration.

- Quand vous obtenez un projet à partir du contrôle de code source, les dossiers de votre projet peuvent être définis en lecture seule. Changez les autorisations des dossiers et réessayez de restaurer les packages.

- Vous utilisez peut-être une ancienne version de NuGet. Pour obtenir les dernières versions recommandées, accédez à [nuget.org/downloads](https://www.nuget.org/downloads). Pour Visual Studio 2015, nous vous recommandons d’utiliser la version 3.6.0.

Si vous rencontrez d’autres problèmes, [soumettez un problème sur GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) pour que nous puissions obtenir plus d’informations de votre part.