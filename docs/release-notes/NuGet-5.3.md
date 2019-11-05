---
title: Zpráva k vydání verze NuGet 5,3
description: Poznámky k verzi pro NuGet 5,3, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: e77219d355f73f3bf01f68283ffb2759813af563
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611328"
---
# <a name="nuget-53-release-notes"></a>Zpráva k vydání verze NuGet 5,3

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v sadě .NET SDK|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,3](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |
| [**5.3.1**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16.3.6](https://visualstudio.microsoft.com/downloads/) | [Budoucí verze: 3.0.101](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core

## <a name="summary-whats-new-in-53"></a>Shrnutí: Novinky v 5,3

* [Ikona balíčku se dá vložit do balíčku](../reference/msbuild-targets.md#packing-an-icon-image-file), takže nemusíte potřebovat externí adresu URL. - [#352](https://github.com/NuGet/Home/issues/352)

* Vylepšené zabezpečení pomocí SHA sledování a vynucení pro balíčky. config- [#7281](https://github.com/NuGet/Home/issues/7281)

* Povolit vyřazení zastaralých a starších balíčků NuGet [#2867](https://github.com/NuGet/Home/issues/2867) | [blogový příspěvek](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](https://docs.microsoft.com/nuget/nuget-org/deprecate-packages)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Štěnic**

* Balíčky NuGet vytvořené pomocí sady 3.0.100-preview9 SDK nemůžou používat uživatelé sady SDK 2,2... v závislosti na časovém pásmu [#8603](https://github.com/NuGet/Home/issues/8603)

* Uvozovky "znaky v cestě způsobují" nepovolené znaky v cestě "`nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)

* VS: sestavení jsou plně Ngen-Ed, ne částečně Ngen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)

* Snižte využití paměti (odhlášení odběru událostí) – [#8471](https://github.com/NuGet/Home/issues/8471)

* Zpráva "Error_UnableToFindProjectInfo" není gramaticky správná – [#8441](https://github.com/NuGet/Home/issues/8441)

* Vylepšení NU1403 – ověřte všechny balíčky, včetně očekávaných nebo skutečných hodnot SHA- [#8424](https://github.com/NuGet/Home/issues/8424)

* Více výčtu ve `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)

* Vrácení "> interní" změny v PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider. getsources (...) má nesprávně definované chování výjimky – [#8383](https://github.com/NuGet/Home/issues/8383)

* Vytvořte znovu PluginManager konstruktor – [#8379](https://github.com/NuGet/Home/issues/8379)

* Metriky pro sledování obnovovací frekvence uživatelského rozhraní PM – [#8369](https://github.com/NuGet/Home/issues/8369)

* Při instalaci prostřednictvím uživatelského rozhraní Správce balíčků snížit počet aktualizací uživatelského rozhraní [#8358](https://github.com/NuGet/Home/issues/8358)

* Telemetrie: hodnoty DateTime používají formáty specifické pro jazykovou verzi – [#8351](https://github.com/NuGet/Home/issues/8351)

* Omezení aktualizací uživatelského rozhraní na kartě Procházet uživatelského rozhraní Správce balíčků #6570- [#8339](https://github.com/NuGet/Home/issues/8339)

* [Selhání testu] "Nelze analyzovat konfigurační soubor", zobrazí se výzva dvakrát [#8320](https://github.com/NuGet/Home/issues/8320)

* Vyvolejte NU5037 chybu se správnou stránkou dokumentu, která vysvětluje opravy zákazníků (v balíčku chybí požadovaný soubor nuspec) – [#8291](https://github.com/NuGet/Home/issues/8291)

* V případě změny RuntimeIdentifier projektu se obnovení uzamčeného režimu nepovede – [#8260](https://github.com/NuGet/Home/issues/8260)

* Nastavit čtení nastavení v VS-opožděné [#8156](https://github.com/NuGet/Home/issues/8156)

* Regrese v `Nuget sources add` způsobí, že znak ":", šestnáctková hodnota 0x3A, nemůže být zahrnutá v názvu "Errors- [#7948](https://github.com/NuGet/Home/issues/7948)

* Zprostředkovatelé přihlašovacích údajů plug-in NuGet – skrýt okno procesu – [#7511](https://github.com/NuGet/Home/issues/7511)

* Vynutilí PackagePathResolver je absolutní cesta – [#7349](https://github.com/NuGet/Home/issues/7349)

* Omezení aktualizací uživatelského rozhraní na kartách instalace a aktualizace uživatelského rozhraní Správce balíčků – [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR**

* Aktualizace rozhraní Xamarin pro mapování na NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Povolit kopírování obsahu okna Preview správce balíčků pro Install/Update- [#8324](https://github.com/NuGet/Home/issues/8324)

* Povolit obnovení souborů. proj – [#8212](https://github.com/NuGet/Home/issues/8212)

* Zavedení `NUGET_NETFX_PLUGIN_PATHS` a `NUGET_NETCORE_PLUGIN_PATHS` pro podporu konfigurace současně [#8151](https://github.com/NuGet/Home/issues/8151)

* Povolit více verzí pro PackageDownload pomocí atributu Version- [#8074](https://github.com/NuGet/Home/issues/8074)

* Možnosti Add-SolutionDirectory a-PackageDirectory do NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)

**[Seznam všech problémů opravených v této verzi – 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**

## <a name="summary-whats-new-in-531"></a>Shrnutí: co je nového v 5.3.1.

* Modul plug-in: úloha byla zrušena. zrušení vlivu na vytvoření instance modulu plug-in [#8648](https://github.com/NuGet/Home/issues/8648)

* Úloha obnovení nemůže být bezpečně spuštěna dvakrát v jednom procesu (při použití zprostředkovatelů pověření) – [#8688](https://github.com/NuGet/Home/issues/8688)
