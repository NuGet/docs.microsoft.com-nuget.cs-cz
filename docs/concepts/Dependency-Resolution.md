---
title: Řešení závislostí balíčku NuGet
description: Podrobnosti o procesu, jehož prostřednictvím jsou vyřešeny a nainstalovány závislosti balíčku NuGet v NuGet 2.x a NuGet 3.x+.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 4b95251e4b055523a9533b4125589b2650be932d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428826"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak NuGet řeší závislosti balíčků

Pokaždé, když balíček je nainstalován nebo přeinstalovat, který zahrnuje instalaci jako součást procesu [obnovení,](../consume-packages/package-restore.md) NuGet také nainstaluje všechny další balíčky, na kterých závisí tento první balíček.

Tyto okamžité závislosti pak mohou mít také závislosti na vlastní, které mohou pokračovat do libovolné hloubky. To vytváří to, co se nazývá *graf závislostí,* který popisuje vztahy mezi balíčky na všech úrovních.

Pokud více balíčků mají stejnou závislost, pak stejné ID balíčku se může zobrazit v grafu vícekrát, potenciálně s různými omezeními verze. Však pouze jednu verzi daného balíčku lze použít v projektu, takže NuGet musí zvolit, která verze se používá. Přesný proces závisí na formátu správy balíčků, který se používá.

## <a name="dependency-resolution-with-packagereference"></a>Rozlišení závislostí s odkazem na balíček

Při instalaci balíčků do projektů pomocí formátu PackageReference, NuGet přidá odkazy na plochý balíček grafu v příslušném souboru a řeší konflikty předem. Tento proces se označuje jako *přenosné obnovení*. Přeinstalace nebo obnovení balíčků je pak proces stahování balíčků uvedených v grafu, což má za následek rychlejší a předvídatelnější sestavení. Můžete také využít plovoucí verze, například 2.8. \*, aby nedošlo k úpravám projektu tak, aby používal nejnovější verzi balíčku.

