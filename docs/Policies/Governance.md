---
title: Gouvernance des projets NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Modèle de gouvernance pour NuGet, y compris les rôles et responsabilités des validateurs, contributeurs et utilisateurs.
keywords: gouvernance pour NuGet, dictateur bienveillant NuGet, responsabilités des validateurs, responsabilités des contributeurs, responsabilités des utilisateurs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: aa48b95482c65de47d54daff142402dd2ff6558a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-governance"></a>Gouvernance pour NuGet

> Ce document est basé sur le [modèle de gouvernance des dictateurs bienveillants](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) établi par l’Université d’Oxford. Il est concédé sous licence [Creative Commons Attribution-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Le projet NuGet est dirigé par un dictateur bienveillant et géré par la communauté. Autrement dit, la communauté contribue activement à la maintenance quotidienne du projet, mais la ligne stratégique générale est dessinée par le dictateur bienveillant. En cas de désaccord, le dictateur bienveillant a le dernier mot.

Il appartient au dictateur bienveillant de résoudre les litiges au sein de la communauté et de s’assurer que le projet peut progresser de façon coordonnée. De son côté, il incombe à la communauté de guider les décisions du dictateur bienveillant par un engagement et une contribution actifs.

## <a name="roles-and-responsibilities"></a>Rôles et responsabilités

Quatre rôles sont décrits ici : dictateur bienveillant, validateurs, contributeurs et utilisateurs.

### <a name="benevolent-dictator"></a>Dictateur bienveillant

L’équipe NuGet principale est automatiquement désignée comme dictateur bienveillant ou responsable de projet. Toutefois, étant donné que la communauté a toujours la possibilité d’effectuer une duplication, l’équipe est entièrement responsable devant la communauté. Le responsable de projet doit comprendre la communauté dans son ensemble et s’efforcer de satisfaire autant de besoins en conflit que possible, tout en garantissant la survie du projet à long terme.

Dans bien des égards, le rôle du dictateur bienveillant relève moins de l’autoritarisme que de la diplomatie. L’important est qu’au fil du développement du projet les personnes appropriées aient une influence sur celui-ci et que la vision du responsable de projet gagne la communauté. Le rôle du responsable consiste alors à s’assurer que les validateurs (voir ci-dessous) prennent les bonnes décisions pour le compte du projet. En règle générale, tant que les validateurs épousent la stratégie du projet, le responsable de projet leur permet de procéder comme ils le souhaitent.

De plus, les équipes de la .NET Foundation considère le responsable de projet comme le premier ou principal point de contact pour NuGet concernant les opérations d’entreprise, y compris les inscriptions de domaine et les services techniques (tels que la signature de code).

### <a name="committers"></a>Validateurs

Les validateurs sont des contributeurs qui ont régulièrement apporté des contributions précieuses à NuGet et sont désignés par le dictateur bienveillant. Une fois nommés, les validateurs sont chargés d’écrire le code directement dans le référentiel et de filtrer les contributions des autres. Les validateurs sont souvent des développeurs, mais ils peuvent contribuer par d’autres moyens.

En règle générale, un validateur se concentre sur un aspect spécifique du projet, apportant un niveau d’expertise et de compréhension qui lui vaut le respect de la communauté et du responsable de projet. Le rôle de validateur n’est pas un rôle officiel ; il s’agit simplement d’une position que les membres influents de la communauté assument quand le responsable de projet se tourne vers eux pour obtenir de l’aide et un soutien.

Les validateurs n’ont aucune autorité sur la direction globale de NuGet. Toutefois, ils ont toute l’attention du chef de projet. Il appartient au validateur de s’assurer que le responsable tient compte des besoins et des objectifs collectifs de la communauté et d’aider à développer ou obtenir des contributions appropriées au projet. Souvent, les validateurs se voient accorder un contrôle informel de leurs domaines de responsabilité spécifiques, ainsi que des droits de modification directe de certaines zones du code source. Autrement dit, bien que les validateurs n’aient pas explicitement autorité en matière de prise de décision, ils constatent souvent que leurs actions concordent avec les décisions prises par le responsable.

### <a name="contributors"></a>Contributors

Les contributeurs sont des membres de la communauté qui soumettent des correctifs à NuGet. Ces correctifs peuvent se produire une ou plusieurs fois. En règle générale, les correctifs soumis par un contributeur sont petits dans un premier temps, puis deviennent plus importants à mesure que leur qualité gagne la confiance des contributeurs, des validateurs et du chef de projet. Les contributeurs sont identifiés dans le document des notes de publication du produit associé.

Avant que le premier correctif d’un contributeur ne soit placé dans le dépôt, ce contributeur doit signer un [contrat de licence de contributeur](http://en.wikipedia.org/wiki/Contributor_License_Agreement) ou un accord d’affectation avec la .NET Foundation. Le correctif peut être soumis et discuté, mais il ne peut pas être validé dans le dépôt sans les papiers appropriés nécessaires. Pour obtenir un contrat de licence de contributeur, envoyez une demande par e-mail à [contributions@nuget.org](mailto:contributions@nuget.org).

Pour devenir contributeur, envoyez une demande de tirage (pull request) à un des dépôts suivants :

- [NuGet Client](https://github.com/NuGet/NuGet.Client)
- [NuGet Gallery](https://github.com/nuget/nugetgallery)
- [NuGet Docs](https://github.com/nuget/nugetdocs)

Le processus détaillé pour l’envoi d’une demande de tirage varie d’un dépôt à l’autre :

- [Instructions de contribution pour NuGet Client et NuGet Gallery](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Instructions de contribution pour NuGet Docs](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Utilisateurs

Les utilisateurs sont des membres de la communauté qui ont besoin de NuGet et qui l’utilisent, en tant qu’auteurs et/ou consommateurs de packages. Les utilisateurs sont les membres les plus importants de la communauté : sans eux, le projet n’aurait aucune utilité. Toute personne peut être utilisateur ; il n’existe aucune condition particulière.

Les utilisateurs doivent être encouragés à participer à la vie de NuGet et de la communauté autant que possible. Les contributions des utilisateurs permettent à l’équipe de projet de s’assurer qu’elle répond aux besoins de ces utilisateurs. Les activités courantes des utilisateurs incluent, entre autres, les suivantes :

- Préconiser l’utilisation du projet
- Informer les développeurs du projet des forces et des faiblesses du point de vue d’un nouvel utilisateur
- Fournir un support moral (un simple merci est très apprécié)
- Écrire de la documentation et des didacticiels
- Archiver les rapports de bogues et les demandes de fonctionnalités
- Participer à des événements de la communauté, tels que des dépistages de bogues
- Participer aux forums Internet et de discussion

Les utilisateurs qui continuent de s’engager dans le projet et sa communauté voient souvent leur implication prendre de l’ampleur. Ces utilisateurs peuvent tenter de devenir contributeurs, comme décrit ci-dessus.

## <a name="package-succession-under-special-circumstances"></a>Succession des packages dans des circonstances particulières

En cas de décès ou d’incapacité d’un détenteur de compte NuGet, nous travaillons avec la communauté pour ajouter un ou des propriétaires appropriés au package si le compte en question jouit d’une propriété exclusive et que le package est publié sous une [licence OSI approuvée](https://opensource.org/licenses/alphabetical). Pour demander la propriété, vous devez nous envoyer les documents suivants :

1. Une photocopie d’une pièce d’identité officielle avec photo
1. Un des documents suivants prouvant l’état du titulaire précédent du compte : 
    - Un certificat de décès officiel si le détenteur précédent du compte est décédé ou
    - Un document certifié, tel qu’un certificat signé par un professionnel de la santé qui assure le suivi d’un titulaire de compte frappé d’incapacité
1. Un des documents suivants prouvant votre droit à la propriété : 
    - Certificat de mariage montrant que vous êtes le conjoint survivant du titulaire du compte
    - Procuration signée
    - Copie d’un testament ou document de fiducie nommant un l’exécuteur ou bénéficiaire
    - Certificat de naissance du titulaire du compte, si vous êtes son parent ou
    - Documents de tutelle si vous êtes tuteur légal du titulaire du compte

Si vous vous sentez concerné, veuillez nous envoyer un e-mail à [support@nuget.org](mailto:support@nuget.org) avec l’ID et la version du package.

## <a name="transparency"></a>Transparence

Bâtir la confiance de la communauté dans la gouvernance d’un projet open source est essentiel à la réussite de ce dernier. À cette fin, la prise de décision doit être effectuée de façon transparente et ouverte. La direction du projet doit faire l’objet d’une présentation publique. La communauté ne doit jamais être prise au dépourvu par une décision du dictateur bienveillant. De plus, la discussion à propos des décisions relatives au projet doit être archivée afin que les membres de la communauté puissent comprendre l’historique complet d’une décision et son contexte.
