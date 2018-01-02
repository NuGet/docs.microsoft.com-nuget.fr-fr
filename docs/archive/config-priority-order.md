### <a name="priority-ordering"></a>Ordre de priorité

Il peut également être utile de réfléchir à l’ordre de priorité dans lequel les paramètres sont appliqués, qui est généralement contraire à l’ordre de traitement. Par exemple, si un projet se trouve dans `c:\A\B\C`, NuGet applique les paramètres dans l’ordre de priorité suivant, où les paramètres qui se trouvent en haut de la liste sont prioritaires :

    (For solution-level packages only in NuGet 2.x; ignored in NuGet 3.x)
    c:\A\B\C\.nuget\NuGet.Config

    (For all version of NuGet)
    c:\A\B\C\NuGet.Config
    c:\A\B\NuGet.Config
    c:\A\NuGet.Config
    c:\NuGet.Config

    configFile, if specified

    (Ignored in NuGet 3.4 and later if -configFile is used)
    %AppData%\NuGet\NuGet.Config

    (NuGet 2.6 to 3.5)
    %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\NuGet.Config
    %ProgramData%\NuGet\Config\{IDE}\{Version}\NuGet.Config
    %ProgramData%\NuGet\Config\{IDE}\NuGet.Config
    %ProgramData%\NuGet\Config\NuGet.Config

    (NuGet 4.0+)
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\{Version}\{SKU}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\{Version}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\NuGet.Config