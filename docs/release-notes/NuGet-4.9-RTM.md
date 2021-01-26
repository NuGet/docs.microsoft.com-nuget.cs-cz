---
title: Poznámky k verzi NuGet 4,9 RTM
description: Poznámky k verzi pro NuGet 4,9, včetně známých problémů, oprav chyb, nových funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 429218fa4968d572ef187ef1dbfacac8a3bde2b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780144"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="3d760-103">Zpráva k vydání verze NuGet 4,9</span><span class="sxs-lookup"><span data-stu-id="3d760-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="3d760-104">Prostředky pro distribuci NuGet:</span><span class="sxs-lookup"><span data-stu-id="3d760-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="3d760-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="3d760-105">NuGet version</span></span> | <span data-ttu-id="3d760-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d760-106">Available in Visual Studio version</span></span>| <span data-ttu-id="3d760-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3d760-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="3d760-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="3d760-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3d760-109">Visual Studio 2017 verze 15.9.0</span><span class="sxs-lookup"><span data-stu-id="3d760-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="3d760-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="3d760-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="3d760-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="3d760-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="3d760-112">Není k dispozici</span><span class="sxs-lookup"><span data-stu-id="3d760-112">n/a</span></span> | <span data-ttu-id="3d760-113">Není k dispozici</span><span class="sxs-lookup"><span data-stu-id="3d760-113">n/a</span></span> |
| [<span data-ttu-id="3d760-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="3d760-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="3d760-115">Visual Studio 2017 verze 15.9.4</span><span class="sxs-lookup"><span data-stu-id="3d760-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="3d760-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="3d760-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="3d760-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="3d760-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="3d760-118">Visual Studio 2017 verze 15.9.6</span><span class="sxs-lookup"><span data-stu-id="3d760-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="3d760-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="3d760-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="3d760-120">Shrnutí: co je nového v 4.9.0</span><span class="sxs-lookup"><span data-stu-id="3d760-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="3d760-121">Podepisování: Povolte ClientPolicies, aby vyžadovala použití sady důvěryhodných autorů a úložišť uvedených v NuGet.Config- [#6961](https://github.com/NuGet/Home/issues/6961), [Blogový příspěvek](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html) .</span><span class="sxs-lookup"><span data-stu-id="3d760-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="3d760-122">Vytvoření souborů. snupkg, které obsahují symboly v sadě Pack – vylepší nabízení oznámení protokolu NuGet pro příjem souborů snupkg pro symbol server – [#6878](https://github.com/NuGet/Home/issues/6878), [Blogový příspěvek](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="3d760-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="3d760-123">Modul plug-in přihlašovacích údajů NuGet v2 – [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="3d760-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="3d760-124">Self-Contained balíčků NuGet – License- [#4628](https://github.com/NuGet/Home/issues/4628), [oznámení](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="3d760-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="3d760-125">Povolení výslovných GeneratePathProperty metadat na PackageReference pro vygenerování vlastnosti MSBuild pro balíček do adresáře foo. Bar\1.0 \" – [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="3d760-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="3d760-126">Zlepšení úspěšnosti zákazníků pomocí operací NuGet – [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="3d760-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="3d760-127">Povolit opakovaně obnovitelné balíčky pomocí zámku souboru – [#5602](https://github.com/NuGet/Home/issues/5602), [oznámení](https://github.com/NuGet/Announcements/issues/28), [Blogový příspěvek](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="3d760-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3d760-128">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="3d760-128">Issues fixed in this release</span></span>

* <span data-ttu-id="3d760-129">Upozornění se zvýšenými oprávněními (přes WarnAsErrors) vyvolaná PackageExtraction by nikdy neměla opustit extrahovaný balíček [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="3d760-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="3d760-130">Nesprávně podepsané balíčky by neměly končit ve složce globálních balíčků – [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="3d760-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="3d760-131">generování přesměrování vazby by nemělo přeskočit sestavení fasády – [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="3d760-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="3d760-132">VersionRange Equals se nerovná plovoucí rozsahy – [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="3d760-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="3d760-133">Obnovení: regrese výkonu pomocí nového rozhraní .NET Core 2,1 HTTP Stack- [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="3d760-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="3d760-134">Aktualizace balíčku by neměla upravovat PrivateAssets PackageReference- [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="3d760-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="3d760-135">Podepisování: když má balíček příliš mnoho položek balíčku (>65534), podpis by se nezdařil. [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="3d760-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="3d760-136">"dotnet NuGet push" codepath by měl podporovat nového poskytovatele pověření – [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="3d760-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="3d760-137">Podpora spouštění modulů plug-in s invariantní jazykovou verzí (jak se děje v Docker) – [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="3d760-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="3d760-138">Přidání zdrojů NuGet by nemělo odstraňovat přihlašovací údaje z NuGet.config- [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="3d760-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="3d760-139">instalace devDependency PackageReference by měla být standardně excludeassets = Compile- [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="3d760-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="3d760-140">Oprava možnosti migrace, která se zobrazí pro všechny projekty a zobrazí chybu, pokud je projekt nekompatibilní – [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="3d760-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="3d760-141">příkaz dotnet Add Package by měl potvrdit jeho obnovení do souboru prostředků – [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="3d760-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="3d760-142">Podepisování: Vylepšete chybové zprávy související s podepisováním – [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="3d760-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="3d760-143">[Selhání testu] [zh-TW] Řetězec "Konzola správce balíčků" není lokalizována do konzoly Správce balíčků – [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="3d760-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="3d760-144">Chybová zpráva: Nepodařilo se najít informace o projektu, musí být v sadě VS- [#5350](https://github.com/NuGet/Home/issues/5350) o něco konkrétnější.</span><span class="sxs-lookup"><span data-stu-id="3d760-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="3d760-145">Chybná chybová zpráva, pokud je nesprávně použita značka verze nuspec sady NuGet Pack- [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="3d760-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="3d760-146">Registrace pro DCR: podpora protokolu NuGet: RepositorySignatures/4.9.0 Resource- [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="3d760-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="3d760-147">Soubor DCR-. nupkg. Metadata se teď vytvoří během extrakce balíčku – obsahuje Content-hash- [#7283](https://github.com/NuGet/Home/issues/7283) .</span><span class="sxs-lookup"><span data-stu-id="3d760-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="3d760-148">DCR – přeskočení ověřování Authenticode pro moduly plug-in při spuštění na mono- [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="3d760-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="3d760-149">Seznam všech problémů opravených v této verzi 4.9.0</span><span class="sxs-lookup"><span data-stu-id="3d760-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="3d760-150">Shrnutí: co je nového v 4.9.1</span><span class="sxs-lookup"><span data-stu-id="3d760-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="3d760-151">Přidání podpory pro čtení zápisu do nuget.config pomocí nového příkazu Trusted-signers- [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="3d760-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3d760-152">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="3d760-152">Issues fixed in this release</span></span>

* <span data-ttu-id="3d760-153">Oprava generování odkazu na licenci – [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="3d760-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="3d760-154">Regrese chybových kódů pro ověřování podpisů – [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="3d760-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="3d760-155">Balíček NuGet. Build. Tasks. Pack neobsahuje informace o licenci – [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="3d760-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="3d760-156">Seznam všech problémů opravených v této verzi 4.9.1</span><span class="sxs-lookup"><span data-stu-id="3d760-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="3d760-157">Shrnutí: co je nového v 4.9.2</span><span class="sxs-lookup"><span data-stu-id="3d760-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3d760-158">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="3d760-158">Issues fixed in this release</span></span>

* <span data-ttu-id="3d760-159">VS/dotnet.exe/nuget.exe/msbuild.exe obnovení nepoužívá přihlašovací údaje, pokud název zdroje obsahuje prázdný znak [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="3d760-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="3d760-160">Problémy s přístupností LicenseAcceptanceWindow a LicenseFileWindow – [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="3d760-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="3d760-161">Oprava FormatException v DateTime. Parse z DateTimeConverter- [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="3d760-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="3d760-162">Seznam všech problémů opravených v této verzi 4.9.2</span><span class="sxs-lookup"><span data-stu-id="3d760-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="3d760-163">Shrnutí: co je nového v 4.9.3</span><span class="sxs-lookup"><span data-stu-id="3d760-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3d760-164">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="3d760-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="3d760-165">"Opakované obnovení balíčku pomocí souboru zámku" problémy</span><span class="sxs-lookup"><span data-stu-id="3d760-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="3d760-166">Uzamčený režim nefunguje, protože hash je nesprávně počítaný pro předchozí balíčky v mezipaměti – [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="3d760-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="3d760-167">Obnovení se překládá na jinou verzi, než je definované v `packages.lock.json` souboru – [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="3d760-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="3d760-168">'--Locked-Mode/RestoreLockedMode ' způsobuje selhání obnovení spurious, když jsou zapojeny ProjectReferences – [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="3d760-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="3d760-169">Překladač sady MSBuild SDK se pokusí ověřit SHA pro balíček sady SDK, který při použití packages.lock.jspři [#7599](https://github.com/NuGet/Home/issues/7599) se nezdařil.</span><span class="sxs-lookup"><span data-stu-id="3d760-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="3d760-170">"Jak uzamknout závislosti pomocí konfigurovatelných zásad důvěryhodnosti"</span><span class="sxs-lookup"><span data-stu-id="3d760-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="3d760-171">dotnet.exe by neměl vyhodnocovat důvěryhodné podepsané, zatímco podepsané balíčky nejsou podporovány – [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="3d760-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="3d760-172">Pořadí trustedSigners v konfiguračním souboru má vliv na vyhodnocení důvěryhodnosti – [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="3d760-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="3d760-173">Nejde implementovat ISettings [způsobené refaktoringem rozhraní API nastavení pro podporu zásad důvěryhodnosti funkce]- [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="3d760-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="3d760-174">"Vylepšené možnosti ladění"</span><span class="sxs-lookup"><span data-stu-id="3d760-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="3d760-175">Nelze publikovat balíček symbolů pro globální nástroj .NET Core – [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="3d760-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="3d760-176">Problémy "samostatné balíčky NuGet – licence"</span><span class="sxs-lookup"><span data-stu-id="3d760-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="3d760-177">Při sestavování balíčku symbol. snupkg při použití vloženého souboru licence došlo k chybě – [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="3d760-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="3d760-178">Seznam všech problémů opravených v této verzi 4.9.3</span><span class="sxs-lookup"><span data-stu-id="3d760-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="3d760-179">Shrnutí: co je nového v 4.9.4</span><span class="sxs-lookup"><span data-stu-id="3d760-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="3d760-180">Oprava zabezpečení: oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) .</span><span class="sxs-lookup"><span data-stu-id="3d760-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="3d760-181">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="3d760-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="3d760-182">dotnet NuGet push--Interactive poskytuje chybu v počítači Mac.</span><span class="sxs-lookup"><span data-stu-id="3d760-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="3d760-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="3d760-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="3d760-184">Problém</span><span class="sxs-lookup"><span data-stu-id="3d760-184">Issue</span></span>
<span data-ttu-id="3d760-185">Rozhraní příkazového `--interactive` řádku dotnet nepřesměrovává na argument a výsledkem je chyba. `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="3d760-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="3d760-186">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="3d760-186">Workaround</span></span>
<span data-ttu-id="3d760-187">Spusťte jakýkoli jiný příkaz dotnet s interaktivní možností, jako je například `dotnet restore --interactive` a ověřování.</span><span class="sxs-lookup"><span data-stu-id="3d760-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="3d760-188">Ověřování pak může poskytovatel přihlašovacích údajů Uložit do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="3d760-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="3d760-189">Potom spusťte `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="3d760-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="3d760-190">Balíčky v FallbackFolders nainstalované pomocí .NET Core SDK jsou vlastní instalace a ověření podpisu při selhání.</span><span class="sxs-lookup"><span data-stu-id="3d760-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="3d760-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="3d760-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="3d760-192">Problém</span><span class="sxs-lookup"><span data-stu-id="3d760-192">Issue</span></span>
<span data-ttu-id="3d760-193">Při použití dotnet.exe 2. x k obnovení projektu, který má více cílů netcoreapp 1. x a netcoreapp 2. x, se záložní složka považuje za informační kanál souboru.</span><span class="sxs-lookup"><span data-stu-id="3d760-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="3d760-194">To znamená, že při obnovení NuGet vybere balíček ze záložní složky a pokusí se ho nainstalovat do složky globálních balíčků a provede běžné ověřování podpisů, které selže.</span><span class="sxs-lookup"><span data-stu-id="3d760-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="3d760-195">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="3d760-195">Workaround</span></span>
<span data-ttu-id="3d760-196">Zakažte použití záložní složky nastavením na `RestoreAdditionalProjectSources` hodnotu Nothing.</span><span class="sxs-lookup"><span data-stu-id="3d760-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="3d760-197">`<RestoreAdditionalProjectSources/>` Postupujte opatrně, protože to způsobí stažení velkého množství balíčků z NuGet.org, které by jinak bylo obnoveno ze záložní složky.</span><span class="sxs-lookup"><span data-stu-id="3d760-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
