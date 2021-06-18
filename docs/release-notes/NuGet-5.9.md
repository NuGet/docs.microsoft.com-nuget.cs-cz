---
title: Zpráva k vydání verze NuGet 5.9
description: Poznámky k verzi pro NuGet 5.9, včetně nových funkcí, oprav chyb a souborů DCRs
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 1152af99cf1421918a42d0d1faa33f1452f54a8f
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323879"
---
# <a name="nuget-59-release-notes"></a>Zpráva k vydání verze NuGet 5.9

Distribuční vozidla NuGet:

| Verze NuGet | K dispozici ve Visual Studio verzi | K dispozici v sadě .NET SDK |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Nainstalované s Visual Studio 2019 s úlohou .NET Core
  
> [!NOTE]
> Visual Studio verze 16.9, MSBuild 16.9 a .NET 5.0.200+ vyžadují NuGet.exe 5.9 nebo novější.

## <a name="summary-whats-new-in-59"></a>Shrnutí: Co je nového ve verze 5.9

* Přidání položky místní nabídky Aktualizovat pro závislosti balíčků, která spustí Správce balíčků uživatelské rozhraní s předem vybranou aktualizací balíčků – [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Aktualizace balíčku kliknutím pravým tlačítkem na balíček](media/releasenotes-59-update.png)

* Zobrazí požadovanou verzi (včetně žádosti o plovoucí verzi nebo rozsah verzí) ve sloupci Verze v seznamu projektů na úrovni řešení v uživatelském Správce balíčků – [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Požadovaná verze v uživatelském rozhraní Správce balíčků řešení](media/releasenotes-59-requested-version.png)

