---
title: Zpráva k vydání verze NuGet 4.9 RTM
description: Zpráva k vydání verze pro NuGet 4.9 včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735133"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="c2027-103">Zpráva k vydání verze 4.9 NuGet</span><span class="sxs-lookup"><span data-stu-id="c2027-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="c2027-104">Distribuce vozidel NuGet:</span><span class="sxs-lookup"><span data-stu-id="c2027-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="c2027-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="c2027-105">NuGet version</span></span> | <span data-ttu-id="c2027-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c2027-106">Available in Visual Studio version</span></span>| <span data-ttu-id="c2027-107">K dispozici v rozhraní .NET SDK, pomocí kterých</span><span class="sxs-lookup"><span data-stu-id="c2027-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| <span data-ttu-id="c2027-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="c2027-108">**4.9.0**</span></span> | <span data-ttu-id="c2027-109">Visual Studio 2017 verze 15.9.0</span><span class="sxs-lookup"><span data-stu-id="c2027-109">Visual Studio 2017 version 15.9.0</span></span> | <span data-ttu-id="c2027-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="c2027-110">2.1.500, 2.2.100</span></span> |
| <span data-ttu-id="c2027-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="c2027-111">**4.9.1**</span></span> | <span data-ttu-id="c2027-112">není k dispozici</span><span class="sxs-lookup"><span data-stu-id="c2027-112">n/a</span></span> | <span data-ttu-id="c2027-113">není k dispozici</span><span class="sxs-lookup"><span data-stu-id="c2027-113">n/a</span></span> |
| [<span data-ttu-id="c2027-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="c2027-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="c2027-115">Visual Studio 2017 verze 15.9.4</span><span class="sxs-lookup"><span data-stu-id="c2027-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="c2027-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="c2027-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a><span data-ttu-id="c2027-117">Shrnutí: Co je nového v 4.9.0</span><span class="sxs-lookup"><span data-stu-id="c2027-117">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="c2027-118">Podpis: Povolit ClientPolicies vyžadují použití sady úložišť uvedené v souboru NuGet.Config – a důvěryhodné autoři [#6961](https://github.com/NuGet/Home/issues/6961), [blogový příspěvek](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="c2027-118">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="c2027-119">Vytvoření souborů ".snupkg" obsahovat symboly v sadě – vylepšovat nabízené pochopit protokol nuget tak, aby přijímal soubory snupkg pro server symbolů - [#6878](https://github.com/NuGet/Home/issues/6878), [blogový příspěvek](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="c2027-119">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="c2027-120">Plugin přihlašovacích údajů NuGet V2 – [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="c2027-120">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="c2027-121">Samostatné balíčky NuGet - licence - [#4628](https://github.com/NuGet/Home/issues/4628), [oznámení](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="c2027-121">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="c2027-122">Umožňují vyjádřit výslovný souhlas metadat "GeneratePathProperty" na PackageReference ke generování jednu vlastnost MSBuild balíčku na "Foo.Bar\1.0\" directory – [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="c2027-122">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="c2027-123">Zlepšení úspěchy zákazníků s operacemi NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="c2027-123">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c2027-124">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="c2027-124">Issues fixed in this release</span></span>

* <span data-ttu-id="c2027-125">Upozornění na chyby (prostřednictvím WarnAsErrors) vyvolané PackageExtraction by nikdy neopustí extrahované balíček kolem - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="c2027-125">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="c2027-126">Nesprávně podepsané balíčky by neměl ukládaly do složky globálních balíčků - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="c2027-126">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="c2027-127">vytváření přesměrování vazby neměli přeskočit sestavení průčelí - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="c2027-127">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="c2027-128">Rovná VersionRange nebude porovnání s plovoucí desetinnou čárkou rozsahy - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="c2027-128">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="c2027-129">Obnovení: zásobník regrese výkonu pomocí nového rozhraní .NET Core 2.1 HTTP - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="c2027-129">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="c2027-130">Aktualizace balíčku neměli měnit PrivateAssets PackageReference – [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="c2027-130">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="c2027-131">Podepisování: podepisování musí selhat, pokud balíček obsahuje příliš mnoho položek balíčku (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="c2027-131">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="c2027-132">cestu "dotnet nuget push" by měl podporu nového poskytovatele přihlašovacích údajů – [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="c2027-132">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="c2027-133">Podpora provádění modulů plug-in pomocí neutrální jazykové verze (stejně jako se stane v dockeru) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="c2027-133">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="c2027-134">Přidání zdroje nuget by neměla odstranit přihlašovací údaje ze souboru NuGet.config – [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="c2027-134">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="c2027-135">instalace devDependency PackageReference by ve výchozím nastavení excludeassets = kompilace - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="c2027-135">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="c2027-136">oprava možnosti migrator má být zobrazen pro všechny projekty a zobrazit chybu, pokud projekt není kompatibilní - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="c2027-136">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="c2027-137">"příkaz dotnet add package" musí potvrdit obnovení provádí do souboru prostředků – [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="c2027-137">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="c2027-138">Podepisování: zlepšení podpisový související chybové zprávy – [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="c2027-138">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="c2027-139">[Selhání testu] [zh-TW] V konzole Správce balíčků - nebude lokalizovat řetězce "Konzola správce balíčků" [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="c2027-139">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="c2027-140">Chybová zpráva kolem "Nepodařilo se najít informace o projektu" by měl být mírně konkrétnější v sadě VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="c2027-140">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="c2027-141">Neužitečné chybové zprávy, pokud nesprávně tagu nuspec verze balíčku nuget - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="c2027-141">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="c2027-142">DCR – podepisování: podporují protokol NuGet: Prostředek RepositorySignatures/4.9.0 – [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="c2027-142">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="c2027-143">DCR –. během extrakce balíčku - obsahuje "content-hash" - se nyní vytvoří soubor nupkg.metadata [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="c2027-143">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="c2027-144">DCR - přeskočit ověření pomocí technologie authenticode pro moduly plug-in při provádění v Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="c2027-144">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="c2027-145">Seznam všech problémů, které jsou opravené v této verzi 4.9.0</span><span class="sxs-lookup"><span data-stu-id="c2027-145">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="c2027-146">Shrnutí: Co je nového v 4.9.1</span><span class="sxs-lookup"><span data-stu-id="c2027-146">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="c2027-147">Přidání podpory pro čtení zápis do souboru nuget.config prostřednictvím nový příkaz důvěryhodné – podepisující osoby - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="c2027-147">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c2027-148">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="c2027-148">Issues fixed in this release</span></span>

* <span data-ttu-id="c2027-149">Oprava generování odkazů licence - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="c2027-149">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="c2027-150">Kódy chyb pro ověřování podpisů regrese- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="c2027-150">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="c2027-151">Balíček NuGet.Build.Tasks.Pack nemá žádné informace o licencích - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="c2027-151">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="c2027-152">Seznam všech problémů, které jsou opravené v této verzi 4.9.1</span><span class="sxs-lookup"><span data-stu-id="c2027-152">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="c2027-153">Shrnutí: Co je nového v 4.9.2</span><span class="sxs-lookup"><span data-stu-id="c2027-153">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c2027-154">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="c2027-154">Issues fixed in this release</span></span>

* <span data-ttu-id="c2027-155">Obnovení VS/dotnet.exe/nuget.exe/msbuild.exe nepoužívá přihlašovacích údajů, když název zdroje obsahuje prázdný znak - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="c2027-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="c2027-156">Problémů s dostupností LicenseFileWindow a LicenseAcceptanceWindow - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="c2027-156">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="c2027-157">Oprava FormatException v DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="c2027-157">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="c2027-158">Seznam všech problémů, které jsou opravené v této verzi 4.9.2</span><span class="sxs-lookup"><span data-stu-id="c2027-158">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a><span data-ttu-id="c2027-159">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="c2027-159">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="c2027-160">DotNet nuget příkaz push--interaktivní vrátí chybu v systému Mac.</span><span class="sxs-lookup"><span data-stu-id="c2027-160">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="c2027-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="c2027-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="c2027-162">Problém</span><span class="sxs-lookup"><span data-stu-id="c2027-162">Issue</span></span>
<span data-ttu-id="c2027-163">`--interactive` Argument není předávaná pomocí rozhraní příkazového řádku dotnet což vede k chybě `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="c2027-163">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="c2027-164">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="c2027-164">Workaround</span></span>
<span data-ttu-id="c2027-165">Spuštění další příkaz dotnet pomocí interaktivní možnosti, jako `dotnet restore --interactive` a provést ověření.</span><span class="sxs-lookup"><span data-stu-id="c2027-165">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="c2027-166">Ověřování potom může do mezipaměti podle poskytovatele přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="c2027-166">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="c2027-167">Potom spusťte `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="c2027-167">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="c2027-168">Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu.</span><span class="sxs-lookup"><span data-stu-id="c2027-168">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="c2027-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="c2027-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="c2027-170">Problém</span><span class="sxs-lookup"><span data-stu-id="c2027-170">Issue</span></span>
<span data-ttu-id="c2027-171">Při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="c2027-171">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="c2027-172">To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="c2027-172">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="c2027-173">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="c2027-173">Workaround</span></span>
<span data-ttu-id="c2027-174">Zakázat používání složky pro použití náhradní lokality tak, že nastavíte `RestoreAdditionalProjectSources` na hodnotu nothing.</span><span class="sxs-lookup"><span data-stu-id="c2027-174">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="c2027-175">`<RestoreAdditionalProjectSources/>` Použití opatrně, protože to způsobí, že mnoho balíčků, které mají být stažené z NuGet.org, který jinak by bylo obnoveno ze záložní složky.</span><span class="sxs-lookup"><span data-stu-id="c2027-175">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
