---
title: "Poznámky k verzi NuGet 2.8.6 přílohy | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Poznámky k verzi pro NuGet 2.8.6 přílohy včetně – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.8.6 přílohy poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="62791-104">Poznámky k verzi NuGet 2.8.6 přílohy</span><span class="sxs-lookup"><span data-stu-id="62791-104">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="62791-105">[Poznámky k verzi NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 poznámky k verzi](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="62791-105">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="62791-106">Byl vydán NuGet 2.8.6 přílohy 20 července 2015 jako menší aktualizace našich 2.8.5 VSIX s některé cílové opravy a vylepšení pro podporu balíčky, které mohou být dodávány s podporou pro model vývoj Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="62791-106">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="62791-107">Tato verze rozšíření Správce balíčků NuGet poskytuje podporu pouze pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="62791-107">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="62791-108">V této verzi dialogové okno Správce balíčků NuGet bylo přidala se podpora:</span><span class="sxs-lookup"><span data-stu-id="62791-108">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="62791-109">Zavedly UAP cílový Framework Přezdívka pro podporu vývoj aplikací pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="62791-109">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="62791-110">Koncové body verze 3 protokolu NuGet</span><span class="sxs-lookup"><span data-stu-id="62791-110">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="62791-111">Podpora pro [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) vlastnost protocolVersion atribut úložiště zdroje.</span><span class="sxs-lookup"><span data-stu-id="62791-111">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="62791-112">Výchozí hodnota je 2.</span><span class="sxs-lookup"><span data-stu-id="62791-112">Default value is "2"</span></span>
* <span data-ttu-id="62791-113">Návratem zpět do vzdáleného úložiště, pokud požadovaný balíček verze není k dispozici v místní mezipaměti</span><span class="sxs-lookup"><span data-stu-id="62791-113">Falling back to remote repository if a required package version is not available in the local cache</span></span>