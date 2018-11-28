---
title: Zpráva k vydání verze NuGet 4.9 RTM
description: Zpráva k vydání verze pro NuGet 4.9 včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453793"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="01503-103">Zpráva k vydání verze 4.9 NuGet</span><span class="sxs-lookup"><span data-stu-id="01503-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="01503-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.9.0 funkce.</span><span class="sxs-lookup"><span data-stu-id="01503-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="01503-105">Příkazový řádek verze stejné funkce jsou také k dispozici:</span><span class="sxs-lookup"><span data-stu-id="01503-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="01503-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="01503-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="01503-107">DotNet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="01503-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="01503-108">Souhrn: Co je nového v 4.9.0</span><span class="sxs-lookup"><span data-stu-id="01503-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="01503-109">Podepisování: Povolit ClientPolicies vyžadují použití sady úložišť uvedené v souboru NuGet.Config – a důvěryhodné autoři [#6961](https://github.com/NuGet/Home/issues/6961)</span><span class="sxs-lookup"><span data-stu-id="01503-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="01503-110">Vytvoření souborů ".snupkg" obsahovat symboly v sadě – vylepšovat nabízené pochopit protokol nuget tak, aby přijímal soubory snupkg pro server symbolů - [#6878](https://github.com/NuGet/Home/issues/6878)</span><span class="sxs-lookup"><span data-stu-id="01503-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="01503-111">Plugin přihlašovacích údajů NuGet V2 – [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="01503-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="01503-112">Samostatný NuGet balíčky - licence - [#4628](https://github.com/NuGet/Home/issues/4628)</span><span class="sxs-lookup"><span data-stu-id="01503-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="01503-113">Umožňují vyjádřit výslovný souhlas metadat "GeneratePathProperty" na PackageReference ke generování jednu vlastnost MSBuild balíčku na "Foo.Bar\1.0\" directory – [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="01503-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="01503-114">Zlepšení úspěchy zákazníků s operacemi NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="01503-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="01503-115">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="01503-115">Issues fixed in this release</span></span>

* <span data-ttu-id="01503-116">Upozornění na chyby (prostřednictvím WarnAsErrors) vyvolané PackageExtraction by nikdy neopustí extrahované balíček kolem - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="01503-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="01503-117">Nesprávně podepsané balíčky by neměl ukládaly do složky globálních balíčků - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="01503-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="01503-118">vytváření přesměrování vazby neměli přeskočit sestavení průčelí - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="01503-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="01503-119">Rovná VersionRange nebude porovnání s plovoucí desetinnou čárkou rozsahy - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="01503-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="01503-120">Obnovení: zásobník regrese výkonu pomocí nového rozhraní .NET Core 2.1 HTTP - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="01503-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="01503-121">Aktualizace balíčku neměli měnit PrivateAssets PackageReference – [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="01503-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="01503-122">Podepisování: podepisování musí selhat, pokud balíček obsahuje příliš mnoho položek balíčku (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="01503-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="01503-123">cestu "dotnet nuget push" by měl podporu nového poskytovatele přihlašovacích údajů – [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="01503-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="01503-124">Podpora provádění modulů plug-in pomocí neutrální jazykové verze (stejně jako se stane v dockeru) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="01503-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="01503-125">Přidání zdroje nuget by neměla odstranit přihlašovací údaje ze souboru NuGet.config – [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="01503-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="01503-126">instalace devDependency PackageReference by ve výchozím nastavení excludeassets = kompilace - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="01503-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="01503-127">oprava možnosti migrator má být zobrazen pro všechny projekty a zobrazit chybu, pokud projekt není kompatibilní - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="01503-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="01503-128">"příkaz dotnet add package" musí potvrdit obnovení provádí do souboru prostředků – [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="01503-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="01503-129">Podepisování: zlepšení podpisový související chybové zprávy – [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="01503-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="01503-130">[Selhání testu] [zh-TW] V konzole Správce balíčků - nebude lokalizovat řetězce "Konzola správce balíčků" [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="01503-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="01503-131">Chybová zpráva kolem "Nepodařilo se najít informace o projektu" by měl být mírně konkrétnější v sadě VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="01503-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="01503-132">Neužitečné chybové zprávy, pokud nesprávně tagu nuspec verze balíčku nuget - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="01503-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="01503-133">DCR – podepisování: podporují protokol NuGet: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="01503-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="01503-134">DCR –. během extrakce balíčku - obsahuje "content-hash" - se nyní vytvoří soubor nupkg.metadata [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="01503-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="01503-135">DCR - přeskočit ověření pomocí technologie authenticode pro moduly plug-in při provádění v Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="01503-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="01503-136">Seznam všech problémů, které jsou opravené v této verzi 4.9.0</span><span class="sxs-lookup"><span data-stu-id="01503-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="01503-137">Souhrn: Co je nového v 4.9.1</span><span class="sxs-lookup"><span data-stu-id="01503-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="01503-138">Přidání podpory pro čtení zápis do souboru nuget.config prostřednictvím nový příkaz důvěryhodné – podepisující osoby - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="01503-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="01503-139">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="01503-139">Issues fixed in this release</span></span>

* <span data-ttu-id="01503-140">Oprava generování odkazů licence - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="01503-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="01503-141">Kódy chyb pro ověřování podpisů regrese- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="01503-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="01503-142">Balíček NuGet.Build.Tasks.Pack nemá žádné informace o licencích - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="01503-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="01503-143">Seznam všech problémů, které jsou opravené v této verzi 4.9.1</span><span class="sxs-lookup"><span data-stu-id="01503-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="01503-144">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="01503-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="01503-145">DotNet.exe/nuget.exe nepoužívá přihlašovacích údajů, když název zdroje obsahuje prázdný znak - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="01503-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="01503-146">Problém</span><span class="sxs-lookup"><span data-stu-id="01503-146">Issue</span></span>
<span data-ttu-id="01503-147">Pokud je prázdný znak v názvu zdroje, nuget.exe vyvolá chybu jako `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span><span class="sxs-lookup"><span data-stu-id="01503-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="01503-148">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="01503-148">Workaround</span></span>
<span data-ttu-id="01503-149">Změňte název zdroje nebude obsahovat prázdný znak.</span><span class="sxs-lookup"><span data-stu-id="01503-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="01503-150">DotNet nuget příkaz push--interaktivní vrátí chybu v systému Mac.</span><span class="sxs-lookup"><span data-stu-id="01503-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="01503-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="01503-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="01503-152">Problém</span><span class="sxs-lookup"><span data-stu-id="01503-152">Issue</span></span>
<span data-ttu-id="01503-153">`--interactive` Argument není předávaná pomocí rozhraní příkazového řádku dotnet což vede k chybě `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="01503-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="01503-154">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="01503-154">Workaround</span></span>
<span data-ttu-id="01503-155">Spuštění další příkaz dotnet pomocí interaktivní možnosti, jako `dotnet restore --interactive` a provést ověření.</span><span class="sxs-lookup"><span data-stu-id="01503-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="01503-156">Ověřování potom může do mezipaměti podle poskytovatele přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="01503-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="01503-157">Potom spusťte `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="01503-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="01503-158">Problémů s dostupností LicenseFileWindow a LicenseAcceptanceWindow - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="01503-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="01503-159">Problém</span><span class="sxs-lookup"><span data-stu-id="01503-159">Issue</span></span>
<span data-ttu-id="01503-160">Okno přijetí licence a okno licenční soubor mají problémy s pomocí navigace klávesnicí a komentář pomocí čtečky obrazovky a čtečky JAWS.</span><span class="sxs-lookup"><span data-stu-id="01503-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="01503-161">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="01503-161">Workaround</span></span>
<span data-ttu-id="01503-162">Alternativní řešení neexistuje.</span><span class="sxs-lookup"><span data-stu-id="01503-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="01503-163">Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu.</span><span class="sxs-lookup"><span data-stu-id="01503-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="01503-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="01503-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="01503-165">Problém</span><span class="sxs-lookup"><span data-stu-id="01503-165">Issue</span></span>
<span data-ttu-id="01503-166">Při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="01503-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="01503-167">To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="01503-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="01503-168">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="01503-168">Workaround</span></span>
<span data-ttu-id="01503-169">Zakázat používání složky pro použití náhradní lokality tak, že nastavíte `RestoreAdditionalProjectSources` na hodnotu nothing.</span><span class="sxs-lookup"><span data-stu-id="01503-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="01503-170">`<RestoreAdditionalProjectSources/>` Použití opatrně, protože to způsobí, že mnoho balíčků, které mají být stažené z NuGet.org, který jinak by bylo obnoveno ze záložní složky.</span><span class="sxs-lookup"><span data-stu-id="01503-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
