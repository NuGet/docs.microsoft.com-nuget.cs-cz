---
title: Moduly plug-in NuGet pro různé platformy
description: Moduly plug-in pro více platforem NuGet pro NuGet. exe, dotnet. exe, MSBuild. exe a Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815303"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="3d21b-103">Moduly plug-in NuGet pro různé platformy</span><span class="sxs-lookup"><span data-stu-id="3d21b-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="3d21b-104">V balíčku NuGet 4,8 + se přidala podpora pro moduly plug-in pro různé platformy.</span><span class="sxs-lookup"><span data-stu-id="3d21b-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="3d21b-105">To bylo dosaženo vytvořením nového modelu rozšiřitelnosti modulu plug-in, který musí odpovídat striktní sadě pravidel operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="3d21b-106">Moduly plug-in jsou samostatné spustitelné soubory (runnables na světě .NET Core), které klienti NuGet spouštějí v samostatném procesu.</span><span class="sxs-lookup"><span data-stu-id="3d21b-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="3d21b-107">Jedná se o skutečný zápis jednou a spustí se modul plug-in všude.</span><span class="sxs-lookup"><span data-stu-id="3d21b-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="3d21b-108">Bude fungovat se všemi klientskými nástroji NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d21b-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="3d21b-109">Moduly plug-in můžou být buď .NET Framework (NuGet. exe, MSBuild. exe a Visual Studio), nebo .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="3d21b-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="3d21b-110">Je definovaný protokol komunikace s verzemi mezi klientem NuGet a modulem plug-in.</span><span class="sxs-lookup"><span data-stu-id="3d21b-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="3d21b-111">Během spuštění metody handshake 2 procesy vyjednají verzi protokolu.</span><span class="sxs-lookup"><span data-stu-id="3d21b-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="3d21b-112">Aby bylo možné pokrýt všechny scénáře klientských nástrojů NuGet, musí jedna z nich potřebovat .NET Framework i modul plug-in .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3d21b-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="3d21b-113">Níže jsou popsány kombinace modulů plug-in a klientů/rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3d21b-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="3d21b-114">Nástroj klienta</span><span class="sxs-lookup"><span data-stu-id="3d21b-114">Client tool</span></span>  | <span data-ttu-id="3d21b-115">Rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d21b-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="3d21b-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d21b-116">Visual Studio</span></span> | <span data-ttu-id="3d21b-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d21b-117">.NET Framework</span></span> |
| <span data-ttu-id="3d21b-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="3d21b-118">dotnet.exe</span></span> | <span data-ttu-id="3d21b-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3d21b-119">.NET Core</span></span> |
| <span data-ttu-id="3d21b-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="3d21b-120">NuGet.exe</span></span> | <span data-ttu-id="3d21b-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d21b-121">.NET Framework</span></span> |
| <span data-ttu-id="3d21b-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="3d21b-122">MSBuild.exe</span></span> | <span data-ttu-id="3d21b-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d21b-123">.NET Framework</span></span> |
| <span data-ttu-id="3d21b-124">NuGet. exe na mono</span><span class="sxs-lookup"><span data-stu-id="3d21b-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="3d21b-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d21b-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="3d21b-126">Jak to funguje</span><span class="sxs-lookup"><span data-stu-id="3d21b-126">How does it work</span></span>

<span data-ttu-id="3d21b-127">Pracovní postup vysoké úrovně lze popsat následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="3d21b-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="3d21b-128">NuGet zjišťuje dostupné moduly plug-in.</span><span class="sxs-lookup"><span data-stu-id="3d21b-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="3d21b-129">V případě potřeby bude NuGet iterovat přes moduly plug-in v pořadí podle priority a spustí je jednou.</span><span class="sxs-lookup"><span data-stu-id="3d21b-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="3d21b-130">NuGet použije první modul plug-in, který může obsluhovat požadavek.</span><span class="sxs-lookup"><span data-stu-id="3d21b-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="3d21b-131">Moduly plug-in budou vypnuty, jakmile již nebudou potřeba.</span><span class="sxs-lookup"><span data-stu-id="3d21b-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="3d21b-132">Obecné požadavky na modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-132">General plugin requirements</span></span>

