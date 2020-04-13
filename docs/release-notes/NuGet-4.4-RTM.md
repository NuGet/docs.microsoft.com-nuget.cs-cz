---
title: NuGet 4.4 RTM Poznámky k verzi
description: Poznámky k verzi pro NuGet 4.3 RTM včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498703"
---
# <a name="nuget-44-release-notes"></a>NuGet 4.4 Poznámky k verzi

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) je dodáván s NuGet 4.4 RTM.

## <a name="summary-whats-new-in-440"></a>Shrnutí: Co je nového v 4.4.0

## <a name="summary-whats-new-in-442"></a>Shrnutí: Co je nového v 4.4.2

* Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-443"></a>Shrnutí: Co je nového v 4.4.3

* Oprava zabezpečení: Soubory uvnitř NUPKGs mohou mít relativní cestu nad adresářem NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s rozhraním .NET Standard 2.0 s rozhraním .NET Framework & NuGet 

.NET Standard & jeho nástroje byly navrženy tak, že projekty zaměřené na rozhraní .NET Framework 4.6.1 mohou využívat balíčky NuGet & projekty zaměřené na standard .NET Standard 2.0 nebo starší. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře, plán pro jejich řešení a řešení, která můžete nasadit s dnešním stavem nástrojů.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter

#### <a name="issue"></a>Problém

V konzole Správce balíčků občas nefunguje klávesa Enter. Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Alternativní řešení

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Případně zkuste znovu smažit `project.lock.json` a obnovit.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Pomocí Nástroje pro balení Nuget nelze zobrazit, přidat nebo aktualizovat nástroje DotNetCLITools.

#### <a name="issue"></a>Problém

Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Alternativní řešení

V souboru projektu se musí ručně upravit DotNetCLIToolReferences.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense

#### <a name="issue"></a>Problém

Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense. To se stává, když jako formát správce balíčků používáte PackageReferences. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Alternativní řešení

Proveďte ruční obnovení.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení

#### <a name="issue"></a>Problém

