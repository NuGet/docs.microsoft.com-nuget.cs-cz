---
title: Podpora rozhraní příkazového řádku NuGet dlouhé cesty
description: Referenční informace pro podporu dlouhé cesty nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547823"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="66a8c-103">Podpora dlouhé cesty (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="66a8c-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="66a8c-104">**Platí pro:** všechny &bullet; **podporované verze:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="66a8c-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="66a8c-105">NuGet.exe 4,8 a novější podporují dlouhé cesty pro soubory a adresáře pro scénáře, jako je balíček, obnovení, instalace a většinu scénářů, které je třeba cesty k souborům.</span><span class="sxs-lookup"><span data-stu-id="66a8c-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="66a8c-106">Požadovaný operační systém</span><span class="sxs-lookup"><span data-stu-id="66a8c-106">Required Operating System</span></span>

-   <span data-ttu-id="66a8c-107">Windows 10 (verze 1607 nebo novější)</span><span class="sxs-lookup"><span data-stu-id="66a8c-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="66a8c-108">Windows 10 (verze. července 2015 nebo verze 1511) je-li upgrade rozhraní .NET Framework verze 4.6.2 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="66a8c-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="66a8c-109">Windows Server 2016 (všechny verze)</span><span class="sxs-lookup"><span data-stu-id="66a8c-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="66a8c-110">Povolení zásad skupiny "Win32 dlouhé cesty"</span><span class="sxs-lookup"><span data-stu-id="66a8c-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="66a8c-111">Jeden je potřeba povolit dlouhé cesty podporu v těchto systémech nastavením zásad skupiny.</span><span class="sxs-lookup"><span data-stu-id="66a8c-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="66a8c-112">Pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="66a8c-112">Steps:</span></span>
1. <span data-ttu-id="66a8c-113">Spuštění **Editor zásad skupiny** – zadejte "Upravit zásady skupiny" na vyhledávacím panelu spuštění nebo spuštění "gpedit.msc" pomocí příkazu Spustit (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="66a8c-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="66a8c-114">V **Editor místních zásad skupiny**, povolte "místní počítač zásad nebo počítač platí následující konfigurace nebo správy šablony/všechny Win32 nastavení a povolit dlouhé cesty".</span><span class="sxs-lookup"><span data-stu-id="66a8c-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Zásady dlouhé cesty](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="66a8c-116">Povolení dalších nástrojů NuGet pro podporu dlouhé cesty</span><span class="sxs-lookup"><span data-stu-id="66a8c-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="66a8c-117">Rozhraní příkazového řádku DotNet podporuje dlouhé cesty bez ohledu na operační systém nebo verzi.</span><span class="sxs-lookup"><span data-stu-id="66a8c-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="66a8c-118">Visual Studio nebo nástroje msbuild/t: Restore zatím nepodporuje dlouhé cesty.</span><span class="sxs-lookup"><span data-stu-id="66a8c-118">Visual Studio or msbuild /t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="66a8c-119">Software, který používá NuGet knihoven ke spuštění obnovení a dalších příkazů, bude podporovat dlouhé cesty na stejných systémů, které NuGet.exe funguje na, pokud také nastavená longPathAware v jejich systému windows manifestu a nakonfigurovat UseLegacyPathHandling na hodnotu false pomocí souboru App.Config [ Další informace naleznete v tématu](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="66a8c-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

