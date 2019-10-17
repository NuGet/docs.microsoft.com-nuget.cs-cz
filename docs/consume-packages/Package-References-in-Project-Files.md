---
title: Formát NuGet PackageReference (odkazy na balíčky v souborech projektu)
description: Podrobnosti o NuGet PackageReference v souborech projektu, které podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 892483760a9f3568da7101663e93c69ce3d70b96
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510813"
---
# <a name="package-references-packagereference-in-project-files"></a>Odkazy na balíčky (PackageReference) v souborech projektu

Odkazy na balíčky, pomocí uzlu `PackageReference`, spravují závislosti NuGet přímo v souborech projektu (na rozdíl od samostatného souboru `packages.config`). Použití PackageReference, jak je voláno, nemá vliv na jiné aspekty NuGet; například nastavení v souborech `NuGet.config` (včetně zdrojů balíčků) jsou stále aplikována, jak je vysvětleno v tématu [běžné konfigurace NuGet](configuring-nuget-behavior.md).

Pomocí PackageReference můžete také použít podmínky nástroje MSBuild k výběru odkazů na balíčky v rámci cílové architektury, konfigurace, platformy nebo dalších seskupení. Umožňuje také jemně odstupňovanou kontrolu nad závislostmi a tokem obsahu. (Další podrobnosti najdete v tématu Další informace o [sadě NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Podpora typu projektu

Ve výchozím nastavení se PackageReference používá pro projekty .NET Core, .NET Standard projekty a projekty UWP cílené na Windows 10 Build 15063 (Creators Update) a novější, s výjimkou C++ projektů UWP. Projekty .NET Framework podporují PackageReference, ale v současné době se ve výchozím nastavení `packages.config`. Chcete-li použít PackageReference, [migrujte](../consume-packages/migrate-packages-config-to-package-reference.md) závislosti z `packages.config` do souboru projektu a pak odeberte soubor Packages. config.

ASP.NET aplikace, které cílí na úplné .NET Framework, zahrnují jenom [omezené podpory](https://github.com/NuGet/Home/issues/5877) pro PackageReference. C++a typy projektů JavaScriptu nejsou podporovány.

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

Konvence určení verze balíčku je stejná jako při použití `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

V příkladu výše 3.6.0 označuje všechny verze, které jsou > = 3.6.0 s upřednostněním pro nejnižší verzi, jak je popsáno v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Použití PackageReference pro projekt bez PackageReferences
Upřesnit: Pokud nemáte v projektu nainstalované žádné balíčky (žádné PackageReferences v souboru projektu a žádný soubor Packages. config), ale chcete, aby se projekt obnovil jako PackageReferenceový styl, můžete nastavit RestoreProjectStyle vlastností projektu na PackageReference. soubor projektu.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
To může být užitečné, pokud odkazujete na projekty, které jsou PackageReference styly (existující projekty csproj nebo sady SDK). Tím umožníte, aby balíčky, na které tyto projekty odkazují, byly "transitně" odkazovány vaším projektem.

## <a name="floating-versions"></a>Plovoucí verze

V `PackageReference` jsou podporovány [plovoucí verze](../concepts/dependency-resolution.md#floating-versions) :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Řízení prostředků závislosti

Je možné, že použijete závislost čistě jako ve vývojovém prostředí a nechcete ji vystavit pro projekty, které budou spotřebovávat váš balíček. V tomto scénáři můžete k řízení tohoto chování použít metadata `PrivateAssets`.

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

| Inteligentní | Popis | Výchozí hodnota |
| --- | --- | --- |
| IncludeAssets | Tyto prostředky budou spotřebovány. | všechny |
| ExcludeAssets | Tyto prostředky nebudou spotřebovány. | žádná |
| PrivateAssets | Tyto prostředky budou spotřebovány, ale nebudou se přesměrovat do nadřazeného projektu. | contentFiles; analyzátory; sestavit |

Přípustné hodnoty pro tyto značky jsou následující, s více hodnotami oddělenými středníkem s výjimkou `all` a `none`, které se musí objevit sami:

| Hodnota | Popis |
| --- | ---
| Sestavení | Obsah složky `lib` a řídí, zda je projekt kompilován proti sestavením v rámci složky |
| modul runtime | Obsah složky `lib` a `runtimes` a určuje, zda budou tato sestavení zkopírována do výstupního adresáře sestavení |
| contentFiles | Obsah složky `contentfiles` |
| sestavení | `.props` a `.targets` ve složce `build` |
| buildMultitargeting | *(4,0)* `.props` a `.targets` ve složce `buildMultitargeting` pro cílení na různé architektury |
| buildTransitive | *(5.0 +)* `.props` a `.targets` ve složce `buildTransitive` pro prostředky, jejichž přenos do libovolného náročného projektu se protéká. Podívejte se na stránku [funkce](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) . |
| analyzátory | Analyzátory .NET |
| nativní | Obsah složky `native` |
| žádná | Žádná z výše uvedených verzí se nepoužívá. |
| všechny | Všechny výše uvedené (kromě `none`) |

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

Všimněte si, že protože `build` není součástí `PrivateAssets`, cíle a props *budou* předávány do nadřazeného projektu. Vezměte v úvahu například, že odkaz výše se používá v projektu, který vytváří balíček NuGet s názvem AppLogger. AppLogger může využívat cíle a props z `Contoso.Utility.UsefulStuff`, stejně jako mohou projekty, které využívají AppLogger.

> [!NOTE]
> Pokud je `developmentDependency` v souboru `.nuspec` nastaveno na hodnotu `true`, bude balíček označen jako součást jenom pro vývoj, což brání v zahrnutí balíčku jako závislosti v jiných balíčcích. Pomocí PackageReference *(NuGet 4,8 +)* tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace. Další informace najdete v tématu [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>Přidání podmínky PackageReference

Podmínku můžete použít k určení, zda je balíček zahrnut, kde podmínky mohou používat jakoukoli proměnnou MSBuild nebo proměnnou definovanou v souboru TARGETS nebo props. V současné době se však podporuje pouze proměnná `TargetFramework`.

Řekněme například, že cílíte `netstandard1.4` a také `net452`, ale máte závislost, která je platná pouze pro `net452`. V takovém případě nechcete, aby projekt `netstandard1.4`, který váš balíček spotřebovává, přidal tuto nepotřebnou závislost. Tomu zabráníte zadáním podmínky `PackageReference` následujícím způsobem:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Balíček sestavený pomocí tohoto projektu zobrazí, že Newtonsoft. JSON je obsažen pouze jako závislost pro cíl `net452`:

![Výsledek použití podmínky v PackageReference s VS2017](media/PackageReference-Condition.png)

Podmínky lze také použít na úrovni `ItemGroup` a budou platit pro všechny podřízené prvky `PackageReference`:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a>Uzamykání závislostí
*Tato funkce je k dispozici pro NuGet **4,9** nebo vyšší a pro Visual Studio 2017 **15,9** nebo vyšší.*

Vstup do obnovení NuGet je sada odkazů na balíčky ze souboru projektu (závislosti na nejvyšší úrovni nebo přímých závislostí) a výstup je plný uzávěr všech závislostí balíčku včetně přenosných závislostí. V případě, že se vstupní seznam PackageReference nezměnil, nástroj NuGet se pokusí vždy vydávat stejný plný uzávěr závislostí balíčku. Existují však situace, kdy to není možné. Příklad:

* Pokud používáte plovoucí verze, jako je `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. I když tady je tento záměr na nejnovější verzi v každé obnovy balíčků, existují situace, kdy uživatelé potřebují, aby byl graf uzamčený na určitou nejnovější verzi a aby byl na novější verzi, pokud je k dispozici, po explicitním gestu.
* Je publikovaná novější verze balíčku, která odpovídá požadavkům verze PackageReference. Například. 

  * Den 1: Pokud jste zadali `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, ale verze dostupné v úložištích NuGet byly 4.1.0, 4.2.0 a 4.3.0. V tomto případě se NuGet přeložil na 4.1.0 (nejbližší minimální verzi).

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

Pokud je tato vlastnost nastavená, obnovení NuGet vygeneruje soubor zámku File-`packages.lock.json` v kořenovém adresáři projektu, který obsahuje seznam všech závislostí balíčku. 

> [!Note]
> Jakmile má projekt `packages.lock.json` v kořenovém adresáři, soubor zámku se vždy používá s obnovením i v případě, že vlastnost `RestorePackagesWithLockFile` není nastavena. Další možností, jak se vyjádřit k této funkci, je vytvořit fiktivní prázdný soubor `packages.lock.json` v kořenovém adresáři projektu.

### <a name="restore-behavior-with-lock-file"></a>chování `restore` se souborem zámku
Pokud je soubor zámku k dispozici pro projekt, NuGet pomocí tohoto souboru zámku spustí `restore`. NuGet provede rychlou kontrolu, jestli se v závislostech balíčku nezměnily žádné změny, jak je uvedeno v souboru projektu (nebo v souborech závislých projektů) a jestli nedošlo k žádným změnám, jenom obnoví balíčky uvedené v souboru zámku. Nedošlo k opakovanému vyhodnocení závislostí balíčku.

Pokud NuGet detekuje změnu v definovaných závislostech, jak je uvedeno v souborech projektu, znovu vyhodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nový uzavření balíčku pro daný projekt.

V případě CI/CD a dalších scénářů, kde byste nechtěli změnit závislosti balíčku za běhu, to můžete provést nastavením `lockedmode` na `true`:

Pro příkaz dotnet. exe spusťte:
```
> dotnet.exe restore --locked-mode
```

Pro MSBuild. exe spusťte:
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

Pokud je uzamčený režim `true`, obnovení obnoví přesné balíčky uvedené v souboru zámku nebo selže, pokud jste aktualizovali definované závislosti balíčku pro projekt po vytvoření souboru zámku.

### <a name="make-lock-file-part-of-your-source-repository"></a>Nastavit zámek souboru jako součást zdrojového úložiště
Pokud vytváříte aplikaci, spustitelný soubor a příslušný projekt jsou na začátku řetězu závislostí a pak proveďte vrácení souboru se zámkem do úložiště zdrojového kódu, aby jej mohla aplikace NuGet využít při obnovení.

Pokud je však projekt knihovnou projektu, který nedodáte nebo se jedná o běžný projekt kódu, na kterém jsou závislé další projekty, **neměli byste** soubory zámku vrátit se změnami jako součást zdrojového kódu. Neexistuje žádný škodný soubor zámku, ale nelze použít uzamčené závislosti balíčku pro běžný projekt kódu, jak je uvedeno v souboru zámku během obnovení nebo sestavení projektu, který je závislý na tomto projektu Common-Code.

EG.
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
Pokud má `ProjectA` závislost na verzi `PackageX` `2.0.0` a odkazuje na `ProjectB`, která závisí na `PackageX` verzi `1.0.0`, pak soubor zámku pro `ProjectB` vypíše závislost na @no__t 7 verze `1.0.0`. Pokud je však vytvořen `ProjectA`, jeho soubor zámku bude obsahovat závislost na `PackageX` verze **`2.0.0`** a **nesmí** `1.0.0`, jak je uvedeno v souboru zámku pro `ProjectB`. Proto soubor zámku pro běžný projekt kódu trochu říká, že balíčky byly vyřešeny pro projekty, které jsou na ní závislé.

### <a name="lock-file-extensibility"></a>Zamknout rozšíření souboru

Můžete řídit různá chování při obnovení pomocí souboru zámku, jak je popsáno níže:

| Možnost | Možnost ekvivalentu MSBuild | Popis|
|:---  |:--- |:--- |
| `--use-lock-file` | RestorePackagesWithLockFile | Výslovný se na použití souboru zámku. | 
| `--locked-mode` | RestoreLockedMode | Zapne uzamčený režim pro obnovení. To je užitečné ve scénářích CI/CD, kde chcete opakovat sestavení.|   
| `--force-evaluate` | RestoreForceEvaluate | Tato možnost je užitečná pro balíčky s plovoucí verzí definovanou v projektu. Ve výchozím nastavení při obnovení NuGet nebude automaticky aktualizovat verzi balíčku pro každé obnovení, pokud u této možnosti nespustíte příkaz Restore. |
| `--lock-file-path` | NuGetLockFilePath | Definuje vlastní umístění souboru zámku pro projekt. Ve výchozím nastavení NuGet podporuje `packages.lock.json` v kořenovém adresáři. Pokud máte ve stejném adresáři více projektů, NuGet podporuje soubor zámku specifický pro projekt `packages.<project_name>.lock.json` |
