---
title: Organisations sur nuget.org
description: Les organisations sur nuget.org vous aide à gérer les packages publiés par groupe ou dans une équipe, l’environnement d’entreprise.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/22/2018
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="0c3b2-103">Organisation sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="0c3b2-103">Organization on nuget.org</span></span>

<span data-ttu-id="0c3b2-104">Organisations permettent aux entreprises et les projets open source pour collaborer sur des packages à l’aide d’une identité unique nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="0c3b2-105">Pour un consommateur de package, un compte d’organisation apparaît identique à un compte d’utilisateur existant sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="0c3b2-106">Comptes d’utilisateurs et comptes d’organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="0c3b2-107">Votre compte d’utilisateur est votre identité sur nuget.org et peut être un membre d’un nombre d’organisations.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="0c3b2-108">Un package peut appartenir à un compte d’organisation comme il peut appartenir à un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="0c3b2-109">Consommateurs de package ne voient aucune différence entre un compte d’utilisateur ou le compte d’organisation : les deux s’affichent en tant que package `owners`.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="0c3b2-110">Un compte organisation a un ou plusieurs comptes d’utilisateur en tant que ses membres.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="0c3b2-111">Ces membres peuvent gérer un ensemble de packages tout en conservant une identité unique pour la propriété.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="0c3b2-112">Ajout d’une organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-112">Adding a new organization</span></span>

<span data-ttu-id="0c3b2-113">Pour ajouter une nouvelle organisation, sélectionnez votre compte sur nuget.org, puis sélectionnez le **aux organisations de gérer...**  commande de menu :</span><span class="sxs-lookup"><span data-stu-id="0c3b2-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Option de menu sur nuget.org pour les organisations de gestionnaire](media/org-manage-option.png)

<span data-ttu-id="0c3b2-115">Sur la page suivante, sélectionnez le **ajouter une nouvelle organisation** bouton :</span><span class="sxs-lookup"><span data-stu-id="0c3b2-115">On the next page, select the **Add new organization** button:</span></span>

![Bouton permettant de créer une nouvelle organisation sur nuget.org](media/org-add-new-option.png)

<span data-ttu-id="0c3b2-117">Sur la page suivante, fournissez l’adresse e-mail et le nom de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="0c3b2-118">Étant donné que les comptes d’organisation partagent le même espace de noms en tant que comptes d’utilisateur, le nom d’organisation doit être différent de tout autre organisation existante ou comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="0c3b2-119">L’adresse de messagerie doit également être unique dans tous les comptes.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-119">The email address must also be unique across all accounts.</span></span>

![Ajouter une nouvelle page de l’organisation sur nuget.org](media/org-add-new-page.png)

<span data-ttu-id="0c3b2-121">Une fois que le compte d’organisation est créé, vous êtes l’administrateur et pouvez envoyer des packages pour l’organisation et ajouter des membres de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="0c3b2-122">Transformer le compte existant à une organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="0c3b2-123">Conversion de compte est irréversible : Impossible de transformer une organisation à un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="0c3b2-124">Si vous gérez des packages en tant qu’équipe à l’aide d’un compte d’utilisateur et que vous souhaitez convertir ce compte dans une organisation, utilisez le **transformer votre compte à l’organisation** option sur le **gérer organisations** page :</span><span class="sxs-lookup"><span data-stu-id="0c3b2-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Option sur nuget.org pour transformer un compte existant à l’organisation](media/org-transform-option.png)

