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
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="1c388-103">NuGet entre les plug-ins de la plateforme</span><span class="sxs-lookup"><span data-stu-id="1c388-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="1c388-104">Dans NuGet 4.8 + prise en charge de cross plug-ins de la plateforme a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="1c388-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="1c388-105">Cela a été atteint avec en créant un nouveau modèle d’extensibilité de plug-in, qui doit être conforme à un ensemble strict de règles de l’opération.</span><span class="sxs-lookup"><span data-stu-id="1c388-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="1c388-106">Les plug-ins sont des exécutables autonomes (runnables dans le monde de .NET Core), les Clients NuGet lancer dans un processus séparé.</span><span class="sxs-lookup"><span data-stu-id="1c388-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="1c388-107">Il s’agit d’une écriture true une fois, exécuter partout plug-in.</span><span class="sxs-lookup"><span data-stu-id="1c388-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="1c388-108">Il fonctionnera avec tous les outils du client NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c388-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="1c388-109">Les plug-ins peuvent être le .NET Framework (NuGet.exe, MSBuild.exe et Visual Studio), ou .NET Core (dotnet.exe).</span><span class="sxs-lookup"><span data-stu-id="1c388-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="1c388-110">Un protocole de communication avec contrôle de version entre le NuGet Client et le plug-in est défini.</span><span class="sxs-lookup"><span data-stu-id="1c388-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="1c388-111">Pendant la négociation de démarrage, les 2 processus négocient la version du protocole.</span><span class="sxs-lookup"><span data-stu-id="1c388-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="1c388-112">Afin de couvrir tous les scénarios d’outils clients NuGet, vous devez à la fois un .NET Framework et un plug-in .NET Core.</span><span class="sxs-lookup"><span data-stu-id="1c388-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="1c388-113">Le ci-dessous décrit les combinaisons de client/framework des plug-ins.</span><span class="sxs-lookup"><span data-stu-id="1c388-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="1c388-114">Outil client</span><span class="sxs-lookup"><span data-stu-id="1c388-114">Client tool</span></span>  | <span data-ttu-id="1c388-115">Framework</span><span class="sxs-lookup"><span data-stu-id="1c388-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="1c388-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1c388-116">Visual Studio</span></span> | <span data-ttu-id="1c388-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1c388-117">.NET Framework</span></span> |
| <span data-ttu-id="1c388-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="1c388-118">dotnet.exe</span></span> | <span data-ttu-id="1c388-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1c388-119">.NET Core</span></span> |
| <span data-ttu-id="1c388-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="1c388-120">NuGet.exe</span></span> | <span data-ttu-id="1c388-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1c388-121">.NET Framework</span></span> |
| <span data-ttu-id="1c388-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="1c388-122">MSBuild.exe</span></span> | <span data-ttu-id="1c388-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1c388-123">.NET Framework</span></span> |
| <span data-ttu-id="1c388-124">NuGet.exe sur Mono</span><span class="sxs-lookup"><span data-stu-id="1c388-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="1c388-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1c388-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="1c388-126">Comment cela fonctionne-t-il</span><span class="sxs-lookup"><span data-stu-id="1c388-126">How does it work</span></span>

<span data-ttu-id="1c388-127">Le flux de travail de haut niveau peut être décrites comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c388-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="1c388-128">NuGet détecte les plug-ins disponibles.</span><span class="sxs-lookup"><span data-stu-id="1c388-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="1c388-129">Le cas échéant, NuGet effectue une itération sur les plug-ins dans l’ordre de priorité et démarre un par un.</span><span class="sxs-lookup"><span data-stu-id="1c388-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="1c388-130">NuGet utilisera le premier plug-in qui peut traiter la requête.</span><span class="sxs-lookup"><span data-stu-id="1c388-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="1c388-131">Les plug-ins s’arrêteront lorsqu’ils ne sont plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="1c388-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="1c388-132">Configuration requise du plug-in général</span><span class="sxs-lookup"><span data-stu-id="1c388-132">General plugin requirements</span></span>

