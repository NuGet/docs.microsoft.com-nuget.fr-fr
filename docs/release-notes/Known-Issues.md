---
title: Problèmes connus
description: Problèmes connus avec NuGet, notamment liés à l’authentification, à l’installation de package et aux outils.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b104eb39ddeacd9ca1ea45937cf98ad57531112a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317145"
---
# <a name="known-issues-with-nuget"></a>Problèmes connus avec NuGet

Voici les problèmes connus avec NuGet les plus couramment signalés. Si vous avez des difficultés à installer NuGet ou à gérer des packages, consultez cette liste de problèmes connus et leur résolution.

> [!Note]
> À compter de NuGet 4.0, les problèmes connus font partie des notes de publication respectives.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problèmes d’authentification avec les flux NuGet dans VSTS avec nuget.exe v3.4.3

**Problème :**

Quand vous utilisez la commande suivante pour stocker les informations d’identification, le jeton d’accès personnel est doublement chiffré.

$PAT = « Votre jeton d’accès personnel » $Feed =« Votre url » .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT

**Solution de contournement :**

Stockez les mots de passe en texte clair à l’aide de l’option [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md).

## <a name="error-installing-packages-with-nuget-34-341"></a>Erreur d’installation de packages avec NuGet 3.4, 3.4.1

**Problème :**

Dans NuGet 3.4 et 3.4.1, quand vous utilisez le complément NuGet, aucune source n’est signalée comme étant disponible et vous ne pouvez pas ajouter de nouvelles sources dans la fenêtre de configuration. Le résultat est similaire à l’image ci-dessous :

![Configuration de NuGet sans sources](./media/knownIssue-34-NoSources.PNG)

