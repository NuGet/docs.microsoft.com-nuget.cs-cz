---
title: Zpráva k vydání verze NuGet 4.9 RTM
description: Zpráva k vydání verze pro NuGet 4.9 včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: aa9bf87504477506dbb1e9ac10d5c1d5841c224f
ms.sourcegitcommit: 885973352d31808e3ddbb45da6d6e54d1e4fca9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/13/2019
ms.locfileid: "56224941"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="0f2b8-103">Zpráva k vydání verze 4.9 NuGet</span><span class="sxs-lookup"><span data-stu-id="0f2b8-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="0f2b8-104">Distribuce vozidel NuGet:</span><span class="sxs-lookup"><span data-stu-id="0f2b8-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="0f2b8-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="0f2b8-105">NuGet version</span></span> | <span data-ttu-id="0f2b8-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f2b8-106">Available in Visual Studio version</span></span>| <span data-ttu-id="0f2b8-107">K dispozici v rozhraní .NET SDK, pomocí kterých</span><span class="sxs-lookup"><span data-stu-id="0f2b8-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="0f2b8-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="0f2b8-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="0f2b8-109">Visual Studio 2017 verze 15.9.0</span><span class="sxs-lookup"><span data-stu-id="0f2b8-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="0f2b8-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="0f2b8-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="0f2b8-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="0f2b8-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="0f2b8-112">není k dispozici</span><span class="sxs-lookup"><span data-stu-id="0f2b8-112">n/a</span></span> | <span data-ttu-id="0f2b8-113">není k dispozici</span><span class="sxs-lookup"><span data-stu-id="0f2b8-113">n/a</span></span> |
| [<span data-ttu-id="0f2b8-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="0f2b8-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="0f2b8-115">Visual Studio 2017 version 15.9.4</span><span class="sxs-lookup"><span data-stu-id="0f2b8-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="0f2b8-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="0f2b8-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="0f2b8-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="0f2b8-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="0f2b8-118">Visual Studio 2017 verze 15.9.6</span><span class="sxs-lookup"><span data-stu-id="0f2b8-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="0f2b8-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="0f2b8-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="0f2b8-120">Shrnutí: Co je nového v 4.9.0</span><span class="sxs-lookup"><span data-stu-id="0f2b8-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="0f2b8-121">Podpis: Povolit ClientPolicies vyžadují použití sady úložišť uvedené v souboru NuGet.Config – a důvěryhodné autoři [#6961](https://github.com/NuGet/Home/issues/6961), [blogový příspěvek](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="0f2b8-122">Vytvoření souborů ".snupkg" obsahovat symboly v sadě – vylepšovat nabízené pochopit protokol nuget tak, aby přijímal soubory snupkg pro server symbolů - [#6878](https://github.com/NuGet/Home/issues/6878), [blogový příspěvek](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="0f2b8-123">Plugin přihlašovacích údajů NuGet V2 – [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="0f2b8-124">Samostatné balíčky NuGet - licence - [#4628](https://github.com/NuGet/Home/issues/4628), [oznámení](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="0f2b8-125">Umožňují vyjádřit výslovný souhlas metadat "GeneratePathProperty" na PackageReference ke generování jednu vlastnost MSBuild balíčku na "Foo.Bar\1.0\" directory – [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="0f2b8-126">Zlepšení úspěchy zákazníků s operacemi NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="0f2b8-127">Povolení opakovatelných balíček obnovení pomocí zámek souboru - [#5602](https://github.com/NuGet/Home/issues/5602), [oznámení](https://github.com/NuGet/Announcements/issues/28), [blogový příspěvek](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0f2b8-128">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="0f2b8-128">Issues fixed in this release</span></span>

* <span data-ttu-id="0f2b8-129">Upozornění na chyby (prostřednictvím WarnAsErrors) vyvolané PackageExtraction by nikdy neopustí extrahované balíček kolem - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="0f2b8-130">Nesprávně podepsané balíčky by neměl ukládaly do složky globálních balíčků - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="0f2b8-131">vytváření přesměrování vazby neměli přeskočit sestavení průčelí - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="0f2b8-132">Rovná VersionRange nebude porovnání s plovoucí desetinnou čárkou rozsahy - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="0f2b8-133">Obnovení: zásobník regrese výkonu pomocí nového rozhraní .NET Core 2.1 HTTP - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="0f2b8-134">Aktualizace balíčku neměli měnit PrivateAssets PackageReference – [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="0f2b8-135">Podepisování: podepisování musí selhat, pokud balíček obsahuje příliš mnoho položek balíčku (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="0f2b8-136">cestu "dotnet nuget push" by měl podporu nového poskytovatele přihlašovacích údajů – [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="0f2b8-137">Podpora provádění modulů plug-in pomocí neutrální jazykové verze (stejně jako se stane v dockeru) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="0f2b8-138">Přidání zdroje nuget by neměla odstranit přihlašovací údaje ze souboru NuGet.config – [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="0f2b8-139">instalace devDependency PackageReference by ve výchozím nastavení excludeassets = kompilace - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="0f2b8-140">oprava možnosti migrator má být zobrazen pro všechny projekty a zobrazit chybu, pokud projekt není kompatibilní - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="0f2b8-141">"příkaz dotnet add package" musí potvrdit obnovení provádí do souboru prostředků – [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="0f2b8-142">Podepisování: zlepšení podpisový související chybové zprávy – [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="0f2b8-143">[Selhání testu] [zh-TW] V konzole Správce balíčků - nebude lokalizovat řetězce "Konzola správce balíčků" [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="0f2b8-144">Chybová zpráva kolem "Nepodařilo se najít informace o projektu" by měl být mírně konkrétnější v sadě VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="0f2b8-145">Neužitečné chybové zprávy, pokud nesprávně tagu nuspec verze balíčku nuget - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="0f2b8-146">DCR – podepisování: podporují protokol NuGet: Prostředek RepositorySignatures/4.9.0 – [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="0f2b8-147">DCR –. během extrakce balíčku - obsahuje "content-hash" - se nyní vytvoří soubor nupkg.metadata [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="0f2b8-148">DCR - přeskočit ověření pomocí technologie authenticode pro moduly plug-in při provádění v Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="0f2b8-149">Seznam všech problémů, které jsou opravené v této verzi 4.9.0</span><span class="sxs-lookup"><span data-stu-id="0f2b8-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="0f2b8-150">Shrnutí: Co je nového v 4.9.1</span><span class="sxs-lookup"><span data-stu-id="0f2b8-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="0f2b8-151">Přidání podpory pro čtení zápis do souboru nuget.config prostřednictvím nový příkaz důvěryhodné – podepisující osoby - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0f2b8-152">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="0f2b8-152">Issues fixed in this release</span></span>

* <span data-ttu-id="0f2b8-153">Oprava generování odkazů licence - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="0f2b8-154">Kódy chyb pro ověřování podpisů regrese- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="0f2b8-155">Balíček NuGet.Build.Tasks.Pack nemá žádné informace o licencích - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="0f2b8-156">Seznam všech problémů, které jsou opravené v této verzi 4.9.1</span><span class="sxs-lookup"><span data-stu-id="0f2b8-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="0f2b8-157">Shrnutí: Co je nového v 4.9.2</span><span class="sxs-lookup"><span data-stu-id="0f2b8-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0f2b8-158">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="0f2b8-158">Issues fixed in this release</span></span>

* <span data-ttu-id="0f2b8-159">Obnovení VS/dotnet.exe/nuget.exe/msbuild.exe nepoužívá přihlašovacích údajů, když název zdroje obsahuje prázdný znak - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="0f2b8-160">Problémů s dostupností LicenseFileWindow a LicenseAcceptanceWindow - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="0f2b8-161">Oprava FormatException v DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="0f2b8-162">Seznam všech problémů, které jsou opravené v této verzi 4.9.2</span><span class="sxs-lookup"><span data-stu-id="0f2b8-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="0f2b8-163">Shrnutí: Co je nového v 4.9.3</span><span class="sxs-lookup"><span data-stu-id="0f2b8-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0f2b8-164">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="0f2b8-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="0f2b8-165">Problémy s "Opakovatelné balíček obnovení pomocí souboru zámku"</span><span class="sxs-lookup"><span data-stu-id="0f2b8-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="0f2b8-166">Uzamčeném režimu nebudou fungovat podle hodnoty hash se počítá nesprávně pro dříve uložené v mezipaměti balíčky - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="0f2b8-167">Obnovení se překládá na jinou verzi než definované v `packages.lock.json` soubor – [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="0f2b8-168">"--uzamčen režim / RestoreLockedMode' způsobuje nesprávné selhání obnovení, když se podílejí projectreferences má za následek - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="0f2b8-169">Překladač sady MSBuild SDK se pokusí ověřit SHA pro balíček sady SDK, které při používání packages.lock.json – se nezdaří obnovení [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="0f2b8-170">Problémy s "Zamknout závislostí pomocí vztahu důvěryhodnosti Konfigurovatelné zásady"</span><span class="sxs-lookup"><span data-stu-id="0f2b8-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="0f2b8-171">DotNet.exe by neměl vyhodnotit důvěryhodné podepisující osoby, zatímco podepsané balíčky nejsou podporovány - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="0f2b8-172">Pořadí trustedSigners v konfiguračním souboru ovlivňuje vyhodnotit důvěryhodnost - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="0f2b8-173">Nejde implementovat ISettings [způsobené refaktoring nastavení rozhraní API k podpoře funkce zásady důvěryhodnosti]- [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="0f2b8-174">Problémy s "Vylepšené možnosti ladění"</span><span class="sxs-lookup"><span data-stu-id="0f2b8-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="0f2b8-175">Nejde publikovat balíček symbolů pro globální nástroji .NET Core – [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="0f2b8-176">Problémy s "Balíčky NuGet samostatná - licence"</span><span class="sxs-lookup"><span data-stu-id="0f2b8-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="0f2b8-177">Chyba při sestavování .snupkg balíček symbolů při použití vložený soubor s licencí - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="0f2b8-178">Seznam všech problémů, které jsou opravené v této verzi 4.9.3</span><span class="sxs-lookup"><span data-stu-id="0f2b8-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")
## <a name="known-issues"></a><span data-ttu-id="0f2b8-179">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="0f2b8-179">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="0f2b8-180">DotNet nuget příkaz push--interaktivní vrátí chybu v systému Mac.</span><span class="sxs-lookup"><span data-stu-id="0f2b8-180">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="0f2b8-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="0f2b8-182">Problém</span><span class="sxs-lookup"><span data-stu-id="0f2b8-182">Issue</span></span>
<span data-ttu-id="0f2b8-183">`--interactive` Argument není předávaná pomocí rozhraní příkazového řádku dotnet což vede k chybě `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="0f2b8-183">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="0f2b8-184">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="0f2b8-184">Workaround</span></span>
<span data-ttu-id="0f2b8-185">Spuštění další příkaz dotnet pomocí interaktivní možnosti, jako `dotnet restore --interactive` a provést ověření.</span><span class="sxs-lookup"><span data-stu-id="0f2b8-185">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="0f2b8-186">Ověřování potom může do mezipaměti podle poskytovatele přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="0f2b8-186">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="0f2b8-187">Potom spusťte `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="0f2b8-187">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="0f2b8-188">Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu.</span><span class="sxs-lookup"><span data-stu-id="0f2b8-188">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="0f2b8-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="0f2b8-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="0f2b8-190">Problém</span><span class="sxs-lookup"><span data-stu-id="0f2b8-190">Issue</span></span>
<span data-ttu-id="0f2b8-191">Při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="0f2b8-191">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="0f2b8-192">To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="0f2b8-192">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="0f2b8-193">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="0f2b8-193">Workaround</span></span>
<span data-ttu-id="0f2b8-194">Zakázat používání složky pro použití náhradní lokality tak, že nastavíte `RestoreAdditionalProjectSources` na hodnotu nothing.</span><span class="sxs-lookup"><span data-stu-id="0f2b8-194">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="0f2b8-195">`<RestoreAdditionalProjectSources/>` Použití opatrně, protože to způsobí, že mnoho balíčků, které mají být stažené z NuGet.org, který jinak by bylo obnoveno ze záložní složky.</span><span class="sxs-lookup"><span data-stu-id="0f2b8-195">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
