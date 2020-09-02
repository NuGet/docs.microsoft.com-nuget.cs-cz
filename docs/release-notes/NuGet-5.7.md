---
title: Zpráva k vydání verze NuGet 5,7
description: Poznámky k verzi pro NuGet 5,7, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364164"
---
# <a name="nuget-57-release-notes"></a>Zpráva k vydání verze NuGet 5,7

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio | K dispozici v sadě .NET SDK |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> nainstaloval se se sadou Visual Studio 2019 s úlohou .NET Core.

## <a name="summary-whats-new-in-57"></a>Shrnutí: Novinky v 5,7

### <a name="features-added-in-this-release"></a>Funkce přidané v této verzi

* Přidání podpory externího aliasu pro odkazy na balíček NuGet – [#4989](https://github.com/NuGet/Home/issues/4989)

* Umožnění přepínání mezi nainstalovanými a aktualizovanými kartami rychleji tím, že jim umožní sdílet zdroj dat a snižovat resfreshing [#8294](https://github.com/NuGet/Home/issues/8294)

* Rychlejší obnovení a zrychlení při vyvolání rozhraní API pro statické grafy MSBuild (dotnet.exe) – [#9644](https://github.com/NuGet/Home/issues/9644)

* Přidání částečného obnovení sady Visual Studio pro projekty PackageReference (No-OP + +) – [#9513](https://github.com/NuGet/Home/issues/9513)

* V uživatelském rozhraní Správce balíčků sady Visual Studio dojde k chybě méně často při hledání chybných zdrojů balíčků, které vracejí více než požadovaný počet výsledků na požadavek HTTP. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Přidání integrace informací PackageVersion pro projekty ve stylu mimo sadu SDK v sadě VS Restore- [#9236](https://github.com/NuGet/Home/issues/9236)

* Přidání podpory pro nuget.exe aktualizace `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Přidání podpory pro více konfiguračních souborů v adresáři%APPDATA%\NuGet – [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths nyní přebírá zdrojové balíčky NuGet v účtu – [#9431](https://github.com/NuGet/Home/issues/9431)

* Přidání rozhraní API pro rozšíření INuGetProjectService. GetInstalledPackagesAsync – [#9702](https://github.com/NuGet/Home/issues/9702)

* Přidání rozhraní API pro vzájemné vytváření výčtu záložních složek bez vyžadování řešení/projektu [#9395](https://github.com/NuGet/Home/issues/9395)

* Přidání `latest` Možnosti pro `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chyby:**

* Pokud není definovaná proměnná prostředí, zkuste v rámci příkazu dotnet CLI při spouštění modulů plug-in pro přihlašovací údaje vyzkoušet příkaz dotnet CLI v systémové cestě `DOTNET_HOST_PATH`  . - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe spec vygeneruje značku copyrightu s pevně zakódovaným textem Copyright yyyy místo `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe vyvolá výjimku "Authors Required" během balení vlastnosti csproj ignorovat zástupné symboly a atributy AssemblyInfo, pokud se změní název sestavení- [#4234](https://github.com/NuGet/Home/issues/4234)

* Zprávy HttpRequestMessage se opakovaně používá několikrát, což není podporováno SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)

* NuGet. Indexing 5.6.0 Preview 3 a novější používá jiný token veřejného klíče – [#9481](https://github.com/NuGet/Home/issues/9481)

* Dodržovat TreatWarningsAsErrors během vytváření balíčku NuGet – [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Balíček Spurious downgrade pro více projektů P2P – [#9549](https://github.com/NuGet/Home/issues/9549)

* Karta procházet není zarovnaná doleva se vyhledávacím polem – [#9559](https://github.com/NuGet/Home/issues/9559)

* Nainstalovaná verze je nekonzistentní s ikonou Embedded v uživatelském rozhraní úrovně řešení PM pro jedno ID balíčku s nainstalovaným více verzemi – [#9321](https://github.com/NuGet/Home/issues/9321)

* Nevracení: Partcreationpolicy platná (výčtu CreationPolicy. nesdílené) NuGet. SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* Vyhněte se čtení souboru assetů při obnovení no-op – [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet. Protocol nepodporuje získání počtu stažení verze ze služby Search- [#9086](https://github.com/NuGet/Home/issues/9086)

* Zvyšte výkon paměti pro PackageMetadataResourceV3 snížením závislostí JObject – [#9719](https://github.com/NuGet/Home/issues/9719)

**Žádosti o změnu návrhu:**

* Potlačení `<owners>` prvku, když je redundantní – [#5134](https://github.com/NuGet/Home/issues/5134)

* Protokolovat IntervalTrackers jako události ETW – [#9593](https://github.com/NuGet/Home/issues/9593)

* Do obnovení se přidala informační zpráva, která informuje uživatele CPVM o tom, že funkce je ve verzi Preview – [#9340](https://github.com/NuGet/Home/issues/9340)

* Naplnit Průzkumník řešení přenosné závislosti balíčku/projektu ze souboru prostředků – [#9580](https://github.com/NuGet/Home/issues/9580)

* Karta nainstalované balíčky by neměla přestránkovat seznam balíčků – [#6995](https://github.com/NuGet/Home/issues/6995)

**[Seznam všech problémů opravených v této verzi – 5,7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Komunitní příspěvky

Děkujeme všem přispěvatelům, kteří vám pomohl tuto verzi NuGet udělat.

|Kdo|PR|Problémy|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet. Protocol nepodporuje získání počtu stažení verze ze služby Search- [#9086](https://github.com/NuGet/Home/issues/9086) </br>Zprávy HttpRequestMessage se opakovaně používá několikrát, což není podporováno SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)|
|[Josepha Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Potlačení `<owners>` prvku, když je redundantní – [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet nemůže obnovit ze zdrojů HTTPS, které vyžadují klientské certifikáty – [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim budoucí kontrolu – [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe spec vygeneruje značku copyrightu s pevně zakódovaným textem Copyright yyyy místo `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (olivier-spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|Pokud není definovaná proměnná prostředí, zkuste v rámci příkazu dotnet CLI při spouštění modulů plug-in pro přihlašovací údaje vyzkoušet příkaz dotnet CLI v systémové cestě `DOTNET_HOST_PATH`  . - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Přidání `latest` Možnosti pro `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|
