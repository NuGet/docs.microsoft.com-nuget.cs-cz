---
title: Moduly plug-in NuGet pro různé platformy
description: Moduly plug-in pro více platforem NuGet pro NuGet. exe, dotnet. exe, MSBuild. exe a Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429106"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="d6be7-103">Moduly plug-in NuGet pro různé platformy</span><span class="sxs-lookup"><span data-stu-id="d6be7-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="d6be7-104">V balíčku NuGet 4,8 + se přidala podpora pro moduly plug-in pro různé platformy.</span><span class="sxs-lookup"><span data-stu-id="d6be7-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="d6be7-105">To bylo dosaženo vytvořením nového modelu rozšiřitelnosti modulu plug-in, který musí odpovídat striktní sadě pravidel operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="d6be7-106">Moduly plug-in jsou samostatné spustitelné soubory (runnables na světě .NET Core), které klienti NuGet spouštějí v samostatném procesu.</span><span class="sxs-lookup"><span data-stu-id="d6be7-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="d6be7-107">Jedná se o skutečný zápis jednou a spustí se modul plug-in všude.</span><span class="sxs-lookup"><span data-stu-id="d6be7-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="d6be7-108">Bude fungovat se všemi klientskými nástroji NuGet.</span><span class="sxs-lookup"><span data-stu-id="d6be7-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="d6be7-109">Moduly plug-in můžou být buď .NET Framework (NuGet. exe, MSBuild. exe a Visual Studio), nebo .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="d6be7-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="d6be7-110">Je definovaný protokol komunikace s verzemi mezi klientem NuGet a modulem plug-in.</span><span class="sxs-lookup"><span data-stu-id="d6be7-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="d6be7-111">Během spuštění metody handshake 2 procesy vyjednají verzi protokolu.</span><span class="sxs-lookup"><span data-stu-id="d6be7-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="d6be7-112">Aby bylo možné pokrýt všechny scénáře klientských nástrojů NuGet, musí jedna z nich potřebovat .NET Framework i modul plug-in .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d6be7-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="d6be7-113">Níže jsou popsány kombinace modulů plug-in a klientů/rozhraní.</span><span class="sxs-lookup"><span data-stu-id="d6be7-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="d6be7-114">Nástroj klienta</span><span class="sxs-lookup"><span data-stu-id="d6be7-114">Client tool</span></span>  | <span data-ttu-id="d6be7-115">Rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d6be7-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="d6be7-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6be7-116">Visual Studio</span></span> | <span data-ttu-id="d6be7-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d6be7-117">.NET Framework</span></span> |
| <span data-ttu-id="d6be7-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="d6be7-118">dotnet.exe</span></span> | <span data-ttu-id="d6be7-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d6be7-119">.NET Core</span></span> |
| <span data-ttu-id="d6be7-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="d6be7-120">NuGet.exe</span></span> | <span data-ttu-id="d6be7-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d6be7-121">.NET Framework</span></span> |
| <span data-ttu-id="d6be7-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="d6be7-122">MSBuild.exe</span></span> | <span data-ttu-id="d6be7-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d6be7-123">.NET Framework</span></span> |
| <span data-ttu-id="d6be7-124">NuGet. exe na mono</span><span class="sxs-lookup"><span data-stu-id="d6be7-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="d6be7-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d6be7-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="d6be7-126">Jak to funguje</span><span class="sxs-lookup"><span data-stu-id="d6be7-126">How does it work</span></span>

<span data-ttu-id="d6be7-127">Pracovní postup vysoké úrovně lze popsat následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d6be7-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="d6be7-128">NuGet zjišťuje dostupné moduly plug-in.</span><span class="sxs-lookup"><span data-stu-id="d6be7-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="d6be7-129">V případě potřeby bude NuGet iterovat přes moduly plug-in v pořadí podle priority a spustí je jednou.</span><span class="sxs-lookup"><span data-stu-id="d6be7-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="d6be7-130">NuGet použije první modul plug-in, který může obsluhovat požadavek.</span><span class="sxs-lookup"><span data-stu-id="d6be7-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="d6be7-131">Moduly plug-in budou vypnuty, jakmile již nebudou potřeba.</span><span class="sxs-lookup"><span data-stu-id="d6be7-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="d6be7-132">Obecné požadavky na modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-132">General plugin requirements</span></span>

