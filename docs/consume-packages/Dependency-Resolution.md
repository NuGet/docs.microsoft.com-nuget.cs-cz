---
title: Řešení závislostí balíčku NuGet
description: Informace o procesu, pomocí kterého se závislosti balíčku NuGet přeložit a nainstalován v obou NuGet 2.x a NuGet 3.x+.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: a2aed3950b3e19e30d9d026ad1b9bdaef44c9d37
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247643"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak NuGet řeší závislosti balíčků

Vždy je balíček nainstalovat nebo přeinstalovat, který obsahuje, se instalují jako součást [obnovení](../consume-packages/package-restore.md) procesu NuGet nainstaluje taky všechny další balíčky, na kterých závisí první balíčku.

Tyto okamžité závislosti potom také může mít závislosti na své vlastní, které můžete dál do libovolné hloubky. Tímto se vytvoří, co se volá *graf závislosti* , který popisuje relace mezi balíčky na všech úrovních.

Když více balíčků mají stejné závislost, pak stejné ID balíčku mohou objevit v grafu více než jednou, potenciálně omezení jinou verzi. Však pouze jedna verze daného balíčku lze v projektu, takže NuGet musíte zvolit, která verze se používá. Přesný postup závisí na formát správy balíčků, který je používán.

## <a name="dependency-resolution-with-packagereference"></a>Řešení závislostí s PackageReference

Při instalaci balíčků do projektů s použitím formátu PackageReference, NuGet přidá odkazy na graf plochých balíčků v příslušný soubor a řeší konflikty předem. Tento proces se označuje jako *tranzitivní obnovení*. Přeinstalace nebo obnovování balíčků je pak proces stahování balíčky uvedené v grafu, výsledkem je rychlejší a předvídatelnější sestavení. Můžete taky využít výhod zástupný znak (s plovoucí desetinnou čárkou) verzí, jako například 2.8. \*, vyhnout náročné a náchylné k chybám volání chyba `nuget update` na klientských počítačích a serverech sestavení.

Když spustíte proces obnovení NuGet před sestavení, nejprve řeší závislosti v paměti a pak zapíše Výsledný graf do souboru s názvem `project.assets.json`. Soubor prostředků, který se nachází v `MSBuildProjectExtensionsPath`, která má výchozí hodnotu "obj" složky projektu. Nástroj MSBuild pak načte tento soubor a převede ho na sadu složek, kde najdete potenciální odkazy a přidá je do stromu projektu v paměti.

