---
title: Formát NuGet PackageReference (odkazy na balíčky v souborech projektu)
description: Podrobnosti o NuGet PackageReference v souborech projektu, které podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237637"
---
# <a name="package-references-packagereference-in-project-files"></a>Odkazy na balíčky (PackageReference) v souborech projektu

Odkazy na balíčky, použití `PackageReference` uzlu, Správa závislostí NuGet přímo v souborech projektu (na rozdíl od samostatného `packages.config` souboru). Použití PackageReference, jak je voláno, nemá vliv na jiné aspekty NuGet; například nastavení v `NuGet.config` souborech (včetně zdrojů balíčků) jsou stále aplikována, jak je vysvětleno v tématu [běžné konfigurace NuGet](configuring-nuget-behavior.md).

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

| Značka | Popis | Výchozí hodnota |
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
````

Vlastnosti nástroje MSBuild a identity balíčku nemají stejná omezení, takže Identita balíčku musí být změněna na popisný název MSBuild, který je opraven slovem `Pkg` .
Chcete-li ověřit přesný název generované vlastnosti, podívejte se do vygenerovaného souboru [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) .

## <a name="nuget-warnings-and-errors"></a>Upozornění a chyby NuGet

*Tato funkce je k dispozici pro NuGet **4,3** nebo vyšší a pro Visual Studio 2017 **15,3** nebo vyšší.*

Pro mnoho scénářů sad a obnovení jsou všechna upozornění a chyby NuGet zakódované a začínají na `NU****` . Všechna upozornění a chyby NuGet jsou uvedená v [referenční](../reference/errors-and-warnings.md) dokumentaci.

NuGet sleduje následující vlastnosti upozornění:

- `TreatWarningsAsErrors`, považovat všechna upozornění za chyby
- `WarningsAsErrors`, považovat specifická upozornění za chyby
- `NoWarn`, skryjte konkrétní upozornění, ať už na úrovni projektu, nebo na úrovni balíčku.

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

I když se vám doporučuje vyřešit všechna upozornění sady NuGet během operací aktualizace a obnovení, v některých případech je jejich potlačení oprávněné.
Chcete-li potlačit projekt s upozorněním na šířku, zvažte provedení těchto akcí:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Upozornění se někdy vztahují jenom na určitý balíček v grafu. Můžeme se rozhodnout pro potlačení tohoto upozornění selektivně přidáním `NoWarn` položky na položku PackageReference. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Potlačení upozornění balíčku NuGet v aplikaci Visual Studio

Při v aplikaci Visual Studio můžete také [potlačit upozornění](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) prostřednictvím integrovaného vývojového prostředí (IDE).

## <a name="locking-dependencies"></a>Uzamykání závislostí

*Tato funkce je k dispozici pro NuGet **4,9** nebo vyšší a pro Visual Studio 2017 **15,9** nebo vyšší.*

Vstup do obnovení NuGet je sada odkazů na balíčky ze souboru projektu (závislosti na nejvyšší úrovni nebo přímých závislostí) a výstup je plný uzávěr všech závislostí balíčku včetně přenosných závislostí. V případě, že se vstupní seznam PackageReference nezměnil, nástroj NuGet se pokusí vždy vydávat stejný plný uzávěr závislostí balíčku. Existují však situace, kdy to není možné. Například:

* Při použití plovoucích verzí, jako je `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` . I když tady je tento záměr na nejnovější verzi v každé obnovy balíčků, existují situace, kdy uživatelé potřebují, aby byl graf uzamčený na určitou nejnovější verzi a aby byl na novější verzi, pokud je k dispozici, po explicitním gestu.
* Je publikovaná novější verze balíčku, která odpovídá požadavkům verze PackageReference. Například 

  * Den 1: Pokud jste zadali `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` verze, které jsou k dispozici v úložištích NuGet, byly 4.1.0, 4.2.0 a 4.3.0. V tomto případě se NuGet přeložil na 4.1.0 (nejbližší minimální verzi).

  * Den 2: verze 4.0.0 se publikuje. NuGet teď najde přesnou shodu a začne řešit na 4.0.0

* Daná verze balíčku se odebere z úložiště. I když nuget.org nepovoluje odstraňování balíčků, ne všechna úložiště balíčků mají tato omezení. Výsledkem je, že NuGet najde nejlepší shodu, když ho nelze vyřešit na odstraněnou verzi.

### <a name="enabling-lock-file"></a>Povoluje se soubor zámku.

