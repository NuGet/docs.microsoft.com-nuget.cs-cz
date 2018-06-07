---
title: Referenční upozornění a chyby NuGet
description: Úplný referenční varování a chyby vystavené NuGet během různé operace NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 368a9554c5caf92b709f9b29e16b8a7cdb264eec
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818513"
---
# <a name="errors-and-warnings"></a>Chyby a upozornění

V NuGet 4.3.0+ chyby a upozornění jsou číslované, jak je popsáno v tomto tématu a poskytují podrobné informace můžete vyřešit problémy související se situací.

S chybami a upozorněními tady jsou k dispozici jenom s [na základě PackageReference](../consume-packages/package-references-in-project-files.md) projekty a NuGet 4.3.0+. NuGet rovněž ctí vlastnosti nástroje MSBuild potlačení upozornění nebo zvýšit jejich chyby. Další informace najdete v tématu [postupy: potlačení upozornění kompilátoru](/visualstudio/ide/how-to-suppress-compiler-warnings) v dokumentaci sady Visual Studio.

**Chyby**

| Skupina | Chyba čísla |
| --- | --- |
| [Neplatné vstupní chyby](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Chybějící chyby balíčku a projektu](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (dříve NU1607), [NU1108](#nu1108) (dříve NU1606) |
| [Chyby kompatibility](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**Upozornění**

| Skupina | Čísla upozornění |
| --- | --- |
| [Neplatné vstupní upozornění](#invalid-input-warnings) | [NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503) |
| [Upozornění verze neočekávané balíčku](#unexpected-package-version-warnings) | [NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605) |
| [Řešitel konfliktů upozornění](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [Balíček záložní upozornění](#package-fallback-warnings) | [NU1701](#nu1701) |
| [Informačního kanálu upozornění](#feed-warnings) | [NU1801](#nu1801) |
| [NuGet vnitřní chyby a upozornění](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |
| [Podepsaný balíčků (vytvoření a ověření)](#signed-packages-creation-and-verification)| [NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>Neplatné vstupní chyby

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problém** | Projekt neobsahuje jeden nebo více rozhraní. |
| **Příklad zprávy** | *Projekt projA neurčuje žádné cílové rozhraní v c:\tmp\projA.csproj* |
| **Řešení** | Přidat `TargetFramework` nebo `TargetFrameworks` vlastnost k souboru zadaného projektu. |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problém** | Neplatná kombinace vstupy společně s ZRUŠTE – klíčové slovo. |
| **Příklad zprávy** | *'CLEAR' nelze použít ve spojení s další hodnoty* |
| **Řešení** | Použít ZRUŠTE sám o sobě a vynechat možnost všechny ostatní vstupy. |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problém** | `PackageTargetFallback` a `AssetTargetFallback` poskytovat různé chování pro výběr prostředky a nelze použít společně. |
| **Příklad zprávy** | *PackageTargetFallback a AssetTargetFallback nelze použít společně. Odeberte PackageTargetFallback(deprecated) odkazy z prostředí projektu.* |
| **Řešení** | Odeberte nepoužívané `PackageTargetFallback` element z projektu. |

## <a name="missing-package-and-project-errors"></a>Chybějící chyby balíčku a projektu

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problém** | Skupina závislosti není možné přeložit. Toto je obecná problém pro typy, které nejsou balíčky nebo projekty. |
| **Příklad zprávy** | *Nelze přeložit System.Missing pro net45* |
| **Řešení** | Otevřete soubor projektu a zkontrolujte seznam jeho závislé součásti. Zkontrolujte, zda má každá závislost na zdroje balíčku, kterou používáte, a zda balíček podporuje cílový framework projektu na. |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problém** | Balíček nebyl nalezen na žádné zdroje. |
| **Příklad zprávy** | *Nepodařilo se najít balíček System.Missing. Neexistují žádné balíčky s tímto id v zdrojích: dotnet-core, dotnet roslyn, nuget.org* |
| **Řešení** | Zkontrolujte závislosti projektu v sadě Visual Studio a zajistit tak, že používáte správný balíček identifikátor a verzi číslo. Také zkontrolujte, zda [NuGet konfigurace](../consume-packages/Configuring-NuGet-Behavior.md) identifikuje zdroje balíčku vaší očekávají, že používat. Pokud používáte balíčky, které mají [sémantické verze 2.0.0](../reference/package-versioning.md#semantic-versioning-200), ujistěte se, že používáte V3 kanálu, `https://api.nuget.org/v3/index.json`v [NuGet konfigurace](../consume-packages/Configuring-NuGet-Behavior.md). |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problém** | Identifikátor balíčku se nenašel, ale nenašla se verze v rozsahu zadaná závislost na některý ze zdrojů. Rozsah může být určena balíček a nikoli uživatele. |
| **Příklad zprávy** | *Nejde najít balíček NuGet.Versioning s verzí (> = 9.0.1)<br/> -30 nalezena verze v nuget.org [nejbližší verze: 4.0.0]<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -nalezen 9 verze v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032]<br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.* |
| **Řešení** | Upravte soubor projektu a opravte verze balíčku. Také zkontrolujte, zda [NuGet konfigurace](../consume-packages/Configuring-NuGet-Behavior.md) identifikuje zdroje balíčku vaší očekávají, že používat. Potřebujete verzi requeted změnit, pokud tento balíček je odkazován objektem projektu přímo. |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problém** | Projektu zadána stabilní verze pro rozsah závislostí, ale v tomto rozsahu nebyly nalezeny žádné stabilní verze. Nebyly nalezeny předběžných verzí, ale nejsou povoleny. |
| **Příklad zprávy** | *Nelze najít stabilní balíček NuGet.Versioning s verzí (> = 3.0.0)<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -verze 9 najít v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032] <br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.* |
| **Řešení** |  Upravte rozsah verze v souboru projektu zahrnout předběžné verze. V tématu [Správa verzí balíčku](../reference/Package-Versioning.md). |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problém** | ProjectReference odkazuje na soubor, který neexistuje. |
| **Příklad zprávy** | *Odkaz na projekt neexistuje 'c:\a.csproj'. Zkontrolujte, že je odkaz na projekt platný a zda existuje soubor projektu.* |
| **Řešení** | Upravte soubor projektu buď opravte cestu k odkazované projektu nebo odebrat odkaz na úplně, pokud je již nepotřebujete. |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problém** | Soubor projektu existuje, ale pro něj k dispozici žádné informace pro obnovení. |
| **Příklad zprávy** | *Nelze číst informace o projektu pro 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.* |
| **Řešení** | V sadě Visual Studio chyba může znamenat, že projekt odpojen, v takovém případě projekt znovu načíst. Z příkazového řádku, to může znamenat, že soubor je poškozený nebo že neobsahuje vlastní "po importy" target potřebná pro obnovení k načtení projektu. Zkontrolujte, zda soubor projektu je platný a obsahuje cílový "po importy". |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problém** | Omezení závislostí nelze přeložit. |
| **Příklad zprávy** | *Nelze vyhovět konfliktním žádostem pro {id}: {cesta konflikt} Framework: {cíl grafu}* |
| **Řešení** | Upravte soubor projektu k určení širší rozsahy závislost, nikoli přesnou verzi. |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (dříve NU1607)

| | |
| --- | --- |
| **Problém** | Nelze vyřešit omezení závislost mezi balíčky. |
| **Příklad zprávy** | *Pro NuGet.Versioning zjištěn konflikt verzí. Odkazují na balíček přímo z projektu k vyřešení tohoto problému.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |
| **Řešení** | Balíčky s omezeními závislosti na přesné verze neumožňují dalších balíčků v případě potřeby zvýšit verze. Přidáte odkaz na balíček přímo (v souboru projektu) s přesnou verzi vyžaduje. |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (dříve NU1606)

| | |
| --- | --- |
| **Problém** | Byla rozpoznána cyklická závislost. |
| **Příklad zprávy** | *Byl zjištěn cyklus: A -> B -> A* |
| **Řešení** | Balíček je vytvořené nesprávně; Obraťte se na vlastníka balíčku a opravte chyb. |

## <a name="compatibility-errors"></a>Chyby kompatibility

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problém** | Závislosti projektu neobsahuje rozhraní kompatibilní s aktuálním projektu. Obvykle je cílový framework projektu na vyšší verzi než náročné projekt. |
| **Příklad zprávy** | *ServerWeb projektu není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Projekt podporuje ServerWeb:<br/> -netstandard1.6 (. Monikerů NETStandard, verze = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, verze = verze 1.0)* |
| **Řešení** | Změňte cílový framework projektu na stejné nebo nižší verzi než náročné projektu. |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problém** | Závislost balíček neobsahuje žádné prostředky, které jsou kompatibilní s projektu. |
| **Příklad zprávy** | *Balíček System.ComponentModel.EventBasedAsync 4.0.11 není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Balíček podporuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, verze = verze 1.0)<br/> -monotouch10 (MonoTouch, verze = verze 1.0)<br/> -net45 (. NETFramework, verze = v4.5)<br/> -netcore50 (. NETCore, verze = v5.0)<br/> -netstandard1.0 (. Monikerů NETStandard, verze = verze 1.0)<br/> -přenositelností net45 + win8 + wp8 + wpa81 (. NETPortable, verze = v0.0, profil = Profile259)<br/> -win8 (Windows, verze = v8.0)<br/> -wp8 (WindowsPhone, verze = v8.0)<br/> -wpa81 (WindowsPhoneApp, verze = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **Řešení** | Změňte cílový framework projektu na na takový, který podporuje balíčku. |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problém** | Balíček nepodporuje projektu `RuntimeIdentifier`. |
| **Příklad zprávy** | *System.Example 1.0.0 poskytuje kompilaci referenční sestavení pro a.dll na net461, ale neexistuje žádné kompatibilní sestavení za běhu.* |
| **Řešení** | Změna `RuntimeIdentifier` hodnoty používané v projektu podle potřeby. |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problém** | Balíček vyžaduje funkce nebo rozhraní není aktuálně podporovaná nainstalovaná verze balíčku NuGet. |
| **Příklad zprávy** | *Balíček 'NuGet.Versioning' vyžaduje NuGet verze klienta, 5.0.0' nebo vyšší, ale aktuální verze NuGet je '4.3.0'.* |
| **Řešení** | Nainstalujte novější verzi systému NuGet. V tématu [NuGet instalaci klienta nástroje](../install-nuget-client-tools.md). |

## <a name="invalid-input-warnings"></a>Neplatné vstupní upozornění

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problém** | Obnovení projektu se pokouší pracovat na nebyl nalezen. |
| **Příklad zprávy** | *Složka 'c:\projects\a' neobsahuje projekt k obnovení.* |
| **Řešení** | Spusťte obnovení nuget ve složce, která obsahuje projektu. |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problém** | `RuntimeSupports` obsahuje neplatný profil. Obvykle se podporuje profil nebyl nalezen v `runtime.json` souboru z aktuální závislostí balíčků.|
| **Příklad zprávy** | *Neznámý kompatibility profilu: aaa* |
| **Řešení** | Zkontrolujte `RuntimeSupports` hodnotu ve vašem projektu. |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problém** | Závislosti projektu neimportuje cíle obnovení NuGet. To se podobá NU1105 ale zde bude přeskočena projektu a ignorovat místo způsobuje všechny obnovení nezdaří. Komplexní řešení často existují jiné typy projektů, které nemusí podporovat obnovení. |
| **Příklad zprávy** | *Přeskočení obnovení pro projekt 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.* |
| **Řešení** | Toto může nastat projekty, které neimportujte běžné props nebo cíle, které automaticky importovat obnovení. Pokud projekt není potřeba obnovit to můžete ignorovat. Upravte, jinak hodnota ovlivněných projektu pro přidání cíle pro obnovení. |

## <a name="unexpected-package-version-warnings"></a>Upozornění verze neočekávané balíčku

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problém** | Přímé projektu závislost byla bumped na vyšší verzi než zadaný projekt. |
| **Příklad zprávy** | *Zadaná závislost byla NuGet.Versioning (> = 3.5.0), ale skončila s NuGet.Versioning 4.0.0.* |
| **Řešení** | Aktualizujte závislostí v projektu na příslušnou verzi. |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problém** | Závislost balíčku chybí dolní mez. To neumožňuje obnovení najít *nejlepší shodu*. Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít. To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele. |
| **Příklad zprávy** | *NuGet.Packaging 4.0.0 neposkytuje (včetně). dolní mez pro závislosti NuGet.Versioning (> 3.5.0). Přibližná nejlepší shody třídy 3.6.0 byl vyřešen.* |
| **Řešení** | Je to obvykle balíček pro tvorbu chyby. Požádejte autora balíčku k vyřešení problému. |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problém** | Zadaná závislost balíčku na verzi, která nebyla nalezena. Obvykle zdroje balíčku neobsahuje očekávaný dolní hranice verze. Vyšší verzi byl použit místo toho, který se liší od co balíček vytvořený proti.<br/><br/>To znamená, že obnovení nebyl nalezen *nejlepší shodu*. Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít. To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele. |
| **Příklad zprávy** | NuGet.Packaging 4.0.0 závisí na NuGet.Versioning (> = 4.0.0), ale 4.0.0 nebyl nalezen. Přibližná nejlepší shody třídy 5.0.0 byl vyřešen. |
| **Řešení** | Pokud balíček očekává ještě neuvolnil to může být balíček pro tvorbu chyby. Požádejte autora balíčku k vyřešení problému. Pokud byla vydána balíčku, potom zkontrolujte, zda je k dispozici na zdroje balíčku, kterou používáte. Pokud používáte privátní zdroje, musíte aktualizovat balíček na který informačního kanálu. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problém** | Závislosti projektu nedefinuje dolní mez.<br/><br/>To znamená, že obnovení nebyl nalezen *nejlepší shodu*. Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít. To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele. |
| **Příklad zprávy** | *Projektu závislosti NuGet.Versioning (< = 9.0.0) doe neobsahuje (včetně). dolní mez. Zahrňte dolní hranice verze závislosti zajistit obnovení konzistentní výsledky.* |
| **Řešení** | Aktualizace projektu `PackageReference` `Version` atribut zahrnout dolní mez. |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problém** | Balíček závislostí zadat omezení verze na vyšší verzi balíčku, než obnovení nakonec přeložit. To znamená z důvodu "nejbližší wins" pravidlo při rozpoznávání balíčky, blíž k uživateli balíčku v grafu může mít přepsat vzdáleným balíčku. |
| **Příklad zprávy** | *Zjištěna přechod na starší verzi balíčku: NuGet.Versioning z 4.0.0 k 3.5.0. Odkazují na balíček přímo z projektu a vyberte jinou verzi.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |
| **Řešení** | Přidejte přímý odkaz na projekt pro vyšší verzi balíčku, který chcete použít. |

## <a name="resolver-conflict-warnings"></a>Řešitel konfliktů upozornění

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problém** | Vyřešený balíček je vyšší, než povoluje omezení závislostí. To znamená, že balíček odkazuje na projekt přepsání omezení závislost z jiných balíčků.|
| **Příklad zprávy** | *Verze balíčku zjištěné mimo omezení závislost: x 1.0.0 vyžaduje y (= 1.0.0), ale verze y 2.0.0 byl vyřešen.* |
| **Řešení** | V některých případech to je úmyslné a lze potlačit upozornění. Změňte, jinak hodnota projektu odkaz na balíček, který chcete rozšířit jeho omezení verze. |

## <a name="package-fallback-warnings"></a>Balíček záložní upozornění

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problém** | `PackageTargetFallback` / `AssetTargetFallback` byl použit k výběru prostředky z balíčku. Upozornění uživatelům vědět, že prostředky nemusí být 100 % kompatibilní. |
| **Příklad zprávy** | *Balíček NuGet.Versioning se obnovil pomocí 'přenositelností net45 + win8' místo toho cílový framework projektu 'netstandard1.5'. Tento balíček nemusí být plně kompatibilní s projektem.* |
| **Řešení** | Změňte cílový framework projektu na na takový, který podporuje balíčku. |

## <a name="feed-warnings"></a>Informačního kanálu upozornění

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problém** | Při načítání informačního kanálu došlo k chybě při `IgnoreFailedSources` je nastaven na hodnotu true, převádí ji nezávažné upozornění. To může obsahovat jakékoli zprávy a je obecná. |
| **Příklad zprávy** | není k dispozici |
| **Řešení** | Upravte konfiguraci zadat platné zdroje. |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet vnitřní chyby a upozornění

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problém** | Bez konkrétní vnitřní chyba z NuGet. |
| **Řešení** | Zkontrolujte protokoly pro další informace |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problém** | Bez konkrétní interní upozornění z NuGet. |
| **Řešení** | Zkontrolujte protokoly pro další informace |

## <a name="signed-packages-creation-and-verification"></a>Podepsaný balíčků (vytvoření a ověření)

*NuGet 4.6.0+*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **Problém** | Není dost konkrétní chyby související s podepisování balíčku a podepsaný balíček ověření. |
| **Řešení** | Zkontrolujte protokoly pro další informace. |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **Problém** | Neplatné argumenty buď [přihlásit příkaz](../tools/cli-ref-sign.md) nebo [ověřte příkaz](../tools/cli-ref-verify.md). |
| **Řešení** | Zkontrolujte a opravte zadaných argumentů. |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **Problém** | `-Timestamper` s nebyla zadána možnost [příkaz přihlašovací nuget](../tools/cli-ref-sign.md). |
| **Příklad zprávy** | *'-Timestamper' nebyla zadána možnost. Podepsaného balíčku nebudou označen časovým razítkem.* |
| **Řešení** | Zadejte `-Timestamper` možnost s `nuget sign`. |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **Problém** | Balíček nepodepsané zadaná k [nuget ověřte příkaz](../tools/cli-ref-verify.md). |
| **Řešení** | Spustit `nuget verify` s podepsaného balíčku. V tématu [přihlásit balíček](../create-packages/Sign-a-Package.md). |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **Problém** | Zkontrolujte integritu balíčku se nezdařila, což znamená, že byla od Podepisovaný manipulováno podepsaného balíčku. |
| **Řešení** | Zkontrolujte počítač pomocí antivirového softwaru. Daný balíček odebrat z počítače, znovu ji nainstalujte a operaci opakujte. Pokud potíže potrvají, obraťte se na vlastníka zdrojových souborů balíčku a balíček vlastníka. |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **Problém** | Vytváření řetězu certifikátů se nezdařilo pro primární podpis. Primární podpisový certifikát není důvěryhodný, odvolán, nebo není k dispozici informace o odvolání certifikátu. |
| **Příklad zprávy** | *Upozornění: NU3018: Funkce zrušení se nepodařilo ověření odvolání certifikátu.* |
| **Řešení** | Používejte důvěryhodné a platný certifikát. Zkontrolujte připojení k Internetu. |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **Problém** | Vytváření řetězu certifikátů se nezdařilo pro podpis časové razítko. Časové razítko podpisový certifikát není důvěryhodný, odvolán, nebo není k dispozici informace o odvolání certifikátu. |
| **Příklad zprávy** | *Upozornění: NU3028: Funkce zrušení se nepodařilo ověření odvolání certifikátu.* |
| **Řešení** | Používejte důvěryhodné a platný certifikát. Zkontrolujte připojení k Internetu. |
