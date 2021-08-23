---
title: Meilleures pratiques pour une chaîne d’approvisionnement de logiciels sécurisée
description: meilleures pratiques pour sécuriser votre chaîne d’approvisionnement logiciel à l’aide de NuGet & GitHub.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726975"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Meilleures pratiques pour une chaîne d’approvisionnement de logiciels sécurisée

Open source est partout. Il se trouve dans de nombreux codes base et projets de la communauté. Pour les organisations et les particuliers, la question actuelle n’est pas de savoir si vous n’utilisez pas de code open source, mais aussi le code open source que vous utilisez et combien de temps.

Si vous n’avez pas conscience de ce qui se trouve dans votre chaîne d’approvisionnement logiciel, une vulnérabilité en amont dans l’une de vos dépendances peut être fatale, ce qui vous permet, ainsi qu’à vos clients, de compromettre la vulnérabilité. Dans ce document, nous étudierons plus en détail ce que signifie le terme « chaîne d’approvisionnement de logiciels », pourquoi il est important et comment vous pouvez contribuer à sécuriser la chaîne logistique de votre projet avec les meilleures pratiques.

![État du Octoverse 2020-Open source](media/opensource-percent.png)

## <a name="dependencies"></a>Les dépendances 

Le terme « chaîne d’approvisionnement logiciel » est utilisé pour faire référence à tout ce qui passe dans vos logiciels et à son origine. Il s’agit des dépendances et des propriétés de vos dépendances dont dépend votre chaîne d’approvisionnement logiciel. Une dépendance est ce que votre logiciel doit exécuter. Il peut s’agir de code, de fichiers binaires ou d’autres composants, et de leur provenance, tel qu’un référentiel ou un gestionnaire de package.

Il comprend qui a écrit le code, quand il a été contribué, comment il a été revu en termes de problèmes de sécurité, de vulnérabilités connues, de versions prises en charge, d’informations sur les licences et tout ce qui le touche à tout moment.

Votre chaîne d’approvisionnement englobe également d’autres parties de votre pile au-delà d’une seule application, par exemple vos scripts de création et d’empaquetage ou le logiciel qui exécute l’infrastructure sur laquelle votre application s’appuie.

## <a name="vulnerabilities"></a>Vulnérabilités

Aujourd’hui, les dépendances logicielles sont omniprésentes. Il est assez courant pour vos projets d’utiliser des centaines de dépendances Open source pour les fonctionnalités que vous n’avez pas besoin d’écrire vous-même. Cela peut signifier que la majeure partie de votre application se compose de code que vous n’avez pas créé. 

![État du Octoverse 2020-Dependencies](media/dependencies.png)

Les vulnérabilités possibles dans vos dépendances tierces ou open source, sont des dépendances présumées que vous ne pouvez pas contrôler aussi étroitement que le code que vous écrivez, ce qui peut créer des risques de sécurité potentiels dans votre chaîne d’approvisionnement.

Si l’une de ces dépendances a une vulnérabilité, il est probable que vous ayez une vulnérabilité. Cela peut être effrayant, car l’une de vos dépendances peut changer sans que vous sachiez même. Même si une vulnérabilité existe aujourd’hui dans une dépendance, mais n’est pas exploitable, elle peut être exploitée à l’avenir. 

La possibilité de tirer parti du travail des milliers de développeurs Open source et d’auteurs de bibliothèques signifie que des milliers de personnes peuvent contribuer efficacement à votre code de production. Votre produit, via votre chaîne d’approvisionnement logiciel, est affecté par des vulnérabilités non corrigées, des erreurs innocentes ou même des attaques malveillantes contre les dépendances.

## <a name="supply-chain-compromises"></a>Compromissions de la chaîne logistique

