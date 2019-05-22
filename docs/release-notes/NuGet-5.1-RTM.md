---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975850"
---
# <a name="nuget-51-release-notes"></a>Poznámky k verzi 5.1 NuGet

Distribuce vozidel NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v rozhraní .NET SDK, pomocí kterých|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>nainstalované s Visual Studio 2019 se sadou .NET Core 

<sup>2</sup>dostupné jako volitelná instalace s Visual Studio 2019 se sadou .NET Core

## <a name="summary-whats-new-in-51"></a>Shrnutí: Co je nového v 5.1

* Podpora přeskočit balíček push, pokud již existuje umožňující lepší integrace s pracovními postupy CI/CD - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio teď umožňuje pohodlný odkaz stránku Galerie nuget.org balíčku - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Podpora pro nové materiály .NET Core 3.0 jako [Targeting Pack](https://github.com/dotnet/cli/issues/10006) a [balíčky Runtime](https://github.com/dotnet/cli/issues/10007)
  * Balíček NuGet a obnovení podporu FrameworkReferences povolit cílení na modul runtime a odkazy na balíčky - [#7342](https://github.com/NuGet/Home/issues/7342)
  * Podpora "stáhnout pouze" balíček scénářem PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)
  * Modul runtime Exlcude a targeting Pack z výsledky hledání & obnovení grafu pomocí PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chyby**

* Moduly plug-in: Podrobnosti o výjimce přijdete při vytváření modulu plug-in – [#8057](https://github.com/NuGet/Home/issues/8057)

* PackageReference rozsahu, s výhradním dolní mez nefunguje, pokud je dolní mez je k dispozici na jeden ze zdrojů. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Zlepšení IsPackableFalseError zpráva – [#8021](https://github.com/NuGet/Home/issues/8021)

* Zabalí zamknout soubor – soubor znovu vygenerovat zámku při změně projektu grafu – [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem chyb: Balíčky Nuget získávání automaticky odebrány - [#8017](https://github.com/NuGet/Home/issues/8017)

* Přidání cíle pro návrat FrameworkReference podobné CollectPackageDownloads a CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP mezipaměti:  Prostředek RepositoryResources neukládá do mezipaměti označené verzí způsobem – [#7997](https://github.com/NuGet/Home/issues/7997)

* Protokolování: zásobníky volání výjimky nejsou nahlásí se podrobné podrobností - [#7955](https://github.com/NuGet/Home/issues/7955)

* Změnit všechny adresy URL NuGet dokumentace pro použití protokolu HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)

* Zlepšení NU3024 upozornění - [#7933](https://github.com/NuGet/Home/issues/7933)

* soubor zámku není při aktualizaci packagereference odebrat - [#7930](https://github.com/NuGet/Home/issues/7930)

* Zlepšení zpracování případu chyb při ověřování elementu licenseurl a licence v souboru nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)

* Klikněte pravým tlačítkem na záhlaví karty a kliknutím na "Otevřít umístění souboru" výsledkem je chyba – uživatelské rozhraní odp. - [#7913](https://github.com/NuGet/Home/issues/7913)

* Moduly plug-in: přihlášení při ukončení procesu modulu plug-in – [#7907](https://github.com/NuGet/Home/issues/7907)

* Moduly plug-in: míra vysoké kolizí v hodnotách data a času protokolování - [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom selže na libovolný soubor nuspec s LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: Neočekávané NU1004 když ProjectReference odkazuje na projekt s vlastní AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)

* Lepší chybové zprávy při spuštění modulu plug-in selže s výjimkou - [#7857](https://github.com/NuGet/Home/issues/7857)

* Vyhněte se při obnovení NoOp, *. dgspec.json zápis v adresáři obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true nebude moci generovat vlastnost na velikosti písmen neshoda - [#7843](https://github.com/NuGet/Home/issues/7843)

* Nastavení: neplatný znak v cestě zdroje balíčku může dojít k selhání VS - [#7820](https://github.com/NuGet/Home/issues/7820)

* Pokud soubor zámku se odstraní, obnovení nelze vytvořit soubor zámku na NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)

* Adresa URL licence a licence způsobí, že čtení došlo k chybě s metadaty - [#7547](https://github.com/NuGet/Home/issues/7547)

* Neošetřené výjimky v V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe vrátí ukončovací kód nula při neplatných argumentech - [#7178](https://github.com/NuGet/Home/issues/7178)

* Aktualizovat chyby a upozornění dokumentace tak, aby odrážely podpisový související scénáře - [#6498](https://github.com/NuGet/Home/issues/6498)

* Soubor prostředků by měl používat relativní cesty k přesunutí projekty povolit snadněji - [#4582](https://github.com/NuGet/Home/issues/4582)

**Chcete**

* Moduly plug-in: povolení protokolování diagnostiky - [#7859](https://github.com/NuGet/Home/issues/7859)

* Zkontrolujte mapování Tizen 6 NetStandard 2.1 – [#7773](https://github.com/NuGet/Home/issues/7773)

**[Seznam všech problémů, které jsou opravené v této verzi - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
