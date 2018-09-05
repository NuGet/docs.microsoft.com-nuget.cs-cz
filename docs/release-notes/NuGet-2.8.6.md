---
title: Zpráva k vydání verze NuGet 2.8.6 přílohy
description: Zpráva k vydání verze pro NuGet 2.8.6 přílohy včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546488"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="c8d24-103">Zpráva k vydání verze NuGet 2.8.6 přílohy</span><span class="sxs-lookup"><span data-stu-id="c8d24-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="c8d24-104">[Zpráva k vydání verze NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [zpráva k vydání verze NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="c8d24-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="c8d24-105">Byla vydána NuGet 2.8.6 přílohy 20. července 2015 jako menší aktualizace našich 2.8.5 VSIX s některými cílová opravy a vylepšení pro podporu balíčky, které mohou být dodávány s podporou pro Windows 10 UPW vývojový model.</span><span class="sxs-lookup"><span data-stu-id="c8d24-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="c8d24-106">Tato verze rozšíření Správce balíčků NuGet poskytuje podporu pouze pro sadu Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c8d24-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="c8d24-107">V této verzi má dialogové okno Správce balíčků NuGet přidány pro podporu:</span><span class="sxs-lookup"><span data-stu-id="c8d24-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="c8d24-108">Zavedená Moniker cílového rozhraní UAP podporovat vývoj aplikací pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c8d24-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="c8d24-109">Koncové body NuGet protokolu verze 3</span><span class="sxs-lookup"><span data-stu-id="c8d24-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="c8d24-110">Podpora pro [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) vlastnost protocolVersion atribut na zdrojích úložiště.</span><span class="sxs-lookup"><span data-stu-id="c8d24-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="c8d24-111">Výchozí hodnota je "2"</span><span class="sxs-lookup"><span data-stu-id="c8d24-111">Default value is "2"</span></span>
* <span data-ttu-id="c8d24-112">Návrat do vzdáleného úložiště, pokud požadovaný balíček verze není k dispozici v místní mezipaměti</span><span class="sxs-lookup"><span data-stu-id="c8d24-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>