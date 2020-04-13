---
title: Odkaz na verzi balíčku NuGet
description: Přesné podrobnosti o určení čísla verzí a rozsahy pro jiné balíčky, na kterých závisí balíček NuGet a jak jsou nainstalovány závislosti.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c79976c2f4ded2fba3796fb847d3c90807d7b86c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147445"
---
# <a name="package-versioning"></a>Správa verzí balíčků

Konkrétní balíček je vždy odkazoval se na pomocí jeho identifikátor balíčku a přesné číslo verze. Například [Entity Framework](https://www.nuget.org/packages/EntityFramework/) na nuget.org má několik desítek konkrétní chytací balíčky k dispozici, od verze *4.1.10311* na verzi *6.1.3* (nejnovější stabilní verze) a různé předběžné verze jako *6.2.0-beta1*.

Při vytváření balíčku přiřadíte konkrétní číslo verze s volitelnou příponou předběžné verze textu. Při spotřebovávání balíčků můžete naopak zadat přesné číslo verze nebo rozsah přijatelných verzí.

V tomto tématu:

- [Základy verze](#version-basics) včetně předprodejních přípon.
- [Rozsahy verzí](#version-ranges)
- [Normalizovaná čísla verzí](#normalized-version-numbers)

## <a name="version-basics"></a>Základy verzí

Konkrétní číslo verze je ve tvaru *Major.Minor.Patch[-Přípona]*, kde komponenty mají následující významy:

- *Hlavní*: Prolomení změn
- *Minor*: Nové funkce, ale zpětně kompatibilní
- *Oprava*: Pouze opravy zpětně kompatibilních chyb
- *-Přípona* (volitelně): pomlčka následovaná řetězcem označujícím předběžnou verzi (podle [sémantického správu verzí nebo konvence SemVer 1.0).](https://semver.org/spec/v1.0.0.html)

**Příklady:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org odmítne jakýkoli balíček nahrát, který postrádá přesné číslo verze. Verze musí být zadána v souboru `.nuspec` nebo projektu použitého k vytvoření balíčku.

### <a name="pre-release-versions"></a>Předběžné verze

Technicky vzato mohou tvůrci balíčků použít libovolný řetězec jako příponu k označení předběžné verze, protože NuGet zachází s jakoukoli takovou verzí jako s předběžnou verzí a neprovádí žádnou jinou interpretaci. To znamená NuGet zobrazí řetězec plné verze v bez ohledu na ui se týká, takže jakýkoli výklad významu přípony pro spotřebitele.

To znamená, že vývojáři balíčků obecně dodržují uznávané konvence pojmenování:

- `-alpha`: Alfa verze, obvykle používaná pro nedokončenou práci a experimentování.
- `-beta`: Beta verze, obvykle taková, která je dokončena pro další plánovanou verzi, ale může obsahovat známé chyby.
- `-rc`: Release candidate, obvykle vydání, které je potenciálně konečné (stabilní), pokud se neobjeví významné chyby.

> [!Note]
> NuGet 4.3.0+ podporuje [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), který podporuje předverze čísla s tečkou notace, jako v *1.0.1-build.23*. Dot notace není podporována s Verzemi NuGet před 4.3.0. Můžete použít formulář jako *1.0.1-build23*.

Při řešení odkazů na balíček a více verzí balíčků se liší pouze příponou, NuGet nejprve vybere verzi bez přípony a pak použije přednost pro předběžné verze v obráceném abecedním pořadí. Například následující verze by byly vybrány v přesném pořadí:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Sémantická správa verzí 2.0.0

S NuGet 4.3.0+ a Visual Studio 2017 verze 15.3+, NuGet podporuje [sémantické versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

Některé sémantiky SemVer v2.0.0 nejsou podporovány ve starších klientů. NuGet považuje verzi balíčku za SemVer v2.0.0 specifické, pokud je splněna některá z následujících příkazů:

- Předprodejní štítek je oddělen tečkami, například *1.0.0-alpha.1*
- Verze má metadata sestavení, například *1.0.0+githash*

Pro nuget.org je balíček definován jako balíček SemVer v2.0.0, pokud je splněn některý z následujících příkazů:

- Vlastní verze balíčku je kompatibilní s ssver v2.0.0, ale není kompatibilní s SemVer v1.0.0, jak je definováno výše.
- Všechny rozsahy verze závislostí balíčku má minimální nebo maximální verzi, která je kompatibilní s semVer v2.0.0, ale není kompatibilní s semVer v1.0.0, definované výše; například *[1.0.0-alpha.1, ).*

Pokud nahrajete balíček specifický pro SemVer v2.0.0 do nuget.org, balíček je pro starší klienty neviditelný a je k dispozici pouze následujícím klientům NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 verze 15.3+
- Visual Studio 2015 s [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Klienti třetích stran:

- JetBrains Jezdec
- Paket verze 5.0+

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>Rozsahy verzí

Při odkazování na závislosti balíčků, NuGet podporuje použití zápisu intervalu pro určení rozsahy verzí, shrnuty takto:

| Notace | Použité pravidlo | Popis |
|----------|--------------|-------------|
| 1.0 | x ≥ 1,0 | Minimální verze včetně |
| (1.0,) | x > 1,0 | Minimální verze, exkluzivní |
| [1.0] | x == 1,0 | Přesná verze odpovídá |
| (,1.0] | x ≤ 1,0 | Maximální verze včetně |
| (,1.0) | x < 1,0 | Maximální verze, exkluzivní |
| [1.0,2.0] | 1,0 ≤ x ≤ 2,0 | Přesný rozsah včetně |
| (1.0,2.0) | 1,0 < x < 2,0 | Přesný rozsah, exkluzivní |
| [1.0,2.0) | 1,0 ≤ x < 2,0 | Smíšená minimální a exkluzivní maximální verze |
| (1.0)    | neplatné | neplatné |

Při použití formátu PackageReference NuGet také podporuje použití \*plovoucí zápis, , pro hlavní, menší, patch a předprodejní přípona části čísla. Plovoucí verze nejsou podporovány `packages.config` s formátem.

> [!Note]
> Rozsahy verzí v PackageReference zahrnují předběžné verze. Plovoucí verze podle návrhu neřeší předběžné verze, pokud nejsou odvráceny. Stav žádosti o související funkce naleznete v [tématu problém 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Příklady

Vždy zadejte rozsah verze nebo verze pro `packages.config` závislosti balíčků `.nuspec` v souborech projektu, souborech a souborech. Bez verze nebo rozsah verze NuGet 2.8.x a dříve vybere nejnovější dostupné verze balíčku při řešení závislosti, vzhledem k tomu, NuGet 3.x a později zvolí nejnižší verzi balíčku. Určení verze nebo rozsah verze se této nejistotě vyhne.

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

V `packages.config`aplikaci je každá závislost `version` uvedena s přesným atributem, který se používá při obnově balíčků. Atribut `allowedVersions` se používá pouze během operací aktualizace omezit verze, na které balíček může být aktualizován.

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

**Odkazy v `.nuspec` souborech**

Atribut `version` v `<dependency>` elementu popisuje verze rozsahu, které jsou přijatelné pro závislost.

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
> Toto je narušující změna pro NuGet 3.4 a novější.

Při získávání balíčků z úložiště během instalace, přeinstalace nebo obnovení operací, NuGet 3.4+ zachází čísla verzí takto:

- Počáteční nuly jsou odstraněny z čísel verzí:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Nula ve čtvrté části čísla verze bude vynechána.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- Metadata sestavení SemVer 2.0.0 jsou odebrána.

        1.0.7+r3456 is treated as 1.0.7

`pack`a `restore` operace normalizují verze, kdykoli je to možné. U již vytvořených balíčků nemá tato normalizace vliv na čísla verzí v samotných balíčcích; ovlivňuje pouze způsob, jakým NuGet odpovídá verzím při řešení závislostí.

Úložiště balíčků NuGet však musí zacházet s těmito hodnotami stejným způsobem jako NuGet, aby se zabránilo duplikaci verze balíčku. Úložiště, které obsahuje verzi *1.0* balíčku, by tedy nemělo být hostitelem verze *1.0.0* jako samostatného a odlišného balíčku.
