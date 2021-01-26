---
title: Demandes de données utilisateur
description: Stratégies de demande d’exportation et de suppression de données utilisateur
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775717"
---
# <a name="user-data-requests"></a><span data-ttu-id="947bd-103">Demandes de données utilisateur</span><span class="sxs-lookup"><span data-stu-id="947bd-103">User Data Requests</span></span>

<span data-ttu-id="947bd-104">les utilisateurs nuget.org peuvent envoyer des demandes de suppression d’informations et des demandes d’exportation d’informations via [NuGet.org](https://www.nuget.org). Les deux types sont soumis sous la forme de demandes de support et sont exécutés par les administrateurs nuget.org dans un délai de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="947bd-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="947bd-105">Les données utilisateur suivantes sont directement accessibles par le biais de nuget.org :</span><span class="sxs-lookup"><span data-stu-id="947bd-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="947bd-106">Données liées aux comptes, telles que les adresses e-mail, les comptes de connexion, les images de profils et les paramètres de notification par e-mail</span><span class="sxs-lookup"><span data-stu-id="947bd-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="947bd-107">Clés d’API détenues</span><span class="sxs-lookup"><span data-stu-id="947bd-107">Owned API Keys</span></span>
* <span data-ttu-id="947bd-108">Liste des packages détenus</span><span class="sxs-lookup"><span data-stu-id="947bd-108">List of owned packages</span></span>

<span data-ttu-id="947bd-109">Ces données ne sont pas incluses dans les données exportées dans le cadre de la demande de support.</span><span class="sxs-lookup"><span data-stu-id="947bd-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="947bd-110">Identification des données client</span><span class="sxs-lookup"><span data-stu-id="947bd-110">Identifying customer data</span></span>

<span data-ttu-id="947bd-111">Les données client peuvent être identifiées comme des noms de comptes d’utilisateur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="947bd-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="947bd-112">Suppression des données client</span><span class="sxs-lookup"><span data-stu-id="947bd-112">Deleting customer data</span></span>

<span data-ttu-id="947bd-113">Pour demander la suppression de données utilisateur de nuget.org :</span><span class="sxs-lookup"><span data-stu-id="947bd-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="947bd-114">L’utilisateur doit se connecter à [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="947bd-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="947bd-115">L’utilisateur doit envoyer une demande de suppression de son compte à [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="947bd-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="947bd-116">Nous conseillons aux utilisateurs qui sont les seuls propriétaires de packages à trouver de nouveaux propriétaires avant de demander la suppression de leur compte.</span><span class="sxs-lookup"><span data-stu-id="947bd-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="947bd-117">Si la propriété de package n’est pas transférée, le package NuGet n’est plus répertorié et, par conséquent, il n’est plus disponible dans les requêtes de recherche dans Visual Studio ou sur le site web nuget.org.</span><span class="sxs-lookup"><span data-stu-id="947bd-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="947bd-118">Avant de supprimer le compte, les administrateurs nuget.org collaborent avec l’utilisateur afin de trouver de nouveaux propriétaires pour leurs packages.</span><span class="sxs-lookup"><span data-stu-id="947bd-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="947bd-119">L’action de suppression du compte est effectuée par l’administrateur nuget.org dans les 30 jours suivant la date de la demande.</span><span class="sxs-lookup"><span data-stu-id="947bd-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="947bd-120">Lors de la suppression du compte, toutes les données de l’utilisateur sont supprimées du système nuget.org et les actions suivantes sont exécutées :</span><span class="sxs-lookup"><span data-stu-id="947bd-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="947bd-121">Le compte supprimé n’est plus inscrit auprès de nuget.org</span><span class="sxs-lookup"><span data-stu-id="947bd-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="947bd-122">Toutes les clés d’API détenues sont supprimées</span><span class="sxs-lookup"><span data-stu-id="947bd-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="947bd-123">Tous les espaces de noms réservés sont libérés</span><span class="sxs-lookup"><span data-stu-id="947bd-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="947bd-124">Les éventuelles propriétés de packages sont supprimées</span><span class="sxs-lookup"><span data-stu-id="947bd-124">Any package ownership are removed</span></span>

<span data-ttu-id="947bd-125">Les packages détenus ne sont *pas* supprimés.</span><span class="sxs-lookup"><span data-stu-id="947bd-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="947bd-126">Bien qu’ils ne figurent plus dans les résultats de recherche, ils restent disponibles par le biais de la restauration de package dans les projets qui en dépendent.</span><span class="sxs-lookup"><span data-stu-id="947bd-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="947bd-127">Exportation des données client</span><span class="sxs-lookup"><span data-stu-id="947bd-127">Exporting customer data</span></span>

<span data-ttu-id="947bd-128">Une fois connecté à nuget.org, un utilisateur peut soumettre une demande d’exportation par le biais de [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="947bd-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="947bd-129">Les données exportées peuvent être téléchargées par l’utilisateur pendant 48 heures par le biais d’un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="947bd-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="947bd-130">Après 48 heures, l’accès expire et l’utilisateur doit envoyer une nouvelle demande d’exportation si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="947bd-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="947bd-131">Les données exportées incluent :</span><span class="sxs-lookup"><span data-stu-id="947bd-131">The exported data includes:</span></span>

* <span data-ttu-id="947bd-132">Les demandes de support de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="947bd-132">The user's support requests</span></span>
* <span data-ttu-id="947bd-133">Les actions de l’utilisateur (publication de package, création de compte) telles que conservées dans les journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="947bd-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="947bd-134">Toutes les informations utilisateur telles que conservées dans les journaux IIS</span><span class="sxs-lookup"><span data-stu-id="947bd-134">Any user information as persisted in the IIS logs</span></span>
