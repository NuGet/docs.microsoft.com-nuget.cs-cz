---
title: "Formát NuGet PackageReference (odkazů balíčku v souborech projektu) | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Podrobnosti o NuGet PackageReference v souborech projektu podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
keywords: "Závislosti balíčků NuGet, balíček odkazuje projektu soubory, PackageReference, souboru packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 24a977f9de535559dcb0392749298ea502c3c7ce
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="package-references-packagereference-in-project-files"></a>Balíček odkazuje (PackageReference) v souborech projektu

Balíček odkazů, pomocí `PackageReference` uzlu, umožňují spravovat závislosti NuGet přímo v rámci soubory projektu, místo nutnosti samostatné `packages.config` souboru. Tato metoda neovlivňuje dalších aspektů NuGet; například nastavení v `NuGet.Config` soubory (včetně zdroje balíčků) jsou stále použít, jak je popsáno v [konfigurace chování NuGet](Configuring-NuGet-Behavior.md).

> [!Important]
> V současné době balíček odkazuje jsou podporovány ve Visual Studio 2017 pouze pro projekty .NET Core, .NET Standard projekty a UWP projektech zacílených na Windows 10 sestavení 15063 (Creators aktualizace).

`PackageReference` Přístup umožňuje používat podmínky nástroje MSBuild vybrat balíček odkazuje na cílové rozhraní, konfigurace, platformu nebo jiných seskupení. Umožňuje také pro jemně odstupňovanou kontrolu nad závislosti a obsahu toku.

Další informace o integraci s odkazů balíčku v souborech projektu nástroje MSBuild v [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md).

## <a name="adding-a-packagereference"></a>Přidání PackageReference

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

V předchozím příkladu 3.6.0 znamená všechny verze, která je > = 3.6.0 s předvolby pro nejnižší verze, jak je popsáno na [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards).

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

## <a name="controlling-dependency-assets"></a>Řízení závislostí prostředky

Může používat závislost čistě jako harness vývoj a nemusí chtějí zpřístupnit, projekty, které bude využívat vašeho balíčku. V tomto scénáři můžete použít `PrivateAssets` metadata, aby bylo toto chování.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Následující značky metadata řídit prostředky závislost:

| Značka | Popis | Výchozí hodnota |
| --- | --- | --- |
| IncludeAssets | Tyto prostředky budou využívat. | všechny |
| ExcludeAssets | Tyto prostředky nebudou využívat. | žádná |
| PrivateAssets | Tyto prostředky budou využívat, ale nebude tok nadřazený projekt | contentfiles; analyzátorů; sestavení |

Povolené hodnoty pro tyto značky jsou následující, s více hodnotami, které jsou odděleny středníkem kromě s `all` a `none` která se musí nacházet ve vlastní účet:

| Hodnota | Popis |
| --- | ---
| compile | Obsah `lib` složky |
| modul runtime | Obsah `runtime` složky |
| contentFiles | Obsah `contentfiles` složky |
| sestavení | Props a cílem v `build` složky |
| Analyzátory | Analyzátory rozhraní .NET |
| nativní | Obsah `native` složky |
| žádná | Žádná z výše uvedeného se používají. |
| všechny | Všechny výše uvedené (s výjimkou `none`) |

V následujícím příkladu se všechno kromě soubory z balíčku obsahu by být využívány službou projektu a všechno kromě souborů obsahu a analyzátory by tok nadřazený projekt.

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

Všimněte si, že protože `build` není součástí `PrivateAssets`, cílem a props *bude* toku nadřazený projekt. Například vezměte v úvahu, že odkaz na výše uvedené se používá v projektu, který NuGet balíček s názvem AppLogger sestavení. AppLogger spotřebovat cílů a props z `Contoso.Utility.UsefulStuff`, jak můžete projekty, které využívají AppLogger.

## <a name="adding-a-packagereference-condition"></a>Přidáním PackageReference podmínky

Můžete vytvořit podmínku, kterou chcete řízení a zda balíček je součástí, kde podmínky můžete použít všechny nástroje MSBuild proměnná nebo Proměnná definovaná v souboru cíle nebo props. Ale na v současné době pouze `TargetFramework` proměnné je podporována.

Řekněme například, že cílení `netstandard1.4` a také `net452` , ale mají závislost, kterou lze použít pouze u `net452`. V takovém případě nechcete, aby `netstandard1.4` projekt, který využívá vašeho balíčku pro přidání tohoto nepotřebné závislosti. Chcete-li tomu zabránit, zadejte podmínku na `PackageReference` následujícím způsobem:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Balíček vytvořená s využitím tohoto projektu se zobrazí, zda jsou zahrnuty jako závislost pouze pro Newtonsoft.json `net452` cíl:

![Výsledek použití podmínku na PackageReference s VS2017](media/PackageReference-Condition.png)

Podmínky lze použít také v `ItemGroup` úrovni a budou platit pro všechny podřízené objekty `PackageReference` prvky:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
