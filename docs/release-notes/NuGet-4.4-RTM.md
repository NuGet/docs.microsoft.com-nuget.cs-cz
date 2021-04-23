---
title: Poznámky k verzi NuGet 4,4 RTM
description: Poznámky k verzi pro NuGet 4,4 RTM, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 980afffcd4202e019ffa87de5dccf947300a9c13
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901704"
---
# <a name="nuget-44-release-notes"></a>Zpráva k vydání verze NuGet 4,4

[Visual Studio 2017 15,4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) obsahuje NUGET 4,4 RTM.

## <a name="summary-whats-new-in-440"></a>Shrnutí: co je nového v 4.4.0

## <a name="summary-whats-new-in-442"></a>Shrnutí: co je nového ve funkci 4.4.2

* Oprava zabezpečení: oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) .

## <a name="summary-whats-new-in-443"></a>Shrnutí: co je nového v 4.4.3

* Oprava zabezpečení: soubory uvnitř NUPKGs můžou mít relativní cestu nad [#7906](https://github.com/NuGet/Home/issues/7906) ADRESÁŘem nupkg.

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET Standard 2,0 s .NET Framework & NuGet 

.NET Standard & jeho nástrojů bylo navrženo tak, aby projekty, které cílí na .NET Framework 4.6.1, mohly využívat balíčky NuGet & projektech cílících na .NET Standard 2,0 nebo starší. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy v tomto scénáři, plán pro jejich adresování a alternativní řešení, která můžete nasadit s dnešním stavem nástrojů.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter

#### <a name="issue"></a>Problém

V konzole Správce balíčků občas nefunguje klávesa Enter. Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Alternativní řešení

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Případně zkuste `project.lock.json` obnovení a znovu obnovit.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Pomocí Správce balíčků NuGet nemůžete zobrazit, přidat ani aktualizovat DotNetCLITools.

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

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problémy opravené v časovém rámci NuGet 4,4 RTM

Zpráva k [vydání verze nuget 4,3 RTM](../release-notes/nuget-4.3-RTM.md) – seznam všech problémů opravených pro NUGET 4,3 RTM

### <a name="features"></a>Funkce

- Podpora zjednodušeného načtení řešení ve scénářích uživatelského rozhraní PMC a NuGet PM – [#5180](https://github.com/NuGet/Home/issues/5180)

- Cíl sady MSBuild Pack musí mít veřejný zavěšení pro spouštění cílových uživatelů před samotným [#5143](https://github.com/NuGet/Home/issues/5143)

- Funkce: Přidání přepínače dependencyVersion do instalace NuGet – [#1806](https://github.com/NuGet/Home/issues/1806)

- UAP 10.0. TODO. 0 by se měl mapovat na .NET Standard 2,0 pro NuGet – [#5684](https://github.com/NuGet/Home/issues/5684)

- Podpora Visual Studio Build Tools SKU pomocí nástroje MSBuild/t: Restore- [#5562](https://github.com/NuGet/Home/issues/5562)

- Při obnovení vygenerujte chybu, pokud je vyžadována podpora .NET 4.6.1 pro .NET Standard 2,0, ale není nainstalovaná – [#5325](https://github.com/NuGet/Home/issues/5325)

- Uživatelské rozhraní klienta rezervace předpony ID balíčku – [#5572](https://github.com/NuGet/Home/issues/5572)

- doručovat lokalizované součásti NuGet, aby podporovaly dotnet.exe lokalizace [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Chyby

- Různá písmena v cestě k projektu můžou způsobit ztrátu PackageReferences [#5855](https://github.com/NuGet/Home/issues/5855)

- Přesunout kódy chyb s čísly upozornění do rozsahu chyb – [#5824](https://github.com/NuGet/Home/issues/5824)

- Zavádějící chyba, pokud .NET Standard verze není známa jako kompatibilní s cílovou architekturou- [#5818](https://github.com/NuGet/Home/issues/5818)

- Testovací soubory s nematoucími licencemi – [#5776](https://github.com/NuGet/Home/issues/5776)

- Chybějící hlavičky licencí v šablonách testů EndToEnd – [#5774](https://github.com/NuGet/Home/issues/5774)

- packages.config Restore zobrazuje chyby jako NU1000- [#5743](https://github.com/NuGet/Home/issues/5743)

- nuget.exe instalace by měla mít DisableParallelProcessing na mono- [#5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe instalace nesprávně zakáže ukládání do mezipaměti – [#5737](https://github.com/NuGet/Home/issues/5737)

- VS spuštění příkazu RESTORE pro packages.config při zakázaném obnovení zobrazuje nesprávnou zprávu- [#5718](https://github.com/NuGet/Home/issues/5718)

- INFRASTRUKTURA Spuštění příkazu RESTORE v případě zakázaného obnovení zobrazí nematoucí zprávu [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask se nezdařila, pokud chybí metadata verze – [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - dotnetcore přidat balíček může vymazat prázdné řádky z csproj- [#5697](https://github.com/NuGet/Home/issues/5697)

- Názvy zdrojů nastavení přihlašovacích údajů v NuGet.Config rozlišují velká a malá písmena – [#5695](https://github.com/NuGet/Home/issues/5695)

- Povolení GeneratePackageOnBuild odstranilo celou historii balíčků – [#5676](https://github.com/NuGet/Home/issues/5676)

- Při obnovení se neobnoví balíčky mono. Cecil nebo semver, ale všechny ostatní balíčky se obnoví. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Chyby a upozornění – chybná chyba, pokud zdroj není k dispozici.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Text stavu instalace NuGet nevypadá v současné době v tmavém motivu správně. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Aktualizace balíčků v řešení aktualizace/instalace pro všechny projekty – [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - sada dotnetcore Pack se chová odlišně v závislosti na TargetFramework a TargetFramework – [#5281](https://github.com/NuGet/Home/issues/5281)

- Zahrnuté knihovny DLL ve složce nástroje vyvolávají upozornění – [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet. ContentModel spotřebovává pro řetězcové operace příliš mnoho paměti – [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper. pro Linux vrátí hodnotu true pro OSX- [#4648](https://github.com/NuGet/Home/issues/4648)

- příkaz dotnet Pack vloží nuspec do obj místo obj\Debug- [#4644](https://github.com/NuGet/Home/issues/4644)

- Vysoce pomalý upgrade balíčku NuGet – [#4534](https://github.com/NuGet/Home/issues/4534)

- Služba CPS není synchronizovaná s obnovením s většími řešeními, která nebyla zapnutá LSL (zjednodušené obnovení řešení) – [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2,0 – balíček NuGet s poskytnutou verzí ignoruje metadata (3.5.0-RTM-1938) – [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3. +) instalovat balíček s číslem verze a příznakem ExcludeVersion neaktualizuje balíček na novější verzi. [#2405](https://github.com/NuGet/Home/issues/2405)

- Project.jspři obnovení by měla upozorňovat na porušení omezení balíčků nejvyšší úrovně – [#2358](https://github.com/NuGet/Home/issues/2358)

- – ConfigFile nenastavuje vlastní konfiguraci příkazu install- [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe instalace nedodržuje přepínač-DisableParallelProcessing- [#1556](https://github.com/NuGet/Home/issues/1556)

- Zakázané zdroje pořád používané DotNet.exe nebo msbuild.exe- [#5704](https://github.com/NuGet/Home/issues/5704)

- Oprava chyb ve scénáři LSL – [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>Chcete odeslat obecnou

- nuget.exe instalaci podpory TargetFramework – [#5736](https://github.com/NuGet/Home/issues/5736)

- Přidejte různé řetězce UserAgent úlohy MSBuild (Netcore vs Desktop MSBuild) – [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver. GetPackageDirectoryName by měl být Virtual- [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Matoucí zpráva při přidávání balíčku NuGet – [#5641](https://github.com/NuGet/Home/issues/5641)

- [Upozornění a chyby] Žádné upozornění neprobíhá přes odkazy na P2P na cestě. [#5501](https://github.com/NuGet/Home/issues/5501)

- Zjednodušené načtení řešení: Common Core for PM UI, PMC a Ideographic-- [#5057](https://github.com/NuGet/Home/issues/5057)

- Zjednodušené načtení řešení: support-PMC- [#5053](https://github.com/NuGet/Home/issues/5053)

- Přidání podpory pro předem obnovený cíl MSBuild, který spouští Visual Studio – [#4781](https://github.com/NuGet/Home/issues/4781)

- Přidejte veřejný cíl do NuGet. cíle, na které se dá odkazovat pomocí BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)

- Cíl sady Pack nemůže vytvořit contentFiles s akcemi sestavení správně – [#4166](https://github.com/NuGet/Home/issues/4166)

- Vlákna fondu vláken RestoreOperationLogger.Do bloků vlákna – [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Dokumentace k příkazům DependencyVersion pro instalaci a příznaky rozhraní – [#5858](https://github.com/NuGet/Home/issues/5858)

- Aktualizace na dokumenty s upozorněními a chybami NuGet – [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Odkazy na problémy GitHubu opravené ve 4,4 RTM

[Seznam problémů 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Seznam problémů 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Seznam problémů 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
