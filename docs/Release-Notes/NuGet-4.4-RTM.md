---
title: Poznámky k verzi 4.4 RTM NuGet
description: Poznámky k verzi pro NuGet 4.3 RTM, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3e969274e69de03ca9851d31a627919dcc46bb7d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-44-rtm-release-notes"></a>Poznámky k verzi 4.4 RTM NuGet

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.4 RTM.

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET standardní 2.0 pomocí rozhraní .NET Framework & NuGet 

.NET standard & jeho nástrojů je navržené tak, aby projektech zacílených na rozhraní .NET Framework 4.6.1 může využívat balíčky NuGet & projektech zacílených na standardní rozhraní .NET 2.0 nebo dřívější. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tento scénář, plán pro adresování a alternativní řešení můžete nasadit s je aktuální stav nástrojů.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter

#### <a name="issue"></a>Problém

V konzole Správce balíčků občas nefunguje klávesa Enter. Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Alternativní řešení

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Případně, zkuste odstranit `project.lock.json` a opakujte obnovení.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nelze zobrazit, přidat nebo aktualizovat DotNetCLITools pomocí Správce balíčků Nuget

#### <a name="issue"></a>Problém

Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Alternativní řešení

V souboru projektu se musí ručně upravit DotNetCLIToolReferences.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense

#### <a name="issue"></a>Problém

Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense. To se stává, když jako formát správce balíčků používáte PackageReferences. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Alternativní řešení

Proveďte ruční obnovení.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení

#### <a name="issue"></a>Problém

