---
title: Řešení závislostí balíčků NuGet
description: Podrobnosti o procesu, při kterém se řeší a instaluje závislosti balíčku NuGet ve verzi NuGet 2.x i NuGet 3.x+.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 69adbbad20debf2e53f247e85d638b3226c0491d
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323749"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak NuGet řeší závislosti balíčků

Pokaždé, když se balíček nainstaluje nebo přeinstaluje, [](../consume-packages/package-restore.md) což zahrnuje instalaci jako součást procesu obnovení, NuGet nainstaluje také všechny další balíčky, na kterých závisí tento první balíček.

Tyto okamžité závislosti pak mohou mít také závislosti samostatně, což může pokračovat do libovolné hloubky. Tím se vytvoří graf  závislostí, který popisuje vztahy mezi balíčky na všech úrovních.

Pokud má více balíčků stejnou závislost, může se stejné ID balíčku v grafu zobrazit vícekrát, potenciálně s různými omezeními verze. V projektu se ale může použít jenom jedna verze daného balíčku, takže NuGet musí zvolit, která verze se použije. Přesný proces závisí na použitém formátu správy balíčků.

## <a name="dependency-resolution-with-packagereference"></a>Řešení závislostí pomocí PackageReference

Při instalaci balíčků do projektů pomocí formátu PackageReference přidá NuGet odkazy na plochý graf balíčků do příslušného souboru a předem vyřeší konflikty. Tento proces se označuje jako *tranzitivní obnovení*. Opětovná instalace nebo obnovení balíčků je pak proces stahování balíčků uvedených v grafu, což vede k rychlejším a předvídatelnějším sestavením. Můžete také využít plovoucí verze, jako je například 2.8. , abyste se vyhnuli úpravám projektu tak, aby se \* využila nejnovější verze balíčku.

