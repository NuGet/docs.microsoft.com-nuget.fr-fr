---
title: Votre organisation sur NuGet.org
description: Les organisations sur NuGet.org vous aident à gérer les packages qui sont publiés par un groupe ou dans une équipe au sein d’une entreprise.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427074"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="2de1b-103">Votre organisation sur NuGet.org</span><span class="sxs-lookup"><span data-stu-id="2de1b-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="2de1b-104">Les organisations permettent à des projets d’entreprise et des projets open source de travailler ensemble sur des packages en utilisant une identité NuGet.org unique.</span><span class="sxs-lookup"><span data-stu-id="2de1b-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="2de1b-105">Pour un consommateur de package, un compte d’organisation se présente de la même façon qu’un compte d’utilisateur existant sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="2de1b-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="2de1b-106">Comptes d’organisation et comptes individuels</span><span class="sxs-lookup"><span data-stu-id="2de1b-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="2de1b-107">Un compte d’organisation comprend un ou plusieurs comptes (d’utilisateur) individuels comme membres.</span><span class="sxs-lookup"><span data-stu-id="2de1b-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="2de1b-108">Ces membres peuvent gérer un ensemble de packages tout en conservant une identité unique pour la propriété.</span><span class="sxs-lookup"><span data-stu-id="2de1b-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="2de1b-109">Votre compte individuel constitue votre identité sur NuGet.org et peut être membre de plusieurs organisations.</span><span class="sxs-lookup"><span data-stu-id="2de1b-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="2de1b-110">Un package peut appartenir à un compte d’organisation ou à un compte individuel.</span><span class="sxs-lookup"><span data-stu-id="2de1b-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="2de1b-111">Pour les consommateurs de packages, il n’y a aucune différence entre un compte individuel et le compte d’organisation : tous deux sont présentés comme les propriétaires (`owners`) des packages.</span><span class="sxs-lookup"><span data-stu-id="2de1b-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="2de1b-112">Ajout d’une nouvelle organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-112">Adding a new organization</span></span>

<span data-ttu-id="2de1b-113">Pour ajouter une nouvelle organisation, sélectionnez votre compte sur NuGet.org, puis sélectionnez la commande de menu **Gérer les organisations...**  :</span><span class="sxs-lookup"><span data-stu-id="2de1b-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Option de menu Gérer les organisations sur NuGet.org](media/org-manage-option.png)

<span data-ttu-id="2de1b-115">Dans la page suivante, sélectionnez le bouton **Ajouter une nouvelle organisation** :</span><span class="sxs-lookup"><span data-stu-id="2de1b-115">On the next page, select the **Add new organization** button:</span></span>

![Bouton pour créer une organisation sur NuGet.org](media/org-add-new-option.png)

<span data-ttu-id="2de1b-117">Dans la page suivante, entrez le nom et l’adresse e-mail de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="2de1b-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="2de1b-118">Dans la mesure où les comptes d’organisation partagent le même espace de noms avec les comptes d’utilisateur, choisissez un nom d’organisation différent des autres noms de compte d’organisation ou d’utilisateur existants.</span><span class="sxs-lookup"><span data-stu-id="2de1b-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="2de1b-119">L’adresse e-mail doit également être unique à chaque compte.</span><span class="sxs-lookup"><span data-stu-id="2de1b-119">The email address must also be unique across all accounts.</span></span>

![Page Ajouter une nouvelle organisation sur NuGet.org](media/org-add-new-page.png)

<span data-ttu-id="2de1b-121">Une fois que vous avez créé le compte d’organisation, vous en êtes l’administrateur et, à ce titre, vous pouvez publier des packages pour l’organisation et ajouter des membres à l’organisation.</span><span class="sxs-lookup"><span data-stu-id="2de1b-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="2de1b-122">Transformer un compte existant en organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="2de1b-123">La conversion de compte est irréversible : vous ne pouvez plus après transformer une organisation en compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2de1b-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="2de1b-124">Si vous gérez les packages d’une équipe à l’aide d’un seul compte d’utilisateur et que vous souhaitez convertir ce compte en organisation, utilisez l’option **Transformer votre compte en organisation** dans la page **Gérer les organisations** :</span><span class="sxs-lookup"><span data-stu-id="2de1b-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Option sur NuGet.org pour transformer un compte existant en organisation](media/org-transform-option.png)