V některých případech použijete-li balíček, který obsahuje sestavení s neplatným podpisem nebo pokud verze balíčku nastavena, DateTime, burzovní, způsobí auto obnovení balíčku ke spuštění v nekonečné smyčce (dotnet projektu – systém #1457).

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Chyby v období NuGet 4.4 RTM

[K vydání verze RTM 4.3 NuGet](../release-notes/nuget-4.3-RTM.md) -obsahuje seznam všech chyb odstraněných NuGet 4.3 RTM

### <a name="features"></a>Funkce

- Podpora pro zatížení řešení Lightweight ve scénářích NuGet PM uživatelského rozhraní a pomocí PMC - [#5180](https://github.com/NuGet/Home/issues/5180)

- Cíle msbuild pack musí mít veřejný háku pro spuštěné cíle uživatele před samotné - [#5143](https://github.com/NuGet/Home/issues/5143)

- Funkce: Přidání přepínače dependencyVersion k instalaci nuget - [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.todo.0 by měla být mapována na rozhraní .NET 2.0 standardní pro NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)

- Podporovat Visual Studio sestavení SKU nástroje msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)

- Během obnovení, generuje chybu, pokud .NET 4.6.1 podpora pro standardní rozhraní .NET 2.0 je vyžadována, ale není nainstalován - [#5325](https://github.com/NuGet/Home/issues/5325)

- Balíček ID předponu rezervace uživatelské rozhraní klienta - [#5572](https://github.com/NuGet/Home/issues/5572)

- poskytovat lokalizované nuget součásti pro podporu dotnet.exe lokalizace - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Chyby

- Skříně cesty jiný projekt může způsobit ztrátu PackageReferences - obnovení [#5855](https://github.com/NuGet/Home/issues/5855)

- Přesunout kódy chyb s čísla upozornění na rozsah chyba - [#5824](https://github.com/NuGet/Home/issues/5824)

- Oklamání chyba, když se ví, .NET Standard verze není kompatibilní s cílové rozhraní - [#5818](https://github.com/NuGet/Home/issues/5818)

- Testování souborů s licencí matoucí - [#5776](https://github.com/NuGet/Home/issues/5776)

- Chybí záhlaví licencí v EndToEnd testování šablony - [#5774](https://github.com/NuGet/Home/issues/5774)

- obnovení souboru Packages.config zobrazuje chyby jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

- instalace nuget.exe by měl mít DisableParallelProcessing na mono - [#5741](https://github.com/NuGet/Home/issues/5741)

- instalace nuget.exe nesprávně zakáže ukládání do mezipaměti - [#5737](https://github.com/NuGet/Home/issues/5737)

- Spuštění příkazu restore pro zobrazení souboru packages.config, když je obnovení zakázáno nesprávný zpráva – VS [#5718](https://github.com/NuGet/Home/issues/5718)

- VS; Spuštění příkazu restore, když je obnovení zakázáno zobrazí zprávu matoucí - [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask selže, pokud chybí metadata verze - [#5716](https://github.com/NuGet/Home/issues/5716)

- DotNet.
  - dotnetcore přidat balíček můžete vymazat prázdné řádky z csproj - [#5697](https://github.com/NuGet/Home/issues/5697)

- Názvy zdrojů nastavení přihlašovacích údajů do souboru NuGet.Config jsou velká a malá písmena - [#5695](https://github.com/NuGet/Home/issues/5695)

- Povolení GeneratePackageOnBuild odstranit mé celou historii balíčků - [#5676](https://github.com/NuGet/Home/issues/5676)

- Obnovení nebude možné obnovit mono.cecil nebo semver balíčků, ale všechny ostatní balíčky získat obnovit. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Chyby a upozornění - chybný při zdroji v není k dispozici.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Text stav instalace NuGet nevypadá aktuálně správné na tmavým motivem. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Aktualizovat balíčky v řešení aktualizací nebo instalace pro všechny projekty - [#5508](https://github.com/NuGet/Home/issues/5508)

- DotNet.
  - dotnetcore pack chová odlišně v závislosti na TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)

- Knihovny DLL zahrnuty do vnitřní nástroje složky throw upozornění - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel využívá příliš mnoho paměti pro operace s řetězci - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux vrátí hodnotu true pro OSX - [#4648](https://github.com/NuGet/Home/issues/4648)

- 'dotnet pack' vloží nuspec pod obj místo obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget velmi pomalé balíček upgradu - [#4534](https://github.com/NuGet/Home/issues/4534)

- Prohlášení CPS synchronizované s obnovením s větší řešení, které nezapnuli dolní limit (lightweight řešení obnovení) - [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - nuget pack s zadaný verze ignoruje metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3 +) nainstalovat balíček s číslem verze a ExcludeVersion příznak není balíček aktualizace na novější verzi - [#2405](https://github.com/NuGet/Home/issues/2405)

- Project.JSON obnovení musí zobrazit upozornění, pokud nejvyšší úrovně balíčky porušují omezení - [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile není nastavení vlastní konfigurace pro příkaz install - [#1646](https://github.com/NuGet/Home/issues/1646)

- instalace nuget.exe nectí '-DisableParallelProcessing' přepínače - [#1556](https://github.com/NuGet/Home/issues/1556)

- Zakázané zdroje, které DotNet.exe nebo msbuild.exe - stále používá [#5704](https://github.com/NuGet/Home/issues/5704)

- Opravte zablokování v dolní limit scénář – [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>Chcete

- nuget.exe nainstalovat podporu TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)

- Přidejte jiný msbuild úloh UserAgent řetězce (msbuild plochy netcore vs) - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName musí být virtuální - [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Složitá zprávy při přidání balíčku NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)

- [Varování a chyby] NoWarn není přechodně procházet skrz P2P odkazy - [#5501](https://github.com/NuGet/Home/issues/5501)

- Prosté řešení zatížení: Běžné základní PM uživatelského rozhraní, pomocí PMC a inicializační vektory-- [#5057](https://github.com/NuGet/Home/issues/5057)

- Prosté řešení zatížení: Podpora - pomocí PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- Přidání podpory pro před obnovením MSBuild cíl, který aktivuje Visual Studio – [#4781](https://github.com/NuGet/Home/issues/4781)

- Přidejte veřejný cíl do NuGet.targets, které můžete odkazovat pomocí BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)

- Cíl Pack nelze vytvořit contentFiles akce sestavení správně - [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do blokuje podprocesy z fondu podprocesů - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Dokumentace pro instalaci příkaz příznaky DependencyVersion a Framework - [#5858](https://github.com/NuGet/Home/issues/5858)

- Aktualizace dokumentace na NuGet upozornění a chyby - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Odkazy na Githubu chyby v 4.4 RTM

[Seznam problémů 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Seznam problémů 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Seznam problémů 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
