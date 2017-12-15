---
title: "NuGet Restore chyby a upozornění odkaz | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Úplný referenční varování a chyby, které jsou vydány při obnovování balíčků NuGet"
keywords: "NuGet chyby, upozornění NuGet diagnostiky"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3423e30eae07ff0c70a010576b8e701be027b847
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="errors-and-warnings"></a>Chyby a upozornění

V NuGet 4.3.0 chyby a upozornění jsou číslované, jak je popsáno v tomto tématu a poskytují podrobné informace můžete vyřešit problémy související se situací. 

S chybami a upozorněními tady jsou k dispozici jenom s [na základě PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) projekty a NuGet 4.3.0. NuGet rovněž ctí vlastnosti nástroje MSBuild potlačení upozornění nebo zvýšit jejich chyby. Další informace najdete v tématu [postupy: potlačení upozornění kompilátoru](https://docs.microsoft.com/visualstudio/ide/how-to-suppress-compiler-warnings) v dokumentaci sady Visual Studio.

**Chyby**

| Skupina | Chyba čísla |
| --- | --- |
| [Neplatné vstupní chyby](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Chybějící chyby balíčku a projektu](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (dříve NU1607), [NU1108](#nu1107) (dříve NU1606) |
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

## <a name="invalid-input-errors"></a>Neplatné vstupní chyby

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problém** | Projekt neobsahuje jeden nebo více rozhraní. |
| **Běžné příčiny** | Neobsahuje projekt `TargetFramework` nebo `TargetFrameworks` vlastnost. |
| **Příklad zprávy** | *Projekt projA neurčuje žádné cílové rozhraní v c:\tmp\projA.csproj* |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problém** | Neplatná kombinace vstupy společně s ZRUŠTE – klíčové slovo. |
| **Běžné příčiny** | CLEAR nelze kombinovat s ostatní vstupy. |
| **Příklad zprávy** | *'CLEAR' nelze použít ve spojení s další hodnoty* |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problém** | `PackageTargetFallback`a `AssetTargetFallback` poskytovat různé chování pro výběr prostředky a nelze použít společně. |
| **Běžné příčiny** | Obě `PackageTargetFallback` a `AssetTargetFallback` existovat v projektu. |
| **Příklad zprávy** | *PackageTargetFallback a AssetTargetFallback nelze použít společně. Odeberte PackageTargetFallback(deprecated) odkazy z prostředí projektu.* |

## <a name="missing-package-and-project-errors"></a>Chybějící chyby balíčku a projektu

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problém** | Skupina závislosti není možné přeložit. Toto je obecná problém pro typy, které nejsou balíčky nebo projekty. |
| **Běžné příčiny** | Projekt obsahuje závislost na položku, která neexistuje. |
| **Příklad zprávy** | *Nelze přeložit System.Missing pro net45* |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problém** | Balíček nebyl nalezen na žádné zdroje. |
| **Běžné příčiny** | Chybí zdroj správný balíček nebo identifikátor balíčku je nesprávný. |
| **Příklad zprávy** | *Nepodařilo se najít balíček System.Missing. Neexistují žádné balíčky s tímto id v zdrojích: dotnet-core, dotnet roslyn, nuget.org* |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problém** | Identifikátor balíčku se nenašel, ale nenašla se verze v rozsahu zadaná závislost na některý ze zdrojů. |
| **Běžné příčiny** | Chybí zdroj správný balíček nebo rozsah závislostí je nesprávný. Rozsah může být určena balíček a nikoli uživatele. Uživatel možná muset přejít k dispozici verze, pokud tento balíček je odkazován objektem projektu přímo. |
| **Příklad zprávy** | *Nejde najít balíček NuGet.Versioning s verzí (> = 9.0.1)<br/> -30 nalezena verze v nuget.org [nejbližší verze: 4.0.0]<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -nalezen 9 verze v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032]<br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.* |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problém** | V rozsahu závislostí nebyly nalezeny žádné stabilní verze. Nebyly nalezeny předběžných verzí, ale nejsou povoleny. |
| **Běžné příčiny** | Projekt zadat stabilní verze pro rozsah závislostí. Uživatelé musí změnit rozsah verze zahrnout předběžné verze. |
| **Příklad zprávy** | *Nelze najít stabilní balíček NuGet.Versioning s verzí (> = 3.0.0)<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -verze 9 najít v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032] <br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.* |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problém** | ProjectReference odkazuje na soubor, který neexistuje. |
| **Běžné příčiny** | Soubor projektu chybí disk nebo odkaz je nesprávný. |
| **Příklad zprávy** | *Odkaz na projekt neexistuje 'c:\a.csproj'. Zkontrolujte, že je odkaz na projekt platný a zda existuje soubor projektu.* |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problém** | Soubor projektu existuje, ale pro něj k dispozici žádné informace pro obnovení. |
| **Běžné příčiny** | V sadě Visual Studio to může znamenat, že projekt je odpojen. Z příkazového řádku to může znamenat, že soubor je poškozený nebo že neobsahuje vlastní po importy cíl potřebná pro obnovení k načtení projektu. |
| **Příklad zprávy** | *Nelze číst informace o projektu pro 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.* |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problém** | Omezení závislostí nelze přeložit. |
| **Běžné příčiny** | Balíčky obsahovat závislosti na přesné verze balíčku místo zprostředkovává rozsahy. |
| **Příklad zprávy** | *Nelze vyhovět konfliktním žádostem pro {id}: {cesta konflikt} Framework: {cíl grafu}* |

< a name = "NU1107 ></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (dříve NU1607)

| | |
| --- | --- |
| **Problém** | Nelze vyřešit omezení závislost mezi balíčky. |
| **Běžné příčiny** | Balíčky s omezeními závislosti na přesné verze neumožňují dalších balíčků v případě potřeby zvýšit verze. |
| **Příklad zprávy** | *Pro NuGet.Versioning zjištěn konflikt verzí. Odkazují na balíček přímo z projektu k vyřešení tohoto problému.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |

< a name = "NU1108 ></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (dříve NU1606)

| | |
| --- | --- |
| **Problém** | Byla rozpoznána cyklická závislost. |
| **Běžné příčiny** | Balíček není správně vytvořeny. |
| **Příklad zprávy** | *Byl zjištěn cyklus: A -> B -> A* |

## <a name="compatibility-errors"></a>Chyby kompatibility

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problém** | Závislosti projektu neobsahuje rozhraní kompatibilní s aktuálním projektu. |
| **Běžné příčiny** | Cílový framework projektu na je vyšší verze než náročné projekt. |
| **Příklad zprávy** | *ServerWeb projektu není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Projekt podporuje ServerWeb:<br/> -netstandard1.6 (. Monikerů NETStandard, verze = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, verze = verze 1.0)* |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problém** | Závislost balíček neobsahuje žádné prostředky, které jsou kompatibilní s projektu. |
| **Běžné příčiny** | Balíček nepodporuje cílový framework projektu na. |
| **Příklad zprávy** | *Balíček System.ComponentModel.EventBasedAsync 4.0.11 není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Balíček podporuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, verze = verze 1.0)<br/> -monotouch10 (MonoTouch, verze = verze 1.0)<br/> -net45 (. NETFramework, verze = v4.5)<br/> -netcore50 (. NETCore, verze = v5.0)<br/> -netstandard1.0 (. Monikerů NETStandard, verze = verze 1.0)<br/> -přenositelností net45 + win8 + wp8 + wpa81 (. NETPortable, verze = v0.0, profil = Profile259)<br/> -win8 (Windows, verze = v8.0)<br/> -wp8 (WindowsPhone, verze = v8.0)<br/> -wpa81 (WindowsPhoneApp, verze = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problém** | Balíček nepodporuje projektu `RuntimeIdentifier`. |
| **Běžné příčiny** | Balíček nepodporuje aktuální `RuntimeIdentifier`. Změna `RuntimeIdentifier` hodnoty používané v projektu, v případě potřeby. |
| **Příklad zprávy** | *System.Example 1.0.0 poskytuje kompilaci referenční sestavení pro a.dll na net461, ale neexistuje žádné kompatibilní sestavení za běhu.* |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problém** | Balíček vyžaduje funkce nebo rozhraní není aktuálně podporovaná nainstalovaná verze balíčku NuGet. |
| **Běžné příčiny** | Upgradujte rozšíření NuGet vyřešit problém. |
| **Příklad zprávy** | *Balíček 'NuGet.Versioning' vyžaduje NuGet verze klienta, 5.0.0' nebo vyšší, ale aktuální verze NuGet je '4.3.0'. Pokud chcete upgradovat NuGet, přejděte na http://docs.nuget.org/consume/installing-nuget.* |

## <a name="invalid-input-warnings"></a>Neplatné vstupní upozornění

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problém** | Obnovení projektu se pokouší pracovat na nebyl nalezen. |
| **Běžné příčiny** | Projekt chybí. |
| **Příklad zprávy** | *Složka 'c:\projects\a' neobsahuje projekt k obnovení.* |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problém** | `RuntimeSupports`obsahuje neplatný profil. |
| **Běžné příčiny** | Podporuje profil nebyl nalezen v `runtime.json` souboru z aktuální závislostí balíčků. |
| **Příklad zprávy** | *Neznámý kompatibility profilu: aaa* |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problém** | Závislosti projektu neimportuje cíle obnovení NuGet. To se podobá NU1105 ale zde bude přeskočena projektu a ignorovat místo způsobuje všechny obnovení nezdaří. Komplexní řešení často existují jiné typy projektů, které nemusí podporovat obnovení. |
| **Běžné příčiny** | Toto může nastat projekty, které neimportujte běžné props nebo cíle, které automaticky importovat obnovení. Pokud projekt není potřeba obnovit to můžete ignorovat. |
| **Příklad zprávy** | *Přeskočení obnovení pro projekt 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.* |

## <a name="unexpected-package-version-warnings"></a>Upozornění verze neočekávané balíčku

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problém** | Přímé projektu závislost byla bumped na vyšší verzi než zadaný projekt. |
| **Běžné příčiny** | Jiný balíček závislostí vyžaduje vyšší verzi a bumped balíček. |
| **Příklad zprávy** | *Zadaná závislost byla NuGet.Versioning (> = 3.5.0), ale skončila s NuGet.Versioning 4.0.0.* |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problém** | Závislost balíčku chybí dolní mez. To neumožňuje obnovení najít *nejlepší shodu*. Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít. To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele. |
| **Běžné příčiny** | Je to obvykle balíček pro tvorbu chyby. |
| **Příklad zprávy** | *NuGet.Packaging 4.0.0 neposkytuje (včetně). dolní mez pro závislosti NuGet.Versioning (> 3.5.0). Přibližná nejlepší shody třídy 3.6.0 byl vyřešen.* |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problém** | Zadaná závislost balíčku na verzi, která nebyla nalezena. Vyšší verzi byl použit místo toho, který se liší od co balíček vytvořený proti.<br/><br/>To znamená, že obnovení nebyl nalezen *nejlepší shodu*. Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít. To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele. |
| **Běžné příčiny** | Zdroje balíčku neobsahuje očekávaný dolní hranice verze. Pokud balíček očekává ještě neuvolnil to může být balíček pro tvorbu chyby. |
| **Příklad zprávy** | NuGet.Packaging 4.0.0 závisí na NuGet.Versioning (> = 4.0.0), ale 4.0.0 nebyl nalezen. Přibližná nejlepší shody třídy 5.0.0 byl vyřešen. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problém** | Závislosti projektu nedefinuje dolní mez.<br/><br/>To znamená, že obnovení nebyl nalezen *nejlepší shodu*. Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít. To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele. |
| **Běžné příčiny** | Projektu *PackageReference* *verze* atributu se musí aktualizovat na zahrnují dolní mez. |
| **Příklad zprávy** | *Projektu závislosti NuGet.Versioning (< = 9.0.0) doe neobsahuje (včetně). dolní mez. Zahrňte dolní hranice verze závislosti zajistit obnovení konzistentní výsledky.* |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problém** | Balíček závislostí zadat omezení verze na vyšší verzi balíčku, než obnovení nakonec přeložit. |
| **Běžné příčiny** | Nejbližší wins při rozpoznávání balíčky. Balíček blíž k uživateli v grafu může přepsat vzdáleným balíčku. |
| **Příklad zprávy** | *Zjištěna přechod na starší verzi balíčku: NuGet.Versioning z 4.0.0 k 3.5.0. Odkazují na balíček přímo z projektu a vyberte jinou verzi.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |

## <a name="resolver-conflict-warnings"></a>Řešitel konfliktů upozornění

[NU1608](#nu1608)

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problém** | Vyřešte balíčku je vyšší, než umožňuje omezení závislostí. V některých případech to je úmyslné a lze potlačit upozornění. |
| **Běžné příčiny** | Balíček odkazuje na projekt se přepíše omezení závislost z jiných balíčků.   |
| **Příklad zprávy** | *Verze balíčku zjištěné mimo omezení závislost: x 1.0.0 vyžaduje y (= 1.0.0), ale verze y 2.0.0 byl vyřešen.* |

## <a name="package-fallback-warnings"></a>Balíček záložní upozornění

[NU1701](#nu1701)

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problém** | *PackageTargetFallback/AssetTargetFallback* byl použit k výběru prostředky z balíčku. Toto je upozornění, aby mohl uživatel vědět, že prostředky nemusí být 100 % kompatibilní. |
| **Běžné příčiny** | Balíček nepodporuje rozhraní projektu. |
| **Příklad zprávy** | *Balíček NuGet.Versioning se obnovil pomocí 'přenositelností net45 + win8' místo toho cílový framework projektu 'netstandard1.5'. Tento balíček nemusí být plně kompatibilní s projektem.* |

## <a name="feed-warnings"></a>Informačního kanálu upozornění

[NU1801](#nu1801)

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problém** | Při načítání informačního kanálu došlo k chybě při `IgnoreFailedSources` je nastaven na hodnotu true, převádí ji nezávažné upozornění. To může obsahovat jakékoli zprávy a je obecná. |
| **Běžné příčiny** | Zdroj je neplatný. |
| **Příklad zprávy** | není k dispozici |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet vnitřní chyby a upozornění

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problém** | Bez konkrétní vnitřní chyba z NuGet. |
| **Běžné příčiny** | Zkontrolujte protokoly pro další informace |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problém** | Bez konkrétní interní upozornění z NuGet. |
| **Běžné příčiny** | Zkontrolujte protokoly pro další informace |
