#### <a name="windows"></a>Windows
1. Visitez [nuget.org/downloads](https://nuget.org/downloads) et sélectionnez NuGet 3.3 ou ultérieure (2.8.6 n’est pas compatible avec Mono). La version la plus récente est toujours recommandée et 4.1.0+ est requise pour publier des packages sur nuget.org.
2. Chaque téléchargement est le `nuget.exe` directement du fichier. Demandez à votre navigateur pour enregistrer le fichier dans un dossier de votre choix. Le fichier est *pas* un programme d’installation ; vous ne voyez rien si vous l’exécutez directement à partir du navigateur.
3. Ajouter le dossier où vous avez placé `nuget.exe` à votre variable d’environnement PATH pour utiliser l’outil d’interface CLI à partir de n’importe quel endroit.

#### <a name="macoslinux"></a>macOS/Linux
Comportements peuvent varier légèrement en distribution de système d’exploitation.

1. Installer [Mono 4.4.2 ou version ultérieure](http://www.mono-project.com/docs/getting-started/install/).
2. Exécutez les commandes suivantes à l’invite de shell :
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. Créer un alias en ajoutant le script suivant dans le fichier approprié pour votre système d’exploitation (généralement `~/.bash_aliases` ou `~/.bash_profile`) :
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. Recharger l’interpréteur de commandes.  Testez l’installation en entrant `nuget` sans paramètres. Aide de NuGet CLI doit s’afficher.