<span data-ttu-id="3d21b-133">Aktuální verze protokolu je *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="3d21b-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="3d21b-134">V rámci této verze jsou požadavky následující:</span><span class="sxs-lookup"><span data-stu-id="3d21b-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="3d21b-135">Mít platná důvěryhodná sestavení podpisů Authenticode, která se budou spouštět v systému Windows a mono.</span><span class="sxs-lookup"><span data-stu-id="3d21b-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="3d21b-136">Neexistují žádné speciální požadavky na vztah důvěryhodnosti pro sestavení spuštěná v systémech Linux a Mac.</span><span class="sxs-lookup"><span data-stu-id="3d21b-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="3d21b-137">Příslušný problém</span><span class="sxs-lookup"><span data-stu-id="3d21b-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="3d21b-138">Podpora bezstavového spouštění v rámci aktuálního kontextu zabezpečení klientských nástrojů NuGet</span><span class="sxs-lookup"><span data-stu-id="3d21b-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="3d21b-139">Například klientské nástroje NuGet neuplatní zvýšení oprávnění ani další inicializaci mimo protokol plug-in, který je popsán později.</span><span class="sxs-lookup"><span data-stu-id="3d21b-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="3d21b-140">Být neinteraktivní, pokud není výslovně zadáno.</span><span class="sxs-lookup"><span data-stu-id="3d21b-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="3d21b-141">Dodržovat verzi protokolu vyjednané modulem plug-in.</span><span class="sxs-lookup"><span data-stu-id="3d21b-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="3d21b-142">Reagovat na všechny žádosti v rozumném časovém období.</span><span class="sxs-lookup"><span data-stu-id="3d21b-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="3d21b-143">Dodržet žádosti o zrušení pro jakékoli probíhající operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="3d21b-144">Technické specifikace jsou podrobněji popsány v následujících specifikacích:</span><span class="sxs-lookup"><span data-stu-id="3d21b-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="3d21b-145">Modul plug-in pro stažení balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="3d21b-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="3d21b-146">Modul plug-in NuGet pro ověřování přes NuGet</span><span class="sxs-lookup"><span data-stu-id="3d21b-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="3d21b-147">Interakce klienta s modulem plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-147">Client - Plugin interaction</span></span>

