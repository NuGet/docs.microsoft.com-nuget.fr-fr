---
title: Plug-ins inter-plateforme NuGet
description: Plug-ins inter-plateforme NuGet pour NuGet. exe, dotnet. exe, MSBuild. exe et Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380500"
---
# <a name="nuget-cross-platform-plugins"></a>Plug-ins inter-plateforme NuGet

Dans NuGet 4.8 +, la prise en charge des plug-ins multiplateforme a été ajoutée.
Pour cela, vous devez créer un nouveau modèle d’extensibilité de plug-in, qui doit se conformer à un ensemble strict de règles d’opération.
Les plug-ins sont des exécutables autonomes (Runnables dans le monde de .NET Core), que les clients NuGet lancent dans un processus distinct.
Il s’agit d’un plug-in réel en écriture unique, Run Everywhere. Il fonctionne avec tous les outils clients NuGet.
Les plug-ins peuvent être .NET Framework (NuGet. exe, MSBuild. exe et Visual Studio) ou .NET Core (dotnet. exe).
Un protocole de communication avec version entre le client NuGet et le plug-in est défini. Au cours de l’établissement de liaison de démarrage, les 2 processus négocient la version du protocole.

Pour couvrir tous les scénarios d’outils clients NuGet, vous devez disposer d’un .NET Framework et d’un plug-in .NET Core.
La description ci-dessous décrit les combinaisons client/Framework des plug-ins.

| Outil client  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet. exe | .NET Core |
| NuGet. exe | .NET Framework |
| MSBuild. exe | .NET Framework |
| NuGet. exe sur mono | .NET Framework |

## <a name="how-does-it-work"></a>Comment cela fonctionne-t-il ?

Le flux de travail de haut niveau peut être décrit comme suit :

1. NuGet Découvre les plug-ins disponibles.
1. Le cas échéant, NuGet effectue une itération sur les plug-ins par ordre de priorité et les démarre un par un.
1. NuGet utilise le premier plug-in qui peut traiter la demande.
1. Les plug-ins sont arrêtés lorsqu’ils ne sont plus nécessaires.

## <a name="general-plugin-requirements"></a>Exigences générales du plug-in

La version actuelle du protocole est *2.0.0*.
Dans cette version, les conditions requises sont les suivantes :

