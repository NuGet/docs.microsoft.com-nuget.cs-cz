---
title: Formát NuGet PackageReference (odkazy na balíček v souborech projektu)
description: Podrobnosti o NuGet PackageReference v projektových souborech podporovaných NuGet 4.0+ a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428868"
---
# <a name="package-references-packagereference-in-project-files"></a>Odkazy na balíčky (PackageReference) v souborech projektu

Odkazy na balíčky `PackageReference` pomocí uzlu spravují závislosti NuGet přímo v rámci `packages.config` souborů projektu (na rozdíl od samostatného souboru). Použití PackageReference, jak se nazývá, nemá vliv na jiné aspekty NuGet; například nastavení `NuGet.config` v souborech (včetně zdrojů balíčků) jsou stále použita, jak je vysvětleno v [běžných konfiguracích NuGet](configuring-nuget-behavior.md).

S PackageReference, můžete také použít MSBuild podmínky zvolit odkazy na balíček na cílové rozhraní nebo jiné seskupení. Umožňuje také jemně odstupňovanou kontrolu nad závislostmi a tok obsahu. (Další podrobnosti naleznete [v balíčku NuGet pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Podpora typu projektu

Ve výchozím nastavení packagereference se používá pro projekty .NET Core, .NET Standard projekty a UPW projekty zaměřené na Windows 10 Sestavení 15063 (Creators Update) a novější, s výjimkou projektů C++ UpWP. Projekty rozhraní .NET Framework podporují odkaz `packages.config`packagereference, ale aktuálně je ve výchozím nastavení . Chcete-li použít PackageReference, `packages.config` [migrujte](../consume-packages/migrate-packages-config-to-package-reference.md) závislosti z do souboru projektu a odeberte soubor packages.config.

ASP.NET aplikace, které cílí na úplnou architekturu .NET Framework, zahrnují pouze [omezenou podporu](https://github.com/NuGet/Home/issues/5877) pro PackageReference. Typy projektů jazyka C++ a JavaScript nejsou podporovány.

## <a name="adding-a-packagereference"></a>Přidání odkazu na balíček

Přidejte závislost do souboru projektu pomocí následující syntaxe:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Řízení verze závislostí

Konvence pro určení verze balíčku je stejná jako `packages.config`při použití :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Ve výše uvedeném příkladu 3.6.0 znamená libovolnou verzi, která je >=3.6.0 s předvolbou pro nejnižší verzi, jak je popsáno v [package versioning](../concepts/package-versioning.md#version-ranges).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Použití Odkazu packagereference pro projekt bez odkazů na balíček

Upřesnit: Pokud nemáte v projektu nainstalovány žádné balíčky (žádné odkazy na balíčky v souboru projektu a žádný soubor packages.config), ale chcete projekt obnovit jako styl PackageReference, můžete v souboru projektu nastavit vlastnost projektu RestoreProjectStyle na PackageReference.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

To může být užitečné, pokud odkazujete na projekty, které jsou stylem PackageReference (existující projekty ve stylu csproj nebo SDK). To umožní balíčky, které tyto projekty odkazují, které mají být "tranzively" odkazuje váš projekt.

## <a name="packagereference-and-sources"></a>PackageReference a zdroje

V projektech PackageReference jsou v době obnovení vyřešeny přenosité verze závislostí. Jako takové v PackageReference projekty všechny zdroje musí být k dispozici pro všechny obnoví. 

## <a name="floating-versions"></a>Plovoucí verze

[Plovoucí verze](../concepts/dependency-resolution.md#floating-versions) jsou `PackageReference`podporovány s :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Řízení prostředků závislostí

Závislost můžete používat čistě jako vývojový svazek a možná nebudete chtít vystavit, že projekty, které budou využívat váš balíček. V tomto scénáři můžete `PrivateAssets` použít metadata k řízení tohoto chování.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Následující značky metadat řídí prostředky závislostí:

| Značka | Popis | Výchozí hodnota |
| --- | --- | --- |
| Zahrnout datové zdroje | Tato aktiva budou spotřebována | Vše |
| Vyloučit majetek | Tato aktiva nebudou spotřebována | Žádná |
| PrivateAssets | Tyto prostředky budou spotřebovány, ale nebudou tok do nadřazeného projektu | contentfiles;analyzátory;sestavení |

Přípustné hodnoty pro tyto značky jsou následující, s více hodnotami `none` oddělenými středníkem s výjimkou a `all` které se musí objevit samy od sebe:

| Hodnota | Popis |
| --- | ---
| kompilovat | Obsah `lib` složky a určuje, zda projekt může kompilovat proti sestavení ve složce |
| modul runtime | `lib` Obsah `runtimes` a složky a určuje, zda budou tato sestavení zkopírována do výstupního adresáře sestavení. |
| contentFiles | Obsah `contentfiles` složky |
| sestavení | `.props`a `.targets` ve `build` složce |
| buildMultitargeting | *(4.0)* `.props` `.targets` a `buildMultitargeting` ve složce pro cílení napříč rámci |
| buildTransitive | *(5.0+)* `.props` `.targets` a `buildTransitive` ve složce pro prostředky, které plynule proudí do jakéhokoli náročného projektu. Podívejte se na stránku [funkcí.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) |
| Analyzátory | Analyzátory .NET |
| nativní | Obsah `native` složky |
| Žádná | Nic z výše uvedeného se nepoužívá. |
| Vše | Všechny výše uvedené `none`(kromě ) |

V následujícím příkladu by projekt spotřeboval vše kromě souborů obsahu z balíčku a vše kromě souborů obsahu a analyzátorů by tok do nadřazeného projektu.

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

Všimněte `build` si, že `PrivateAssets`vzhledem k tomu, že není součástí , cíle a rekvizity *bude* tok do nadřazeného projektu. Zvažte například, že výše uvedený odkaz se používá v projektu, který vytváří balíček NuGet s názvem AppLogger. AppLogger může spotřebovat cíle `Contoso.Utility.UsefulStuff`a rekvizity z , stejně jako projekty, které spotřebovávají AppLogger.

> [!NOTE]
> Pokud `developmentDependency` je `true` nastavena `.nuspec` na v souboru, to označí balíček jako závislost pouze pro vývoj, který zabraňuje balíček zahrnuty jako závislost v jiných balíčcích. S PackageReference *(NuGet 4.8+)* tento příznak také znamená, že vyloučí prostředky kompilace v době kompilace. Další informace naleznete v [tématu DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>Přidání podmínky PackageReference

Podmínku můžete použít k řízení, zda je součástí balíčku, kde podmínky můžete použít libovolnou proměnnou MSBuild nebo proměnnou definovanou v souboru cílů nebo rekvizit. V současné době je `TargetFramework` však podporována pouze proměnná.

Řekněme například, že `netstandard1.4` cílíte stejně jako `net452` ale máte `net452`závislost, která je použitelná pouze pro . V takovém případě nechcete, `netstandard1.4` aby projekt, který spotřebovává váš balíček, přidal tuto zbytečnou závislost. Chcete-li tomu zabránit, zadejte podmínku `PackageReference` následujícím způsobem:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Balíček postavený pomocí tohoto projektu ukáže, že Newtonsoft.Json je `net452` zahrnut jako závislost pouze pro cíl:

![Výsledek použití Condition on PackageReference s VS2017](media/PackageReference-Condition.png)

Podmínky mohou být také `ItemGroup` použity na úrovni `PackageReference` a budou se vztahovat na všechny podřízené prvky:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Tato funkce je k dispozici s NuGet **5.0** nebo vyšší a s Visual Studio 2019 **16.0** nebo vyšší.

Někdy je žádoucí odkazovat na soubory v balíčku z cíle MSBuild.
V `packages.config` projektech založených na balíčcích jsou balíčky nainstalovány ve složce vzhledem k souboru projektu. Vbalíčcích Však v PackageReference balíčky jsou [spotřebovány](../concepts/package-installation-process.md) ze složky *globální balíčky,* které se mohou lišit od počítače k počítači.

Chcete-li překlenout tuto mezeru, NuGet představil vlastnost, která odkazuje na umístění, ze kterého bude balíček spotřebována.

Příklad:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Navíc NuGet bude automaticky generovat vlastnosti pro balíčky obsahující složky nástrojů.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

Vlastnosti MSBuild a identity balíčků nemají stejná omezení, takže identitu balíčku je třeba změnit na `Pkg`popisný název MSBuild, předponou slovem .
Chcete-li ověřit přesný název generované vlastnosti, podívejte se na generovaný soubor [nuget.g.props.](../reference/msbuild-targets.md#restore-outputs)

## <a name="nuget-warnings-and-errors"></a>Upozornění a chyby NuGet

*Tato funkce je k dispozici s NuGet **4.3** nebo vyšší a s Visual Studio 2017 **15.3** nebo vyšší.*

Pro mnoho scénářů pack a obnovení všechna upozornění nuget `NU****`a chyby jsou kódovány a začínat . Všechna upozornění a chyby NuGet jsou uvedeny v [referenční](../reference/errors-and-warnings.md) dokumentaci.

NuGet dodržuje následující vlastnosti upozornění:

- `TreatWarningsAsErrors`, považovat všechna varování za chyby
- `WarningsAsErrors`, považovat konkrétní varování za chyby
- `NoWarn`, skryjte konkrétní varování, ať už v rámci celého projektu, nebo v rámci celého balíčku.

Příklady:

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>Potlačení upozornění NuGet

Zatímco je doporučeno vyřešit všechna upozornění NuGet během operace balení a obnovení, v určitých situacích jejich potlačení je oprávněné.
Chcete-li potlačit celý projekt upozornění, zvažte provedení:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Někdy se upozornění vztahují pouze na určitý balíček v grafu. Můžeme se rozhodnout potlačit toto upozornění `NoWarn` selektivně přidáním položky PackageReference. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Potlačení upozornění balíčku NuGet v sadě Visual Studio

Když v sadě Visual Studio, můžete také [potlačit upozornění](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) prostřednictvím ide.

## <a name="locking-dependencies"></a>Zamykání závislostí

*Tato funkce je k dispozici s NuGet **4.9** nebo vyšší a s Visual Studio 2017 **15.9** nebo vyšší.*

Vstup do NuGet obnovení je sada odkazů na balíček ze souboru projektu (nejvyšší úrovně nebo přímé závislosti) a výstup je úplné uzavření všech závislostí balíčku, včetně přenositých závislostí. NuGet se pokusí vždy vytvořit stejné úplné uzavření závislostí balíčku, pokud se nezměnil vstupní seznam PackageReference. Existují však některé scénáře, kde není schopen tak učinit. Příklad:

* Při použití plovoucí verze `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`jako . Zatímco záměrem je zde plovoucí na nejnovější verzi na každé obnovení balíčků, existují scénáře, kde uživatelé vyžadují, aby graf být uzamčen na určitou nejnovější verzi a plovoucí na novější verzi, pokud je k dispozici, na explicitní gesto.
* Je publikována novější verze balíčku odpovídajícího požadavkům na verzi PackageReference. Například 

  * Den 1: Pokud `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` jste zadali, ale verze dostupné v úložištích NuGet byly 4.1.0, 4.2.0 a 4.3.0. V tomto případě by NuGet vyřešeny na 4.1.0 (nejbližší minimální verze)

  * Den 2: Verze 4.0.0 dostane zveřejněny. NuGet nyní najde přesnou shodu a začne řešit na 4.0.0

* Daná verze balíčku je odebrána z úložiště. Přestože nuget.org neumožňuje odstranění balíčků, ne všechny úložiště balíčků mají tato omezení. To má za následek NuGet hledání nejlepší shody, když nelze přeložit na odstraněnou verzi.

### <a name="enabling-lock-file"></a>Povolení souboru zámku

Chcete-li zachovat úplné uzavření závislostí balíčků, můžete se přihlásit k funkci uzamčení souboru nastavením vlastnosti `RestorePackagesWithLockFile` MSBuild pro váš projekt:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Pokud je tato vlastnost nastavena, Obnovení NuGet vygeneruje soubor zámku - `packages.lock.json` soubor v kořenovém adresáři projektu, který obsahuje seznam všech závislostí balíčku. 

> [!Note]
> Jakmile má `packages.lock.json` projekt soubor v kořenovém adresáři, soubor zámku `RestorePackagesWithLockFile` se vždy používá s obnovením i v případě, že vlastnost není nastavena. Takže další způsob, jak se přihlásit k této `packages.lock.json` funkci, je vytvořit fiktivní prázdný soubor v kořenovém adresáři projektu.

### <a name="restore-behavior-with-lock-file"></a>`restore`chování se souborem zámku
Pokud je pro projekt k dispozici soubor zámku, `restore`použije nuget tento soubor zámku ke spuštění . NuGet provádí rychlou kontrolu, zda došlo k nějaké změny v závislostech balíčku, jak je uvedeno v souboru projektu (nebo soubory závislé projekty) a pokud nedošlo k žádné změny pouze obnoví balíčky uvedené v souboru zámku. Neexistuje žádné přehodnocení závislostí balíčků.

Pokud NuGet zjistí změnu definovaných závislostí, jak je uvedeno v souboru projektu, přehodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nové uzavření balíčku pro projekt.

Pro CI/CD a další scénáře, kde byste nechtěli měnit závislosti balíčků za běhu, `lockedmode` `true`můžete tak učinit nastavením na :

Pro dotnet.exe spusťte:

```
> dotnet.exe restore --locked-mode
```

Pro msbuild.exe spusťte:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Tuto podmíněnou vlastnost MSBuild můžete také nastavit v souboru projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Pokud je `true`uzamčen režim , obnovení buď obnoví přesné balíčky, jak jsou uvedeny v souboru zámku, nebo se nezdaří, pokud jste aktualizovali definované závislosti balíčků pro projekt po vytvoření souboru zámku.

### <a name="make-lock-file-part-of-your-source-repository"></a>Nastavení souboru zámku do zdrojového úložiště
Pokud vytváříte aplikaci, spustitelný soubor a dotyčný projekt je na začátku řetězce závislostí, pak zkontrolujte soubor zámku do úložiště zdrojového kódu, aby jej NuGet mohl využít během obnovení.

Pokud je však projekt projekt knihovny, který nedodáváte, nebo projekt společného kódu, na kterém závisí jiné projekty, **neměli** byste zamykat soubor jako součást zdrojového kódu. Neexistuje žádná náhrada zachycování souboru zámku, ale uzamčený balíček závislostí pro společný kód projektu nemusí být použity, jak je uvedeno v souboru zámku, během obnovení nebo sestavení projektu, který závisí na tomto projektu společného kódu.

Např.

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Pokud `ProjectA` má závislost na `PackageX` `2.0.0` verzi a `ProjectB` také odkazy, `1.0.0`které závisí na `ProjectB` `PackageX` verzi , pak `PackageX` `1.0.0`soubor zámku pro bude seznam závislost na verzi . Však `ProjectA` při vytvoření, jeho zámek soubor bude `PackageX` **`2.0.0`** obsahovat závislost na verzi `ProjectB`a **není** `1.0.0` uvedeno v souboru zámku pro . Proto zámek soubor uspolečného projektu kódu má málo co říci nad balíčky vyřešen pro projekty, které jsou na něm závislé.

### <a name="lock-file-extensibility"></a>Rozšiřitelnost souboru zamykat

Můžete řídit různé chování obnovení pomocí souboru zámku, jak je popsáno níže:

| NuGet.exe, volba | dotnet, volba | Ekvivalentní možnost MSBuild | Popis |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | ObnovitPackagesWithLockFile | Přihlásí se k použití souboru zámku. |
| `-LockedMode` | `--locked-mode` | Obnovit uzamčený režim | Povolí uzamčený režim pro obnovení. To je užitečné ve scénářích CI/CD, kde chcete opakovatelné sestavení.|   
| `-ForceEvaluate` | `--force-evaluate` | ObnovitVyhodnocení síly | Tato možnost je užitečná u balíčků s plovoucí verzí definovanou v projektu. Ve výchozím nastavení NuGet obnovení nebude aktualizovat verzi balíčku automaticky při každém obnovení, pokud spustíte obnovení s touto možností. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Definuje vlastní umístění souboru zámku pro projekt. Ve výchozím nastavení `packages.lock.json` podporuje NuGet v kořenovém adresáři. Pokud máte více projektů ve stejném adresáři, NuGet podporuje soubor uzamčení specifické pro projekt`packages.<project_name>.lock.json` |
