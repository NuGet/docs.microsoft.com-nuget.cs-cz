---
title: Poskytovatelé přihlašovacích údajů nuget.exe
description: poskytovatelé přihlašovacích údajů nuget.exe ověřoval informační kanál a jsou implementovány jako spustitelné soubory příkazového řádku, které odpovídají konvencím konkrétní.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550186"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="43dca-103">Ověřování informačních kanálů prostřednictvím nuget.exe poskytovatelé přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="43dca-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="43dca-104">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="43dca-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="43dca-105">Když `nuget.exe` potřebuje přihlašovací údaje pro ověření pomocí informační kanál, pro ně vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="43dca-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="43dca-106">NuGet nejprve hledá přihlašovací údaje v `Nuget.Config` soubory.</span><span class="sxs-lookup"><span data-stu-id="43dca-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="43dca-107">NuGet použije poskytovatelé modul plugin přihlašovacích údajů, v souladu s níže uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="43dca-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="43dca-108">(A je příklad [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="43dca-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="43dca-109">NuGet potom zobrazí výzvu pro přihlašovací údaje na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="43dca-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="43dca-110">Všimněte si, že poskytovatelé přihlašovacích údajů je zde popsáno, fungovat pouze v `nuget.exe` a ne v "dotnet restore" nebo Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43dca-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="43dca-111">Poskytovatelé přihlašovacích údajů pomocí sady Visual Studio, naleznete v tématu [nuget.exe poskytovatelé přihlašovacích údajů pro Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="43dca-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="43dca-112">poskytovatelé přihlašovacích údajů nuget.exe dá 3 způsoby:</span><span class="sxs-lookup"><span data-stu-id="43dca-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="43dca-113">**Globálně**: zpřístupnění poskytovatele přihlašovacích údajů pro všechny výskyty `nuget.exe` běžet pod aktuální uživatelského profilu, přidejte ji do `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="43dca-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="43dca-114">Je potřeba vytvořit `CredentialProviders` složky.</span><span class="sxs-lookup"><span data-stu-id="43dca-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="43dca-115">Poskytovatelé přihlašovacích údajů se dá nainstalovat na kořenovém adresáři `CredentialProviders` složku nebo podsložku.</span><span class="sxs-lookup"><span data-stu-id="43dca-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="43dca-116">Pokud poskytovatel přihlašovacích údajů má více souborů nebo sestavení, můžete zachovat poskytovatelé uspořádané podsložky.</span><span class="sxs-lookup"><span data-stu-id="43dca-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="43dca-117">**Z proměnné prostředí**: poskytovatelé přihlašovacích údajů mohou být uložena kdekoli a tak ho zpřístupnit `nuget.exe` nastavením `%NUGET_CREDENTIALPROVIDERS_PATH%` proměnnou prostředí pro umístění poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="43dca-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="43dca-118">Tato proměnná může být seznam oddělený středníkem (například `path1;path2`) Pokud máte víc umístění.</span><span class="sxs-lookup"><span data-stu-id="43dca-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="43dca-119">**Vedle nuget.exe**: nuget.exe poskytovatelé přihlašovacích údajů mohou být umístěny ve stejné složce jako `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="43dca-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="43dca-120">Při načítání poskytovatelé přihlašovacích údajů `nuget.exe` hledá výše uvedené umístění v pořadí, pro všechny soubory s názvem `credentialprovider*.exe`, pak načte těchto souborů v pořadí, se nenašel.</span><span class="sxs-lookup"><span data-stu-id="43dca-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="43dca-121">Pokud ve stejné složce existuje více poskytovatelé přihlašovacích údajů, jsou načteny v abecedním pořadí.</span><span class="sxs-lookup"><span data-stu-id="43dca-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="43dca-122">Vytvoření poskytovatele přihlašovacích údajů nuget.exe</span><span class="sxs-lookup"><span data-stu-id="43dca-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="43dca-123">Poskytovatel přihlašovacích údajů je spustitelného souboru příkazového řádku s názvem ve formě `CredentialProvider*.exe`, který shromažďuje vstupů, získá přihlašovací údaje podle potřeby a vrátí odpovídající ukončovací kód stavu a standardní výstup.</span><span class="sxs-lookup"><span data-stu-id="43dca-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="43dca-124">Zprostředkovatel musíte udělat toto:</span><span class="sxs-lookup"><span data-stu-id="43dca-124">A provider must do the following:</span></span>

- <span data-ttu-id="43dca-125">Určení, zda může poskytnout přihlašovací údaje pro cílový identifikátor URI před zahájením získání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="43dca-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="43dca-126">Pokud ne, měla by vrátit stavový kód 1 bez pověření.</span><span class="sxs-lookup"><span data-stu-id="43dca-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="43dca-127">Nelze změnit `Nuget.Config` (například nastavení přihlašovacích údajů existuje).</span><span class="sxs-lookup"><span data-stu-id="43dca-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="43dca-128">Popisovač HTTP konfiguraci proxy serveru na svůj vlastní jako NuGet neposkytuje informace o proxy serveru pro modul plug-in.</span><span class="sxs-lookup"><span data-stu-id="43dca-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="43dca-129">Vrátí přihlašovací údaje nebo podrobnosti o chybě `nuget.exe` zápisem objektu odpovědi JSON (viz níže) do stdout, pomocí kódování UTF-8.</span><span class="sxs-lookup"><span data-stu-id="43dca-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="43dca-130">Volitelně vysílat protokolování další trasování do stderr.</span><span class="sxs-lookup"><span data-stu-id="43dca-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="43dca-131">Žádné tajných kódů mají být někdy zapisovány do stderr, protože úrovni podrobností "normální" nebo "podrobné" Tato trasování opakována balíčkem NuGet do konzoly.</span><span class="sxs-lookup"><span data-stu-id="43dca-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="43dca-132">Neočekávané parametry by měl být ignorovány, poskytuje kompatibilitu s budoucí verze balíčku nuget.</span><span class="sxs-lookup"><span data-stu-id="43dca-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="43dca-133">Vstupní parametry</span><span class="sxs-lookup"><span data-stu-id="43dca-133">Input parameters</span></span>

| <span data-ttu-id="43dca-134">Parametr/přepínače</span><span class="sxs-lookup"><span data-stu-id="43dca-134">Parameter/Switch</span></span> |<span data-ttu-id="43dca-135">Popis</span><span class="sxs-lookup"><span data-stu-id="43dca-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="43dca-136">Identifikátor URI {value}</span><span class="sxs-lookup"><span data-stu-id="43dca-136">Uri {value}</span></span> | <span data-ttu-id="43dca-137">Identifikátor URI vyžadující přihlašovací údaje ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="43dca-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="43dca-138">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="43dca-138">NonInteractive</span></span> | <span data-ttu-id="43dca-139">Pokud jsou k dispozici, nevyvolá poskytovatele interaktivní výzvy.</span><span class="sxs-lookup"><span data-stu-id="43dca-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="43dca-140">isRetry</span><span class="sxs-lookup"><span data-stu-id="43dca-140">IsRetry</span></span> | <span data-ttu-id="43dca-141">Pokud jsou k dispozici, určuje, že je tento pokus opakování dříve neúspěšném pokusu.</span><span class="sxs-lookup"><span data-stu-id="43dca-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="43dca-142">Poskytovatelé obvykle používají tento příznak zajistíte, že všechny stávající mezipaměti obejít a výzvu pro nové přihlašovací údaje, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="43dca-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="43dca-143">Úroveň podrobností {value}</span><span class="sxs-lookup"><span data-stu-id="43dca-143">Verbosity {value}</span></span> | <span data-ttu-id="43dca-144">Pokud jsou k dispozici, použijte některou z následujících hodnot: "normální", "quiet" nebo "podrobné".</span><span class="sxs-lookup"><span data-stu-id="43dca-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="43dca-145">Pokud není zadána žádná hodnota, výchozí hodnota je "normální".</span><span class="sxs-lookup"><span data-stu-id="43dca-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="43dca-146">Poskytovatelé by měl použít jako údaj o úroveň protokolování volitelné vygenerovat standardní chybový proud.</span><span class="sxs-lookup"><span data-stu-id="43dca-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="43dca-147">Kódy ukončení</span><span class="sxs-lookup"><span data-stu-id="43dca-147">Exit codes</span></span>

| <span data-ttu-id="43dca-148">Kód</span><span class="sxs-lookup"><span data-stu-id="43dca-148">Code</span></span> |<span data-ttu-id="43dca-149">Výsledek</span><span class="sxs-lookup"><span data-stu-id="43dca-149">Result</span></span> | <span data-ttu-id="43dca-150">Popis</span><span class="sxs-lookup"><span data-stu-id="43dca-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="43dca-151">0</span><span class="sxs-lookup"><span data-stu-id="43dca-151">0</span></span> | <span data-ttu-id="43dca-152">Úspěch</span><span class="sxs-lookup"><span data-stu-id="43dca-152">Success</span></span> | <span data-ttu-id="43dca-153">Přihlašovací údaje byly úspěšně získány a byl zapsán do stdout.</span><span class="sxs-lookup"><span data-stu-id="43dca-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="43dca-154">1</span><span class="sxs-lookup"><span data-stu-id="43dca-154">1</span></span> | <span data-ttu-id="43dca-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="43dca-155">ProviderNotApplicable</span></span> | <span data-ttu-id="43dca-156">Aktuální zprostředkovatel neposkytuje přihlašovací údaje pro daný identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="43dca-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="43dca-157">2</span><span class="sxs-lookup"><span data-stu-id="43dca-157">2</span></span> | <span data-ttu-id="43dca-158">selhání</span><span class="sxs-lookup"><span data-stu-id="43dca-158">Failure</span></span> | <span data-ttu-id="43dca-159">Zprostředkovatel je správný zprostředkovatele pro daný identifikátor URI, ale nemůže poskytnout přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="43dca-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="43dca-160">V takovém případě nuget.exe nebude opakovat pokus o ověření a se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="43dca-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="43dca-161">Typickým příkladem je, když uživatel zruší interaktivního přihlášení.</span><span class="sxs-lookup"><span data-stu-id="43dca-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="43dca-162">Standardní výstup</span><span class="sxs-lookup"><span data-stu-id="43dca-162">Standard output</span></span>

| <span data-ttu-id="43dca-163">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="43dca-163">Property</span></span> |<span data-ttu-id="43dca-164">Poznámky</span><span class="sxs-lookup"><span data-stu-id="43dca-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="43dca-165">uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="43dca-165">Username</span></span> | <span data-ttu-id="43dca-166">Uživatelské jméno u ověřených požadavků.</span><span class="sxs-lookup"><span data-stu-id="43dca-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="43dca-167">Heslo</span><span class="sxs-lookup"><span data-stu-id="43dca-167">Password</span></span> | <span data-ttu-id="43dca-168">Heslo pro ověření žádosti.</span><span class="sxs-lookup"><span data-stu-id="43dca-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="43dca-169">Zpráva</span><span class="sxs-lookup"><span data-stu-id="43dca-169">Message</span></span> | <span data-ttu-id="43dca-170">Volitelné podrobnosti o odpověď, slouží pouze k zobrazení dalších podrobností v případy selhání.</span><span class="sxs-lookup"><span data-stu-id="43dca-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="43dca-171">Příklad výstupu stdout:</span><span class="sxs-lookup"><span data-stu-id="43dca-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="43dca-172">Řešení potíží s poskytovatele přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="43dca-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="43dca-173">V současné době nenabízí NuGet mnohem přímou podporu pro ladění poskytovatelé přihlašovacích údajů vlastní; [vydat 4598](https://github.com/NuGet/Home/issues/4598) sleduje tuto práci.</span><span class="sxs-lookup"><span data-stu-id="43dca-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="43dca-174">Můžete také provést následující:</span><span class="sxs-lookup"><span data-stu-id="43dca-174">You can also do the following:</span></span>

- <span data-ttu-id="43dca-175">Spusťte nuget.exe s `-verbosity` přepínače ke kontrole podrobný výstup.</span><span class="sxs-lookup"><span data-stu-id="43dca-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="43dca-176">Přidat zprávy ladění k `stdout` příslušných místech.</span><span class="sxs-lookup"><span data-stu-id="43dca-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="43dca-177">Ujistěte se, že používáte nuget.exe 3.3 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="43dca-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="43dca-178">Připojte ladicí program při spuštění s tímto fragmentem kódu:</span><span class="sxs-lookup"><span data-stu-id="43dca-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="43dca-179">O další pomoc [odeslat žádost o podporu nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="43dca-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
