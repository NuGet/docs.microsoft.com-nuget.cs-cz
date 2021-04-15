---
title: Zpráva k vydání verze NuGet 5,9
description: Poznámky k verzi pro NuGet 5,9, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 50fd277a4f1f39b4a68a89cd07af4e21f0d3d831
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508810"
---
# <a name="nuget-59-release-notes"></a>Zpráva k vydání verze NuGet 5,9

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio | K dispozici v sadě .NET SDK |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> nainstaloval se se sadou Visual Studio 2019 s úlohou .NET Core.
  
> [!NOTE]
> Sady Visual Studio 16,9, MSBuild 16,9 a .NET 5.0.200 + vyžadují NuGet.exe 5,9 nebo novější.

## <a name="summary-whats-new-in-59"></a>Shrnutí: Novinky v 5,9

* Přidejte položku kontextové nabídky aktualizovat pro závislosti balíčků, které spustí uživatelské rozhraní Správce balíčků s předem vybranými balíčky k aktualizaci [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Klikněte pravým tlačítkem na možnost aktualizovat možnosti balíčku.](media/releasenotes-59-update.png)

* Zobrazit požadovanou verzi (včetně plovoucí verze nebo požadavku na rozsah verze) ve sloupci "verze" v seznamu projektu v uživatelském rozhraní Správce balíčků na úrovni řešení – [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Požadovaná verze v uživatelském rozhraní Správce balíčků na úrovni řešení](media/releasenotes-59-requested-version.png)

* Návrhy balíčku IntelliCode na kartě procházení uživatelského rozhraní Správce balíčků vydaná jako #10053 A/B test- [](https://github.com/NuGet/Home/issues/10053)