Aby se zachoval úplný konec závislostí balíčku, můžete se přihlásit k funkci zámek souboru nastavením vlastnosti MSBuild `RestorePackagesWithLockFile` pro váš projekt:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Pokud je tato vlastnost nastavená, obnovení NuGet vygeneruje soubor zámku File `packages.lock.json` v kořenovém adresáři projektu, který obsahuje seznam všech závislostí balíčku. 

> [!Note]
> Jakmile projekt obsahuje `packages.lock.json` soubor ve svém kořenovém adresáři, soubor zámku se vždy používá s obnovením i v případě, že vlastnost není `RestorePackagesWithLockFile` nastavena. Další možností, jak se vyjádřit k této funkci, je vytvořit fiktivní prázdný `packages.lock.json` soubor v kořenovém adresáři projektu.

### <a name="restore-behavior-with-lock-file"></a>`restore` chování se souborem zámku
Pokud je soubor zámku k dispozici pro projekt, nástroj NuGet používá ke spuštění tento soubor zámku `restore` . NuGet provede rychlou kontrolu, jestli se v závislostech balíčku nezměnily žádné změny, jak je uvedeno v souboru projektu (nebo v souborech závislých projektů) a jestli nedošlo k žádným změnám, jenom obnoví balíčky uvedené v souboru zámku. Nedošlo k opakovanému vyhodnocení závislostí balíčku.

Pokud NuGet detekuje změnu v definovaných závislostech, jak je uvedeno v souborech projektu, znovu vyhodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nový uzavření balíčku pro daný projekt.

V případě CI/CD a dalších scénářů, kde byste nechtěli změnit závislosti balíčku za běhu, můžete to provést nastavením `lockedmode` na `true` :

Pro dotnet.exe spusťte:

```
> dotnet.exe restore --locked-mode
```

Pro msbuild.exe spusťte:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Tuto vlastnost podmíněného MSBuild můžete nastavit také v souboru projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Pokud je uzamčený režim `true` , obnovení obnoví buď přesné balíčky uvedené v souboru zámku, nebo selže, pokud jste aktualizovali definované závislosti balíčků pro projekt po vytvoření souboru zámku.

### <a name="make-lock-file-part-of-your-source-repository"></a>Nastavit zámek souboru jako součást zdrojového úložiště
Pokud vytváříte aplikaci, spustitelný soubor a příslušný projekt jsou na začátku řetězu závislostí a pak proveďte vrácení souboru se zámkem do úložiště zdrojového kódu, aby jej mohla aplikace NuGet využít při obnovení.

Pokud je však projekt knihovnou projektu, který nedodáte nebo se jedná o běžný projekt kódu, na kterém jsou závislé další projekty, **neměli byste** soubory zámku vrátit se změnami jako součást zdrojového kódu. Neexistuje žádný škodný soubor zámku, ale nelze použít uzamčené závislosti balíčku pro běžný projekt kódu, jak je uvedeno v souboru zámku během obnovení nebo sestavení projektu, který je závislý na tomto projektu Common-Code.

Např.

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Pokud `ProjectA` má závislost na `PackageX` verzi `2.0.0` a také odkazy `ProjectB` , které závisejí na `PackageX` verzi `1.0.0` , pak soubor zámku pro `ProjectB` bude zobrazovat závislost na `PackageX` verzi `1.0.0` . Když je však `ProjectA` sestaven, jeho soubor zámku bude obsahovat závislost na `PackageX` verzi **`2.0.0`** a **nikoli** `1.0.0` , jak je uvedeno v souboru zámku pro `ProjectB` . Proto soubor zámku pro běžný projekt kódu trochu říká, že balíčky byly vyřešeny pro projekty, které jsou na ní závislé.

### <a name="lock-file-extensibility"></a>Zamknout rozšíření souboru

Můžete řídit různá chování při obnovení pomocí souboru zámku, jak je popsáno níže:

| Možnost NuGet.exe | dotnet – možnost | Možnost ekvivalentu MSBuild | Popis |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Výslovný se na použití souboru zámku. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Zapne uzamčený režim pro obnovení. To je užitečné ve scénářích CI/CD, kde chcete opakovat sestavení.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Tato možnost je užitečná pro balíčky s plovoucí verzí definovanou v projektu. Ve výchozím nastavení při obnovení NuGet nebude automaticky aktualizovat verzi balíčku pro každé obnovení, pokud u této možnosti nespustíte příkaz Restore. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Definuje vlastní umístění souboru zámku pro projekt. Ve výchozím nastavení NuGet podporuje `packages.lock.json` v kořenovém adresáři. Pokud máte ve stejném adresáři více projektů, NuGet podporuje soubor zámku specifický pro projekt. `packages.<project_name>.lock.json` |
