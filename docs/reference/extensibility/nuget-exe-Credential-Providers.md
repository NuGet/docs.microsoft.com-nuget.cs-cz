---
title: nuget.exe zprostředkovatelů přihlašovacích údajů
description: nuget.exe přihlašovacích údajů ověřují pomocí informačního kanálu a jsou implementovány jako spustitelné soubory příkazového řádku, které dodržují konkrétní konvence.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323827"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="42e6c-103">Ověřování informačních kanálů pomocí nuget.exe zprostředkovatelů přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="42e6c-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="42e6c-104">Ve verzi `3.3` byla přidána podpora pro `nuget.exe` konkrétní zprostředkovatele přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="42e6c-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="42e6c-105">Od té doby byla přidána `4.8` [podpora verzí pro zprostředkovatele](NuGet-Cross-Platform-Authentication-Plugin.md) přihlašovacích údajů, kteří pracují ve všech scénářích příkazového řádku ( `nuget.exe` , , `dotnet.exe` `msbuild.exe` ).</span><span class="sxs-lookup"><span data-stu-id="42e6c-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="42e6c-106">Další [podrobnosti o všech přístupech k](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) ověřování najdete v tématu Využívání balíčků z ověřených informačních kanálů. `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="42e6c-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="42e6c-107">nuget.exe poskytovatele přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="42e6c-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="42e6c-108">nuget.exe přihlašovacích údajů je možné použít 3 způsoby:</span><span class="sxs-lookup"><span data-stu-id="42e6c-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="42e6c-109">**Globálně:** Pokud chcete poskytovatele přihlašovacích údajů zprostředkovatele zprostředkovatele přihlašovacích údajů zprostředkovatele identity zprostředkovatele identity spustit v rámci profilu aktuálního uživatele, přidejte `nuget.exe` ho do `%LocalAppData%\NuGet\CredentialProviders` .</span><span class="sxs-lookup"><span data-stu-id="42e6c-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="42e6c-110">Možná budete muset složku `CredentialProviders` vytvořit.</span><span class="sxs-lookup"><span data-stu-id="42e6c-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="42e6c-111">Zprostředkovatele přihlašovacích údajů je možné nainstalovat v kořenovém adresáři `CredentialProviders`  složky nebo v podsložce.</span><span class="sxs-lookup"><span data-stu-id="42e6c-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="42e6c-112">Pokud poskytovatel přihlašovacích údajů obsahuje více souborů nebo sestavení, můžete pomocí podsložek zachovat uspořádání poskytovatelů.</span><span class="sxs-lookup"><span data-stu-id="42e6c-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="42e6c-113">**Z proměnné prostředí:** Poskytovatelé přihlašovacích údajů mohou být uloženi kdekoli a zpřístupněni nastavením proměnné prostředí `nuget.exe` na umístění `%NUGET_CREDENTIALPROVIDERS_PATH%` poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="42e6c-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="42e6c-114">Tato proměnná může být seznam oddělený středníkem (například ), pokud `path1;path2` máte více umístění.</span><span class="sxs-lookup"><span data-stu-id="42e6c-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="42e6c-115">**Vedle nuget.exe**: nuget.exe zprostředkovatelé přihlašovacích údajů mohou být umístěny ve stejné složce jako `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="42e6c-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="42e6c-116">Při načítání zprostředkovatelů přihlašovacích údajů vyhledá ve výše uvedených umístěních v uvedeném pořadí libovolný soubor s názvem a pak tyto soubory načte v pořadí, v uvedeném `nuget.exe` `credentialprovider*.exe` pořadí.</span><span class="sxs-lookup"><span data-stu-id="42e6c-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="42e6c-117">Pokud ve stejné složce existuje více zprostředkovatelů přihlašovacích údajů, načítá se v abecedním pořadí.</span><span class="sxs-lookup"><span data-stu-id="42e6c-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="42e6c-118">Vytvoření zprostředkovatele nuget.exe přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="42e6c-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="42e6c-119">Zprostředkovatel přihlašovacích údajů je spustitelný soubor příkazového řádku s názvem ve formátu , který shromažďuje vstupy, získává přihlašovací údaje podle potřeby a pak vrací odpovídající stavový kód ukončení a `CredentialProvider*.exe` standardní výstup.</span><span class="sxs-lookup"><span data-stu-id="42e6c-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="42e6c-120">Poskytovatel musí provést následující akce:</span><span class="sxs-lookup"><span data-stu-id="42e6c-120">A provider must do the following:</span></span>