Když se proces obnovení NuGet spustí před sestavením, nejprve překládá závislosti v paměti a výsledný graf zapíše do souboru s názvem `project.assets.json` . Zapíše také vyřešené závislosti do souboru zámku s názvem , pokud `packages.lock.json` je funkce souboru zámku [povolená.](../consume-packages/package-references-in-project-files.md#locking-dependencies)
Soubor assets se nachází ve složce , která ve výchozím nastavení používá složku `MSBuildProjectExtensionsPath` obj projektu. Nástroj MSBuild pak tento soubor přečte a přeloží ho do sady složek, kde lze najít potenciální odkazy, a pak je přidá do stromu projektu v paměti.

Soubor `project.assets.json` je dočasný a neměl by se přidávat do správy zdrojového kódu. Ve výchozím nastavení je uvedený v i `.gitignore` `.tfignore` . Viz [Balíčky a řízení zdrojového kódu.](../consume-packages/packages-and-source-control.md)

### <a name="dependency-resolution-rules"></a>Pravidla řešení závislostí

Přechodné obnovení používá čtyři hlavní pravidla pro řešení závislostí: nejnižší platnou verzi, plovoucí verze, nejbližší výhry a závislosti na úrovni systému.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Nejnižší příslušná verze

Nejnižší použitelné pravidlo verze obnoví nejnižší možnou verzi balíčku definovanou jeho závislostmi. Platí také pro závislosti na aplikaci nebo knihovně tříd, pokud není deklarován jako s plovoucí [desetinnou čárkou](#floating-versions).

Na následujícím obrázku je například verze 1.0-beta považována za nižší než 1.0, takže NuGet zvolí verzi 1.0:

![Výběr nejnižší vhodné verze](media/projectJson-dependency-1.png)

Na následujícím obrázku verze 2.1 není v informačním kanálu dostupná, ale protože omezení verze je >= 2.1, NuGet vybere další nejnižší verzi, která se na ní najde, v tomto případě 2.2:

![Výběr další nejnižší verze dostupné v informačním kanálu](media/projectJson-dependency-2.png)

Když aplikace zadá přesné číslo verze, například 1.2, které není k dispozici v informačním kanálu, NuGet selže s chybou při pokusu o instalaci nebo obnovení balíčku:

![NuGet vygeneruje chybu, když není k dispozici přesná verze balíčku.](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a>Plovoucí verze

Verze plovoucí závislosti je zadaná pomocí \* znaku . Například, `6.0.*`. Tato specifikace verze říká "použijte nejnovější verzi 6.0.x"; `4.*` znamená "použít nejnovější verzi 4.x". Použití libovolné verze redukuje změny v souboru projektu a zároveň udržuje aktuálnost nejnovější verze závislosti.

Při použití plovoucí verze NuGet překládá nejvyšší verzi balíčku, která odpovídá vzoru verze, například získá nejvyšší verzi balíčku, která začíná `6.0.*` na verzi 6.0:

![Volba verze 6.0.1 při vyžádání plovoucí verze 6.0.*](media/projectJson-dependency-4.png)

> [!Note]
> Informace o chování verzí s plovoucí desetinnou čárkou a předběžné verze najdete v tématu [o verzích balíčků.](package-versioning.md#version-ranges)


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Nejbližší vítězové

Pokud graf balíčků pro aplikaci obsahuje různé verze stejného balíčku, NuGet zvolí balíček, který je v grafu nejblíže aplikaci, a ignoruje všechny ostatní. Toto chování umožňuje aplikaci přepsat libovolnou konkrétní verzi balíčku v grafu závislostí.

V následujícím příkladu aplikace závisí přímo na balíčku B s omezením verze >= 2.0. Aplikace také závisí na balíčku A, který zase závisí na balíčku B, ale s omezením >= 1.0. Vzhledem k tomu, že závislost na balíčku B 2.0 je v grafu blízko aplikaci, používá se tato verze:

![Aplikace využívající pravidlo Nejbližší wins](media/projectJson-dependency-5.png)

>[!Warning]
> Pravidlo Nejbližší wins může vést k downgradu verze balíčku, což může vést k přerušení dalších závislostí v grafu. Proto se toto pravidlo použije s upozorněním, které uživatele upozorní.

Toto pravidlo také zvyšuje efektivitu díky rozsáhlému grafu závislostí (například grafům s balíčky seznamu BCL), protože jakmile se danou závislost ignoruje, NuGet také ignoruje všechny zbývající závislosti na dané větvi grafu. Například v následujícím diagramu, protože se používá balíček C 2.0, NuGet ignoruje všechny větve v grafu, které odkazují na starší verzi balíčku C:

![Když NuGet ignoruje balíček v grafu, ignoruje celou větev.](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Neschůdné závislosti

Pokud se v grafu od aplikace ve stejné vzdálenosti od aplikace označují různé verze balíčků, NuGet použije nejnižší [](#lowest-applicable-version) verzi, která splňuje všechny požadavky na verzi (stejně jako nejnižší platná verze a pravidla plovoucích [verzí).](#floating-versions) Na následujícím obrázku například verze 2.0 balíčku B splňuje druhé omezení >= 1.0, a proto se používá:

![Řešení problémových závislostí s využitím nižší verze, která splňuje všechna omezení](media/projectJson-dependency-7.png)

V některých případech není možné splnit všechny požadavky na verzi. Jak je znázorněno níže, pokud balíček A vyžaduje přesně balíček B 1.0 a balíček C vyžaduje balíček B >= 2.0, NuGet nemůže závislosti vyřešit a zobrazí chybu.

![Nerozpoznatelné závislosti kvůli přesnému požadavku na verzi](media/projectJson-dependency-8.png)

V těchto situacích by příjemce nejvyšší úrovně (aplikace nebo balíček) měl přidat vlastní přímou závislost na balíčku B, aby se na něj vztahuje [pravidlo Nejbližší](#nearest-wins) wins.

## <a name="dependency-resolution-with-packagesconfig"></a>Řešení závislostí s packages.config

V systému jsou závislosti projektu zapsány do jako `packages.config` `packages.config` plochý seznam. Všechny závislosti těchto balíčků jsou také zapsány do stejného seznamu. Při instalaci balíčků může NuGet také upravit `.csproj` soubor , a další jednotlivé `app.config` `web.config` soubory.

Pomocí `packages.config` se NuGet pokusí vyřešit konflikty závislostí během instalace jednotlivých balíčků. To znamená, že pokud se instaluje balíček A a závisí na balíčku B a balíček B je už uvedený jako závislost něčeho jiného, NuGet porovná požadované verze balíčku B a pokusí se najít verzi, která splňuje všechna omezení `packages.config` verzí. Konkrétně NuGet vybere nižší hlavní *verzi.podverzovanou,* která splňuje závislosti.

NuGet 2.8 ve výchozím nastavení hledá nejnižší verzi opravy (viz Poznámky k verzi [NuGet 2.8).](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) Toto nastavení můžete řídit prostřednictvím atributu v souboru a `DependencyVersion` `NuGet.Config` přepínače na příkazovém `-DependencyVersion` řádku.  

Proces řešení závislostí se u větších grafů `packages.config` závislostí komplikuje. Každá nová instalace balíčku vyžaduje procházení celého grafu a vyvolává šanci na konflikty verzí. Když dojde ke konfliktu, instalace se zastaví a projekt se ponechá v neurčitém stavu, zejména s potenciálními úpravami samotného souboru projektu. Toto není problém při použití jiných formátů správy balíčků.

## <a name="managing-dependency-assets"></a>Správa prostředků závislostí

Při použití formátu PackageReference můžete řídit tok prostředků ze závislostí do projektu nejvyšší úrovně. Podrobnosti najdete v tématu [PackageReference.](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)

Pokud je projekt nejvyšší úrovně sám balíčkem, máte nad tímto tokem kontrolu také pomocí atributů a se závislostmi uvedenými `include` `exclude` v souboru `.nuspec` . Viz [.nuspec Reference – Dependencies](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Vyloučení odkazů

Existují scénáře, ve kterých se na sestavení se stejným názvem může v projektu odkazovat vícekrát, což vytváří chyby v době návrhu a při sestavení. Představte si projekt, který obsahuje vlastní verzi , a `C.dll` odkazuje na balíček C, který obsahuje také `C.dll` . Současně závisí projekt také na balíčku B, který také závisí na balíčku C a `C.dll` . NuGet proto nemůže určit, který z těchto balíčků se má použít, ale nemůžete jenom odebrat závislost projektu na balíčku C, protože na tom závisí i balíček `C.dll` B.

Pokud chcete tento problém vyřešit, musíte přímo odkazovat na objekt , který chcete (nebo použít jiný balíček, který odkazuje na ten správný), a pak přidat závislost na balíčku C, který vyloučí všechny `C.dll` jeho prostředky. To se provádí takto v závislosti na formátu správy balíčků, který se používá:

- [PackageReference:](../consume-packages/package-references-in-project-files.md) `ExcludeAssets="All"` přidejte závislost:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: Odebere odkaz na PackageC ze souboru tak, aby odkaz měl jenom na verzi, `.csproj` `C.dll` kterou chcete.
    
## <a name="dependency-updates-during-package-install"></a>Aktualizace závislostí během instalace balíčku 

Pokud už je verze závislosti splněná, při jiných instalacích balíčků se závislost ne aktualizována. Představte si například balíček A, který závisí na balíčku B a jako číslo verze určuje 1.0. Zdrojové úložiště obsahuje verze 1.0, 1.1 a 1.2 balíčku B. Pokud je A nainstalované v projektu, který už obsahuje B verze 1.0, pak B 1.0 zůstane v použití, protože splňuje omezení verze. Pokud by ale balíček A měl požadavky B verze 1.1 nebo vyšší, byla by nainstalovaná verze B 1.2. 

## <a name="resolving-incompatible-package-errors"></a>Řešení chyb nekompatibilních balíčků

Během operace obnovení balíčku se může zobrazit chyba Jeden nebo více balíčků není kompatibilní... nebo že balíček "není kompatibilní" s cílovou architekturou projektu.

K této chybě dochází v případě, že jeden nebo více balíčků odkazovaných ve vašem projektu neznačí, že podporují cílovou rozhraní projektu. To znamená, že balíček neobsahuje vhodnou knihovnu DLL ve své složce pro cílovou `lib` rozhraní, která je kompatibilní s projektem. (Seznam [najdete v tématu](../reference/target-frameworks.md) Cílová rozhraní.) 

Pokud například projekt cílí na a pokusíte se nainstalovat balíček, který obsahuje knihovny DLL pouze ve složkách a , zobrazí se pro balíček a případně i jeho závislé zprávy jako `netstandard1.6` `lib\net20` `\lib\net45` následující:

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

Nekompatibilitu vyřešíte jedním z následujících způsobů:

- Změřte svůj projekt na rozhraní podporované balíčky, které chcete použít.
- Obraťte se na autora balíčků a spojte se s nimi a přidejte podporu pro vámi zvolenou architekturu. Každá stránka výpisu balíčků [v nuget.org](https://www.nuget.org/) má pro tento účel odkaz **Vlastníci** kontaktů.
