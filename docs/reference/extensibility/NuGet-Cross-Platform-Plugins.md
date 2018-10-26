---
title: NuGet pro různé platformy modulů plug-in
description: NuGet pro různé platformy moduly plug-in pro NuGet.exe, dotnet.exe, msbuild.exe a sady Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: fdefc5b6189051fd83b2de644080284c09dd85f4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548203"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="c5ec6-103">NuGet pro různé platformy modulů plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="c5ec6-104">Ve Správci NuGet 4.8 + byla přidána podpora pro různé platformy moduly plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="c5ec6-105">Bylo dosaženo pomocí vytvořením nový model rozšiřitelnosti modulu plug-in, obsahující tak, aby odpovídal striktní sadu pravidel operace.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="c5ec6-106">Moduly plug-in jsou samostatné spustitelné soubory (runnables ve světě .NET Core), který klienti NuGet spustit v samostatném procesu.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="c5ec6-107">To je PRAVDA zápis jednou spustit všude, kde modul plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="c5ec6-108">Bude fungovat s všechny klientské nástroje Nugetu.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="c5ec6-109">Moduly plug-in může být rozhraní .NET Framework (NuGet.exe, MSBuild.exe a sady Visual Studio) nebo .NET Core (dotnet.exe).</span><span class="sxs-lookup"><span data-stu-id="c5ec6-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="c5ec6-110">Je definovaný verzí komunikační protokol mezi klientem NuGet a modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="c5ec6-111">Během handshake spuštění 2 procesy vyjednávat verze protokolu.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="c5ec6-112">Aby bylo možné měli pokryté všechny scénáře nástroje klienta NuGet, jedna bude nutné rozhraní .NET Framework a .NET Core modul plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="c5ec6-113">Níže jsou popsány kombinace klienta a rozhraní moduly plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="c5ec6-114">Klienta nástroje</span><span class="sxs-lookup"><span data-stu-id="c5ec6-114">Client tool</span></span>  | <span data-ttu-id="c5ec6-115">Rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c5ec6-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="c5ec6-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c5ec6-116">Visual Studio</span></span> | <span data-ttu-id="c5ec6-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c5ec6-117">.NET Framework</span></span> |
| <span data-ttu-id="c5ec6-118">DotNet.exe</span><span class="sxs-lookup"><span data-stu-id="c5ec6-118">dotnet.exe</span></span> | <span data-ttu-id="c5ec6-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c5ec6-119">.NET Core</span></span> |
| <span data-ttu-id="c5ec6-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="c5ec6-120">NuGet.exe</span></span> | <span data-ttu-id="c5ec6-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c5ec6-121">.NET Framework</span></span> |
| <span data-ttu-id="c5ec6-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="c5ec6-122">MSBuild.exe</span></span> | <span data-ttu-id="c5ec6-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c5ec6-123">.NET Framework</span></span> |
| <span data-ttu-id="c5ec6-124">NuGet.exe v Mono</span><span class="sxs-lookup"><span data-stu-id="c5ec6-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="c5ec6-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c5ec6-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="c5ec6-126">Jak to funguje</span><span class="sxs-lookup"><span data-stu-id="c5ec6-126">How does it work</span></span>

<span data-ttu-id="c5ec6-127">Základní pracovní postup lze popsat následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="c5ec6-128">NuGet zjistí dostupné moduly plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="c5ec6-129">V případě potřeby NuGet provádí iterace nad moduly plug-in v pořadí podle priority a začne je jeden po druhém.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="c5ec6-130">NuGet použije první modul plug-in, která může obsluhovat žádosti.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="c5ec6-131">Moduly plug-in se ukončí, pokud už nepotřebujete.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="c5ec6-132">Modul plug-in obecné požadavky</span><span class="sxs-lookup"><span data-stu-id="c5ec6-132">General plugin requirements</span></span>

