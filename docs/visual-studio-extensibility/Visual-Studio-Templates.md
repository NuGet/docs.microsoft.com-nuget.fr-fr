---
title: "Packages NuGet dans les modèles Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/03/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Instructions pour inclure des packages NuGet dans des modèles de projet et d’élément Visual Studio."
keywords: "NuGet dans Visual Studio, modèles de projet Visual Studio, modèles d’élément Visual Studio, packages dans des modèles de projet, packages dans des modèles d’élément"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 65b914e1fa59c28615f195b470880a12bf80efbb
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="packages-in-visual-studio-templates"></a>Packages dans des modèles Visual Studio

Les modèles de projet et d’élément Visual Studio doivent souvent vérifier que certains packages y sont installés lors de la création d’un projet ou d’un élément. Par exemple, le modèle ASP.NET MVC 3 installe jQuery, Modernizr et d’autres packages.

Pour la prise en charge de cette contrainte, les créateurs de modèle peuvent indiquer à NuGet d’installer les packages nécessaires, au lieu de bibliothèques individuelles. Les développeurs peuvent ensuite facilement mettre à jour ces packages à tout moment.

Pour en savoir plus sur la création des modèles eux-mêmes, reportez-vous à [Guide pratique pour créer des modèles de projet](/visualstudio/ide/how-to-create-project-templates) ou à [Création de modèles de projet et d’élément personnalisés](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Le reste de cette section décrit les étapes spécifiques à effectuer lors de la création d’un modèle pour inclure correctement des packages NuGet.

- [Ajout de packages à un modèle](#adding-packages-to-a-template)
- [Bonnes pratiques](#best-practices)

Pour obtenir un exemple, consultez [l’exemple NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Ajout de packages à un modèle

Quand un modèle est instancié, un [Assistant Modèle](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) est appelé pour charger la liste des packages à installer, ainsi que des informations sur l’emplacement où rechercher ces packages. Les packages peuvent être incorporés dans l’extension VSIX, incorporés dans le modèle ou situés sur le disque dur local, auquel cas vous utilisez une clé de Registre pour référencer le chemin de fichier. Vous pouvez trouver plus d’informations sur ces emplacements plus loin dans cette section.

Les packages préinstallés fonctionnent avec des [Assistants Modèle](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Un Assistant spécial est appelé quand le modèle est instancié. L’Assistant charge la liste des packages qui doivent être installés et passe ces informations aux API NuGet appropriées.

Étapes pour inclure des packages dans un modèle :

1. Dans votre fichier `vstemplate`, ajoutez une référence à l’Assistant Modèle NuGet en ajoutant un élément [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) :

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` est un assembly contenant seulement la classe `TemplateWizard`, qui est un simple wrapper qui effectue un appel dans l’implémentation actuelle de `NuGet.VisualStudio.dll`. La version de l’assembly ne change jamais : les modèles de projet/élément continuent donc de fonctionner avec les nouvelles versions de NuGet.

1. Ajoutez la liste des packages à installer dans le projet :

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    *(NuGet 2.2.1+)*  L’Assistant prend en charge plusieurs éléments `<package>`, ce qui permet la prise en charge de plusieurs sources de packages. Les attributs `id` et `version` sont tous deux obligatoires, ce qui signifie qu’une version spécifique d’un package est installée même si une version plus récente est disponible. Ceci évite que les mises à jour des packages ne compromettent le bon fonctionnement du modèle, en laissant au développeur la possibilité de mettre à jour le package avec le modèle.

1. Spécifiez le référentiel où NuGet peut trouver les packages, comme décrit dans les sections suivantes.

### <a name="vsix-package-repository"></a>Référentiel de packages VSIX

L’approche recommandée du déploiement pour les modèles de projet/élément Visual Studio est une [extension VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions), car elle vous permet de placer ensemble dans un package plusieurs modèles de projet/élément, et permet aux développeurs de découvrir facilement vos modèles avec le Gestionnaire d’extensions Visual Studio ou avec la galerie Visual Studio. Les mises à jour de l’extension sont également faciles à déployer avec le [mécanisme de mise à jour automatique du Gestionnaire d’extensions Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

L’extension VSIX elle-même peut être utilisée comme source pour les packages nécessaires au modèle :

1. Modifiez l’élément `<packages>` dans le fichier `.vstemplate` comme suit :

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    L’attribut `repository` spécifie le type de référentiel comme étant `extension`, tandis que `repositoryId` est l’identificateur unique de l’extension VSIX elle-même (c’est la valeur de l’attribut `ID` dans le fichier `vsixmanifest` de l’extension, voir [Informations de référence sur l’extension VSIX avec un schéma 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Placez vos fichiers `nupkg` dans un dossier nommé `Packages` au sein de l’extension VSIX.

1. Ajoutez les fichiers de package nécessaires comme `<Asset>` dans votre fichier `vsixmanifest` (voir [Informations de référence sur l’extension VSIX avec un schéma 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)) :

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Notez que vous pouvez distribuer des packages dans la même extension VSIX que vos modèles de projet, ou les placer dans une extension VSIX distincte si c’est plus approprié pour votre scénario. Ne référencez cependant aucune extension VSIX dont vous n’avez pas le contrôle, car les modifications apportées à cette extension peuvent compromettre le bon fonctionnement de votre modèle.

### <a name="template-package-repository"></a>Référentiel de packages de modèles

Si vous distribuez un seul modèle de projet/élément et que vous n’avez pas besoin de placer plusieurs modèles dans un package, vous pouvez utiliser une approche plus simple mais plus limitée, qui inclut des packages directement dans le fichier ZIP du modèle de projet/élément :

1. Modifiez l’élément `<packages>` dans le fichier `.vstemplate` comme suit :

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    L’attribut `repository` a la valeur `template` et l’attribut `repositoryId` n’est pas nécessaire.

1. Placez les packages dans le dossier racine du fichier ZIP du modèle de projet/élément.

Notez que l’utilisation de cette approche dans une extension VSIX qui contient plusieurs modèles aboutit à un encombrement inutile quand un ou plusieurs packages sont communs aux modèles. Dans ce cas, utilisez [l’extension VSIX comme référentiel](#vsix-package-repository), comme décrit dans la section précédente.

### <a name="registry-specified-folder-path"></a>Chemin de dossier spécifié dans le Registre

Les SDK qui sont installés avec un fichier MSI peuvent installer des packages NuGet directement sur l’ordinateur du développeur. Ceci les rend immédiatement disponibles quand un modèle de projet ou un élément est utilisé, au lieu d’obliger à les extraire à ce moment-là. Les modèles ASP.NET utilisent cette approche.

1. Faites en sorte que le fichier MSI installe les packages sur l’ordinateur. Vous pouvez installer seulement les fichiers `.nupkg`, ou vous pouvez les installer en même temps que le contenu développé, ce qui vous épargne une étape supplémentaire quand le modèle est utilisé. Dans ce cas, suivez la structure de dossiers standard de NuGet, où les fichiers `.nupkg` se trouvent dans le dossier racine, chaque package ayant un sous-dossier dont le nom correspond à la paire ID/version.

1. Écrivez une clé de Registre pour identifier l’emplacement du package :

    - Emplacement de la clé : une clé `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` à l’échelle de l’ordinateur. S’il s’agit de modèles et de packages installés au niveau de l’utilisateur, vous pouvez également utiliser `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Nom de la clé : utilisez un nom qui est unique pour vous. Par exemple, les modèles ASP.NET MVC 4 pour Visual Studio 2012 utilisent `AspNetMvc4VS11`.
    - Valeurs : le chemin complet du dossier des packages.

1. Dans l’élément `<packages>` du fichier `.vstemplate`, ajoutez l’attribut `repository="registry"` et spécifiez le nom de votre clé de Registre dans l’attribut `keyName`.

    - Si vous avez déjà décompressé vos packages, utilisez l’attribut `isPreunzipped="true"`.
    - *(NuGet 3.2 +)*  Si vous voulez forcer une build au moment du design à la fin de l’installation du package, ajoutez l’attribut `forceDesignTimeBuild="true"`.
    - À titre d’optimisation, ajoutez `skipAssemblyReferences="true"`, car le modèle lui-même inclut déjà les références nécessaires.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Meilleures pratiques

1. Déclarez une dépendance sur l’extension VSIX NuGet en ajoutant une référence à celle-ci dans votre manifeste VSIX :

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Forcez l’enregistrement des modèles de projet/élément lors de la création en ajoutant [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) dans le fichier `.vstemplate`.

1. Les modèles ne comportent pas de fichier `packages.config` ; n’incluez aucune référence ni aucun contenu qui serait ajouté lors de l’installation des packages NuGet.
