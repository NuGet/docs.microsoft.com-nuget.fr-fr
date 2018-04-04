---
title: Problèmes connus dans NuGet | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Problèmes connus avec NuGet, notamment liés à l’authentification, à l’installation de package et aux outils.
keywords: problèmes connus NuGet, problèmes NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: c36da5dc73dddbd540a36d171583cbf542e0678f
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="8cb08-104">Problèmes connus avec NuGet</span><span class="sxs-lookup"><span data-stu-id="8cb08-104">Known Issues with NuGet</span></span>

<span data-ttu-id="8cb08-105">Voici les problèmes connus avec NuGet les plus couramment signalés.</span><span class="sxs-lookup"><span data-stu-id="8cb08-105">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="8cb08-106">Si vous avez des difficultés à installer NuGet ou à gérer des packages, consultez cette liste de problèmes connus et leur résolution.</span><span class="sxs-lookup"><span data-stu-id="8cb08-106">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="8cb08-107">À compter de NuGet 4.0, les problèmes connus font partie des notes de publication respectives.</span><span class="sxs-lookup"><span data-stu-id="8cb08-107">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="8cb08-108">Problèmes d’authentification avec les flux NuGet dans VSTS avec nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="8cb08-108">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="8cb08-109">**Problème :**</span><span class="sxs-lookup"><span data-stu-id="8cb08-109">**Problem:**</span></span>

<span data-ttu-id="8cb08-110">Quand vous utilisez la commande suivante pour stocker les informations d’identification, le jeton d’accès personnel est doublement chiffré.</span><span class="sxs-lookup"><span data-stu-id="8cb08-110">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="8cb08-111">$PAT = « Votre jeton d’accès personnel » $Feed =« Votre url » .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="8cb08-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="8cb08-112">**Solution de contournement :**</span><span class="sxs-lookup"><span data-stu-id="8cb08-112">**Workaround:**</span></span>

