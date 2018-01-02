---
title: "Résolution des litiges autour des noms de package NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6d664378-3f7b-426e-aef3-2254d745fe60
description: "Processus de résolution des litiges entre les éditeurs de packages NuGet liés à la personnalisation, aux marques et autres situations de conflit."
keywords: "litiges autour des packages NuGet, résolution des litiges autour de NuGet, processus de résolution des litiges"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32f5f766a49a2e4254a81978757d973fc5353db1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="bb1e4-104">Résolution des litiges autour des noms de package NuGet</span><span class="sxs-lookup"><span data-stu-id="bb1e4-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="bb1e4-105">Ce document présente un processus de résolution recommandé à l’attention des membres de la communauté pour résoudre les litiges avec d’autres éditeurs NuGet.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-105">This document is a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>  

<span data-ttu-id="bb1e4-106">Par exemple, supposons que Northwind Traders crée un système CRM pour lequel il fournit des pilotes clients sous la forme d’un fichier MSI téléchargeable à partir de son site web.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="bb1e4-107">Nancy, développeuse indépendante, souhaite faciliter l’utilisation de la bibliothèque cliente de Northwind et la convertit en package NuGet appelé `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="bb1e4-108">Peu après, Northwind veut produire de son côté un package NuGet officiel pour leur bibliothèque cliente et souhaite donc contester à Nancy la propriété du nom du package.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="bb1e4-109">Dans ce scénario, Nancy ne semble pas agir avec de mauvaises intentions. Au contraire, elle agit plutôt en faveur des outils et des clients de Northwind en donnant de son temps et en contribuant avec son code.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="bb1e4-110">Parallèlement, Northwind est le propriétaire légitime du nom Northwind.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="bb1e4-111">En suivant la procédure ci-dessous, Northwind et Nancy peuvent rechercher ensemble une résolution appropriée, car l’un comme l’autre souhaitent servir la communauté des développeurs.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="bb1e4-112">Il n’est généralement pas nécessaire que l’équipe NuGet intervienne, car la collaboration résout généralement tous les problèmes.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="bb1e4-113">En fait, à ce jour, chaque litige soumis à l’équipe NuGet a été résolu sans qu’elle ait dû se prononcer.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>


## <a name="process"></a><span data-ttu-id="bb1e4-114">Procédure</span><span class="sxs-lookup"><span data-stu-id="bb1e4-114">Process</span></span>

1. <span data-ttu-id="bb1e4-115">Contactez les propriétaires du package auxquels vous oppose le litige en utilisant le lien **Contact Owners** (Contacter les propriétaires) dans la page de détails du package.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="bb1e4-116">Expliquez votre problème de manière claire et courtoise.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-116">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="bb1e4-117">Envoyez une copie de votre message à [support@nuget.org](mailto:support@nuget.org) afin que NuGet et la .NET Foundation prennent connaissance de votre litige.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="bb1e4-118">Si le litige n’est pas résolu au bout de 30 jours, renotifiez [support@nuget.org](mailto:support@nuget.org).</span><span class="sxs-lookup"><span data-stu-id="bb1e4-118">Wait a maximum of 30 days for a resolution, after which notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="bb1e4-119">L’équipe de support nuget.org prendra part au dossier afin de résoudre le litige avec les deux parties.</span><span class="sxs-lookup"><span data-stu-id="bb1e4-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
