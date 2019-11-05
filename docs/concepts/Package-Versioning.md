---
title: Reference k verzi balíčku NuGet
description: Přesné podrobnosti o zadání čísel a rozsahů verzí pro další balíčky, na kterých závisí balíček NuGet, a jak se nainstalují závislosti.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: e0014a812ea591ef40c961e13864652d75ebdf6c
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610989"
---
# <a name="package-versioning"></a>Správa verzí balíčků

U konkrétního balíčku se vždy používá identifikátor jeho balíčku a přesné číslo verze. Například [Entity Framework](https://www.nuget.org/packages/EntityFramework/) v NuGet.org má k dispozici několik desítek specifických balíčků, od verze *4.1.10311* po verzi *6.1.3* (nejnovější stabilní verze) a řadu předběžných verzí, jako je *6.2.0-Beta1.* .

Při vytváření balíčku přiřadíte konkrétní číslo verze s volitelnou příponou textu v předběžné verzi. Při využívání balíčků můžete na druhou stranu zadat buď přesné číslo verze, nebo rozsah přijatelných verzí.

V tomto tématu:

- [Základní informace o verzích](#version-basics) včetně přípon předběžné verze.
- [Rozsahy verzí a zástupné znaky](#version-ranges-and-wildcards)
- [Normalizovaná čísla verzí](#normalized-version-numbers)

## <a name="version-basics"></a>Základy verzí

Konkrétní číslo verze je ve formátu *hlavní. podverze. Oprava [-přípona]* , kde tyto komponenty mají následující význam:

- *Hlavní*: přerušující se změny
- *Vedlejší*: nové funkce, ale zpětně kompatibilní
- *Oprava*: zpětně kompatibilní opravy chyb
- *-Přípona* (volitelné): spojovník následovaný řetězcem, který označuje předběžnou verzi (podle [konvence sémantické verze nebo SemVer 1,0](https://semver.org/spec/v1.0.0.html)).

**4.6**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org odmítne jakékoli nahrání balíčku, který nemá přesné číslo verze. Verze musí být zadaná v `.nuspec` nebo souboru projektu, který se používá k vytvoření balíčku.

### <a name="pre-release-versions"></a>Předběžné verze verzí

Pro technicky řečeno, tvůrci balíčků můžou použít libovolný řetězec jako příponu k označení předprodejní verze, protože NuGet považuje takovou verzi za předběžnou verzi a neprovede žádnou další interpretaci. To znamená, že NuGet zobrazí úplný řetězec verze v jakémkoli uživatelském rozhraní, a ponechává všechny výklady významu přípony pro příjemce.

V takovém případě vývojáři balíčku většinou následují jako rozpoznané konvence pojmenování:

- `-alpha`: verze alfa, která se obvykle používá pro práci a experimentování.
- `-beta`: beta verze, obvykle ta, která je dokončena pro příští plánované vydání, ale může obsahovat známé chyby.
- `-rc`: verze Release Candidate, obvykle verze, která je potenciálně finální (stabilní), pokud se objevují významné chyby.

> [!Note]
> NuGet 4.3.0 + podporuje [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), která podporuje předběžná vydání čísel s tečkami Notation, jako v *1.0.1-Build. 23*. Zápis tečky není u verzí NuGet před 4.3.0 podporován. Můžete použít formulář jako *1.0.1-build23*.

Při překládání odkazů na balíčky a více verzí balíčku se liší pouze příponou, NuGet zvolí verzi bez přípony a pak použije přednost na předběžné verze v obráceném abecedním pořadí. Například následující verze se volí v uvedeném pořadí:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>2\.0.0 sémantických verzí

Pomocí NuGet 4.3.0 + a sady Visual Studio 2017 verze 15.3 + NuGet podporuje [sémantickou správu verzí 2.0.0](https://semver.org/spec/v2.0.0.html).

Některé sémantiky SemVer v 2.0.0 se ve starších klientech nepodporují. NuGet považuje verzi balíčku za SemVer v 2.0.0, pokud je splněn některý z následujících příkazů:

- Jmenovka před vydáním je oddělená tečkami, například *1.0.0-Alpha. 1*
- Verze obsahuje sestavení – metadata, například *1.0.0 + githash* .

V případě nuget.org je balíček definován jako balíček SemVer v 2.0.0, pokud je splněn některý z následujících příkazů:

- Vlastní verze balíčku je kompatibilní s SemVer v 2.0.0, ale ne SemVer v 1.0.0, jak je definováno výše.
- Všechny rozsahy verzí závislostí balíčku mají minimální nebo maximální verzi, která je kompatibilní s SemVer v 2.0.0, ale ne SemVer v 1.0.0 kompatibilní, definovaná výše; například *[1.0.0-Alpha. 1,)* .

Pokud nahrajete balíček SemVer v 2.0.0 pro nuget.org, balíček je neviditelná pro starší klienty a je k dispozici pouze pro následující klienty NuGet:

- 4\.3.0 NuGet +
- Visual Studio 2017 verze 15.3 +
- Visual Studio 2015 s [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore. exe (sada .NET SDK 2.0.0 +)

Klienti třetích stran:

- JetBrains řidiče
- Paket verze 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Rozsahy verzí a zástupné znaky

Při odkazování na závislosti balíčků podporuje NuGet použití zápisu intervalů pro určení rozsahů verzí shrnutý takto:

| Zápis | Použité pravidlo | Popis |
|----------|--------------|-------------|
| 1.0 | × ≥ 1,0 | Minimální verze, včetně |
| (1,0,) | x > 1,0 | Minimální verze, exkluzivní |
| [1,0] | x = = 1,0 | Přesná shoda verze |
| (, 1,0] | × ≤ 1,0 | Maximální verze, včetně |
| (, 1,0) | x < 1,0 | Maximální verze, exkluzivní |
| [1.0, 2.0] | 1,0 ≤ x ≤ 2,0 | Přesný rozsah (včetně) |
| (1.0, 2.0) | 1,0 < x < 2,0 | Přesný rozsah, exkluzivní |
| [1.0, 2.0) | 1,0 ≤ x < 2,0 | Smíšené celkové minimální a exkluzivní verze |
| (1,0)    | neplatné | neplatné |

V případě použití formátu PackageReference podporuje NuGet také použití zástupných \*znaků pro hlavní, dílčí, opravné a předběžné verze částí čísla. Ve formátu `packages.config` se nepodporují zástupné znaky.

> [!Note]
> Mezi rozsahy verzí v PackageReference patří předběžné verze. V případě návrhu nebudou plovoucí verze překládat předběžné verze, pokud se na ně nerozhodnete. Stav související žádosti o funkci najdete v tématu věnovaném [problému 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Příklady

Vždy zadejte verzi nebo rozsah verzí pro závislosti balíčku v souborech projektu, `packages.config` soubory a `.nuspec` soubory. Bez verze nebo rozsahu verze sada NuGet 2.8. x a starší zvolí nejnovější dostupnou verzi balíčku při řešení závislosti, zatímco NuGet 3. x a novější zvolí nejnižší verzi balíčku. Zadání verze nebo rozsahu verze zabrání této nejistotě.

#### <a name="references-in-project-files-packagereference"></a>Odkazy v souborech projektu (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Odkazy v `packages.config`:**

V `packages.config`je každá závislost uvedená s přesným `version` atributem, který se používá při obnovování balíčků. Atribut `allowedVersions` se používá jenom během operací aktualizace k omezení verzí, na které se balíček může aktualizovat.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**Odkazy v souborech `.nuspec`**

Atribut `version` v elementu `<dependency>` popisuje verze rozsahu, které jsou pro závislost přijatelné.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>Normalizovaná čísla verzí

> [!Note]
> Toto je zásadní změna pro NuGet 3,4 a novější.

Při získávání balíčků z úložiště během instalace, přeinstalace nebo obnovení operací, NuGet 3.4 + zpracovává čísla verzí následujícím způsobem:

- Počáteční nuly jsou odebrány z čísel verzí:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Hodnota nula ve čtvrté části čísla verze bude vynechána.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

operace `pack` a `restore` normalizují verze, kdykoli je to možné. U balíčků už je tato normalizace neovlivněna čísly verzí v samotných balíčcích. má vliv jenom na to, jak NuGet odpovídá verzím při řešení závislostí.

Úložiště balíčků NuGet ale musí tyto hodnoty nakládat stejným způsobem jako NuGet, aby se zabránilo duplikaci verze balíčku. Proto úložiště, které obsahuje verzi *1,0* balíčku, by nemělo také hostovat verzi *1.0.0* jako samostatný a jiný balíček.
