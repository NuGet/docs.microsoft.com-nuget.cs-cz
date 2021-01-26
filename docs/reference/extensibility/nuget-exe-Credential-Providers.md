---
title: Poskytovatelé přihlašovacích údajů nuget.exe
description: nuget.exe poskytovatelé přihlašovacích údajů ověřují pomocí informačního kanálu a jsou implementovány jako spustitelné soubory příkazového řádku, které následují konkrétní konvence.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 285504508fa88c96f5c7a23f15ef14d81ebc21e1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777763"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="cb222-103">Ověřování informačních kanálů s nuget.exe zprostředkovateli přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="cb222-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="cb222-104">V `3.3` podpoře verze se přidaly pro `nuget.exe` konkrétní poskytovatele přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="cb222-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="cb222-105">Od té doby byla v `4.8` [podpoře verzí pro poskytovatele přihlašovacích údajů](NuGet-Cross-Platform-Authentication-Plugin.md) , které fungují ve všech scénářích příkazového řádku ( `nuget.exe` , `dotnet.exe` , `msbuild.exe` ), přidána.</span><span class="sxs-lookup"><span data-stu-id="cb222-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="cb222-106">Další podrobnosti o všech přístupech k ověřování pro najdete v tématu [využívání balíčků ze ověřených informačních kanálů](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) . `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="cb222-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="cb222-107">Zjišťování poskytovatele pověření nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cb222-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="cb222-108">Poskytovatelé přihlašovacích údajů nuget.exe můžou používat 3 způsoby:</span><span class="sxs-lookup"><span data-stu-id="cb222-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="cb222-109">**Globálně**: Pokud chcete poskytovatele přihlašovacích údajů zpřístupnit všem instancím `nuget.exe` běhu v profilu aktuálního uživatele, přidejte ho do `%LocalAppData%\NuGet\CredentialProviders` .</span><span class="sxs-lookup"><span data-stu-id="cb222-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="cb222-110">Možná budete muset vytvořit `CredentialProviders` složku.</span><span class="sxs-lookup"><span data-stu-id="cb222-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="cb222-111">Poskytovatelé přihlašovacích údajů se dají nainstalovat do kořenového adresáře `CredentialProviders`  složky nebo do podsložky.</span><span class="sxs-lookup"><span data-stu-id="cb222-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="cb222-112">Pokud má poskytovatel přihlašovacích údajů více souborů nebo sestavení, můžete použít podsložky a zachovat tak jejich poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="cb222-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="cb222-113">**Z proměnné prostředí**: poskytovatelé přihlašovacích údajů můžou být uložené kdekoli a zpřístupněni tak, že `nuget.exe` nastaví `%NUGET_CREDENTIALPROVIDERS_PATH%` proměnnou prostředí na umístění poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="cb222-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="cb222-114">Tato proměnná může být seznam oddělený středníkem (například), `path1;path2` Pokud máte více umístění.</span><span class="sxs-lookup"><span data-stu-id="cb222-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="cb222-115">**Vedle nuget.exe**: poskytovatelé přihlašovacích údajů nuget.exe můžou umístit do stejné složky jako `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="cb222-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="cb222-116">Při načítání zprostředkovatelů přihlašovacích údajů `nuget.exe` prohledají výše uvedená umístění v případě libovolného souboru s názvem `credentialprovider*.exe` a pak tyto soubory načte v pořadí, v jakém byly nalezeny.</span><span class="sxs-lookup"><span data-stu-id="cb222-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="cb222-117">Pokud ve stejné složce existuje více zprostředkovatelů přihlašovacích údajů, načtou se v abecedním pořadí.</span><span class="sxs-lookup"><span data-stu-id="cb222-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="cb222-118">Vytvoření poskytovatele pověření nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cb222-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="cb222-119">Poskytovatel pověření je spustitelný soubor příkazového řádku pojmenovaný ve formuláři `CredentialProvider*.exe` , který shromáždí vstupy, získá přihlašovací údaje podle potřeby a vrátí příslušný stavový kód ukončení a standardní výstup.</span><span class="sxs-lookup"><span data-stu-id="cb222-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="cb222-120">Poskytovatel musí provádět tyto akce:</span><span class="sxs-lookup"><span data-stu-id="cb222-120">A provider must do the following:</span></span>

