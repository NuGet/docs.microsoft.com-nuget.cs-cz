---
title: Poznámky k verzi NuGet 2.8.6 přílohy
description: Poznámky k verzi pro NuGet 2.8.6 přílohy včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819715"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="ad758-103">Poznámky k verzi NuGet 2.8.6 přílohy</span><span class="sxs-lookup"><span data-stu-id="ad758-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="ad758-104">[Poznámky k verzi NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 poznámky k verzi](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="ad758-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="ad758-105">Byl vydán NuGet 2.8.6 přílohy 20 července 2015 jako menší aktualizace našich 2.8.5 VSIX s některé cílové opravy a vylepšení pro podporu balíčky, které mohou být dodávány s podporou pro model vývoj Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="ad758-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="ad758-106">Tato verze rozšíření Správce balíčků NuGet poskytuje podporu pouze pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="ad758-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="ad758-107">V této verzi dialogové okno Správce balíčků NuGet bylo přidala se podpora:</span><span class="sxs-lookup"><span data-stu-id="ad758-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="ad758-108">Zavedly UAP cílový Framework Přezdívka pro podporu vývoj aplikací pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ad758-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="ad758-109">Koncové body verze 3 protokolu NuGet</span><span class="sxs-lookup"><span data-stu-id="ad758-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="ad758-110">Podpora pro [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) vlastnost protocolVersion atribut úložiště zdroje.</span><span class="sxs-lookup"><span data-stu-id="ad758-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="ad758-111">Výchozí hodnota je 2.</span><span class="sxs-lookup"><span data-stu-id="ad758-111">Default value is "2"</span></span>
* <span data-ttu-id="ad758-112">Návratem zpět do vzdáleného úložiště, pokud požadovaný balíček verze není k dispozici v místní mezipaměti</span><span class="sxs-lookup"><span data-stu-id="ad758-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>