La définition traditionnelle d’une chaîne d’approvisionnement provient de la fabrication ; Il s’agit de la chaîne de processus requise pour créer et fournir un résultat. Il comprend la planification, l’approvisionnement des matériaux, la fabrication et la vente au détail. Une chaîne d’approvisionnement de logiciels est similaire, à l’exception de Materials, code. Au lieu de fabriquer, il s’agit du développement. Au lieu de plonger dans le sol, le code provient de fournisseurs, commerciaux ou open source et, en général, le code open source provient de dépôts. L’ajout de code à partir d’un référentiel signifie que votre produit est dépendant de ce code.

Par exemple, une attaque par chaîne d’approvisionnement logiciel se produit lorsque du code malveillant est volontairement ajouté à une dépendance, à l’aide de la chaîne d’approvisionnement de cette dépendance pour distribuer le code à ses victimes. Les attaques par chaîne d’approvisionnement sont réelles. Il existe de nombreuses méthodes pour attaquer une chaîne d’approvisionnement, de l’insertion directe d’un code malveillant en tant que nouveau contributeur, à la reprise d’un compte de contributeur sans que d’autres personnes se aperçoivent, voire à la compromission d’une clé de signature pour distribuer un logiciel qui ne fait pas officiellement partie de la dépendance.

Une attaque par chaîne d’approvisionnement de logiciel est rarement l’objectif final, mais il est rare qu’il s’agisse d’une occasion pour une personne malveillante d’insérer des logiciels malveillants ou de fournir un Backdoor pour un accès futur.

![État du cycle de vie Octoverse 2020-Vulnerability](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Logiciels non corrigés

L’utilisation d’open source aujourd’hui est importante et n’est pas censée ralentir à tout moment. Étant donné que nous n’allons pas cesser d’utiliser le logiciel open source, la menace de fournir la sécurité de la chaîne n’est pas corrigée. Sachant cela, comment pouvez-vous résoudre le risque qu’une dépendance de votre projet comporte une vulnérabilité ?

- **Savoir ce qui se trouve dans votre environnement.** Cela nécessite de découvrir vos dépendances et toutes les dépendances transitives pour comprendre les risques liés à ces dépendances, tels que les vulnérabilités ou les restrictions de licence.
- **Gérez vos dépendances.** Lorsqu’une nouvelle vulnérabilité de sécurité est découverte, vous devez déterminer si vous êtes concerné et, le cas échéant, mettre à jour vers la version la plus récente et le correctif de sécurité disponible. Ceci est particulièrement important pour passer en revue les modifications qui introduisent de nouvelles dépendances ou auditant régulièrement les dépendances plus anciennes.
- **Surveillez votre chaîne d’approvisionnement.** Cela s’effectue en auditant les contrôles que vous avez en place pour gérer vos dépendances. Cela vous permet d’appliquer des conditions plus restrictives à respecter pour vos dépendances.

![État du Octoverse 2020-conseils](media/advisories.png)

nous allons aborder différents outils et techniques fournis par NuGet et GitHub, que vous pouvez utiliser aujourd’hui pour résoudre les risques potentiels au sein de votre projet. 

## <a name="knowing-what-is-in-your-environment"></a>Savoir ce qui se trouve dans votre environnement

### <a name="nuget-dependency-graph"></a>NuGet graphique de dépendance

**📦 Consommateur de package**

vous pouvez afficher vos dépendances de NuGet dans votre projet en regardant directement dans le fichier projet respectif.

Il se trouve généralement dans l’un des deux emplacements suivants :

-   [`packages.config`](../reference/packages-config.md) : Situé à la racine du projet.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) : Situé dans le fichier projet. 

selon la méthode que vous utilisez pour gérer vos dépendances de NuGet, vous pouvez également utiliser Visual Studio pour afficher vos dépendances directement dans [Explorateur de solutions](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) ou [NuGet Gestionnaire de package](../consume-packages/install-use-packages-visual-studio.md).

Pour les environnements CLI, vous pouvez utiliser la [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) commande pour répertorier les dépendances de votre projet ou de votre solution. 

pour plus d’informations sur la gestion des dépendances de NuGet, [consultez la documentation suivante](../consume-packages/overview-and-workflow.md).

