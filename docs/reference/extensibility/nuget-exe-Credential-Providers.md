---
title: Fournisseurs d’informations d’identification NuGet.exe
description: fournisseurs d’informations d’identification NuGet.exe auprès d’un flux et sont implémentées en tant qu’exécutables de ligne de commande qui suivent les conventions spécifiques.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550187"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>L’authentification de flux avec des fournisseurs d’informations d’identification nuget.exe

*NuGet 3.3 +*

Lorsque `nuget.exe` a besoin d’informations d’identification pour s’authentifier avec un flux, il recherche les de la manière suivante :

1. NuGet recherche d’abord les informations d’identification dans `Nuget.Config` fichiers.
1. NuGet utilise ensuite les fournisseurs de plug-in informations d’identification, soumis à l’ordre indiqué ci-dessous. (Et de l’exemple est la [fournisseur d’informations d’identification de Visual Studio Team Services](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet invite ensuite l’utilisateur pour les informations d’identification sur la ligne de commande.

Notez que les fournisseurs d’informations d’identification décrites ici fonctionnent uniquement dans `nuget.exe` et non dans « dotnet restore » ou de Visual Studio. Pour les fournisseurs d’informations d’identification avec Visual Studio, consultez [nuget.exe fournisseurs d’informations d’identification pour Visual Studio](nuget-credential-providers-for-visual-studio.md)

fournisseurs d’informations d’identification NuGet.exe peuvent être utilisés de 3 façons :

- **Dans le monde entier**: de proposer un fournisseur d’informations d’identification pour toutes les instances de `nuget.exe` s’exécutent sous le profil utilisateur actuel, ajoutez-la à `%LocalAppData%\NuGet\CredentialProviders`. Vous devrez peut-être créer les `CredentialProviders` dossier. Les fournisseurs d’informations d’identification peuvent être installés à la racine de la `CredentialProviders` dossier ou dans un sous-dossier. Si un fournisseur d’informations d’identification a plusieurs fichiers/assemblys, vous pouvez utiliser des sous-dossiers pour conserver les fournisseurs organisés.

- **À partir d’une variable d’environnement**: les fournisseurs d’informations d’identification peuvent être stockés et rendus accessibles à `nuget.exe` en définissant le `%NUGET_CREDENTIALPROVIDERS_PATH%` variable d’environnement à l’emplacement du fournisseur. Cette variable peut être une liste délimitée par des points-virgules (par exemple, `path1;path2`) si vous disposez de plusieurs emplacements.

- **En même temps que nuget.exe**: fournisseurs d’informations d’identification nuget.exe peuvent être placés dans le même dossier que `nuget.exe`.

Lors du chargement des fournisseurs d’informations d’identification, `nuget.exe` recherche les emplacements ci-dessus, dans l’ordre, pour tous les fichiers nommés `credentialprovider*.exe`, puis charge ces fichiers dans l’ordre, elles sont trouvées. Si plusieurs fournisseurs d’informations d’identification existent dans le même dossier, elles sont chargées dans l’ordre alphabétique.

## <a name="creating-a-nugetexe-credential-provider"></a>Création d’un fournisseur d’informations d’identification nuget.exe

Un fournisseur d’informations d’identification est un exécutable de ligne de commande, sous la forme `CredentialProvider*.exe`, qui rassemble les entrées, acquiert des informations d’identification appropriées, puis retourne le code d’état de sortie appropriée et la sortie standard.

Un fournisseur doit effectuer ce qui suit :

- Déterminer si elle peut fournir des informations d’identification pour l’URI cible avant de lancer l’acquisition des informations d’identification. Si ce n’est pas le cas, elle doit retourner le code d’état 1 sans informations d’identification.
- Ne modifiez pas `Nuget.Config` (telles que la définition des informations d’identification il).
- Configuration du proxy HTTP de handle sur son propre, en tant que NuGet ne fournit pas les informations de proxy pour le plug-in.
- Retourner des informations d’identification ou les détails de l’erreur à `nuget.exe` en écrivant un objet de réponse JSON (voir ci-dessous) dans stdout, à l’aide du codage UTF-8.
- Éventuellement émettre de journalisation de suivi supplémentaires à stderr. Aucun secret ne doit jamais être écrites dans stderr, étant donné que les niveaux de détail « normale » ou « détaillé » ces traces sont répercutées par NuGet dans la console.
- Paramètres inattendus doivent être ignorées, en fournissant une compatibilité ascendante avec les futures versions de NuGet.

### <a name="input-parameters"></a>Paramètres d’entrée

| Paramètre/commutateur |Description|
|----------------|-----------|
| URI {value} | Informations d’identification de la nécessité d’une URI source du lot.|
| NonInteractive | Le cas échéant, fournisseur n’émet pas d’invites interactives. |
| isRetry | S’il est présent, indique que cette tentative est une nouvelle tentative d’une tentative ayant échouée précédemment. Fournisseurs utilisent généralement cet indicateur pour vous assurer qu’ils contournent n’importe quel cache existant et que vous invitent pour les nouvelles informations d’identification si possible.|
| Niveau de détail {value} | Le cas échéant, une des valeurs suivantes : « normal », « silencieux » ou « détaillé ». Si aucune valeur n’est fournie, valeur par défaut est « normal ». Fournisseurs doivent utiliser cela comme une indication du niveau de journalisation facultatives à émettre dans le flux d’erreur standard. |

### <a name="exit-codes"></a>Codes de sortie

| Code |Résultat | Description |
|----------------|-----------|-----------|
| 0 | Opération réussie | Informations d’identification ont été acquis et ont été écrites dans stdout.|
| 1 | ProviderNotApplicable | Le fournisseur actuel ne fournit pas les informations d’identification pour l’URI donné.|
| 2 | Échec | Le fournisseur est le fournisseur approprié pour l’URI donné, mais ne peut pas fournir les informations d’identification. Dans ce cas, nuget.exe ne sera pas relancé l’authentification et échoue. Un exemple classique est quand un utilisateur annule une connexion interactive. |

### <a name="standard-output"></a>Objet de flux de sortie standard

| Propriété |Notes|
|----------------|-----------|
| Utilisateur | Nom d’utilisateur pour les demandes authentifiées.|
| Mot de passe | Mot de passe pour les demandes authentifiées.|
| Message | Détails facultatifs sur la réponse, utilisée uniquement pour afficher des détails supplémentaires en cas d’échec. |

Exemple stdout :

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Résolution des problèmes d’un fournisseur d’informations d’identification

À l’heure actuelle, NuGet ne fournit pas beaucoup de support direct pour déboguer les fournisseurs d’informations d’identification personnalisées ; [émettre 4598](https://github.com/NuGet/Home/issues/4598) effectue le suivi de ce travail.

Vous pouvez également effectuer les opérations suivantes :

- Exécutez nuget.exe avec le `-verbosity` commutateur pour inspecter la sortie détaillée.
- Ajouter des messages de débogage à `stdout` dans les emplacements appropriés.
- N’oubliez pas que vous utilisez nuget.exe 3.3 ou version ultérieure.
- Attacher le débogueur au démarrage avec cet extrait de code :

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Pour plus d’informations, [soumettre une demande de prise en charge un nuget.org](https://www.nuget.org/policies/Contact).