<span data-ttu-id="2de1b-126">Dans la page suivante, sélectionnez un compte d’utilisateur différent et définissez-le en tant qu’administrateur de l’organisation, puis sélectionnez **Transformer**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Saisie des informations pour la transformation d’un compte d’utilisateur en organisation](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="2de1b-128">Gérer les membres de l’organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-128">Managing organization members</span></span>

<span data-ttu-id="2de1b-129">En tant qu’administrateur de l’organisation, vous pouvez ajouter des membres en indiquant le *nom du compte d’utilisateur* NuGet.org de chaque membre (l’ajout avec les adresses e-mail n’est pas possible).</span><span class="sxs-lookup"><span data-stu-id="2de1b-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="2de1b-130">Vous définissez ensuite chaque membre comme collaborateur ou administrateur avec les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2de1b-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="2de1b-131">Autorisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-131">Permission</span></span> | <span data-ttu-id="2de1b-132">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="2de1b-132">Collaborator</span></span> | <span data-ttu-id="2de1b-133">Administrateur</span><span class="sxs-lookup"><span data-stu-id="2de1b-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2de1b-134">Gérer les packages de l’organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-134">Manage the organization's packages</span></span><br/><span data-ttu-id="2de1b-135">(publier de nouveaux packages, mettre à jour des packages existants ou en retirer de la liste)</span><span class="sxs-lookup"><span data-stu-id="2de1b-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="2de1b-136">Oui</span><span class="sxs-lookup"><span data-stu-id="2de1b-136">Yes</span></span> | <span data-ttu-id="2de1b-137">Oui</span><span class="sxs-lookup"><span data-stu-id="2de1b-137">Yes</span></span> |
| <span data-ttu-id="2de1b-138">Modifier les métadonnées de l’organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-138">Change organization metadata</span></span><br/><span data-ttu-id="2de1b-139">(adresse e-mail, paramètres de notification)</span><span class="sxs-lookup"><span data-stu-id="2de1b-139">(email address, notification settings)</span></span> | <span data-ttu-id="2de1b-140">Non</span><span class="sxs-lookup"><span data-stu-id="2de1b-140">No</span></span> | <span data-ttu-id="2de1b-141">Oui</span><span class="sxs-lookup"><span data-stu-id="2de1b-141">Yes</span></span> |
| <span data-ttu-id="2de1b-142">Gérer les membres de l’organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-142">Manage organization members</span></span> | <span data-ttu-id="2de1b-143">Non</span><span class="sxs-lookup"><span data-stu-id="2de1b-143">No</span></span> | <span data-ttu-id="2de1b-144">Oui</span><span class="sxs-lookup"><span data-stu-id="2de1b-144">Yes</span></span> |
| <span data-ttu-id="2de1b-145">Demander la copropriété ou agir sur les demandes de copropriété pour les packages de l’organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="2de1b-146">Non</span><span class="sxs-lookup"><span data-stu-id="2de1b-146">No</span></span> | <span data-ttu-id="2de1b-147">Oui</span><span class="sxs-lookup"><span data-stu-id="2de1b-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="2de1b-148">Gérer les packages</span><span class="sxs-lookup"><span data-stu-id="2de1b-148">Managing packages</span></span>

<span data-ttu-id="2de1b-149">Dans la page [Gérer les packages](https://www.nuget.org/account/Packages), vous pouvez voir tous les packages associés à votre compte et toutes les organisations dont vous êtes membre.</span><span class="sxs-lookup"><span data-stu-id="2de1b-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="2de1b-150">Pour voir les packages associés à votre compte ou ceux d’une organisation spécifique, utilisez le filtre de comptes situé en haut à droite de la page.</span><span class="sxs-lookup"><span data-stu-id="2de1b-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Gestion des packages avec le filtre de comptes](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="2de1b-152">Transférer des packages vers une organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-152">Transferring packages to an organization</span></span>
<span data-ttu-id="2de1b-153">Si vous souhaitez transférer certains de vos packages vers une organisation que vous venez de créer, demandez au compte d’organisation d’être copropriétaire du package, puis supprimez votre compte en tant que propriétaire.</span><span class="sxs-lookup"><span data-stu-id="2de1b-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="2de1b-154">Si vous êtes un administrateur de l’organisation, aucune confirmation n’est nécessaire pour accepter la propriété.</span><span class="sxs-lookup"><span data-stu-id="2de1b-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="2de1b-155">En revanche, si vous êtes un collaborateur, l’ajout de l’organisation en tant que propriétaire nécessite que l’un des administrateurs accepte la propriété.</span><span class="sxs-lookup"><span data-stu-id="2de1b-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="2de1b-156">Publication de packages</span><span class="sxs-lookup"><span data-stu-id="2de1b-156">Publishing packages</span></span>

<span data-ttu-id="2de1b-157">Vous pouvez publier des packages dans une organisation comme vous le faites dans un compte d’utilisateur : en chargeant le package directement sur NuGet.org ou en envoyant (push) le package à l’aide des commandes CLI `nuget push` ou `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="2de1b-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="2de1b-158">Charger des packages</span><span class="sxs-lookup"><span data-stu-id="2de1b-158">Uploading packages</span></span>

<span data-ttu-id="2de1b-159">Quand vous chargez un nouveau package directement sur la page [Charger sur NuGet.org](https://www.nuget.org/packages/manage/upload), vous attribuez la propriété du package à un compte d’utilisateur ou d’organisation :</span><span class="sxs-lookup"><span data-stu-id="2de1b-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Charger un package avec l’option du compte](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="2de1b-161">Utiliser des clés API</span><span class="sxs-lookup"><span data-stu-id="2de1b-161">Using API keys</span></span>

<span data-ttu-id="2de1b-162">Pour envoyer (push) un package à l’aide des commandes CLI `nuget push` ou `dotnet nuget push`, vous devez préalablement obtenir la clé API dont ces commandes ont besoin.</span><span class="sxs-lookup"><span data-stu-id="2de1b-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="2de1b-163">Pour plus d’informations, consultez [Publier un package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="2de1b-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="2de1b-164">Quand vous créez une clé API, sélectionnez l’organisation appropriée dans le menu déroulant **Propriétaire du package**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="2de1b-165">Chaque clé API que vous créez s’applique uniquement à l’organisation choisie :</span><span class="sxs-lookup"><span data-stu-id="2de1b-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Clé API avec l’option du compte](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="2de1b-167">Supprimer une organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-167">Removing an organization</span></span>

<span data-ttu-id="2de1b-168">En tant qu’utilisateur, vous pouvez vous retirer d’une organisation en sélectionnant le bouton **X** à côté de votre appartenance à l’organisation :</span><span class="sxs-lookup"><span data-stu-id="2de1b-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Retrait d’un compte d’utilisateur d’une organisation](media/org-remove-self-option.png)

<span data-ttu-id="2de1b-170">Les administrateurs peuvent retirer n’importe quel membre de l’organisation, y compris les autres administrateurs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="2de1b-171">Si vous êtes le seul administrateur d’une organisation, vous ne pouvez pas vous retirer, sauf si vous ajoutez un autre membre comme administrateur.</span><span class="sxs-lookup"><span data-stu-id="2de1b-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="2de1b-172">Supprimer un compte d’organisation</span><span class="sxs-lookup"><span data-stu-id="2de1b-172">Deleting an organization account</span></span>

<span data-ttu-id="2de1b-173">Vous pouvez supprimer un compte d’organisation en cliquant sur le bouton **Supprimer** figurant dans la page de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="2de1b-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Supprimer une organisation](media/org-delete-option.png)

<span data-ttu-id="2de1b-175">Pour supprimer l’organisation, vous devez confirmer l’opération en cliquant sur le bouton de confirmation **Supprimer l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
