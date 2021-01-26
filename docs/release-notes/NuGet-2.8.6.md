---
title: Poznámky k verzi NuGet 2.8.6
description: Poznámky k verzi pro NuGet 2.8.6, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776704"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="caaff-103">Poznámky k verzi NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="caaff-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="caaff-104">Poznámky k verzi [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Poznámky k verzi NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="caaff-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="caaff-105">2.8.6 NuGet byl vydán 20. července 2015 jako dílčí aktualizace našeho 2.8.5 VSIX s některými cílenými opravami a vylepšení pro podporu balíčků, které mohou být dodávány s podporou pro vývojového modelu Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="caaff-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="caaff-106">Tato verze rozšíření Správce balíčků NuGet poskytuje podporu jenom pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="caaff-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="caaff-107">V této verzi bylo dialogové okno Správce balíčků NuGet přidáno pro:</span><span class="sxs-lookup"><span data-stu-id="caaff-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="caaff-108">Zavedl (a) moniker cílového rozhraní UAP, který podporuje vývoj aplikací pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="caaff-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="caaff-109">Verze 3 koncové body protokolu NuGet</span><span class="sxs-lookup"><span data-stu-id="caaff-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="caaff-110">Podpora [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributu protocolVersion u zdrojů úložiště.</span><span class="sxs-lookup"><span data-stu-id="caaff-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="caaff-111">Výchozí hodnota je "2".</span><span class="sxs-lookup"><span data-stu-id="caaff-111">Default value is "2"</span></span>
* <span data-ttu-id="caaff-112">Návrat do vzdáleného úložiště, pokud není požadovaná verze balíčku k dispozici v místní mezipaměti</span><span class="sxs-lookup"><span data-stu-id="caaff-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>