---
title: NuGet entre les plug-ins de la plateforme
description: NuGet cross plug-ins de la plateforme pour NuGet.exe, dotnet.exe, msbuild.exe et Visual Studio
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794178"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet entre les plug-ins de la plateforme

Dans NuGet 4.8 + prise en charge de cross plug-ins de la plateforme a été ajouté.
Cela a été atteint avec en créant un nouveau modèle d’extensibilité de plug-in, qui doit être conforme à un ensemble strict de règles de l’opération.
Les plug-ins sont des exécutables autonomes (runnables dans le monde de .NET Core), les Clients NuGet lancer dans un processus séparé.
Il s’agit d’une écriture true une fois, exécuter partout plug-in. Il fonctionnera avec tous les outils du client NuGet.
Les plug-ins peuvent être le .NET Framework (NuGet.exe, MSBuild.exe et Visual Studio), ou .NET Core (dotnet.exe).
Un protocole de communication avec contrôle de version entre le NuGet Client et le plug-in est défini. Pendant la négociation de démarrage, les 2 processus négocient la version du protocole.

Afin de couvrir tous les scénarios d’outils clients NuGet, vous devez à la fois un .NET Framework et un plug-in .NET Core.
Le ci-dessous décrit les combinaisons de client/framework des plug-ins.

| Outil client  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| NuGet.exe sur Mono | .NET Framework |

## <a name="how-does-it-work"></a>Comment cela fonctionne-t-il

Le flux de travail de haut niveau peut être décrites comme suit :

1. NuGet détecte les plug-ins disponibles.
1. Le cas échéant, NuGet effectue une itération sur les plug-ins dans l’ordre de priorité et démarre un par un.
1. NuGet utilisera le premier plug-in qui peut traiter la requête.
1. Les plug-ins s’arrêteront lorsqu’ils ne sont plus nécessaires.

## <a name="general-plugin-requirements"></a>Configuration requise du plug-in général

La version actuelle de protocole est *2.0.0*.
Dans cette version, les exigences sont les suivantes :

