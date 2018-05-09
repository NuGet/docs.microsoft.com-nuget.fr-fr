---
title: Demandes de données utilisateur
description: Stratégies de demande d’exportation et de suppression de données utilisateur
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
---
# <a name="user-data-requests"></a>Demandes de données utilisateur

Les utilisateurs de nuget.org peuvent envoyer des demandes de suppression d’informations et des demandes d’exportation d’informations par le biais de [nuget.org](https://www.nuget.org). Ces deux types de demandes sont envoyés sous forme de demande de support et sont exécutés par les administrateurs nuget.org dans les 30 jours.

Les données utilisateur suivantes sont directement accessibles par le biais de nuget.org :

* Données liées aux comptes, telles que les adresses e-mail, les comptes de connexion, les images de profils et les paramètres de notification par e-mail
* Clés d’API détenues
* Liste des packages détenus

Ces données ne sont pas incluses dans les données exportées dans le cadre de la demande de support.

## <a name="identifying-customer-data"></a>Identification des données client

Les données client peuvent être identifiées comme des noms de comptes d’utilisateur nuget.org.

## <a name="deleting-customer-data"></a>Suppression de données client

Pour demander la suppression de données utilisateur de nuget.org :

1. L’utilisateur doit se connecter à [nuget.org](https://www.nuget.org)
1. L’utilisateur doit envoyer une demande de suppression de son compte à [nuget.org/account/delete](https://www.nuget.org/account/delete)

Nous conseillons aux utilisateurs qui sont les seuls propriétaires de packages à trouver de nouveaux propriétaires avant de demander la suppression de leur compte. Si la propriété de package n’est pas transférée, le package NuGet n’est plus répertorié et, par conséquent, il n’est plus disponible dans les requêtes de recherche dans Visual Studio ou sur le site web nuget.org. Avant de supprimer le compte, les administrateurs nuget.org collaborent avec l’utilisateur afin de trouver de nouveaux propriétaires pour leurs packages.

L’action de suppression du compte est effectuée par l’administrateur nuget.org dans les 30 jours suivant la date de la demande.

Lors de la suppression du compte, toutes les données de l’utilisateur sont supprimées du système nuget.org et les actions suivantes sont exécutées :

* Le compte supprimé n’est plus inscrit auprès de nuget.org
* Toutes les clés d’API détenues sont supprimées
* Tous les espaces de noms réservés sont libérés
* Les éventuelles propriétés de packages sont supprimées

Les packages détenus ne sont *pas* supprimés. Bien qu’ils ne figurent plus dans les résultats de recherche, ils restent disponibles par le biais de la restauration de package dans les projets qui en dépendent.

## <a name="exporting-customer-data"></a>Exportation de données client

Une fois connecté à nuget.org, un utilisateur peut soumettre une demande d’exportation par le biais de [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact).

Les données exportées peuvent être téléchargées par l’utilisateur pendant 48 heures par le biais d’un objet blob Azure. Après 48 heures, l’accès expire et l’utilisateur doit envoyer une nouvelle demande d’exportation si nécessaire.

Les données exportées incluent :

* Les demandes de support de l’utilisateur
* Les actions de l’utilisateur (publication de package, création de compte) telles que conservées dans les journaux d’audit
* Toutes les informations utilisateur telles que conservées dans les journaux IIS
