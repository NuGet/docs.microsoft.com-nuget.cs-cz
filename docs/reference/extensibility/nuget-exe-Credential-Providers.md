---
title: Poskytovatelé přihlašovacích údajů nuget.exe
description: poskytovatelé přihlašovacích údajů nuget.exe ověření prostřednictvím informačního kanálu a jsou implementované jako příkazového řádku spustitelné soubory, které dodržují konvence konkrétní prostředí.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: ebd3354c298eae8bc8158a987327374ac4a8d4f0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818757"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="d0ef6-103">Ověřování informačních kanálů s nuget.exe poskytovatelé přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="d0ef6-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="d0ef6-104">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="d0ef6-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="d0ef6-105">Když `nuget.exe` potřebuje přihlašovací údaje k ověřování pro informační kanál, vypadá pro ně následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d0ef6-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="d0ef6-106">NuGet nejprve hledá přihlašovací údaje v `Nuget.Config` soubory.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="d0ef6-107">NuGet pak použije poskytovatelé přihlašovacích údajů modul plug-in, podstoupí níže uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="d0ef6-108">(A je třeba [Visual Studio Team Services přihlašovací údaje poskytovatele](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="d0ef6-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="d0ef6-109">NuGet vyzve uživatele k zadání přihlašovacích údajů na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="d0ef6-110">Všimněte si, že poskytovatelé přihlašovacích údajů, které jsou zde popsané fungovat pouze v `nuget.exe` a není v 'dotnet obnovení, nebo Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="d0ef6-111">Poskytovatelé přihlašovacích údajů pomocí sady Visual Studio, najdete v části [nuget.exe poskytovatelé přihlašovacích údajů pro sadu Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="d0ef6-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="d0ef6-112">poskytovatelé přihlašovacích údajů nuget.exe mohou být používány 3 způsoby:</span><span class="sxs-lookup"><span data-stu-id="d0ef6-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="d0ef6-113">**Globálně**: Chcete-li k dispozici pro všechny instance poskytovatele přihlašovacích údajů `nuget.exe` běžet pod aktuální uživatelský profil, přidejte ho do `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="d0ef6-114">Budete muset vytvořit `CredentialProviders` složky.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="d0ef6-115">Poskytovatelé přihlašovacích údajů se dá nainstalovat na kořenovém `CredentialProviders` složku nebo podsložku.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="d0ef6-116">Pokud poskytovatel pověření má několik souborů nebo sestavení, můžete zachovat zprostředkovatele uspořádané podsložky.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="d0ef6-117">**Na proměnné prostředí**: poskytovatelé přihlašovacích údajů můžete uložit kdekoli a přístupné `nuget.exe` nastavením `%NUGET_CREDENTIALPROVIDERS_PATH%` proměnnou prostředí k umístění poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="d0ef6-118">Tato proměnná může být seznam oddělených středníkem (například `path1;path2`) Pokud máte více lokalit.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="d0ef6-119">**Spolu s nuget.exe**: nuget.exe poskytovatelé přihlašovacích údajů mohou být umístěny ve stejné složce jako `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="d0ef6-120">Při načítání poskytovatelé přihlašovacích údajů, `nuget.exe` hledá výše uvedené umístění, aby všechny soubory s názvem `credentialprovider*.exe`, potom se načte těchto souborů v pořadí, které se nacházejí.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="d0ef6-121">Pokud existuje více poskytovatelů pověření ve stejné složce, jsou načíst v abecedním pořadí.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="d0ef6-122">Vytvoření zprostředkovatele nuget.exe přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="d0ef6-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="d0ef6-123">Poskytovatel pověření je spustitelného souboru příkazového řádku, s názvem ve formátu `CredentialProvider*.exe`, který shromažďuje vstupy, získá přihlašovací údaje podle potřeby a vrátí ukončovací odpovídající stavový kód a standardní výstup.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="d0ef6-124">Zprostředkovatel postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="d0ef6-124">A provider must do the following:</span></span>

- <span data-ttu-id="d0ef6-125">Určí, zda může poskytnout přihlašovací údaje pro cílový identifikátor URI před zahájením získání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="d0ef6-126">Pokud ne, měla by vrátit stavovým kódem 1 bez pověření.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="d0ef6-127">Nelze změnit `Nuget.Config` (například nastavení přihlašovacích údajů existuje).</span><span class="sxs-lookup"><span data-stu-id="d0ef6-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="d0ef6-128">Popisovač HTTP konfiguraci proxy serveru na svůj vlastní jako NuGet neposkytuje informace o proxy serveru pro tento modul plug-in.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="d0ef6-129">Vrátí přihlašovací údaje nebo podrobnosti o chybě `nuget.exe` zápisem objekt odpovědi JSON (viz níže) do datového proudu stdout pomocí kódování UTF-8.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="d0ef6-130">Volitelně emitování protokolování další trasování do stderr.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="d0ef6-131">Žádné tajné klíče někdy budou zasílány do stderr, protože úrovni podrobností "normální" nebo "podrobné" takové trasování opakována rozšířením NuGet do konzoly.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="d0ef6-132">Neočekávané parametry by měl být ignorovány, poskytuje dopřednou kompatibilitu s budoucími verzemi NuGet.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0ef6-133">Vstupní parametry</span><span class="sxs-lookup"><span data-stu-id="d0ef6-133">Input parameters</span></span>

