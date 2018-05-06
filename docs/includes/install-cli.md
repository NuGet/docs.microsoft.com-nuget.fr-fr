#### <a name="windows"></a>Windows

1. Visitez [nuget.org/downloads](https://nuget.org/downloads) et sélectionnez NuGet 3.3 ou une version ultérieure (2.8.6 n’est pas compatible avec Mono). La version la plus récente est toujours recommandée, et 4.1.0 ou une version ultérieure est requise pour publier des packages sur nuget.org.
1. Chaque téléchargement est le fichier `nuget.exe` directement. Demandez à votre navigateur d’enregistrer le fichier dans un dossier de votre choix. Le fichier n’est *pas* un programme d’installation ; vous ne verrez rien si vous l’exécutez directement à partir du navigateur.
1. Ajouter le dossier où vous avez placé `nuget.exe` à votre variable d’environnement PATH pour utiliser l’outil d’interface CLI à partir de n’importe quel endroit.

#### <a name="macoslinux"></a>macOS/Linux

Les comportements peuvent varier légèrement en fonction de la distribution du système d’exploitation.

1. Installez [Mono 4.4.2 ou une version ultérieure](http://www.mono-project.com/docs/getting-started/install/).

1. Tapez les commandes suivante à l'invite de l’interpréteur de commandes :

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```

1. Créez un alias en ajoutant le script suivant dans le fichier approprié de votre système d’exploitation (généralement `~/.bash_aliases` ou `~/.bash_profile`) :

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Rechargez l’interpréteur de commandes.  Testez l’installation en entrant `nuget` sans paramètres. L’aide de l’interface de ligne de commande NuGet CLI doit s’afficher.