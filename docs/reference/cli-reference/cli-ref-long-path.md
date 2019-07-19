---
title: Podpora dlouhých cest CLI NuGet
description: Referenční informace o podpoře dlouhých cest NuGet. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328306"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="c58d4-103">Podpora dlouhých cest (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="c58d4-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="c58d4-104">**Platí pro:** všechny &bullet; **podporované verze:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="c58d4-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="c58d4-105">NuGet. exe 4,8 a novější podporuje dlouhé cesty k souborům a adresářům pro scénáře, jako jsou balíčky, obnovení, instalace a většina dalších scénářů, které potřebují cesty k souborům.</span><span class="sxs-lookup"><span data-stu-id="c58d4-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="c58d4-106">Požadovaný operační systém</span><span class="sxs-lookup"><span data-stu-id="c58d4-106">Required Operating System</span></span>

-   <span data-ttu-id="c58d4-107">Windows 10 (verze 1607 nebo novější)</span><span class="sxs-lookup"><span data-stu-id="c58d4-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="c58d4-108">Windows 10 (verze z července 2015 nebo verze 1511) Pokud upgradujete .NET Framework na verze 4.6.2 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="c58d4-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="c58d4-109">Windows Server 2016 (všechny verze)</span><span class="sxs-lookup"><span data-stu-id="c58d4-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="c58d4-110">Povolte "dlouhé cesty Win32" Zásady skupiny</span><span class="sxs-lookup"><span data-stu-id="c58d4-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="c58d4-111">Jedna z nich musí povolit podporu dlouhých cest v těchto systémech nastavením zásad skupiny.</span><span class="sxs-lookup"><span data-stu-id="c58d4-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="c58d4-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="c58d4-112">Steps:</span></span>
1. <span data-ttu-id="c58d4-113">Spusťte **Zásady skupiny editoru** – na panelu hledání spusťte příkaz upravit zásady skupiny nebo spusťte gpedit. msc z příkazu Run (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="c58d4-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="c58d4-114">V **Editor místních zásad skupiny**povolte položku místní zásady počítače/Konfigurace počítače/šablony pro správu/všechna nastavení/Povolit dlouhé cesty Win32.</span><span class="sxs-lookup"><span data-stu-id="c58d4-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Zásady dlouhých cest](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="c58d4-116">Povolení dalších nástrojů NuGet pro podporu dlouhých cest</span><span class="sxs-lookup"><span data-stu-id="c58d4-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="c58d4-117">Dotnet CLI podporuje dlouhé cesty bez ohledu na operační systém nebo verzi.</span><span class="sxs-lookup"><span data-stu-id="c58d4-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="c58d4-118">Visual Studio nebo MSBuild-t:Restore ještě nepodporuje dlouhé cesty.</span><span class="sxs-lookup"><span data-stu-id="c58d4-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="c58d4-119">Software, který používá knihovny NuGet ke spouštění obnovení a dalších příkazů, bude podporovat dlouhé cesty ke stejným systémům, na kterých funguje nástroj NuGet. exe, pokud také nastavil longPathAware v manifestu Windows a konfiguruje UseLegacyPathHandling na hodnotu false prostřednictvím App. config [. Zobrazit další informace](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="c58d4-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