| <span data-ttu-id="d0ef6-134">Parametr/přepínače</span><span class="sxs-lookup"><span data-stu-id="d0ef6-134">Parameter/Switch</span></span> |<span data-ttu-id="d0ef6-135">Popis</span><span class="sxs-lookup"><span data-stu-id="d0ef6-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="d0ef6-136">Identifikátor URI {value}</span><span class="sxs-lookup"><span data-stu-id="d0ef6-136">Uri {value}</span></span> | <span data-ttu-id="d0ef6-137">Identifikátor URI vyžadují přihlašovací údaje ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="d0ef6-138">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="d0ef6-138">NonInteractive</span></span> | <span data-ttu-id="d0ef6-139">Pokud je k dispozici, zprostředkovatele nevydává interaktivní výzvy.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="d0ef6-140">IsRetry</span><span class="sxs-lookup"><span data-stu-id="d0ef6-140">IsRetry</span></span> | <span data-ttu-id="d0ef6-141">Pokud je k dispozici, označuje, že je tento pokus dříve neúspěšných pokusů o opakování.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="d0ef6-142">Poskytovatelé obvykle používají tento příznak k zajistěte, aby vynechat všechny existující mezipaměti a výzvu k nové přihlašovací údaje, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="d0ef6-143">Podrobností {value}</span><span class="sxs-lookup"><span data-stu-id="d0ef6-143">Verbosity {value}</span></span> | <span data-ttu-id="d0ef6-144">Pokud je k dispozici, jednu z následujících hodnot: "normální", "quiet" nebo "podrobné".</span><span class="sxs-lookup"><span data-stu-id="d0ef6-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="d0ef6-145">Pokud je zadána žádná hodnota, použije výchozí hodnota "normální".</span><span class="sxs-lookup"><span data-stu-id="d0ef6-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="d0ef6-146">Zprostředkovatelé by měl použít jako údajem o úroveň protokolování volitelné pro vydávání na standardní chybový proud.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="d0ef6-147">Kódy ukončení</span><span class="sxs-lookup"><span data-stu-id="d0ef6-147">Exit codes</span></span>

| <span data-ttu-id="d0ef6-148">Kód</span><span class="sxs-lookup"><span data-stu-id="d0ef6-148">Code</span></span> |<span data-ttu-id="d0ef6-149">Výsledek</span><span class="sxs-lookup"><span data-stu-id="d0ef6-149">Result</span></span> | <span data-ttu-id="d0ef6-150">Popis</span><span class="sxs-lookup"><span data-stu-id="d0ef6-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="d0ef6-151">0</span><span class="sxs-lookup"><span data-stu-id="d0ef6-151">0</span></span> | <span data-ttu-id="d0ef6-152">Úspěch</span><span class="sxs-lookup"><span data-stu-id="d0ef6-152">Success</span></span> | <span data-ttu-id="d0ef6-153">Přihlašovací údaje úspěšně získala a byl zapsán do stdout.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="d0ef6-154">1</span><span class="sxs-lookup"><span data-stu-id="d0ef6-154">1</span></span> | <span data-ttu-id="d0ef6-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="d0ef6-155">ProviderNotApplicable</span></span> | <span data-ttu-id="d0ef6-156">Aktuální zprostředkovatel neposkytuje přihlašovací údaje pro daný identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="d0ef6-157">2</span><span class="sxs-lookup"><span data-stu-id="d0ef6-157">2</span></span> | <span data-ttu-id="d0ef6-158">Selhání</span><span class="sxs-lookup"><span data-stu-id="d0ef6-158">Failure</span></span> | <span data-ttu-id="d0ef6-159">Zprostředkovatel je správný zprostředkovatele pro daný identifikátor URI, ale nelze poskytnout pověření.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="d0ef6-160">V takovém případě nuget.exe nebude opakovat pokus o ověření a se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="d0ef6-161">Typickým příkladem je, když uživatel zruší interaktivní přihlášení.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="d0ef6-162">Standardní výstup</span><span class="sxs-lookup"><span data-stu-id="d0ef6-162">Standard output</span></span>

| <span data-ttu-id="d0ef6-163">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="d0ef6-163">Property</span></span> |<span data-ttu-id="d0ef6-164">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d0ef6-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="d0ef6-165">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="d0ef6-165">Username</span></span> | <span data-ttu-id="d0ef6-166">Uživatelské jméno u ověřených požadavků.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="d0ef6-167">Heslo</span><span class="sxs-lookup"><span data-stu-id="d0ef6-167">Password</span></span> | <span data-ttu-id="d0ef6-168">Heslo pro ověření žádosti.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="d0ef6-169">Zpráva</span><span class="sxs-lookup"><span data-stu-id="d0ef6-169">Message</span></span> | <span data-ttu-id="d0ef6-170">Volitelné údaje o odpověď, používají pouze pro účely zobrazit další podrobnosti v případě selhání.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="d0ef6-171">Příklad stdout:</span><span class="sxs-lookup"><span data-stu-id="d0ef6-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="d0ef6-172">Řešení potíží s poskytovatel pověření</span><span class="sxs-lookup"><span data-stu-id="d0ef6-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="d0ef6-173">V současné době NuGet neposkytuje mnohem přímé podpory pro ladění zprostředkovatelů vlastní pověření; [vydání 4598](https://github.com/NuGet/Home/issues/4598) je sledování této práce.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="d0ef6-174">Můžete provést také následující:</span><span class="sxs-lookup"><span data-stu-id="d0ef6-174">You can also do the following:</span></span>

- <span data-ttu-id="d0ef6-175">Spustit nuget.exe s `-verbosity` přepínač tak, aby kontrolovat podrobný výstup.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="d0ef6-176">Přidat zprávy ladění na `stdout` příslušná místa.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="d0ef6-177">Ujistěte se, že používáte nuget.exe 3.3 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="d0ef6-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="d0ef6-178">Připojte ladicí program při spuštění s Tento fragment kódu:</span><span class="sxs-lookup"><span data-stu-id="d0ef6-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="d0ef6-179">Další informace [odeslat žádost o podporu nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="d0ef6-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
