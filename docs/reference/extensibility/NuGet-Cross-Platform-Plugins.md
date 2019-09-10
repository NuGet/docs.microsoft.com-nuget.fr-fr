---
title: Plug-ins inter-plateforme NuGet
description: Plug-ins inter-plateforme NuGet pour NuGet. exe, dotnet. exe, MSBuild. exe et Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815308"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="2ab1d-103">Plug-ins inter-plateforme NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="2ab1d-104">Dans NuGet 4.8 +, la prise en charge des plug-ins multiplateforme a été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="2ab1d-105">Pour cela, vous devez créer un nouveau modèle d’extensibilité de plug-in, qui doit se conformer à un ensemble strict de règles d’opération.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="2ab1d-106">Les plug-ins sont des exécutables autonomes (Runnables dans le monde de .NET Core), que les clients NuGet lancent dans un processus distinct.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="2ab1d-107">Il s’agit d’un plug-in réel en écriture unique, Run Everywhere.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="2ab1d-108">Il fonctionne avec tous les outils clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="2ab1d-109">Les plug-ins peuvent être .NET Framework (NuGet. exe, MSBuild. exe et Visual Studio) ou .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="2ab1d-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="2ab1d-110">Un protocole de communication avec version entre le client NuGet et le plug-in est défini.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="2ab1d-111">Au cours de l’établissement de liaison de démarrage, les 2 processus négocient la version du protocole.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="2ab1d-112">Pour couvrir tous les scénarios d’outils clients NuGet, vous devez disposer d’un .NET Framework et d’un plug-in .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="2ab1d-113">La description ci-dessous décrit les combinaisons client/Framework des plug-ins.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="2ab1d-114">Outil client</span><span class="sxs-lookup"><span data-stu-id="2ab1d-114">Client tool</span></span>  | <span data-ttu-id="2ab1d-115">Framework</span><span class="sxs-lookup"><span data-stu-id="2ab1d-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="2ab1d-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ab1d-116">Visual Studio</span></span> | <span data-ttu-id="2ab1d-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="2ab1d-117">.NET Framework</span></span> |
| <span data-ttu-id="2ab1d-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="2ab1d-118">dotnet.exe</span></span> | <span data-ttu-id="2ab1d-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2ab1d-119">.NET Core</span></span> |
| <span data-ttu-id="2ab1d-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="2ab1d-120">NuGet.exe</span></span> | <span data-ttu-id="2ab1d-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="2ab1d-121">.NET Framework</span></span> |
| <span data-ttu-id="2ab1d-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="2ab1d-122">MSBuild.exe</span></span> | <span data-ttu-id="2ab1d-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="2ab1d-123">.NET Framework</span></span> |
| <span data-ttu-id="2ab1d-124">NuGet. exe sur mono</span><span class="sxs-lookup"><span data-stu-id="2ab1d-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="2ab1d-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="2ab1d-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="2ab1d-126">Comment cela fonctionne-t-il ?</span><span class="sxs-lookup"><span data-stu-id="2ab1d-126">How does it work</span></span>

<span data-ttu-id="2ab1d-127">Le flux de travail de haut niveau peut être décrit comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="2ab1d-128">NuGet Découvre les plug-ins disponibles.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="2ab1d-129">Le cas échéant, NuGet effectue une itération sur les plug-ins par ordre de priorité et les démarre un par un.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="2ab1d-130">NuGet utilise le premier plug-in qui peut traiter la demande.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="2ab1d-131">Les plug-ins sont arrêtés lorsqu’ils ne sont plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="2ab1d-132">Exigences générales du plug-in</span><span class="sxs-lookup"><span data-stu-id="2ab1d-132">General plugin requirements</span></span>

<span data-ttu-id="2ab1d-133">La version actuelle du protocole est *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="2ab1d-134">Dans cette version, les conditions requises sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="2ab1d-135">Avoir un assembly de signature Authenticode valide et approuvé qui s’exécutera sur Windows et mono.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="2ab1d-136">Il n’existe pas encore d’exigence de confiance spéciale pour les assemblys exécutés sur Linux et Mac.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="2ab1d-137">Problème pertinent</span><span class="sxs-lookup"><span data-stu-id="2ab1d-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="2ab1d-138">Prend en charge le lancement sans état dans le contexte de sécurité actuel des outils clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="2ab1d-139">Par exemple, les outils clients NuGet n’effectuent pas d’élévation ou d’initialisation supplémentaire en dehors du protocole de plug-in décrit plus loin.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="2ab1d-140">Être non interactif, sauf spécification explicite.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="2ab1d-141">Adhérer à la version du protocole de plug-in négocié.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="2ab1d-142">Répondez à toutes les demandes dans un délai raisonnable.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="2ab1d-143">Honorez les demandes d’annulation pour toute opération en cours.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="2ab1d-144">La spécification technique est décrite plus en détail dans les spécifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="2ab1d-145">Plug-in de téléchargement de package NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="2ab1d-146">Plug-in d’authentification Cross plat NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="2ab1d-147">Interaction client-plug-in</span><span class="sxs-lookup"><span data-stu-id="2ab1d-147">Client - Plugin interaction</span></span>

