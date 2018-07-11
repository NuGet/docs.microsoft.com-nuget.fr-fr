#### <a name="windows"></a><span data-ttu-id="59a4b-101">Windows</span><span class="sxs-lookup"><span data-stu-id="59a4b-101">Windows</span></span>

1. <span data-ttu-id="59a4b-102">Visitez [nuget.org/downloads](https://nuget.org/downloads) et sélectionnez NuGet 3.3 ou une version ultérieure (2.8.6 n’est pas compatible avec Mono).</span><span class="sxs-lookup"><span data-stu-id="59a4b-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="59a4b-103">La version la plus récente est toujours recommandée, et 4.1.0 ou une version ultérieure est requise pour publier des packages sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="59a4b-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="59a4b-104">Chaque téléchargement est le fichier `nuget.exe` directement.</span><span class="sxs-lookup"><span data-stu-id="59a4b-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="59a4b-105">Demandez à votre navigateur d’enregistrer le fichier dans un dossier de votre choix.</span><span class="sxs-lookup"><span data-stu-id="59a4b-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="59a4b-106">Le fichier n’est *pas* un programme d’installation ; vous ne verrez rien si vous l’exécutez directement à partir du navigateur.</span><span class="sxs-lookup"><span data-stu-id="59a4b-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="59a4b-107">Ajouter le dossier où vous avez placé `nuget.exe` à votre variable d’environnement PATH pour utiliser l’outil d’interface CLI à partir de n’importe quel endroit.</span><span class="sxs-lookup"><span data-stu-id="59a4b-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="59a4b-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="59a4b-108">macOS/Linux</span></span>

<span data-ttu-id="59a4b-109">Les comportements peuvent varier légèrement en fonction de la distribution du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="59a4b-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="59a4b-110">Installez [Mono 4.4.2 ou une version ultérieure](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="59a4b-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="59a4b-111">Tapez la commande suivante à l'invite de l’interpréteur de commandes :</span><span class="sxs-lookup"><span data-stu-id="59a4b-111">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="59a4b-112">Créez un alias en ajoutant le script suivant dans le fichier approprié de votre système d’exploitation (généralement `~/.bash_aliases` ou `~/.bash_profile`) :</span><span class="sxs-lookup"><span data-stu-id="59a4b-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="59a4b-113">Rechargez l’interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="59a4b-113">Reload the shell.</span></span>  <span data-ttu-id="59a4b-114">Testez l’installation en entrant `nuget` sans paramètres.</span><span class="sxs-lookup"><span data-stu-id="59a4b-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="59a4b-115">L’aide de l’interface de ligne de commande NuGet CLI doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="59a4b-115">NuGet CLI help should display.</span></span>
