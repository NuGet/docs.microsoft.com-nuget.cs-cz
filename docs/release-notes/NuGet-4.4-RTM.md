---
title: Zpráva k vydání verze NuGet 4.4 RTM
description: Zpráva k vydání verze pro NuGet 4.3 RTM, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9ea11ad5476b02940b171fdc69ac0bf56598418d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548411"
---
# <a name="nuget-44-rtm-release-notes"></a>Zpráva k vydání verze NuGet 4.4 RTM

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.4 RTM.

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET Standard 2.0 pomocí rozhraní .NET Framework a NuGet 

.NET standard a jeho nástroje je navržená tak, že projekty cílené na rozhraní .NET Framework 4.6.1 může spotřebovat balíčky NuGet & projekty cílené na .NET Standard 2.0 nebo dřívější. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře plánu pro účely řešení a alternativní řešení můžete nasadit s dnešní stavu nástrojů.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter

#### <a name="issue"></a>Problém

V konzole Správce balíčků občas nefunguje klávesa Enter. Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Alternativní řešení

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Alternativně můžete zkusit odstranění `project.lock.json` a znovu ho obnovit.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nejde zobrazit, přidat ani aktualizovat DotNetCLITools pomocí Správce balíčků Nuget

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

V některých případech použijete balíček, který obsahuje sestavení s neplatným podpisem, nebo když se verze balíčku nastaví pomocí časovače "DateTime, může to způsobí, že auto obnovení balíčku občas způsobit nekonečnou smyčku (dotnet/project-system #1457).

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problémy opravené ve verzi RTM 4.4 NuGet časový rámec

[4.3 RTM poznámkách k verzi NuGet](../release-notes/nuget-4.3-RTM.md) – zobrazí seznam všech problémů stanovené pro verzi RTM 4.3 NuGet

### <a name="features"></a>Funkce

