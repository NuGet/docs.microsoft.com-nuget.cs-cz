---
title: Zpráva k vydání verze NuGet 5,8
description: Poznámky k verzi pro NuGet 5,8, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 550971d77ed4b15129fdc58fef95e0cceda8d8d1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776166"
---
# <a name="nuget-58-release-notes"></a>Zpráva k vydání verze NuGet 5,8

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio | K dispozici v sadě .NET SDK |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1</sup> nainstaloval se se sadou Visual Studio 2019 s úlohou .NET Core.
  
> [!NOTE]
> Visual Studio 16,8, MSBuild 16,8 a .NET 5,0 vyžadují NuGet.exe 5,8 nebo novější.


## <a name="summary-whats-new-in-58"></a>Shrnutí: Novinky v 5,8
🎉 **Toto je první verze, která nabízí úplnou podporu pro balíčky NuGet cílené na .net 5,0** 🎉

* Urychlení extrakce nupkg pomocí MMAP/CreateFileMapping- [#9807](https://github.com/NuGet/Home/issues/9807)

* Zobrazit podrobnosti o ohrožení zabezpečení balíčku v podokně podrobností balíčku uživatelského rozhraní Správce balíčků – [#9850](https://github.com/NuGet/Home/issues/9850)

* Ověření podepsaných balíčků NuGet pomocí nového [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) příkazu [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) podporuje `--prerelease` možnost Přidat nejnovější verzi balíčku, včetně předprodejních verzí – [#4699](https://github.com/NuGet/Home/issues/4699)

* Vyhledat balíčky v rozhraní [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) příkazového řádku pomocí příkazu [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) příkaz podporuje `--verbosity` možnost – [#9600](https://github.com/NuGet/Home/issues/9600)

* Povolení Optimalizace rychlého obnovení No-Op pro projekty založené na stylu csproj v aplikaci Visual Studio – [#9565](https://github.com/NuGet/Home/issues/9565)

* Operace uživatelského rozhraní Správce balíčků na úrovni řešení, jako je instalace balíčků a aktualizace, jsou až 10x rychlejší – [#6010](https://github.com/NuGet/Home/issues/6010)

* Několik dalších vylepšení výkonu NuGet v aplikaci Visual Studio – [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052) [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chcete odeslat obecnou**

* .NET 5,0 TFM: pravidla priorit architektury – [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet by neměl při analýze [#9842](https://github.com/NuGet/Home/issues/9842) targetFramework odvodit verzi platformy teček.

* Použijte TargetFrameworkMoniker & TargetPlatformMoniker k odvodit architektury namísto použití jednotlivých TFI, TFV, TPI, TPV Properties- [#9895](https://github.com/NuGet/Home/issues/9895)

* Aktualizace `GetReferenceNearestTargetFrameworkTask()` pro podporu cílových rozhraní s platformami (například NET 5.0-Windows) – [#9894](https://github.com/NuGet/Home/issues/9894)

* Rozhraní .NET 5,0 Visual Studio API – [#9650](https://github.com/NuGet/Home/issues/9650)

* Uživatelské rozhraní Správce balíčků: operace konsolidovat nebo aktualizovat balíčky by neměly být blokované z důvodu chyb (downgrade balíčků atd.) – [#9224](https://github.com/NuGet/Home/issues/9224)

* Funkce NuGet by se měly pro projekty, které mají schopnost, vysvětlovat. "PackageReferences" – [#9957](https://github.com/NuGet/Home/issues/9957)

* Potlačit No-Op obnovení zpráv v aplikaci Visual Studio – [#6384](https://github.com/NuGet/Home/issues/6384)

**Chyby:**

* Konstruktor OutputWindowTextWriter by neměl být volán pro vlákno na pozadí – [#9764](https://github.com/NuGet/Home/issues/9764)

* Obnovte podepsané balíčky na procesorech big endian – [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger by neměl volat metody spřažené v konstruktorech MEF – [#9591](https://github.com/NuGet/Home/issues/9591)

* Chyba v NuGet. CommandLine. Console `PrintJustified()` – Metoda- [#9737](https://github.com/NuGet/Home/issues/9737)

* Nevracení paměti uživatelského rozhraní Správce balíčků při uvolnění metadat balíčku z důvodu chybné vazby – [#9757](https://github.com/NuGet/Home/issues/9757)

* Hlašuje V Seznam chyb při instalaci podepsaného balíčku s packages.config formátu v uživatelském rozhraní Správce balíčků se nezobrazí žádné upozornění [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine. XPlat by neměl mít veřejná rozhraní API – [#9821](https://github.com/NuGet/Home/issues/9821)

* Zmenšení kolizí prostředků v době načtení řešení způsobené blokováním vlákna vlákna ve fondu s `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* V rámci obnovení příkazového řádku s více cílenými projekty by měl NuGet číst cílové rozhraní, které souvisí s informacemi z vnitřního sestavení- [#9869](https://github.com/NuGet/Home/issues/9869)

* Čtení grafu identifikátoru za běhu prostřednictvím položky TargetFrameworkInformation- [#9874](https://github.com/NuGet/Home/issues/9874)

* Statické obnovení grafu je nekonzistentní s ohledem na vlastnost CrossTargeting ve srovnání se sadou Visual Studio a pravidelným obnovením nástroje MSBuild – [#9881](https://github.com/NuGet/Home/issues/9881)

* V rámci statického obnovení grafu s více cílenými projekty by měl NuGet číst cílové rozhraní související informace z interního sestavení. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Povolení `net5.0-platform` načtení a obnovení projektů v aplikaci Visual Studio – [#9863](https://github.com/NuGet/Home/issues/9863)

* Zobrazit přeloženou verzi v uživatelském rozhraní Správce balíčků – [#9826](https://github.com/NuGet/Home/issues/9826)

* Uživatelské rozhraní Správce balíčků: Průzkumník řešení nezobrazuje všechny závislosti balíčků NuGet – [#9898](https://github.com/NuGet/Home/issues/9898)

* Aktualizace seznamu licencí SPDX – [#9946](https://github.com/NuGet/Home/issues/9946)

* VS 2019 zhroucení po otevření spravovat balíčky NuGet: ikona způsobuje neošetřenou výjimku v imagi Conversio- [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. balení. extrakce vyžaduje ilmerge Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)

* Balení s ContinuePackingAfterGeneratingNuspec = false by nemělo selhat, pokud nejsou k dispozici žádné chyby – [#9786](https://github.com/NuGet/Home/issues/9786)

* Uživatelské rozhraní Správce balíčků: ikony nemění správně barvy – [#10017](https://github.com/NuGet/Home/issues/10017)

* Nesprávný počet projektů pro aktualizované a No-Op projekty při obnovení – [#10026](https://github.com/NuGet/Home/issues/10026)

* Použití `/p:RestoreUseStaticGraphEvaluation=true` výsledků v hodnotě nemůže být null – [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` nepoužitý alias pro projekty knihovny WPF – [#10020](https://github.com/NuGet/Home/issues/10020)

* Uživatelské rozhraní Správce balíčků: NullReferenceException, když se ověřování signatury nezdařilo- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: Nepoužívejte `object` typ pro hodnoty metadat projektu – [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: ukládání zdrojů balíčků do možností nástroje přepíše přihlašovací údaje – [#9711](https://github.com/NuGet/Home/issues/9711)


**[Seznam všech problémů opravených v této verzi – 5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Seznam problémů v této verzi – 5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Komunitní příspěvky

Děkujeme všem přispěvatelům, kteří vám pomohl tuto verzi NuGet udělat.

|Kdo|PR|Problémy|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Překlep v chybové zprávě. "správce" místo "správce" – [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | Sada NuGet Pack s neplatnými sestavami AssemblyInformationalVersion je povinná – [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` nepoužívá se pro větev a vlastnosti potvrzení – [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Kliknutí na kód Nu v okně Visual studia seznam chyb by měl přejít na https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Při přidávání nového zdroje balíčků pomocí možností sady Visual Studio použijte ' https://' – [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problémy s výkonem na mono- [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Přidejte TypeConverter pro třídu SemanticVersion- [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Shrnutí: co je nového v 5.8.1

* packages.config package.lock.jsna používá nesprávnou cílovou architekturu v 5,8 – [#10257](https://github.com/NuGet/Home/issues/10257)

* 5,8 + 16,8 nemůže vyřešit přenositelné závislosti projektů při smíchání PackageReference a packages.config- [#10326](https://github.com/NuGet/Home/issues/10326)

**[Seznam všech problémů opravených v tomto vydání – 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Seznam potvrzení v tomto vydání – 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Úvodní názory

Váš názor je pro nás důležitý.  Pokud se v této verzi vyskytnou nějaké problémy, podívejte se na naše [problémy GitHubu](https://github.com/NuGet/Home/issues) a [komunitu vývojářů pro Visual Studio](https://developercommunity.visualstudio.com/) , kde najdete stávající problémy.  Pro nové problémy v rámci NuGet ohlaste [problém GitHubu](https://github.com/NuGet/Home/issues/new).
Pro obecné problémy s prostředím NuGet nám dejte informace v části **Help > nahlásit problém** pomocí možnosti [nahlásit problém](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) , která se nachází ve vašem oblíbeném prostředí IDE.