* Návrhy balíčků IntelliCode na kartě Procházet Správce balíčků uživatelského rozhraní vydané jako test A/B – [#10053](https://github.com/NuGet/Home/issues/10053)

* Rozšíření souboru `.nupkg.metadata` tak, aby zahrnoval zdroj instalace [– #10354](https://github.com/NuGet/Home/issues/10354)

* Zavedení nové vlastnosti nástroje msbuild pro vyloučení výstupu sestavení [](https://github.com/NuGet/Home/issues/10396) pro konkrétní TFM během úlohy #10396

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Žádosti o změnu návrhu:**

* Ikona dolů při instalaci nejnovější verze balíčku není intuitivní. Starý zelený kmitání byl dokonalý [– #9789](https://github.com/NuGet/Home/issues/9789)

* Podrobnost ladění Nugetu by měla říci, odkud balíček pochází – [#3055](https://github.com/NuGet/Home/issues/3055)

* Balíček NuGet by měl zachytit nesprávné vynechání tečky v číslech verzí – [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Zakázání připnutí centrálních tranzitivních závislostí – [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: Vyprodukuje chybu při chybějícím protokolu TPV [– #9441](https://github.com/NuGet/Home/issues/9441)

* Protokol balíčku contenthash během protokolování obnovení (během extrakce) [– #10384](https://github.com/NuGet/Home/issues/10384)

* Implementujte mechanismus předběžné registrace pro starší projekty PR, které volají obnovení v otevřeném řešení [– #9986](https://github.com/NuGet/Home/issues/9986)

* Doporučovač balíčků NuGet by měl fungovat, když je ve správci balíčků vybráno více než jeden zdroj – [#10433](https://github.com/NuGet/Home/issues/10433)

* Při obnovování s normálním podrobnostem protokolovat, ze kterého zdroje se balíček obnovuje – [#10461](https://github.com/NuGet/Home/issues/10461)

**Chyby:**

* INuGetPackageFileService – Načtení imagí a vložených licencí pro samostatné a připojené Codespaces – [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: Chybějící formátovací modul IProjectMetadataContextInfo – [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] Zmenšete informace zapsané do centralTransitiveDependencyGroups – [#10002](https://github.com/NuGet/Home/issues/10002)

* Operace obnovení, které vynětí z důvodu nenačítanosti projektu, se hlásí `NoOp` jako v telemetrii – [#9985](https://github.com/NuGet/Home/issues/9985)

* Ikony s určitými barevnými paletami způsobí, že uživatelské rozhraní PM způsobí selhání VS – [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf] Omezte klon PackageSpec při přidávání informací o CPVM – [#10003](https://github.com/NuGet/Home/issues/10003)

* Uživatelské rozhraní PM – načítání ikon asyncify – [#10009](https://github.com/NuGet/Home/issues/10009)

* Zpoždění uživatelského rozhraní při načítání adres URL ikon v uživatelském rozhraní PM – [#8505](https://github.com/NuGet/Home/issues/8505)

* Spřažení vláken ve vláknech BitmapSource a WPF UI – [#9161](https://github.com/NuGet/Home/issues/9161)

* Upozornění na upozornění NU5128, když packastool s aliasem targetframework [– #10097](https://github.com/NuGet/Home/issues/10097)

* Logika OutputPath v cílech Balíčku v přizpůsobených sestaveních nefunguje správně – [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: ukládání instance IServiceBroker do mezipaměti na [klientovi – #10141](https://github.com/NuGet/Home/issues/10141)

* Vytvoření Akce NuGetProjectActions pro odinstalaci z uživatelského rozhraní PM jako paralelní operace – [#9956](https://github.com/NuGet/Home/issues/9956)

* Výkon: Snižte počet chyb UIDelays v GetPackageSpecsAsync pro starší a jiné projekty než pr – [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` nenasudí více než jeden soubor – [#4393](https://github.com/NuGet/Home/issues/4393)

* Výstup se při přesměrování v systému macOS zabalí na 80 znaků – [#10198](https://github.com/NuGet/Home/issues/10198)

* Obnovení selže s možností -Source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp5.0-windows nezajme zpáteční cestu a neanasuje informace o platformě – [#10177](https://github.com/NuGet/Home/issues/10177)

* Vlastní projekty CPS vyžadují k obnovení schopnost projektu AssemblyReferences. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Kontrola existence souboru licencí a ikon by měla vždy používat porovnání s rozlišování malých a malých písmen – [#9817](https://github.com/NuGet/Home/issues/9817)

* Obnovení DotnetCLiToolReference ztěžuje úvahy o počtu projektů no-op/uptodateprojectscount – [#10038](https://github.com/NuGet/Home/issues/10038)

* Při procházení pomocí karty v dialogovém okně Zvolit formát balíčku NuGet Správce balíčků v tmavém motivu je obtížné zobrazit pole s pomlčkou [– #9729](https://github.com/NuGet/Home/issues/9729)

* Vyloučení tranzitivních odkazů architektury `CollectFrameworkReferences`  -  [z #10314](https://github.com/NuGet/Home/issues/10314)

* Porovnávací statické vlastnosti by měly být idempotentní [– #10339](https://github.com/NuGet/Home/issues/10339)

* řešení načítání sestavení interních kontraktů (oprava RPS nebo získání výjimky) [– #9919](https://github.com/NuGet/Home/issues/9919)

* Nahraďte GetService getServiceAsync v NuGet.Clients, část 1 – [#10362](https://github.com/NuGet/Home/issues/10362)

* Instalace rozhraní příkazového řádku by neměla instalovat neuvedené balíčky [– #7466](https://github.com/NuGet/Home/issues/7466)

* Static msbuild graph restore – unnnecessary logging about MSBuildStartupDirectory - [#10335](https://github.com/NuGet/Home/issues/10335)

* Project Dependencies of ProjectReferences marked as PrivateAssets should be included in the lock file up to date check - [#8565](https://github.com/NuGet/Home/issues/8565)

* Projekty SDK se špatnými daty nezobrazují chyby obnovení ve VS – [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 při obnovování řešení, které má smíšené projekty Legacy a netstandard2 z příkazového řádku s hodnotou LockedMode – [#9623](https://github.com/NuGet/Home/issues/9623)

* Balíček obsahuje obsah, který se přenesl prostřednictvím balíčků závislostí do balíčku aktuálního projektu (pouze projekty založené na sadě SDK) [– #8867](https://github.com/NuGet/Home/issues/8867)

* Přidání telemetrie pro chyby rozhraní VS API rozšiřitelnosti NuGetu – [#10062](https://github.com/NuGet/Home/issues/10062)

* Přidejte GenerateRestoreGraphFile do obnovení statického grafu, abyste zlepšili možnosti ladění.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Správce balíčků NuGet nelze otevřít – [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Předčítání nečte popisek Licence pro odkaz Apache-2.0 – [#10425](https://github.com/NuGet/Home/issues/10425)

* Aktuální stavová zpráva není ve VS skvělá – [#9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.jspoužívá nesprávnou cílovou rozhraní – [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: Oprava telemetrie https://github.com/NuGet/NuGet.Client/pull/3786  -  [z #10439](https://github.com/NuGet/Home/issues/10439)

* Chyba NU1004 zmizí při sestavování řešení po povolení možnosti RestoreLockedMode – [#8973](https://github.com/NuGet/Home/issues/8973)

* Při přechádování pomocí tabulátoru pmui v opačném směru by se měl zrcadlit směr [dopředu – #10234](https://github.com/NuGet/Home/issues/10234)

* Ladění PMUI v experimentální instanci někdy vyvolá výjimku InvalidCastException z SolutionView do ProjectView – [#10416](https://github.com/NuGet/Home/issues/10416)

* Výchozí verze je null po kliknutí na zastaralý balíček na kartě Procházet – [#10380](https://github.com/NuGet/Home/issues/10380)

* Správce NuGet v Visual Studio znovu načte po opětovném získání fokusu – [#4176](https://github.com/NuGet/Home/issues/4176)

* Odebrání IPackageSourceProvider2 a souvisejících typů [– #10098](https://github.com/NuGet/Home/issues/10098)

* Balíček NameOfPackage je nekompatibilní se všemi rozhraními v projektu [– #5127](https://github.com/NuGet/Home/issues/5127)

* Metoda CreateVersionsAsync nesrovnává nuGetVersion zbytečně – [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet.Client by měl nahradit použití ManagedImageMonikers za KnownMonikers – [#9977](https://github.com/NuGet/Home/issues/9977)

* Zastaralá ikona se překrývá s verzí zastaralého balíčku na kartě Procházet – [#10452](https://github.com/NuGet/Home/issues/10452)

* Zpracování chyb NU1604 PackageReference se liší v rámci sady VS a příkazového řádku (& Správce balíčků uživatelského rozhraní) – [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: nezaregistruje se nezbytné [formátovací](https://github.com/NuGet/Home/issues/10467) #10467

* Odebrání net45 jako cílové architektury z NuGet.Frameworks – [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementace – přidejte nové telemetrie pro sledování událostí souvisejících s pmc a využitím PowerShellu. - [#10142](https://github.com/NuGet/Home/issues/10142)

* V okně Náhled změn se zobrazí pouze jeden balíček, pokud je v [](https://github.com/NuGet/Home/issues/10483) uživatelském rozhraní nástroje Správce balíčků k dispozici #10483

* Při balení vícecílových projektů by se měly generovat prázdné skupiny frameworkReferences – [#10218](https://github.com/NuGet/Home/issues/10218)

* Při navigaci přes kartu Tab in Blue/Blue (Extra Contrast)/Light themes (Vysoký kontrast) / Světlé motivy je obtížné zobrazit zaškrtávací políčko balíčku na kartě Aktualizace je zamkřené pomocí pomlčky – [#8963](https://github.com/NuGet/Home/issues/8963)

* Zaškrtávací políčka karty Aktualizace nefungují dobře se čtečkami obrazovky – [#10449](https://github.com/NuGet/Home/issues/10449)

* Aktualizace v PMUI způsobí, že odkaz na objekt není nastavený na instanci objektu – [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementace – Přidejte nové telemetrie pro sledování událostí souvisejících s využitím PMC a PowerShellu. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Chyba kopírování a vkládání ve V2FeedPackageInfo [– #10480](https://github.com/NuGet/Home/issues/10480)

* Oprava NuGetPackageFileService – použití pro stream paměti na jedno použití – [#10503](https://github.com/NuGet/Home/issues/10503)

**[Seznam všech problémů opravených v této verzi – 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Seznam potvrzení v této verzi – 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Komunitní příspěvky

Děkujeme všem přispěvatelům, kteří této verzi NuGet pomohli udělat vynikající!

|Kdo|PRS|Problémy|
|----|----|----|
[omajid (id souboru)](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Chyba kopírování a vkládání ve V2FeedPackageInfo [– #10480](https://github.com/NuGet/Home/issues/10480)
[přichytávka-smyšlová](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Chybějící testy pro případ, kdy se na balíčky odkazuje atributem PrivateAssets="All" – [#10397](https://github.com/NuGet/Home/issues/10397)
[přichytávka-smyšlová](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Přidání podpory pro vkládání více balíčků – [#4393](https://github.com/NuGet/Home/issues/4393)
[přichytávka-smyšlová](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Sestavení knihoven NuGet je přerušeno, když je podepisování sestavení zakázané – [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Vyčištění dokumentace k přispívání – [#10399](https://github.com/NuGet/Home/issues/10399)
[Umisnídavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Kontrola existence souboru licencí a ikon by měla vždy používat porovnání s rozlišování malých a malých písmen – [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Alternativním řešením problému WPF při použití DecodePixelWidth – [#10037](https://github.com/NuGet/Home/issues/10037)
[b jejich úsece](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Windows SDK 10 v průvodci příspěvky pro klienta NuGet.Client – [#10099](https://github.com/NuGet/Home/issues/10099)
[b jejich úsece](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Relativní odkazy jsou v průvodci laděním NuGet.Client poškozené – [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Vylepšení testovacích testů a souvisejícího [kódu – #9996](https://github.com/NuGet/Home/issues/9996)
[rolfb tesne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Výstup se při přesměrování v systému macOS zabalí na 80 znaků – [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Získejte NuGet.PackageManagement jako .NET Standard balíček – [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Zavedení nové vlastnosti nástroje msbuild pro vyloučení výstupu sestavení [](https://github.com/NuGet/Home/issues/10396) pro konkrétní tfms během úlohy #10396

## <a name="summary-whats-new-in-591"></a>Shrnutí: Co je nového ve 5.9.1

* "dotnet nuget remove source nuget.org" nefunguje poprvé – [#10745](https://github.com/NuGet/Home/issues/10745)
* Zakázat výchozí ověřování v Linuxu, ale ve výchozím nastavení je povolené ve Windows – [#10713](https://github.com/NuGet/Home/issues/10713)

**[Seznam všech problémů opravených v této verzi – 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Seznam potvrzení v této verzi – 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="known-issues"></a>Známé problémy

### <a name="nuget-59-pack-raises-null-reference-exception---10685"></a>Balíček nuget 5.9 vyvolá `Null Reference` výjimku. - [#10685](https://github.com/NuGet/Home/issues/10685)

#### <a name="issue"></a>Problém
Při pokusu o použití souboru vyvolá verze výjimku, pokud jsou zadány explicitní odkazy na sestavení bez přidání jakéhokoli pro `pack` `.nuspec` `NuGet 5.9` `null reference` [](../reference/nuspec.md#explicit-assembly-references) `reference groups` projekty, které cílí na `multiple frameworks` .

#### <a name="workaround"></a>Alternativní řešení
Použijte `nuget.exe` [jinou verzi než 5.8.1](https://dist.nuget.org/win-x86-commandline/v5.8.1/nuget.exe)  nebo nejnovější `5.9.1` verzi.

## <a name="feedback-welcome"></a>Váš názor – vítejte

Vaše názory jsou pro nás důležité.  Pokud dojde k problémům s touto verzí, podívejte se na naše problémy [na GitHubu](https://github.com/NuGet/Home/issues) [a Visual Studio Developer Community](https://developercommunity.visualstudio.com/) o existujících problémech.  V případě nových problémů v rámci NuGetu nahlásit problém [GitHubu.](https://github.com/NuGet/Home/issues/new)
V případě obecných problémů s prostředím NuGet nás dejte vědět prostřednictvím možnosti Nahlásit problém, která se nachází ve vašem oblíbeném integrovaném vývojovém prostředí (IDE) v části Help > Report a Problem (Nahlásit **problém).** [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)