- Podpora pro zjednodušené načtení řešení v PMC a NuGet PM uživatelského scénáře: [#5180](https://github.com/NuGet/Home/issues/5180)

- Cíl nástroje msbuild pack by měl mít veřejný vidlici pro spuštění cíle uživatele před samotný - [#5143](https://github.com/NuGet/Home/issues/5143)

- Funkce: Přidejte přepínač dependencyVersion do instalace nuget – [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.todo.0 mělo mapovat .NET Standard 2.0 pro NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)

- Podporovat SKU Visual Studio sestavení nástroje msbuild/t: Restore - [#5562](https://github.com/NuGet/Home/issues/5562)

- Během obnovení, vygenerují chybu, pokud .NET 4.6.1 podpora .NET Standard 2.0 je vyžadována, ale není nainstalovaná - [#5325](https://github.com/NuGet/Home/issues/5325)

- Balíček ID předponu rezervace uživatelské rozhraní klienta - [#5572](https://github.com/NuGet/Home/issues/5572)

- doručování součásti lokalizované nuget pro podporu lokalizace dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Chyby

- Cesta písmen jiný projekt může způsobit obnovení přijít o PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)

- Přesunout na rozsah chyby – kódy chyb s čísla upozornění [#5824](https://github.com/NuGet/Home/issues/5824)

- Když se ví, .NET Standard verze není kompatibilní s cílovou architekturu - zavádějící chyba [#5818](https://github.com/NuGet/Home/issues/5818)

- Soubory s licencí matoucí – testování [#5776](https://github.com/NuGet/Home/issues/5776)

- Chybí záhlaví licence v EndToEnd testovací šablony - [#5774](https://github.com/NuGet/Home/issues/5774)

- obnovení souboru Packages.config se zobrazí chyby jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

- instalace nuget.exe by měl mít DisableParallelProcessing v mono - [#5741](https://github.com/NuGet/Home/issues/5741)

- instalace nuget.exe nesprávně zakáže ukládání do mezipaměti – [#5737](https://github.com/NuGet/Home/issues/5737)

- VS pro zobrazení souboru packages.config při obnovení zakázáno nesprávná zpráva – spouštění příkazu restore [#5718](https://github.com/NuGet/Home/issues/5718)

- VS; Spuštění příkazu restore, když je obnovení zakázáno zobrazí zprávu matoucí - [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask není úspěšné při chybí metadata verze – [#5716](https://github.com/NuGet/Home/issues/5716)

- DotNet
  - dotnetcore přidat balíček můžete vymazat prázdné řádky ze souboru csproj - [#5697](https://github.com/NuGet/Home/issues/5697)

- Názvy zdrojů nastavení přihlašovacích údajů do souboru NuGet.Config jsou malá a velká písmena - [#5695](https://github.com/NuGet/Home/issues/5695)

- Povolení GeneratePackageOnBuild odstranit celou historii balíčků - [#5676](https://github.com/NuGet/Home/issues/5676)

- Restore neobnoví balíčky mono.cecil nebo semver, ale všechny ostatní balíčky obnovena. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Chyby a upozornění - chybný při zdroj není k dispozici.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Instalace NuGet stavový text nevypadá aktuálně správné na tmavý motiv. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Aktualizovat balíčky v řešení aktualizací nebo instalace pro všechny projekty - [#5508](https://github.com/NuGet/Home/issues/5508)

- DotNet
  - balíček dotnetcore chová odlišně v závislosti na vs TargetFramework TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)

- Zahrnout knihovny DLL uvnitř nástroje pro složku throw upozornění - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel spotřebovává příliš mnoho paměti pro operace s řetězci - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux vrací hodnotu true pro OS x - [#4648](https://github.com/NuGet/Home/issues/4648)

- soubor nuspec pod obj místo obj\Debug – vloží "balíčku dotnet" [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget velmi pomalé aktualizaci balíčku - [#4534](https://github.com/NuGet/Home/issues/4534)

- Prohlášení CPS synchronizovaný s obnovení s větší řešení, které nezapnuli zjednodušeného načtení řešení (obnovení zjednodušeného řešení) – [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - nuget pack s zadaná verze ignoruje metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3 +) nainstalujte balíček s číslem verze a ExcludeVersion příznaku neprovede aktualizaci balíčku na novější verzi - [#2405](https://github.com/NuGet/Home/issues/2405)

- Project.JSON obnovení musí zobrazit upozornění, pokud nejvyšší úrovně balíčky porušení omezení - [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile není nastavení vlastní konfigurace pro příkaz install - [#1646](https://github.com/NuGet/Home/issues/1646)

- instalace nuget.exe nerespektuje "-DisableParallelProcessing" přepínač - [#1556](https://github.com/NuGet/Home/issues/1556)

- Zakázané zdrojů i nadále používat DotNet.exe nebo msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)

- Opravit. program přestane reagovat ve scénáři zjednodušeného načtení řešení - [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>Chcete

- nuget.exe nainstalovat podporu TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)

- Přidejte jiný msbuild úloh UserAgent řetězce (msbuild klasické pracovní plochy netcore vs) - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName by měl být virtuální - [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Matoucí zprávy při přidání balíčku NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)

- [Upozornění a chyby] NoWarn není přechodně probíhat přes odkazy P2P - [#5501](https://github.com/NuGet/Home/issues/5501)

- Zjednodušené načtení řešení: Common jádro pro uživatelské rozhraní PM, PMC a vektory IV-- [#5057](https://github.com/NuGet/Home/issues/5057)

- Zjednodušené načtení řešení: Podpora - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- Přidání podpory pro před obnovením cíl nástroje MSBuild, který spustí Visual Studio – [#4781](https://github.com/NuGet/Home/issues/4781)

- Přidat veřejný cíl NuGet.targets, který může být odkazováno pomocí BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)

- Cíl Pack nelze contentFiles vytvořit s akcí sestavení správně – [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do blokuje vláken fondu vláken - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Dokumentace pro instalaci příkazu DependencyVersion a Framework příznaky - [#5858](https://github.com/NuGet/Home/issues/5858)

- Aktualizace dokumentace pro NuGet upozornění a chyby - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Odkazy na problémy Githubu Vyřešeno ve verzi RTM 4.4

[Seznam problémů, 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Seznam problémů, 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Seznam problémů, 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
