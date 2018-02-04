---
title: "Fournisseurs d’informations d’identification de NuGet.exe | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "fournisseurs d’informations d’identification de NuGet.exe auprès d’un flux et sont implémentées comme des exécutables de ligne de commande qui suivent les conventions spécifiques."
keywords: "fournisseurs d’informations d’identification de NuGet.exe, informations d’identification du fournisseur, auprès de l’alimentation, auprès de la galerie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Flux de l’authentification avec les fournisseurs d’informations d’identification de nuget.exe

*NuGet 3.3 +*

Lorsque `nuget.exe` a besoin d’informations d’identification pour s’authentifier auprès d’un flux, il recherche de la manière suivante :

1. NuGet recherche d’abord les informations d’identification dans `Nuget.Config` fichiers.
1. NuGet utilise ensuite les fournisseurs d’informations d’identification du plug-in, soumis à l’ordre indiqué ci-dessous. (Et est par exemple le [fournisseur d’informations d’identification de Visual Studio Team Services](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet puis invite l’utilisateur pour les informations d’identification sur la ligne de commande.

Notez que les fournisseurs d’informations d’identification décrites ici fonctionnent uniquement dans `nuget.exe` et non dans 'dotnet restore' ou de Visual Studio. Pour les fournisseurs d’informations d’identification avec Visual Studio, consultez [nuget.exe fournisseurs d’informations d’identification pour Visual Studio](nuget-credential-providers-for-visual-studio.md)

fournisseurs d’informations d’identification de NuGet.exe peuvent être utilisés de 3 façons :

- **Global**: de proposer un fournisseur d’informations d’identification pour toutes les instances de `nuget.exe` s’exécutent sous le profil utilisateur actuel, ajoutez-la à `%LocalAppData%\NuGet\CredentialProviders`. Il se pouvez que vous deviez créer le `CredentialProviders` dossier. Les fournisseurs d’informations d’identification peuvent être installés à la racine de la `CredentialProviders` dossier ou dans un sous-dossier. Si un fournisseur d’informations d’identification a plusieurs fichiers/assemblys, vous pouvez utiliser des sous-dossiers pour conserver les fournisseurs organisés.

- **À partir d’une variable d’environnement**: les fournisseurs d’informations d’identification peuvent être stockés partout et accessibles via `nuget.exe` en définissant le `%NUGET_CREDENTIALPROVIDERS_PATH%` variable d’environnement à l’emplacement du fournisseur. Cette variable peut être une liste délimitée par des points-virgules (par exemple, `path1;path2`) si vous disposez de plusieurs emplacements.

- **En même temps que nuget.exe**: fournisseurs d’informations d’identification de nuget.exe peuvent être placées dans le même dossier que `nuget.exe`.

Lors du chargement des fournisseurs d’informations d’identification, `nuget.exe` recherche les emplacements ci-dessus, dans l’ordre, pour tous les fichiers nommés `credentialprovider*.exe`, charge ensuite ces fichiers dans l’ordre, elles sont détectées. S’il existe plusieurs fournisseurs d’informations d’identification dans le même dossier, qu’elles sont chargées dans l’ordre alphabétique.

## <a name="creating-a-nugetexe-credential-provider"></a>Création d’un fournisseur d’informations d’identification de nuget.exe

Un fournisseur d’informations d’identification est un exécutable de ligne de commande, appelé dans le formulaire `CredentialProvider*.exe`, qui rassemble les entrées, acquiert des informations d’identification comme approprié, puis retourne le code d’état de sortie appropriée et la sortie standard.

Un fournisseur doit effectuer le des opérations suivantes :

- Déterminer si elle peut fournir des informations d’identification pour l’URI cible avant de lancer l’acquisition des informations d’identification. Si ce n’est pas le cas, elle doit retourner le code d’état 1 sans informations d’identification.
- Ne modifiez pas `Nuget.Config` (telles que la définition des informations d’identification il).
- Configuration du proxy HTTP de handle sur son propre comme NuGet ne fournit pas les informations de proxy pour le plug-in.
- Retourner des informations d’identification ou des détails de l’erreur à `nuget.exe` en écrivant un objet de réponse JSON (voir ci-dessous) dans stdout, à l’aide du codage UTF-8.
- Si vous le souhaitez émettre de journalisation de suivi supplémentaires vers stderr. Aucun secret ne doit est écrite dans stderr, étant donné que les niveaux de détail « normal » ou « détaillé » ces traces sont répercutées par NuGet dans la console.
- Paramètres inattendus doivent être ignorées, en fournissant une compatibilité ascendante avec les futures versions de NuGet.

### <a name="input-parameters"></a>Paramètres d’entrée

| Commutateur de paramètre / |Description|
|----------------|-----------|
| Uri {value} | Le package source des informations d’identification nécessitant des URI.|
| Non interactif | S’il est présent, le fournisseur n’émet pas invites interactives. |
| IsRetry | Le cas échéant, indique que cette tentative est une nouvelle tentative d’une tentative ayant échouée précédemment. Fournisseurs utilisent généralement cet indicateur pour vous assurer qu’ils contournent un cache existant et demander de nouvelles informations d’identification, si possible.|
| Niveau de détail {value} | Le cas échéant, une des valeurs suivantes : « normal », « silencieuse » ou « détaillé ». Si aucune valeur n’est fournie, valeur par défaut est « normal ». Fournisseurs doivent utiliser cela comme une indication du niveau de journalisation facultatives pour émettre le flux d’erreur standard. |

### <a name="exit-codes"></a>Codes de sortie

| Code |Résultat | Description |
|----------------|-----------|-----------|
| 0 | Opération réussie | Informations d’identification ont été acquis avec succès et ont été écrites dans stdout.|
| 1 | ProviderNotApplicable | Le fournisseur actuel ne fournit pas les informations d’identification de l’URI spécifié.|
| 2 | Échec | Le fournisseur est le fournisseur approprié pour l’URI donné, mais ne peut pas fournir les informations d’identification. Dans ce cas, nuget.exe ne sera pas relancé l’authentification et échoue. Un exemple classique est lorsqu’un utilisateur annule une connexion interactive. |

### <a name="standard-output"></a>Objet de flux de sortie standard

| Propriété |Notes|
|----------------|-----------|
| Utilisateur | Nom d’utilisateur pour les demandes authentifiées.|
| Mot de passe | Mot de passe pour les requêtes authentifiées.|
| Message | Détails facultatifs sur la réponse, utilisé uniquement pour afficher des détails supplémentaires en cas d’échec. |

Exemple stdout :

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Résolution des problèmes d’un fournisseur d’informations d’identification

À l’heure actuelle, NuGet ne fournit pas de prise en charge directe pour déboguer les fournisseurs d’informations d’identification personnalisées ; [émettre 4598](https://github.com/NuGet/Home/issues/4598) effectue le suivi de ce travail.

Vous pouvez également effectuer les opérations suivantes :

- Exécutez nuget.exe avec la `-verbosity` commutateur pour inspecter une sortie détaillée.
- Ajouter des messages de débogage pour `stdout` endroits appropriés.
- N’oubliez pas que vous utilisez nuget.exe 3.3 ou ultérieure.
- Attacher le débogueur au démarrage avec cet extrait de code :

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Pour plus d’informations, [soumettre une demande de prise en charge un nuget.org](https://www.nuget.org/policies/Contact).