- <span data-ttu-id="cb222-121">Před zahájením získání přihlašovacích údajů určete, jestli může poskytnout přihlašovací údaje pro cílový identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="cb222-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="cb222-122">V takovém případě by měl vrátit stavový kód 1 bez přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="cb222-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="cb222-123">Neupravovat `Nuget.Config` (jako je třeba nastavení přihlašovacích údajů).</span><span class="sxs-lookup"><span data-stu-id="cb222-123">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="cb222-124">Vlastní zpracování konfigurace proxy HTTP, protože NuGet neposkytuje informace o proxy serveru modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="cb222-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="cb222-125">Vraťte přihlašovací údaje nebo podrobnosti chyby do `nuget.exe` zápisu objektu odpovědi JSON (viz níže) do STDOUT pomocí kódování UTF-8.</span><span class="sxs-lookup"><span data-stu-id="cb222-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="cb222-126">Volitelně můžete vygenerovat další protokolování trasování do stderr.</span><span class="sxs-lookup"><span data-stu-id="cb222-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="cb222-127">Do stderr by se nikdy neměly zapisovat žádná tajná klíčová slova, protože u úrovní podrobností "normální" nebo "podrobná" jsou trasování v rámci nástroje NuGet pro konzolu odezva.</span><span class="sxs-lookup"><span data-stu-id="cb222-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="cb222-128">Neočekávané parametry by měly být ignorovány, čímž je zajištěna dopředná kompatibilita s budoucími verzemi NuGet.</span><span class="sxs-lookup"><span data-stu-id="cb222-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="cb222-129">Vstupní parametry</span><span class="sxs-lookup"><span data-stu-id="cb222-129">Input parameters</span></span>

| <span data-ttu-id="cb222-130">Parametr/Switch</span><span class="sxs-lookup"><span data-stu-id="cb222-130">Parameter/Switch</span></span> |<span data-ttu-id="cb222-131">Popis</span><span class="sxs-lookup"><span data-stu-id="cb222-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="cb222-132">Identifikátor URI {Value}</span><span class="sxs-lookup"><span data-stu-id="cb222-132">Uri {value}</span></span> | <span data-ttu-id="cb222-133">Identifikátor URI zdroje balíčku vyžaduje přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="cb222-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="cb222-134">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="cb222-134">NonInteractive</span></span> | <span data-ttu-id="cb222-135">Pokud je přítomen, zprostředkovatel nevydá interaktivní výzvy.</span><span class="sxs-lookup"><span data-stu-id="cb222-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="cb222-136">Opakování</span><span class="sxs-lookup"><span data-stu-id="cb222-136">IsRetry</span></span> | <span data-ttu-id="cb222-137">Pokud je k dispozici, znamená to, že se tento pokus pokusí o opakování dříve neúspěšného pokusu.</span><span class="sxs-lookup"><span data-stu-id="cb222-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="cb222-138">Poskytovatelé obvykle používají tento příznak k zajištění toho, aby využívali jakoukoli existující mezipaměť a zobrazila výzvu k zadání nových přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="cb222-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="cb222-139">Podrobnosti {Value}</span><span class="sxs-lookup"><span data-stu-id="cb222-139">Verbosity {value}</span></span> | <span data-ttu-id="cb222-140">Pokud je k dispozici jedna z následujících hodnot: "normální", "tichá" nebo "podrobná".</span><span class="sxs-lookup"><span data-stu-id="cb222-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="cb222-141">Pokud není zadaná žádná hodnota, použije se výchozí hodnota "Normal".</span><span class="sxs-lookup"><span data-stu-id="cb222-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="cb222-142">Poskytovatelé by ho měli používat jako indikaci úrovně volitelného protokolování, které se má vygenerovat do standardního chybového proudu.</span><span class="sxs-lookup"><span data-stu-id="cb222-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="cb222-143">Ukončovací kódy</span><span class="sxs-lookup"><span data-stu-id="cb222-143">Exit codes</span></span>