<span data-ttu-id="d6be7-133">Aktuální verze protokolu je *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="d6be7-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="d6be7-134">V rámci této verze jsou požadavky následující:</span><span class="sxs-lookup"><span data-stu-id="d6be7-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="d6be7-135">Mít platná důvěryhodná sestavení podpisů Authenticode, která se budou spouštět v systému Windows a mono.</span><span class="sxs-lookup"><span data-stu-id="d6be7-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="d6be7-136">Neexistují žádné speciální požadavky na vztah důvěryhodnosti pro sestavení spuštěná v systémech Linux a Mac.</span><span class="sxs-lookup"><span data-stu-id="d6be7-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="d6be7-137">Příslušný problém</span><span class="sxs-lookup"><span data-stu-id="d6be7-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="d6be7-138">Podpora bezstavového spouštění v rámci aktuálního kontextu zabezpečení klientských nástrojů NuGet</span><span class="sxs-lookup"><span data-stu-id="d6be7-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="d6be7-139">Například klientské nástroje NuGet neuplatní zvýšení oprávnění ani další inicializaci mimo protokol plug-in, který je popsán později.</span><span class="sxs-lookup"><span data-stu-id="d6be7-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="d6be7-140">Být neinteraktivní, pokud není výslovně zadáno.</span><span class="sxs-lookup"><span data-stu-id="d6be7-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="d6be7-141">Dodržovat verzi protokolu vyjednané modulem plug-in.</span><span class="sxs-lookup"><span data-stu-id="d6be7-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="d6be7-142">Reagovat na všechny žádosti v rozumném časovém období.</span><span class="sxs-lookup"><span data-stu-id="d6be7-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="d6be7-143">Dodržet žádosti o zrušení pro jakékoli probíhající operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="d6be7-144">Technické specifikace jsou podrobněji popsány v následujících specifikacích:</span><span class="sxs-lookup"><span data-stu-id="d6be7-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="d6be7-145">Modul plug-in pro stažení balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="d6be7-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="d6be7-146">Modul plug-in NuGet pro ověřování přes NuGet</span><span class="sxs-lookup"><span data-stu-id="d6be7-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="d6be7-147">Interakce klienta s modulem plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-147">Client - Plugin interaction</span></span>

