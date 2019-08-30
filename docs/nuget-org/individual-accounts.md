---
title: Comptes individuels - NuGet.org
description: Des comptes individuels sur NuGet.org sont nécessaires pour publier des packages
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 63c6b5eb5ad635e436b4d53a5f833af35f72d76f
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999966"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="32f74-103">Comptes individuels sur NuGet.org</span><span class="sxs-lookup"><span data-stu-id="32f74-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="32f74-104">Vous devez créer un compte individuel pour publier et gérer des packages sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="32f74-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="32f74-105">Comptes individuels et comptes d’organisation</span><span class="sxs-lookup"><span data-stu-id="32f74-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="32f74-106">Votre compte individuel (utilisateur) est votre identité sur NuGet.org et peut être membre de plusieurs organisations.</span><span class="sxs-lookup"><span data-stu-id="32f74-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="32f74-107">Un package peut appartenir à un compte d’organisation ou à un compte individuel.</span><span class="sxs-lookup"><span data-stu-id="32f74-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="32f74-108">Pour les consommateurs de packages, il n’y a aucune différence entre un compte individuel et le compte d’organisation : tous deux apparaissent comme `owners` de packages.</span><span class="sxs-lookup"><span data-stu-id="32f74-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="32f74-109">Un compte d’organisation comprend un ou plusieurs comptes individuels comme membres.</span><span class="sxs-lookup"><span data-stu-id="32f74-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="32f74-110">Ces membres peuvent gérer un ensemble de packages tout en conservant une identité unique pour appropriation.</span><span class="sxs-lookup"><span data-stu-id="32f74-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="32f74-111">Ajouter un nouveau compte individuel</span><span class="sxs-lookup"><span data-stu-id="32f74-111">Add a new individual account</span></span>

<span data-ttu-id="32f74-112">Pour créer un compte NuGet.org, vous devez disposer d’un compte Microsoft personnel (MSA) ou d’un compte Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="32f74-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="32f74-113">Si vous n’en avez pas, vous pouvez en [créer](https://signup.live.com) un.</span><span class="sxs-lookup"><span data-stu-id="32f74-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="32f74-114">Effectuez les étapes suivantes si vous disposez d’un compte MSA ou AAD.</span><span class="sxs-lookup"><span data-stu-id="32f74-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="32f74-115">Accédez à la [page de connexion de NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="32f74-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="32f74-116">Cliquez sur le bouton **Se connecter avec Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="32f74-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="32f74-117">Entrez les détails de votre compte Microsoft ou Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32f74-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="32f74-118">Cliquez sur **Oui** pour accepter les autorisations à donner à l’application *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="32f74-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Octroi d’autorisations à NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="32f74-120">Vous allez être redirigé vers *nuget.org* et invité à inscrire un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="32f74-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="32f74-121">Spécifiez le nom d’utilisateur dans la zone d’entrée.</span><span class="sxs-lookup"><span data-stu-id="32f74-121">Specify the username in the input box.</span></span> <span data-ttu-id="32f74-122">Notez que le nom d’utilisateur **est** sensible à la casse et ne peut pas être changé ou renommé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="32f74-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Spécifier un nom d’utilisateur sur NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="32f74-124">Cliquez sur le bouton **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="32f74-124">Click the **Register** button.</span></span>

<span data-ttu-id="32f74-125">Vous disposez maintenant d’un compte NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="32f74-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="32f74-126">Vous pouvez effectuer la gestion des comptes dans la page des [paramètres du compte](https://www.nuget.org/account).</span><span class="sxs-lookup"><span data-stu-id="32f74-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="32f74-127">Activer l’authentification à 2 facteurs (2FA)</span><span class="sxs-lookup"><span data-stu-id="32f74-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="32f74-128">Pour mieux protéger votre compte, activez l’authentification à 2 facteurs (recommandé).</span><span class="sxs-lookup"><span data-stu-id="32f74-128">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="32f74-129">Une fois connecté à votre compte, ouvrez votre profil et choisissez **Activer** sous **Compte de connexion**.</span><span class="sxs-lookup"><span data-stu-id="32f74-129">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Activer la 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="32f74-131">Vous voyez un message vous indiquant que la prochaine fois que vous vous connecterez *à nuget.org*, vous serez invité à fournir des informations d’identification supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="32f74-131">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="32f74-132">Pour terminer l’authentification à ce stade, déconnectez-vous, puis reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="32f74-132">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="32f74-133">Quand vous vous connectez, choisissez le texte ou le courrier électronique comme deuxième forme d’authentification.</span><span class="sxs-lookup"><span data-stu-id="32f74-133">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="32f74-134">Vérifiez le numéro de téléphone ou l’adresse e-mail qui est déjà associée à votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32f74-134">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="32f74-135">Vous devrez peut-être entrer un nouveau numéro de téléphone ou une nouvelle adresse e-mail pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="32f74-135">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="32f74-136">Dans ce cas, entrez les informations requises comme indiqué, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="32f74-136">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Activer la 2FA](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="32f74-138">Vérifiez votre appareil ou votre compte de messagerie, puis entrez le code que vous venez de recevoir.</span><span class="sxs-lookup"><span data-stu-id="32f74-138">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Activer la 2FA](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="32f74-140">Suivez les instructions supplémentaires pour terminer l’authentification à 2 deux facteurs.</span><span class="sxs-lookup"><span data-stu-id="32f74-140">Follow any additional instructions to complete Two-factor authentication.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="32f74-141">Supprimer un compte NuGet.org</span><span class="sxs-lookup"><span data-stu-id="32f74-141">Delete a NuGet.org account</span></span>

<span data-ttu-id="32f74-142">Pour obtenir de l’aide sur d’autres tâches en lien avec les comptes, comme supprimer un compte NuGet.org, consultez [Gestion des comptes NuGet.org](nuget-org-faq.md#nugetorg-account-management).</span><span class="sxs-lookup"><span data-stu-id="32f74-142">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
