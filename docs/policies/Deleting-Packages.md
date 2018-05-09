---
title: Suppression de packages NuGet de nuget.org
description: Stratégies de retrait de packages de nuget.org ; la suppression définitive n’est pas prise en charge, sauf quand les packages ne respectent pas les autres stratégies.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: bea4f1589f184d38da27e5d82c3ce17a183fbdd1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="deleting-packages"></a><span data-ttu-id="0353e-103">Suppression de packages</span><span class="sxs-lookup"><span data-stu-id="0353e-103">Deleting packages</span></span>

<span data-ttu-id="0353e-104">NuGet.org ne prend pas en charge la suppression définitive de packages.</span><span class="sxs-lookup"><span data-stu-id="0353e-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="0353e-105">Cela compromettrait chaque projet dépendant de la disponibilité du package, en particulier dans le cas des workflows de build qui impliquent la restauration du package.</span><span class="sxs-lookup"><span data-stu-id="0353e-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="0353e-106">NuGet.org prend en charge *la suppression d’un package de la liste*, opération qui peut être effectuée dans la page de gestion des packages sur le site web.</span><span class="sxs-lookup"><span data-stu-id="0353e-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="0353e-107">Les packages supprimés de la liste n’apparaissent ni sur nuget.org ni dans l’interface utilisateur de Visual Studio, ni dans les résultats d’une recherche.</span><span class="sxs-lookup"><span data-stu-id="0353e-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="0353e-108">Toutefois, vous pouvez quand même les télécharger et les installer en utilisant un numéro de version exact qui prend en charge la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="0353e-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="0353e-109">De plus, il est toujours possible de découvrir les packages supprimés de la liste dans les scénarios spécifiques suivants :</span><span class="sxs-lookup"><span data-stu-id="0353e-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="0353e-110">Restauration de packages à l’aide de versions flottantes (par exemple, `1.0.0-*`), si le dernier package disponible correspondant aux contraintes de version ou dépendance est un package supprimé de la liste.</span><span class="sxs-lookup"><span data-stu-id="0353e-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="0353e-111">Réplication des packages par le biais du catalogue (qui, lui aussi, contient des packages supprimés de la liste).</span><span class="sxs-lookup"><span data-stu-id="0353e-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="0353e-112">Exceptions</span><span class="sxs-lookup"><span data-stu-id="0353e-112">Exceptions</span></span>

<span data-ttu-id="0353e-113">Dans des situations exceptionnelles, comme la violation de droits d’auteur et la présence de contenu potentiellement dangereux, les packages peuvent être supprimés manuellement par l’équipe NuGet.</span><span class="sxs-lookup"><span data-stu-id="0353e-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="0353e-114">Envoyez une demande de support par le biais de la [Galerie NuGet](http://www.nuget.org) pour démarrer la procédure.</span><span class="sxs-lookup"><span data-stu-id="0353e-114">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="0353e-115">Utilisation interdite</span><span class="sxs-lookup"><span data-stu-id="0353e-115">Prohibited use</span></span>

<span data-ttu-id="0353e-116">Les packages qui répondent aux critères suivants ne sont pas autorisés dans la galerie NuGet publique et sont immédiatement supprimés sans discussion.</span><span class="sxs-lookup"><span data-stu-id="0353e-116">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="0353e-117">Toutefois, les propriétaires des packages sont informés de leur suppression.</span><span class="sxs-lookup"><span data-stu-id="0353e-117">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="0353e-118">Contiennent des programmes malveillants, des logiciels de publicité ou tout type de logiciels espions.</span><span class="sxs-lookup"><span data-stu-id="0353e-118">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="0353e-119">Sont conçus pour endommager la station de travail d’un développeur ou son organisation.</span><span class="sxs-lookup"><span data-stu-id="0353e-119">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="0353e-120">Violent les droits d’auteur ou les licences.</span><span class="sxs-lookup"><span data-stu-id="0353e-120">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="0353e-121">Contiennent du contenu illégal.</span><span class="sxs-lookup"><span data-stu-id="0353e-121">Contains illegal content.</span></span>
- <span data-ttu-id="0353e-122">Sont utilisés pour monopoliser les identificateurs de package, y compris les packages totalement dépourvus de contenu de production.</span><span class="sxs-lookup"><span data-stu-id="0353e-122">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="0353e-123">Les packages doivent contenir du code ou les propriétaires doivent concéder l’identificateur à une personne qui a effectivement un produit à livrer.</span><span class="sxs-lookup"><span data-stu-id="0353e-123">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="0353e-124">Essaient de faire faire à la galerie une opération pour laquelle elle n’est pas explicitement conçue.</span><span class="sxs-lookup"><span data-stu-id="0353e-124">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="0353e-125">Si vous trouvez un package qui enfreint un de ces éléments, cliquez sur le lien **Signaler un abus** dans la page des détails du package, puis envoyez un rapport.</span><span class="sxs-lookup"><span data-stu-id="0353e-125">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="0353e-126">Notez que l’équipe NuGet et la .NET Foundation se réservent le droit de changer ces critères à tout moment.</span><span class="sxs-lookup"><span data-stu-id="0353e-126">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