| <span data-ttu-id="cb222-144">Kód</span><span class="sxs-lookup"><span data-stu-id="cb222-144">Code</span></span> |<span data-ttu-id="cb222-145">Výsledek</span><span class="sxs-lookup"><span data-stu-id="cb222-145">Result</span></span> | <span data-ttu-id="cb222-146">Popis</span><span class="sxs-lookup"><span data-stu-id="cb222-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="cb222-147">0</span><span class="sxs-lookup"><span data-stu-id="cb222-147">0</span></span> | <span data-ttu-id="cb222-148">Success</span><span class="sxs-lookup"><span data-stu-id="cb222-148">Success</span></span> | <span data-ttu-id="cb222-149">Přihlašovací údaje byly úspěšně získány a zapsány do STDOUT.</span><span class="sxs-lookup"><span data-stu-id="cb222-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="cb222-150">1</span><span class="sxs-lookup"><span data-stu-id="cb222-150">1</span></span> | <span data-ttu-id="cb222-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="cb222-151">ProviderNotApplicable</span></span> | <span data-ttu-id="cb222-152">Aktuální zprostředkovatel neposkytuje přihlašovací údaje pro daný identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="cb222-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="cb222-153">2</span><span class="sxs-lookup"><span data-stu-id="cb222-153">2</span></span> | <span data-ttu-id="cb222-154">Selhání</span><span class="sxs-lookup"><span data-stu-id="cb222-154">Failure</span></span> | <span data-ttu-id="cb222-155">Zprostředkovatel je správného poskytovatele pro daný identifikátor URI, ale nemůže poskytnout přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="cb222-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="cb222-156">V takovém případě se nuget.exe neopakuje ověřování a nezdaří se.</span><span class="sxs-lookup"><span data-stu-id="cb222-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="cb222-157">Typickým příkladem je, že uživatel zruší interaktivní přihlášení.</span><span class="sxs-lookup"><span data-stu-id="cb222-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="cb222-158">Standardní výstup</span><span class="sxs-lookup"><span data-stu-id="cb222-158">Standard output</span></span>

| <span data-ttu-id="cb222-159">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="cb222-159">Property</span></span> |<span data-ttu-id="cb222-160">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cb222-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="cb222-161">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="cb222-161">Username</span></span> | <span data-ttu-id="cb222-162">Uživatelské jméno pro ověřené požadavky.</span><span class="sxs-lookup"><span data-stu-id="cb222-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="cb222-163">Heslo</span><span class="sxs-lookup"><span data-stu-id="cb222-163">Password</span></span> | <span data-ttu-id="cb222-164">Heslo pro ověřené požadavky.</span><span class="sxs-lookup"><span data-stu-id="cb222-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="cb222-165">Zpráva</span><span class="sxs-lookup"><span data-stu-id="cb222-165">Message</span></span> | <span data-ttu-id="cb222-166">Volitelné podrobnosti o odpovědi, které se používají jenom k zobrazení dalších podrobností v případech selhání.</span><span class="sxs-lookup"><span data-stu-id="cb222-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="cb222-167">Příklad stdout:</span><span class="sxs-lookup"><span data-stu-id="cb222-167">Example stdout:</span></span>

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="cb222-168">Řešení potíží s poskytovatelem přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="cb222-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="cb222-169">V současné době NuGet neposkytuje mnohem přímou podporu pro ladění vlastních poskytovatelů přihlašovacích údajů; Tato práce sleduje [problém 4598](https://github.com/NuGet/Home/issues/4598) .</span><span class="sxs-lookup"><span data-stu-id="cb222-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="cb222-170">Můžete také provést následující:</span><span class="sxs-lookup"><span data-stu-id="cb222-170">You can also do the following:</span></span>

- <span data-ttu-id="cb222-171">Spusťte nuget.exe s `-verbosity` přepínačem pro kontrolu podrobného výstupu.</span><span class="sxs-lookup"><span data-stu-id="cb222-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="cb222-172">Na vhodné místo přidejte zprávy pro ladění `stdout` .</span><span class="sxs-lookup"><span data-stu-id="cb222-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="cb222-173">Ujistěte se, že používáte nuget.exe 3,3 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="cb222-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="cb222-174">Připojit ladicí program při spuštění pomocí tohoto fragmentu kódu:</span><span class="sxs-lookup"><span data-stu-id="cb222-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