<span data-ttu-id="0c3b2-126">Sur la page suivante, spécifiez le compte d’utilisateur différent pour attribuer en tant que l’administrateur de l’organisation, puis sélectionnez **transformer**.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Entrer des informations pour la transformation d’un compte d’utilisateur à l’organisation](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="0c3b2-128">Gestion des membres de l’organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-128">Managing organization members</span></span>

<span data-ttu-id="0c3b2-129">En tant qu’administrateur de l’organisation, vous pouvez ajouter des membres en fournissant nuget.org de chaque membre *nom de compte d’utilisateur*; les adresses de messagerie ne peut pas être utilisés.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="0c3b2-130">Marquez ensuite chaque membre en tant que collaborateur ou administrateur avec les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c3b2-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="0c3b2-131">Autorisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-131">Permission</span></span> | <span data-ttu-id="0c3b2-132">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="0c3b2-132">Collaborator</span></span> | <span data-ttu-id="0c3b2-133">Administrateur</span><span class="sxs-lookup"><span data-stu-id="0c3b2-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c3b2-134">Gérer les packages de l’organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-134">Manage the organization's packages</span></span><br/><span data-ttu-id="0c3b2-135">(nouveaux packages, mettre à jour ou de retrait de la liste des packages existants)</span><span class="sxs-lookup"><span data-stu-id="0c3b2-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="0c3b2-136">Oui</span><span class="sxs-lookup"><span data-stu-id="0c3b2-136">Yes</span></span> | <span data-ttu-id="0c3b2-137">Oui</span><span class="sxs-lookup"><span data-stu-id="0c3b2-137">Yes</span></span> |
| <span data-ttu-id="0c3b2-138">Métadonnées modifiées organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-138">Change organization metadata</span></span><br/><span data-ttu-id="0c3b2-139">(adresse de messagerie, les paramètres de notification)</span><span class="sxs-lookup"><span data-stu-id="0c3b2-139">(email address, notification settings)</span></span> | <span data-ttu-id="0c3b2-140">Non</span><span class="sxs-lookup"><span data-stu-id="0c3b2-140">No</span></span> | <span data-ttu-id="0c3b2-141">Oui</span><span class="sxs-lookup"><span data-stu-id="0c3b2-141">Yes</span></span> |
| <span data-ttu-id="0c3b2-142">Gérer les membres de l’organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-142">Manage organization members</span></span> | <span data-ttu-id="0c3b2-143">Non</span><span class="sxs-lookup"><span data-stu-id="0c3b2-143">No</span></span> | <span data-ttu-id="0c3b2-144">Oui</span><span class="sxs-lookup"><span data-stu-id="0c3b2-144">Yes</span></span> |
| <span data-ttu-id="0c3b2-145">Demande ou agir sur les demandes co-propriété pour les packages de l’organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="0c3b2-146">Non</span><span class="sxs-lookup"><span data-stu-id="0c3b2-146">No</span></span> | <span data-ttu-id="0c3b2-147">Oui</span><span class="sxs-lookup"><span data-stu-id="0c3b2-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="0c3b2-148">Gestion des packages</span><span class="sxs-lookup"><span data-stu-id="0c3b2-148">Managing packages</span></span>

<span data-ttu-id="0c3b2-149">Vous pouvez afficher tous les packages sur votre compte et toutes les organisations dont vous êtes un membre sur le [gérer les Packages](https://www.nuget.org/account/Packages) page.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="0c3b2-150">Pour afficher les packages spécifiques à votre compte ou de toute organisation spécifique, utilisez le filtre de comptes dans la partie supérieure droite de la page.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Gestion des packages avec le filtre de compte](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="0c3b2-152">Transfert de packages à l’organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-152">Transferring packages to an organization</span></span>
<span data-ttu-id="0c3b2-153">Si vous souhaitez transférer certains de vos packages à une organisation qui vient d’être créée, vous pouvez le faire en demandant le compte d’organisation à copropriétaires du package puis supprimer vous-même en tant que le propriétaire.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="0c3b2-154">Si vous êtes un administrateur de l’organisation, il n’existe aucune confirmation pas obligée d’accepter la propriété.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="0c3b2-155">Toutefois, si vous êtes un collaborateur, ajout de l’organisation en tant que propriétaire nécessite l’un des administrateurs pour accepter la propriété.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="0c3b2-156">Publication de packages</span><span class="sxs-lookup"><span data-stu-id="0c3b2-156">Publishing packages</span></span>

<span data-ttu-id="0c3b2-157">Publier des packages à l’organisation que vous publiez des packages sur un compte d’utilisateur : en directement en chargeant le package à nuget.org ou en appuyant sur le package le `nuget push` ou `dotnet nuget push` commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="0c3b2-158">Téléchargement des packages</span><span class="sxs-lookup"><span data-stu-id="0c3b2-158">Uploading packages</span></span>

<span data-ttu-id="0c3b2-159">Lorsque vous téléchargez directement un nouveau package sur le [nuget.org téléchargement](https://www.nuget.org/packages/manage/upload) page, vous affectez le propriétaire du lot à un compte d’utilisateur ou de l’organisation :</span><span class="sxs-lookup"><span data-stu-id="0c3b2-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Télécharger le package avec l’option de compte](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="0c3b2-161">À l’aide de clés de l’API</span><span class="sxs-lookup"><span data-stu-id="0c3b2-161">Using API keys</span></span>

<span data-ttu-id="0c3b2-162">Pour distribuer un package le `nuget push` ou `dotnet nuget push` commandes CLI, vous devez obtenir une clé d’API requise par ces commandes.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="0c3b2-163">Pour plus d’informations, consultez [publier un package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="0c3b2-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="0c3b2-164">Lorsque vous créez une nouvelle clé d’API, sélectionnez l’organisation appropriée dans le **Package propriétaire** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="0c3b2-165">N’importe quelle touche API que vous créez s’applique uniquement à l’organisation choisie :</span><span class="sxs-lookup"><span data-stu-id="0c3b2-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Clé API avec l’option de compte](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="0c3b2-167">Suppression d’une organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-167">Removing an organization</span></span>

<span data-ttu-id="0c3b2-168">En tant qu’utilisateur, vous pouvez vous désinscrire à partir d’une organisation en sélectionnant le `X` affiché par l’appartenance à votre organisation :</span><span class="sxs-lookup"><span data-stu-id="0c3b2-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Suppression d’un compte d’utilisateur à partir d’une organisation](media/org-remove-self-option.png)

<span data-ttu-id="0c3b2-170">Les administrateurs peuvent supprimer n’importe quel membre de l’organisation, y compris d’autres administrateurs.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="0c3b2-171">Si vous êtes le seul administrateur d’une organisation, vous ne pouvez pas vous supprimer sauf si vous ajoutez un autre membre en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="0c3b2-172">Suppression d’un compte d’organisation</span><span class="sxs-lookup"><span data-stu-id="0c3b2-172">Deleting an organization account</span></span>

<span data-ttu-id="0c3b2-173">Cette fonctionnalité sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="0c3b2-173">This feature is coming soon.</span></span>