<span data-ttu-id="1c388-133">La version actuelle de protocole est *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="1c388-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="1c388-134">Dans cette version, les exigences sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c388-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="1c388-135">Avoir un assemblys de signature Authenticode valide et approuvée qui seront exécute sur Windows et Mono.</span><span class="sxs-lookup"><span data-stu-id="1c388-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="1c388-136">Il n’existe aucune exigence de confiance particulière pour les assemblys exécutés encore sur Linux et Mac.</span><span class="sxs-lookup"><span data-stu-id="1c388-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="1c388-137">Problème pertinentes</span><span class="sxs-lookup"><span data-stu-id="1c388-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="1c388-138">Prise en charge sans état de lancement dans le contexte de sécurité actuelle des outils clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c388-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="1c388-139">Par exemple, les outils clients NuGet n’effectue une élévation ou une initialisation supplémentaire en dehors du protocole de plug-in décrit plus loin.</span><span class="sxs-lookup"><span data-stu-id="1c388-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="1c388-140">Être non interactive, sauf spécification explicite.</span><span class="sxs-lookup"><span data-stu-id="1c388-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="1c388-141">Respecter la version du protocole négocié plug-in.</span><span class="sxs-lookup"><span data-stu-id="1c388-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="1c388-142">Répondre à toutes les demandes dans un laps de temps raisonnable.</span><span class="sxs-lookup"><span data-stu-id="1c388-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="1c388-143">Honorer les demandes d’annulation pour toute opération en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1c388-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="1c388-144">La spécification technique est décrite plus en détail dans les spécifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c388-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="1c388-145">Plug-in de téléchargement de Package NuGet</span><span class="sxs-lookup"><span data-stu-id="1c388-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="1c388-146">NuGet cross plat plug-in d’authentification</span><span class="sxs-lookup"><span data-stu-id="1c388-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="1c388-147">Client - interaction avec le plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-147">Client - Plugin interaction</span></span>

