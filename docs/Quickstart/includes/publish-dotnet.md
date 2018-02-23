1. Accédez au dossier contenant le fichier `.nupkg`.

1. Exécutez la commande suivante, en spécifiant le nom de votre package et en remplaçant la valeur de la clé par celle de votre clé API :

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. dotnet affiche les résultats du processus de publication :

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

Voir [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).