### <a name="github-dependency-graph"></a>Graphique des dépendances de GitHub 

**📦 Consommateur de package | 📦🖊 Auteur du package**

vous pouvez utiliser le graphique de dépendance de GitHub pour voir les packages dont votre projet dépend et les dépôts qui en dépendent. Cela peut vous aider à voir toutes les vulnérabilités détectées dans ses dépendances.

pour plus d’informations sur les dépendances de référentiel GitHub, [consultez la documentation suivante](https://github.co/dependency-graph).

### <a name="dependency-versions"></a>Versions de dépendance

**📦 Consommateur de package | 📦🖊 Auteur du package**

Pour garantir une chaîne d’approvisionnement sécurisée des dépendances, vous devez vous assurer que toutes vos dépendances & outils sont régulièrement mises à jour vers la dernière version stable, car elles incluent souvent les derniers correctifs de sécurité et de fonctionnalités pour les vulnérabilités connues. Vos dépendances peuvent inclure le code dont vous dépendez, les fichiers binaires que vous consommez, les outils que vous utilisez et d’autres composants. Cela peut inclure :

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [Runtime SDK .NET &](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Packages NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Gérer vos dépendances

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet les dépendances déconseillées et vulnérables

**📦 Consommateur de package | 📦🖊 Auteur du package**

Vous pouvez utiliser l' [interface CLI dotnet](/dotnet/core/tools/dotnet-list-package) pour répertorier toutes les dépendances connues ou vulnérables que vous pouvez avoir dans votre projet ou votre solution. Vous pouvez utiliser la commande `dotnet list package --deprecated` ou `dotnet list package --vulnerable` pour obtenir une liste de toutes les vulnérabilités ou désapprobations connues.

### <a name="github-vulnerable-dependencies"></a>GitHub les dépendances vulnérables

**📦 Consommateur de package | 📦🖊 Auteur du package**

si votre projet est hébergé sur GitHub, vous pouvez tirer parti de la [sécurité GitHub](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) pour rechercher les failles de sécurité et les erreurs dans votre projet, et Dependabot les corriger en ouvrant une demande de tirage (pull request) sur votre base de code. 

L’interception des dépendances vulnérables avant leur introduction est l’un des objectifs du déplacement [« décalage vers la gauche »](https://en.wikipedia.org/wiki/Shift-left_testing) . La possibilité d’avoir des informations sur vos dépendances, telles que leur licence, les dépendances transitives et l’âge des dépendances, vous permet de le faire.

Pour plus d’informations sur les alertes Dependabot & les mises à jour de sécurité, [consultez la documentation suivante](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).

### <a name="nuget-feeds"></a>flux NuGet

**📦 Consommateur de package**

lors de l’utilisation de plusieurs flux source de NuGet publics & privés, un package peut être téléchargé à partir de n’importe quel flux. Pour vous assurer que votre Build est prévisible et sécurisée à partir d’attaques connues telles que la [confusion des dépendances](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), il est recommandé de savoir quels flux spécifiques proviennent de vos packages. Vous pouvez utiliser un flux unique ou un flux privé avec des capacités de protection en amont.

Pour plus d’informations sur la sécurisation de vos flux de packages, consultez [3 façons d’atténuer les risques lors de l’utilisation de flux de packages privés](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).

### <a name="client-trust-policies"></a>Stratégies d’approbation des clients

**📦 Consommateur de package**

Il existe des stratégies que vous pouvez choisir pour lesquelles vous avez besoin des packages que vous utilisez pour être signés. cela vous permet de faire confiance à l’auteur d’un package, à condition qu’il soit signé ou approuvé par un package s’il appartient à un utilisateur ou à un compte spécifique qui est un référentiel signé par NuGet. org.

Pour configurer des stratégies d’approbation [du client, consultez la documentation suivante](../consume-packages/installing-signed-packages.md).

### <a name="lock-files"></a>Verrouiller les fichiers

**📦 Consommateur de package**

Les fichiers de verrouillage stockent le hachage du contenu de votre package. Si le hachage de contenu d’un package que vous souhaitez installer correspond au fichier de verrouillage, il garantit la répétabilité des packages.

Pour activer les fichiers de verrouillage, [consultez la documentation suivante](../consume-packages/package-references-in-project-files.md#locking-dependencies).

## <a name="monitor-your-supply-chain"></a>Surveiller votre chaîne d’approvisionnement

### <a name="github-secret-scanning"></a>Analyse du secret GitHub

**📦🖊 Auteur du package**

GitHub analyse les référentiels pour les clés d’API NuGet pour empêcher les utilisations frauduleuses de secrets qui ont été validés par erreur. 

Pour en savoir plus sur l’analyse des secrets, consultez [à propos de l’analyse des secrets](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning).

### <a name="author-package-signing"></a>Créer une signature de package

**📦🖊 Auteur du package**

La signature de l' [auteur](../reference/signed-packages-reference.md) permet à l’auteur d’un package d’horodater son identité sur un package et à un consommateur de s’assurer qu’il vient de vous. Cela vous protège contre la falsification du contenu et sert de source unique de vérité sur l’origine du package et l’authenticité du package. Lorsqu’il est associé à des stratégies de confiance client, vous pouvez vérifier qu’un package provient d’un auteur spécifique.

Pour créer un package, consultez [signer un package](../create-packages/sign-a-package.md).

### <a name="two-factor-authentication-2fa"></a>Authentification Two-Factor (2FA)

**📦🖊 Auteur du package**

l’activation de l’authentification à deux facteurs (2FA) peut ajouter une couche de sécurité supplémentaire lors de la [connexion à votre compte GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) ou au [référentiel du package public NuGet. org](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa). Il est recommandé d’activer l’authentification à deux facteurs pour protéger votre compte.

### <a name="package-id-prefix-reservation"></a>Réservation du préfixe d’ID de package 

**📦🖊 Auteur du package**

Pour protéger l’identité de vos packages, vous pouvez réserver un préfixe d’ID de package à votre espace de noms respectif pour associer un propriétaire correspondant si votre préfixe d’ID de package se trouve correctement dans les [critères spécifiés](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria). 

Pour en savoir plus sur la réservation des préfixes d’ID, consultez [réservation de préfixe d’ID de package](../nuget-org/id-prefix-reservation.md).

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Dépréciation et retrait d’une liste de packages vulnérables

**📦🖊 Auteur du package**

Pour protéger l’écosystème de packages .NET quand vous avez pris connaissance d’une vulnérabilité dans un package que vous avez créé, faites-le mieux pour déprécier et supprimer la liste du package afin qu’il ne soit plus visible par les utilisateurs recherchant des packages. Si vous consommez un package qui est déconseillé et non répertorié, vous devez éviter d’utiliser le package.

Pour savoir comment déconseiller et délister un package, consultez la documentation suivante sur la [désapprobation](../nuget-org/deprecate-packages.md) et la [désinscription des packages](../nuget-org/policies/deleting-packages.md#unlisting-a-package).

## <a name="summary"></a>Récapitulatif

Votre chaîne d’approvisionnement logiciel est tout ce qui entre ou affecte votre code. Même si les compromets de chaîne d’approvisionnement sont réels et en pleine popularité, ils sont toujours rares. l’élément le plus important que vous puissiez faire est de protéger votre chaîne logistique en **connaissant vos dépendances, en gérant vos dépendances** et en **surveillant votre chaîne logistique.**

vous avez appris les différentes méthodes qui NuGet et [GitHub](/learn/modules/maintain-secure-repository-github/) vous permettent d’être plus efficaces pour l’affichage, la gestion et la surveillance de votre chaîne d’approvisionnement.

Pour plus d’informations sur la sécurisation des logiciels du monde, consultez [l’état du rapport de sécurité Octoverse 2020](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).