Při spuštění procesu obnovení NuGet před sestavením vyřeší závislosti nejprve v paměti a poté `project.assets.json`zapíše výsledný graf do souboru s názvem . Také zapíše vyřešené závislosti do `packages.lock.json`souboru zámku s názvem , pokud [je povolena funkce souboru zámku](../consume-packages/package-references-in-project-files.md#locking-dependencies).
Soubor datových zdrojů `MSBuildProjectExtensionsPath`je umístěn na adrese , která je výchozí pro složku obj projektu. MSBuild pak přečte tento soubor a převede jej do sady složek, kde lze nalézt potenciální odkazy a přidá je do stromu projektu v paměti.

Soubor `project.assets.json` je dočasný a neměl by být přidán do správy zdrojového kódu. Je uveden ve výchozím `.gitignore` nastavení `.tfignore`v obou a . Viz [Balíčky a smělá směšení zdrojů](../consume-packages/packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Pravidla řešení závislostí

Přenosné obnovení použije čtyři hlavní pravidla k vyřešení závislostí: nejnižší použitelná verze, plovoucí verze, nejbližší wins a cousin závislosti.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Nejnižší použitelná verze

Nejnižší platné pravidlo verze obnoví nejnižší možnou verzi balíčku, jak je definováno jeho závislostmi. Platí také pro závislosti na aplikaci nebo knihovně tříd, pokud není deklarována jako [plovoucí](#floating-versions).

Na následujícím obrázku je například 1.0-beta považován za nižší než 1.0, takže NuGet zvolí verzi 1.0:

![Výběr nejnižší použitelné verze](media/projectJson-dependency-1.png)

Na následujícím obrázku verze 2.1 není k dispozici v informačním kanálu, ale protože omezení verze je >= 2.1 NuGet vybere další nejnižší verzi, kterou může najít, v tomto případě 2.2:

![Výběr další nejnižší verze dostupné v informačním kanálu](media/projectJson-dependency-2.png)

Pokud aplikace určuje přesné číslo verze, například 1.2, která není k dispozici v informačním kanálu, NuGet selže s chybou při pokusu o instalaci nebo obnovení balíčku:

![NuGet generuje chybu, když není k dispozici přesná verze balíčku](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a>Plovoucí verze

Plovoucí verze závislosti je určena \* se znakem. Například, `6.0.*`. Tato specifikace verze říká" použijte nejnovější verzi 6.0.x"; `4.*` znamená "použijte nejnovější verzi 4.x". Použití plovoucí verze snižuje změny v souboru projektu při zachování aktuální s nejnovější verzí závislosti.

Při použití plovoucí verze NuGet řeší nejvyšší verzi balíčku, který odpovídá `6.0.*` vzor verze, například získá nejvyšší verzi balíčku, který začíná 6.0:

![Výběr verze 6.0.1 při požadavku na plovoucí verzi 6.0.*](media/projectJson-dependency-4.png)

> [!Note]
> Informace o chování plovoucích verzí a předběžných verzí naleznete v [tématu Package versioning](package-versioning.md#version-ranges).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Nejbližší vyhrává

Když graf balíčku pro aplikaci obsahuje různé verze stejného balíčku, NuGet vybere balíček, který je nejblíže k aplikaci v grafu a ignoruje všechny ostatní. Toto chování umožňuje aplikaci přepsat jakoukoli konkrétní verzi balíčku v grafu závislostí.

V níže uvedeném příkladu aplikace závisí přímo na balíčku B s omezením verze >=2.0. Aplikace také závisí na balíčku A, který zase závisí také na balíčku B, ale s >= 1.0 omezení. Vzhledem k tomu, že závislost na balíčku B 2.0 je blíže k aplikaci v grafu, tato verze se používá:

![Aplikace používající pravidlo Nejbližší výhry](media/projectJson-dependency-5.png)

>[!Warning]
> Pravidlo nejbližší výhry může mít za následek downgrade verze balíčku, tedy potenciálně porušení jiných závislostí v grafu. Proto toto pravidlo se používá s upozorněním upozornit uživatele.

Toto pravidlo také vede k větší účinnosti s grafem velké závislosti (například s balíčky BCL), protože jakmile je daná závislost ignorována, NuGet také ignoruje všechny zbývající závislosti na této větvi grafu. V níže uvedeném diagramu, například protože balíček C 2.0 se používá, NuGet ignoruje všechny větve v grafu, které odkazují na starší verzi balíčku C:

![Když NuGet ignoruje balíček v grafu, ignoruje celou větev](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Bratrancovy závislosti

Pokud jsou různé verze balíčku označovány ve stejné vzdálenosti v grafu z aplikace, NuGet používá nejnižší verzi, která splňuje všechny požadavky na verzi (jako s [nejnižší použitelnou verzi](#lowest-applicable-version) a [plovoucí verze](#floating-versions) pravidla). Na obrázku níže například verze 2.0 balíčku B splňuje ostatní >= 1.0 omezení, a proto se používá:

![Řešení závislostí bratrance pomocí nižší verze, která splňuje všechna omezení](media/projectJson-dependency-7.png)

V některých případech není možné splnit všechny požadavky na verzi. Jak je znázorněno níže, pokud balíček A vyžaduje přesně balíček B 1.0 a balíček C vyžaduje balíček B >= 2.0, pak NuGet nelze vyřešit závislosti a dává chybu.

![Neřešitelné závislosti z důvodu požadavku na přesnou verzi](media/projectJson-dependency-8.png)

V těchto situacích příjemce nejvyšší úrovně (aplikace nebo balíček) by měl přidat vlastní přímou závislost na balíčku B tak, aby se použije pravidlo [nejbližší výhry.](#nearest-wins)

## <a name="dependency-resolution-with-packagesconfig"></a>Řešení závislostí pomocí souboru packages.config

V `packages.config`aplikaci jsou závislosti projektu `packages.config` zapsány jako plochý seznam. Všechny závislosti těchto balíčků jsou také zapsány ve stejném seznamu. Při instalaci balíčků, NuGet může `.csproj` také `app.config` `web.config`upravit soubor, , a další jednotlivé soubory.

S `packages.config`, NuGet pokusí vyřešit konflikty závislostí během instalace každého jednotlivého balíčku. To znamená, že pokud je balíček A nainstalován a závisí `packages.config` na balíčku B a balíček B je již uveden jako závislost na něčem jiném, NuGet porovnává požadované verze balíčku B a pokusí se najít verzi, která splňuje všechna omezení verze. Konkrétně NuGet vybere nižší *major.minor* verze, která splňuje závislosti.

Ve výchozím nastavení NuGet 2.8 hledá nejnižší verzi opravy (viz [NuGet 2.8 poznámky k verzi).](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) Toto nastavení můžete `DependencyVersion` ovládat `Nuget.Config` pomocí `-DependencyVersion` atributu v a přepínače na příkazovém řádku.  

Proces `packages.config` řešení závislostí se komplikuje pro větší grafy závislostí. Každá instalace nového balíčku vyžaduje průchod celého grafu a zvyšuje pravděpodobnost konfliktů verzí. Dojde-li ke konfliktu, instalace je zastavena, takže projekt v neurčitém stavu, zejména s možnými změnami samotného souboru projektu. To to není problém při použití jiných formátů správy balíčků.

## <a name="managing-dependency-assets"></a>Správa prostředků závislostí

Při použití formátu PackageReference můžete určit, které prostředky ze závislostí toku do projektu nejvyšší úrovně. Podrobnosti naleznete v [tématu PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Pokud projekt nejvyšší úrovně je sám balíček, máte také kontrolu `include` `exclude` nad tento tok pomocí `.nuspec` atributy a se závislostmi uvedenými v souboru. Viz [odkaz .nuspec - závislosti](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Kromě odkazů

Existují scénáře, ve kterých sestavení se stejným názvem může odkazovat více než jednou v projektu, produkovat chyby návrhu a sestavení. Zvažte projekt, který obsahuje `C.dll`vlastní verzi aplikace , `C.dll`a odkazuje na balíček C, který také obsahuje . Projekt zároveň závisí také na balíčku B, který závisí `C.dll`také na balíčku C a . V důsledku toho NuGet nelze `C.dll` určit, které chcete použít, ale nelze jednoduše odebrat závislost projektu na balíček C, protože balíček B také závisí na něm.

Chcete-li tento problém vyřešit, musíte přímo odkazovat na `C.dll` požadovaný (nebo použít jiný balíček, který odkazuje na ten správný) a pak přidat závislost na balíčku C, který vylučuje všechny jeho prostředky. To se provádí takto v závislosti na formátu správy balíčků v použití:

- [PackageReference](../consume-packages/package-references-in-project-files.md): `ExcludeAssets="All"` přidejte závislost:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: odeberte odkaz na `.csproj` Soubor PackageC tak, aby `C.dll` odkazoval pouze na verzi, kterou chcete.
    
## <a name="dependency-updates-during-package-install"></a>Aktualizace závislostí během instalace balíčku 

Pokud je již splněna verze závislosti, závislost není aktualizována během jiných instalací balíčku. Zvažte například balíček A, který závisí na balíčku B a určuje 1.0 pro číslo verze. Zdrojové úložiště obsahuje verze 1.0, 1.1 a 1.2 balíčku B. Pokud A je nainstalován v projektu, který již obsahuje Verzi B 1.0, pak B 1.0 zůstane v provozu, protože splňuje omezení verze. Pokud by však balíček A měl požadavky verze 1.1 nebo vyšší z B, pak by byl nainstalován B 1.2. 

## <a name="resolving-incompatible-package-errors"></a>Řešení nekompatibilních chyb balíčků

Během operace obnovení balíčku se může zobrazit chyba "Jeden nebo více balíčků není kompatibilní..." nebo že balíček "není kompatibilní" s cílovým rámcem projektu.

K této chybě dochází, když jeden nebo více balíčků odkazovaných v projektu neoznačují, že podporují cílový rámec projektu; to znamená, že balíček neobsahuje vhodnou `lib` dll ve své složce pro cílovou architekturu, která je kompatibilní s projektem. (Viz [Cílové rámce](../reference/target-frameworks.md) pro seznam.) 

Například pokud projekt `netstandard1.6` cíle a pokusíte se nainstalovat balíček, `lib\net20` který `\lib\net45` obsahuje knihovny DLL pouze a složky, pak se zobrazí zprávy, jako je následující pro balíček a případně jeho závislé položky:

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

Chcete-li vyřešit nekompatibility, proveďte jeden z následujících akcí:

- Přesměrujte projekt na rámec, který je podporován balíčky, které chcete použít.
- Obraťte se na autora balíčků a spolupracujte s nimi a přidejte podporu pro zvolený rámec. Každá stránka s výpisem balíčku na [nuget.org](https://www.nuget.org/) má pro tento účel odkaz **Na vlastnísloži kontaktů.**