<span data-ttu-id="c5ec6-133">Je aktuální verze protokolu *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="c5ec6-134">V této verzi jsou následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="c5ec6-135">Máte platný a důvěryhodné Authenticode podpis sestavení, které poběží na Windows a Mono.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="c5ec6-136">Neexistuje žádný požadavek speciální vztahu důvěryhodnosti pro sestavení ještě spuštěna na Linuxu a Macu.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="c5ec6-137">Relevantní problém</span><span class="sxs-lookup"><span data-stu-id="c5ec6-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="c5ec6-138">Podpora bezstavové, spouští se v aktuálním kontextu zabezpečení klientských nástrojů Nugetu.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="c5ec6-139">Klientské nástroje Nugetu nebude provádět například zvýšení úrovně oprávnění nebo další inicializace mimo protokolu modulu plug-in je popsáno dále.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="c5ec6-140">Pokud není výslovně být není interaktivní.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="c5ec6-141">Proto zavázala dodržovat verze protokolu vyjednávaný modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="c5ec6-142">Reagovat na všechny požadavky v příslušném časovém období.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="c5ec6-143">Případném dalším sdílení dodržovat požadavky zrušení pro všechny probíhající operace.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="c5ec6-144">Technické specifikace je popsána podrobněji následující specifikace:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="c5ec6-145">Modul plug-in stahování balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="c5ec6-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="c5ec6-146">NuGet pro různé platformy ověřování modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="c5ec6-147">Klient – modul plug-in interakce</span><span class="sxs-lookup"><span data-stu-id="c5ec6-147">Client - Plugin interaction</span></span>

<span data-ttu-id="c5ec6-148">Klientské nástroje Nugetu a moduly plug-in komunikaci s JSON přes standardní datové proudy (stdin, stdout a stderr).</span><span class="sxs-lookup"><span data-stu-id="c5ec6-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="c5ec6-149">Všechna data musí být UTF-8.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="c5ec6-150">Moduly plug-in jsou spouštěny v argumentu "-modul plug-in".</span><span class="sxs-lookup"><span data-stu-id="c5ec6-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="c5ec6-151">V případě, že uživatel přímo spustí spustitelný soubor bez tohoto argumentu modulu plug-in, modul plug-in vám může poskytnout informativní zprávy místo abyste čekali, protokol metody handshake.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="c5ec6-152">Časový limit metody handshake protokolu je 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="c5ec6-153">Modul plug-in by se měl dokončit v nastavení jako nemá množství co nejvíc.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="c5ec6-154">Klientské nástroje Nugetu bude dotaz podporované operace modulu plug-in předáním index služby pro zdroj NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="c5ec6-155">Modul plug-in může index služby použijte ke kontrole přítomnosti podporovaných typů služeb.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="c5ec6-156">Komunikace mezi klientské nástroje Nugetu a modulu plug-in je obousměrný.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="c5ec6-157">Každá žádost má časový limit 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="c5ec6-158">Pokud máte operace trvá déle by měl odpovídající proces odeslání zprávu o průběhu chcete zabránit vypršení časového limitu žádosti. Modul plug-in po jedné minutě nečinnosti považuje za nečinné a je vypnutý.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="c5ec6-159">Instalace modulu plug-in a zjišťování</span><span class="sxs-lookup"><span data-stu-id="c5ec6-159">Plugin installation and discovery</span></span>

