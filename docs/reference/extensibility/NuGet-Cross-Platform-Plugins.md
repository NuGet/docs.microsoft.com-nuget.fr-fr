---
title: Plug-ins inter-plateforme NuGet
description: Plug-ins inter-plateforme NuGet pour NuGet. exe, dotnet. exe, MSBuild. exe et Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429107"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="f95c0-103">Plug-ins inter-plateforme NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="f95c0-104">Dans NuGet 4.8 +, la prise en charge des plug-ins multiplateforme a été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="f95c0-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="f95c0-105">Pour cela, vous devez créer un nouveau modèle d’extensibilité de plug-in, qui doit se conformer à un ensemble strict de règles d’opération.</span><span class="sxs-lookup"><span data-stu-id="f95c0-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="f95c0-106">Les plug-ins sont des exécutables autonomes (Runnables dans le monde de .NET Core), que les clients NuGet lancent dans un processus distinct.</span><span class="sxs-lookup"><span data-stu-id="f95c0-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="f95c0-107">Il s’agit d’un plug-in réel en écriture unique, Run Everywhere.</span><span class="sxs-lookup"><span data-stu-id="f95c0-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="f95c0-108">Il fonctionne avec tous les outils clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="f95c0-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="f95c0-109">Les plug-ins peuvent être .NET Framework (NuGet. exe, MSBuild. exe et Visual Studio) ou .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="f95c0-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="f95c0-110">Un protocole de communication avec version entre le client NuGet et le plug-in est défini.</span><span class="sxs-lookup"><span data-stu-id="f95c0-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="f95c0-111">Au cours de l’établissement de liaison de démarrage, les 2 processus négocient la version du protocole.</span><span class="sxs-lookup"><span data-stu-id="f95c0-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="f95c0-112">Pour couvrir tous les scénarios d’outils clients NuGet, vous devez disposer d’un .NET Framework et d’un plug-in .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f95c0-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="f95c0-113">La description ci-dessous décrit les combinaisons client/Framework des plug-ins.</span><span class="sxs-lookup"><span data-stu-id="f95c0-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="f95c0-114">Outil client</span><span class="sxs-lookup"><span data-stu-id="f95c0-114">Client tool</span></span>  | <span data-ttu-id="f95c0-115">Framework</span><span class="sxs-lookup"><span data-stu-id="f95c0-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="f95c0-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f95c0-116">Visual Studio</span></span> | <span data-ttu-id="f95c0-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f95c0-117">.NET Framework</span></span> |
| <span data-ttu-id="f95c0-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="f95c0-118">dotnet.exe</span></span> | <span data-ttu-id="f95c0-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f95c0-119">.NET Core</span></span> |
| <span data-ttu-id="f95c0-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="f95c0-120">NuGet.exe</span></span> | <span data-ttu-id="f95c0-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f95c0-121">.NET Framework</span></span> |
| <span data-ttu-id="f95c0-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="f95c0-122">MSBuild.exe</span></span> | <span data-ttu-id="f95c0-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f95c0-123">.NET Framework</span></span> |
| <span data-ttu-id="f95c0-124">NuGet. exe sur mono</span><span class="sxs-lookup"><span data-stu-id="f95c0-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="f95c0-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f95c0-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="f95c0-126">Comment cela fonctionne-t-il ?</span><span class="sxs-lookup"><span data-stu-id="f95c0-126">How does it work</span></span>

<span data-ttu-id="f95c0-127">Le flux de travail de haut niveau peut être décrit comme suit :</span><span class="sxs-lookup"><span data-stu-id="f95c0-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="f95c0-128">NuGet Découvre les plug-ins disponibles.</span><span class="sxs-lookup"><span data-stu-id="f95c0-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="f95c0-129">Le cas échéant, NuGet effectue une itération sur les plug-ins par ordre de priorité et les démarre un par un.</span><span class="sxs-lookup"><span data-stu-id="f95c0-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="f95c0-130">NuGet utilise le premier plug-in qui peut traiter la demande.</span><span class="sxs-lookup"><span data-stu-id="f95c0-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="f95c0-131">Les plug-ins sont arrêtés lorsqu’ils ne sont plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="f95c0-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="f95c0-132">Exigences générales du plug-in</span><span class="sxs-lookup"><span data-stu-id="f95c0-132">General plugin requirements</span></span>