Soubor zámku je dočasný a neměl by se přidávat do správy zdrojového kódu. Je uvedený ve výchozím nastavení v obou `.gitignore` a `.tfignore`. Zobrazit [balíčky a Správa zdrojového kódu](packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Pravidla řešení závislostí

Přenositelné obnovení používá čtyři hlavní pravidla vyřešit závislosti: nejnižší použitelná verze, verze s plovoucí desetinnou čárkou, nejbližší wins a cousin závislosti.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Nejnižší použitelná verze

Nejnižší pravidlo použitelná verze obnoví nejnižší verzi balíčku dle jeho závislosti. To platí také pro závislosti na aplikaci nebo knihovny tříd Pokud nejsou deklarovány jako [s plovoucí desetinnou čárkou](#floating-versions).

Na následujícím obrázku třeba 1.0 beta se považuje za nižší než 1.0, NuGet zvolí verzi 1.0:

![Výběr nejnižší použitelná verze](media/projectJson-dependency-1.png)

Následující obrázek, není k dispozici na informační kanál verze 2.1, ale protože je omezení verze > = Další nejnižší verze můžete najít v tomto případě 2.2 2.1 NuGet položky:

![Výběr další nejnižší verze k dispozici na informační kanál](media/projectJson-dependency-2.png)

Když aplikace určuje přesné číslo verze protokolu, jako je například 1.2, který není k dispozici na informační kanál, NuGet se při pokusu o instalaci nebo obnovit balíček nezdaří s chybou:

![NuGet dojde k chybě, pokud není k dispozici ve verzi přesné balíčku](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Verze s plovoucí desetinnou čárkou (zástupný znak)

Číslo s plovoucí čárkou nebo zástupný znak verze závislosti není zadán s \* zástupných znaků, stejně jako u 6.0.\*. Tato specifikace verze říká "používat nejnovější verzi 6.0.x"; 4.\* znamená "pomocí nejnovější verze 4.x." Použití zástupného znaku umožňuje závislost balíčku pokračovat bez nutnosti provádění změn spotřebitelskou aplikací se vyvíjejí (nebo balíček).

Při použití zástupného znaku, NuGet řeší nejvyšší verzi balíčku, který odpovídá vzoru verze, třeba 6.0. \* získá nejvyšší verzi balíčku, který začíná 6.0:

![Výběr verze 6.0.1 při plovoucí verze 6.0. * je požadováno](media/projectJson-dependency-4.png)

> [!Note]
> Informace o chování zástupné znaky a předběžných verzí, naleznete v tématu [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Nejbližší wins

Když balíček grafu pro aplikaci obsahuje různé verze stejného balíčku, NuGet vybere balíček, který je nejblíž k aplikaci v grafu a ignoruje všechny ostatní. Toto chování umožňuje aplikaci pro přepsání jakékoli verze konkrétního balíčku v grafu závislostí.

V následujícím příkladu je aplikace závislá přímo B balíček s omezení verze > = 2.0. Aplikace také závisí na balíčku A které pak také závisí na balíčku B, ale s > = 1.0 omezení. Závislost na balíčku B 2.0 je blíže vzhledem ke aplikace v grafu, se používá tuto verzi:

![Aplikace s použitím pravidla nejbližší služby Wins](media/projectJson-dependency-5.png)

>[!Warning]
> Pravidlo nejbližší Wins může způsobit přechod na starší verze balíčku, proto potenciálně zásadní Další závislosti v grafu. Proto toto pravidlo se použije s upozorněním k upozornění uživatele.

Toto pravidlo vyšší efektivity s graf závislostí velké (například s balíčky BCL) také výsledkem, protože jakmile dané závislosti se ignoruje, NuGet ignoruje všechny zbývající závislosti v této větvi grafu. Na obrázku níže například Package C 2.0, protože se používají NuGet ignoruje všechny větve v grafu, které odkazují na starší verzi balíčku C:

![Když NuGet ignoruje balíček v grafu, ignoruje tuto celou větev](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Cousin závislosti

Když jiný balíček verze jsou uvedené ve stejném vzdálenosti v grafu z aplikace, používá NuGet nejnižší verze, která splňuje všechny požadavky na verzi (stejně jako u [nejnižší použitelná verze](#lowest-applicable-version) a [ plovoucí verze](#floating-versions) pravidla). Na obrázku níže, například verze 2.0 balíček B splňuje druhé > = 1.0 omezení a proto se používá:

![Řešení závislostí cousin použití nižší verzi, která splňuje všechna omezení](media/projectJson-dependency-7.png)

V některých případech to není možné splněné všechny požadavky na verzi. Jak je znázorněno níže, pokud balíček A vyžaduje přesně balíček B 1.0 a balíček C vyžaduje balíček B > = 2.0, pak NuGet nejde vyřešit závislosti a vrátí chybu.

![Nelze rozpoznat závislosti z důvodu požadavku na přesnou verzi](media/projectJson-dependency-8.png)

V těchto situacích nejvyšší úrovně příjemce (k aplikaci nebo balíčku) přidat vlastní přímou závislost na balíčku B tak, aby [nejbližší Wins](#nearest-wins) pravidlo vztahuje.

## <a name="dependency-resolution-with-packagesconfig"></a>Řešení závislostí s souboru packages.config

S `packages.config`, závislosti projektu se zapisují do `packages.config` jako seznam bez stromové struktury. Všechny závislosti tyto balíčky je také zapsaná ve stejném seznamu. Při instalaci balíčků NuGet může také upravit `.csproj` souboru `app.config`, `web.config`a další jednotlivé soubory.

S `packages.config`, pokusí přeložit konfliktům v závislostech během instalace každé jednotlivé balíčku NuGet. To znamená, pokud balíček A se instaluje a závisí na balíčku B a B balíček je už uvedené v `packages.config` jako závislost něco jiného, porovnává verze balíčku B žádá a pokusí se najít verzi, která splňuje všechny verze NuGet omezení. Konkrétně vybere NuGet nižší *hlavní.vedlejší* verzi, která splňuje závislosti.

Ve výchozím nastavení, NuGet 2.8 vyhledá nejnižší verze opravy (viz [zpráva k vydání verze NuGet 2.8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). Toto nastavení můžete řídit `DependencyVersion` atribut `Nuget.Config` a `-DependencyVersion` přepnout na příkazovém řádku.  

`packages.config` Zpracování pro řešení závislostí získá složité pro větší grafy závislosti. Každé nové instalace balíčku vyžaduje procházení celý graf a vyvolává minimalizuje konflikty verzí. Když dojde ke konfliktu, instalace se zastaví, byste museli opustit projektu v neurčitém stavu, zejména s potenciální úpravy samotný soubor projektu. To není problém, při použití jiných formátů správu balíčků.

## <a name="managing-dependency-assets"></a>Správa závislostí prostředky

Při použití formátu PackageReference, můžete určit, jaké prostředky z toku závislostí do nejvyšší úrovně projektu. Podrobnosti najdete v tématu [PackageReference](package-references-in-project-files.md#controlling-dependency-assets).

Když projekt nejvyšší úrovně samotného je balíček, také mít kontrolu nad tento tok s použitím `include` a `exclude` atributy uvedené v závislosti `.nuspec` souboru. Zobrazit [souboru .nuspec Reference - závislosti](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Kromě odkazů

Existují scénáře, ve kterých sestavení se stejným názvem, může odkazovat více než jednou v projektu, vytváření návrhu a čas sestavení chyby. Vezměte v úvahu projekt, který obsahuje vlastní verzi `C.dll`a odkazuje na C balíček, který také obsahuje `C.dll`. Ve stejnou dobu projektu také závisí na balíčku B, který také závisí na balíčku C a `C.dll`. V důsledku toho, NuGet nelze určit, které `C.dll` používat, ale závislosti projektu na C balíčku nelze právě odebrat, protože balíček B také na něm závisí.

Chcete-li tento problém vyřešit, musí přímo odkazovat `C.dll` mají (nebo použijte jiný balíček, který odkazuje na ten správný) a pak přidat závislost na balíčku C, který vylučuje všechny její prostředky. To v závislosti na formát správy balíčků v pomocí provádí následujícím způsobem:

- [PackageReference](../consume-packages/package-references-in-project-files.md): Přidat `ExcludeAssets="All"` v závislost:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: odeberte odkaz na PackageC z `.csproj` souboru tak, aby odkazoval pouze verzi `C.dll` , který chcete.
    
## <a name="dependency-updates-during-package-install"></a>Instalace aktualizací závislostí během balíčku 

Při splnění závislostí verze se už není během instalace dalších balíčků aktualizován závislost. Představte si třeba balíček A závisí na balíčku B, který určuje dobu, verze 1.0. Zdrojové úložiště obsahuje verze 1.0, 1.1 a 1.2 balíčku B. Pokud objekt je nainstalovaný v projektu, který již obsahuje B verze 1.0, B 1.0 nadále používá vzhledem k tomu, že splňuje omezení verze. Nicméně pokud balíček A požadavky na verzi 1.1 nebo vyšší b, pak B 1.2 by se nainstaloval. 

## <a name="resolving-incompatible-package-errors"></a>Řešení chyb nekompatibilní balíček

Během balíček operace obnovení, může se zobrazit chyba "jeden nebo více balíčků nejsou kompatibilní...", nebo balíček "není kompatibilní" s cílovou architekturu projektu.

Tato chyba nastane, pokud jeden nebo více balíčků v projektu nevyplývá, že podporují cílové rozhraní projektu; To znamená, že balíček neobsahuje vhodný knihovny DLL v jeho `lib` složku pro cílovou architekturu, která je kompatibilní s projektem. (Viz [platforem](../reference/target-frameworks.md) seznam.) 

Například, pokud je projekt cílen `netstandard1.6` a pokusíte nainstalovat balíček, který obsahuje knihovny DLL v pouze `lib\net20` a `\lib\net45` složky a potom zobrazit zprávy následujícím postupem pro balíček a případně jejích závislých hodnot:

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

Řešení nekompatibility, proveďte jednu z následujících akcí:

- Změnit cíl projekt tak, aby systém, který podporuje balíčky, které chcete použít.
- Obraťte se na autora balíčky a pracovat s nimi při přidání podpory pro zvolenou platformu. Každý balíček výpis stránky na [nuget.org](https://www.nuget.org/) má **kontakt vlastníky** odkaz pro tento účel.

