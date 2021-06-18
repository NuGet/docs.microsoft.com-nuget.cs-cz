---
title: Formát NuGet PackageReference (odkazy na balíčky v souborech projektu)
description: Podrobnosti o NuGet PackageReference v souborech projektu, které podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c7b963352e0e9640844a213767a58c883ed0eeb9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323710"
---
# <a name="package-references-packagereference-in-project-files"></a>Odkazy na balíčky ( `PackageReference` ) v souborech projektu

Odkazy na balíčky, použití `PackageReference` uzlu, Správa závislostí NuGet přímo v souborech projektu (na rozdíl od samostatného `packages.config` souboru). Použití PackageReference, jak je voláno, nemá vliv na jiné aspekty NuGet; například nastavení v `NuGet.Config` souborech (včetně zdrojů balíčků) jsou stále aplikována, jak je vysvětleno v tématu [běžné konfigurace NuGet](configuring-nuget-behavior.md).

Pomocí PackageReference můžete také použít podmínky nástroje MSBuild pro výběr odkazů na balíčky na cílové rozhraní nebo jiná seskupení. Umožňuje také jemně odstupňovanou kontrolu nad závislostmi a tokem obsahu. (Další podrobnosti najdete v tématu Další informace o [sadě NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Podpora typu projektu

Ve výchozím nastavení se PackageReference používá pro projekty .NET Core, .NET Standard projekty a projekty UWP cílené na Windows 10 Build 15063 (Creators Update) a novější, s výjimkou projektů v jazyce C++ UWP. Projekty .NET Framework podporují PackageReference, ale aktuálně mají výchozí hodnotu `packages.config` . Chcete-li použít PackageReference, [migrujte](../consume-packages/migrate-packages-config-to-package-reference.md) závislosti z nástroje `packages.config` do souboru projektu a pak odeberte packages.config.

ASP.NET aplikace, které cílí na úplné .NET Framework, zahrnují jenom [omezené podpory](https://github.com/NuGet/Home/issues/5877) pro PackageReference. Typy projektů C++ a JavaScript nejsou podporovány.

## <a name="adding-a-packagereference"></a>Přidání PackageReference

Přidejte závislost do souboru projektu pomocí následující syntaxe:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Řízení verze závislosti

Konvence pro určení verze balíčku je stejná jako při použití `packages.config` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

V příkladu výše 3.6.0 označuje všechny verze, které jsou >= 3.6.0 s upřednostněním pro nejnižší verzi, jak je popsáno v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Použití PackageReference pro projekt bez PackageReferences

Upřesnit: Pokud nemáte v projektu nainstalované žádné balíčky (žádné PackageReferences v souboru projektu a žádný soubor packages.config), ale chcete, aby se projekt obnovil jako PackageReferenceový styl, můžete v souboru projektu nastavit RestoreProjectStyle vlastností projektu na PackageReference.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

To může být užitečné, pokud odkazujete na projekty, které jsou PackageReference styly (existující projekty csproj nebo sady SDK). Tím umožníte, aby balíčky, na které tyto projekty odkazují, byly "transitně" odkazovány vaším projektem.

## <a name="packagereference-and-sources"></a>PackageReference a zdroje

V projektech PackageReference se v době obnovení vyřeší verze přenosných závislostí. V takovém případě musí být v projektech PackageReference k dispozici všechny zdroje pro všechna obnovení. 

## <a name="floating-versions"></a>Plovoucí verze

[Plovoucí verze](../concepts/dependency-resolution.md#floating-versions) jsou podporované pomocí `PackageReference` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Řízení prostředků závislosti

Je možné, že použijete závislost čistě jako ve vývojovém prostředí a nechcete ji vystavit pro projekty, které budou spotřebovávat váš balíček. V tomto scénáři můžete `PrivateAssets` k řízení tohoto chování použít metadata.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Následující Tagy metadat řídí prostředky závislostí:

| Značka | Description | Výchozí hodnota |
| --- | --- | --- |
| IncludeAssets | Tyto prostředky budou spotřebovány. | Vše |
| ExcludeAssets | Tyto prostředky nebudou spotřebovány. | žádné |
| PrivateAssets | Tyto prostředky budou spotřebovány, ale nebudou se přesměrovat do nadřazeného projektu. | contentFiles; analyzátory; sestavit |

Přípustné hodnoty pro tyto značky jsou následující, s více hodnotami oddělenými středníkem s výjimkou `all` a, `none` které se musí objevit sami:

| Hodnota | Popis |
| --- | ---
| kompilovat | Obsah `lib` složky a určuje, zda je projekt kompilován proti sestavením v rámci složky |
| modul runtime | Obsah `lib` `runtimes` složky a určuje, zda budou tato sestavení zkopírována do výstupního adresáře sestavení |
| contentFiles | Obsah `contentfiles` složky |
| sestavení | `.props` a `.targets` ve `build` složce |
| buildMultitargeting | *(4,0)* `.props` a `.targets` ve `buildMultitargeting` složce pro cílení na různé architektury |
| buildTransitive | *(5.0 +)* `.props` a `.targets` ve `buildTransitive` složce pro prostředky, jejichž přenos do libovolného náročného projektu se protéká. Podívejte se na stránku [funkce](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) . |
| analyzátory | Analyzátory .NET |
| nativní | Obsah `native` složky |
| žádné | Žádná z výše uvedených verzí se nepoužívá. |
| Vše | Všechny výše uvedené (kromě `none` ) |

V následujícím příkladu je vše kromě souborů obsahu z balíčku spotřebováno projektem a vše kromě souborů obsahu a analyzátory by vedlo k nadřazenému projektu.

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

Všimněte si, že protože `build` není součástí `PrivateAssets` , cíle a props *budou* tok do nadřazeného projektu. Vezměte v úvahu například, že odkaz výše se používá v projektu, který vytváří balíček NuGet s názvem AppLogger. AppLogger může využívat cíle a props z `Contoso.Utility.UsefulStuff` , jako mohou projekty, které využívají AppLogger.

> [!NOTE]
> Když `developmentDependency` je v souboru nastavená na `true` `.nuspec` , označí balíček jako součást jedinou pro vývoj, která zabrání zahrnutí balíčku jako závislosti v jiných balíčcích. Pomocí PackageReference *(NuGet 4,8 +)* tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace. Další informace najdete v tématu [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>Přidání podmínky PackageReference

Podmínku můžete použít k určení, zda je balíček zahrnut, kde podmínky mohou používat jakoukoli proměnnou MSBuild nebo proměnnou definovanou v souboru TARGETS nebo props. V předsoučasném případě je však podporována pouze `TargetFramework` Proměnná.

Řekněme například, že cílíte `netstandard1.4` i na `net452` , ale máte závislost, která je platná pouze pro `net452` . V takovém případě nechcete, aby `netstandard1.4` projekt, který váš balíček spotřebovává, přidal tuto nepotřebnou závislost. Tomu zabráníte tak, že zadáte podmínku v následujícím `PackageReference` příkladu:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Balíček sestavený pomocí tohoto projektu zobrazí, že Newtonsoft.Jsv je součástí pouze závislosti pro `net452` cíl:

![Výsledek použití podmínky v PackageReference s VS2017](media/PackageReference-Condition.png)

Podmínky lze také použít na `ItemGroup` úrovni a budou platit pro všechny podřízené `PackageReference` prvky:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Tato funkce je k dispozici pro NuGet **5,0** nebo vyšší a pro Visual Studio 2019 **16,0** nebo vyšší.

V některých případech je žádoucí, aby odkazovaly na soubory v balíčku z cíle MSBuild.
V `packages.config` projektech založených na projektech jsou balíčky nainstalovány ve složce relativní vzhledem k souboru projektu. V PackageReference jsou však balíčky [spotřebovány](../concepts/package-installation-process.md) ze složky *Global-Packages* , která se může lišit v závislosti na počítači.

Za účelem přemostění NuGet představila vlastnost, která odkazuje na umístění, ze kterého se balíček spotřebuje.

Příklad:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Kromě toho NuGet automaticky vygeneruje vlastnosti pro balíčky obsahující složku Tools.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

Vlastnosti nástroje MSBuild a identity balíčku nemají stejná omezení, takže Identita balíčku musí být změněna na popisný název MSBuild, který je opraven slovem `Pkg` .
Chcete-li ověřit přesný název generované vlastnosti, podívejte se do vygenerovaného souboru [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) .

## <a name="packagereference-aliases"></a>PackageReference aliasy

V některých vzácných instancích budou různé balíčky obsahovat třídy ve stejném oboru názvů. Počínaje verzí NuGet 5,7 & Visual Studio 2019 Update 7, který je ekvivalentní s ProjectReference, PackageReference podporuje [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .
Ve výchozím nastavení nejsou k dispozici žádné aliasy. Když je zadán alias, *všechna* sestavení pocházející z balíčku s poznámkami musí být odkazována aliasem.

Můžete se podívat na ukázkové použití na [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)

V souboru projektu zadejte aliasy následujícím způsobem:

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

a v kódu ho použijte následujícím způsobem:

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a>Upozornění a chyby NuGetu

*Tato funkce je dostupná pro NuGet **4.3** nebo vyšší a s Visual Studio 2017 **15.3** nebo vyšší.*

V mnoha scénářích balíčků a obnovení se všechna upozornění a chyby NuGet kódují a začínají na `NU****` . Všechna upozornění a chyby NuGetu jsou uvedená v [referenční](../reference/errors-and-warnings.md) dokumentaci.

NuGet pozoruje následující vlastnosti upozornění:

- `TreatWarningsAsErrors`– zachází se všemi upozorněními jako s chybami
- `WarningsAsErrors`– zacházení s konkrétními upozorněními jako s chybami
- `NoWarn`– skryje konkrétní upozornění, ať už celého projektu, nebo celého balíčku.

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

### <a name="suppressing-nuget-warnings"></a>Potlačení upozornění NuGetu

Přestože se doporučuje vyřešit všechna upozornění NuGetu během operací balíčku a obnovení, v určitých situacích je jejich potlačení zaručuje.
Pokud chcete potlačit projekt upozornění v celém projektu, zvažte následující:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Někdy se upozornění vztahují pouze na určitý balíček v grafu. Můžeme se rozhodnout toto upozornění potlačit selektivně tak, že do `NoWarn` položky PackageReference přidáme . 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Potlačení upozornění balíčku NuGet v Visual Studio

V Visual Studio můžete také potlačit [upozornění prostřednictvím](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) integrovaného vývojového prostředí.

## <a name="locking-dependencies"></a>Zamykání závislostí

*Tato funkce je dostupná pro NuGet **4.9** nebo vyšší a s Visual Studio 2017 **15.9** nebo vyšší.*

Vstup pro obnovení NuGetu je sada odkazů na balíčky ze souboru projektu (hlavní úroveň nebo přímé závislosti) a výstupem je úplné uzavření všech závislostí balíčku, včetně tranzitivních závislostí. NuGet se pokusí vždy vytvořit stejné úplné uzavření závislostí balíčku, pokud se vstupní seznam PackageReference nezměnil. Existují však některé scénáře, kdy to nemůže udělat. Příklad:

* Při použití plovoucích verzí, jako je `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` . I když se zde záměrem při každém obnovení balíčků vrátit na nejnovější verzi, existují scénáře, kdy uživatelé vyžadují, aby byl graf uzamčený na určitou nejnovější verzi, a s plovoucí desetinnou čárkou na novější verzi, pokud je k dispozici, při explicitním gestu.
* Publikovaná je novější verze balíčku, která odpovídá požadavkům na verzi PackageReference. Například 

  * Den 1: Pokud jste zadali , ale verze dostupné v úložištích NuGet byly `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` 4.1.0, 4.2.0 a 4.3.0. V tomto případě by se NuGet vyřešil na verzi 4.1.0 (nejbližší minimální verze).

  * 2. den: Publikovaná verze 4.0.0. NuGet teď najde přesnou shodu a začne se překládání na verzi 4.0.0.

* Z úložiště se odebere given package version (verze balíčku). Přestože nuget.org odstranění balíčků nepovoluje, ne všechna úložiště balíčků mají tato omezení. Výsledkem je, že NuGet najde nejlepší shodu, když se nemůže přeložit na odstraněnou verzi.

### <a name="enabling-lock-file"></a>Povolení souboru zámku

Pokud chcete zachovat úplné uzavření závislostí balíčků, můžete se přihlásit k funkci souboru zámku nastavením vlastnosti MSBuild `RestorePackagesWithLockFile` pro váš projekt:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Pokud je tato vlastnost nastavená, obnovení NuGet vygeneruje soubor zámku – soubor v kořenovém adresáři projektu se `packages.lock.json` seznamem všech závislostí balíčku. 

> [!Note]
> Jakmile projekt obsahuje soubor v kořenovém adresáři, soubor zámku se vždy používá s obnovením, i když `packages.lock.json` vlastnost `RestorePackagesWithLockFile` není nastavená. Dalším způsobem, jak se k této funkci přihlásit, je vytvořit fiktivní prázdný soubor v kořenovém adresáři `packages.lock.json` projektu.

### <a name="restore-behavior-with-lock-file"></a>`restore` chování se zamykacím souborem
Pokud je pro projekt k dispozici soubor zámku, NuGet použije tento soubor zámku ke spuštění `restore` . NuGet rychle zkontroluje, jestli v závislostech balíčků došlo k žádným změnám, jak je uvedeno v souboru projektu (nebo v souborech závislých projektů), a pokud k žádným změnám došlo, pouze obnoví balíčky uvedené v souboru zámku. Neexistuje žádné opětovné vyhodnocení závislostí balíčků.

Pokud NuGet zjistí změnu v definovaných závislostech, jak je uvedeno v souborech projektu, znovu vyhodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nový uzavření balíčku pro projekt.

V případě CI/CD a dalších scénářů, kdy nechcete měnit závislosti balíčku za běhu, můžete to provést nastavením `lockedmode` na `true` :

Pokud dotnet.exe, spusťte:

```
> dotnet.exe restore --locked-mode
```

Pokud msbuild.exe, spusťte:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Tuto podmíněnou vlastnost MSBuild můžete nastavit také v souboru projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Pokud je uzamčený režim , obnovení buď obnoví přesné balíčky uvedené v souboru zámku, nebo selže, pokud jste po vytvoření souboru zámku aktualizovali definované `true` závislosti balíčku pro projekt.

### <a name="make-lock-file-part-of-your-source-repository"></a>Zmknutí souboru jako součásti zdrojového úložiště
Pokud aplikaci tvoříte, spustitelný soubor a na začátku řetězu závislostí se nachází sporý projekt, zkontrolujte soubor zámku v úložišti zdrojového kódu, aby ho NuGet mohl využít během obnovení.

Pokud je ale váš projekt projekt knihovny, který dodáte, nebo společný  projekt kódu, na kterém závisí jiné projekty, neměli byste se v rámci zdrojového kódu účastnit souboru zámku. Zachování souboru zámku není škodou, ale během obnovování/sestavování projektu, který závisí na tomto projektu společného kódu, se nemusí použít závislosti uzamčeného balíčku pro společný projekt kódu, jak je uvedeno v souboru zámku.

Např.

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Pokud má závislost na verzi a také odkazuje na verzi , pak soubor zámku pro zobrazí závislost `ProjectA` `PackageX` na verzi `2.0.0` `ProjectB` `PackageX` `1.0.0` `ProjectB` `PackageX` `1.0.0` . Pokud je však sestaven, bude jeho soubor zámku obsahovat závislost na verzi, a ne tak, jak je uvedeno v `ProjectA` `PackageX` souboru zámku pro **`2.0.0`**  `1.0.0` `ProjectB` . Proto má soubor zámků společného projektu kódu nad balíčky vyřešené pro projekty, které na tomto projektu závisejí, jen malé říci.

### <a name="lock-file-extensibility"></a>Rozšiřitelnost souboru zámků

Pomocí souboru zámku můžete řídit různé chování obnovení, jak je popsáno níže:

| NuGet.exe možnosti | možnost dotnet | Ekvivalentní možnost nástroje MSBuild | Description |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Vyjádí výslovný souhlas s použitím souboru zámku. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Povolí uzamčený režim obnovení. To je užitečné ve scénářích CI/CD, kde chcete opakovatelná sestavení.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Tato možnost je užitečná u balíčků s plovoucí verzí definovanou v projektu. Obnovení NuGet ve výchozím nastavení při každém obnovení automaticky aktualizuje verzi balíčku, pokud s touto možností nespouštěte obnovení. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Definuje vlastní umístění souboru zámku pro projekt. NuGet ve výchozím nastavení podporuje `packages.lock.json` v kořenovém adresáři. Pokud máte ve stejném adresáři více projektů, NuGet podporuje soubor zámku specifický pro projekt. `packages.<project_name>.lock.json` |

## <a name="assettargetfallback"></a>AssetTargetFallback

Vlastnost umožňuje zadat další kompatibilní verze architektury pro projekty, na které projekt odkazuje, a balíčky `AssetTargetFallback` NuGet, které váš projekt využívá.

Pokud pomocí příkazu zadáte závislost balíčku, ale tento balíček neobsahuje prostředky, které jsou kompatibilní s cílovou architekturou vašich projektů, vlastnost `PackageReference` se pro vás `AssetTargetFallback` hraje. Kompatibilita odkazovaného balíčku se znovu prověří pomocí každé cílové architektury, která je zadaná v `AssetTargetFallback` .
Pokud se na objekt nebo odkazuje prostřednictvím , bude vyvoláno upozornění `project` `package` `AssetTargetFallback` [NU1701.](../reference/errors-and-warnings/NU1701.md)

Příklady ovlivnění kompatibility najdete `AssetTargetFallback` v následující tabulce.

| Rozhraní projektu | AssetTargetFallback | Architektury balíčků | Výsledek |
|-------------------|---------------------|--------------------|--------|
|  .NET Framework 4.7.2 | | .NET Standard 2.0 | .NET Standard 2.0 |
| Aplikace .NET Core 3.1 | | .NET Standard 2.0, .NET Framework 4.7.2 | .NET Standard 2.0 |
| Aplikace .NET Core 3.1 | |  .NET Framework 4.7.2 | Nekompatibilní, selhání s [`NU1202`](../reference/errors-and-warnings/NU1202.md) |
| Aplikace .NET Core 3.1 | net472, net471 |  .NET Framework 4.7.2 | .NET Framework 4.7.2 s [`NU1701`](../reference/errors-and-warnings/NU1701.md) |

Pomocí lze zadat více architektur `;` jako oddělovač. Pokud chcete přidat záložní rozhraní, můžete provést následující akce:

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

Pokud chcete přepsat místo přidávání k existujícím hodnotám, můžete toto nastavení `$(AssetTargetFallback)` `AssetTargetFallback` ponechat vypnuté.

> [!NOTE]
> Pokud používáte projekt založený [na sadě .NET SDK,](/dotnet/core/sdk)jsou nakonfigurované odpovídající hodnoty a není nutné je `$(AssetTargetFallback)` nastavovat ručně.
>
> `$(PackageTargetFallback)` byla dřívější funkce, která se pokusila tuto výzvu řešit, ale v podstatě je porušená a *neměla* by se používat. Pokud chcete `$(PackageTargetFallback)` migrovat z `$(AssetTargetFallback)` na , stačí změnit název vlastnosti.