<span data-ttu-id="3d21b-148">Klientské nástroje NuGet a moduly plug-in komunikují s JSON přes standardní streamy (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="3d21b-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="3d21b-149">Všechna data musí mít kódování UTF-8.</span><span class="sxs-lookup"><span data-stu-id="3d21b-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="3d21b-150">Moduly plug-in se spustí s argumentem "-plugin".</span><span class="sxs-lookup"><span data-stu-id="3d21b-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="3d21b-151">V případě, že uživatel přímo spustí spustitelný soubor modulu plug-in bez tohoto argumentu, může modul plug-in poskytnout informativní zprávu místo čekání na protokol handshake.</span><span class="sxs-lookup"><span data-stu-id="3d21b-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="3d21b-152">Časový limit protokolu handshake je 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="3d21b-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="3d21b-153">Modul plug-in by měl dokončit instalaci v co nejkratší možné míře.</span><span class="sxs-lookup"><span data-stu-id="3d21b-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="3d21b-154">Klientské nástroje NuGet se dotazují na podporované operace modulu plug-in tak, že přejdou do indexu služby pro zdroj NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d21b-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="3d21b-155">Modul plug-in může použít index služby ke kontrole přítomnosti podporovaných typů služeb.</span><span class="sxs-lookup"><span data-stu-id="3d21b-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="3d21b-156">Komunikace mezi klientskými nástroji NuGet a modulem plug-in je obousměrná.</span><span class="sxs-lookup"><span data-stu-id="3d21b-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="3d21b-157">Každý požadavek má časový limit 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="3d21b-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="3d21b-158">Pokud by operace měly trvat déle, než by měl příslušný proces zaslat zprávu o průběhu, aby se zabránilo vypršení časového limitu žádosti. Po 1 minutách nečinnosti se modul plug-in považuje za nečinný a vypne se.</span><span class="sxs-lookup"><span data-stu-id="3d21b-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="3d21b-159">Instalace a zjišťování modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-159">Plugin installation and discovery</span></span>

<span data-ttu-id="3d21b-160">Moduly plug-in budou zjištěny prostřednictvím struktury adresáře založené na konvencích.</span><span class="sxs-lookup"><span data-stu-id="3d21b-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="3d21b-161">Scénáře CI/CD a skupiny Power Users můžou chování přepsat pomocí proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="3d21b-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="3d21b-162">Všimněte si `NUGET_NETFX_PLUGIN_PATHS` , `NUGET_NETCORE_PLUGIN_PATHS` že a jsou k dispozici pouze ve verzi 5.3 + verze nástrojů NuGet a novějších.</span><span class="sxs-lookup"><span data-stu-id="3d21b-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="3d21b-163">`NUGET_NETFX_PLUGIN_PATHS`– definuje moduly plug-in, které budou použity pomocí nástrojů založených na .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="3d21b-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="3d21b-164">Má přednost před `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="3d21b-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="3d21b-165">(Jenom NuGet verze 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="3d21b-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="3d21b-166">`NUGET_NETCORE_PLUGIN_PATHS`– definuje moduly plug-in, které budou použity nástroji založené na .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="3d21b-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="3d21b-167">Má přednost před `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="3d21b-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="3d21b-168">(Jenom NuGet verze 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="3d21b-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="3d21b-169">`NUGET_PLUGIN_PATHS`– definuje moduly plug-in, které se použijí pro tento proces NuGet, prioritní rezervované.</span><span class="sxs-lookup"><span data-stu-id="3d21b-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="3d21b-170">Pokud je tato proměnná prostředí nastavena, přepíše zjišťování na základě konvence.</span><span class="sxs-lookup"><span data-stu-id="3d21b-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="3d21b-171">Ignoruje se, pokud je zadána jedna z proměnných specifických pro rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3d21b-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="3d21b-172">User-Location, domovské umístění NuGet v `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="3d21b-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="3d21b-173">Toto umístění nelze přepsat.</span><span class="sxs-lookup"><span data-stu-id="3d21b-173">This location cannot be overriden.</span></span> <span data-ttu-id="3d21b-174">Pro moduly plug-in a .NET Framework se bude používat jiný kořenový adresář.</span><span class="sxs-lookup"><span data-stu-id="3d21b-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="3d21b-175">Rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d21b-175">Framework</span></span> | <span data-ttu-id="3d21b-176">Umístění kořenového zjišťování</span><span class="sxs-lookup"><span data-stu-id="3d21b-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="3d21b-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3d21b-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="3d21b-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d21b-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="3d21b-179">Každý modul plug-in musí být nainstalovaný ve vlastní složce.</span><span class="sxs-lookup"><span data-stu-id="3d21b-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="3d21b-180">Vstupním bodem modulu plug-in bude název nainstalované složky s příponami. dll pro .NET Core a příponou. exe pro .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3d21b-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="3d21b-181">Pro instalaci modulů plug-in není aktuálně k dispozici uživatelský scénář.</span><span class="sxs-lookup"><span data-stu-id="3d21b-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="3d21b-182">Je to tak jednoduché jako přesunutí požadovaných souborů do předem definovaného umístění.</span><span class="sxs-lookup"><span data-stu-id="3d21b-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="3d21b-183">Podporované operace</span><span class="sxs-lookup"><span data-stu-id="3d21b-183">Supported operations</span></span>

<span data-ttu-id="3d21b-184">V rámci nového protokolu plug-in jsou podporovány dvě operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="3d21b-185">Název operace</span><span class="sxs-lookup"><span data-stu-id="3d21b-185">Operation name</span></span> | <span data-ttu-id="3d21b-186">Minimální verze protokolu</span><span class="sxs-lookup"><span data-stu-id="3d21b-186">Minimum protocol version</span></span> | <span data-ttu-id="3d21b-187">Minimální verze klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="3d21b-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="3d21b-188">Stáhnout balíček</span><span class="sxs-lookup"><span data-stu-id="3d21b-188">Download Package</span></span> | <span data-ttu-id="3d21b-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3d21b-189">1.0.0</span></span> | <span data-ttu-id="3d21b-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="3d21b-190">4.3.0</span></span> |
| [<span data-ttu-id="3d21b-191">Ověřování</span><span class="sxs-lookup"><span data-stu-id="3d21b-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="3d21b-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="3d21b-192">2.0.0</span></span> | <span data-ttu-id="3d21b-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="3d21b-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="3d21b-194">Spouštění modulů plug-in v rámci správného běhu</span><span class="sxs-lookup"><span data-stu-id="3d21b-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="3d21b-195">Pro NuGet ve scénářích dotnet. exe musí být moduly plug-in v rámci tohoto konkrétního modulu runtime nástroje dotnet. exe schopné spustit.</span><span class="sxs-lookup"><span data-stu-id="3d21b-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="3d21b-196">Je na poskytovateli modulů plug-in a příjemci, aby bylo zajištěno, že se používá kompatibilní kombinace dotnet. exe/plugin.</span><span class="sxs-lookup"><span data-stu-id="3d21b-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="3d21b-197">Může dojít k potenciálnímu problému s moduly plug-in umístění uživatele, pokud se například příkaz dotnet. exe v modulu runtime 2,0 pokusí použít modul plug-in napsaný pro modul runtime 2,1.</span><span class="sxs-lookup"><span data-stu-id="3d21b-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="3d21b-198">Ukládání schopností do mezipaměti</span><span class="sxs-lookup"><span data-stu-id="3d21b-198">Capabilities caching</span></span>

<span data-ttu-id="3d21b-199">Ověření zabezpečení a vytváření instancí modulů plug-in je nákladné.</span><span class="sxs-lookup"><span data-stu-id="3d21b-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="3d21b-200">Operace stahování se provádí častěji než operace ověřování, ale průměrný uživatel NuGet má pravděpodobně pouze modul plug-in ověřování.</span><span class="sxs-lookup"><span data-stu-id="3d21b-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="3d21b-201">Pro zlepšení prostředí NuGet uloží deklarace operací pro daný požadavek do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="3d21b-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="3d21b-202">Tato mezipaměť je vázaná na jeden modul plug-in a klíč modulu plug-in je cestou k modulu plug-in a vypršení platnosti této mezipaměti schopností je 30 dní.</span><span class="sxs-lookup"><span data-stu-id="3d21b-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="3d21b-203">Mezipaměť je umístěna v `%LocalAppData%/NuGet/plugins-cache` a je přepsaná pomocí proměnné `NUGET_PLUGINS_CACHE_PATH`prostředí.</span><span class="sxs-lookup"><span data-stu-id="3d21b-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="3d21b-204">Pokud chcete vymazat tuto [mezipaměť](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jedna může spustit příkaz lokálních hodnot s `plugins-cache` možností.</span><span class="sxs-lookup"><span data-stu-id="3d21b-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="3d21b-205">Možnost `all` místní hodnoty nyní také odstraní mezipaměť modulů plug-in.</span><span class="sxs-lookup"><span data-stu-id="3d21b-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="3d21b-206">Index zpráv protokolu</span><span class="sxs-lookup"><span data-stu-id="3d21b-206">Protocol messages index</span></span>

<span data-ttu-id="3d21b-207">Zprávy verze *1.0.0* protokolu:</span><span class="sxs-lookup"><span data-stu-id="3d21b-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="3d21b-208">Zavřít</span><span class="sxs-lookup"><span data-stu-id="3d21b-208">Close</span></span>
    * <span data-ttu-id="3d21b-209">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d21b-210">Požadavek nebude obsahovat žádnou datovou část.</span><span class="sxs-lookup"><span data-stu-id="3d21b-210">The request will contain no payload</span></span>
    * <span data-ttu-id="3d21b-211">Není očekávána žádná odpověď.</span><span class="sxs-lookup"><span data-stu-id="3d21b-211">No response is expected.</span></span>  <span data-ttu-id="3d21b-212">Správná odpověď je pro proces modulu plug-in k okamžitému ukončení.</span><span class="sxs-lookup"><span data-stu-id="3d21b-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="3d21b-213">Kopírovat soubory v balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-213">Copy files in package</span></span>
    * <span data-ttu-id="3d21b-214">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d21b-215">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-215">The request will contain:</span></span>
        * <span data-ttu-id="3d21b-216">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-216">the package ID and version</span></span>
        * <span data-ttu-id="3d21b-217">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-217">the package source repository location</span></span>
        * <span data-ttu-id="3d21b-218">Cesta k cílovému adresáři</span><span class="sxs-lookup"><span data-stu-id="3d21b-218">destination directory path</span></span>
        * <span data-ttu-id="3d21b-219">výčty souborů v balíčku, které se mají zkopírovat do cesty k cílovému adresáři</span><span class="sxs-lookup"><span data-stu-id="3d21b-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="3d21b-220">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-220">A response will contain:</span></span>
        * <span data-ttu-id="3d21b-221">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d21b-222">Vyčíslitelné úplných cest pro zkopírované soubory v cílovém adresáři, pokud byla operace úspěšná.</span><span class="sxs-lookup"><span data-stu-id="3d21b-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="3d21b-223">Kopírovat soubor balíčku (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="3d21b-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="3d21b-224">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d21b-225">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-225">The request will contain:</span></span>
        * <span data-ttu-id="3d21b-226">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-226">the package ID and version</span></span>
        * <span data-ttu-id="3d21b-227">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-227">the package source repository location</span></span>
        * <span data-ttu-id="3d21b-228">Cesta k cílovému souboru</span><span class="sxs-lookup"><span data-stu-id="3d21b-228">the destination file path</span></span>
    * <span data-ttu-id="3d21b-229">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-229">A response will contain:</span></span>
        * <span data-ttu-id="3d21b-230">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="3d21b-231">Získat přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="3d21b-231">Get credentials</span></span>
    * <span data-ttu-id="3d21b-232">Směr požadavku: modul plug-in > NuGet</span><span class="sxs-lookup"><span data-stu-id="3d21b-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="3d21b-233">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-233">The request will contain:</span></span>
        * <span data-ttu-id="3d21b-234">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-234">the package source repository location</span></span>
        * <span data-ttu-id="3d21b-235">Stavový kód protokolu HTTP získaný ze zdrojového úložiště balíčku pomocí aktuálních přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="3d21b-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="3d21b-236">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-236">A response will contain:</span></span>
        * <span data-ttu-id="3d21b-237">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d21b-238">uživatelské jméno, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="3d21b-238">a username, if available</span></span>
        * <span data-ttu-id="3d21b-239">heslo, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="3d21b-239">a password, if available</span></span>

5.  <span data-ttu-id="3d21b-240">Získat soubory v balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-240">Get files in package</span></span>
    * <span data-ttu-id="3d21b-241">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d21b-242">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-242">The request will contain:</span></span>
        * <span data-ttu-id="3d21b-243">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-243">the package ID and version</span></span>
        * <span data-ttu-id="3d21b-244">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-244">the package source repository location</span></span>
    * <span data-ttu-id="3d21b-245">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-245">A response will contain:</span></span>
        * <span data-ttu-id="3d21b-246">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d21b-247">výčty cest k souborům v balíčku, pokud byla operace úspěšná</span><span class="sxs-lookup"><span data-stu-id="3d21b-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="3d21b-248">Získat deklarace operací</span><span class="sxs-lookup"><span data-stu-id="3d21b-248">Get operation claims</span></span> 
    * <span data-ttu-id="3d21b-249">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d21b-250">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-250">The request will contain:</span></span>
        * <span data-ttu-id="3d21b-251">index služby. JSON pro zdroj balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="3d21b-252">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-252">the package source repository location</span></span>
    * <span data-ttu-id="3d21b-253">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-253">A response will contain:</span></span>
        * <span data-ttu-id="3d21b-254">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d21b-255">výčtem podporovaných operací (např.: stažení balíčku), pokud operace byla úspěšná.</span><span class="sxs-lookup"><span data-stu-id="3d21b-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="3d21b-256">Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.</span><span class="sxs-lookup"><span data-stu-id="3d21b-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="3d21b-257">Tato zpráva se aktualizovala ve verzi *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="3d21b-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="3d21b-258">Je na klientovi, aby byla zachována zpětná kompatibilita.</span><span class="sxs-lookup"><span data-stu-id="3d21b-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="3d21b-259">Získat hodnotu hash balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-259">Get package hash</span></span>
    * <span data-ttu-id="3d21b-260">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d21b-261">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-261">The request will contain:</span></span>
        * <span data-ttu-id="3d21b-262">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-262">the package ID and version</span></span>
        * <span data-ttu-id="3d21b-263">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-263">the package source repository location</span></span>
        * <span data-ttu-id="3d21b-264">algoritmus hash</span><span class="sxs-lookup"><span data-stu-id="3d21b-264">the hash algorithm</span></span>
    * <span data-ttu-id="3d21b-265">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-265">A response will contain:</span></span>
        * <span data-ttu-id="3d21b-266">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d21b-267">hodnota hash souboru balíčku pomocí požadovaného algoritmu hash, pokud byla operace úspěšná</span><span class="sxs-lookup"><span data-stu-id="3d21b-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="3d21b-268">Získat verze balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-268">Get package versions</span></span>
    * <span data-ttu-id="3d21b-269">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d21b-270">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-270">The request will contain:</span></span>
        * <span data-ttu-id="3d21b-271">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-271">the package ID</span></span>
        * <span data-ttu-id="3d21b-272">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-272">the package source repository location</span></span>
    * <span data-ttu-id="3d21b-273">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-273">A response will contain:</span></span>
        * <span data-ttu-id="3d21b-274">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d21b-275">Vyčíslitelné verze balíčku, pokud byla operace úspěšná</span><span class="sxs-lookup"><span data-stu-id="3d21b-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="3d21b-276">Získat index služby</span><span class="sxs-lookup"><span data-stu-id="3d21b-276">Get service index</span></span>
    * <span data-ttu-id="3d21b-277">Směr požadavku: modul plug-in > NuGet</span><span class="sxs-lookup"><span data-stu-id="3d21b-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="3d21b-278">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-278">The request will contain:</span></span>
        * <span data-ttu-id="3d21b-279">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-279">the package source repository location</span></span>
    * <span data-ttu-id="3d21b-280">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-280">A response will contain:</span></span>
        * <span data-ttu-id="3d21b-281">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d21b-282">index služby, pokud byla operace úspěšná</span><span class="sxs-lookup"><span data-stu-id="3d21b-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="3d21b-283">Metody handshake</span><span class="sxs-lookup"><span data-stu-id="3d21b-283">Handshake</span></span>
     * <span data-ttu-id="3d21b-284">Směr požadavku:  Modul plug-in < NuGet ></span><span class="sxs-lookup"><span data-stu-id="3d21b-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="3d21b-285">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-285">The request will contain:</span></span>
         * <span data-ttu-id="3d21b-286">aktuální verze protokolu modulů plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="3d21b-287">minimální podporovaná verze protokolu modulů plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="3d21b-288">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-288">A response will contain:</span></span>
         * <span data-ttu-id="3d21b-289">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="3d21b-290">dohodnutá verze protokolu, pokud byla operace úspěšná.</span><span class="sxs-lookup"><span data-stu-id="3d21b-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="3d21b-291">V důsledku selhání dojde k ukončení modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="3d21b-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="3d21b-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="3d21b-292">Initialize</span></span>
     * <span data-ttu-id="3d21b-293">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d21b-294">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-294">The request will contain:</span></span>
         * <span data-ttu-id="3d21b-295">verze klientského nástroje NuGet</span><span class="sxs-lookup"><span data-stu-id="3d21b-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="3d21b-296">efektivní jazyk klientského nástroje NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d21b-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="3d21b-297">Toto nastavení ForceEnglishOutput se bere v úvahu při použití.</span><span class="sxs-lookup"><span data-stu-id="3d21b-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="3d21b-298">výchozí časový limit požadavku, který nahrazuje výchozí protokol.</span><span class="sxs-lookup"><span data-stu-id="3d21b-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="3d21b-299">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-299">A response will contain:</span></span>
         * <span data-ttu-id="3d21b-300">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="3d21b-301">V důsledku selhání dojde k ukončení modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="3d21b-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="3d21b-302">protokol</span><span class="sxs-lookup"><span data-stu-id="3d21b-302">Log</span></span>
     * <span data-ttu-id="3d21b-303">Směr požadavku: modul plug-in > NuGet</span><span class="sxs-lookup"><span data-stu-id="3d21b-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="3d21b-304">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-304">The request will contain:</span></span>
         * <span data-ttu-id="3d21b-305">úroveň protokolu pro požadavek</span><span class="sxs-lookup"><span data-stu-id="3d21b-305">the log level for the request</span></span>
         * <span data-ttu-id="3d21b-306">zpráva, která se má protokolovat</span><span class="sxs-lookup"><span data-stu-id="3d21b-306">a message to log</span></span>
     * <span data-ttu-id="3d21b-307">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-307">A response will contain:</span></span>
         * <span data-ttu-id="3d21b-308">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="3d21b-309">Ukončení procesu NuGetu monitorování</span><span class="sxs-lookup"><span data-stu-id="3d21b-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="3d21b-310">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d21b-311">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-311">The request will contain:</span></span>
         * <span data-ttu-id="3d21b-312">ID procesu NuGet</span><span class="sxs-lookup"><span data-stu-id="3d21b-312">the NuGet process ID</span></span>
     * <span data-ttu-id="3d21b-313">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-313">A response will contain:</span></span>
         * <span data-ttu-id="3d21b-314">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="3d21b-315">Předběžné načtení balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-315">Prefetch package</span></span>
     * <span data-ttu-id="3d21b-316">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d21b-317">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-317">The request will contain:</span></span>
         * <span data-ttu-id="3d21b-318">ID a verze balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-318">the package ID and version</span></span>
         * <span data-ttu-id="3d21b-319">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-319">the package source repository location</span></span>
     * <span data-ttu-id="3d21b-320">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-320">A response will contain:</span></span>
         * <span data-ttu-id="3d21b-321">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="3d21b-322">Nastavit přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="3d21b-322">Set credentials</span></span>
     * <span data-ttu-id="3d21b-323">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d21b-324">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-324">The request will contain:</span></span>
         * <span data-ttu-id="3d21b-325">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-325">the package source repository location</span></span>
         * <span data-ttu-id="3d21b-326">poslední známé zdrojové uživatelské jméno balíčku, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="3d21b-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="3d21b-327">poslední známé heslo zdroje balíčku, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="3d21b-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="3d21b-328">poslední známé uživatelské jméno proxy, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="3d21b-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="3d21b-329">poslední známé heslo proxy serveru, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="3d21b-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="3d21b-330">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-330">A response will contain:</span></span>
         * <span data-ttu-id="3d21b-331">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="3d21b-332">Nastavit úroveň protokolu</span><span class="sxs-lookup"><span data-stu-id="3d21b-332">Set log level</span></span>
     * <span data-ttu-id="3d21b-333">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d21b-334">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-334">The request will contain:</span></span>
         * <span data-ttu-id="3d21b-335">Výchozí úroveň protokolování</span><span class="sxs-lookup"><span data-stu-id="3d21b-335">the default log level</span></span>
     * <span data-ttu-id="3d21b-336">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-336">A response will contain:</span></span>
         * <span data-ttu-id="3d21b-337">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="3d21b-338">Zprávy verze protokolu *2.0.0*</span><span class="sxs-lookup"><span data-stu-id="3d21b-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="3d21b-339">Získat deklarace operací</span><span class="sxs-lookup"><span data-stu-id="3d21b-339">Get Operation Claims</span></span>

* <span data-ttu-id="3d21b-340">Směr požadavku:  NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d21b-341">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-341">The request will contain:</span></span>
        * <span data-ttu-id="3d21b-342">index služby. JSON pro zdroj balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="3d21b-343">umístění zdrojového úložiště balíčku</span><span class="sxs-lookup"><span data-stu-id="3d21b-343">the package source repository location</span></span>
    * <span data-ttu-id="3d21b-344">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-344">A response will contain:</span></span>
        * <span data-ttu-id="3d21b-345">kód odpovědi, který indikuje výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="3d21b-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d21b-346">výčtem podporovaných operací, pokud byla operace úspěšná.</span><span class="sxs-lookup"><span data-stu-id="3d21b-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="3d21b-347">Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.</span><span class="sxs-lookup"><span data-stu-id="3d21b-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="3d21b-348">Pokud má index služby a zdroj balíčku hodnotu null, může modul plug-in odpovědět s ověřováním.</span><span class="sxs-lookup"><span data-stu-id="3d21b-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="3d21b-349">Získat přihlašovací údaje pro ověření</span><span class="sxs-lookup"><span data-stu-id="3d21b-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="3d21b-350">Směr požadavku: NuGet – > modul plug-in</span><span class="sxs-lookup"><span data-stu-id="3d21b-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="3d21b-351">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="3d21b-351">The request will contain:</span></span>
    * <span data-ttu-id="3d21b-352">Uri</span><span class="sxs-lookup"><span data-stu-id="3d21b-352">Uri</span></span>
    * <span data-ttu-id="3d21b-353">Opakování</span><span class="sxs-lookup"><span data-stu-id="3d21b-353">isRetry</span></span>
    * <span data-ttu-id="3d21b-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3d21b-354">NonInteractive</span></span>
    * <span data-ttu-id="3d21b-355">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="3d21b-355">CanShowDialog</span></span>
* <span data-ttu-id="3d21b-356">Odpověď bude obsahovat</span><span class="sxs-lookup"><span data-stu-id="3d21b-356">A response will contain</span></span>
    * <span data-ttu-id="3d21b-357">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="3d21b-357">Username</span></span>
    * <span data-ttu-id="3d21b-358">Heslo</span><span class="sxs-lookup"><span data-stu-id="3d21b-358">Password</span></span>
    * <span data-ttu-id="3d21b-359">Message</span><span class="sxs-lookup"><span data-stu-id="3d21b-359">Message</span></span>
    * <span data-ttu-id="3d21b-360">Seznam typů ověřování</span><span class="sxs-lookup"><span data-stu-id="3d21b-360">List of Auth Types</span></span>
    * <span data-ttu-id="3d21b-361">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="3d21b-361">MessageResponseCode</span></span>