- Avoir un assemblys de signature Authenticode valide et approuvée qui seront exécute sur Windows et Mono. Il n’existe aucune exigence de confiance particulière pour les assemblys exécutés encore sur Linux et Mac. [Problème pertinentes](https://github.com/NuGet/Home/issues/6702)
- Prise en charge sans état de lancement dans le contexte de sécurité actuelle des outils clients NuGet. Par exemple, les outils clients NuGet n’effectue une élévation ou une initialisation supplémentaire en dehors du protocole de plug-in décrit plus loin.
- Être non interactive, sauf spécification explicite.
- Respecter la version du protocole négocié plug-in.
- Répondre à toutes les demandes dans un laps de temps raisonnable.
- Honorer les demandes d’annulation pour toute opération en cours d’exécution.

La spécification technique est décrite plus en détail dans les spécifications suivantes :

- [Plug-in de téléchargement de Package NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet cross plat plug-in d’authentification](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Client - interaction avec le plug-in

Outils clients NuGet et les plug-ins communiquent avec JSON sur des flux standards (stdin, stdout, stderr). Toutes les données doivent être encodé en UTF-8.
Les plug-ins sont lancées avec l’argument «-plug-in ». Dans le cas où un utilisateur lance directement un plug-in exécutable sans cet argument, le plug-in peut donner un message d’information au lieu d’attendre une négociation de protocole.
Le délai d’expiration de la négociation de protocole est de 5 secondes. Le plug-in doit terminer l’installation dans en tant que suffisamment d’un montant que possible.
Outils clients NuGet interrogera les opérations prises en charge du plug-in en passant l’index de service pour une source NuGet. Un plug-in peut utiliser l’index de service pour vérifier la présence des types de service pris en charge.

La communication entre les outils clients NuGet et le plug-in est bidirectionnel. Chaque requête a un délai d’attente de 5 secondes. Si les opérations sont censées prendre plus de temps le processus respectif doit envoyer un message de progression pour empêcher l’expiration du délai de la demande. Après 1 minute d’inactivité un plug-in est considéré comme inactif et est arrêté.

## <a name="plugin-installation-and-discovery"></a>Découverte et l’installation du plug-in

Les plug-ins seront détectés via une structure de répertoires basé sur une convention.
Scénarios d’intégration continue et aux décideurs peuvent utiliser une variable d’environnement pour remplacer le comportement.

- `NUGET_PLUGIN_PATHS` -définit les plug-ins qui seront utilisés pour ce processus de NuGet, priorité réservé. Si cette variable d’environnement est définie, elle remplace la découverte basé sur une convention.
-  Emplacement de l’utilisateur, l’emplacement de l’accueil de NuGet dans `%UserProfile%/.nuget/plugins`. Cet emplacement ne peut pas être remplacé. Un autre répertoire racine sera utilisé pour les plug-ins .NET Core et .NET Framework.

| Framework | Emplacement de détection de racine  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Chaque plug-in doit être installé dans son propre dossier.
Le point d’entrée de plug-in sera le nom du dossier installé, avec les extensions .dll pour .NET Core et l’extension .exe pour .NET Framework.

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
> Il n’existe actuellement aucun récit utilisateur pour l’installation des plug-ins. Il est aussi simple que de déplacer les fichiers requis dans l’emplacement prédéterminé.

## <a name="supported-operations"></a>Opérations prises en charge

Deux opérations sont prises en charge sous le nouveau protocole de plug-in.

| Nom de l’opération | Version de protocole minimale | Version minimale du client NuGet |
| -------------- | ----------------------- | --------------------- |
| Télécharger le Package | 1.0.0 | 4.3.0 |
| [Authentification](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Plug-ins sous le runtime approprié est en cours d’exécution

Pour le package NuGet dans les scénarios de dotnet.exe, plug-ins doivent être en mesure d’exécuter sous ce runtime spécifique de la dotnet.exe.
Il se trouve sur le fournisseur de plug-in et le consommateur pour vous assurer qu'une combinaison compatible dotnet.exe/plugin est utilisée.
Un problème potentiel peut se produire avec les plug-ins de l’emplacement de l’utilisateur lorsque, par exemple, un dotnet.exe sous le runtime 2.0 essaie d’utiliser un plug-in écrit pour le runtime 2.1.

## <a name="capabilities-caching"></a>Fonctionnalités de la mise en cache

La vérification de sécurité et l’instanciation des plug-ins est coûteuse. L’opération de téléchargement a lieu beaucoup plus fréquemment que l’opération d’authentification, cependant, l’utilisateur moyen de NuGet est uniquement susceptible d’avoir un plug-in d’authentification.
Pour améliorer l’expérience, NuGet met en cache les revendications de l’opération pour la demande donnée. Ce cache est par le plug-in avec la clé de plug-in qui est le chemin d’accès du plug-in, et l’expiration pour ce cache de fonctionnalités est de 30 jours. 

Le cache se trouve dans `%LocalAppData%/NuGet/plugins-cache` et être remplacé par la variable d’environnement `NUGET_PLUGINS_CACHE_PATH`. Pour effacer cette [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), les variables locales exécutable avec la `plugins-cache` option.
Le `all` variables locales option maintenant également supprime le cache de plug-ins. 

## <a name="protocol-messages-index"></a>Index des messages de protocole

Version du protocole *1.0.0* messages :

1.  Fermer
    * Demande de direction : NuGet -> plug-in
    * La demande ne contiendra aucune charge utile
    * Aucune réponse n’est attendue.  La réponse correcte est le processus de plug-in s’arrête rapidement.

2.  Copier les fichiers de package
    * Demande de direction : NuGet -> plug-in
    * La requête contient :
        * l’ID de package et de la version
        * emplacement de dépôt source du package
        * chemin d’accès du répertoire de destination
        * une collection énumérable de fichiers dans le package à copier vers le chemin d’accès du répertoire de destination
    * Une réponse contiendra :
        * un code de réponse indiquant le résultat de l’opération
        * une collection énumérable de chemins d’accès complets des fichiers copiés dans le répertoire de destination si l’opération a réussi

3.  Copiez le fichier de package (fichier .nupkg)
    * Demande de direction : NuGet -> plug-in
    * La requête contient :
        * l’ID de package et de la version
        * emplacement de dépôt source du package
        * le chemin d’accès du fichier de destination
    * Une réponse contiendra :
        * un code de réponse indiquant le résultat de l’opération

4.  Obtenir des informations d’identification
    * Demande de direction : plug-in -> NuGet
    * La requête contient :
        * emplacement de dépôt source du package
        * le code d’état HTTP obtenu à partir du référentiel de source de package à l’aide des informations d’identification actuelles
    * Une réponse contiendra :
        * un code de réponse indiquant le résultat de l’opération
        * un nom d’utilisateur, s’il est disponible
        * un mot de passe, s’il est disponible

5.  Obtenir les fichiers dans le package
    * Demande de direction : NuGet -> plug-in
    * La requête contient :
        * l’ID de package et de la version
        * emplacement de dépôt source du package
    * Une réponse contiendra :
        * un code de réponse indiquant le résultat de l’opération
        * une collection énumérable de chemins d’accès de fichier dans le package si l’opération a réussi

6.  Obtenir les revendications de l’opération 
    * Demande de direction : NuGet -> plug-in
    * La requête contient :
        * le service index.json pour une source de package
        * emplacement de dépôt source du package
    * Une réponse contiendra :
        * un code de réponse indiquant le résultat de l’opération
        * énumérable des opérations prises en charge (par exemple : téléchargement du package) si l’opération a réussi.  Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un jeu d’opérations prises en charge vide.

> [!Note]
> Ce message a été mis à jour dans la version *2.0.0*. Il se trouve sur le client pour préserver la compatibilité descendante.

7.  Obtenir le hachage du package
    * Demande de direction : NuGet -> plug-in
    * La requête contient :
        * l’ID de package et de la version
        * emplacement de dépôt source du package
        * l’algorithme de hachage
    * Une réponse contiendra :
        * un code de réponse indiquant le résultat de l’opération
        * un hachage de fichier de package à l’aide de l’algorithme de hachage demandé si l’opération a réussi

8.  Obtenir les versions de package
    * Demande de direction : NuGet -> plug-in
    * La requête contient :
        * l’ID de package
        * emplacement de dépôt source du package
    * Une réponse contiendra :
        * un code de réponse indiquant le résultat de l’opération
        * une collection énumérable de versions de package si l’opération a réussi

9.  Obtenir l’index de service
    * Demande de direction : plug-in -> NuGet
    * La requête contient :
        * emplacement de dépôt source du package
    * Une réponse contiendra :
        * un code de réponse indiquant le résultat de l’opération
        * l’index de service si l’opération a réussi

10.  Protocole de transfert
     * Demande de direction : plug-in NuGet <> –
     * La requête contient :
         * la version actuelle du protocole de plug-in
         * la valeur minimale prise en charge la version de protocole de plug-in
     * Une réponse contiendra :
         * un code de réponse indiquant le résultat de l’opération
         * la version de protocole négocié si l’opération a réussi.  Un échec entraînera l’arrêt du plug-in.

11.  initialiser
     * Demande de direction : NuGet -> plug-in
     * La requête contient :
         * l’outil de version de NuGet client
         * le langage NuGet client outil efficace.  Cela tient compte du paramètre ForceEnglishOutput, si utilisé.
         * le délai de requête par défaut, qui remplace la valeur par défaut du protocole.
     * Une réponse contiendra :
         * un code de réponse indiquant le résultat de l’opération.  Un échec entraînera l’arrêt du plug-in.

12.  Log
     * Demande de direction : plug-in -> NuGet
     * La requête contient :
         * le niveau de journalisation pour la demande
         * un message à enregistrer
     * Une réponse contiendra :
         * un code de réponse indiquant le résultat de l’opération.

13.  Surveiller la sortie du processus de NuGet
     * Demande de direction : NuGet -> plug-in
     * La requête contient :
         * l’ID de processus de NuGet
     * Une réponse contiendra :
         * un code de réponse indiquant le résultat de l’opération.

14.  Package de prérécupération
     * Demande de direction : NuGet -> plug-in
     * La requête contient :
         * l’ID de package et de la version
         * emplacement de dépôt source du package
     * Une réponse contiendra :
         * un code de réponse indiquant le résultat de l’opération

15.  Informations d’identification de l’ensemble
     * Demande de direction : NuGet -> plug-in
     * La requête contient :
         * emplacement de dépôt source du package
         * le dernier package connus source nom d’utilisateur, s’il est disponible
         * le dernier package connus source mot de passe, s’il est disponible
         * le dernier proxy connus nom d’utilisateur, s’il est disponible
         * le dernier proxy connus mot de passe, s’il est disponible
     * Une réponse contiendra :
         * un code de réponse indiquant le résultat de l’opération

16.  Définir le niveau de journal
     * Demande de direction : NuGet -> plug-in
     * La requête contient :
         * le niveau de journalisation par défaut
     * Une réponse contiendra :
         * un code de réponse indiquant le résultat de l’opération

Version du protocole *2.0.0* messages

17. Obtenir les revendications de l’opération

* Demande de direction : NuGet -> plug-in
    * La requête contient :
        * le service index.json pour une source de package
        * emplacement de dépôt source du package
    * Une réponse contiendra :
        * un code de réponse indiquant le résultat de l’opération
        * énumérable des opérations prises en charge si l’opération a réussi.  Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un jeu d’opérations prises en charge vide.

    Si la source de package et les index de service est null, le plug-in peut répondre avec l’authentification.

18. Obtenir des informations d’identification d’authentification

* Demande de direction : NuGet -> plug-in
* La requête contient :
    * URI
    * isRetry
    * NonInteractive
    * CanShowDialog
* Contient une réponse
    * Utilisateur
    * Mot de passe
    * Message
    * Liste des Types d’authentification
    * MessageResponseCode