<span data-ttu-id="f95c0-133">La version actuelle du protocole est *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="f95c0-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="f95c0-134">Dans cette version, les conditions requises sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f95c0-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="f95c0-135">Avoir un assembly de signature Authenticode valide et approuvé qui s’exécutera sur Windows et mono.</span><span class="sxs-lookup"><span data-stu-id="f95c0-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="f95c0-136">Il n’existe pas encore d’exigence de confiance spéciale pour les assemblys exécutés sur Linux et Mac.</span><span class="sxs-lookup"><span data-stu-id="f95c0-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="f95c0-137">Problème pertinent</span><span class="sxs-lookup"><span data-stu-id="f95c0-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="f95c0-138">Prend en charge le lancement sans état dans le contexte de sécurité actuel des outils clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="f95c0-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="f95c0-139">Par exemple, les outils clients NuGet n’effectuent pas d’élévation ou d’initialisation supplémentaire en dehors du protocole de plug-in décrit plus loin.</span><span class="sxs-lookup"><span data-stu-id="f95c0-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="f95c0-140">Être non interactif, sauf spécification explicite.</span><span class="sxs-lookup"><span data-stu-id="f95c0-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="f95c0-141">Adhérer à la version du protocole de plug-in négocié.</span><span class="sxs-lookup"><span data-stu-id="f95c0-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="f95c0-142">Répondez à toutes les demandes dans un délai raisonnable.</span><span class="sxs-lookup"><span data-stu-id="f95c0-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="f95c0-143">Honorez les demandes d’annulation pour toute opération en cours.</span><span class="sxs-lookup"><span data-stu-id="f95c0-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="f95c0-144">La spécification technique est décrite plus en détail dans les spécifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="f95c0-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="f95c0-145">Plug-in de téléchargement de package NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="f95c0-146">Plug-in d’authentification Cross plat NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="f95c0-147">Interaction client-plug-in</span><span class="sxs-lookup"><span data-stu-id="f95c0-147">Client - Plugin interaction</span></span>

