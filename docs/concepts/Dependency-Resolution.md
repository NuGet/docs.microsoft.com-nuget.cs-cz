---
title: Řešení závislostí balíčku NuGet
description: Podrobnosti o procesu, pomocí kterého se v NuGet 2. x a NuGet 3. x + vyřeší a nainstalují závislosti balíčku NuGet.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: c6f50e6eb21826afebcdcd4045c7ab8b6e6489e3
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813322"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak NuGet řeší závislosti balíčků

Při každém instalaci nebo přeinstalaci balíčku, který zahrnuje instalaci jako součást procesu [obnovení](../consume-packages/package-restore.md) , nainstaluje také všechny další balíčky, na kterých je první balíček závislý.

Tyto okamžité závislosti mohou mít také vlastní závislosti, které mohou pokračovat s libovolnou hloubkou. Tím se říká *graf závislosti* , který popisuje vztahy mezi balíčky na všech úrovních.

Pokud má více balíčků stejnou závislost, pak se stejné ID balíčku může v grafu zobrazit víckrát, potenciálně s různými omezeními verze. V projektu se však dá použít jenom jedna verze daného balíčku, takže NuGet musí zvolit, která verze se má použít. Přesný proces závisí na použitém formátu správy balíčků.

## <a name="dependency-resolution-with-packagereference"></a>Rozlišení závislosti s PackageReference

Při instalaci balíčků do projektů pomocí formátu PackageReference přidá NuGet v příslušném souboru odkazy na graf plochých balíčků a vyřeší konflikty před časem. Tento proces se označuje jako *přechodné obnovení*. Přeinstalace nebo obnovení balíčků je proces stahování balíčků uvedených v grafu, což vede k rychlejšímu a více předvídatelným sestavením. Můžete také využít výhod zástupných znaků (plovoucí), například 2,8.\*, což umožňuje vyhnout se nákladným a náchylným chybám a voláním `nuget update` na klientských počítačích a serverech sestavení.

