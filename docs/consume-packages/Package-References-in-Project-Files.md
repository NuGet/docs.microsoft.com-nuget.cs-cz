---
title: Formát NuGet PackageReference (odkazy na balíček v souborech projektu)
description: Podrobnosti na NuGet PackageReference v souborech projektu podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c2dfce8de6b28aaee99e3d5ab75cd28950a8cb0f
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812835"
---
# <a name="package-references-packagereference-in-project-files"></a>Odkazy na balíček (PackageReference) v souborech projektu

Balíček odkazů pomocí nástroje `PackageReference` uzlu, správě závislostí NuGet přímo v rámci projektových souborů (na rozdíl od samostatné `packages.config` souboru). Pomocí PackageReference, jako je volána, nemá vliv na ostatní aspekty NuGet; například nastavení v `NuGet.config` soubory (včetně zdroje balíčků) se uplatní, jak je vysvětleno v [konfigurace chování Nugetu](configuring-nuget-behavior.md).

S PackageReference můžete také použít podmínky nástroje MSBuild zvolit odkazy na balíček na cílovou architekturu, konfigurace, platformy nebo další seskupení. Umožňuje také pro detailní kontrolu nad závislostí a obsahu toku. (Další podrobnosti najdete v [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Podpora typu projektu

Ve výchozím nastavení je použít PackageReference pro projekty .NET Core, .NET Standard projekty a projekty UPW cílení na Windows 10 sestavení 15063 (Creators Update) a novější, s výjimkou projekty C++ UWP. Projekty rozhraní .NET framework podporují PackageReference, ale nyní jako výchozí `packages.config`. Použití PackageReference, [migrovat](../reference/migrate-packages-config-to-package-reference.md) závislosti z `packages.config` do souboru projektu, odstraňte soubor packages.config.

Aplikace ASP.NET cílí na úplné rozhraní .NET Framework obsahují pouze [omezenou podporu](https://github.com/NuGet/Home/issues/5877) pro PackageReference. C++a typy projektů jazyka JavaScript se nepodporují.

## <a name="adding-a-packagereference"></a>Přidávání PackageReference

Přidáte závislost v souboru projektu pomocí následující syntaxe:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Řízení verze závislosti

Konvence pro určení verze balíčku je stejný jako při použití `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

V předchozím příkladu 3.6.0 znamená, že všechny verze, která je > = 3.6.0 s předností nejnižší verze, jak je popsáno na [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Pomocí projektu s PackageReferences žádné PackageReference
Pokročilé: Pokud jste žádné balíčky nainstalované v projektu (žádné PackageReferences v souboru projektu) a žádný soubor packages.config, ale chcete projekt tak, aby se obnovit jako PackageReference styl, můžete nastavit vlastnost projektu RestoreProjectStyle na PackageReference v projektu soubor.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
To může být užitečné, pokud se budete odkazovat na projekty, které jsou PackageReference ve stylu (existující csproj nebo projekty založenými na sadu SDK). Tato možnost povolí balíčky, které odkazují tyto projekty, do "přechodně" odkazuje váš projekt.

## <a name="floating-versions"></a>Plovoucí verze

[Plovoucí verze](../consume-packages/dependency-resolution.md#floating-versions) podporují `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Řízení závislosti prostředků

Může používat závislost čistě jako vývojové prostředí a nemusí chcete je zveřejnit, která do projektů, které budou využívat vašeho balíčku. V tomto scénáři můžete použít `PrivateAssets` metadat a řídit tak toto chování.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Následující značky metadat určovat závislost prostředky:

| Značka | Popis | Výchozí hodnota |
| --- | --- | --- |
| IncludeAssets | Tyto prostředky budou využívat. | všechny |
| ExcludeAssets | Tyto prostředky nebude využívat. | žádná |
| PrivateAssets | Tyto prostředky budou využívat, ale nebude směrovat do nadřazeného projektu | contentfiles; analyzátory; sestavení |

Povolené hodnoty pro tyto značky jsou následujícím způsobem s více hodnotami, které jsou odděleny středníkem s výjimkou s `all` a `none` který musí být uvedena samy o sobě:

| Value | Popis |
| --- | ---
| Kompilace | Obsah `lib` složky a ovládací prvky, jestli můžete zkompilovat váš projekt proti sestavení ve složce |
| modul runtime | Obsah `lib` a `runtimes` složky a ovládací prvky, jestli tato sestavení bude zkopírována do sestavení výstupního adresáře |
| contentFiles | Obsah `contentfiles` složky |
| sestavení | Vlastnosti a cíle ve `build` složky |
| Analyzátory | Analyzátory .NET |
| nativní | Obsah `native` složky |
| žádná | Žádná z výše uvedených se používají. |
| všechny | Všechny výš uvedené (s výjimkou `none`) |

V následujícím příkladu se všechno kromě soubory obsahu z balíčku by být využívány službou projektu a všechno, co s výjimkou souborů obsahu a analyzátory by tok na nadřazený projekt.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Upozorňujeme, že `build` není součástí `PrivateAssets`, zaměřuje a props *bude* tok, který nadřazeného projektu. Zvažte například, že výše uvedené odkaz se používá v projektu, který vytvoří balíček NuGet s názvem AppLogger. AppLogger může spotřebovat cíle a vlastnosti z `Contoso.Utility.UsefulStuff`, jak můžete projektech, které využívají AppLogger.

## <a name="adding-a-packagereference-condition"></a>Přidání podmínky PackageReference

Můžete použít podmínku pro ovládací prvek, jestli balíček je zahrnuta, pokud podmínky můžete použít jakoukoli proměnnou MSBuild nebo Proměnná definovaná v souboru cílů nebo vlastnosti. Ale v současnosti pouze `TargetFramework` proměnná je podporována.

Předpokládejme například, že vývoji cílíte `netstandard1.4` stejně jako `net452` , ale mají závislost, kterou lze použít pouze pro `net452`. V tomto případě nechcete `netstandard1.4` projekt, který se spotřebovává balíček pro přidání tohoto zbytečné závislosti. Chcete-li tomu zabránit, určíte podmínku na `PackageReference` následujícím způsobem:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Balíček vytvořené pomocí tohoto projektu se zobrazí, že je jako závislost pouze pro Newtonsoft.Json `net452` cíl:

![Výsledek použití podmínku na PackageReference s VS2017](media/PackageReference-Condition.png)

Podmínek je také možné použít na `ItemGroup` úrovně a má platit pro všechny podřízené objekty `PackageReference` prvky:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a>Uzamčení závislosti
*Tato funkce je k dispozici s NuGet **4.9** nebo vyšší a sadou Visual Studio 2017 **15.9** nebo vyšší.*

Vstup pro obnovení NuGet je sada odkazy na balíčky ze souboru projektu (závislosti nejvyšší úrovně a direct) a výstup je úplné uzavření všechny závislosti balíčků, včetně přechodné závislosti. NuGet se pokusí vždy vytvořila stejný úplný uzavření závislosti balíčků, pokud nedošlo ke změně vstupní seznam PackageReference. Existují však některé scénáře, kdy je to možné. Příklad:

* Při použití s plovoucí desetinnou čárkou, jako je verze `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. I když jsou záměr zde uvolnění na nejnovější verzi na každý obnovení balíčků, jsou scénáře, kdy uživatelé vyžadují graf tak, aby být pevně nastavené na určitého nejnovější verzi a plovoucí desetinnou čárkou na novější verzi, pokud je k dispozici na explicitní gest.
* Je publikovaný novější verzi balíčku požadavky na odpovídající verzi PackageReference. Například 

  * Dne 1: Pokud jste zadali `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` ale byly k dispozici verze na úložiště NuGet 4.1.0, 4.2.0 a 4.3.0. V takovém případě by byly vyřešeny NuGet do 4.1.0 (nejbližší minimální verze)

  * Dne 2: Získá publikované verze 4.0.0. NuGet teď najít přesnou shodu a začít překládat 4.0.0

* Verze daného balíčku bude odebrána z úložiště. Když nuget.org neumožňuje balíček odstranění, ne všechna úložiště balíčků nastavit toto omezení. Výsledkem je najít nejlepší shodu při nelze přeložit na odstraněné verze NuGet.

### <a name="enabling-lock-file"></a>Povolení soubor zámku
Aby bylo možné zachovat Úplné uzavření závislosti balíčků můžete můžete vyjádřit výslovný souhlas s funkcí soubor zámku nastavením vlastnosti MSBuild `RestorePackagesWithLockFile` pro váš projekt:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Pokud je tato vlastnost nastavena, obnovení NuGet vygeneruje soubor zámku - `packages.lock.json` souboru v kořenovém adresáři projektu, který obsahuje seznam všech balíčků závislostí. 

> [!Note]
> Jakmile je projekt `packages.lock.json` soubor v kořenovém adresáři soubor zámku je vždy využít i v případě obnovení vlastnost `RestorePackagesWithLockFile` není nastaven. Dalším způsobem, jak vyjádřit výslovný souhlas s touto funkcí je vytvořte fiktivního prázdný `packages.lock.json` souboru v kořenovém adresáři projektu.

### <a name="restore-behavior-with-lock-file"></a>`restore` chování s soubor zámku
Pokud se nachází soubor zámku pro projekt, NuGet používá ke spuštění tohoto uzamknout souboru `restore`. NuGet nemá Rychlá kontrola, zda byly změny v závislosti balíčků, jak je uvedeno v souboru projektu (nebo soubory závislých projektů) a pokud nejsou žádné změny jenom obnoví balíčky uvedené v souboru zámku. Neexistuje žádné opakované vyhodnocení závislosti balíčků.

NuGet zjistí změnu v definované závislostí, jak je uvedeno v souborech projektů, znovu vyhodnotí grafu balíčku a aktualizuje soubor zámku tak, aby odrážely nový balíček uzavření pro projekt.

Pro CI/CD a další scénáře, ve kterém by chcete změnit závislosti balíčků v reálném čase, můžete to provést nastavením `lockedmode` k `true`:

Pro dotnet.exe spusťte:
```
> dotnet.exe restore --locked-mode
```

Msbuild.exe spusťte tento příkaz:
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Může také nastavit podmíněné vlastnost MSBuild v souboru projektu:
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Pokud uzamčeném režimu `true`, obnovení bude obnovení přesné balíčků, jak je uvedeno v souboru zámku nebo selhat, pokud jste aktualizovali závislosti definované balíčků pro projekt, po vytvoření souboru zámku.

### <a name="make-lock-file-part-of-your-source-repository"></a>Zařazení zamknout soubor zdrojového úložiště
Pokud vytváříte aplikaci, spustitelný soubor a dotyčný projektu je na začátku řetězu závislostí zkontrolujte v souboru zámku na úložiště zdrojového kódu tak, aby NuGet můžete využít během obnovení.

Ale pokud váš projekt je projekt knihovny, který jste Nedodávejte nebo běžné projekt kódu na další projekty se závisí na vás **by neměla** jako součást vašeho zdrojového kódu se změnami soubor zámku. Neexistuje nezpůsobily žádné potíže ochraně souboru zámku ale závislosti uzamčené balíčků pro běžné projekt kódu nesmí být použit, jak je uvedeno v souboru zámku během obnovení/sestavení projektu, který závisí na tomto společný kód projektu.

Např.
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
Pokud `ProjectA` závislý na `PackageX` verze `2.0.0` a také odkazuje na `ProjectB` , který závisí na `PackageX` verze `1.0.0`, pak soubor zámku pro `ProjectB` zobrazí seznam závislost na `PackageX` verze `1.0.0`. Ale když `ProjectA` vytvořili, platnost zámku soubor bude obsahovat závislost na `PackageX` verze **`2.0.0`** a **není** `1.0.0` jak je uvedeno v souboru zámku pro `ProjectB`. Proto soubor zámku běžné kódového projektu má málo say přeložit pro projekty, které jsou na ní závislé balíčky.

### <a name="lock-file-extensibility"></a>Rozšíření souboru zámku
Jak je popsáno níže, můžete se soubor zámku ovládání různého chování obnovení:

| Možnost | Ekvivalentní možnosti MSBuild | 
|:---  |:--- |
| `--use-lock-file` | Bootstraps použít soubor zámku pro projekt. Můžete také nastavit `RestorePackagesWithLockFile` vlastnost v souboru projektu | 
| `--locked-mode` | Umožňuje uzamčeném režimu pro obnovení. To je užitečné ve scénářích CI/CD, kde byste chtěli získání opakovatelných sestavení. To může být také tak, že nastavíte `RestoreLockedMode` vlastnosti nástroje MSBuild `true` |  
| `--force-evaluate` | Tato možnost je užitečná s balíčky verzí s plovoucí desetinnou čárkou definované v projektu. Ve výchozím nastavení, obnovení NuGet se neaktualizuje automaticky při každé obnovení verze balíčku není-li spustit obnovení s `--force-evaluate` možnost. |
| `--lock-file-path` | Definuje vlastní zámek umístění souboru projektu. To můžete také dosáhnout nastavením vlastnosti MSBuild `NuGetLockFilePath`. Ve výchozím nastavení podporuje NuGet `packages.lock.json` v kořenovém adresáři. Pokud máte více projektů ve stejném adresáři, NuGet podporuje konkrétní zámek souboru projektu `packages.<project_name>.lock.json` |
