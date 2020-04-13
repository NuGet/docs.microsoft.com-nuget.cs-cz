---
title: NuGet 4.9 RTM Poznámky k verzi
description: Poznámky k verzi pro NuGet 4.9 včetně známých problémů, oprav chyb, nových funkcí a řadičů domény.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496465"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="f1238-103">NuGet 4.9 Poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="f1238-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="f1238-104">Distribuční vozidla NuGet:</span><span class="sxs-lookup"><span data-stu-id="f1238-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="f1238-105">NuGet verze</span><span class="sxs-lookup"><span data-stu-id="f1238-105">NuGet version</span></span> | <span data-ttu-id="f1238-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1238-106">Available in Visual Studio version</span></span>| <span data-ttu-id="f1238-107">K dispozici v sadach .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f1238-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="f1238-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="f1238-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f1238-109">Visual Studio 2017 verze 15.9.0</span><span class="sxs-lookup"><span data-stu-id="f1238-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="f1238-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="f1238-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="f1238-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="f1238-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="f1238-112">neuvedeno</span><span class="sxs-lookup"><span data-stu-id="f1238-112">n/a</span></span> | <span data-ttu-id="f1238-113">neuvedeno</span><span class="sxs-lookup"><span data-stu-id="f1238-113">n/a</span></span> |
| [<span data-ttu-id="f1238-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="f1238-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="f1238-115">Visual Studio 2017 verze 15.9.4</span><span class="sxs-lookup"><span data-stu-id="f1238-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="f1238-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="f1238-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="f1238-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="f1238-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="f1238-118">Visual Studio 2017 verze 15.9.6</span><span class="sxs-lookup"><span data-stu-id="f1238-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="f1238-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="f1238-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="f1238-120">Shrnutí: Co je nového v 4.9.0</span><span class="sxs-lookup"><span data-stu-id="f1238-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="f1238-121">Podepisování: Povolit zásadám ClientPolicies vyžadovat použití sady důvěryhodných autorů a úložišť uvedených v souboru NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [příspěvku blogu](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="f1238-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="f1238-122">vytvořit ".snupkg" soubory, které obsahují symboly v balení - zvýšit push pochopit nuget protokol přijímat snupkg soubory pro symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="f1238-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="f1238-123">NuGet přihlašovací plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="f1238-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="f1238-124">Samostatné balíčky NuGet - Licence - [#4628](https://github.com/NuGet/Home/issues/4628), [oznámení](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="f1238-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="f1238-125">Povolte přihlášení metadata "GeneratePathProperty" na PackageReference pro generování vlastnosti MSBuild na balíček\" do adresáře Foo.Bar\1.0 - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="f1238-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="f1238-126">Zlepšete úspěch zákazníků s operacemi NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="f1238-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="f1238-127">Povolení opakovatelných obnovení balíčků pomocí souboru zámku - [#5602](https://github.com/NuGet/Home/issues/5602), [oznámení](https://github.com/NuGet/Announcements/issues/28), [příspěvek blogu](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="f1238-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f1238-128">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="f1238-128">Issues fixed in this release</span></span>

* <span data-ttu-id="f1238-129">Upozornění zvýšené na chyby (přes WarnAsErrors) vyvolané PackageExtraction by nikdy opustit extrahovaný balíček kolem - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="f1238-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="f1238-130">Špatně podepsané balíčky by neměly skončit ve složce globálních balíčků - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="f1238-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="f1238-131">generování přesměrování vazby by nemělo přeskočit sestavy fasád - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="f1238-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="f1238-132">VersionRange Equals neporovnává plovoucí rozsahy - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="f1238-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="f1238-133">Obnovení: regrese výkonu pomocí nového zásobníku HTTP .NET Core 2.1 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="f1238-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="f1238-134">Aktualizace Package by neměla měnit PrivateAssets PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="f1238-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="f1238-135">Podepisování: podepisování by mělo selhat, pokud balíček má příliš mnoho položek balíčku (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="f1238-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="f1238-136">"dotnet nuget push" kódová cesta by měla podporovat nového zprostředkovatele pověření - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="f1238-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="f1238-137">Podpora provádění pluginů s invariantní jazykovou verzí (jak se děje v dockeru) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="f1238-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="f1238-138">nuget zdroje přidat by neměl a odstranit pověření z NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="f1238-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="f1238-139">instalace devDependency PackageReference by měla být výchozí pro excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="f1238-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="f1238-140">opravit možnost migrator, která má být zobrazena pro všechny projekty a zobrazit chybu, pokud je projekt nekompatibilní - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="f1238-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="f1238-141">"dotnet add package" by měl potvrdit obnovení, které provádí do souboru datových zdrojů - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="f1238-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="f1238-142">Podepisování: zlepšit podepisování související choujecí zprávy - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="f1238-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="f1238-143">[Selhání testu] To je v pořádku. Řetězec "Konzola správce balíčků" není lokalizovat na konzoli Správce balíčků - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="f1238-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="f1238-144">Chybová zpráva kolem "Nelze najít informace o projektu" by měla být trochu konkrétnější uvnitř VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="f1238-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="f1238-145">Neužitečné chybové hlášení při nesprávném použití nuspec verze značky nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="f1238-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="f1238-146">DCR - Podepisování: podpora protokolu NuGet: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="f1238-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="f1238-147">Soubor DCR - .nupkg.metadata bude nyní vytvořen během extrakce balíčku - obsahuje "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="f1238-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="f1238-148">DCR - Přeskočit ověření authenticode pro pluginy při provádění na Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="f1238-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="f1238-149">Seznam všech problémů opravených v této verzi 4.9.0</span><span class="sxs-lookup"><span data-stu-id="f1238-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="f1238-150">Shrnutí: Co je nového v 4.9.1</span><span class="sxs-lookup"><span data-stu-id="f1238-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="f1238-151">Přidejte podporu pro čtení zápisu do nuget.config pomocí nového příkazu trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="f1238-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f1238-152">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="f1238-152">Issues fixed in this release</span></span>

* <span data-ttu-id="f1238-153">Oprava generování licenčního propojení - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="f1238-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="f1238-154">Regrese kódů chyb pro ověřování podpisů - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="f1238-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="f1238-155">Balíček NuGet.Build.Tasks.Pack nemá informace o licenci - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="f1238-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="f1238-156">Seznam všech problémů opravených v této verzi 4.9.1</span><span class="sxs-lookup"><span data-stu-id="f1238-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="f1238-157">Shrnutí: Co je nového v 4.9.2</span><span class="sxs-lookup"><span data-stu-id="f1238-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f1238-158">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="f1238-158">Issues fixed in this release</span></span>

* <span data-ttu-id="f1238-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore nepoužívá pověření, pokud název zdroje obsahuje mezery - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="f1238-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="f1238-160">LicenseAcceptanceWindow a LicenseFileWindow Problémy s usnadněním přístupnosti - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="f1238-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="f1238-161">Opravit FormatException v DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="f1238-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="f1238-162">Seznam všech problémů opravených v této verzi 4.9.2</span><span class="sxs-lookup"><span data-stu-id="f1238-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="f1238-163">Shrnutí: Co je nového v 4.9.3</span><span class="sxs-lookup"><span data-stu-id="f1238-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f1238-164">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="f1238-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="f1238-165">Problémy s opakováním balíčku se obnoví pomocí uzamykaného souboru</span><span class="sxs-lookup"><span data-stu-id="f1238-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="f1238-166">Uzamčený režim nefunguje tak, jak je hash vypočtena nesprávně pro dříve uložené balíčky - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="f1238-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="f1238-167">Obnovení se změní na jinou `packages.lock.json` verzi, než je definováno v souboru – [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="f1238-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="f1238-168">'--locked-mode / RestoreLockedMode' způsobuje falešné obnovení selhání při ProjectReferences jsou zapojeny - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="f1238-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="f1238-169">Překladač sady MSBuild SDK se pokusí ověřit sha pro balíček Sady SDK, který se nezdaří obnovení při použití packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="f1238-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="f1238-170">Problémy s uzamčením závislostí pomocí konfigurovatelných zásad důvěryhodnosti</span><span class="sxs-lookup"><span data-stu-id="f1238-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="f1238-171">dotnet.exe by neměl vyhodnocovat důvěryhodné podepisující, pokud podepsané balíčky nejsou podporovány – [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="f1238-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="f1238-172">Pořadí důvěryhodných typů v konfiguračním souboru ovlivňuje hodnocení důvěryhodnosti - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="f1238-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="f1238-173">Nelze implementovat ISettings [Způsobené refaktoringnastavení nastavení API pro podporu zásad důvěryhodnosti funkce] - [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="f1238-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="f1238-174">"Vylepšené problémy s laděním"</span><span class="sxs-lookup"><span data-stu-id="f1238-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="f1238-175">Balíček symbolů pro globální nástroj .NET Core nelze publikovat [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="f1238-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="f1238-176">"Samostatné balíčky NuGet - licence" Problémy</span><span class="sxs-lookup"><span data-stu-id="f1238-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="f1238-177">Chyba při vytváření symbolu .snupkg balíček při použití vloženého licenčního souboru - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="f1238-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="f1238-178">Seznam všech problémů opravených v této verzi 4.9.3</span><span class="sxs-lookup"><span data-stu-id="f1238-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="f1238-179">Shrnutí: Co je nového v 4.9.4</span><span class="sxs-lookup"><span data-stu-id="f1238-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="f1238-180">Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="f1238-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="f1238-181">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="f1238-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="f1238-182">dotnet nuget push --interactive dává chybu na Macu.</span><span class="sxs-lookup"><span data-stu-id="f1238-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="f1238-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="f1238-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="f1238-184">Problém</span><span class="sxs-lookup"><span data-stu-id="f1238-184">Issue</span></span>
<span data-ttu-id="f1238-185">Argument `--interactive` není předáván dotnet cli a má za následek chybu`error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="f1238-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="f1238-186">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="f1238-186">Workaround</span></span>
<span data-ttu-id="f1238-187">Spusťte jakýkoli jiný příkaz dotnet `dotnet restore --interactive` s interaktivní volbou, například a ověřte.</span><span class="sxs-lookup"><span data-stu-id="f1238-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="f1238-188">Ověřování pak může být uloženo do mezipaměti zprostředkovatelem pověření.</span><span class="sxs-lookup"><span data-stu-id="f1238-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="f1238-189">Potom spusťte `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="f1238-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="f1238-190">Balíčky v záložních složkách nainstalované sadou .NET Core SDK jsou nainstalovány na vlastní instalaci a nepodaří se ověření podpisu.</span><span class="sxs-lookup"><span data-stu-id="f1238-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="f1238-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="f1238-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="f1238-192">Problém</span><span class="sxs-lookup"><span data-stu-id="f1238-192">Issue</span></span>
<span data-ttu-id="f1238-193">Při použití dotnet.exe 2.x obnovit projekt, který více-cíle netcoreapp 1.x a netcoreapp 2.x, záložní složka je považována za soubor krmiva.</span><span class="sxs-lookup"><span data-stu-id="f1238-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="f1238-194">To znamená, že při obnovení NuGet vybere balíček ze záložní složky a pokusí se jej nainstalovat do složky globální balíčky a provést obvyklé ověření podepisování, které se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="f1238-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="f1238-195">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="f1238-195">Workaround</span></span>
<span data-ttu-id="f1238-196">Zakažte použití záložní složky `RestoreAdditionalProjectSources` nastavením na nic.</span><span class="sxs-lookup"><span data-stu-id="f1238-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="f1238-197">`<RestoreAdditionalProjectSources/>`Používejte to s opatrností, protože to způsobí, že mnoho balíčků ke stažení z NuGet.org které by jinak byly obnoveny ze záložní složky.</span><span class="sxs-lookup"><span data-stu-id="f1238-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