* Rozšíříte `.nupkg.metadata` soubor tak, aby zahrnoval zdroj instalace – [#10354](https://github.com/NuGet/Home/issues/10354)

* Zavést novou vlastnost MSBuild pro vyloučení výstupu sestavení pro konkrétní TFM během úlohy balíčku – [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chcete odeslat obecnou (návrh žádosti o změnu):**

* Ikona ikony dolů, když je nainstalovaná nejnovější verze balíčku, není intuitivní. Starý zelený impuls byl dokonalý – [#9789](https://github.com/NuGet/Home/issues/9789)

* Podrobnost ladění NuGet by měla vyslovit, kdy balíček pochází z- [#3055](https://github.com/NuGet/Home/issues/3055)

* Sada NuGet Pack by měla zachytit nesprávné vynechání tečky v číslech verze – [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Zakázat připnutí centrálních přenosných závislostí – [#10132](https://github.com/NuGet/Home/issues/10132)

* NET5 TFM: vyprodukuje chybu, když chybí TPV- [#9441](https://github.com/NuGet/Home/issues/9441)

* Během extrahování contenthash balíček protokolu (během extrakce) – [#10384](https://github.com/NuGet/Home/issues/10384)

* Implementace mechanismu před registrací pro starší projekty žádosti o přijetí změn, které volají obnovení při řešení Open- [#9986](https://github.com/NuGet/Home/issues/9986)

* Doporučený balíček NuGet by měl fungovat, když je ve Správci balíčků vybrán více než jeden zdroj – [#10433](https://github.com/NuGet/Home/issues/10433)

* Při obnovení při normálním podrobném podrobnostech se protokoluje, že se zdrojový balíček obnovuje [#10461](https://github.com/NuGet/Home/issues/10461)

**Chyby:**

* INuGetPackageFileService – načtení imagí a vložených licencí pro Codespaces a samostatnou [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: IProjectMetadataContextInfo chybí modul pro formátování [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-perf] Omezte informace zapsané do centralTransitiveDependencyGroups- [#10002](https://github.com/NuGet/Home/issues/10002)

* Operace obnovení, které se vyvolají kvůli nenačtenému projektu, jsou hlášeny jako `NoOp` v telemetrii – [#9985](https://github.com/NuGet/Home/issues/9985)

* Ikony s určitými barevnými paletami způsobují selhání uživatelského rozhraní pro odpoledne a [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-perf] Omezit klon PackageSpec při přidávání informací CPVM – [#10003](https://github.com/NuGet/Home/issues/10003)

* Uživatelské rozhraní PM – ikona asyncify načítání – [#10009](https://github.com/NuGet/Home/issues/10009)

* Zpoždění uživatelského rozhraní při načítání adres URL ikon v uživatelském rozhraní PM – [#8505](https://github.com/NuGet/Home/issues/8505)

* Spřažení vláken v vláknech uživatelského rozhraní BitmapSource a WPF – [#9161](https://github.com/NuGet/Home/issues/9161)

* Upozornění pro upozornění NU5128 při packastool s aliasem targetFramework – [#10097](https://github.com/NuGet/Home/issues/10097)

* Logika OutputPath v cílech balíčku v přizpůsobeném sestavení nefunguje správně – [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: IServiceBroker instance mezipaměti v klientovi – [#10141](https://github.com/NuGet/Home/issues/10141)

* Vytvoření NuGetProjectActions pro odinstalaci z uživatelského rozhraní PM paralelní operace – [#9956](https://github.com/NuGet/Home/issues/9956)

* Výkon: Snižte UIDelays v GetPackageSpecsAsync pro starší projekty a nepr projekty – [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` nenabízí více než jeden soubor – [#4393](https://github.com/NuGet/Home/issues/4393)

* Výstup se zabalí za 80 znaků v macOS při přesměrování – [#10198](https://github.com/NuGet/Home/issues/10198)

* Obnovení selhalo se zdrojem <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp 5.0 – Windows nezaokrouhluje Trip a neanalyzuje informace o platformě – [#10177](https://github.com/NuGet/Home/issues/10177)

* Vlastní projekty CPS vyžadují schopnost projektu odkazy AssemblyReferences, aby se daly obnovit. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Při kontrole existence souboru s licencí a ikonami by měla být vždy použita porovnávání s rozlišováním velkých a malých písmen – [#9817](https://github.com/NuGet/Home/issues/9817)

* Obnovení DotnetCLiToolReference je obtížné kvůli neurčitému počtu projektů no-op nebo uptodateprojectscount- [#10038](https://github.com/NuGet/Home/issues/10038)

* Těžko se při navigaci na kartě v dialogovém okně Volba formátu správce balíčků NuGet v tmavém motivu zobrazí pole s přerušovaným řádkem, [#9729](https://github.com/NuGet/Home/issues/9729)

* Vyloučit odkazy na přenositelné rozhraní z `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* Statické vlastnosti porovnávače by měly být idempotentní- [#10339](https://github.com/NuGet/Home/issues/10339)

* vyřešit načítání sestavení interních smluv (oprava RPS nebo Get Exception) – [#9919](https://github.com/NuGet/Home/issues/9919)

* Nahraďte příkaz GetService pomocí GetServiceAsync v NuGet. clients, část 1 – [#10362](https://github.com/NuGet/Home/issues/10362)

* Instalace rozhraní příkazového řádku by neměly instalovat neuvedené balíčky – [#7466](https://github.com/NuGet/Home/issues/7466)

* Statické obnovení grafu MSBuild – unnnecessary protokolování informací o MSBuildStartupDirectory- [#10335](https://github.com/NuGet/Home/issues/10335)

* Závislosti projektu ProjectReferences označené jako PrivateAssets by neměly být zahrnuty do stavu souboru zámku – [#8565](https://github.com/NuGet/Home/issues/8565)

* Projekty SDK s chybnými daty nezobrazuje chyby při obnovení ve VS- [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 při obnovení řešení, které obsahuje smíšené starší verze a projekty netstandard2 z příkazového řádku s LockedMode- [#9623](https://github.com/NuGet/Home/issues/9623)

* Sada zahrnuje obsah, který se v balíčcích závislostí do balíčku aktuálního projektu (jenom projekty založené na sadě SDK) – [#8867](https://github.com/NuGet/Home/issues/8867)

* Přidání telemetrie pro chyby rozhraní API rozšiřitelnosti sady NuGet a [#10062](https://github.com/NuGet/Home/issues/10062)

* Přidejte GenerateRestoreGraphFile do statického obnovení grafu pro zlepšení ladění.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Správce balíčků NuGet nejde otevřít – [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Narrator nečte označení "License" (licence ") pro linku Apache-2,0, [#10425](https://github.com/NuGet/Home/issues/10425)

* Aktuální zpráva stavového řádku není v sadě VS- [#9402](https://github.com/NuGet/Home/issues/9402) Skvělé.

* packages.config package.lock.jsna používá nesprávnou cílovou architekturu – [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: Oprava telemetrie z https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* Při sestavování řešení po povolení "RestoreLockedMode" se při sestavování řešení Error NU1004 zmizí. [#8973](https://github.com/NuGet/Home/issues/8973)

* Procházení tabulátory prostřednictvím PMUI v opačném případě by mělo zrcadlové směrování mezi [#10234](https://github.com/NuGet/Home/issues/10234)

* Ladění PMUI v experimentální instanci někdy vyvolá InvalidCastException od SolutionView do ProjectView- [#10416](https://github.com/NuGet/Home/issues/10416)

* Výchozí verze je null po kliknutí na vyřazený balíček na kartě Procházet – [#10380](https://github.com/NuGet/Home/issues/10380)

* Správce NuGet v aplikaci Visual Studio se znovu načte při opětovném získání fokusu – [#4176](https://github.com/NuGet/Home/issues/4176)

* Odebrat IPackageSourceProvider2 a související typy – [#10098](https://github.com/NuGet/Home/issues/10098)

* Balíček ' NameOfPackage ' není kompatibilní s architekturou ' All ' v projektu – [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync nepotřebné NuGetVersiony porovnává – [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet. Client by měl nahradit pomocí ManagedImageMonikers s KnownMonikers- [#9977](https://github.com/NuGet/Home/issues/9977)

* Zastaralá ikona se překrývá s verzí zastaralého balíčku na kartě Procházet – [#10452](https://github.com/NuGet/Home/issues/10452)

* Zpracování chyb PackageReference NU1604 se v nástroji VS a příkazovém řádku liší (obnovení & uživatelského rozhraní Správce balíčků) – [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: nezbytné formátovací moduly nejsou registrovány – [#10467](https://github.com/NuGet/Home/issues/10467)

* Odeberte Net45 jako cílovou architekturu z NuGet. Frameworks – [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementace – přidejte nové telemetrií pro sledování událostí souvisejících s využitím PMC a prostředí PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Když je v uživatelském rozhraní Správce balíčků k dispozici více balíčků pro aktualizaci, je v okně Náhled změn zobrazen pouze jeden balíček – [#10483](https://github.com/NuGet/Home/issues/10483)

* Při balení projektů s více cíli by se měly vygenerovat prázdné frameworkReferences skupiny – [#10218](https://github.com/NuGet/Home/issues/10218)

* Těžko vidíte, že se zaškrtávací políčko balení na kartě aktualizace zaměřuje na přerušované pole, když přejdete přes kartu modře-modrý (extra Contrast)/Light motivy – [#8963](https://github.com/NuGet/Home/issues/8963)

* Zaškrtávací políčka na kartě aktualizace nefungují dobře s čtečkami obrazovky – [#10449](https://github.com/NuGet/Home/issues/10449)

* Aktualizace v PMUI způsobí, že odkaz na objekt není nastavený na instanci objektu – [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementace – přidejte nové telemetrií pro sledování událostí souvisejících s PMC a využitím prostředí PowerShell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Chyba kopírování a vkládání v V2FeedPackageInfo – [#10480](https://github.com/NuGet/Home/issues/10480)

* NuGetPackageFileService Fix – použití pro použití pro typu MemoryStream není- [#10503](https://github.com/NuGet/Home/issues/10503)

**[Seznam všech problémů opravených v tomto vydání – 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Seznam potvrzení v tomto vydání – 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Komunitní příspěvky

Děkujeme všem přispěvatelům, kteří vám pomohl tuto verzi NuGet udělat.

|Kdo|PR|Problémy|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Chyba kopírování a vkládání v V2FeedPackageInfo – [#10480](https://github.com/NuGet/Home/issues/10480)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Chybějící testy pro případ, kde jsou balíčky odkazovány pomocí PrivateAssets = "All" atributu- [#10397](https://github.com/NuGet/Home/issues/10397)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Přidání podpory pro vložení více balíčků – [#4393](https://github.com/NuGet/Home/issues/4393)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Sestavení knihoven NuGet je přerušeno, když je zakázáno podepisování sestavení- [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Vyčištění přispívajících dokumentů – [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Při kontrole existence souboru s licencí a ikonami by měla být vždy použita porovnávání s rozlišováním velkých a malých písmen – [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Použití BitmapCreateOptions. IgnoreColorProfile k řešení potíží s WPF při použití DecodePixelWidth- [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | V NuGet je přerušeno propojení Windows SDK 10. Průvodce příspěvkem klienta – [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Relativní odkazy jsou v NuGetu poškozené. Průvodce laděním klienta – [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Zlepšení zkušebních přípravek a souvisejících [#9996](https://github.com/NuGet/Home/issues/9996) kódu
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Výstup se zabalí za 80 znaků v macOS při přesměrování – [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Zpřístupnit NuGet. PackageManagement jako balíček .NET Standard – [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Zavést novou vlastnost MSBuild pro vyloučení výstupu sestavení pro konkrétní TFM během úlohy balíčku – [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>Shrnutí: co je nového v 5.9.1

* "dotnet NuGet Remove source nuget.org" při prvním [#10745](https://github.com/NuGet/Home/issues/10745) nefunguje
* Nastavit výchozí ověřování v systému Linux, ale ve výchozím nastavení povoleno ve Windows – [#10713](https://github.com/NuGet/Home/issues/10713)

**[Seznam všech problémů opravených v tomto vydání – 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Seznam potvrzení v tomto vydání – 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="feedback-welcome"></a>Úvodní názory

Váš názor je pro nás důležitý.  Pokud se v této verzi vyskytnou nějaké problémy, podívejte se na naše [problémy GitHubu](https://github.com/NuGet/Home/issues) a [komunitu vývojářů pro Visual Studio](https://developercommunity.visualstudio.com/) , kde najdete stávající problémy.  Pro nové problémy v rámci NuGet ohlaste [problém GitHubu](https://github.com/NuGet/Home/issues/new).
Pro obecné problémy s prostředím NuGet nám dejte informace v části **Help > nahlásit problém** pomocí možnosti [nahlásit problém](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) , která se nachází ve vašem oblíbeném prostředí IDE.