Le fichier `NuGet.Config` dans votre dossier `%AppData%\NuGet\` (Windows) ou `~/.nuget/` (Mac/Linux) a été vidé accidentellement. Pour résoudre ce problème : Fermez Visual Studio (sur Windows, le cas échéant), supprimez le fichier `NuGet.Config`, puis recommencez l’opération. NuGet génère un nouveau fichier `NuGet.Config` et vous devez pouvoir continuer.

## <a name="error-installing-packages-with-nuget-27"></a>Erreur d’installation de packages avec NuGet 2.7

**Problème :**

Dans NuGet 2.7 ou version ultérieure, quand vous tentez d’installer un package qui contient des références d’assembly, vous pouvez recevoir le message d’erreur **« Le format de la chaîne d’entrée est incorrect. »** , comme illustré ci-dessous :

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

Cela est dû au fait que la bibliothèque de types pour le composant COM `VSLangProj.dll` est désinscrite sur votre système. Cela peut se produire par exemple quand vous avez deux versions de Visual Studio installées côte à côte, et que vous désinstallez l’ancienne version. Cela peut annuler par inadvertance l’inscription de la bibliothèque COM ci-dessus.

**Solution :**

Exécutez cette commande à partir d’une **invite de commandes avec élévation de privilèges** pour réinscrire la bibliothèque de types pour `VSLangProj.dll`.

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Si la commande échoue, vérifiez si le fichier existe à cet emplacement.

Pour plus d’informations sur cette erreur, consultez cet [élément de travail](https://nuget.codeplex.com/workitem/3609 "Élément de travail 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Échec de la build après la mise à jour de package dans Visual Studio 2012

Problème : Vous utilisez Visual Studio 2012 RTM. Lors de la mise à jour des packages NuGet, vous recevez le message suivant : « Un ou plusieurs packages n’ont pas pu être désinstallés ». et vous êtes invité à redémarrer Visual Studio. Après le redémarrage de Visual Studio, vous obtenez des erreurs de build étranges.

Elles sont dues au fait que certains fichiers dans les anciens packages sont verrouillés par un processus MSBuild en arrière-plan. Même après le redémarrage de Visual Studio, le processus MSBuild en arrière-plan utilise toujours les fichiers des anciens packages, ce qui provoque les échecs de build.

La solution consiste à installer une mise à jour de Visual Studio 2012, par exemple Visual Studio 2012 Update 2.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>La mise à niveau vers la version la plus récente de NuGet à partir d’une version plus ancienne provoque une erreur de vérification de signature

Si vous exécutez Visual Studio 2010 SP1, vous pouvez recevoir le message d’erreur suivant quand vous tentez de mettre à niveau NuGet si une version plus ancienne est installée.

![Programme d’installation d’extension Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Quand vous affichez les journaux, vous pouvez remarquer la présence d’une exception `SignatureMismatchException`.

Pour éviter ce problème, vous pouvez installer un [correctif logiciel pour Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) .
Une autre solution de contournement consiste à désinstaller simplement NuGet (pendant que vous exécutez Visual Studio en tant qu’administrateur) puis à l’installer à partir de la galerie d’extensions Visual Studio.  Pour plus d’informations, consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>La console du Gestionnaire de package lève une exception quand le complément Reflector de Visual Studio est également installé.

Lors de l’exécution de la console du Gestionnaire de Package, vous pouvez recevoir le message d’exception suivant si le complément Reflector de Visual Studio est installé sur votre ordinateur.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

ou

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

Nous avons contacté l’auteur du complément dans l’espoir de trouver une solution.

<p class="info">Mise à jour : Nous avons vérifié que la dernière version de Reflector, 6.5, ne provoquait plus cette exception dans la console.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>L’ouverture de la console du Gestionnaire de package échoue avec l’exception ObjectSecurity

Ces erreurs peuvent s’afficher quand vous essayez d’ouvrir la console du Gestionnaire de package :

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Dans ce cas, suivez la solution [présentée sur StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) pour résoudre le problème.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>La boîte de dialogue Ajouter une référence de bibliothèque de packages lève une exception si la solution contient un projet InstallShield Limited Edition

Si votre solution contient un ou plusieurs projets InstallShield Limited Edition, la boîte de dialogue **Ajouter une référence de bibliothèque de packages** lève une exception lors de l’ouverture. Il n’existe actuellement aucune solution de contournement, hormis la suppression ou le déchargement des projets InstallShield.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Bouton Désinstaller grisé ? NuGet nécessite des privilèges d’administrateur pour installer ou désinstaller

Si vous essayez de désinstaller NuGet par le biais du Gestionnaire d’extensions Visual Studio, vous pouvez remarquer que le bouton Désinstaller est désactivé. NuGet nécessite un accès administrateur pour installer et désinstaller. Redémarrez Visual Studio en tant qu’administrateur pour désinstaller l’extension. L’utilisation de NuGet ne nécessite pas d’accès administrateur.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>La console du Gestionnaire de package se bloque quand je l’ouvre dans Windows XP. Quel est le problème ?

NuGet nécessite le runtime Powershell 2.0. Windows XP, par défaut, ne dispose pas de Powershell 2.0. Vous pouvez télécharger le runtime Powershell 2.0 à partir de [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929). Après l’installation, redémarrez Visual Studio. Vous devriez pouvoir ouvrir la console du Gestionnaire de package.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Visual Studio 2010 SP1 bêta se bloque lors de sa fermeture si la console du Gestionnaire de package est ouverte.

Si vous avez installé Visual Studio 2010 SP1 bêta, vous pouvez remarquer que si vous laissez la console du Gestionnaire de package ouverte et que vous fermez Visual Studio, il se bloque. Il s’agit d’un problème connu dans Visual Studio. Il sera résolu dans la version SP1 RTM. Pour le moment, ignorez simplement l’incident ou désinstallez SP1 bêta, si vous le pouvez.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>L’exception « L’élément 'metadata'... a un élément enfant non valide » se produit

Si vous avez installé des packages créés avec une préversion de NuGet, vous pouvez recevoir un message d’erreur indiquant que « L’élément 'metadata' dans l’espace de noms 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' a un élément enfant non valide » quand vous exécutez la version RTM de NuGet avec ce projet. Vous devez désinstaller puis réinstaller chaque package à l’aide de la version RTM de NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Une tentative d’installation ou de désinstallation provoque l’erreur « Impossible de créer un fichier lorsque ce fichier existe déjà. »

Pour une raison quelconque, les extensions Visual Studio peuvent basculer dans un état étrange quand vous avez désinstallé l’extension VSIX mais que certains fichiers ont été conservés. Pour contourner ce problème, procédez comme suit :

1. Quitter Visual Studio
1. Ouvrez le dossier suivant (il peut être sur un lecteur différent sur votre ordinateur) :

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. Supprimez tous les fichiers avec l’extension *.deleteme*.
1. Rouvrez Visual Studio.

Après avoir suivi ces étapes, vous devriez pouvoir continuer.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Dans de rares cas, la compilation avec Analyse du code activée provoque une erreur

Vous pouvez recevoir l’erreur suivante si vous installez FluentNHibernate avec la console du Gestionnaire de package et que vous compilez ensuite votre projet avec l’option « Analyse du code » activée.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Par défaut, FluentNHibernate nécessite NHibernate 3.0.0.2001. Toutefois, par défaut NuGet installe NHibernate 3.0.0.4000 dans votre projet et ajoute les redirections de liaison appropriées pour qu’il fonctionne. Votre projet sera compilé correctement si l’analyse du code n’est pas activée. Contrairement au compilateur, l’outil d’analyse du code ne suit pas correctement les redirections de liaison pour utiliser 3.0.0.4000 au lieu de 3.0.0.2001. Vous pouvez contourner le problème en installant NHibernate 3.0.0.2001 ou en indiquant à l’outil d’analyse du code qu’il se comporte comme le compilateur en procédant comme suit :

1. Accédez à *%PROGRAMFILES%\Microsoft Visual Studio 10. 0\Team Tools\Static Analysis Tools\FxCop*.
1. Ouvrez FxCopCmd.exe.config et modifiez `AssemblyReferenceResolveMode` de `StrongName` en `StrongNameIgnoringVersion`.
1. Enregistrez les modifications et régénérez votre projet.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>La commande Write-Error ne fonctionne pas dans install.ps1/uninstall.ps1/init.ps1

Il s'agit d'un problème connu. Au lieu d’appeler Write-Error, essayez d’appeler throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>L’installation de NuGet avec accès restreint sur Windows 2003 peut provoquer le blocage de Visual Studio

Quand vous tentez d’installer NuGet à l’aide du Gestionnaire d’extensions Visual Studio et que vous ne l’exécutez pas en tant qu’administrateur, la boîte de dialogue « Exécuter en tant que » s’affiche avec la case « Exécuter ce programme avec un accès restreint » cochée par défaut.

![Boîte de dialogue Exécuter en tant que](./media/RunAsRestricted.png)

Si cette case est cochée et que vous cliquez sur OK, Visual Studio se bloque. Veillez à désactiver cette option avant d’installer NuGet.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Impossible de désinstaller NuGet pour les Outils Windows Phone

Les Outils Windows Phone ne prennent pas en charge le Gestionnaire d’extensions de Visual Studio. Pour désinstaller NuGet, exécutez la commande suivante.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>La modification de la casse des ID de packages NuGet interrompt la restauration des packages

Comme l’explique en détail [ce problème GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), la modification de la mise en majuscules de packages NuGet peut être effectuée par le support NuGet, mais elle provoque des complications lors de la restauration de package pour les utilisateurs dont le dossier *global-packages* contient déjà des packages à la casse différente. Nous vous recommandons de demander un changement de casse uniquement quand vous avez la possibilité d’informer les utilisateurs de votre package de la rupture susceptible de se produire lors de la restauration des packages au moment de la build.

## <a name="reporting-issues"></a>Problèmes liés aux rapports

Pour signaler des problèmes liés à NuGet, visitez [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).