<span data-ttu-id="1c388-148">Outils clients NuGet et les plug-ins communiquent avec JSON sur des flux standards (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="1c388-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="1c388-149">Toutes les données doivent être encodé en UTF-8.</span><span class="sxs-lookup"><span data-stu-id="1c388-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="1c388-150">Les plug-ins sont lancées avec l’argument «-plug-in ».</span><span class="sxs-lookup"><span data-stu-id="1c388-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="1c388-151">Dans le cas où un utilisateur lance directement un plug-in exécutable sans cet argument, le plug-in peut donner un message d’information au lieu d’attendre une négociation de protocole.</span><span class="sxs-lookup"><span data-stu-id="1c388-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="1c388-152">Le délai d’expiration de la négociation de protocole est de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="1c388-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="1c388-153">Le plug-in doit terminer l’installation dans en tant que suffisamment d’un montant que possible.</span><span class="sxs-lookup"><span data-stu-id="1c388-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="1c388-154">Outils clients NuGet interrogera les opérations prises en charge du plug-in en passant l’index de service pour une source NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c388-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="1c388-155">Un plug-in peut utiliser l’index de service pour vérifier la présence des types de service pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1c388-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="1c388-156">La communication entre les outils clients NuGet et le plug-in est bidirectionnel.</span><span class="sxs-lookup"><span data-stu-id="1c388-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="1c388-157">Chaque requête a un délai d’attente de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="1c388-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="1c388-158">Si les opérations sont censées prendre plus de temps le processus respectif doit envoyer un message de progression pour empêcher l’expiration du délai de la demande. Après 1 minute d’inactivité un plug-in est considéré comme inactif et est arrêté.</span><span class="sxs-lookup"><span data-stu-id="1c388-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="1c388-159">Découverte et l’installation du plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-159">Plugin installation and discovery</span></span>

<span data-ttu-id="1c388-160">Les plug-ins seront détectés via une structure de répertoires basé sur une convention.</span><span class="sxs-lookup"><span data-stu-id="1c388-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="1c388-161">Scénarios d’intégration continue et aux décideurs peuvent utiliser une variable d’environnement pour remplacer le comportement.</span><span class="sxs-lookup"><span data-stu-id="1c388-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="1c388-162">`NUGET_PLUGIN_PATHS` -définit les plug-ins qui seront utilisés pour ce processus de NuGet, priorité réservé.</span><span class="sxs-lookup"><span data-stu-id="1c388-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="1c388-163">Si cette variable d’environnement est définie, elle remplace la découverte basé sur une convention.</span><span class="sxs-lookup"><span data-stu-id="1c388-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="1c388-164">Emplacement de l’utilisateur, l’emplacement de l’accueil de NuGet dans `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="1c388-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="1c388-165">Cet emplacement ne peut pas être remplacé.</span><span class="sxs-lookup"><span data-stu-id="1c388-165">This location cannot be overriden.</span></span> <span data-ttu-id="1c388-166">Un autre répertoire racine sera utilisé pour les plug-ins .NET Core et .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1c388-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="1c388-167">Framework</span><span class="sxs-lookup"><span data-stu-id="1c388-167">Framework</span></span> | <span data-ttu-id="1c388-168">Emplacement de détection de racine</span><span class="sxs-lookup"><span data-stu-id="1c388-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="1c388-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1c388-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="1c388-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1c388-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="1c388-171">Chaque plug-in doit être installé dans son propre dossier.</span><span class="sxs-lookup"><span data-stu-id="1c388-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="1c388-172">Le point d’entrée de plug-in sera le nom du dossier installé, avec les extensions .dll pour .NET Core et l’extension .exe pour .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1c388-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="1c388-173">Il n’existe actuellement aucun récit utilisateur pour l’installation des plug-ins.</span><span class="sxs-lookup"><span data-stu-id="1c388-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="1c388-174">Il est aussi simple que de déplacer les fichiers requis dans l’emplacement prédéterminé.</span><span class="sxs-lookup"><span data-stu-id="1c388-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="1c388-175">Opérations prises en charge</span><span class="sxs-lookup"><span data-stu-id="1c388-175">Supported operations</span></span>

<span data-ttu-id="1c388-176">Deux opérations sont prises en charge sous le nouveau protocole de plug-in.</span><span class="sxs-lookup"><span data-stu-id="1c388-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="1c388-177">Nom de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-177">Operation name</span></span> | <span data-ttu-id="1c388-178">Version de protocole minimale</span><span class="sxs-lookup"><span data-stu-id="1c388-178">Minimum protocol version</span></span> | <span data-ttu-id="1c388-179">Version minimale du client NuGet</span><span class="sxs-lookup"><span data-stu-id="1c388-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="1c388-180">Télécharger le Package</span><span class="sxs-lookup"><span data-stu-id="1c388-180">Download Package</span></span> | <span data-ttu-id="1c388-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1c388-181">1.0.0</span></span> | <span data-ttu-id="1c388-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="1c388-182">4.3.0</span></span> |
| [<span data-ttu-id="1c388-183">Authentification</span><span class="sxs-lookup"><span data-stu-id="1c388-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="1c388-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="1c388-184">2.0.0</span></span> | <span data-ttu-id="1c388-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="1c388-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="1c388-186">Plug-ins sous le runtime approprié est en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="1c388-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="1c388-187">Pour le package NuGet dans les scénarios de dotnet.exe, plug-ins doivent être en mesure d’exécuter sous ce runtime spécifique de la dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="1c388-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="1c388-188">Il se trouve sur le fournisseur de plug-in et le consommateur pour vous assurer qu'une combinaison compatible dotnet.exe/plugin est utilisée.</span><span class="sxs-lookup"><span data-stu-id="1c388-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="1c388-189">Un problème potentiel peut se produire avec les plug-ins de l’emplacement de l’utilisateur lorsque, par exemple, un dotnet.exe sous le runtime 2.0 essaie d’utiliser un plug-in écrit pour le runtime 2.1.</span><span class="sxs-lookup"><span data-stu-id="1c388-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="1c388-190">Fonctionnalités de la mise en cache</span><span class="sxs-lookup"><span data-stu-id="1c388-190">Capabilities caching</span></span>

<span data-ttu-id="1c388-191">La vérification de sécurité et l’instanciation des plug-ins est coûteuse.</span><span class="sxs-lookup"><span data-stu-id="1c388-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="1c388-192">L’opération de téléchargement a lieu beaucoup plus fréquemment que l’opération d’authentification, cependant, l’utilisateur moyen de NuGet est uniquement susceptible d’avoir un plug-in d’authentification.</span><span class="sxs-lookup"><span data-stu-id="1c388-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="1c388-193">Pour améliorer l’expérience, NuGet met en cache les revendications de l’opération pour la demande donnée.</span><span class="sxs-lookup"><span data-stu-id="1c388-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="1c388-194">Ce cache est par le plug-in avec la clé de plug-in qui est le chemin d’accès du plug-in, et l’expiration pour ce cache de fonctionnalités est de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="1c388-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="1c388-195">Le cache se trouve dans `%LocalAppData%/NuGet/plugins-cache` et être remplacé par la variable d’environnement `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="1c388-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="1c388-196">Pour effacer cette [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), les variables locales exécutable avec la `plugins-cache` option.</span><span class="sxs-lookup"><span data-stu-id="1c388-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="1c388-197">Le `all` variables locales option maintenant également supprime le cache de plug-ins.</span><span class="sxs-lookup"><span data-stu-id="1c388-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="1c388-198">Index des messages de protocole</span><span class="sxs-lookup"><span data-stu-id="1c388-198">Protocol messages index</span></span>

<span data-ttu-id="1c388-199">Version du protocole *1.0.0* messages :</span><span class="sxs-lookup"><span data-stu-id="1c388-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="1c388-200">Fermer</span><span class="sxs-lookup"><span data-stu-id="1c388-200">Close</span></span>
    * <span data-ttu-id="1c388-201">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1c388-202">La demande ne contiendra aucune charge utile</span><span class="sxs-lookup"><span data-stu-id="1c388-202">The request will contain no payload</span></span>
    * <span data-ttu-id="1c388-203">Aucune réponse n’est attendue.</span><span class="sxs-lookup"><span data-stu-id="1c388-203">No response is expected.</span></span>  <span data-ttu-id="1c388-204">La réponse correcte est le processus de plug-in s’arrête rapidement.</span><span class="sxs-lookup"><span data-stu-id="1c388-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="1c388-205">Copier les fichiers de package</span><span class="sxs-lookup"><span data-stu-id="1c388-205">Copy files in package</span></span>
    * <span data-ttu-id="1c388-206">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1c388-207">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-207">The request will contain:</span></span>
        * <span data-ttu-id="1c388-208">l’ID de package et de la version</span><span class="sxs-lookup"><span data-stu-id="1c388-208">the package ID and version</span></span>
        * <span data-ttu-id="1c388-209">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-209">the package source repository location</span></span>
        * <span data-ttu-id="1c388-210">chemin d’accès du répertoire de destination</span><span class="sxs-lookup"><span data-stu-id="1c388-210">destination directory path</span></span>
        * <span data-ttu-id="1c388-211">une collection énumérable de fichiers dans le package à copier vers le chemin d’accès du répertoire de destination</span><span class="sxs-lookup"><span data-stu-id="1c388-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="1c388-212">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-212">A response will contain:</span></span>
        * <span data-ttu-id="1c388-213">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1c388-214">une collection énumérable de chemins d’accès complets des fichiers copiés dans le répertoire de destination si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="1c388-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="1c388-215">Copiez le fichier de package (fichier .nupkg)</span><span class="sxs-lookup"><span data-stu-id="1c388-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="1c388-216">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1c388-217">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-217">The request will contain:</span></span>
        * <span data-ttu-id="1c388-218">l’ID de package et de la version</span><span class="sxs-lookup"><span data-stu-id="1c388-218">the package ID and version</span></span>
        * <span data-ttu-id="1c388-219">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-219">the package source repository location</span></span>
        * <span data-ttu-id="1c388-220">le chemin d’accès du fichier de destination</span><span class="sxs-lookup"><span data-stu-id="1c388-220">the destination file path</span></span>
    * <span data-ttu-id="1c388-221">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-221">A response will contain:</span></span>
        * <span data-ttu-id="1c388-222">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="1c388-223">Obtenir des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="1c388-223">Get credentials</span></span>
    * <span data-ttu-id="1c388-224">Demande de direction : plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="1c388-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="1c388-225">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-225">The request will contain:</span></span>
        * <span data-ttu-id="1c388-226">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-226">the package source repository location</span></span>
        * <span data-ttu-id="1c388-227">le code d’état HTTP obtenu à partir du référentiel de source de package à l’aide des informations d’identification actuelles</span><span class="sxs-lookup"><span data-stu-id="1c388-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="1c388-228">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-228">A response will contain:</span></span>
        * <span data-ttu-id="1c388-229">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1c388-230">un nom d’utilisateur, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="1c388-230">a username, if available</span></span>
        * <span data-ttu-id="1c388-231">un mot de passe, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="1c388-231">a password, if available</span></span>

5.  <span data-ttu-id="1c388-232">Obtenir les fichiers dans le package</span><span class="sxs-lookup"><span data-stu-id="1c388-232">Get files in package</span></span>
    * <span data-ttu-id="1c388-233">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1c388-234">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-234">The request will contain:</span></span>
        * <span data-ttu-id="1c388-235">l’ID de package et de la version</span><span class="sxs-lookup"><span data-stu-id="1c388-235">the package ID and version</span></span>
        * <span data-ttu-id="1c388-236">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-236">the package source repository location</span></span>
    * <span data-ttu-id="1c388-237">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-237">A response will contain:</span></span>
        * <span data-ttu-id="1c388-238">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1c388-239">une collection énumérable de chemins d’accès de fichier dans le package si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="1c388-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="1c388-240">Obtenir les revendications de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-240">Get operation claims</span></span> 
    * <span data-ttu-id="1c388-241">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1c388-242">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-242">The request will contain:</span></span>
        * <span data-ttu-id="1c388-243">le service index.json pour une source de package</span><span class="sxs-lookup"><span data-stu-id="1c388-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="1c388-244">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-244">the package source repository location</span></span>
    * <span data-ttu-id="1c388-245">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-245">A response will contain:</span></span>
        * <span data-ttu-id="1c388-246">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1c388-247">énumérable des opérations prises en charge (par exemple : téléchargement du package) si l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="1c388-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="1c388-248">Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un jeu d’opérations prises en charge vide.</span><span class="sxs-lookup"><span data-stu-id="1c388-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="1c388-249">Ce message a été mis à jour dans la version *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="1c388-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="1c388-250">Il se trouve sur le client pour préserver la compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="1c388-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="1c388-251">Obtenir le hachage du package</span><span class="sxs-lookup"><span data-stu-id="1c388-251">Get package hash</span></span>
    * <span data-ttu-id="1c388-252">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1c388-253">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-253">The request will contain:</span></span>
        * <span data-ttu-id="1c388-254">l’ID de package et de la version</span><span class="sxs-lookup"><span data-stu-id="1c388-254">the package ID and version</span></span>
        * <span data-ttu-id="1c388-255">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-255">the package source repository location</span></span>
        * <span data-ttu-id="1c388-256">l’algorithme de hachage</span><span class="sxs-lookup"><span data-stu-id="1c388-256">the hash algorithm</span></span>
    * <span data-ttu-id="1c388-257">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-257">A response will contain:</span></span>
        * <span data-ttu-id="1c388-258">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1c388-259">un hachage de fichier de package à l’aide de l’algorithme de hachage demandé si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="1c388-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="1c388-260">Obtenir les versions de package</span><span class="sxs-lookup"><span data-stu-id="1c388-260">Get package versions</span></span>
    * <span data-ttu-id="1c388-261">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1c388-262">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-262">The request will contain:</span></span>
        * <span data-ttu-id="1c388-263">l’ID de package</span><span class="sxs-lookup"><span data-stu-id="1c388-263">the package ID</span></span>
        * <span data-ttu-id="1c388-264">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-264">the package source repository location</span></span>
    * <span data-ttu-id="1c388-265">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-265">A response will contain:</span></span>
        * <span data-ttu-id="1c388-266">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1c388-267">une collection énumérable de versions de package si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="1c388-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="1c388-268">Obtenir l’index de service</span><span class="sxs-lookup"><span data-stu-id="1c388-268">Get service index</span></span>
    * <span data-ttu-id="1c388-269">Demande de direction : plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="1c388-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="1c388-270">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-270">The request will contain:</span></span>
        * <span data-ttu-id="1c388-271">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-271">the package source repository location</span></span>
    * <span data-ttu-id="1c388-272">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-272">A response will contain:</span></span>
        * <span data-ttu-id="1c388-273">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1c388-274">l’index de service si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="1c388-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="1c388-275">Protocole de transfert</span><span class="sxs-lookup"><span data-stu-id="1c388-275">Handshake</span></span>
     * <span data-ttu-id="1c388-276">Demande de direction : plug-in NuGet <> –</span><span class="sxs-lookup"><span data-stu-id="1c388-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="1c388-277">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-277">The request will contain:</span></span>
         * <span data-ttu-id="1c388-278">la version actuelle du protocole de plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="1c388-279">la valeur minimale prise en charge la version de protocole de plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="1c388-280">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-280">A response will contain:</span></span>
         * <span data-ttu-id="1c388-281">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="1c388-282">la version de protocole négocié si l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="1c388-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="1c388-283">Un échec entraînera l’arrêt du plug-in.</span><span class="sxs-lookup"><span data-stu-id="1c388-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="1c388-284">initialiser</span><span class="sxs-lookup"><span data-stu-id="1c388-284">Initialize</span></span>
     * <span data-ttu-id="1c388-285">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1c388-286">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-286">The request will contain:</span></span>
         * <span data-ttu-id="1c388-287">l’outil de version de NuGet client</span><span class="sxs-lookup"><span data-stu-id="1c388-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="1c388-288">le langage NuGet client outil efficace.</span><span class="sxs-lookup"><span data-stu-id="1c388-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="1c388-289">Cela tient compte du paramètre ForceEnglishOutput, si utilisé.</span><span class="sxs-lookup"><span data-stu-id="1c388-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="1c388-290">le délai de requête par défaut, qui remplace la valeur par défaut du protocole.</span><span class="sxs-lookup"><span data-stu-id="1c388-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="1c388-291">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-291">A response will contain:</span></span>
         * <span data-ttu-id="1c388-292">un code de réponse indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="1c388-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="1c388-293">Un échec entraînera l’arrêt du plug-in.</span><span class="sxs-lookup"><span data-stu-id="1c388-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="1c388-294">Log</span><span class="sxs-lookup"><span data-stu-id="1c388-294">Log</span></span>
     * <span data-ttu-id="1c388-295">Demande de direction : plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="1c388-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="1c388-296">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-296">The request will contain:</span></span>
         * <span data-ttu-id="1c388-297">le niveau de journalisation pour la demande</span><span class="sxs-lookup"><span data-stu-id="1c388-297">the log level for the request</span></span>
         * <span data-ttu-id="1c388-298">un message à enregistrer</span><span class="sxs-lookup"><span data-stu-id="1c388-298">a message to log</span></span>
     * <span data-ttu-id="1c388-299">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-299">A response will contain:</span></span>
         * <span data-ttu-id="1c388-300">un code de réponse indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="1c388-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="1c388-301">Surveiller la sortie du processus de NuGet</span><span class="sxs-lookup"><span data-stu-id="1c388-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="1c388-302">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1c388-303">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-303">The request will contain:</span></span>
         * <span data-ttu-id="1c388-304">l’ID de processus de NuGet</span><span class="sxs-lookup"><span data-stu-id="1c388-304">the NuGet process ID</span></span>
     * <span data-ttu-id="1c388-305">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-305">A response will contain:</span></span>
         * <span data-ttu-id="1c388-306">un code de réponse indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="1c388-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="1c388-307">Package de prérécupération</span><span class="sxs-lookup"><span data-stu-id="1c388-307">Prefetch package</span></span>
     * <span data-ttu-id="1c388-308">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1c388-309">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-309">The request will contain:</span></span>
         * <span data-ttu-id="1c388-310">l’ID de package et de la version</span><span class="sxs-lookup"><span data-stu-id="1c388-310">the package ID and version</span></span>
         * <span data-ttu-id="1c388-311">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-311">the package source repository location</span></span>
     * <span data-ttu-id="1c388-312">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-312">A response will contain:</span></span>
         * <span data-ttu-id="1c388-313">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="1c388-314">Informations d’identification de l’ensemble</span><span class="sxs-lookup"><span data-stu-id="1c388-314">Set credentials</span></span>
     * <span data-ttu-id="1c388-315">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1c388-316">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-316">The request will contain:</span></span>
         * <span data-ttu-id="1c388-317">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-317">the package source repository location</span></span>
         * <span data-ttu-id="1c388-318">le dernier package connus source nom d’utilisateur, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="1c388-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="1c388-319">le dernier package connus source mot de passe, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="1c388-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="1c388-320">le dernier proxy connus nom d’utilisateur, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="1c388-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="1c388-321">le dernier proxy connus mot de passe, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="1c388-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="1c388-322">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-322">A response will contain:</span></span>
         * <span data-ttu-id="1c388-323">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="1c388-324">Définir le niveau de journal</span><span class="sxs-lookup"><span data-stu-id="1c388-324">Set log level</span></span>
     * <span data-ttu-id="1c388-325">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1c388-326">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-326">The request will contain:</span></span>
         * <span data-ttu-id="1c388-327">le niveau de journalisation par défaut</span><span class="sxs-lookup"><span data-stu-id="1c388-327">the default log level</span></span>
     * <span data-ttu-id="1c388-328">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-328">A response will contain:</span></span>
         * <span data-ttu-id="1c388-329">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="1c388-330">Version du protocole *2.0.0* messages</span><span class="sxs-lookup"><span data-stu-id="1c388-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="1c388-331">Obtenir les revendications de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-331">Get Operation Claims</span></span>

* <span data-ttu-id="1c388-332">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1c388-333">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-333">The request will contain:</span></span>
        * <span data-ttu-id="1c388-334">le service index.json pour une source de package</span><span class="sxs-lookup"><span data-stu-id="1c388-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="1c388-335">emplacement de dépôt source du package</span><span class="sxs-lookup"><span data-stu-id="1c388-335">the package source repository location</span></span>
    * <span data-ttu-id="1c388-336">Une réponse contiendra :</span><span class="sxs-lookup"><span data-stu-id="1c388-336">A response will contain:</span></span>
        * <span data-ttu-id="1c388-337">un code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="1c388-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1c388-338">énumérable des opérations prises en charge si l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="1c388-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="1c388-339">Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un jeu d’opérations prises en charge vide.</span><span class="sxs-lookup"><span data-stu-id="1c388-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="1c388-340">Si la source de package et les index de service est null, le plug-in peut répondre avec l’authentification.</span><span class="sxs-lookup"><span data-stu-id="1c388-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="1c388-341">Obtenir des informations d’identification d’authentification</span><span class="sxs-lookup"><span data-stu-id="1c388-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="1c388-342">Demande de direction : NuGet -> plug-in</span><span class="sxs-lookup"><span data-stu-id="1c388-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="1c388-343">La requête contient :</span><span class="sxs-lookup"><span data-stu-id="1c388-343">The request will contain:</span></span>
    * <span data-ttu-id="1c388-344">URI</span><span class="sxs-lookup"><span data-stu-id="1c388-344">Uri</span></span>
    * <span data-ttu-id="1c388-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="1c388-345">isRetry</span></span>
    * <span data-ttu-id="1c388-346">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1c388-346">NonInteractive</span></span>
    * <span data-ttu-id="1c388-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="1c388-347">CanShowDialog</span></span>
* <span data-ttu-id="1c388-348">Contient une réponse</span><span class="sxs-lookup"><span data-stu-id="1c388-348">A response will contain</span></span>
    * <span data-ttu-id="1c388-349">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="1c388-349">Username</span></span>
    * <span data-ttu-id="1c388-350">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="1c388-350">Password</span></span>
    * <span data-ttu-id="1c388-351">Message</span><span class="sxs-lookup"><span data-stu-id="1c388-351">Message</span></span>
    * <span data-ttu-id="1c388-352">Liste des Types d’authentification</span><span class="sxs-lookup"><span data-stu-id="1c388-352">List of Auth Types</span></span>
    * <span data-ttu-id="1c388-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="1c388-353">MessageResponseCode</span></span>