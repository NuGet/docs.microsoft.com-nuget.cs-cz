---
title: Řešení sporů názvů balíčků NuGet
description: Proces řešení sporů mezi vydavateli balíčků NuGet týkající se brandingu, ochranných známek a dalších konfliktních situací.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427497"
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="fc01b-103">Řešení sporů ohledně názvů balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="fc01b-103">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="fc01b-104">Tento článek poskytuje doporučený proces řešení pro členy komunity k řešení sporů s jinými vydavateli NuGet.</span><span class="sxs-lookup"><span data-stu-id="fc01b-104">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="fc01b-105">Předpokládejme například, že Northwind Traders vytvoří CRM systém, pro který poskytují ovladače klienta jako ke stažení MSI z jejich webových stránek.</span><span class="sxs-lookup"><span data-stu-id="fc01b-105">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="fc01b-106">Nancy, nezávislý vývojář, chce usnadnit použití northwind klientské knihovny a změní ji `NorthwindTraders.Client`na balíček NuGet s názvem .</span><span class="sxs-lookup"><span data-stu-id="fc01b-106">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="fc01b-107">Později Northwind chce vytvořit oficiální Balíček NuGet pro jejich vlastní pro jejich klientské knihovny, a proto by chtěli zpochybnit Nancy vlastnictví názvu balíčku.</span><span class="sxs-lookup"><span data-stu-id="fc01b-107">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="fc01b-108">V tomto scénáři Nancy nezdá se, že jedná se špatnými úmysly, ale spíše podporuje nástroje a zákazníky společnosti Northwind tím, že přispívá svým vlastním časem a kódem.</span><span class="sxs-lookup"><span data-stu-id="fc01b-108">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="fc01b-109">Ve stejné době, Northwind je legitimní vlastník northwind jméno.</span><span class="sxs-lookup"><span data-stu-id="fc01b-109">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="fc01b-110">Podle níže uvedeného procesu mohou společnosti Northwind a Nancy spolupracovat na vhodném řešení, protože oba mají zájem sloužit komunitě vývojářů.</span><span class="sxs-lookup"><span data-stu-id="fc01b-110">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="fc01b-111">Obvykle není nutné, aby se tým NuGet zapojil; spolupráce obvykle funguje nejlépe.</span><span class="sxs-lookup"><span data-stu-id="fc01b-111">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="fc01b-112">Ve skutečnosti každý spor, který byl do týmu NuGet dosud upozorněn, byl vypracován bez nutnosti vynášet rozsudky.</span><span class="sxs-lookup"><span data-stu-id="fc01b-112">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="fc01b-113">Proces</span><span class="sxs-lookup"><span data-stu-id="fc01b-113">Process</span></span>

1. <span data-ttu-id="fc01b-114">Obraťte se na vlastníky balíčku máte spor s pomocí **kontaktu vlastníci** odkaz na stránce podrobnosti o balíčku.</span><span class="sxs-lookup"><span data-stu-id="fc01b-114">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="fc01b-115">Vysvětlete svůj problém laskavým a přímým způsobem.</span><span class="sxs-lookup"><span data-stu-id="fc01b-115">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="fc01b-116">Odešlete kopii [support@nuget.org](mailto:support@nuget.org) zprávy tak, aby NuGet a .NET Foundation jsou si vědomi vašeho sporu.</span><span class="sxs-lookup"><span data-stu-id="fc01b-116">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="fc01b-117">Počkejte maximálně 30 dní na [support@nuget.org](mailto:support@nuget.org) řešení a poté jej znovu oznamte.</span><span class="sxs-lookup"><span data-stu-id="fc01b-117">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="fc01b-118">Tým nuget.org podpory se zapojí a pokusí se vyřešit spor s oběma stranami.</span><span class="sxs-lookup"><span data-stu-id="fc01b-118">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