<span data-ttu-id="d6be7-148">Klientské nástroje NuGet a moduly plug-in komunikují s JSON přes standardní streamy (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="d6be7-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="d6be7-149">Všechna data musí mít kódování UTF-8.</span><span class="sxs-lookup"><span data-stu-id="d6be7-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="d6be7-150">Moduly plug-in se spustí s argumentem "-plugin".</span><span class="sxs-lookup"><span data-stu-id="d6be7-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="d6be7-151">V případě, že uživatel přímo spustí spustitelný soubor modulu plug-in bez tohoto argumentu, může modul plug-in poskytnout informativní zprávu místo čekání na protokol handshake.</span><span class="sxs-lookup"><span data-stu-id="d6be7-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="d6be7-152">Časový limit protokolu handshake je 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="d6be7-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="d6be7-153">Modul plug-in by měl dokončit instalaci v co nejkratší možné míře.</span><span class="sxs-lookup"><span data-stu-id="d6be7-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="d6be7-154">Klientské nástroje NuGet se dotazují na podporované operace modulu plug-in tak, že přejdou do indexu služby pro zdroj NuGet.</span><span class="sxs-lookup"><span data-stu-id="d6be7-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="d6be7-155">Modul plug-in může použít index služby ke kontrole přítomnosti podporovaných typů služeb.</span><span class="sxs-lookup"><span data-stu-id="d6be7-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="d6be7-156">Komunikace mezi klientskými nástroji NuGet a modulem plug-in je obousměrná.</span><span class="sxs-lookup"><span data-stu-id="d6be7-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="d6be7-157">Každý požadavek má časový limit 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="d6be7-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="d6be7-158">Pokud by operace měly trvat déle, než by měl příslušný proces zaslat zprávu o průběhu, aby se zabránilo vypršení časového limitu žádosti. Po 1 minutách nečinnosti se modul plug-in považuje za nečinný a vypne se.</span><span class="sxs-lookup"><span data-stu-id="d6be7-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="d6be7-159">Instalace a zjišťování modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-159">Plugin installation and discovery</span></span>

<span data-ttu-id="d6be7-160">Moduly plug-in budou zjištěny prostřednictvím struktury adresáře založené na konvencích.</span><span class="sxs-lookup"><span data-stu-id="d6be7-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="d6be7-161">Scénáře CI/CD a skupiny Power Users můžou chování přepsat pomocí proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="d6be7-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="d6be7-162">Při použití proměnných prostředí jsou povoleny pouze absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="d6be7-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="d6be7-163">Všimněte si, že `NUGET_NETFX_PLUGIN_PATHS` a `NUGET_NETCORE_PLUGIN_PATHS` jsou k dispozici pouze ve verzi 5.3 + verze nástrojů NuGet a novějších.</span><span class="sxs-lookup"><span data-stu-id="d6be7-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="d6be7-164">`NUGET_NETFX_PLUGIN_PATHS` – definuje moduly plug-in, které budou použity pomocí nástrojů založených na .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d6be7-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="d6be7-165">Má přednost před `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="d6be7-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="d6be7-166">(Jenom NuGet verze 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="d6be7-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="d6be7-167">`NUGET_NETCORE_PLUGIN_PATHS` – definuje moduly plug-in, které budou použity nástroji založené na .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="d6be7-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="d6be7-168">Má přednost před `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="d6be7-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="d6be7-169">(Jenom NuGet verze 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="d6be7-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="d6be7-170">`NUGET_PLUGIN_PATHS` – definuje moduly plug-in, které se budou používat pro tento proces NuGet, přičemž priorita zůstane zachovaná.</span><span class="sxs-lookup"><span data-stu-id="d6be7-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="d6be7-171">Pokud je tato proměnná prostředí nastavena, přepíše zjišťování na základě konvence.</span><span class="sxs-lookup"><span data-stu-id="d6be7-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="d6be7-172">Ignoruje se, pokud je zadána jedna z proměnných specifických pro rozhraní.</span><span class="sxs-lookup"><span data-stu-id="d6be7-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="d6be7-173">User-Location, domovské umístění NuGet v `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="d6be7-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="d6be7-174">Toto umístění nelze přepsat.</span><span class="sxs-lookup"><span data-stu-id="d6be7-174">This location cannot be overriden.</span></span> <span data-ttu-id="d6be7-175">Pro moduly plug-in a .NET Framework se bude používat jiný kořenový adresář.</span><span class="sxs-lookup"><span data-stu-id="d6be7-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="d6be7-176">Rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d6be7-176">Framework</span></span> | <span data-ttu-id="d6be7-177">Umístění kořenového zjišťování</span><span class="sxs-lookup"><span data-stu-id="d6be7-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="d6be7-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d6be7-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="d6be7-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d6be7-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="d6be7-180">Každý modul plug-in musí být nainstalovaný ve vlastní složce.</span><span class="sxs-lookup"><span data-stu-id="d6be7-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="d6be7-181">Vstupním bodem modulu plug-in bude název nainstalované složky s příponami. dll pro .NET Core a příponou. exe pro .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d6be7-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="d6be7-182">Pro instalaci modulů plug-in není aktuálně k dispozici uživatelský scénář.</span><span class="sxs-lookup"><span data-stu-id="d6be7-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="d6be7-183">Je to tak jednoduché jako přesunutí požadovaných souborů do předem definovaného umístění.</span><span class="sxs-lookup"><span data-stu-id="d6be7-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="d6be7-184">Podporované operace</span><span class="sxs-lookup"><span data-stu-id="d6be7-184">Supported operations</span></span>

<span data-ttu-id="d6be7-185">V rámci nového protokolu plug-in jsou podporovány dvě operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="d6be7-186">Název operace</span><span class="sxs-lookup"><span data-stu-id="d6be7-186">Operation name</span></span> | <span data-ttu-id="d6be7-187">Minimální verze protokolu</span><span class="sxs-lookup"><span data-stu-id="d6be7-187">Minimum protocol version</span></span> | <span data-ttu-id="d6be7-188">Minimální verze klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="d6be7-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="d6be7-189">Stáhnout balíček</span><span class="sxs-lookup"><span data-stu-id="d6be7-189">Download Package</span></span> | <span data-ttu-id="d6be7-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="d6be7-190">1.0.0</span></span> | <span data-ttu-id="d6be7-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="d6be7-191">4.3.0</span></span> |
| [<span data-ttu-id="d6be7-192">Ověřování</span><span class="sxs-lookup"><span data-stu-id="d6be7-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="d6be7-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d6be7-193">2.0.0</span></span> | <span data-ttu-id="d6be7-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="d6be7-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="d6be7-195">Spouštění modulů plug-in v rámci správného běhu</span><span class="sxs-lookup"><span data-stu-id="d6be7-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="d6be7-196">Pro NuGet ve scénářích dotnet. exe musí být moduly plug-in v rámci tohoto konkrétního modulu runtime nástroje dotnet. exe schopné spustit.</span><span class="sxs-lookup"><span data-stu-id="d6be7-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="d6be7-197">Je na poskytovateli modulů plug-in a příjemci, aby bylo zajištěno, že se používá kompatibilní kombinace dotnet. exe/plugin.</span><span class="sxs-lookup"><span data-stu-id="d6be7-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="d6be7-198">Může dojít k potenciálnímu problému s moduly plug-in umístění uživatele, pokud se například příkaz dotnet. exe v modulu runtime 2,0 pokusí použít modul plug-in napsaný pro modul runtime 2,1.</span><span class="sxs-lookup"><span data-stu-id="d6be7-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="d6be7-199">Ukládání schopností do mezipaměti</span><span class="sxs-lookup"><span data-stu-id="d6be7-199">Capabilities caching</span></span>

<span data-ttu-id="d6be7-200">Ověření zabezpečení a vytváření instancí modulů plug-in je nákladné.</span><span class="sxs-lookup"><span data-stu-id="d6be7-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="d6be7-201">Operace stahování se provádí častěji než operace ověřování, ale průměrný uživatel NuGet má pravděpodobně pouze modul plug-in ověřování.</span><span class="sxs-lookup"><span data-stu-id="d6be7-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="d6be7-202">Pro zlepšení prostředí NuGet uloží deklarace operací pro daný požadavek do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="d6be7-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="d6be7-203">Tato mezipaměť je vázaná na jeden modul plug-in a klíč modulu plug-in je cestou k modulu plug-in a vypršení platnosti této mezipaměti schopností je 30 dní.</span><span class="sxs-lookup"><span data-stu-id="d6be7-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="d6be7-204">Mezipaměť je umístěna v `%LocalAppData%/NuGet/plugins-cache` a bude přepsaná pomocí proměnné prostředí `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="d6be7-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="d6be7-205">Pokud chcete vymazat tuto [mezipaměť](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jedna může spustit příkaz místní hodnoty s možností `plugins-cache`.</span><span class="sxs-lookup"><span data-stu-id="d6be7-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="d6be7-206">Možnost `all` Locals nyní odstraní také mezipaměť modulů plug-in.</span><span class="sxs-lookup"><span data-stu-id="d6be7-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="d6be7-207">Index zpráv protokolu</span><span class="sxs-lookup"><span data-stu-id="d6be7-207">Protocol messages index</span></span>

<span data-ttu-id="d6be7-208">Zprávy verze *1.0.0* protokolu:</span><span class="sxs-lookup"><span data-stu-id="d6be7-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="d6be7-209">Zavřít</span><span class="sxs-lookup"><span data-stu-id="d6be7-209">Close</span></span>
    * <span data-ttu-id="d6be7-210">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d6be7-211">Požadavek nebude obsahovat žádnou datovou část.</span><span class="sxs-lookup"><span data-stu-id="d6be7-211">The request will contain no payload</span></span>
    * <span data-ttu-id="d6be7-212">Není očekávána žádná odpověď.</span><span class="sxs-lookup"><span data-stu-id="d6be7-212">No response is expected.</span></span>  <span data-ttu-id="d6be7-213">Správná odpověď je pro proces modulu plug-in k okamžitému ukončení.</span><span class="sxs-lookup"><span data-stu-id="d6be7-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="d6be7-214">Kopírovat soubory v balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-214">Copy files in package</span></span>
    * <span data-ttu-id="d6be7-215">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d6be7-216">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-216">The request will contain:</span></span>
        * <span data-ttu-id="d6be7-217">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-217">the package ID and version</span></span>
        * <span data-ttu-id="d6be7-218">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-218">the package source repository location</span></span>
        * <span data-ttu-id="d6be7-219">Cesta k cílovému adresáři</span><span class="sxs-lookup"><span data-stu-id="d6be7-219">destination directory path</span></span>
        * <span data-ttu-id="d6be7-220">výčty souborů v balíčku, které se mají zkopírovat do cesty k cílovému adresáři</span><span class="sxs-lookup"><span data-stu-id="d6be7-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="d6be7-221">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-221">A response will contain:</span></span>
        * <span data-ttu-id="d6be7-222">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d6be7-223">Vyčíslitelné úplných cest pro zkopírované soubory v cílovém adresáři, pokud byla operace úspěšná.</span><span class="sxs-lookup"><span data-stu-id="d6be7-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="d6be7-224">Kopírovat soubor balíčku (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="d6be7-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="d6be7-225">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d6be7-226">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-226">The request will contain:</span></span>
        * <span data-ttu-id="d6be7-227">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-227">the package ID and version</span></span>
        * <span data-ttu-id="d6be7-228">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-228">the package source repository location</span></span>
        * <span data-ttu-id="d6be7-229">Cesta k cílovému souboru</span><span class="sxs-lookup"><span data-stu-id="d6be7-229">the destination file path</span></span>
    * <span data-ttu-id="d6be7-230">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-230">A response will contain:</span></span>
        * <span data-ttu-id="d6be7-231">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="d6be7-232">Získat přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="d6be7-232">Get credentials</span></span>
    * <span data-ttu-id="d6be7-233">Směr požadavku: modul plug-in > NuGet</span><span class="sxs-lookup"><span data-stu-id="d6be7-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="d6be7-234">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-234">The request will contain:</span></span>
        * <span data-ttu-id="d6be7-235">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-235">the package source repository location</span></span>
        * <span data-ttu-id="d6be7-236">Stavový kód protokolu HTTP získaný ze zdrojového úložiště balíčku pomocí aktuálních přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="d6be7-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="d6be7-237">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-237">A response will contain:</span></span>
        * <span data-ttu-id="d6be7-238">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d6be7-239">uživatelské jméno, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="d6be7-239">a username, if available</span></span>
        * <span data-ttu-id="d6be7-240">heslo, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="d6be7-240">a password, if available</span></span>

5.  <span data-ttu-id="d6be7-241">Získat soubory v balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-241">Get files in package</span></span>
    * <span data-ttu-id="d6be7-242">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d6be7-243">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-243">The request will contain:</span></span>
        * <span data-ttu-id="d6be7-244">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-244">the package ID and version</span></span>
        * <span data-ttu-id="d6be7-245">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-245">the package source repository location</span></span>
    * <span data-ttu-id="d6be7-246">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-246">A response will contain:</span></span>
        * <span data-ttu-id="d6be7-247">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d6be7-248">výčty cest k souborům v balíčku, pokud byla operace úspěšná</span><span class="sxs-lookup"><span data-stu-id="d6be7-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="d6be7-249">Získat deklarace operací</span><span class="sxs-lookup"><span data-stu-id="d6be7-249">Get operation claims</span></span> 
    * <span data-ttu-id="d6be7-250">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d6be7-251">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-251">The request will contain:</span></span>
        * <span data-ttu-id="d6be7-252">index služby. JSON pro zdroj balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="d6be7-253">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-253">the package source repository location</span></span>
    * <span data-ttu-id="d6be7-254">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-254">A response will contain:</span></span>
        * <span data-ttu-id="d6be7-255">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d6be7-256">výčtem podporovaných operací (např.: stažení balíčku), pokud operace byla úspěšná.</span><span class="sxs-lookup"><span data-stu-id="d6be7-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="d6be7-257">Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.</span><span class="sxs-lookup"><span data-stu-id="d6be7-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="d6be7-258">Tato zpráva se aktualizovala ve verzi *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="d6be7-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="d6be7-259">Je na klientovi, aby byla zachována zpětná kompatibilita.</span><span class="sxs-lookup"><span data-stu-id="d6be7-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="d6be7-260">Získat hodnotu hash balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-260">Get package hash</span></span>
    * <span data-ttu-id="d6be7-261">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d6be7-262">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-262">The request will contain:</span></span>
        * <span data-ttu-id="d6be7-263">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-263">the package ID and version</span></span>
        * <span data-ttu-id="d6be7-264">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-264">the package source repository location</span></span>
        * <span data-ttu-id="d6be7-265">algoritmus hash</span><span class="sxs-lookup"><span data-stu-id="d6be7-265">the hash algorithm</span></span>
    * <span data-ttu-id="d6be7-266">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-266">A response will contain:</span></span>
        * <span data-ttu-id="d6be7-267">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d6be7-268">hodnota hash souboru balíčku pomocí požadovaného algoritmu hash, pokud byla operace úspěšná</span><span class="sxs-lookup"><span data-stu-id="d6be7-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="d6be7-269">Získat verze balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-269">Get package versions</span></span>
    * <span data-ttu-id="d6be7-270">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d6be7-271">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-271">The request will contain:</span></span>
        * <span data-ttu-id="d6be7-272">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-272">the package ID</span></span>
        * <span data-ttu-id="d6be7-273">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-273">the package source repository location</span></span>
    * <span data-ttu-id="d6be7-274">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-274">A response will contain:</span></span>
        * <span data-ttu-id="d6be7-275">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d6be7-276">Vyčíslitelné verze balíčku, pokud byla operace úspěšná</span><span class="sxs-lookup"><span data-stu-id="d6be7-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="d6be7-277">Získat index služby</span><span class="sxs-lookup"><span data-stu-id="d6be7-277">Get service index</span></span>
    * <span data-ttu-id="d6be7-278">Směr požadavku: modul plug-in > NuGet</span><span class="sxs-lookup"><span data-stu-id="d6be7-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="d6be7-279">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-279">The request will contain:</span></span>
        * <span data-ttu-id="d6be7-280">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-280">the package source repository location</span></span>
    * <span data-ttu-id="d6be7-281">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-281">A response will contain:</span></span>
        * <span data-ttu-id="d6be7-282">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d6be7-283">index služby, pokud byla operace úspěšná</span><span class="sxs-lookup"><span data-stu-id="d6be7-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="d6be7-284">Metody handshake</span><span class="sxs-lookup"><span data-stu-id="d6be7-284">Handshake</span></span>
     * <span data-ttu-id="d6be7-285">Směr požadavku: NuGet <-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="d6be7-286">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-286">The request will contain:</span></span>
         * <span data-ttu-id="d6be7-287">aktuální verze protokolu modulů plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="d6be7-288">minimální podporovaná verze protokolu modulů plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="d6be7-289">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-289">A response will contain:</span></span>
         * <span data-ttu-id="d6be7-290">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="d6be7-291">dohodnutá verze protokolu, pokud byla operace úspěšná.</span><span class="sxs-lookup"><span data-stu-id="d6be7-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="d6be7-292">V důsledku selhání dojde k ukončení modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="d6be7-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="d6be7-293">Initialize</span><span class="sxs-lookup"><span data-stu-id="d6be7-293">Initialize</span></span>
     * <span data-ttu-id="d6be7-294">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d6be7-295">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-295">The request will contain:</span></span>
         * <span data-ttu-id="d6be7-296">verze klientského nástroje NuGet</span><span class="sxs-lookup"><span data-stu-id="d6be7-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="d6be7-297">efektivní jazyk klientského nástroje NuGet.</span><span class="sxs-lookup"><span data-stu-id="d6be7-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="d6be7-298">Toto nastavení ForceEnglishOutput se bere v úvahu při použití.</span><span class="sxs-lookup"><span data-stu-id="d6be7-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="d6be7-299">výchozí časový limit požadavku, který nahrazuje výchozí protokol.</span><span class="sxs-lookup"><span data-stu-id="d6be7-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="d6be7-300">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-300">A response will contain:</span></span>
         * <span data-ttu-id="d6be7-301">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="d6be7-302">V důsledku selhání dojde k ukončení modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="d6be7-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="d6be7-303">Protokol</span><span class="sxs-lookup"><span data-stu-id="d6be7-303">Log</span></span>
     * <span data-ttu-id="d6be7-304">Směr požadavku: modul plug-in > NuGet</span><span class="sxs-lookup"><span data-stu-id="d6be7-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="d6be7-305">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-305">The request will contain:</span></span>
         * <span data-ttu-id="d6be7-306">úroveň protokolu pro požadavek</span><span class="sxs-lookup"><span data-stu-id="d6be7-306">the log level for the request</span></span>
         * <span data-ttu-id="d6be7-307">zpráva, která se má protokolovat</span><span class="sxs-lookup"><span data-stu-id="d6be7-307">a message to log</span></span>
     * <span data-ttu-id="d6be7-308">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-308">A response will contain:</span></span>
         * <span data-ttu-id="d6be7-309">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="d6be7-310">Ukončení procesu NuGetu monitorování</span><span class="sxs-lookup"><span data-stu-id="d6be7-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="d6be7-311">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d6be7-312">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-312">The request will contain:</span></span>
         * <span data-ttu-id="d6be7-313">ID procesu NuGet</span><span class="sxs-lookup"><span data-stu-id="d6be7-313">the NuGet process ID</span></span>
     * <span data-ttu-id="d6be7-314">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-314">A response will contain:</span></span>
         * <span data-ttu-id="d6be7-315">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="d6be7-316">Předběžné načtení balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-316">Prefetch package</span></span>
     * <span data-ttu-id="d6be7-317">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d6be7-318">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-318">The request will contain:</span></span>
         * <span data-ttu-id="d6be7-319">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-319">the package ID and version</span></span>
         * <span data-ttu-id="d6be7-320">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-320">the package source repository location</span></span>
     * <span data-ttu-id="d6be7-321">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-321">A response will contain:</span></span>
         * <span data-ttu-id="d6be7-322">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="d6be7-323">Nastavení přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="d6be7-323">Set credentials</span></span>
     * <span data-ttu-id="d6be7-324">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d6be7-325">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-325">The request will contain:</span></span>
         * <span data-ttu-id="d6be7-326">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-326">the package source repository location</span></span>
         * <span data-ttu-id="d6be7-327">poslední známé zdrojové uživatelské jméno balíčku, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="d6be7-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="d6be7-328">poslední známé heslo zdroje balíčku, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="d6be7-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="d6be7-329">poslední známé uživatelské jméno proxy, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="d6be7-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="d6be7-330">poslední známé heslo proxy serveru, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="d6be7-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="d6be7-331">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-331">A response will contain:</span></span>
         * <span data-ttu-id="d6be7-332">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="d6be7-333">Nastavit úroveň protokolu</span><span class="sxs-lookup"><span data-stu-id="d6be7-333">Set log level</span></span>
     * <span data-ttu-id="d6be7-334">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d6be7-335">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-335">The request will contain:</span></span>
         * <span data-ttu-id="d6be7-336">Výchozí úroveň protokolování</span><span class="sxs-lookup"><span data-stu-id="d6be7-336">the default log level</span></span>
     * <span data-ttu-id="d6be7-337">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-337">A response will contain:</span></span>
         * <span data-ttu-id="d6be7-338">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="d6be7-339">Zprávy verze protokolu *2.0.0*</span><span class="sxs-lookup"><span data-stu-id="d6be7-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="d6be7-340">Získat deklarace operací</span><span class="sxs-lookup"><span data-stu-id="d6be7-340">Get Operation Claims</span></span>

* <span data-ttu-id="d6be7-341">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d6be7-342">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-342">The request will contain:</span></span>
        * <span data-ttu-id="d6be7-343">index služby. JSON pro zdroj balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="d6be7-344">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="d6be7-344">the package source repository location</span></span>
    * <span data-ttu-id="d6be7-345">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-345">A response will contain:</span></span>
        * <span data-ttu-id="d6be7-346">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="d6be7-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d6be7-347">výčtem podporovaných operací, pokud byla operace úspěšná.</span><span class="sxs-lookup"><span data-stu-id="d6be7-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="d6be7-348">Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.</span><span class="sxs-lookup"><span data-stu-id="d6be7-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="d6be7-349">Pokud má index služby a zdroj balíčku hodnotu null, může modul plug-in odpovědět s ověřováním.</span><span class="sxs-lookup"><span data-stu-id="d6be7-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="d6be7-350">Získat přihlašovací údaje pro ověření</span><span class="sxs-lookup"><span data-stu-id="d6be7-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="d6be7-351">Směr požadavku: NuGet-> modul plug-in</span><span class="sxs-lookup"><span data-stu-id="d6be7-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="d6be7-352">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="d6be7-352">The request will contain:</span></span>
    * <span data-ttu-id="d6be7-353">Uri</span><span class="sxs-lookup"><span data-stu-id="d6be7-353">Uri</span></span>
    * <span data-ttu-id="d6be7-354">Opakování</span><span class="sxs-lookup"><span data-stu-id="d6be7-354">isRetry</span></span>
    * <span data-ttu-id="d6be7-355">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d6be7-355">NonInteractive</span></span>
    * <span data-ttu-id="d6be7-356">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="d6be7-356">CanShowDialog</span></span>
* <span data-ttu-id="d6be7-357">Odpověď bude obsahovat</span><span class="sxs-lookup"><span data-stu-id="d6be7-357">A response will contain</span></span>
    * <span data-ttu-id="d6be7-358">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="d6be7-358">Username</span></span>
    * <span data-ttu-id="d6be7-359">Heslo</span><span class="sxs-lookup"><span data-stu-id="d6be7-359">Password</span></span>
    * <span data-ttu-id="d6be7-360">Zpráva</span><span class="sxs-lookup"><span data-stu-id="d6be7-360">Message</span></span>
    * <span data-ttu-id="d6be7-361">Seznam typů ověřování</span><span class="sxs-lookup"><span data-stu-id="d6be7-361">List of Auth Types</span></span>
    * <span data-ttu-id="d6be7-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="d6be7-362">MessageResponseCode</span></span>
