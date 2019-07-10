---
title: Comptes individuels
description: Des comptes individuels sur NuGet.org sont nécessaires pour publier des packages
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427134"
---
# <a name="individual-accounts"></a><span data-ttu-id="bfb2a-103">Comptes individuels</span><span class="sxs-lookup"><span data-stu-id="bfb2a-103">Individual accounts</span></span>

<span data-ttu-id="bfb2a-104">Vous devez créer un compte individuel pour publier et gérer des packages sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="bfb2a-105">Comptes individuels et comptes d’organisation</span><span class="sxs-lookup"><span data-stu-id="bfb2a-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="bfb2a-106">Votre compte individuel (utilisateur) est votre identité sur NuGet.org et peut être membre de plusieurs organisations.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="bfb2a-107">Un package peut appartenir à un compte d’organisation ou à un compte individuel.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="bfb2a-108">Pour les consommateurs de packages, il n’y a aucune différence entre un compte individuel et le compte d’organisation : tous deux apparaissent comme `owners` de packages.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="bfb2a-109">Un compte d’organisation comprend un ou plusieurs comptes individuels comme membres.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="bfb2a-110">Ces membres peuvent gérer un ensemble de packages tout en conservant une identité unique pour appropriation.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="bfb2a-111">Ajouter un nouveau compte individuel</span><span class="sxs-lookup"><span data-stu-id="bfb2a-111">Add a new individual account</span></span>

<span data-ttu-id="bfb2a-112">Pour créer un compte NuGet.org, vous devez disposer d’un compte Microsoft personnel (MSA) ou d’un compte Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="bfb2a-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="bfb2a-113">Si vous n’en avez pas, vous pouvez en [créer](https://signup.live.com) un.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="bfb2a-114">Effectuez les étapes suivantes si vous disposez d’un compte MSA ou AAD.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="bfb2a-115">Accédez à la [page de connexion de NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="bfb2a-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="bfb2a-116">Cliquez sur le bouton **Se connecter avec Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="bfb2a-117">Entrez les détails de votre compte Microsoft ou Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="bfb2a-118">Cliquez sur **Oui** pour accepter les autorisations à donner à l’application *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Octroi d’autorisations à NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="bfb2a-120">Vous allez être redirigé vers *nuget.org* et invité à inscrire un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="bfb2a-121">Spécifiez le nom d’utilisateur dans la zone d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-121">Specify the username in the input box.</span></span> <span data-ttu-id="bfb2a-122">Notez que le nom d’utilisateur **est** sensible à la casse et ne peut pas être changé ou renommé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Spécifier un nom d’utilisateur sur NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="bfb2a-124">Cliquez sur le bouton **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-124">Click the **Register** button.</span></span>

<span data-ttu-id="bfb2a-125">Vous disposez maintenant d’un compte NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="bfb2a-126">Vous pouvez effectuer la gestion des comptes dans la page des [paramètres du compte](https://www.nuget.org/account).</span><span class="sxs-lookup"><span data-stu-id="bfb2a-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