Když použijete balíček, který obsahuje sestavení s neplatným podpisem, nebo když je verze balíčku nastavená pomocí časovače DateTime, může při automatickém obnovení balíčku občas vzniknout nekonečná smyčka (dotnet/project-system#1457).

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problémy opravené v časovém rámci NuGet 4.4 RTM

[NuGet 4.3 RTM Poznámky k verzi](../release-notes/nuget-4.3-RTM.md) - Seznam všech problémů opravených pro NuGet 4.3 RTM

### <a name="features"></a>Funkce

- Podpora pro zjednodušené zatížení řešení ve scénářích PMC a NuGet PM UI – [#5180](https://github.com/NuGet/Home/issues/5180)

- Cíl msbuild pack by měl mít veřejný háček pro spuštění uživatelských cílů před sebou - [#5143](https://github.com/NuGet/Home/issues/5143)

- Funkce: Přidání závislostiVersion přepínač nuget nainstalovat - [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 by měl mapovat na .NET Standard 2.0 pro NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)

- Podpora nástroje sestavení sady Visual Studio s ku s msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)

- Během obnovení vygenerujte chybu, pokud je vyžadována podpora rozhraní .NET 4.6.1 pro rozhraní .NET Standard 2.0, ale není nainstalována - [#5325](https://github.com/NuGet/Home/issues/5325)

- UI klienta předpony id balíčku - [#5572](https://github.com/NuGet/Home/issues/5572)

- Doručují lokalizované nugetové komponenty pro podporu lokalizace dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Chyby

- Různé cesty projektu kryty může způsobit obnovení ztratit PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)

- Přesunout kódy chyb s čísly upozornění do rozsahu chyb - [#5824](https://github.com/NuGet/Home/issues/5824)

- Zavádějící chyba, pokud není známo, že verze rozhraní .NET Standard je kompatibilní s cílovým rozhraním [, #5818](https://github.com/NuGet/Home/issues/5818)

- Testování souborů s matoucími licencemi - [#5776](https://github.com/NuGet/Home/issues/5776)

- Chybějící záhlaví licencí v testovacích šablonách EndToEnd - [#5774](https://github.com/NuGet/Home/issues/5774)

- packages.config restore zobrazuje chyby jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

- Nuget.exe instalace by měla mít DisableParallelProcessing na mono - [#5741](https://github.com/NuGet/Home/issues/5741)

- Nuget.exe instalace nesprávně zakáže ukládání do mezipaměti - [#5737](https://github.com/NuGet/Home/issues/5737)

- VS Spuštění příkazu Obnovení pro packages.config při obnovení je zakázáno zobrazí nesprávnou zprávu - [#5718](https://github.com/NuGet/Home/issues/5718)

- VS; Spuštění příkazu obnovit při zakázání obnovení zobrazí matoucí zprávu - [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask se nezdaří, když chybí metadata verze - [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - dotnetcore přidat balíček může vymazat prázdné řádky z csproj - [#5697](https://github.com/NuGet/Home/issues/5697)

- Zdrojové názvy nastavení pověření v Souboru NuGet.Config rozlišují malá a velká písmena – [#5695](https://github.com/NuGet/Home/issues/5695)

- Povolení GeneratePackageOnBuild odstranilo celou historii balíčků - [#5676](https://github.com/NuGet/Home/issues/5676)

- Obnovení neobnoví balíčky mono.cecil nebo semver, ale všechny ostatní balíčky budou obnoveny. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Chyby a upozornění - chybná chyba, když zdroj není k dispozici.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [Konzistence návrhu] NuGet Instalace stav ový text nevypadá správně na tmavé téma v současné době. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Aktualizace balíčků při aktualizacích/instalacích řešení pro všechny projekty - [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - dotnetcore pack se chová odlišně v závislosti na TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)

- Zahrnuté knihovny DLL uvnitř upozornění na vyvolání složky Nástroje - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel spotřebovává příliš mnoho paměti pro operace řetězce - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux vrátí true pro OSX - [#4648](https://github.com/NuGet/Home/issues/4648)

- 'dotnet pack' klade nuspec pod obj místo obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget extrémně pomalý upgrade balíčku - [#4534](https://github.com/NuGet/Home/issues/4534)

- Server CPS není synchronizován s obnovením s většími řešeními, která nezapnula LSL (zjednodušené obnovení řešení) – [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - nuget pack s dodaným verzí ignoruje metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3.+) instalační balíček s číslem verze a příznakem ExcludeVersion neaktualizuje balíček na novější verzi - [#2405](https://github.com/NuGet/Home/issues/2405)

- Obnovení aplikace Project.json by mělo upozornit, pokud balíčky nejvyšší úrovně porušují omezení – [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile nenastavuje vlastní konfiguraci při příkazu install - [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe instalace nerespektuje '-DisableParallelProcessing' přepínač - [#1556](https://github.com/NuGet/Home/issues/1556)

- Zakázané zdroje stále používané dotNet.exe nebo msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)

- Oprava zablokování ve scénáři LSL - [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>Řadiče domény

- podpora nuget.exe install TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)

- Přidat různé msbuild úkol UserAgent řetězce (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName by měl být virtuální - [#5700](https://github.com/NuGet/Home/issues/5700)

- [Konzistence návrhu] Matoucí zpráva při přidávání balíčku NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)

- [Varování a chyby] NoWarn neprotéká přechodně přes P2P odkazy - [#5501](https://github.com/NuGet/Home/issues/5501)

- Lehké zatížení řešení: Společné jádro pro PM ui, PMC a IV- - [#5057](https://github.com/NuGet/Home/issues/5057)

- Lehké zatížení řešení: Podpora - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- Přidání podpory pro cíl MSBuild před obnovením, který visual studio aktivuje – [#4781](https://github.com/NuGet/Home/issues/4781)

- Přidejte veřejný cíl nuget.targets, na který lze odkazovat pomocí beforetargets - [#4634](https://github.com/NuGet/Home/issues/4634)

- Cíl balíčku nemůže správně vytvářet contentFiles s akcemi sestavení – [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do blokuje vlákna fondu vláken - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Docs for Install příkaz DependencyVersion a Framework příznaky - [#5858](https://github.com/NuGet/Home/issues/5858)

- Aktualizace dokumentů na NuGet upozornění a chyby - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Odkazy na problémy GitHubu opravené v 4.4 RTM

[Seznam problémů 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Seznam problémů 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Seznam problémů 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