- <span data-ttu-id="42e6c-121">Před zahájením získání přihlašovacích údajů zjistěte, jestli může poskytnout přihlašovací údaje pro cílový identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="42e6c-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="42e6c-122">Pokud ne, měl by vrátit stavový kód 1 bez přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="42e6c-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="42e6c-123">`NuGet.Config`Neupravujte je (například nastavujte přihlašovací údaje).</span><span class="sxs-lookup"><span data-stu-id="42e6c-123">Not modify `NuGet.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="42e6c-124">Konfigurace proxy serveru HTTP je sama o sobě, protože NuGet neposkytuje informace o proxy serveru modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="42e6c-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="42e6c-125">Vraťte přihlašovací údaje nebo podrobnosti o chybě do souboru zápisem `nuget.exe` objektu odpovědi JSON (viz níže) do výstupu stdout pomocí kódování UTF-8.</span><span class="sxs-lookup"><span data-stu-id="42e6c-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="42e6c-126">Volitelně můžete do stderr generovat další protokolování trasování.</span><span class="sxs-lookup"><span data-stu-id="42e6c-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="42e6c-127">Do stderru by se nikdy neměly zapisovat žádné tajné kódy, protože nuGet na úrovni podrobností "normální" nebo "podrobné" takové trasování vyjádřuje NuGet do konzoly.</span><span class="sxs-lookup"><span data-stu-id="42e6c-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="42e6c-128">Neočekávané parametry by se měly ignorovat a zajistit dopředné kompatibility s budoucími verzemi NuGetu.</span><span class="sxs-lookup"><span data-stu-id="42e6c-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="42e6c-129">Vstupní parametry</span><span class="sxs-lookup"><span data-stu-id="42e6c-129">Input parameters</span></span>

| <span data-ttu-id="42e6c-130">Parametr/Přepínač</span><span class="sxs-lookup"><span data-stu-id="42e6c-130">Parameter/Switch</span></span> |<span data-ttu-id="42e6c-131">Description</span><span class="sxs-lookup"><span data-stu-id="42e6c-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="42e6c-132">Identifikátor URI {value}</span><span class="sxs-lookup"><span data-stu-id="42e6c-132">Uri {value}</span></span> | <span data-ttu-id="42e6c-133">Identifikátor URI zdroje balíčku, který vyžaduje přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="42e6c-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="42e6c-134">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="42e6c-134">NonInteractive</span></span> | <span data-ttu-id="42e6c-135">Pokud je k dispozici, poskytovatel nevydá interaktivní výzvy.</span><span class="sxs-lookup"><span data-stu-id="42e6c-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="42e6c-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="42e6c-136">IsRetry</span></span> | <span data-ttu-id="42e6c-137">Pokud je k dispozici, znamená to, že se jedná o pokus o opakování dříve neúspěšných pokusů.</span><span class="sxs-lookup"><span data-stu-id="42e6c-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="42e6c-138">Poskytovatelé obvykle tento příznak používají k tomu, aby zajistili, že obejití existující mezipaměti, a pokud je to možné, zobrazí se výzva k zadání nových přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="42e6c-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="42e6c-139">Podrobnost {value}</span><span class="sxs-lookup"><span data-stu-id="42e6c-139">Verbosity {value}</span></span> | <span data-ttu-id="42e6c-140">Pokud je k dispozici, jedna z následujících hodnot: "normal", "quiet" nebo "detailed".</span><span class="sxs-lookup"><span data-stu-id="42e6c-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="42e6c-141">Pokud není zadána žádná hodnota, výchozí hodnota je "normální".</span><span class="sxs-lookup"><span data-stu-id="42e6c-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="42e6c-142">Poskytovatelé by měli tuto úroveň použít jako indikaci úrovně volitelného protokolování pro vysílání do standardního chybového streamu.</span><span class="sxs-lookup"><span data-stu-id="42e6c-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="42e6c-143">Ukončovací kódy</span><span class="sxs-lookup"><span data-stu-id="42e6c-143">Exit codes</span></span>

| <span data-ttu-id="42e6c-144">Kód</span><span class="sxs-lookup"><span data-stu-id="42e6c-144">Code</span></span> |<span data-ttu-id="42e6c-145">Výsledek</span><span class="sxs-lookup"><span data-stu-id="42e6c-145">Result</span></span> | <span data-ttu-id="42e6c-146">Popis</span><span class="sxs-lookup"><span data-stu-id="42e6c-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="42e6c-147">0</span><span class="sxs-lookup"><span data-stu-id="42e6c-147">0</span></span> | <span data-ttu-id="42e6c-148">Success</span><span class="sxs-lookup"><span data-stu-id="42e6c-148">Success</span></span> | <span data-ttu-id="42e6c-149">Přihlašovací údaje se úspěšně získaly a byly zapsány do stdout.</span><span class="sxs-lookup"><span data-stu-id="42e6c-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="42e6c-150">1</span><span class="sxs-lookup"><span data-stu-id="42e6c-150">1</span></span> | <span data-ttu-id="42e6c-151">PoskytovatelNotApplicable</span><span class="sxs-lookup"><span data-stu-id="42e6c-151">ProviderNotApplicable</span></span> | <span data-ttu-id="42e6c-152">Aktuální zprostředkovatel neposkytuje přihlašovací údaje pro daný identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="42e6c-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="42e6c-153">2</span><span class="sxs-lookup"><span data-stu-id="42e6c-153">2</span></span> | <span data-ttu-id="42e6c-154">Selhání</span><span class="sxs-lookup"><span data-stu-id="42e6c-154">Failure</span></span> | <span data-ttu-id="42e6c-155">Zprostředkovatel je správným zprostředkovatelem pro daný identifikátor URI, ale nemůže zadat přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="42e6c-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="42e6c-156">V takovém případě nuget.exe nebude opakovat ověřování a selže.</span><span class="sxs-lookup"><span data-stu-id="42e6c-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="42e6c-157">Typickým příkladem je zrušení interaktivního přihlášení uživatelem.</span><span class="sxs-lookup"><span data-stu-id="42e6c-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="42e6c-158">Standardní výstup</span><span class="sxs-lookup"><span data-stu-id="42e6c-158">Standard output</span></span>

| <span data-ttu-id="42e6c-159">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="42e6c-159">Property</span></span> |<span data-ttu-id="42e6c-160">Poznámky</span><span class="sxs-lookup"><span data-stu-id="42e6c-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="42e6c-161">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="42e6c-161">Username</span></span> | <span data-ttu-id="42e6c-162">Uživatelské jméno pro ověřené požadavky.</span><span class="sxs-lookup"><span data-stu-id="42e6c-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="42e6c-163">Heslo</span><span class="sxs-lookup"><span data-stu-id="42e6c-163">Password</span></span> | <span data-ttu-id="42e6c-164">Heslo pro ověřené požadavky.</span><span class="sxs-lookup"><span data-stu-id="42e6c-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="42e6c-165">Zpráva</span><span class="sxs-lookup"><span data-stu-id="42e6c-165">Message</span></span> | <span data-ttu-id="42e6c-166">Volitelné podrobnosti o odpovědi, které slouží pouze k zobrazení dalších podrobností v případech selhání.</span><span class="sxs-lookup"><span data-stu-id="42e6c-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="42e6c-167">Příklad stdout:</span><span class="sxs-lookup"><span data-stu-id="42e6c-167">Example stdout:</span></span>

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="42e6c-168">Řešení potíží s poskytovatelem přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="42e6c-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="42e6c-169">NuGet v současné době neposkytuje přímou podporu ladění vlastních zprostředkovatelů přihlašovacích údajů. [problém 4598](https://github.com/NuGet/Home/issues/4598) tuto práci sleduje.</span><span class="sxs-lookup"><span data-stu-id="42e6c-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="42e6c-170">Můžete také provést následující:</span><span class="sxs-lookup"><span data-stu-id="42e6c-170">You can also do the following:</span></span>

- <span data-ttu-id="42e6c-171">Spusťte nuget.exe `-verbosity` přepínačem a zkontrolujte podrobný výstup.</span><span class="sxs-lookup"><span data-stu-id="42e6c-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="42e6c-172">Na příslušných místech `stdout` přidejte do souboru ladicí zprávy.</span><span class="sxs-lookup"><span data-stu-id="42e6c-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="42e6c-173">Ujistěte se, že používáte nuget.exe 3.3 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="42e6c-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="42e6c-174">Připojte ladicí program při spuštění pomocí tohoto fragmentu kódu:</span><span class="sxs-lookup"><span data-stu-id="42e6c-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