- Avoir un assembly de signature Authenticode valide et approuvé qui s’exécutera sur Windows et mono. Il n’existe pas encore d’exigence de confiance spéciale pour les assemblys exécutés sur Linux et Mac. [Problème pertinent](https://github.com/NuGet/Home/issues/6702)
- Prend en charge le lancement sans état dans le contexte de sécurité actuel des outils clients NuGet. Par exemple, les outils clients NuGet n’effectuent pas d’élévation ou d’initialisation supplémentaire en dehors du protocole de plug-in décrit plus loin.
- Être non interactif, sauf spécification explicite.
- Adhérer à la version du protocole de plug-in négocié.
- Répondez à toutes les demandes dans un délai raisonnable.
- Honorez les demandes d’annulation pour toute opération en cours.

La spécification technique est décrite plus en détail dans les spécifications suivantes :

- [Plug-in de téléchargement de package NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Plug-in d’authentification Cross plat NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Interaction client-plug-in

Les outils clients NuGet et les plug-ins communiquent avec JSON sur les flux standard (stdin, stdout, stderr). Toutes les données doivent être encodées en UTF-8.
Les plug-ins sont lancés avec l’argument « -plugin ». Si un utilisateur lance directement un exécutable de plug-in sans cet argument, le plug-in peut fournir un message d’information au lieu d’attendre une négociation de protocole.
Le délai d’expiration de la négociation de protocole est de 5 secondes. Le plug-in doit effectuer l’installation dans un montant aussi réduit que possible.
Les outils clients NuGet interrogent les opérations prises en charge par un plug-in en passant l’index de service pour une source NuGet. Un plug-in peut utiliser l’index de service pour vérifier la présence de types de service pris en charge.

La communication entre les outils clients NuGet et le plug-in est bidirectionnelle. Chaque demande a un délai d’expiration de 5 secondes. Si les opérations sont censées prendre plus de temps, le processus concerné doit envoyer un message de progression pour empêcher l’expiration du délai d’attente de la demande. Après 1 minute d’inactivité, un plug-in est considéré comme inactif et est arrêté.

## <a name="plugin-installation-and-discovery"></a>Installation et détection du plug-in

Les plug-ins seront découverts via une structure de répertoires basée sur une convention.
Les scénarios CI/CD et les utilisateurs avec pouvoir peuvent utiliser des variables d’environnement pour remplacer le comportement. Lorsque vous utilisez des variables d’environnement, seuls les chemins d’accès absolus sont autorisés. Notez que `NUGET_NETFX_PLUGIN_PATHS` et `NUGET_NETCORE_PLUGIN_PATHS` sont uniquement disponibles avec 5.3 + version des outils NuGet et versions ultérieures.

- `NUGET_NETFX_PLUGIN_PATHS` : définit les plug-ins qui seront utilisés par les outils basés sur .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio). Est prioritaire sur `NUGET_PLUGIN_PATHS`. (NuGet version 5.3 + uniquement)
- `NUGET_NETCORE_PLUGIN_PATHS` : définit les plug-ins qui seront utilisés par les outils basés sur .NET Core (dotnet. exe). Est prioritaire sur `NUGET_PLUGIN_PATHS`. (NuGet version 5.3 + uniquement)
- `NUGET_PLUGIN_PATHS` : définit les plug-ins qui seront utilisés pour ce processus NuGet, priorité préservée. Si cette variable d’environnement est définie, elle remplace la détection basée sur une convention. Ignoré si l’une des variables spécifiques à l’infrastructure est spécifiée.
-  Utilisateur-emplacement, emplacement d’hébergement NuGet dans `%UserProfile%/.nuget/plugins`. Cet emplacement ne peut pas être remplacé. Un répertoire racine différent sera utilisé pour les plug-ins .NET Core et .NET Framework.

| Framework | Emplacement de la détection racine  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Chaque plug-in doit être installé dans son propre dossier.
Le point d’entrée du plug-in sera le nom du dossier installé, avec les extensions. dll pour .NET Core et l’extension. exe pour .NET Framework.

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> Il n’existe actuellement aucun récit utilisateur pour l’installation des plug-ins. C’est aussi simple que de déplacer les fichiers requis à l’emplacement prédéterminé.

## <a name="supported-operations"></a>Opérations prises en charge

Deux opérations sont prises en charge dans le nouveau protocole de plug-in.

| Nom de l’opération | Version de protocole minimale | Version minimale du client NuGet |
| -------------- | ----------------------- | --------------------- |
| Télécharger le package | 1.0.0 | 4.3.0 |
| [Authentification](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Exécution de plug-ins sous le runtime approprié

Pour le NuGet dans les scénarios dotnet. exe, les plug-ins doivent être en mesure de s’exécuter sous ce Runtime spécifique du dotNET. exe.
Il se trouve sur le fournisseur de plug-ins et le consommateur pour s’assurer qu’une combinaison dotnet. exe/plugin compatible est utilisée.
Un problème potentiel peut survenir avec les plug-ins d’emplacement utilisateur quand, par exemple, un dotnet. exe sous le runtime 2,0 essaie d’utiliser un plug-in écrit pour le runtime 2,1.

## <a name="capabilities-caching"></a>Mise en cache des fonctionnalités

La vérification de la sécurité et l’instanciation des plug-ins sont coûteux. L’opération de téléchargement se produit plus fréquemment que l’opération d’authentification, mais l’utilisateur NuGet moyen est uniquement susceptible d’avoir un plug-in d’authentification.
Pour améliorer l’expérience, NuGet met en cache les revendications d’opération pour la demande donnée. Ce cache est par plug-in dont la clé de plug-in est le chemin du plug-in, et l’expiration pour ce cache de fonctionnalités est de 30 jours. 

Le cache se trouve dans `%LocalAppData%/NuGet/plugins-cache` et est remplacé par la variable d’environnement `NUGET_PLUGINS_CACHE_PATH`. Pour effacer ce [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), vous pouvez exécuter la commande variables locales avec l’option `plugins-cache`.
L’option variables locales `all` va également supprimer le cache des plug-ins. 

## <a name="protocol-messages-index"></a>Index des messages de protocole

Messages de la version de protocole *1.0.0* :

1.  Close
    * Direction de la requête : plug-in NuGet->
    * La demande ne contient pas de charge utile
    * Aucune réponse n’est attendue.  La réponse appropriée est que le processus du plug-in s’arrête rapidement.

2.  Copier les fichiers dans le package
    * Direction de la requête : plug-in NuGet->
    * La demande contient :
        * ID et version du package
        * emplacement du référentiel source du package
        * chemin du répertoire de destination
        * énumérable des fichiers dans le package à copier dans le chemin d’accès au répertoire de destination
    * Une réponse contient les éléments suivants :
        * Code de réponse indiquant le résultat de l’opération
        * énumérable de chemins d’accès complets pour les fichiers copiés dans le répertoire de destination si l’opération a réussi

3.  Copier le fichier de package (. nupkg)
    * Direction de la requête : plug-in NuGet->
    * La demande contient :
        * ID et version du package
        * emplacement du référentiel source du package
        * chemin d’accès au fichier de destination
    * Une réponse contient les éléments suivants :
        * Code de réponse indiquant le résultat de l’opération

4.  Récupérer les informations d’identification
    * Direction de la demande : plugin-> NuGet
    * La demande contient :
        * emplacement du référentiel source du package
        * code d’état HTTP obtenu à partir du référentiel source du package à l’aide des informations d’identification actuelles
    * Une réponse contient les éléments suivants :
        * Code de réponse indiquant le résultat de l’opération
        * un nom d’utilisateur, s’il est disponible
        * un mot de passe, s’il est disponible

5.  Récupérer les fichiers dans le package
    * Direction de la requête : plug-in NuGet->
    * La demande contient :
        * ID et version du package
        * emplacement du référentiel source du package
    * Une réponse contient les éléments suivants :
        * Code de réponse indiquant le résultat de l’opération
        * énumérable de chemins d’accès de fichiers dans le package si l’opération a réussi

6.  Récupération des revendications d’opération 
    * Direction de la requête : plug-in NuGet->
    * La demande contient :
        * service index. JSON pour une source de package
        * emplacement du référentiel source du package
    * Une réponse contient les éléments suivants :
        * Code de réponse indiquant le résultat de l’opération
        * énumérable des opérations prises en charge (par exemple, téléchargement de package) si l’opération a réussi.  Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un ensemble vide d’opérations prises en charge.

> [!Note]
> Ce message a été mis à jour dans la version *2.0.0*. Il se trouve sur le client pour préserver la compatibilité descendante.

7.  Obtient le hachage du package
    * Direction de la requête : plug-in NuGet->
    * La demande contient :
        * ID et version du package
        * emplacement du référentiel source du package
        * algorithme de hachage
    * Une réponse contient les éléments suivants :
        * Code de réponse indiquant le résultat de l’opération
        * hachage de fichier de package utilisant l’algorithme de hachage demandé si l’opération a réussi

8.  Obtient les versions du package
    * Direction de la requête : plug-in NuGet->
    * La demande contient :
        * ID du package
        * emplacement du référentiel source du package
    * Une réponse contient les éléments suivants :
        * Code de réponse indiquant le résultat de l’opération
        * énumérable des versions de packages si l’opération a réussi

9.  Obtient l’index de service
    * Direction de la demande : plugin-> NuGet
    * La demande contient :
        * emplacement du référentiel source du package
    * Une réponse contient les éléments suivants :
        * Code de réponse indiquant le résultat de l’opération
        * index du service si l’opération a réussi

10.  Négociation
     * Direction de la demande : < NuGet-plug-in >
     * La demande contient :
         * version actuelle du protocole de plug-in
         * version de protocole du plug-in minimale prise en charge
     * Une réponse contient les éléments suivants :
         * Code de réponse indiquant le résultat de l’opération
         * version du protocole négocié si l’opération a réussi.  Une défaillance entraînera l’arrêt du plug-in.

11.  Initialize
     * Direction de la requête : plug-in NuGet->
     * La demande contient :
         * version de l’outil client NuGet
         * langage de l’outil client NuGet en vigueur.  Cela prend en compte le paramètre ForceEnglishOutput, s’il est utilisé.
         * délai d’expiration de la demande par défaut, qui remplace la valeur par défaut du protocole.
     * Une réponse contient les éléments suivants :
         * Code de réponse indiquant le résultat de l’opération.  Une défaillance entraînera l’arrêt du plug-in.

12.  Log
     * Direction de la demande : plugin-> NuGet
     * La demande contient :
         * niveau de journalisation de la demande
         * message à consigner
     * Une réponse contient les éléments suivants :
         * Code de réponse indiquant le résultat de l’opération.

13.  Surveiller la sortie du processus NuGet
     * Direction de la requête : plug-in NuGet->
     * La demande contient :
         * l’ID de processus NuGet
     * Une réponse contient les éléments suivants :
         * Code de réponse indiquant le résultat de l’opération.

14.  Prérécupérer le package
     * Direction de la requête : plug-in NuGet->
     * La demande contient :
         * ID et version du package
         * emplacement du référentiel source du package
     * Une réponse contient les éléments suivants :
         * Code de réponse indiquant le résultat de l’opération

15.  Définir les informations d’identification
     * Direction de la requête : plug-in NuGet->
     * La demande contient :
         * emplacement du référentiel source du package
         * dernier nom d’utilisateur source de package connu, s’il est disponible
         * dernier mot de passe de source de package connu, s’il est disponible
         * dernier nom d’utilisateur du proxy connu, s’il est disponible
         * dernier mot de passe du proxy connu, s’il est disponible
     * Une réponse contient les éléments suivants :
         * Code de réponse indiquant le résultat de l’opération

16.  Définir le niveau de journal
     * Direction de la requête : plug-in NuGet->
     * La demande contient :
         * niveau de journalisation par défaut
     * Une réponse contient les éléments suivants :
         * Code de réponse indiquant le résultat de l’opération

Messages du protocole version *2.0.0*

17. Récupération des revendications d’opération

* Direction de la requête : plug-in NuGet->
    * La demande contient :
        * service index. JSON pour une source de package
        * emplacement du référentiel source du package
    * Une réponse contient les éléments suivants :
        * Code de réponse indiquant le résultat de l’opération
        * énumérable des opérations prises en charge si l’opération a réussi.  Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un ensemble vide d’opérations prises en charge.

    Si l’index de service et la source de package ont la valeur null, le plug-in peut répondre avec l’authentification.

18. Récupérer les informations d’identification d’authentification

* Direction de la requête : plug-in NuGet->
* La demande contient :
    * URI
    * isRetry
    * Non interactive
    * CanShowDialog
* Une réponse contient
    * Utilisateur
    * Mot de passe
    * Message
    * Liste des types d’authentification
    * MessageResponseCode
