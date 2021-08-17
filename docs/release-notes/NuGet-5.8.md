---
title: zpráva k vydání verze NuGet 5,8
description: poznámky k verzi NuGet 5,8, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: fca9d2d068aadec207bfbf12f3ea82af872825a5
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209927"
---
# <a name="nuget-58-release-notes"></a>zpráva k vydání verze NuGet 5,8

NuGet distribučních vozidel:

| verze NuGet | k dispozici ve verzi Visual Studio | K dispozici v sadě .NET SDK |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [verze Visual Studio 2019 16,8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1</sup> nainstalovaná s Visual Studio 2019 s úlohou .net Core
  
> [!NOTE]
> Visual Studio 16,8, MSBuild 16,8 a .net 5,0 vyžadují NuGet.exe 5,8 nebo novější.


## <a name="summary-whats-new-in-58"></a>Shrnutí: Novinky v 5,8
🎉 **toto je první verze, která nabízí úplnou podporu vytváření a obnovení balíčků NuGet cílících na rozhraní .net 5,0** 🎉

* Urychlení extrakce nupkg pomocí MMAP/CreateFileMapping- [#9807](https://github.com/NuGet/Home/issues/9807)

* zobrazit podrobnosti o ohrožení zabezpečení balíčku v podokně podrobností balíčku uživatelského rozhraní Správce balíčků – [#9850](https://github.com/NuGet/Home/issues/9850)

* ověření podepsaných balíčků NuGet pomocí nového [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) příkazu [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) podporuje `--prerelease` možnost Přidat nejnovější verzi balíčku, včetně předprodejních verzí – [#4699](https://github.com/NuGet/Home/issues/4699)

* Vyhledat balíčky v rozhraní [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) příkazového řádku pomocí příkazu [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) příkaz podporuje `--verbosity` možnost – [#9600](https://github.com/NuGet/Home/issues/9600)

* povolení optimalizace rychlého No-Op obnovení pro projekty založené na PackageReference ve stylu csproj v Visual Studio- [#9565](https://github.com/NuGet/Home/issues/9565)

* úroveň řešení Správce balíčků operace uživatelského rozhraní, jako jsou instalace a aktualizace balíčků, jsou až do 10x rychlejší – [#6010](https://github.com/NuGet/Home/issues/6010)

* několik dalších NuGet vylepšení výkonu Visual Studio- [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984) [#10052 #9903](https://github.com/NuGet/Home/issues/10052) [](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chcete odeslat obecnou**

* .NET 5,0 TFM: pravidla priorit architektury – [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet by při analýze TargetFramework- [#9842](https://github.com/NuGet/Home/issues/9842) neměla odvodit verzi platformy teček.

* Použijte TargetFrameworkMoniker & TargetPlatformMoniker k odvodit architektury namísto použití jednotlivých TFI, TFV, TPI, TPV Properties- [#9895](https://github.com/NuGet/Home/issues/9895)

* Aktualizace `GetReferenceNearestTargetFrameworkTask()` pro podporu cílových rozhraní s platformami (například NET 5.0-Windows) – [#9894](https://github.com/NuGet/Home/issues/9894)

* rozhraní .net 5,0 Visual Studio rozhraní api – [#9650](https://github.com/NuGet/Home/issues/9650)

* Správce balíčků Uživatelské rozhraní: operace konsolidovat nebo aktualizovat balíčky by neměly být zablokované kvůli chybám (downgrade balíčků atd.) – [#9224](https://github.com/NuGet/Home/issues/9224)

* NuGet funkce by se měly vysvětlovat pro projekty, které mají schopnost; "PackageReferences" – [#9957](https://github.com/NuGet/Home/issues/9957)

* potlačit No-Op obnovení zpráv v Visual Studio- [#6384](https://github.com/NuGet/Home/issues/6384)

**Chyby:**

* Konstruktor OutputWindowTextWriter by neměl být volán pro vlákno na pozadí – [#9764](https://github.com/NuGet/Home/issues/9764)

* Obnovte podepsané balíčky na procesorech big endian – [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger by neměl volat metody spřažené v konstruktorech MEF – [#9591](https://github.com/NuGet/Home/issues/9591)

* Chyba v NuGet. CommandLine. Console `PrintJustified()` – Metoda – [#9737](https://github.com/NuGet/Home/issues/9737)

* Správce balíčků Nevrácení paměti uživatelského rozhraní, když je metadata balíčku uvolněna z paměti z důvodu chybné vazby [#9757](https://github.com/NuGet/Home/issues/9757)

* Hlašuje v Seznam chyb se při instalaci podepsaného balíčku s packages.config formátu v Správce balíčků uživatelském rozhraní nezobrazilo žádné upozornění [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. Příkaz CommandLine. XPlat by neměl mít veřejná rozhraní API – [#9821](https://github.com/NuGet/Home/issues/9821)

* Zmenšení kolizí prostředků v době načtení řešení způsobené blokováním vlákna vlákna ve fondu s `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* při obnovení příkazového řádku s více cílovými projekty by NuGet měly číst informace o cílovém rozhraní, které se vztahují na vnitřní sestavení- [#9869](https://github.com/NuGet/Home/issues/9869)

* Čtení grafu identifikátoru za běhu prostřednictvím položky TargetFrameworkInformation- [#9874](https://github.com/NuGet/Home/issues/9874)

* statické obnovení grafu je nekonzistentní s ohledem na vlastnost CrossTargeting ve srovnání s Visual Studio a pravidelným obnovením MSBuild vyhodnocení [#9881](https://github.com/NuGet/Home/issues/9881)

* v rámci statického obnovení grafu s více cílovými projekty by NuGet mělo číst cílové rozhraní související informace z vnitřního sestavení. - [#9870](https://github.com/NuGet/Home/issues/9870)

* povolení `net5.0-platform` načtení a obnovení projektů v Visual Studio- [#9863](https://github.com/NuGet/Home/issues/9863)

* zobrazit přeloženou verzi v uživatelském rozhraní Správce balíčků – [#9826](https://github.com/NuGet/Home/issues/9826)

* Správce balíčků uživatelské rozhraní: Průzkumník řešení nezobrazuje všechny závislosti balíčků NuGet – [#9898](https://github.com/NuGet/Home/issues/9898)

* Aktualizace seznamu licencí SPDX – [#9946](https://github.com/NuGet/Home/issues/9946)

* VS 2019 zhroucení po otevření spravovat NuGet balíčky: ikona způsobuje neošetřenou výjimku v imagi conversio- [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Balení. extrakce vyžaduje ilmerge Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)

* Balení s ContinuePackingAfterGeneratingNuspec = false by nemělo selhat, pokud nejsou k dispozici žádné chyby – [#9786](https://github.com/NuGet/Home/issues/9786)

* Správce balíčků UI: ikony nemění správně barvy – [#10017](https://github.com/NuGet/Home/issues/10017)

* Nesprávný počet projektů pro aktualizované a No-Op projekty při obnovení – [#10026](https://github.com/NuGet/Home/issues/10026)

* Použití `/p:RestoreUseStaticGraphEvaluation=true` výsledků v hodnotě nemůže být null – [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` nepoužitý alias pro projekty knihovny WPF – [#10020](https://github.com/NuGet/Home/issues/10020)

* Správce balíčků UI: NullReferenceException při neúspěšném ověření podpisu – [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: Nepoužívejte `object` typ pro hodnoty metadat projektu – [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: ukládání zdrojů balíčků do možností nástroje přepíše přihlašovací údaje – [#9711](https://github.com/NuGet/Home/issues/9711)


**[Seznam všech problémů opravených v této verzi – 5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Seznam problémů v této verzi – 5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Komunitní příspěvky

děkujeme všem přispěvatelům, kteří vám pomohl tuto NuGet vydávat.

|Kdo|PR|Problémy|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Překlep v chybové zprávě. "správce" místo "správce" – [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | NuGet Vyžaduje se balíček s neplatnými AssemblyInformationalVersion sestavami – [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` nepoužívá se pro větev a vlastnosti potvrzení – [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | kliknutí na kód na NU v Visual Studio Seznam chyb okno by mělo přejít na [https://docs.microsoft.com/nuget/reference/errors-and-warnings/](/nuget/reference/errors-and-warnings/)  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | při přidávání nového zdroje balíčků prostřednictvím možností Visual Studio použijte ' https://' – [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problémy s výkonem na mono- [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Přidejte TypeConverter pro třídu SemanticVersion- [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Shrnutí: co je nového v 5.8.1

* packages.config package.lock.jsna používá nesprávnou cílovou architekturu v 5,8 – [#10257](https://github.com/NuGet/Home/issues/10257)

* 5,8 + 16,8 nemůže vyřešit přenositelné závislosti projektů při smíchání PackageReference a packages.config- [#10326](https://github.com/NuGet/Home/issues/10326)

**[Seznam všech problémů opravených v tomto vydání – 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Seznam potvrzení v tomto vydání – 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Úvodní názory

Váš názor je pro nás důležitý.  pokud se v této verzi vyskytnou nějaké problémy, podívejte se na naše [problémy s GitHub](https://github.com/NuGet/Home/issues) a [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) pro stávající problémy.  V případě nových problémů v NuGet nahlásit problém [GitHub problémy.](https://github.com/NuGet/Home/issues/new)
V případě obecných NuGet problémů s [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) prostředím nám dejte vědět prostřednictvím možnosti Nahlásit problém, která se nachází ve vašem oblíbeném integrovaném vývojovém prostředí v části **Nápověda > ohlásit problém.**