<span data-ttu-id="f95c0-148">Les outils clients NuGet et les plug-ins communiquent avec JSON sur les flux standard (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="f95c0-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="f95c0-149">Toutes les données doivent être encodées en UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f95c0-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="f95c0-150">Les plug-ins sont lancés avec l’argument « -plugin ».</span><span class="sxs-lookup"><span data-stu-id="f95c0-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="f95c0-151">Si un utilisateur lance directement un exécutable de plug-in sans cet argument, le plug-in peut fournir un message d’information au lieu d’attendre une négociation de protocole.</span><span class="sxs-lookup"><span data-stu-id="f95c0-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="f95c0-152">Le délai d’expiration de la négociation de protocole est de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="f95c0-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="f95c0-153">Le plug-in doit effectuer l’installation dans un montant aussi réduit que possible.</span><span class="sxs-lookup"><span data-stu-id="f95c0-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="f95c0-154">Les outils clients NuGet interrogent les opérations prises en charge par un plug-in en passant l’index de service pour une source NuGet.</span><span class="sxs-lookup"><span data-stu-id="f95c0-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="f95c0-155">Un plug-in peut utiliser l’index de service pour vérifier la présence de types de service pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f95c0-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="f95c0-156">La communication entre les outils clients NuGet et le plug-in est bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="f95c0-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="f95c0-157">Chaque demande a un délai d’expiration de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="f95c0-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="f95c0-158">Si les opérations sont censées prendre plus de temps, le processus concerné doit envoyer un message de progression pour empêcher l’expiration du délai d’attente de la demande. Après 1 minute d’inactivité, un plug-in est considéré comme inactif et est arrêté.</span><span class="sxs-lookup"><span data-stu-id="f95c0-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="f95c0-159">Installation et détection du plug-in</span><span class="sxs-lookup"><span data-stu-id="f95c0-159">Plugin installation and discovery</span></span>

<span data-ttu-id="f95c0-160">Les plug-ins seront découverts via une structure de répertoires basée sur une convention.</span><span class="sxs-lookup"><span data-stu-id="f95c0-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="f95c0-161">Les scénarios CI/CD et les utilisateurs avec pouvoir peuvent utiliser des variables d’environnement pour remplacer le comportement.</span><span class="sxs-lookup"><span data-stu-id="f95c0-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="f95c0-162">Lorsque vous utilisez des variables d’environnement, seuls les chemins d’accès absolus sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="f95c0-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="f95c0-163">Notez que `NUGET_NETFX_PLUGIN_PATHS` et `NUGET_NETCORE_PLUGIN_PATHS` sont uniquement disponibles avec 5.3 + version des outils NuGet et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="f95c0-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="f95c0-164">`NUGET_NETFX_PLUGIN_PATHS` : définit les plug-ins qui seront utilisés par les outils basés sur .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="f95c0-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="f95c0-165">Est prioritaire sur `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="f95c0-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="f95c0-166">(NuGet version 5.3 + uniquement)</span><span class="sxs-lookup"><span data-stu-id="f95c0-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="f95c0-167">`NUGET_NETCORE_PLUGIN_PATHS` : définit les plug-ins qui seront utilisés par les outils basés sur .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="f95c0-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="f95c0-168">Est prioritaire sur `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="f95c0-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="f95c0-169">(NuGet version 5.3 + uniquement)</span><span class="sxs-lookup"><span data-stu-id="f95c0-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="f95c0-170">`NUGET_PLUGIN_PATHS` : définit les plug-ins qui seront utilisés pour ce processus NuGet, priorité préservée.</span><span class="sxs-lookup"><span data-stu-id="f95c0-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="f95c0-171">Si cette variable d’environnement est définie, elle remplace la détection basée sur une convention.</span><span class="sxs-lookup"><span data-stu-id="f95c0-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="f95c0-172">Ignoré si l’une des variables spécifiques à l’infrastructure est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="f95c0-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="f95c0-173">Utilisateur-emplacement, emplacement d’hébergement NuGet dans `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="f95c0-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="f95c0-174">Cet emplacement ne peut pas être remplacé.</span><span class="sxs-lookup"><span data-stu-id="f95c0-174">This location cannot be overriden.</span></span> <span data-ttu-id="f95c0-175">Un répertoire racine différent sera utilisé pour les plug-ins .NET Core et .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f95c0-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="f95c0-176">Framework</span><span class="sxs-lookup"><span data-stu-id="f95c0-176">Framework</span></span> | <span data-ttu-id="f95c0-177">Emplacement de la détection racine</span><span class="sxs-lookup"><span data-stu-id="f95c0-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="f95c0-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f95c0-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="f95c0-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f95c0-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="f95c0-180">Chaque plug-in doit être installé dans son propre dossier.</span><span class="sxs-lookup"><span data-stu-id="f95c0-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="f95c0-181">Le point d’entrée du plug-in sera le nom du dossier installé, avec les extensions. dll pour .NET Core et l’extension. exe pour .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f95c0-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="f95c0-182">Il n’existe actuellement aucun récit utilisateur pour l’installation des plug-ins.</span><span class="sxs-lookup"><span data-stu-id="f95c0-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="f95c0-183">C’est aussi simple que de déplacer les fichiers requis à l’emplacement prédéterminé.</span><span class="sxs-lookup"><span data-stu-id="f95c0-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="f95c0-184">Opérations prises en charge</span><span class="sxs-lookup"><span data-stu-id="f95c0-184">Supported operations</span></span>

<span data-ttu-id="f95c0-185">Deux opérations sont prises en charge dans le nouveau protocole de plug-in.</span><span class="sxs-lookup"><span data-stu-id="f95c0-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="f95c0-186">Nom d’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-186">Operation name</span></span> | <span data-ttu-id="f95c0-187">Version de protocole minimale</span><span class="sxs-lookup"><span data-stu-id="f95c0-187">Minimum protocol version</span></span> | <span data-ttu-id="f95c0-188">Version minimale du client NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="f95c0-189">Télécharger le package</span><span class="sxs-lookup"><span data-stu-id="f95c0-189">Download Package</span></span> | <span data-ttu-id="f95c0-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f95c0-190">1.0.0</span></span> | <span data-ttu-id="f95c0-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="f95c0-191">4.3.0</span></span> |
| [<span data-ttu-id="f95c0-192">Authentification</span><span class="sxs-lookup"><span data-stu-id="f95c0-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="f95c0-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="f95c0-193">2.0.0</span></span> | <span data-ttu-id="f95c0-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="f95c0-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="f95c0-195">Exécution de plug-ins sous le runtime approprié</span><span class="sxs-lookup"><span data-stu-id="f95c0-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="f95c0-196">Pour le NuGet dans les scénarios dotnet. exe, les plug-ins doivent être en mesure de s’exécuter sous ce Runtime spécifique du dotNET. exe.</span><span class="sxs-lookup"><span data-stu-id="f95c0-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="f95c0-197">Il se trouve sur le fournisseur de plug-ins et le consommateur pour s’assurer qu’une combinaison dotnet. exe/plugin compatible est utilisée.</span><span class="sxs-lookup"><span data-stu-id="f95c0-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="f95c0-198">Un problème potentiel peut survenir avec les plug-ins d’emplacement utilisateur quand, par exemple, un dotnet. exe sous le runtime 2,0 essaie d’utiliser un plug-in écrit pour le runtime 2,1.</span><span class="sxs-lookup"><span data-stu-id="f95c0-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="f95c0-199">Mise en cache des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="f95c0-199">Capabilities caching</span></span>

<span data-ttu-id="f95c0-200">La vérification de la sécurité et l’instanciation des plug-ins sont coûteux.</span><span class="sxs-lookup"><span data-stu-id="f95c0-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="f95c0-201">L’opération de téléchargement se produit plus fréquemment que l’opération d’authentification, mais l’utilisateur NuGet moyen est uniquement susceptible d’avoir un plug-in d’authentification.</span><span class="sxs-lookup"><span data-stu-id="f95c0-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="f95c0-202">Pour améliorer l’expérience, NuGet met en cache les revendications d’opération pour la demande donnée.</span><span class="sxs-lookup"><span data-stu-id="f95c0-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="f95c0-203">Ce cache est par plug-in dont la clé de plug-in est le chemin du plug-in, et l’expiration pour ce cache de fonctionnalités est de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="f95c0-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="f95c0-204">Le cache se trouve dans `%LocalAppData%/NuGet/plugins-cache` et est remplacé par la variable d’environnement `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="f95c0-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="f95c0-205">Pour effacer ce [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), vous pouvez exécuter la commande variables locales avec l’option `plugins-cache`.</span><span class="sxs-lookup"><span data-stu-id="f95c0-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="f95c0-206">L’option `all` variables locales va également supprimer le cache des plug-ins.</span><span class="sxs-lookup"><span data-stu-id="f95c0-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="f95c0-207">Index des messages de protocole</span><span class="sxs-lookup"><span data-stu-id="f95c0-207">Protocol messages index</span></span>

<span data-ttu-id="f95c0-208">Messages de la version de protocole *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="f95c0-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="f95c0-209">fermez</span><span class="sxs-lookup"><span data-stu-id="f95c0-209">Close</span></span>
    * <span data-ttu-id="f95c0-210">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f95c0-211">La demande ne contient pas de charge utile</span><span class="sxs-lookup"><span data-stu-id="f95c0-211">The request will contain no payload</span></span>
    * <span data-ttu-id="f95c0-212">Aucune réponse n’est attendue.</span><span class="sxs-lookup"><span data-stu-id="f95c0-212">No response is expected.</span></span>  <span data-ttu-id="f95c0-213">La réponse appropriée est que le processus du plug-in s’arrête rapidement.</span><span class="sxs-lookup"><span data-stu-id="f95c0-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="f95c0-214">Copier les fichiers dans le package</span><span class="sxs-lookup"><span data-stu-id="f95c0-214">Copy files in package</span></span>
    * <span data-ttu-id="f95c0-215">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f95c0-216">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-216">The request will contain:</span></span>
        * <span data-ttu-id="f95c0-217">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-217">the package ID and version</span></span>
        * <span data-ttu-id="f95c0-218">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-218">the package source repository location</span></span>
        * <span data-ttu-id="f95c0-219">chemin du répertoire de destination</span><span class="sxs-lookup"><span data-stu-id="f95c0-219">destination directory path</span></span>
        * <span data-ttu-id="f95c0-220">énumérable des fichiers dans le package à copier dans le chemin d’accès au répertoire de destination</span><span class="sxs-lookup"><span data-stu-id="f95c0-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="f95c0-221">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-221">A response will contain:</span></span>
        * <span data-ttu-id="f95c0-222">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f95c0-223">énumérable de chemins d’accès complets pour les fichiers copiés dans le répertoire de destination si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="f95c0-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="f95c0-224">Copier le fichier de package (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="f95c0-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="f95c0-225">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f95c0-226">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-226">The request will contain:</span></span>
        * <span data-ttu-id="f95c0-227">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-227">the package ID and version</span></span>
        * <span data-ttu-id="f95c0-228">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-228">the package source repository location</span></span>
        * <span data-ttu-id="f95c0-229">chemin d’accès au fichier de destination</span><span class="sxs-lookup"><span data-stu-id="f95c0-229">the destination file path</span></span>
    * <span data-ttu-id="f95c0-230">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-230">A response will contain:</span></span>
        * <span data-ttu-id="f95c0-231">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="f95c0-232">Récupérer les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="f95c0-232">Get credentials</span></span>
    * <span data-ttu-id="f95c0-233">Direction de la demande : plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="f95c0-234">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-234">The request will contain:</span></span>
        * <span data-ttu-id="f95c0-235">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-235">the package source repository location</span></span>
        * <span data-ttu-id="f95c0-236">code d’état HTTP obtenu à partir du référentiel source du package à l’aide des informations d’identification actuelles</span><span class="sxs-lookup"><span data-stu-id="f95c0-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="f95c0-237">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-237">A response will contain:</span></span>
        * <span data-ttu-id="f95c0-238">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f95c0-239">un nom d’utilisateur, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="f95c0-239">a username, if available</span></span>
        * <span data-ttu-id="f95c0-240">un mot de passe, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="f95c0-240">a password, if available</span></span>

5.  <span data-ttu-id="f95c0-241">Récupérer les fichiers dans le package</span><span class="sxs-lookup"><span data-stu-id="f95c0-241">Get files in package</span></span>
    * <span data-ttu-id="f95c0-242">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f95c0-243">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-243">The request will contain:</span></span>
        * <span data-ttu-id="f95c0-244">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-244">the package ID and version</span></span>
        * <span data-ttu-id="f95c0-245">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-245">the package source repository location</span></span>
    * <span data-ttu-id="f95c0-246">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-246">A response will contain:</span></span>
        * <span data-ttu-id="f95c0-247">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f95c0-248">énumérable de chemins d’accès de fichiers dans le package si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="f95c0-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="f95c0-249">Récupération des revendications d’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-249">Get operation claims</span></span> 
    * <span data-ttu-id="f95c0-250">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f95c0-251">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-251">The request will contain:</span></span>
        * <span data-ttu-id="f95c0-252">service index. JSON pour une source de package</span><span class="sxs-lookup"><span data-stu-id="f95c0-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="f95c0-253">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-253">the package source repository location</span></span>
    * <span data-ttu-id="f95c0-254">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-254">A response will contain:</span></span>
        * <span data-ttu-id="f95c0-255">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f95c0-256">énumérable des opérations prises en charge (par exemple, téléchargement de package) si l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="f95c0-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="f95c0-257">Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un ensemble vide d’opérations prises en charge.</span><span class="sxs-lookup"><span data-stu-id="f95c0-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="f95c0-258">Ce message a été mis à jour dans la version *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="f95c0-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="f95c0-259">Il se trouve sur le client pour préserver la compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="f95c0-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="f95c0-260">Obtient le hachage du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-260">Get package hash</span></span>
    * <span data-ttu-id="f95c0-261">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f95c0-262">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-262">The request will contain:</span></span>
        * <span data-ttu-id="f95c0-263">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-263">the package ID and version</span></span>
        * <span data-ttu-id="f95c0-264">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-264">the package source repository location</span></span>
        * <span data-ttu-id="f95c0-265">algorithme de hachage</span><span class="sxs-lookup"><span data-stu-id="f95c0-265">the hash algorithm</span></span>
    * <span data-ttu-id="f95c0-266">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-266">A response will contain:</span></span>
        * <span data-ttu-id="f95c0-267">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f95c0-268">hachage de fichier de package utilisant l’algorithme de hachage demandé si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="f95c0-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="f95c0-269">Obtenir des versions de packages</span><span class="sxs-lookup"><span data-stu-id="f95c0-269">Get package versions</span></span>
    * <span data-ttu-id="f95c0-270">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f95c0-271">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-271">The request will contain:</span></span>
        * <span data-ttu-id="f95c0-272">ID du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-272">the package ID</span></span>
        * <span data-ttu-id="f95c0-273">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-273">the package source repository location</span></span>
    * <span data-ttu-id="f95c0-274">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-274">A response will contain:</span></span>
        * <span data-ttu-id="f95c0-275">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f95c0-276">énumérable des versions de packages si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="f95c0-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="f95c0-277">Obtient l’index de service</span><span class="sxs-lookup"><span data-stu-id="f95c0-277">Get service index</span></span>
    * <span data-ttu-id="f95c0-278">Direction de la demande : plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="f95c0-279">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-279">The request will contain:</span></span>
        * <span data-ttu-id="f95c0-280">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-280">the package source repository location</span></span>
    * <span data-ttu-id="f95c0-281">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-281">A response will contain:</span></span>
        * <span data-ttu-id="f95c0-282">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f95c0-283">index du service si l’opération a réussi</span><span class="sxs-lookup"><span data-stu-id="f95c0-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="f95c0-284">Négociation</span><span class="sxs-lookup"><span data-stu-id="f95c0-284">Handshake</span></span>
     * <span data-ttu-id="f95c0-285">Direction de la demande : < NuGet-plug-in ></span><span class="sxs-lookup"><span data-stu-id="f95c0-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="f95c0-286">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-286">The request will contain:</span></span>
         * <span data-ttu-id="f95c0-287">version actuelle du protocole de plug-in</span><span class="sxs-lookup"><span data-stu-id="f95c0-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="f95c0-288">version de protocole du plug-in minimale prise en charge</span><span class="sxs-lookup"><span data-stu-id="f95c0-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="f95c0-289">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-289">A response will contain:</span></span>
         * <span data-ttu-id="f95c0-290">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="f95c0-291">version du protocole négocié si l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="f95c0-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="f95c0-292">Une défaillance entraînera l’arrêt du plug-in.</span><span class="sxs-lookup"><span data-stu-id="f95c0-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="f95c0-293">Initialiser</span><span class="sxs-lookup"><span data-stu-id="f95c0-293">Initialize</span></span>
     * <span data-ttu-id="f95c0-294">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f95c0-295">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-295">The request will contain:</span></span>
         * <span data-ttu-id="f95c0-296">version de l’outil client NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="f95c0-297">langage de l’outil client NuGet en vigueur.</span><span class="sxs-lookup"><span data-stu-id="f95c0-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="f95c0-298">Cela prend en compte le paramètre ForceEnglishOutput, s’il est utilisé.</span><span class="sxs-lookup"><span data-stu-id="f95c0-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="f95c0-299">délai d’expiration de la demande par défaut, qui remplace la valeur par défaut du protocole.</span><span class="sxs-lookup"><span data-stu-id="f95c0-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="f95c0-300">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-300">A response will contain:</span></span>
         * <span data-ttu-id="f95c0-301">Code de réponse indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="f95c0-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="f95c0-302">Une défaillance entraînera l’arrêt du plug-in.</span><span class="sxs-lookup"><span data-stu-id="f95c0-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="f95c0-303">Journal</span><span class="sxs-lookup"><span data-stu-id="f95c0-303">Log</span></span>
     * <span data-ttu-id="f95c0-304">Direction de la demande : plugin-> NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="f95c0-305">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-305">The request will contain:</span></span>
         * <span data-ttu-id="f95c0-306">niveau de journalisation de la demande</span><span class="sxs-lookup"><span data-stu-id="f95c0-306">the log level for the request</span></span>
         * <span data-ttu-id="f95c0-307">message à consigner</span><span class="sxs-lookup"><span data-stu-id="f95c0-307">a message to log</span></span>
     * <span data-ttu-id="f95c0-308">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-308">A response will contain:</span></span>
         * <span data-ttu-id="f95c0-309">Code de réponse indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="f95c0-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="f95c0-310">Surveiller la sortie du processus NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="f95c0-311">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f95c0-312">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-312">The request will contain:</span></span>
         * <span data-ttu-id="f95c0-313">l’ID de processus NuGet</span><span class="sxs-lookup"><span data-stu-id="f95c0-313">the NuGet process ID</span></span>
     * <span data-ttu-id="f95c0-314">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-314">A response will contain:</span></span>
         * <span data-ttu-id="f95c0-315">Code de réponse indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="f95c0-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="f95c0-316">Prérécupérer le package</span><span class="sxs-lookup"><span data-stu-id="f95c0-316">Prefetch package</span></span>
     * <span data-ttu-id="f95c0-317">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f95c0-318">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-318">The request will contain:</span></span>
         * <span data-ttu-id="f95c0-319">ID et version du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-319">the package ID and version</span></span>
         * <span data-ttu-id="f95c0-320">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-320">the package source repository location</span></span>
     * <span data-ttu-id="f95c0-321">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-321">A response will contain:</span></span>
         * <span data-ttu-id="f95c0-322">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="f95c0-323">Définition des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="f95c0-323">Set credentials</span></span>
     * <span data-ttu-id="f95c0-324">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f95c0-325">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-325">The request will contain:</span></span>
         * <span data-ttu-id="f95c0-326">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-326">the package source repository location</span></span>
         * <span data-ttu-id="f95c0-327">dernier nom d’utilisateur source de package connu, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="f95c0-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="f95c0-328">dernier mot de passe de source de package connu, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="f95c0-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="f95c0-329">dernier nom d’utilisateur du proxy connu, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="f95c0-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="f95c0-330">dernier mot de passe du proxy connu, s’il est disponible</span><span class="sxs-lookup"><span data-stu-id="f95c0-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="f95c0-331">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-331">A response will contain:</span></span>
         * <span data-ttu-id="f95c0-332">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="f95c0-333">Définir le niveau de journal</span><span class="sxs-lookup"><span data-stu-id="f95c0-333">Set log level</span></span>
     * <span data-ttu-id="f95c0-334">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f95c0-335">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-335">The request will contain:</span></span>
         * <span data-ttu-id="f95c0-336">niveau de journalisation par défaut</span><span class="sxs-lookup"><span data-stu-id="f95c0-336">the default log level</span></span>
     * <span data-ttu-id="f95c0-337">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-337">A response will contain:</span></span>
         * <span data-ttu-id="f95c0-338">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="f95c0-339">Messages du protocole version *2.0.0*</span><span class="sxs-lookup"><span data-stu-id="f95c0-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="f95c0-340">Récupération des revendications d’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-340">Get Operation Claims</span></span>

* <span data-ttu-id="f95c0-341">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f95c0-342">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-342">The request will contain:</span></span>
        * <span data-ttu-id="f95c0-343">service index. JSON pour une source de package</span><span class="sxs-lookup"><span data-stu-id="f95c0-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="f95c0-344">emplacement du référentiel source du package</span><span class="sxs-lookup"><span data-stu-id="f95c0-344">the package source repository location</span></span>
    * <span data-ttu-id="f95c0-345">Une réponse contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f95c0-345">A response will contain:</span></span>
        * <span data-ttu-id="f95c0-346">Code de réponse indiquant le résultat de l’opération</span><span class="sxs-lookup"><span data-stu-id="f95c0-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f95c0-347">énumérable des opérations prises en charge si l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="f95c0-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="f95c0-348">Si un plug-in ne prend pas en charge la source du package, le plug-in doit retourner un ensemble vide d’opérations prises en charge.</span><span class="sxs-lookup"><span data-stu-id="f95c0-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="f95c0-349">Si l’index de service et la source de package ont la valeur null, le plug-in peut répondre avec l’authentification.</span><span class="sxs-lookup"><span data-stu-id="f95c0-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="f95c0-350">Récupérer les informations d’identification d’authentification</span><span class="sxs-lookup"><span data-stu-id="f95c0-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="f95c0-351">Direction de la requête : plug-in NuGet-></span><span class="sxs-lookup"><span data-stu-id="f95c0-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="f95c0-352">La demande contient :</span><span class="sxs-lookup"><span data-stu-id="f95c0-352">The request will contain:</span></span>
    * <span data-ttu-id="f95c0-353">Uri</span><span class="sxs-lookup"><span data-stu-id="f95c0-353">Uri</span></span>
    * <span data-ttu-id="f95c0-354">IsRetry</span><span class="sxs-lookup"><span data-stu-id="f95c0-354">isRetry</span></span>
    * <span data-ttu-id="f95c0-355">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f95c0-355">NonInteractive</span></span>
    * <span data-ttu-id="f95c0-356">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="f95c0-356">CanShowDialog</span></span>
* <span data-ttu-id="f95c0-357">Une réponse contient</span><span class="sxs-lookup"><span data-stu-id="f95c0-357">A response will contain</span></span>
    * <span data-ttu-id="f95c0-358">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f95c0-358">Username</span></span>
    * <span data-ttu-id="f95c0-359">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="f95c0-359">Password</span></span>
    * <span data-ttu-id="f95c0-360">Message</span><span class="sxs-lookup"><span data-stu-id="f95c0-360">Message</span></span>
    * <span data-ttu-id="f95c0-361">Liste des types d’authentification</span><span class="sxs-lookup"><span data-stu-id="f95c0-361">List of Auth Types</span></span>
    * <span data-ttu-id="f95c0-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="f95c0-362">MessageResponseCode</span></span>