<span data-ttu-id="2ab1d-148">Les outils clients NuGet et les plug-ins communiquent avec JSON sur les flux standard (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="2ab1d-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="2ab1d-149">Toutes les données doivent être encodées en UTF-8.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="2ab1d-150">Les plug-ins sont lancés avec l’argument « -plugin ».</span><span class="sxs-lookup"><span data-stu-id="2ab1d-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="2ab1d-151">Si un utilisateur lance directement un exécutable de plug-in sans cet argument, le plug-in peut fournir un message d’information au lieu d’attendre une négociation de protocole.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="2ab1d-152">Le délai d’expiration de la négociation de protocole est de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="2ab1d-153">Le plug-in doit effectuer l’installation dans un montant aussi réduit que possible.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="2ab1d-154">Les outils clients NuGet interrogent les opérations prises en charge par un plug-in en passant l’index de service pour une source NuGet.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="2ab1d-155">Un plug-in peut utiliser l’index de service pour vérifier la présence de types de service pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="2ab1d-156">La communication entre les outils clients NuGet et le plug-in est bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="2ab1d-157">Chaque demande a un délai d’expiration de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="2ab1d-158">Si les opérations sont censées prendre plus de temps, le processus concerné doit envoyer un message de progression pour empêcher l’expiration du délai d’attente de la demande. Après 1 minute d’inactivité, un plug-in est considéré comme inactif et est arrêté.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="2ab1d-159">Installation et détection du plug-in</span><span class="sxs-lookup"><span data-stu-id="2ab1d-159">Plugin installation and discovery</span></span>

<span data-ttu-id="2ab1d-160">Les plug-ins seront découverts via une structure de répertoires basée sur une convention.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="2ab1d-161">Les scénarios CI/CD et les utilisateurs avec pouvoir peuvent utiliser des variables d’environnement pour remplacer le comportement.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="2ab1d-162">Notez que `NUGET_NETFX_PLUGIN_PATHS` et `NUGET_NETCORE_PLUGIN_PATHS` sont uniquement disponibles avec 5.3 + version des outils NuGet et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="2ab1d-163">`NUGET_NETFX_PLUGIN_PATHS`-définit les plug-ins qui seront utilisés par les outils basés sur .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="2ab1d-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="2ab1d-164">Est prioritaire sur `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="2ab1d-165">(NuGet version 5.3 + uniquement)</span><span class="sxs-lookup"><span data-stu-id="2ab1d-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="2ab1d-166">`NUGET_NETCORE_PLUGIN_PATHS`-définit les plug-ins qui seront utilisés par les outils basés sur .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="2ab1d-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="2ab1d-167">Est prioritaire sur `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="2ab1d-168">(NuGet version 5.3 + uniquement)</span><span class="sxs-lookup"><span data-stu-id="2ab1d-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="2ab1d-169">`NUGET_PLUGIN_PATHS`-définit les plug-ins qui seront utilisés pour ce processus NuGet, avec une priorité réservée.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="2ab1d-170">Si cette variable d’environnement est définie, elle remplace la détection basée sur une convention.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="2ab1d-171">Ignoré si l’une des variables spécifiques à l’infrastructure est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="2ab1d-172">User-Location, l’emplacement d’hébergement NuGet `%UserProfile%/.nuget/plugins`dans.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="2ab1d-173">Cet emplacement ne peut pas être remplacé.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-173">This location cannot be overriden.</span></span> <span data-ttu-id="2ab1d-174">Un répertoire racine différent sera utilisé pour les plug-ins .NET Core et .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="2ab1d-175">Framework</span><span class="sxs-lookup"><span data-stu-id="2ab1d-175">Framework</span></span> | <span data-ttu-id="2ab1d-176">Emplacement de la détection racine</span><span class="sxs-lookup"><span data-stu-id="2ab1d-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="2ab1d-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2ab1d-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="2ab1d-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="2ab1d-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="2ab1d-179">Chaque plug-in doit être installé dans son propre dossier.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="2ab1d-180">Le point d’entrée du plug-in sera le nom du dossier installé, avec les extensions. dll pour .NET Core et l’extension. exe pour .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="2ab1d-181">Il n’existe actuellement aucun récit utilisateur pour l’installation des plug-ins.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="2ab1d-182">C’est aussi simple que de déplacer les fichiers requis à l’emplacement prédéterminé.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="2ab1d-183">Opérations prises en charge</span><span class="sxs-lookup"><span data-stu-id="2ab1d-183">Supported operations</span></span>

<span data-ttu-id="2ab1d-184">Deux opérations sont prises en charge dans le nouveau protocole de plug-in.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="2ab1d-185">Nom d’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-185">Operation name</span></span> | <span data-ttu-id="2ab1d-186">Version de protocole minimale</span><span class="sxs-lookup"><span data-stu-id="2ab1d-186">Minimum protocol version</span></span> | <span data-ttu-id="2ab1d-187">Version minimale du client NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="2ab1d-188">Télécharger le package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-188">Download Package</span></span> | <span data-ttu-id="2ab1d-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="2ab1d-189">1.0.0</span></span> | <span data-ttu-id="2ab1d-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="2ab1d-190">4.3.0</span></span> |
| [<span data-ttu-id="2ab1d-191">Authentification</span><span class="sxs-lookup"><span data-stu-id="2ab1d-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="2ab1d-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="2ab1d-192">2.0.0</span></span> | <span data-ttu-id="2ab1d-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="2ab1d-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="2ab1d-194">Exécution de plug-ins sous le runtime approprié</span><span class="sxs-lookup"><span data-stu-id="2ab1d-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="2ab1d-195">Pour le NuGet dans les scénarios dotnet. exe, les plug-ins doivent être en mesure de s’exécuter sous ce Runtime spécifique du dotNET. exe.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="2ab1d-196">Il se trouve sur le fournisseur de plug-ins et le consommateur pour s’assurer qu’une combinaison dotnet. exe/plugin compatible est utilisée.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="2ab1d-197">Un problème potentiel peut survenir avec les plug-ins d’emplacement utilisateur quand, par exemple, un dotnet. exe sous le runtime 2,0 essaie d’utiliser un plug-in écrit pour le runtime 2,1.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="2ab1d-198">Mise en cache des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="2ab1d-198">Capabilities caching</span></span>

<span data-ttu-id="2ab1d-199">La vérification de la sécurité et l’instanciation des plug-ins sont coûteux.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="2ab1d-200">L’opération de téléchargement se produit plus fréquemment que l’opération d’authentification, mais l’utilisateur NuGet moyen est uniquement susceptible d’avoir un plug-in d’authentification.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="2ab1d-201">Pour améliorer l’expérience, NuGet met en cache les revendications d’opération pour la demande donnée.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="2ab1d-202">Ce cache est par plug-in dont la clé de plug-in est le chemin du plug-in, et l’expiration pour ce cache de fonctionnalités est de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="2ab1d-203">Le cache se trouve dans `%LocalAppData%/NuGet/plugins-cache` et est remplacé par la variable `NUGET_PLUGINS_CACHE_PATH`d’environnement.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="2ab1d-204">Pour effacer ce [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), vous pouvez exécuter la commande variables locales avec l' `plugins-cache` option.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="2ab1d-205">L' `all` option variables locales va également supprimer le cache des plug-ins.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="2ab1d-206">Index des messages de protocole</span><span class="sxs-lookup"><span data-stu-id="2ab1d-206">Protocol messages index</span></span>

<span data-ttu-id="2ab1d-207">Messages de la version de protocole *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="2ab1d-208">Fermer</span><span class="sxs-lookup"><span data-stu-id="2ab1d-208">Close</span></span>
    * <span data-ttu-id="2ab1d-209">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="2ab1d-210">La demande ne contient pas de charge utile</span><span class="sxs-lookup"><span data-stu-id="2ab1d-210">The request will contain no payload</span></span>
    * <span data-ttu-id="2ab1d-211">Aucune réponse n’est attendue.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-211">No response is expected.</span></span>  <span data-ttu-id="2ab1d-212">La réponse appropriée est que le processus du plug-in s’arrête rapidement.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="2ab1d-213">Copier les fichiers dans le package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-213">Copy files in package</span></span>
    * <span data-ttu-id="2ab1d-214">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="2ab1d-215">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-215">The request will contain:</span></span>
        * <span data-ttu-id="2ab1d-216">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-216">the package ID and version</span></span>
        * <span data-ttu-id="2ab1d-217">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-217">the package source repository location</span></span>
        * <span data-ttu-id="2ab1d-218">chemin du répertoire de destination</span><span class="sxs-lookup"><span data-stu-id="2ab1d-218">destination directory path</span></span>
        * <span data-ttu-id="2ab1d-219">énumérable des fichiers dans le package à copier dans le chemin d’accès au répertoire de destination</span><span class="sxs-lookup"><span data-stu-id="2ab1d-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="2ab1d-220">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-220">A response will contain:</span></span>
        * <span data-ttu-id="2ab1d-221">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="2ab1d-222">énumérable de chemins d’accès complets pour les fichiers copiés dans le répertoire de destination si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="2ab1d-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="2ab1d-223">Copier le fichier de package (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="2ab1d-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="2ab1d-224">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="2ab1d-225">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-225">The request will contain:</span></span>
        * <span data-ttu-id="2ab1d-226">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-226">the package ID and version</span></span>
        * <span data-ttu-id="2ab1d-227">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-227">the package source repository location</span></span>
        * <span data-ttu-id="2ab1d-228">chemin d’accès au fichier de destination</span><span class="sxs-lookup"><span data-stu-id="2ab1d-228">the destination file path</span></span>
    * <span data-ttu-id="2ab1d-229">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-229">A response will contain:</span></span>
        * <span data-ttu-id="2ab1d-230">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="2ab1d-231">Récupérer les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="2ab1d-231">Get credentials</span></span>
    * <span data-ttu-id="2ab1d-232">Direction de la demande : plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="2ab1d-233">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-233">The request will contain:</span></span>
        * <span data-ttu-id="2ab1d-234">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-234">the package source repository location</span></span>
        * <span data-ttu-id="2ab1d-235">code d’état HTTP obtenu à partir du référentiel source du package à l’aide des informations d’identification actuelles</span><span class="sxs-lookup"><span data-stu-id="2ab1d-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="2ab1d-236">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-236">A response will contain:</span></span>
        * <span data-ttu-id="2ab1d-237">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="2ab1d-238">un nom d’utilisateur, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="2ab1d-238">a username, if available</span></span>
        * <span data-ttu-id="2ab1d-239">un mot de passe, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="2ab1d-239">a password, if available</span></span>

5.  <span data-ttu-id="2ab1d-240">Récupérer les fichiers dans le package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-240">Get files in package</span></span>
    * <span data-ttu-id="2ab1d-241">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="2ab1d-242">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-242">The request will contain:</span></span>
        * <span data-ttu-id="2ab1d-243">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-243">the package ID and version</span></span>
        * <span data-ttu-id="2ab1d-244">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-244">the package source repository location</span></span>
    * <span data-ttu-id="2ab1d-245">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-245">A response will contain:</span></span>
        * <span data-ttu-id="2ab1d-246">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="2ab1d-247">énumérable de chemins d’accès de fichiers dans le package si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="2ab1d-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="2ab1d-248">Récupération des revendications d’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-248">Get operation claims</span></span> 
    * <span data-ttu-id="2ab1d-249">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="2ab1d-250">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-250">The request will contain:</span></span>
        * <span data-ttu-id="2ab1d-251">service index. JSON pour une source de package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="2ab1d-252">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-252">the package source repository location</span></span>
    * <span data-ttu-id="2ab1d-253">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-253">A response will contain:</span></span>
        * <span data-ttu-id="2ab1d-254">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="2ab1d-255">énumérable des opérations prises en charge (par exemple, téléchargement de package) si l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="2ab1d-256">Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un ensemble vide d’opérations prises en charge.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="2ab1d-257">Ce message a été mis à jour dans la version *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="2ab1d-258">Il se trouve sur le client pour préserver la compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="2ab1d-259">Obtient le hachage du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-259">Get package hash</span></span>
    * <span data-ttu-id="2ab1d-260">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="2ab1d-261">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-261">The request will contain:</span></span>
        * <span data-ttu-id="2ab1d-262">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-262">the package ID and version</span></span>
        * <span data-ttu-id="2ab1d-263">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-263">the package source repository location</span></span>
        * <span data-ttu-id="2ab1d-264">algorithme de hachage</span><span class="sxs-lookup"><span data-stu-id="2ab1d-264">the hash algorithm</span></span>
    * <span data-ttu-id="2ab1d-265">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-265">A response will contain:</span></span>
        * <span data-ttu-id="2ab1d-266">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="2ab1d-267">hachage de fichier de package utilisant l’algorithme de hachage demandé si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="2ab1d-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="2ab1d-268">Obtient les versions du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-268">Get package versions</span></span>
    * <span data-ttu-id="2ab1d-269">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="2ab1d-270">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-270">The request will contain:</span></span>
        * <span data-ttu-id="2ab1d-271">ID du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-271">the package ID</span></span>
        * <span data-ttu-id="2ab1d-272">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-272">the package source repository location</span></span>
    * <span data-ttu-id="2ab1d-273">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-273">A response will contain:</span></span>
        * <span data-ttu-id="2ab1d-274">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="2ab1d-275">énumérable des versions de packages si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="2ab1d-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="2ab1d-276">Obtient l’index de service</span><span class="sxs-lookup"><span data-stu-id="2ab1d-276">Get service index</span></span>
    * <span data-ttu-id="2ab1d-277">Direction de la demande : plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="2ab1d-278">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-278">The request will contain:</span></span>
        * <span data-ttu-id="2ab1d-279">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-279">the package source repository location</span></span>
    * <span data-ttu-id="2ab1d-280">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-280">A response will contain:</span></span>
        * <span data-ttu-id="2ab1d-281">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="2ab1d-282">index du service si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="2ab1d-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="2ab1d-283">Négociation</span><span class="sxs-lookup"><span data-stu-id="2ab1d-283">Handshake</span></span>
     * <span data-ttu-id="2ab1d-284">Direction de la demande :  < NuGet-plug-in ></span><span class="sxs-lookup"><span data-stu-id="2ab1d-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="2ab1d-285">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-285">The request will contain:</span></span>
         * <span data-ttu-id="2ab1d-286">version actuelle du protocole de plug-in</span><span class="sxs-lookup"><span data-stu-id="2ab1d-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="2ab1d-287">version de protocole du plug-in minimale prise en charge</span><span class="sxs-lookup"><span data-stu-id="2ab1d-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="2ab1d-288">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-288">A response will contain:</span></span>
         * <span data-ttu-id="2ab1d-289">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="2ab1d-290">version du protocole négocié si l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="2ab1d-291">Une défaillance entraînera l’arrêt du plug-in.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="2ab1d-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="2ab1d-292">Initialize</span></span>
     * <span data-ttu-id="2ab1d-293">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="2ab1d-294">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-294">The request will contain:</span></span>
         * <span data-ttu-id="2ab1d-295">version de l’outil client NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="2ab1d-296">langage de l’outil client NuGet en vigueur.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="2ab1d-297">Cela prend en compte le paramètre ForceEnglishOutput, s’il est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="2ab1d-298">délai d’expiration de la demande par défaut, qui remplace la valeur par défaut du protocole.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="2ab1d-299">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-299">A response will contain:</span></span>
         * <span data-ttu-id="2ab1d-300">Code de réponse indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="2ab1d-301">Une défaillance entraînera l’arrêt du plug-in.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="2ab1d-302">Journal</span><span class="sxs-lookup"><span data-stu-id="2ab1d-302">Log</span></span>
     * <span data-ttu-id="2ab1d-303">Direction de la demande : plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="2ab1d-304">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-304">The request will contain:</span></span>
         * <span data-ttu-id="2ab1d-305">niveau de journalisation de la demande</span><span class="sxs-lookup"><span data-stu-id="2ab1d-305">the log level for the request</span></span>
         * <span data-ttu-id="2ab1d-306">message à consigner</span><span class="sxs-lookup"><span data-stu-id="2ab1d-306">a message to log</span></span>
     * <span data-ttu-id="2ab1d-307">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-307">A response will contain:</span></span>
         * <span data-ttu-id="2ab1d-308">Code de réponse indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="2ab1d-309">Surveiller la sortie du processus NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="2ab1d-310">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="2ab1d-311">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-311">The request will contain:</span></span>
         * <span data-ttu-id="2ab1d-312">l’ID de processus NuGet</span><span class="sxs-lookup"><span data-stu-id="2ab1d-312">the NuGet process ID</span></span>
     * <span data-ttu-id="2ab1d-313">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-313">A response will contain:</span></span>
         * <span data-ttu-id="2ab1d-314">Code de réponse indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="2ab1d-315">Prérécupérer le package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-315">Prefetch package</span></span>
     * <span data-ttu-id="2ab1d-316">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="2ab1d-317">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-317">The request will contain:</span></span>
         * <span data-ttu-id="2ab1d-318">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-318">the package ID and version</span></span>
         * <span data-ttu-id="2ab1d-319">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-319">the package source repository location</span></span>
     * <span data-ttu-id="2ab1d-320">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-320">A response will contain:</span></span>
         * <span data-ttu-id="2ab1d-321">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="2ab1d-322">Définir les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="2ab1d-322">Set credentials</span></span>
     * <span data-ttu-id="2ab1d-323">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="2ab1d-324">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-324">The request will contain:</span></span>
         * <span data-ttu-id="2ab1d-325">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-325">the package source repository location</span></span>
         * <span data-ttu-id="2ab1d-326">dernier nom d’utilisateur source de package connu, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="2ab1d-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="2ab1d-327">dernier mot de passe de source de package connu, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="2ab1d-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="2ab1d-328">dernier nom d’utilisateur du proxy connu, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="2ab1d-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="2ab1d-329">dernier mot de passe du proxy connu, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="2ab1d-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="2ab1d-330">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-330">A response will contain:</span></span>
         * <span data-ttu-id="2ab1d-331">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="2ab1d-332">Définir le niveau de journal</span><span class="sxs-lookup"><span data-stu-id="2ab1d-332">Set log level</span></span>
     * <span data-ttu-id="2ab1d-333">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="2ab1d-334">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-334">The request will contain:</span></span>
         * <span data-ttu-id="2ab1d-335">niveau de journalisation par défaut</span><span class="sxs-lookup"><span data-stu-id="2ab1d-335">the default log level</span></span>
     * <span data-ttu-id="2ab1d-336">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-336">A response will contain:</span></span>
         * <span data-ttu-id="2ab1d-337">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="2ab1d-338">Messages du protocole version *2.0.0*</span><span class="sxs-lookup"><span data-stu-id="2ab1d-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="2ab1d-339">Récupération des revendications d’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-339">Get Operation Claims</span></span>

* <span data-ttu-id="2ab1d-340">Direction de la demande :  Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="2ab1d-341">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-341">The request will contain:</span></span>
        * <span data-ttu-id="2ab1d-342">service index. JSON pour une source de package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="2ab1d-343">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="2ab1d-343">the package source repository location</span></span>
    * <span data-ttu-id="2ab1d-344">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-344">A response will contain:</span></span>
        * <span data-ttu-id="2ab1d-345">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="2ab1d-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="2ab1d-346">énumérable des opérations prises en charge si l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="2ab1d-347">Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un ensemble vide d’opérations prises en charge.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="2ab1d-348">Si l’index de service et la source de package ont la valeur null, le plug-in peut répondre avec l’authentification.</span><span class="sxs-lookup"><span data-stu-id="2ab1d-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="2ab1d-349">Récupérer les informations d’identification d’authentification</span><span class="sxs-lookup"><span data-stu-id="2ab1d-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="2ab1d-350">Direction de la demande : Plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="2ab1d-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="2ab1d-351">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="2ab1d-351">The request will contain:</span></span>
    * <span data-ttu-id="2ab1d-352">URI</span><span class="sxs-lookup"><span data-stu-id="2ab1d-352">Uri</span></span>
    * <span data-ttu-id="2ab1d-353">isRetry</span><span class="sxs-lookup"><span data-stu-id="2ab1d-353">isRetry</span></span>
    * <span data-ttu-id="2ab1d-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2ab1d-354">NonInteractive</span></span>
    * <span data-ttu-id="2ab1d-355">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="2ab1d-355">CanShowDialog</span></span>
* <span data-ttu-id="2ab1d-356">Une réponse contient</span><span class="sxs-lookup"><span data-stu-id="2ab1d-356">A response will contain</span></span>
    * <span data-ttu-id="2ab1d-357">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2ab1d-357">Username</span></span>
    * <span data-ttu-id="2ab1d-358">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="2ab1d-358">Password</span></span>
    * <span data-ttu-id="2ab1d-359">Message</span><span class="sxs-lookup"><span data-stu-id="2ab1d-359">Message</span></span>
    * <span data-ttu-id="2ab1d-360">Liste des types d’authentification</span><span class="sxs-lookup"><span data-stu-id="2ab1d-360">List of Auth Types</span></span>
    * <span data-ttu-id="2ab1d-361">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="2ab1d-361">MessageResponseCode</span></span>
