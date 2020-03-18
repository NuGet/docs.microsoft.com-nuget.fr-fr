---
title: Fournisseurs d’informations d’identification NuGet. exe
description: les fournisseurs d’informations d’identification NuGet. exe s’authentifient avec un flux, et sont implémentés en tant qu’exécutables en ligne de commande qui suivent des conventions spécifiques.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428722"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Authentification de flux avec des fournisseurs d’informations d’identification NuGet. exe

La prise en charge de la version `3.3` a été ajoutée pour `nuget.exe` fournisseurs d’informations d’identification spécifiques. Depuis, dans la version `4.8` la [prise en charge des fournisseurs d’informations d’identification](NuGet-Cross-Platform-Authentication-Plugin.md) qui fonctionnent dans tous les scénarios de ligne de commande (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) a été ajoutée.

Pour plus d’informations sur toutes les approches d’authentification pour `nuget.exe`, consultez [consommation de packages à partir de flux authentifiés](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)

## <a name="nugetexe-credential-provider-discovery"></a>découverte de fournisseur d’informations d’identification NuGet. exe

les fournisseurs d’informations d’identification NuGet. exe peuvent être utilisés de trois manières :

- **Globalement**: pour mettre un fournisseur d’informations d’identification à la disposition de toutes les instances de `nuget.exe` s’exécuter sous le profil de l’utilisateur actuel, ajoutez-le à `%LocalAppData%\NuGet\CredentialProviders`. Vous devrez peut-être créer le dossier `CredentialProviders`. Les fournisseurs d’informations d’identification peuvent être installés à la racine du dossier `CredentialProviders` ou dans un sous-dossier. Si un fournisseur d’informations d’identification contient plusieurs fichiers/assemblys, vous pouvez utiliser des sous-dossiers pour organiser les fournisseurs.

- **À partir d’une variable d’environnement**: les fournisseurs d’informations d’identification peuvent être stockés n’importe où et rendus accessibles à `nuget.exe` en affectant à la variable d’environnement `%NUGET_CREDENTIALPROVIDERS_PATH%` l’emplacement du fournisseur. Cette variable peut être une liste séparée par des points-virgules (par exemple, `path1;path2`) si vous avez plusieurs emplacements.

- À **côté de NuGet. exe**: les fournisseurs d’informations d’identification NuGet. exe peuvent être placés dans le même dossier que `nuget.exe`.

Lors du chargement des fournisseurs d’informations d’identification, `nuget.exe` recherche les emplacements ci-dessus, dans l’ordre, pour tout fichier nommé `credentialprovider*.exe`, puis charge ces fichiers dans l’ordre où ils sont trouvés. Si plusieurs fournisseurs d’informations d’identification existent dans le même dossier, ils sont chargés dans l’ordre alphabétique.

## <a name="creating-a-nugetexe-credential-provider"></a>Création d’un fournisseur d’informations d’identification NuGet. exe

Un fournisseur d’informations d’identification est un exécutable de ligne de commande, nommé sous la forme `CredentialProvider*.exe`, qui recueille les entrées, acquiert les informations d’identification appropriées, puis retourne le code d’état de sortie et la sortie standard appropriés.

Un fournisseur doit effectuer les opérations suivantes :

- Déterminez si elle peut fournir des informations d’identification pour l’URI ciblé avant de lancer l’acquisition des informations d’identification. Si ce n’est pas le cas, il doit renvoyer le code d’État 1 sans informations d’identification.
- Ne modifiez pas `Nuget.Config` (par exemple, en définissant des informations d’identification).
- Gérez la configuration du proxy HTTP seul, car NuGet ne fournit pas d’informations de proxy au plug-in.
- Retournez les informations d’identification ou les détails de l’erreur à `nuget.exe` en écrivant un objet de réponse JSON (voir ci-dessous) dans stdout, en utilisant l’encodage UTF-8.
- Émettez éventuellement une journalisation de suivi supplémentaire vers stderr. Aucun secret ne doit jamais être écrit dans stderr, car à des niveaux de détail « normal » ou « détaillé », ces traces sont répercutées par NuGet sur la console.
- Les paramètres inattendus doivent être ignorés, ce qui fournit une compatibilité ascendante avec les futures versions de NuGet.

### <a name="input-parameters"></a>Paramètres d'entrée

| Paramètre/commutateur |Description|
|----------------|-----------|
| URI {valeur} | URI source du package nécessitant des informations d’identification.|
| NonInteractive | Si elle est présente, le fournisseur n’émet pas d’invites interactives. |
| IsRetry | S’il est présent, indique que cette tentative est une nouvelle tentative d’échec d’une tentative précédente. Les fournisseurs utilisent généralement cet indicateur pour s’assurer qu’ils contournent tout cache existant et demandent de nouvelles informations d’identification, si possible.|
| Verbosity {value} | S’il est présent, l’une des valeurs suivantes : « normal », « quiet » ou « detailed ». Si aucune valeur n’est fournie, la valeur par défaut est « normal ». Les fournisseurs doivent l’utiliser comme indication du niveau de journalisation facultatif à émettre au flux d’erreurs standard. |

### <a name="exit-codes"></a>Codes de sortie

| Code |Résultats | Description |
|----------------|-----------|-----------|
| 0 | Succès | Les informations d’identification ont été correctement acquises et ont été écrites dans stdout.|
| 1 | ProviderNotApplicable | Le fournisseur actuel ne fournit pas d’informations d’identification pour l’URI donné.|
| 2 | Échec | Le fournisseur est le fournisseur approprié pour l’URI donné, mais il ne peut pas fournir d’informations d’identification. Dans ce cas, NuGet. exe ne réessaiera pas l’authentification et échouera. Par exemple, un utilisateur annule une connexion interactive. |

### <a name="standard-output"></a>Sortie standard

| Propriété |Notes|
|----------------|-----------|
| Nom d’utilisateur | Nom d’utilisateur pour les demandes authentifiées.|
| Mot de passe | Mot de passe pour les demandes authentifiées.|
| Message | Détails facultatifs sur la réponse, utilisés uniquement pour afficher des détails supplémentaires dans les cas d’échec. |

Exemple stdout :

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Résolution des problèmes d’un fournisseur d’informations d’identification

À l’heure actuelle, NuGet ne fournit pas une prise en charge bien directe du débogage des fournisseurs d’informations d’identification personnalisés. le [problème 4598](https://github.com/NuGet/Home/issues/4598) suit ce travail.

Vous pouvez également effectuer les opérations suivantes :

- Exécutez NuGet. exe avec le commutateur `-verbosity` pour inspecter la sortie détaillée.
- Ajoutez des messages de débogage à `stdout` aux emplacements appropriés.
- Assurez-vous que vous utilisez NuGet. exe 3,3 ou une version ultérieure.
- Attachez le débogueur au démarrage avec cet extrait de code :

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
