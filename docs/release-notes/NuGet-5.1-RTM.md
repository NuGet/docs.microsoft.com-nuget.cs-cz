---
title: Poznámky k verzi NuGet 5,1 RTM
description: Poznámky k verzi pro NuGet 5,1, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780137"
---
# <a name="nuget-51-release-notes"></a>Zpráva k vydání verze NuGet 5,1

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v sadě .NET SDK|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core 

<sup>2</sup> . K dispozici jako volitelná instalace se sadou Visual Studio 2019 s úlohou .NET Core

## <a name="summary-whats-new-in-51"></a>Shrnutí: Novinky v 5,1

* Podpora pro přeskočení nabízených oznámení balíčku, pokud už existuje, aby bylo možné lepší integraci s pracovními postupy CI/CD – [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio teď nabízí pohodlný odkaz na stránku Galerie nuget.org balíčku – [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Podpora nových prostředků .NET Core 3,0, jako jsou například [cílené balíčky](https://github.com/dotnet/cli/issues/10006) a [sady runtime](https://github.com/dotnet/cli/issues/10007)
  * Sada NuGet Pack a podpora obnovení pro FrameworkReferences, aby bylo možné povolit cílení a běhové odkazy na balíčky – [#7342](https://github.com/NuGet/Home/issues/7342)
  * Podpora "stažení pouze" balíčku s PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * Vylučte za běhu a cílení balíčků z výsledků hledání & obnovení grafu pomocí PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Štěnic**

* Moduly plug-in: ztráty podrobností výjimky během vytváření modulu plug-in – [#8057](https://github.com/NuGet/Home/issues/8057)

* Rozsah PackageReference s výhradním dolním limitem nefunguje, pokud dolní hranice je k dispozici na jednom ze zdrojů. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Vylepšit zprávu IsPackableFalseError [#8021](https://github.com/NuGet/Home/issues/8021)

* Soubor zámku balíčků – při změně grafu projektu znovu vygeneruje soubor zámku – [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem Chyba: balíčky NuGet získávají Automatické odebrání – [#8017](https://github.com/NuGet/Home/issues/8017)

* Přidejte cíl pro vrácení FrameworkReference, který se podobá CollectPackageDownloads a CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* Mezipaměť HTTP: prostředek RepositoryResources není uložený v mezipaměti způsobem, který je ve verzi [#7997](https://github.com/NuGet/Home/issues/7997)

* Protokolování: výjimka zásobníky volání není hlášena s detailní podrobností – [#7955](https://github.com/NuGet/Home/issues/7955)

* Změňte všechny adresy URL dokumentů NuGet na použití HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)

* Vylepšit zprávu upozornění NU3024 – [#7933](https://github.com/NuGet/Home/issues/7933)

* Při odebrání packagereference zamknout soubor bez aktualizace – [#7930](https://github.com/NuGet/Home/issues/7930)

* Zlepšení zpracování případných chyb při ověřování licenseurl a licenčního prvku v nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)

* PM uživatelské rozhraní: klikněte pravým tlačítkem na záhlaví karty a kliknutím na Otevřít umístění souboru dojde k chybě – [#7913](https://github.com/NuGet/Home/issues/7913)

* Moduly plug-in: protokol, když se proces modulu plug-in ukončí – [#7907](https://github.com/NuGet/Home/issues/7907)

* Moduly plug-in: vysoká míra kolizí při protokolování hodnot DateTime – [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest. ReadFrom se nezdařil při každém nuspec s LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: Neočekávaná NU1004 při ProjectReference odkazuje na projekt s vlastním AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889)

* Lepší chybová zpráva, když spuštění modulu plug-in selhává s výjimkou [#7857](https://github.com/NuGet/Home/issues/7857)

* Při obnovení NoOp Vyhněte se tomu * .dgspec.jspři zápisu do adresáře obj – [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true nemůže generovat vlastnost při neshodě případu – [#7843](https://github.com/NuGet/Home/issues/7843)

* Nastavení: neplatný znak v cestě zdroje balíčku může selhat a [#7820](https://github.com/NuGet/Home/issues/7820)

* Pokud se soubor zámku odstraní, obnovení negeneruje soubor zámku na NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)

* Adresa URL licence a licence způsobily chybu čtení s metadaty [#7547](https://github.com/NuGet/Home/issues/7547)

* Neošetřené výjimky v V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe vrátí ukončovací kód nula pro neplatné argumenty – [#7178](https://github.com/NuGet/Home/issues/7178)

* Aktualizace chyb a varovných dokumentů pro vyjádření souvisejících scénářů podepisování – [#6498](https://github.com/NuGet/Home/issues/6498)

* Soubor prostředků by měl použít relativní cesty, aby bylo možné přesouvat projekty snadněji [#4582](https://github.com/NuGet/Home/issues/4582)

**Chcete odeslat obecnou**

* Moduly plug-in: povolení protokolování diagnostiky – [#7859](https://github.com/NuGet/Home/issues/7859)

* Nastavte Tizen 6 na NetStandard 2,1 – [#7773](https://github.com/NuGet/Home/issues/7773)

**[Seznam všech problémů opravených v této verzi – 5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
