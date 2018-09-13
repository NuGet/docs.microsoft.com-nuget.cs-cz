---
title: Formát NuGet PackageReference (odkazy na balíček v souborech projektu)
description: Podrobnosti na NuGet PackageReference v souborech projektu podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 648b2679538e38b2451d7857beb5d070deeef7c5
ms.sourcegitcommit: 47858da1103848cc1b15bdc00ac7219c0ee4a6a0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/12/2018
ms.locfileid: "44516201"
---
# <a name="package-references-packagereference-in-project-files"></a>Odkazy na balíček (PackageReference) v souborech projektu

Balíček odkazů pomocí nástroje `PackageReference` uzlu, správě závislostí NuGet přímo v rámci projektových souborů (na rozdíl od samostatné `packages.config` souboru). Pomocí PackageReference, jako je volána, nemá vliv na ostatní aspekty NuGet; například nastavení v `NuGet.Config` soubory (včetně zdroje balíčků) se uplatní, jak je vysvětleno v [konfigurace chování Nugetu](configuring-nuget-behavior.md).

S PackageReference můžete také použít podmínky nástroje MSBuild zvolit odkazy na balíček na cílovou architekturu, konfigurace, platformy nebo další seskupení. Umožňuje také pro detailní kontrolu nad závislostí a obsahu toku. (Další podrobnosti najdete v [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md).)

Ve výchozím nastavení je použít PackageReference pro projekty .NET Core, .NET Standard projekty a projekty UPW cílení na Windows 10 sestavení 15063 (Creators Update) a novější, s výjimkou projekty C++ UWP. Projekty rozhraní .NET framework podporují PackageReference, ale nyní jako výchozí `packages.config`. Použití PackageReference migrovat závislosti z `packages.config` do souboru projektu, odstraňte soubor packages.config.

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
Pokročilé: Pokud jste žádné balíčky nainstalované v projektu (žádné PackageReferences v souboru projektu) a žádný soubor packages.config, ale chcete projekt tak, aby se obnovit jako PackageReference styl, můžete nastavit vlastnost RestoreProjectStyle projektu na PackageReference v váš soubor projektu.
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

| Hodnota | Popis |
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
