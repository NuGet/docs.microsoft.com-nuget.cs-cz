---
title: Řešení sporů s názvem balíčku NuGet
description: Proces řešení sporů mezi vydavateli balíčků NuGet souvisejících se značkou, ochrannými známkami a dalšími situacemi v konfliktu.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: d9ed7de95a1f38ea2c288b28958519b1dff0e595
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775659"
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="0b0e6-103">Řešení sporů přes názvy balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="0b0e6-103">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="0b0e6-104">Tento článek poskytuje doporučený proces řešení pro členy komunity pro řešení sporů s jinými vydavateli NuGet.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-104">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="0b0e6-105">Předpokládejme například, že Northwind Traders vytvoří systém CRM, pro který poskytuje klientské ovladače jako ke stažení MSI z webu.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-105">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="0b0e6-106">Jana, nezávislý vývojář, chce usnadnit používání klientské knihovny Northwind a převede ho do balíčku NuGet s názvem `NorthwindTraders.Client` .</span><span class="sxs-lookup"><span data-stu-id="0b0e6-106">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="0b0e6-107">Později verze Northwind chce pro svou klientskou knihovnu předložit oficiální balíček NuGet, který by tedy chtěl jednat o vlastnictví názvu balíčku.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-107">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="0b0e6-108">V tomto scénáři se Jana zdá, že se nejedná o nesprávné záměry, ale místo toho podporuje nástroje a zákazníky Northwind a přispívá vlastní čas a kód.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-108">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="0b0e6-109">V současné době je Northwind legitimním vlastníkem názvu Northwind.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-109">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="0b0e6-110">Pomocí následujícího postupu mohou databáze Northwind a Petr spolupracovat na vhodném rozlišení, protože obě mají zájem o poskytování komunitě vývojářů.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-110">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="0b0e6-111">Obvykle není nutné, aby se tým NuGet účastnil. spolupráce obvykle funguje nejlépe.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-111">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span>

## <a name="process"></a><span data-ttu-id="0b0e6-112">Proces</span><span class="sxs-lookup"><span data-stu-id="0b0e6-112">Process</span></span>

1. <span data-ttu-id="0b0e6-113">Kontaktujte vlastníky balíčku, ke kterému máte spor, pomocí odkazu **vlastníci kontaktu** na stránce s podrobnostmi balíčku.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-113">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="0b0e6-114">Vysvětlete svůj problém tak, že budete mít nějaký druh a přímým způsobem.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-114">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="0b0e6-115">Poslat kopii zprávy na [support@nuget.org](mailto:support@nuget.org) , aby NuGet a .NET Foundation věděli o vašem sporu.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-115">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="0b0e6-116">Počkejte na vyřešení maximálně 30 dní a pak [support@nuget.org](mailto:support@nuget.org) znovu upozorněte.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-116">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="0b0e6-117">Tým podpory nuget.org se zapojí a zkusí vyřešit spor s oběma stranami.</span><span class="sxs-lookup"><span data-stu-id="0b0e6-117">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