Když se proces obnovení NuGet spustí před sestavením, vyřeší nejprve závislosti v paměti a pak zapíše výsledný graf do souboru s názvem `project.assets.json`. Zapisuje také vyřešené závislosti do souboru zámku s názvem `packages.lock.json`, pokud [je povolena funkce zámku souboru](../consume-packages/package-references-in-project-files.md#locking-dependencies).
Soubor prostředků je umístěn na `MSBuildProjectExtensionsPath`, který je ve výchozím nastavení složkou "obj" projektu. Nástroj MSBuild pak přečte tento soubor a převede ho do sady složek, kde mohou být nalezeny možné odkazy, a poté je přidá do stromu projektu v paměti.

Soubor `project.assets.json` je dočasný a neměl by být přidán do správy zdrojových kódů. Je uvedený ve výchozím nastavení v `.gitignore` i `.tfignore`. Viz [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Pravidla řešení závislostí

Přenosné obnovení používá čtyři hlavní pravidla pro řešení závislostí: nejnižší použitelná verze, plovoucí verze, nejbližší služba WINS a závislosti Cousin.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Nejnižší platná verze

Nejnižší platná verze pravidla obnoví nejnižší možnou verzi balíčku, jak je definuje jeho závislosti. Platí také pro závislosti na aplikaci nebo knihovně tříd, pokud není deklarována jako [plovoucí](#floating-versions).

Na následujícím obrázku je například 1,0-beta považován za nižší než 1,0, takže NuGet zvolí verzi 1,0:

![Výběr nejnižší použitelné verze](media/projectJson-dependency-1.png)

Na následujícím obrázku verze 2,1 není v informačním kanálu k dispozici, ale vzhledem k tomu, že omezení verze je > = 2,1 NuGet vybere další nejnižší verzi, kterou může najít, v tomto případě 2,2:

![Výběr nejbližší nejnižší verze dostupné v informačním kanálu](media/projectJson-dependency-2.png)

Když aplikace určí přesné číslo verze, například 1,2, které není v informačním kanálu k dispozici, NuGet při pokusu o instalaci nebo obnovení balíčku dojde k chybě.

![NuGet vygeneruje chybu, pokud není dostupná přesná verze balíčku.](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Plovoucí verze (zástupné znaky)

V případě, že je zadána verze s plovoucí nebo zástupné znaky, je \* zástupný znak, jako je 6,0.\*. Tato specifikace verze říká "použít nejnovější verzi 6.0. x"; 4.\* znamená "použít nejnovější verzi 4. x." Použití zástupného znaku umožňuje, aby balíček závislostí pokračoval ve vývoji bez nutnosti změny náročné aplikace (nebo balíčku).

Při použití zástupného znaku NuGet vyřeší nejvyšší verzi balíčku, který odpovídá vzoru verze, například 6,0.\* získá nejvyšší verzi balíčku, který začíná 6,0:

![Výběr verze 6.0.1, když se požaduje plovoucí verze 6,0. *](media/projectJson-dependency-4.png)

> [!Note]
> Informace o chování zástupných znaků a předběžných verzích najdete v tématu [Správa verzí balíčků](package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Nejbližší služba WINS

Když graf balíčku pro aplikaci obsahuje různé verze stejného balíčku, vybere NuGet balíček, který je nejblíže aplikaci v grafu a ignoruje všechny ostatní. Toto chování umožňuje aplikaci přepsat jakoukoli konkrétní verzi balíčku v grafu závislostí.

V následujícím příkladu aplikace závisí přímo na balíčku B s omezením verze > = 2.0. Aplikace také závisí na balíčku A, který také závisí na balíčku B, ale s omezením > = 1.0. Vzhledem k tomu, že závislost na balíčku B 2,0 je blízko aplikace v grafu, používá se tato verze:

![Aplikace používající nejbližší pravidlo služby WINS](media/projectJson-dependency-5.png)

>[!Warning]
> Nejbližší pravidlo služby WINS může mít za následek downgrade verze balíčku, takže může poškodit jiné závislosti v grafu. Proto se toto pravidlo použije s upozorněním na upozornění uživatele.

Toto pravidlo také vede k větší efektivitě s rozsáhlým grafem závislosti (jako jsou s balíčky BCL), protože jakmile se daná závislost ignoruje, NuGet také ignoruje všechny zbývající závislosti v této větvi grafu. V následujícím diagramu, například, protože se používá balíček C 2,0, ignoruje NuGet všechny větve v grafu, které odkazují na starší verzi balíčku C:

![Když NuGet ignoruje balíček v grafu, ignoruje celou větev.](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Závislosti Cousin

V případě, že se na stejnou vzdálenost v grafu od aplikace odkazují různé verze balíčků, používá NuGet nejnižší verzi, která splňuje všechny požadavky na verzi (stejně jako u [nejnižší použitelné verze](#lowest-applicable-version) a pravidla pro [plovoucí verze](#floating-versions) ). Na následujícím obrázku je například verze 2,0 balíčku B, která splňuje jiné omezení > = 1.0 a používá se takto:

![Řešení závislostí Cousin pomocí nižší verze, která splňuje všechna omezení](media/projectJson-dependency-7.png)

V některých případech není možné splnit všechny požadavky na verzi. Jak je vidět níže, pokud balíček A vyžaduje přesně balíček B 1,0 a balíček C vyžaduje balíček B > = 2.0, nemůže NuGet vyřešit závislosti a zobrazí chybu.

![Nepřeložitelné závislosti z důvodu přesného požadavku na verzi](media/projectJson-dependency-8.png)

V těchto situacích by měl uživatel nejvyšší úrovně (aplikace nebo balíček) přidat vlastní přímou závislost na balíčku B, aby se [nejbližší pravidlo služby WINS](#nearest-wins) naplatilo.

## <a name="dependency-resolution-with-packagesconfig"></a>Řešení závislosti s balíčky. config

Při `packages.config`jsou závislosti projektu zapisovány do `packages.config` jako nestrukturovaný seznam. Všechny závislosti těchto balíčků jsou také zapsány ve stejném seznamu. Po instalaci balíčků může NuGet změnit také soubor `.csproj`, `app.config`, `web.config`a další jednotlivé soubory.

Při `packages.config`se NuGet pokusí vyřešit konflikty závislostí při instalaci každého jednotlivého balíčku. To znamená, že pokud je balíček A nainstalován a závisí na balíčku B, a balíček B je již uveden v `packages.config` jako závislost nějakého jiného, NuGet porovná požadované verze balíčku B a pokusí se najít verzi, která splňuje všechna omezení verzí. Konkrétně vybere nižší *hlavní verzi.* podverze, která splňuje závislosti.

Ve výchozím nastavení vyhledá NuGet 2,8 nejnižší verzi opravy (viz zpráva k [vydání verze NuGet 2,8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). Toto nastavení můžete řídit pomocí atributu `DependencyVersion` v `Nuget.Config` a přepínače `-DependencyVersion` na příkazovém řádku.  

Proces `packages.config` pro řešení závislostí bude pro větší grafy závislostí složitý. Každé nové instalaci balíčku vyžaduje procházení celého grafu a vyvolává pravděpodobnost konfliktu verzí. Dojde-li ke konfliktu, instalace je zastavena a projekt zůstane v neurčitém stavu, zejména s případnými změnami samotného souboru projektu. Nejedná se o problém při použití jiných formátů správy balíčků.

## <a name="managing-dependency-assets"></a>Správa prostředků závislosti

Při použití formátu PackageReference můžete řídit, které prostředky se mají směrovat do projektu nejvyšší úrovně. Podrobnosti najdete v tématu [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Když je projekt nejvyšší úrovně sám balíčkem, máte také kontrolu nad tímto tokem pomocí atributů `include` a `exclude` se závislostmi uvedenými v souboru `.nuspec`. Viz [referenční závislosti. nuspec](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Vyloučení odkazů

Existují scénáře, ve kterých může být sestavení se stejným názvem v projektu odkazována více než jednou, což vyprodukuje chyby návrhu a doby sestavování. Vezměte v úvahu projekt, který obsahuje vlastní verzi `C.dll`a odkazuje na balíček C, který obsahuje také `C.dll`. Zároveň projekt závisí také na balíčku B, který také závisí na balíčku C a `C.dll`. V důsledku toho NuGet nemůže určit, který `C.dll` použít, ale nemůžete pouze odebrat závislost projektu na balíčku C, protože na něm také závisí balíček B.

Chcete-li tento problém vyřešit, musíte přímo odkazovat na `C.dll`, které chcete (nebo použít jiný balíček, který odkazuje na příslušný soubor), a pak přidat závislost na balíčku C, který vylučuje všechny jeho prostředky. To se provádí takto v závislosti na použitém formátu správy balíčků:

- [PackageReference](../consume-packages/package-references-in-project-files.md): přidejte `ExcludeAssets="All"` v závislosti:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: Odeberte odkaz na PackageC ze souboru `.csproj`, aby odkazoval jenom na požadovanou verzi `C.dll`.
    
## <a name="dependency-updates-during-package-install"></a>Aktualizace závislostí při instalaci balíčku 

Pokud je už verze závislosti splněná, závislost se během dalších instalací balíčku neaktualizuje. Zvažte například balíček A, který je závislý na balíčku B, a pro číslo verze určí 1,0. Zdrojové úložiště obsahuje verze 1,0, 1,1 a 1,2 balíčku B. Pokud je nainstalován v projektu, který již obsahuje B verze 1,0, pak B 1,0 zůstává používán, protože splňuje omezení verze. Pokud se ale v balíčku A dostaly požadavky verze 1,1 nebo vyšší z B, pak se nainstaluje B 1,2. 

## <a name="resolving-incompatible-package-errors"></a>Řešení chyb nekompatibilních balíčků

Během operace obnovení balíčku se může zobrazit chyba, že jeden nebo více balíčků není kompatibilních... nebo že balíček "není kompatibilní" s cílovým rozhraním projektu.

K této chybě dochází, pokud jeden nebo více balíčků, na které se odkazuje v projektu, neindikuje, že podporují cílové rozhraní projektu. To znamená, že balíček neobsahuje vhodnou knihovnu DLL ve složce `lib` pro cílovou architekturu, která je kompatibilní s projektem. (Viz [cílové architektury](../reference/target-frameworks.md) pro seznam.) 

Například pokud projekt cílí na `netstandard1.6` a pokusíte se nainstalovat balíček, který obsahuje knihovny DLL pouze v `lib\net20` a `\lib\net45` složky, pak se zobrazí zprávy podobné následujícímu balíčku pro balíček a případně jeho závislé položky:

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

Chcete-li vyřešit nekompatibilitu, proveďte jednu z následujících akcí:

- Svůj projekt můžete změnit na rámec, který podporují balíčky, které chcete použít.
- Kontaktujte autora balíčků a pracujte s nimi a přidejte podporu pro zvolenou architekturu. Každá stránka se seznamem balíčků na [NuGet.org](https://www.nuget.org/) má pro tento účel odkaz pro **vlastníky kontaktů** .
