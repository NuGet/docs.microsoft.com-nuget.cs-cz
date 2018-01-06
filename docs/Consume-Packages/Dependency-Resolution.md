---
title: "Balíček NuGet závislostí řešení | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1d530a72-3486-4a0d-b6fb-017524616f91
description: "Informace o procesu, pomocí kterého se balíček NuGet závislosti vyřešen a nainstalované v obou NuGet 2.x a NuGet 3.x+."
keywords: "Závislosti balíčků NuGet, Správa verzí NuGet, verze závislosti, verze grafu, verze rozlišení, přenositelné obnovení"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 251ae6944cc0010f596c9b3daf95c318595a5c4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak NuGet řeší závislosti balíčků

Vždy, když je balíček nainstalován, nebo přeinstalovat, včetně instaluje jako součást [obnovení](../consume-packages/package-restore.md) procesu NuGet nainstaluje také všechny další balíčky, na kterých závisí tento první balíček.

Tyto okamžité závislosti potom také může mít závislosti na jejich vlastní, které můžete pokračovat v libovolné hloubka. To vytváří, co se nazývá *graf závislostí* která popisuje vztahy mezi balíčky jsou všechny úrovně.

Pokud více balíčků stejné závislosti, pak stejné ID balíčku může vyskytovat v grafu vícekrát, potenciálně s omezeními jinou verzi. Však jenom jedna verze nástroje daného balíčku můžete použít v projektu, takže NuGet musíte zvolit, která verze je použít. Přesný postup závisí na formátu odkaz balíčku, který je používán.

