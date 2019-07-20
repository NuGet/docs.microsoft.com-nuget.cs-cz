---
title: Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových bodů rozhodování, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 6774329138c2bf26908496860267e3570a94d39c
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/19/2019
ms.locfileid: "68346157"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet

Bez ohledu na to, co váš balíček používá, nebo jaký kód obsahuje, můžete použít jeden z nástrojů rozhraní `nuget.exe` příkazového řádku (nebo `dotnet.exe`) k zabalení této funkce do komponenty, kterou lze sdílet a používat v jakémkoli počtu jiných vývojářů. Tento článek popisuje, jak vytvořit balíček pomocí rozhraní příkazového řádku dotnet. Informace o instalaci `dotnet` rozhraní příkazového řádku najdete v tématu [Instalace nástrojů klienta NuGet](../install-nuget-client-tools.md). Počínaje sadou Visual Studio 2017 je rozhraní příkazového řádku dotnet součástí úloh .NET Core.

Pro projekty .NET Core a .NET Standard, které používají [Formát styly sady SDK](../resources/check-project-format.md)a všechny další projekty ve stylu sady SDK, nástroj NuGet používá informace v souboru projektu přímo k vytvoření balíčku. Podrobné kurzy najdete v tématu [Vytvoření balíčků .NET Standard pomocí příkazu DOTNET CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [vytváření balíčků .NET Standard pomocí sady Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack`je obdobou `dotnet pack`funkcí. Pro sestavení pomocí nástroje MSBuild jsou koncepty stejné, jak je popsáno v tomto článku, ale příkazy příkazového řádku se mírně liší. Podobně s projektem, který není ve stylu sady SDK, `<PackageReference>`a můžete použít. `msbuild /t:pack` V těchto scénářích je nutné přidat balíček NuGet. Build. Tasks. Pack do svých závislostí. Podívejte [se na téma NuGet Pack a obnovte jako cíle MSBuild](../reference/msbuild-targets.md).

> [!IMPORTANT]
> Toto téma se vztahuje na projekty ve [stylu sady SDK](../resources/check-project-format.md) , obvykle v projektech .NET Core a .NET Standard.

## <a name="set-properties"></a>Nastavit vlastnosti

Pro vytvoření balíčku jsou vyžadovány následující vlastnosti.

- `PackageId`, identifikátor balíčku, který musí být jedinečný v rámci Galerie, která hostuje balíček. Pokud není zadaný, použije se výchozí hodnota `AssemblyName`.
- `Version`, konkrétní číslo verze ve formátu *hlavní. podverze. Oprava [-přípona]* , kde *-přípona* identifikuje [předběžné verze verzí](prerelease-packages.md). Pokud není zadaný, použije se výchozí hodnota 1.0.0.
- Název balíčku, jak by měl být zobrazen na hostiteli (například nuget.org)
- `Authors`, informace o autorovi a vlastníka. Pokud není zadaný, použije se výchozí hodnota `AssemblyName`.
- `Company`, název vaší společnosti. Pokud není zadaný, použije se výchozí hodnota `AssemblyName`.

V sadě Visual Studio můžete nastavit tyto hodnoty ve vlastnostech projektu (klikněte pravým tlačítkem myši na projekt v Průzkumník řešení, zvolte **vlastnosti**a vyberte kartu **balíček** ). Tyto vlastnosti lze také nastavit přímo v souborech projektu (`.csproj`).

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> Poskytněte balíčku identifikátor, který je jedinečný v rámci nuget.org nebo jakýkoli ze zdrojů balíčku, který používáte.

Můžete také nastavit volitelné vlastnosti, například `Title` `PackageDescription`, `PackageTags`a, jak je popsáno v tématu [cíle sady MSBuild](../reference/msbuild-targets.md#pack-target), [řízení prostředků závislosti](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)a [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.

Podrobnosti o deklarování závislostí a zadání čísel verzí najdete v tématu [Správa verzí balíčků](../reference/package-versioning.md). Je také možné Surface prostředků ze závislostí přímo v balíčku pomocí `<IncludeAssets>` atributů a. `<ExcludeAssets>` Další informace najdete v Seee [řízení prostředků závislostí](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Vyberte jedinečný identifikátor balíčku a nastavte číslo verze.

Identifikátor balíčku a číslo verze jsou dvě nejdůležitější hodnoty v projektu, protože jednoznačně identifikují přesný kód obsažený v balíčku.

**Osvědčené postupy pro identifikátor balíčku:**

- **Jedinečnost**: Identifikátor musí být jedinečný v rámci nuget.org nebo bez ohledu na to, jakou galerii hostují balíček. Než se rozhodnete pro identifikátor, vyhledejte příslušnou galerii a ověřte, jestli se tento název už používá. Aby nedocházelo ke konfliktům, dobrým vzorem je použít název vaší společnosti jako první část identifikátoru, například `Contoso.`.
- **Názvy podobných oborům názvů**: Sledujte vzor podobný oborům názvů v rozhraní .NET pomocí notace tečky namísto spojovníků. Použijte `Contoso.Utility.UsefulStuff` například `Contoso-Utility-UsefulStuff` místo nebo`Contoso_Utility_UsefulStuff`. Příjemci také naleznou užitečné, pokud se identifikátor balíčku shoduje s obory názvů použitými v kódu.
- **Ukázkové balíčky**: Pokud vytváříte balíček ukázkového kódu, který ukazuje, jak použít jiný balíček, připojte `.Sample` se jako přípona k identifikátoru, jako `Contoso.Utility.UsefulStuff.Sample`v. (Vzorový balíček samozřejmě má závislost na druhém balíčku.) Při vytváření ukázkového balíčku použijte `contentFiles` hodnotu v. `<IncludeAssets>` Ve složce uspořádejte vzorový kód do složky s názvem `\Samples\<identifier>` jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`. `content`

**Osvědčené postupy pro verzi balíčku:**

- Obecně platí, že nastavte verzi balíčku tak, aby odpovídala projektu (nebo sestavení), i když to není bezpodmínečně nutné. Toto je jednoduchá skutečnost při omezení balíčku na jediné sestavení. Celkově mějte na paměti, že aplikace NuGet pracuje s verzemi balíčku při řešení závislostí, nikoli ve verzích sestavení.
- Při použití nestandardního schématu verzí nezapomeňte zvážit pravidla správy verzí NuGet, jak je vysvětleno v tématu [Správa verzí balíčků](../reference/package-versioning.md). NuGet je většinou [kompatibilní s semver 2](../reference/package-versioning.md#semantic-versioning-200).

> Informace o řešení závislostí najdete v tématu věnovaném [řešení závislostí s PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Starší informace, které mohou být užitečné také pro lepší pochopení správy verzí, najdete v této sérii příspěvků na blogu.
>
> - [Část 1: Přijetí na Hell knihovny DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Část 2: Základní algoritmus](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Část 3: Sjednocení pomocí přesměrování vazeb](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="run-the-pack-command"></a>Spuštění příkazu Pack

Chcete-li vytvořit balíček NuGet ( `.nupkg` soubor) z projektu, `dotnet pack` spusťte příkaz, který také automaticky vytvoří projekt:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Výstup zobrazuje cestu k `.nupkg` souboru:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automaticky generovat balíček při sestavení

Chcete-li `dotnet pack` automaticky spustit při `dotnet build`spuštění, přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Při spuštění `dotnet pack` v řešení jsou všechny projekty v řešení, které lze zabalit ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) vlastnost nastavena na `true`.

> [!NOTE]
> Když balíček automaticky vygenerujete, čas k zabalení zvýší čas sestavení pro váš projekt.

### <a name="test-package-installation"></a>Instalace testovacího balíčku

Před publikováním balíčku obvykle budete chtít otestovat proces instalace balíčku do projektu. Testy zajistí, že všechny soubory v projektu budou mít všechny na správném místě.

Instalaci můžete v aplikaci Visual Studio nebo na příkazovém řádku otestovat ručně pomocí [kroků normální instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Balíčky jsou neměnné. Pokud problém opravíte, znovu ho změňte a znovu spusťte. při opětovném testování bude stále použita stará verze balíčku, dokud nevymažete složku [globálních balíčků](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) . To je obzvláště důležité při testování balíčků, které nepoužívají jedinečný popisek předprodejní verze pro každé sestavení.

## <a name="next-steps"></a>Další kroky

Po vytvoření balíčku, který je `.nupkg` soubor, můžete ho publikovat do Galerie podle svého výběru, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).

Můžete také chtít zvětšit možnosti vašeho balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:

- [Správa verzí balíčků](../reference/package-versioning.md)
- [Podpora více cílových architektur](../create-packages/supporting-multiple-target-frameworks.md)
- [Transformace zdrojových a konfiguračních souborů](../create-packages/source-and-config-file-transformations.md)
- [Lokalizace](../create-packages/creating-localized-packages.md)
- [Předběžné verze verzí](../create-packages/prerelease-packages.md)
- [Nastavení typu balíčku](../create-packages/set-package-type.md)
- [Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Nakonec existují další typy balíčků, o kterých byste měli vědět:

- [Nativní balíčky](../create-packages/native-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