<span data-ttu-id="8cb08-113">Stockez les mots de passe en texte clair à l’aide de l’option [-StorePasswordInClearText](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="8cb08-113">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="8cb08-114">Erreur d’installation de packages avec NuGet 3.4, 3.4.1</span><span class="sxs-lookup"><span data-stu-id="8cb08-114">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="8cb08-115">**Problème :**</span><span class="sxs-lookup"><span data-stu-id="8cb08-115">**Problem:**</span></span>

<span data-ttu-id="8cb08-116">Dans NuGet 3.4 et 3.4.1, quand vous utilisez le complément NuGet, aucune source n’est signalée comme étant disponible et vous ne pouvez pas ajouter de nouvelles sources dans la fenêtre de configuration.</span><span class="sxs-lookup"><span data-stu-id="8cb08-116">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="8cb08-117">Le résultat est similaire à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8cb08-117">The result is similar to the image below:</span></span>

![Configuration de NuGet sans sources](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="8cb08-119">Le fichier `NuGet.Config` dans votre dossier `%AppData%\NuGet\` (Windows) ou `~/.nuget/` (Mac/Linux) a été vidé accidentellement.</span><span class="sxs-lookup"><span data-stu-id="8cb08-119">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="8cb08-120">Pour résoudre ce problème : Fermez Visual Studio (sur Windows, le cas échéant), supprimez le fichier `NuGet.Config`, puis recommencez l’opération.</span><span class="sxs-lookup"><span data-stu-id="8cb08-120">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="8cb08-121">NuGet génère un nouveau fichier `NuGet.Config` et vous devez pouvoir continuer.</span><span class="sxs-lookup"><span data-stu-id="8cb08-121">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="8cb08-122">Erreur d’installation de packages avec NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="8cb08-122">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="8cb08-123">**Problème :**</span><span class="sxs-lookup"><span data-stu-id="8cb08-123">**Problem:**</span></span>

<span data-ttu-id="8cb08-124">Dans NuGet 2.7 ou version ultérieure, quand vous tentez d’installer un package qui contient des références d’assembly, vous pouvez recevoir le message d’erreur **« Le format de la chaîne d’entrée est incorrect. »** , comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8cb08-124">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

<span data-ttu-id="8cb08-125">Cela est dû au fait que la bibliothèque de types pour le composant COM `VSLangProj.dll` est désinscrite sur votre système.</span><span class="sxs-lookup"><span data-stu-id="8cb08-125">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="8cb08-126">Cela peut se produire par exemple quand vous avez deux versions de Visual Studio installées côte à côte, et que vous désinstallez l’ancienne version.</span><span class="sxs-lookup"><span data-stu-id="8cb08-126">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="8cb08-127">Cela peut annuler par inadvertance l’inscription de la bibliothèque COM ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8cb08-127">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="8cb08-128">**Solution :**</span><span class="sxs-lookup"><span data-stu-id="8cb08-128">**Solution:**:</span></span>

<span data-ttu-id="8cb08-129">Exécutez cette commande à partir d’une **invite de commandes avec élévation de privilèges** pour réinscrire la bibliothèque de types pour `VSLangProj.dll`.</span><span class="sxs-lookup"><span data-stu-id="8cb08-129">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="8cb08-130">Si la commande échoue, vérifiez si le fichier existe à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="8cb08-130">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="8cb08-131">Pour plus d’informations sur cette erreur, consultez cet [élément de travail](https://nuget.codeplex.com/workitem/3609 "Élément de travail 3609").</span><span class="sxs-lookup"><span data-stu-id="8cb08-131">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="8cb08-132">Échec de la build après la mise à jour de package dans Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="8cb08-132">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="8cb08-133">Le problème : vous utilisez Visual Studio 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="8cb08-133">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="8cb08-134">Lors de la mise à jour de packages NuGet, vous recevez ce message : « Un ou plusieurs packages n’ont pas pu être désinstallés complètement. »</span><span class="sxs-lookup"><span data-stu-id="8cb08-134">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="8cb08-135">et vous êtes invité à redémarrer Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8cb08-135">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="8cb08-136">Après le redémarrage de Visual Studio, vous obtenez des erreurs de build étranges.</span><span class="sxs-lookup"><span data-stu-id="8cb08-136">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="8cb08-137">Elles sont dues au fait que certains fichiers dans les anciens packages sont verrouillés par un processus MSBuild en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="8cb08-137">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="8cb08-138">Même après le redémarrage de Visual Studio, le processus MSBuild en arrière-plan utilise toujours les fichiers des anciens packages, ce qui provoque les échecs de build.</span><span class="sxs-lookup"><span data-stu-id="8cb08-138">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="8cb08-139">La solution consiste à installer une mise à jour de Visual Studio 2012, par exemple Visual Studio 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="8cb08-139">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="8cb08-140">La mise à niveau vers la version la plus récente de NuGet à partir d’une version plus ancienne provoque une erreur de vérification de signature</span><span class="sxs-lookup"><span data-stu-id="8cb08-140">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="8cb08-141">Si vous exécutez Visual Studio 2010 SP1, vous pouvez recevoir le message d’erreur suivant quand vous tentez de mettre à niveau NuGet si une version plus ancienne est installée.</span><span class="sxs-lookup"><span data-stu-id="8cb08-141">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Programme d’installation d’extension Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="8cb08-143">Quand vous affichez les journaux, vous pouvez remarquer la présence d’une exception `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="8cb08-143">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="8cb08-144">Pour éviter ce problème, vous pouvez installer un [correctif logiciel pour Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) .</span><span class="sxs-lookup"><span data-stu-id="8cb08-144">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="8cb08-145">Une autre solution de contournement consiste à désinstaller simplement NuGet (pendant que vous exécutez Visual Studio en tant qu’administrateur) puis à l’installer à partir de la galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8cb08-145">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="8cb08-146">Pour plus d’informations, consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="8cb08-146">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="8cb08-147">La console du Gestionnaire de package lève une exception quand le complément Reflector de Visual Studio est également installé.</span><span class="sxs-lookup"><span data-stu-id="8cb08-147">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="8cb08-148">Lors de l’exécution de la console du Gestionnaire de Package, vous pouvez recevoir le message d’exception suivant si le complément Reflector de Visual Studio est installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8cb08-148">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="8cb08-149">ou</span><span class="sxs-lookup"><span data-stu-id="8cb08-149">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="8cb08-150">Nous avons contacté l’auteur du complément dans l’espoir de trouver une solution.</span><span class="sxs-lookup"><span data-stu-id="8cb08-150">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="8cb08-151">Mise à jour : Nous avons confirmé que la dernière version de Reflector, 6.5, ne provoquait plus cette exception dans la console.</span><span class="sxs-lookup"><span data-stu-id="8cb08-151">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="8cb08-152">L’ouverture de la console du Gestionnaire de package échoue avec l’exception ObjectSecurity</span><span class="sxs-lookup"><span data-stu-id="8cb08-152">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="8cb08-153">Ces erreurs peuvent s’afficher quand vous essayez d’ouvrir la console du Gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="8cb08-153">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="8cb08-154">Dans ce cas, suivez la solution [présentée sur StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="8cb08-154">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="8cb08-155">La boîte de dialogue Ajouter une référence de bibliothèque de packages lève une exception si la solution contient un projet InstallShield Limited Edition</span><span class="sxs-lookup"><span data-stu-id="8cb08-155">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="8cb08-156">Si votre solution contient un ou plusieurs projets InstallShield Limited Edition, la boîte de dialogue **Ajouter une référence de bibliothèque de packages** lève une exception lors de l’ouverture.</span><span class="sxs-lookup"><span data-stu-id="8cb08-156">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="8cb08-157">Il n’existe actuellement aucune solution de contournement, hormis la suppression ou le déchargement des projets InstallShield.</span><span class="sxs-lookup"><span data-stu-id="8cb08-157">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="8cb08-158">Bouton Désinstaller grisé ?</span><span class="sxs-lookup"><span data-stu-id="8cb08-158">Uninstall Button Greyed out?</span></span> <span data-ttu-id="8cb08-159">NuGet nécessite des privilèges d’administrateur pour installer ou désinstaller</span><span class="sxs-lookup"><span data-stu-id="8cb08-159">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="8cb08-160">Si vous essayez de désinstaller NuGet par le biais du Gestionnaire d’extensions Visual Studio, vous pouvez remarquer que le bouton Désinstaller est désactivé.</span><span class="sxs-lookup"><span data-stu-id="8cb08-160">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="8cb08-161">NuGet nécessite un accès administrateur pour installer et désinstaller.</span><span class="sxs-lookup"><span data-stu-id="8cb08-161">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="8cb08-162">Redémarrez Visual Studio en tant qu’administrateur pour désinstaller l’extension.</span><span class="sxs-lookup"><span data-stu-id="8cb08-162">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="8cb08-163">L’utilisation de NuGet ne nécessite pas d’accès administrateur.</span><span class="sxs-lookup"><span data-stu-id="8cb08-163">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="8cb08-164">La console du Gestionnaire de package se bloque quand je l’ouvre dans Windows XP.</span><span class="sxs-lookup"><span data-stu-id="8cb08-164">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="8cb08-165">Quel est le problème ?</span><span class="sxs-lookup"><span data-stu-id="8cb08-165">What's wrong?</span></span>

<span data-ttu-id="8cb08-166">NuGet nécessite le runtime Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="8cb08-166">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="8cb08-167">Windows XP, par défaut, ne dispose pas de Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="8cb08-167">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="8cb08-168">Vous pouvez télécharger le runtime Powershell 2.0 à partir de [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="8cb08-168">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="8cb08-169">Après l’installation, redémarrez Visual Studio. Vous devriez pouvoir ouvrir la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="8cb08-169">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="8cb08-170">Visual Studio 2010 SP1 bêta se bloque lors de sa fermeture si la console du Gestionnaire de package est ouverte.</span><span class="sxs-lookup"><span data-stu-id="8cb08-170">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="8cb08-171">Si vous avez installé Visual Studio 2010 SP1 bêta, vous pouvez remarquer que si vous laissez la console du Gestionnaire de package ouverte et que vous fermez Visual Studio, il se bloque.</span><span class="sxs-lookup"><span data-stu-id="8cb08-171">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="8cb08-172">Il s’agit d’un problème connu dans Visual Studio. Il sera résolu dans la version SP1 RTM.</span><span class="sxs-lookup"><span data-stu-id="8cb08-172">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="8cb08-173">Pour le moment, ignorez simplement l’incident ou désinstallez SP1 bêta, si vous le pouvez.</span><span class="sxs-lookup"><span data-stu-id="8cb08-173">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="8cb08-174">L’exception « L’élément 'metadata'... a un élément enfant non valide » se produit</span><span class="sxs-lookup"><span data-stu-id="8cb08-174">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="8cb08-175">Si vous avez installé des packages créés avec une préversion de NuGet, vous pouvez recevoir un message d’erreur indiquant que « L’élément 'metadata' dans l’espace de noms 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' a un élément enfant non valide » quand vous exécutez la version RTM de NuGet avec ce projet.</span><span class="sxs-lookup"><span data-stu-id="8cb08-175">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="8cb08-176">Vous devez désinstaller puis réinstaller chaque package à l’aide de la version RTM de NuGet.</span><span class="sxs-lookup"><span data-stu-id="8cb08-176">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="8cb08-177">Une tentative d’installation ou de désinstallation provoque l’erreur « Impossible de créer un fichier lorsque ce fichier existe déjà. »</span><span class="sxs-lookup"><span data-stu-id="8cb08-177">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="8cb08-178">Pour une raison quelconque, les extensions Visual Studio peuvent basculer dans un état étrange quand vous avez désinstallé l’extension VSIX mais que certains fichiers ont été conservés.</span><span class="sxs-lookup"><span data-stu-id="8cb08-178">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="8cb08-179">Pour contourner ce problème, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8cb08-179">To work around this issue:</span></span>

1. <span data-ttu-id="8cb08-180">Quitter Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8cb08-180">Exit Visual Studio</span></span>
1. <span data-ttu-id="8cb08-181">Ouvrez le dossier suivant (il peut être sur un lecteur différent sur votre ordinateur) :</span><span class="sxs-lookup"><span data-stu-id="8cb08-181">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="8cb08-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span><span class="sxs-lookup"><span data-stu-id="8cb08-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="8cb08-183">Supprimez tous les fichiers avec l’extension *.deleteme*.</span><span class="sxs-lookup"><span data-stu-id="8cb08-183">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="8cb08-184">Rouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8cb08-184">Re-open Visual Studio</span></span>

<span data-ttu-id="8cb08-185">Après avoir suivi ces étapes, vous devriez pouvoir continuer.</span><span class="sxs-lookup"><span data-stu-id="8cb08-185">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="8cb08-186">Dans de rares cas, la compilation avec Analyse du code activée provoque une erreur</span><span class="sxs-lookup"><span data-stu-id="8cb08-186">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="8cb08-187">Vous pouvez recevoir l’erreur suivante si vous installez FluentNHibernate avec la console du Gestionnaire de package et que vous compilez ensuite votre projet avec l’option « Analyse du code » activée.</span><span class="sxs-lookup"><span data-stu-id="8cb08-187">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="8cb08-188">Par défaut, FluentNHibernate nécessite NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="8cb08-188">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="8cb08-189">Toutefois, par défaut NuGet installe NHibernate 3.0.0.4000 dans votre projet et ajoute les redirections de liaison appropriées pour qu’il fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8cb08-189">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="8cb08-190">Votre projet sera compilé correctement si l’analyse du code n’est pas activée.</span><span class="sxs-lookup"><span data-stu-id="8cb08-190">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="8cb08-191">Contrairement au compilateur, l’outil d’analyse du code ne suit pas correctement les redirections de liaison pour utiliser 3.0.0.4000 au lieu de 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="8cb08-191">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="8cb08-192">Vous pouvez contourner le problème en installant NHibernate 3.0.0.2001 ou en indiquant à l’outil d’analyse du code qu’il se comporte comme le compilateur en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="8cb08-192">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="8cb08-193">Accédez à *%PROGRAMFILES%\Microsoft Visual Studio 10. 0\Team Tools\Static Analysis Tools\FxCop*.</span><span class="sxs-lookup"><span data-stu-id="8cb08-193">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="8cb08-194">Ouvrez FxCopCmd.exe.config et modifiez `AssemblyReferenceResolveMode` de `StrongName` en `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="8cb08-194">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="8cb08-195">Enregistrez les modifications et régénérez votre projet.</span><span class="sxs-lookup"><span data-stu-id="8cb08-195">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="8cb08-196">La commande Write-Error ne fonctionne pas dans install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="8cb08-196">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="8cb08-197">Il s'agit d'un problème connu.</span><span class="sxs-lookup"><span data-stu-id="8cb08-197">This is a known issue.</span></span> <span data-ttu-id="8cb08-198">Au lieu d’appeler Write-Error, essayez d’appeler throw.</span><span class="sxs-lookup"><span data-stu-id="8cb08-198">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="8cb08-199">L’installation de NuGet avec accès restreint sur Windows 2003 peut provoquer le blocage de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8cb08-199">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="8cb08-200">Quand vous tentez d’installer NuGet à l’aide du Gestionnaire d’extensions Visual Studio et que vous ne l’exécutez pas en tant qu’administrateur, la boîte de dialogue « Exécuter en tant que » s’affiche avec la case « Exécuter ce programme avec un accès restreint » cochée par défaut.</span><span class="sxs-lookup"><span data-stu-id="8cb08-200">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Boîte de dialogue Exécuter en tant que](./media/RunAsRestricted.png)

<span data-ttu-id="8cb08-202">Si cette case est cochée et que vous cliquez sur OK, Visual Studio se bloque.</span><span class="sxs-lookup"><span data-stu-id="8cb08-202">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="8cb08-203">Veillez à désactiver cette option avant d’installer NuGet.</span><span class="sxs-lookup"><span data-stu-id="8cb08-203">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="8cb08-204">Impossible de désinstaller NuGet pour les Outils Windows Phone</span><span class="sxs-lookup"><span data-stu-id="8cb08-204">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="8cb08-205">Les Outils Windows Phone ne prennent pas en charge le Gestionnaire d’extensions de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8cb08-205">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="8cb08-206">Pour désinstaller NuGet, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="8cb08-206">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="8cb08-207">La modification de la casse des ID de packages NuGet interrompt la restauration des packages</span><span class="sxs-lookup"><span data-stu-id="8cb08-207">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="8cb08-208">Comme l’explique en détail [ce problème GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), la modification de la mise en majuscules de packages NuGet peut être effectuée par le support NuGet, mais elle provoque des complications lors de la restauration de package pour les utilisateurs dont le dossier *global-packages* contient déjà des packages à la casse différente.</span><span class="sxs-lookup"><span data-stu-id="8cb08-208">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="8cb08-209">Nous vous recommandons de demander un changement de casse uniquement quand vous avez la possibilité d’informer les utilisateurs de votre package de la rupture susceptible de se produire lors de la restauration des packages au moment de la build.</span><span class="sxs-lookup"><span data-stu-id="8cb08-209">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="8cb08-210">Problèmes liés aux rapports</span><span class="sxs-lookup"><span data-stu-id="8cb08-210">Reporting issues</span></span>

<span data-ttu-id="8cb08-211">Pour signaler des problèmes liés à NuGet, visitez [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="8cb08-211">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
