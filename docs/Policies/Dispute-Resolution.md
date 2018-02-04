---
title: "Balíček NuGet název řešení sporů | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Proces pro řešení sporů mezi vydavatelů balíček NuGet související s brandingem, ochranné známky a jiných situacích konflikt."
keywords: "Sporů balíčku NuGet, řešení sporů NuGet, procesu překladu, který sporu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="7faa4-104">Řešení sporů přes názvy balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="7faa4-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="7faa4-105">Tento článek obsahuje doporučené řešení proces pro členy komunity pro řešení sporů s jinými vydavateli NuGet.</span><span class="sxs-lookup"><span data-stu-id="7faa4-105">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="7faa4-106">Předpokládejme například, že Northwind Traders vytvoří systému CRM, pro kterou poskytují ovladače klienta jako souboru MSI ke stažení z jejich webu.</span><span class="sxs-lookup"><span data-stu-id="7faa4-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="7faa4-107">Nancy vývojář nezávislé chce usnadnit používání společnosti Northwind klientské knihovny a převede ji balíček NuGet s názvem `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="7faa4-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="7faa4-108">Později Northwind chce vytvořit balíček NuGet oficiální vlastní, pro jejich klientské knihovny a proto chcete spor Nancyin vlastnictví název balíčku.</span><span class="sxs-lookup"><span data-stu-id="7faa4-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="7faa4-109">V tomto scénáři Nancy nezdá se být funguje s chybný záměry, ale je místo Podpora nástrojů a zákazníků společnosti Northwind přispěje svůj vlastní čas a kódu.</span><span class="sxs-lookup"><span data-stu-id="7faa4-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="7faa4-110">Northwind ve stejnou dobu, je legitimní vlastníkem Northwind název.</span><span class="sxs-lookup"><span data-stu-id="7faa4-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="7faa4-111">Podle následujících instrukcí níže, Northwind a Nancy můžou spolupracovat a vhodné řešení, protože obě zajímá obsluhující komunity vývojářů.</span><span class="sxs-lookup"><span data-stu-id="7faa4-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="7faa4-112">Obvykle není nutné pro tým NuGet se; spolupráce obvykle funguje nejlépe.</span><span class="sxs-lookup"><span data-stu-id="7faa4-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="7faa4-113">Ve skutečnosti každých sporu oznámena týmem NuGet k datu byla fungovala bez týmem museli předat rozhodnutí.</span><span class="sxs-lookup"><span data-stu-id="7faa4-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="7faa4-114">Proces</span><span class="sxs-lookup"><span data-stu-id="7faa4-114">Process</span></span>

1. <span data-ttu-id="7faa4-115">Obraťte se na vlastníky balíčku máte sporu s použitím **vlastníky obraťte se na** odkaz na stránce s podrobnostmi o balíčku.</span><span class="sxs-lookup"><span data-stu-id="7faa4-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="7faa4-116">Popisují problém druh a přímé způsobem.</span><span class="sxs-lookup"><span data-stu-id="7faa4-116">Explain your issue in a kind and direct manner.</span></span>
1. <span data-ttu-id="7faa4-117">Odeslat kopie zprávy do [ support@nuget.org ](mailto:support@nuget.org) tak, aby si vědomi spor NuGet a Foundation rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="7faa4-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
1. <span data-ttu-id="7faa4-118">Počkejte 30 dnů pro řešení, a upozorní [ support@nuget.org ](mailto:support@nuget.org) znovu.</span><span class="sxs-lookup"><span data-stu-id="7faa4-118">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="7faa4-119">Tým podpory nuget.org bude zapojení a pokuste se pracovat obě strany sporu.</span><span class="sxs-lookup"><span data-stu-id="7faa4-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