<span data-ttu-id="c5ec6-160">Moduly plug-in, bude zjištěno prostřednictvím založené na konvenci adresářovou strukturu.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="c5ec6-161">CI/CD scénáře IT a zkušené uživatele můžete použít proměnnou prostředí k potlačení chování.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="c5ec6-162">`NUGET_PLUGIN_PATHS` -Definuje moduly plug-in, který se použije pro tento proces NuGet, priority, které jsou vyhrazené.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="c5ec6-163">Pokud tato proměnná prostředí je nastavena, přepíše zjišťování na základě konvence.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="c5ec6-164">Umístění uživatele, NuGet domovskou místo v `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="c5ec6-165">Toto umístění nelze přepsat.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-165">This location cannot be overriden.</span></span> <span data-ttu-id="c5ec6-166">Různé kořenový adresář se použije pro moduly plug-in pro .NET Core a .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="c5ec6-167">Rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c5ec6-167">Framework</span></span> | <span data-ttu-id="c5ec6-168">Kořenový adresář zjišťování</span><span class="sxs-lookup"><span data-stu-id="c5ec6-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="c5ec6-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c5ec6-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="c5ec6-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c5ec6-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="c5ec6-171">Každý modul plug-in musí být nainstalován ve vlastní složce.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="c5ec6-172">Vstupní bod modulu plug-in bude název nainstalovaných složku s příponou DLL pro .NET Core a příponou .exe pro rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="c5ec6-173">Aktuálně neexistuje žádný uživatelský scénář pro instalaci na moduly plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="c5ec6-174">Je snadné – stačí přesunu požadované soubory do předem umístění.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="c5ec6-175">Podporované operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-175">Supported operations</span></span>

<span data-ttu-id="c5ec6-176">Dvě operace jsou podporovány v rámci nového modulu plug-in protokolu.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="c5ec6-177">Název operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-177">Operation name</span></span> | <span data-ttu-id="c5ec6-178">Protokol minimální verze</span><span class="sxs-lookup"><span data-stu-id="c5ec6-178">Minimum protocol version</span></span> | <span data-ttu-id="c5ec6-179">Minimální verzi klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="c5ec6-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="c5ec6-180">Stáhněte si balíček</span><span class="sxs-lookup"><span data-stu-id="c5ec6-180">Download Package</span></span> | <span data-ttu-id="c5ec6-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c5ec6-181">1.0.0</span></span> | <span data-ttu-id="c5ec6-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="c5ec6-182">4.3.0</span></span> |
| [<span data-ttu-id="c5ec6-183">Ověřování</span><span class="sxs-lookup"><span data-stu-id="c5ec6-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="c5ec6-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="c5ec6-184">2.0.0</span></span> | <span data-ttu-id="c5ec6-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="c5ec6-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="c5ec6-186">S moduly plug-in v rámci správné modulu runtime</span><span class="sxs-lookup"><span data-stu-id="c5ec6-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="c5ec6-187">Moduly plug-in pro NuGet ve scénářích dotnet.exe, musí být moci být prováděny v rámci tohoto konkrétního modulu runtime dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="c5ec6-188">Je na modul plug-in zprostředkovatele a spotřebitele Ujistěte se, že se používá dotnet.exe/plugin kompatibilní kombinace.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="c5ec6-189">Potenciální problém může vzniknout s moduly plug-in umístění uživatele, když například, dotnet.exe v rámci 2.0 modulu runtime se pokusí použít modul plug-in napsané pro modul runtime 2.1.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="c5ec6-190">Možnosti ukládání do mezipaměti</span><span class="sxs-lookup"><span data-stu-id="c5ec6-190">Capabilities caching</span></span>

<span data-ttu-id="c5ec6-191">Ověření zabezpečení a vytvoření instance na moduly plug-in je nákladné.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="c5ec6-192">Operace stahování se stane způsobem častěji než operaci ověřování, ale Průměrný uživatel NuGet je pouze nejspíš ověřování modul plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="c5ec6-193">Vylepšit celkovou funkčnost, bude mezipaměti NuGet deklarace operací pro danou žádost.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="c5ec6-194">Tato mezipaměť je každý modul plug-in s klíčem modul plug-in se cesta modulu plug-in a vypršení platnosti pro mezipaměť této možnosti je 30 dní.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="c5ec6-195">Mezipaměť se nachází v `%LocalAppData%/NuGet/plugins-cache` a být monitorconfigurationoverride proměnnou prostředí `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="c5ec6-196">Vymazat tím [mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jedno spuštění lokální příkaz `plugins-cache` možnost.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="c5ec6-197">`all` Možnost místní hodnoty nyní také odstraní mezipaměti moduly plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="c5ec6-198">Index zprávy protokolu</span><span class="sxs-lookup"><span data-stu-id="c5ec6-198">Protocol messages index</span></span>

<span data-ttu-id="c5ec6-199">Verze protokolu *1.0.0* zprávy:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="c5ec6-200">Zavřít</span><span class="sxs-lookup"><span data-stu-id="c5ec6-200">Close</span></span>
    * <span data-ttu-id="c5ec6-201">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c5ec6-202">Požadavek bude obsahovat žádné datové části</span><span class="sxs-lookup"><span data-stu-id="c5ec6-202">The request will contain no payload</span></span>
    * <span data-ttu-id="c5ec6-203">Není očekávána žádná odpověď.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-203">No response is expected.</span></span>  <span data-ttu-id="c5ec6-204">Správné odpovědi je pro proces modulu plug-in k okamžitému ukončení.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="c5ec6-205">Kopírování souborů v balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-205">Copy files in package</span></span>
    * <span data-ttu-id="c5ec6-206">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c5ec6-207">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-207">The request will contain:</span></span>
        * <span data-ttu-id="c5ec6-208">ID balíčku a verzi</span><span class="sxs-lookup"><span data-stu-id="c5ec6-208">the package ID and version</span></span>
        * <span data-ttu-id="c5ec6-209">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-209">the package source repository location</span></span>
        * <span data-ttu-id="c5ec6-210">cílový adresář</span><span class="sxs-lookup"><span data-stu-id="c5ec6-210">destination directory path</span></span>
        * <span data-ttu-id="c5ec6-211">Výčtový objekt souborů v balíčku budou zkopírovány do cílovou cestu adresáře</span><span class="sxs-lookup"><span data-stu-id="c5ec6-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="c5ec6-212">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-212">A response will contain:</span></span>
        * <span data-ttu-id="c5ec6-213">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c5ec6-214">Výčtový objekt úplné cesty pro zkopírované soubory v cílovém adresáři, pokud operace byla úspěšná</span><span class="sxs-lookup"><span data-stu-id="c5ec6-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="c5ec6-215">Zkopírujte soubor balíčku (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="c5ec6-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="c5ec6-216">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c5ec6-217">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-217">The request will contain:</span></span>
        * <span data-ttu-id="c5ec6-218">ID balíčku a verzi</span><span class="sxs-lookup"><span data-stu-id="c5ec6-218">the package ID and version</span></span>
        * <span data-ttu-id="c5ec6-219">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-219">the package source repository location</span></span>
        * <span data-ttu-id="c5ec6-220">Cesta k cílovému souboru</span><span class="sxs-lookup"><span data-stu-id="c5ec6-220">the destination file path</span></span>
    * <span data-ttu-id="c5ec6-221">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-221">A response will contain:</span></span>
        * <span data-ttu-id="c5ec6-222">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="c5ec6-223">Získání přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="c5ec6-223">Get credentials</span></span>
    * <span data-ttu-id="c5ec6-224">Požádat o směr: modul plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="c5ec6-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="c5ec6-225">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-225">The request will contain:</span></span>
        * <span data-ttu-id="c5ec6-226">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-226">the package source repository location</span></span>
        * <span data-ttu-id="c5ec6-227">Stavový kód HTTP získané z úložiště zdroje balíčků pomocí aktuální přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="c5ec6-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="c5ec6-228">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-228">A response will contain:</span></span>
        * <span data-ttu-id="c5ec6-229">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c5ec6-230">uživatelské jméno, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="c5ec6-230">a username, if available</span></span>
        * <span data-ttu-id="c5ec6-231">heslo, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="c5ec6-231">a password, if available</span></span>

5.  <span data-ttu-id="c5ec6-232">Získání souborů v balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-232">Get files in package</span></span>
    * <span data-ttu-id="c5ec6-233">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c5ec6-234">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-234">The request will contain:</span></span>
        * <span data-ttu-id="c5ec6-235">ID balíčku a verzi</span><span class="sxs-lookup"><span data-stu-id="c5ec6-235">the package ID and version</span></span>
        * <span data-ttu-id="c5ec6-236">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-236">the package source repository location</span></span>
    * <span data-ttu-id="c5ec6-237">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-237">A response will contain:</span></span>
        * <span data-ttu-id="c5ec6-238">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c5ec6-239">Výčtový objekt cesty k souborům v balíčku, pokud operace byla úspěšná</span><span class="sxs-lookup"><span data-stu-id="c5ec6-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="c5ec6-240">Získat deklarace operací</span><span class="sxs-lookup"><span data-stu-id="c5ec6-240">Get operation claims</span></span> 
    * <span data-ttu-id="c5ec6-241">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c5ec6-242">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-242">The request will contain:</span></span>
        * <span data-ttu-id="c5ec6-243">Služba index.json zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="c5ec6-244">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-244">the package source repository location</span></span>
    * <span data-ttu-id="c5ec6-245">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-245">A response will contain:</span></span>
        * <span data-ttu-id="c5ec6-246">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c5ec6-247">Výčtový objekt podporované operace (např: stahování balíčku) Pokud operace byla úspěšná.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="c5ec6-248">Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="c5ec6-249">Aktualizovali jsme tuto zprávu ve verzi *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="c5ec6-250">Je na klientovi pro zachování zpětné kompatibility.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="c5ec6-251">Získá hodnotu hash balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-251">Get package hash</span></span>
    * <span data-ttu-id="c5ec6-252">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c5ec6-253">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-253">The request will contain:</span></span>
        * <span data-ttu-id="c5ec6-254">ID balíčku a verzi</span><span class="sxs-lookup"><span data-stu-id="c5ec6-254">the package ID and version</span></span>
        * <span data-ttu-id="c5ec6-255">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-255">the package source repository location</span></span>
        * <span data-ttu-id="c5ec6-256">Hashovací algoritmus</span><span class="sxs-lookup"><span data-stu-id="c5ec6-256">the hash algorithm</span></span>
    * <span data-ttu-id="c5ec6-257">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-257">A response will contain:</span></span>
        * <span data-ttu-id="c5ec6-258">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c5ec6-259">Hodnota hash souboru balíčku pomocí požadované hashovacího algoritmu, pokud operace byla úspěšná</span><span class="sxs-lookup"><span data-stu-id="c5ec6-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="c5ec6-260">Získání verze balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-260">Get package versions</span></span>
    * <span data-ttu-id="c5ec6-261">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c5ec6-262">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-262">The request will contain:</span></span>
        * <span data-ttu-id="c5ec6-263">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-263">the package ID</span></span>
        * <span data-ttu-id="c5ec6-264">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-264">the package source repository location</span></span>
    * <span data-ttu-id="c5ec6-265">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-265">A response will contain:</span></span>
        * <span data-ttu-id="c5ec6-266">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c5ec6-267">Výčtový objekt verze balíčku, pokud operace byla úspěšná</span><span class="sxs-lookup"><span data-stu-id="c5ec6-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="c5ec6-268">Získat index služby</span><span class="sxs-lookup"><span data-stu-id="c5ec6-268">Get service index</span></span>
    * <span data-ttu-id="c5ec6-269">Požádat o směr: modul plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="c5ec6-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="c5ec6-270">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-270">The request will contain:</span></span>
        * <span data-ttu-id="c5ec6-271">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-271">the package source repository location</span></span>
    * <span data-ttu-id="c5ec6-272">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-272">A response will contain:</span></span>
        * <span data-ttu-id="c5ec6-273">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c5ec6-274">index služby, pokud operace byla úspěšná</span><span class="sxs-lookup"><span data-stu-id="c5ec6-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="c5ec6-275">Metoda Handshake</span><span class="sxs-lookup"><span data-stu-id="c5ec6-275">Handshake</span></span>
     * <span data-ttu-id="c5ec6-276">Požádat o směr: NuGet <> – modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="c5ec6-277">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-277">The request will contain:</span></span>
         * <span data-ttu-id="c5ec6-278">aktuální verze protokolu modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="c5ec6-279">Minimální podporovaná verze protokolu modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="c5ec6-280">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-280">A response will contain:</span></span>
         * <span data-ttu-id="c5ec6-281">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="c5ec6-282">vyjednávaný protocol verze, pokud byla operace úspěšná.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="c5ec6-283">Selhání způsobí ukončení modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="c5ec6-284">Inicializace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-284">Initialize</span></span>
     * <span data-ttu-id="c5ec6-285">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c5ec6-286">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-286">The request will contain:</span></span>
         * <span data-ttu-id="c5ec6-287">Nástroj pro verzi klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="c5ec6-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="c5ec6-288">jazyk efektivní klienta nástroje NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="c5ec6-289">To vezme v úvahu ForceEnglishOutput nastavení, pokud se používá.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="c5ec6-290">Výchozí časový limit požadavku, která nahrazuje výchozí protokolu.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="c5ec6-291">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-291">A response will contain:</span></span>
         * <span data-ttu-id="c5ec6-292">Kód odpovědi udávající výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="c5ec6-293">Selhání způsobí ukončení modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="c5ec6-294">protokol</span><span class="sxs-lookup"><span data-stu-id="c5ec6-294">Log</span></span>
     * <span data-ttu-id="c5ec6-295">Požádat o směr: modul plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="c5ec6-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="c5ec6-296">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-296">The request will contain:</span></span>
         * <span data-ttu-id="c5ec6-297">úroveň protokolu pro žádost</span><span class="sxs-lookup"><span data-stu-id="c5ec6-297">the log level for the request</span></span>
         * <span data-ttu-id="c5ec6-298">zaznamenávané zprávy</span><span class="sxs-lookup"><span data-stu-id="c5ec6-298">a message to log</span></span>
     * <span data-ttu-id="c5ec6-299">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-299">A response will contain:</span></span>
         * <span data-ttu-id="c5ec6-300">Kód odpovědi udávající výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="c5ec6-301">Ukončení procesu monitorování NuGet</span><span class="sxs-lookup"><span data-stu-id="c5ec6-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="c5ec6-302">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c5ec6-303">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-303">The request will contain:</span></span>
         * <span data-ttu-id="c5ec6-304">ID procesu NuGet</span><span class="sxs-lookup"><span data-stu-id="c5ec6-304">the NuGet process ID</span></span>
     * <span data-ttu-id="c5ec6-305">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-305">A response will contain:</span></span>
         * <span data-ttu-id="c5ec6-306">Kód odpovědi udávající výsledek operace.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="c5ec6-307">Předběžné načtení balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-307">Prefetch package</span></span>
     * <span data-ttu-id="c5ec6-308">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c5ec6-309">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-309">The request will contain:</span></span>
         * <span data-ttu-id="c5ec6-310">ID balíčku a verzi</span><span class="sxs-lookup"><span data-stu-id="c5ec6-310">the package ID and version</span></span>
         * <span data-ttu-id="c5ec6-311">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-311">the package source repository location</span></span>
     * <span data-ttu-id="c5ec6-312">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-312">A response will contain:</span></span>
         * <span data-ttu-id="c5ec6-313">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="c5ec6-314">Nastavení přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="c5ec6-314">Set credentials</span></span>
     * <span data-ttu-id="c5ec6-315">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c5ec6-316">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-316">The request will contain:</span></span>
         * <span data-ttu-id="c5ec6-317">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-317">the package source repository location</span></span>
         * <span data-ttu-id="c5ec6-318">poslední známý balíček zdroj uživatelské jméno, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="c5ec6-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="c5ec6-319">poslední známý zdroj heslo balíčku, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="c5ec6-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="c5ec6-320">poslední známé proxy uživatelské jméno, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="c5ec6-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="c5ec6-321">poslední známé heslo k proxy serveru, pokud je k dispozici</span><span class="sxs-lookup"><span data-stu-id="c5ec6-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="c5ec6-322">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-322">A response will contain:</span></span>
         * <span data-ttu-id="c5ec6-323">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="c5ec6-324">Úroveň protokolu sady</span><span class="sxs-lookup"><span data-stu-id="c5ec6-324">Set log level</span></span>
     * <span data-ttu-id="c5ec6-325">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c5ec6-326">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-326">The request will contain:</span></span>
         * <span data-ttu-id="c5ec6-327">Výchozí úroveň protokolování</span><span class="sxs-lookup"><span data-stu-id="c5ec6-327">the default log level</span></span>
     * <span data-ttu-id="c5ec6-328">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-328">A response will contain:</span></span>
         * <span data-ttu-id="c5ec6-329">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="c5ec6-330">Verze protokolu *2.0.0* zprávy</span><span class="sxs-lookup"><span data-stu-id="c5ec6-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="c5ec6-331">Získat deklarace operací</span><span class="sxs-lookup"><span data-stu-id="c5ec6-331">Get Operation Claims</span></span>

* <span data-ttu-id="c5ec6-332">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c5ec6-333">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-333">The request will contain:</span></span>
        * <span data-ttu-id="c5ec6-334">Služba index.json zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="c5ec6-335">umístění úložiště zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ec6-335">the package source repository location</span></span>
    * <span data-ttu-id="c5ec6-336">Odpověď bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-336">A response will contain:</span></span>
        * <span data-ttu-id="c5ec6-337">Kód odpovědi udávající výsledek operace</span><span class="sxs-lookup"><span data-stu-id="c5ec6-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c5ec6-338">Výčtový objekt podporované operace, pokud byla operace úspěšná.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="c5ec6-339">Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="c5ec6-340">Pokud zdroj index a balíček služby mají hodnotu null, modul plug-in lze odpovědět pomocí ověřování.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="c5ec6-341">Získání přihlašovacích údajů pro ověřování</span><span class="sxs-lookup"><span data-stu-id="c5ec6-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="c5ec6-342">Požádat o směr: NuGet -> modulu plug-in</span><span class="sxs-lookup"><span data-stu-id="c5ec6-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="c5ec6-343">Požadavek bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="c5ec6-343">The request will contain:</span></span>
    * <span data-ttu-id="c5ec6-344">Identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="c5ec6-344">Uri</span></span>
    * <span data-ttu-id="c5ec6-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="c5ec6-345">isRetry</span></span>
    * <span data-ttu-id="c5ec6-346">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="c5ec6-346">NonInteractive</span></span>
    * <span data-ttu-id="c5ec6-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="c5ec6-347">CanShowDialog</span></span>
* <span data-ttu-id="c5ec6-348">Odpověď bude obsahovat.</span><span class="sxs-lookup"><span data-stu-id="c5ec6-348">A response will contain</span></span>
    * <span data-ttu-id="c5ec6-349">uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="c5ec6-349">Username</span></span>
    * <span data-ttu-id="c5ec6-350">Heslo</span><span class="sxs-lookup"><span data-stu-id="c5ec6-350">Password</span></span>
    * <span data-ttu-id="c5ec6-351">Zpráva</span><span class="sxs-lookup"><span data-stu-id="c5ec6-351">Message</span></span>
    * <span data-ttu-id="c5ec6-352">Seznam typů ověřování</span><span class="sxs-lookup"><span data-stu-id="c5ec6-352">List of Auth Types</span></span>
    * <span data-ttu-id="c5ec6-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="c5ec6-353">MessageResponseCode</span></span>