V tomto tématu:
- [Řešení závislostí s PackageReference a project.json](#dependency-resolution-with-packagereference-and-projectjson)
- [Řešení závislostí s souboru Packages.config je.](#dependency-resolution-with-packagesconfig)
- [S výjimkou odkazy](#excluding-references), který je nezbytný, pokud dojde ke konfliktu mezi závislost zadanou v jednom projektu a sestavení, které se vytvářejí pomocí jiného.
- [Instalace aktualizací závislostí během balíčku](#dependency-updates-during-package-install)
- [Řešení chyb při nekompatibilní balíčku](#resolving-incompatible-package-errors)

## <a name="dependency-resolution-with-packagereference-and-projectjson"></a>Řešení závislostí s PackageReference a project.json

Při instalaci balíčků do projektů pomocí PackageReference nebo `project.json` formátů, NuGet přidá reference na graf ploché balíčku v příslušný soubor a řeší konflikty předem. Tento proces se označuje jako *přenositelné obnovení*. Přeinstalovat nebo při obnovování balíčků je pak proces stahování balíčky uvedené v tomto grafu, výsledkem je rychlejší a předvídatelnější sestavení. Můžete také využít výhod zástupný znak (plovoucí) verze, jako je například 2.8. \*, zabraňující nákladné a Chyba volání náchylné k chybám `nuget update` na klientské počítače a servery sestavení.

Když je proces obnovení NuGet spuštěna před sestavení, nejprve přeloží závislosti v paměti a pak zapíše výsledný grafu do souboru s názvem `project.assets.json` v `obj` složce projektu pomocí PackageReference nebo do souboru s názvem `project.lock.json` spolu s `project.json`. MSBuild pak přečte tento soubor a překládá do sady složek, kde naleznete potenciální odkazy a přidá je do stromu projektu v paměti.

Soubor zámků je dočasný a by neměly být přidávány do správy zdrojového kódu. Je uvedena ve výchozím nastavení v obou `.gitignore` a `.tfignore`. V tématu [balíčky a Správa zdrojového kódu](Packages-and-Source-Control.md).

### <a name="dependency-resolution-rules"></a>Pravidla řešení závislostí

Přenositelné obnovení používá čtyři hlavní pravidla o vyřešení závislostí: nejnižší příslušné verze, plovoucí verze, nejbližší wins a cousin závislosti.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Nejnižší příslušné verze

Nejnižší verze příslušné pravidlo obnoví nejnižší verzi balíčku podle definice jeho závislé součásti. Platí také pro závislosti na aplikaci nebo knihovny tříd Pokud deklarovaný jako [plovoucí](#floating-versions).

Na následujícím obrázku například 1.0 beta je považováno za nižší než 1.0, NuGet zvolí 1.0 verze:

![Výběr nejnižší příslušné verze](media/projectJson-dependency-1.png)

Na obrázku další verze 2.1 není k dispozici na informační kanál, ale protože je omezení verze > = 2.1 vyskladnění NuGet další nejnižší verze můžete najít v tomto případě 2.2:

![Výběr další dostupná na informační kanál nejnižší verze](media/projectJson-dependency-2.png)

Pokud aplikace určuje přesné číslo verze protokolu, například 1.2, který není k dispozici na informační kanál, NuGet selže s chybou při pokusu o instalaci nebo obnovení balíčku:

![NuGet vygeneruje chybu, když je přesný balíčku verze není k dispozici](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Plovoucí verze (zástupný znak)

Číslo s plovoucí čárkou nebo zástupné verze závislosti zadaný \* zástupný znak, stejně jako u 6.0.\*. Tato verze specifikace říká "použít nejnovější verzi 6.0.x"; 4.\* znamená "pomocí nejnovější verze 4.x." Pomocí zástupného znaku umožňuje závislost balíčku pokračujte vyvíjející se bez nutnosti změny spotřebitelskou aplikaci (nebo balíček).

Pokud používáte zástupný znak, NuGet řeší nejvyšší verzi balíčku, který odpovídá vzorku verze, například 6.0. \* získá nejvyšší verzi balíčku, který začíná 6.0:

![Výběr verze 6.0.1 při plovoucí verze 6.0. * se požaduje](media/projectJson-dependency-4.png)

> [!Note]
> Informace o chování zástupné znaky a předběžných verzí, naleznete v části [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Nejbližší wins

Když graf balíčku pro aplikace obsahuje různé verze stejného balíčku, NuGet zvolí balíček, který je nejblíže k aplikaci v grafu a všechny ostatní ignoruje. Toto chování umožňuje aplikaci přepsat všechny verze konkrétní balíček v grafu závislostí.

V následujícím příkladu je aplikace závislá přímo na balíček B s omezením na verzi > = 2.0. Aplikace také závisí na balíčku A, což pak také závisí na balíčku B, ale s > = 1.0 omezení. Protože závislost na balíček B 2.0 je blíže aplikace v grafu, že verze se má použít:

![Aplikace pomocí pravidla nejbližší služby Wins](media/projectJson-dependency-5.png)

>[!Warning]
> Pravidlo nejbližší Wins může způsobit přechod na nižší verzi balíčku, proto potenciálně nejnovější Další závislosti v grafu. Proto je použito toto pravidlo upozornění k upozornění uživatele.

Toto pravidlo také výsledkem vyšší efektivity s velké závislost grafu (jako jsou ty balíčky BCL), protože po dané závislost je ignorován, NuGet ignoruje všechny zbývající závislosti na tuto větev grafu. V následujícím diagramu například, protože se používá balíček C 2.0, NuGet ignoruje větve v grafu, které odkazují na starší verzi balíčku C:

![Při NuGet ignoruje balíček v grafu, je ignorováno uvedené celý pobočky](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Cousin závislosti

Pokud jiný balíček verze jsou uvedené ve stejné vzdálenosti v grafu z aplikace, NuGet použije nejnižší verze, která splňuje všechny požadavky verze (stejně jako u [nejnižší příslušné verze](#lowest-applicable-version) a [ plovoucí verze](#floating-versions) pravidla). Na obrázku níže například verze 2.0 balíček B splňuje dalších > = 1.0 omezení a je tedy používá:

![Řešení závislostí cousin pomocí nižší verzi, která splňuje všechna omezení](media/projectJson-dependency-7.png)

V některých případech není možné splňují všechny požadavky verze. Jak je uvedeno níže, pokud balíček A vyžaduje přesně balíček B 1.0 a C balíčku vyžaduje balíček B > = 2.0, pak NuGet nelze vyřešit závislosti a ohlásí chybu.

![Nepřeložitelný závislosti z důvodu požadavku na přesnou verzi](media/projectJson-dependency-8.png)

V těchto situacích nejvyšší úrovně příjemce (aplikace nebo balíčku) přidejte vlastní přímé závislost na balíček B tak, aby [nejbližší Wins](#nearest-wins) pravidlo vztahuje.

## <a name="dependency-resolution-with-packagesconfig"></a>Řešení závislostí s souboru Packages.config je.

S `packages.config`, závislosti projektu se zapisují do `packages.config` jako plochý seznam. Všechny závislosti tyto balíčky se zapisují taky ve stejném seznamu. Při instalaci balíčků NuGet může také upravit `.csproj` souboru `app.config`, `web.config`a další jednotlivé soubory.

S `packages.config`, NuGet pokusí o řešení konfliktů závislostí při instalaci jednotlivých jednotlivých balíčků. To znamená, pokud balíček A probíhá instalace a závisí na balíčku B a B balíček je již uveden v `packages.config` jako závislost něco jiného, porovná verze balíčku B požadovanou NuGet a pokusí se najít na verzi, která splňuje všechny verze omezení. Konkrétně NuGet vybere dolní *major.minor* verzi, která splňuje závislosti.

Ve výchozím nastavení, vyřeší nejvyšší NuGet 2.7 a starší *oprava* verze (pomocí *major.minor.patch.build* convention). [NuGet 2,8 a vyšší](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) toto chování má být vyhledán nejnižší verze opravy ve výchozím nastavení se změní. Můžete řídit prostřednictvím toto nastavení `DependencyVersion` atribut `Nuget.Config` a `-DependencyVersion` přepnout na příkazovém řádku.  

`packages.config` Zpracování pro řešení závislostí získá složitý pro větší grafy závislostí. Každé nové instalace balíčku vyžaduje přecházení přes celou grafu a vyvolá riziko pro konflikty verzí. Když dojde ke konfliktu, instalace se zastaví, nechat projektu v neurčitém stavu, zejména s potenciální úpravy samotný soubor projektu. Nejedná se o problém při použití jiných formátů odkaz na balíček.


## <a name="managing-dependency-assets"></a>Správa závislostí prostředky

Při použití `project.json` nebo PackageReference formáty, které prostředky z toku závislosti do nejvyšší úrovně projektu můžete řídit. Podrobnosti najdete v tématu [project.json](../Schema/project-json.md) a [balíček odkazy v souborech projektu](Package-References-in-Project-Files.md#controlling-dependency-assets).

Pokud nejvyšší úrovně projektu samotné je balíček, máte také kontrolu nad tento tok pomocí `include` a `exclude` atributy s uvedené v závislosti `.nuspec` souboru. V tématu [příponou .nuspec odkaz - závislosti](../Schema/nuspec.md#dependencies).

## <a name="excluding-references"></a>S výjimkou odkazy

Existují scénáře, ve kterých sestavení se stejným názvem může odkazovat více než jednou v projektu generovala chyby při návrhu a čase vytvoření buildu. Zvažte projekt, který obsahuje vlastní verzi `C.dll`a odkazuje na C balíček, který také obsahuje `C.dll`. Ve stejnou dobu, projekt také závisí na balíčku B, který také závisí na balíčku C a `C.dll`. V důsledku toho by který NuGet nelze určit `C.dll` chcete použít, ale projektu závislost na balíček C nelze právě odebrat, protože balíček B také na něm závisí.

Chcete-li tento problém vyřešili, musíte přímý odkaz `C.dll` mají (nebo použijte jiný balíček, který odkazuje na ten správný) a potom ho přidat závislost na C balíček, který vyloučí všechny její prostředky. To v závislosti na formátu odkaz balíčku používá provádí následujícím způsobem:

- [PackageReference](../consume-packages/package-references-in-project-files.md): Přidejte `Exclude="All"` v závislost:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- `packages.config`: odeberte odkaz na PackageC z `.csproj` tak, aby odkazuje jenom verze `C.dll` , které chcete.
    
- `project.json`: Přidejte `"exclude" : "all"` v závislost PackageC:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="dependency-updates-during-package-install"></a>Instalace aktualizací závislostí během balíčku 

U balíčku NuGet 2.4.x a dříve, pokud balíček je nainstalovaná, jejichž závislostí v projektu již existuje, závislost se aktualizuje na nejnovější verzi, která splňuje omezení verze i v případě, že stávající verzi také splňuje tyto omezení. 

Představte si třeba balíček A, který závisí na balíčku B a určuje 1.0 pro číslo verze. Zdrojové úložiště obsahuje obě verze 1.0, 1.1 a 1.2 balíčku B. Pokud v projektu, který již obsahuje B verze 1.0 je nainstalovaná A, B se aktualizuje verze 1.2. 

S NuGet 2.5 nebo novější Pokud je již splnit verze závislosti, závislost neaktualizuje během instalace dalších balíčků. 

V tomto příkladě výše instalaci balíčku, který zůstane balíček B 1.0 v projektu A do projektu s NuGet 2.5 nebo novější, protože již splňuje omezení verze. Ale pokud balíček A měli požadavky verze 1.1 nebo vyšší b, B 1.2 by možné nainstalovat. 

## <a name="resolving-incompatible-package-errors"></a>Řešení chyb při nekompatibilní balíčku

Během balíček operaci obnovení, mohou se zobrazit chyba "jeden nebo více balíčků nejsou kompatibilní...", nebo balíček "není kompatibilní" s cílový framework projektu na.

K této chybě dojde, když jeden nebo více balíčků, kterou se odkazuje v projektu neoznačují podporují cílový framework projektu na; To znamená, balíček neobsahuje vhodný knihovny DLL v jeho `lib` složku pro cílové rozhraní, které je kompatibilní s projektu. (Viz [cílové architektury](../Schema/Target-Frameworks.md) seznam.) 

Například, pokud cíle projektu `netstandard1.6` a zkusíte nainstalovat balíček, který obsahuje knihovny DLL v pouze `lib\net20` a `\lib\net45` složky a potom zobrazí zprávy, jako je pro balíček a případně jeho položky závislé na následující:

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

Pro vyřešení problémům s kompatibilitou, proveďte jednu z těchto možností:

- Změňte cíl projektu pro rozhraní, které podporuje balíčky, které chcete použít.
- Obraťte se na autora balíčků a pracovat s nimi přidání podpory pro vaši zvolenou framework. Každý balíček výpis stránky na [nuget.org](https://www.nuget.org/) má **kontaktujte vlastníky** odkaz pro tento účel.
- **Nedoporučuje se**: jako dočasné řešení při práci s autora balíčku projekty cílení na `netcore`, `netstandard`, a `netcoreapp` mohou ostatní platformy jako kompatibilní, a tím umožní balíčky cílené na těch, které označují ostatní platformy, který se má použít. V tématu [project.json importuje](../Schema/project-json.md#imports) a [cíl obnovení MSBuild PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback). To může způsobit neočekávané chování, proto znovu, je vhodné řešení nekompatibility balíček ve spolupráci s autora balíčku na aktualizace.
