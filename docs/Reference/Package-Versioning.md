---
title: Odkaz na balíček NuGet verze
description: Přesné informace o zadání čísla verzí a rozsahy adres pro jiné balíčky, na který závislý balíček NuGet, a způsob instalace závislosti.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: d17d964ac73075f05678b9727e90d481a30da62e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="package-versioning"></a>Správa verzí balíčku

Konkrétní balíček se vždy označuje pomocí jeho identifikátoru balíčku a představuje počet přesnou verzi. Například [Entity Framework](https://www.nuget.org/packages/EntityFramework/) v nuget.org má několik desítek konkrétní balíčky k dispozici od verze *4.1.10311* verzi *6.1.3* (nejnovější stabilní verzi) a celou řadu předprodejní verze, jako jsou *6.2.0-beta1*.

Při vytváření balíčku, můžete přiřadit konkrétní verzi číslo s příponou volitelné text předběžné verze. Při využívání balíčky, na druhé straně, můžete číslo přesné verze nebo rozsah přijatelné verzí.

V tomto tématu:

- [Základní informace o verzi](#version-basics) včetně přípony předběžné verze.
- [Verze rozsahy a zástupné znaky](#version-ranges-and-wildcards)
- [Čísla verzí normalizovaný](#normalized-version-numbers)

## <a name="version-basics"></a>Základní informace o verzi

Číslo konkrétní verze je ve formátu *Major.Minor.Patch [-přípona]*, kde součásti mají následující významy:

- *Hlavní*: nejnovější změny
- *Méně závažné*: nové funkce, ale zpětně kompatibilní
- *Oprava*: pouze zpětně kompatibilní opravy chyb
- *-Přípona* (volitelné): pomlčka následuje řetězec představující předběžné verze (následující [sémantické verze nebo SemVer 1.0 konvence](http://semver.org/spec/v1.0.0.html)).

**Příklady:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org odmítne všechny nahrávání balíčku, který představuje počet přesnou verzi chybí. Verze musí být zadán v `.nuspec` nebo projektu soubor použitý k vytvoření balíčku.

### <a name="pre-release-versions"></a>Předběžné verze

Technicky platí, že tvůrci balíček můžete použít libovolný řetězec jako příponu k označení předběžné verze, jako NuGet zpracovává všechny tyto verze jako předběžné verze a umožňuje žádné jiné interpretace. To znamená je zahrnuta NuGet zobrazí na plnou verzi řetězce v jakémkoli uživatelského rozhraní, a jakýkoli výklad význam tuto příponu k příjemce.

Ale nutné dodat, balíček vývojáři obvykle podle rozpoznaný zásady vytváření názvů:

- `-alpha`: Alfa verze, obvykle se používá pro práce v průběhu a experimenty.
- `-beta`: Beta verze, obvykle ten, který je funkce dokončení další plánované verze, ale může obsahovat známé chyby.
- `-rc`: Release candidate, obvykle verzi, která je potenciálně konečné (stable), pokud vznikat významné chyby.

> [!Note]
> Podporuje NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), který podporuje předběžné verze čísla s zápisu s tečkou, jako v *1.0.1-build.23*. Verze NuGet před 4.3.0 nepodporuje zápisu s tečkou. Můžete použít formuláře jako *1.0.1-build23*.

Při rozpoznávání, že balíček odkazuje a více verzí balíčku liší pouze příponu, NuGet vybere první verze bez přípony a pak použije prioritu pro předběžné verze verze ve vzestupném abecedním pořadí. Například by být zvolena následující verze v uvedeném pořadí:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Sémantické verze 2.0.0

NuGet 4.3.0+ a Visual Studio 2017 verze 15.3 +, podporuje NuGet [sémantické verze 2.0.0](http://semver.org/spec/v2.0.0.html).

Některé sémantiku SemVer v2.0.0 nepodporuje starší klienty. NuGet zvažuje verze balíčku byl SemVer v2.0.0 konkrétní, pokud je splněna jedna z následujících příkazů:

- Předběžné verze popisek je oddělené tečkou, například *1.0.0-alpha.1*
- Verze má sestavení metadata, například *1.0.0+githash*

Pro nuget.org balíček definován jako balíček v2.0.0 SemVer, pokud platí některá z následujících příkazů:

- Verze balíčku pro vlastní je SemVer v2.0.0 kompatibilní, ale ne SemVer v1.0.0 předpisy, podle definice výše.
- Žádné z rozsahů verze závislosti balíčku má minimální nebo maximální verzi, která je kompatibilní s SemVer v2.0.0, ale není SemVer v1.0.0 předpisy, definovaný nad; například *[1.0.0-alpha.1,)*.

Pokud balíček v2.0.0 specifické SemVer nahrajete do nuget.org, je balíček neviditelná pro starší klienty a k dispozici pouze na následující klienty NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 verze 15.3 +
- Visual Studio 2015 se [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- DotNet.
  - dotnetcore.exe (2.0.0+ .NET SDK)

Klienti třetí strany:

- JetBrains Rider
- Stáhnout verze 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Verze rozsahy a zástupné znaky

Při odkazování na závislosti balíčků, NuGet podporuje notaci interval pro určení rozsahu verzí shrnout takto:

| Zápis | Použité pravidlo | Popis |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Minimální verze, včetně. |
| (1.0,) | x > 1.0 | Minimální verze, exkluzivní |
| [1.0] | x == 1.0 | Shoda přesnou verzi |
| (,1.0] | x ≤ 1.0 | Maximální verze, včetně. |
| (,1.0) | x < 1.0 | Maximální verze, exkluzivní |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Přesný rozsahu (včetně). |
| (1.0,2.0) | 1.0 < x < 2.0 | Přesný rozsah výhradní |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Smíšená (včetně) minimální a výhradní maximální verze |
| (1.0)    | neplatné | neplatné |

Při použití formátu PackageReference, NuGet podporuje také notaci zástupný znak, \*, pro hlavní, vedlejší, opravy a příponu předběžné verze součástí číslo. Zástupné znaky nejsou podporovány `packages.config` formátu.

> [!Note]
> Předběžné verze nejsou zahrnuty při rozpoznávání rozsahy verze. Předběžné verze verze *jsou* zahrnuty při pomocí zástupného znaku (\*). Rozsah verze *[1.0,2.0]*, například nezahrnuje 2.0 beta, ale zápis zástupný znak _2.0-*_ nepodporuje. V tématu [vydání 912](https://github.com/NuGet/Home/issues/912) Další informace o předběžné verze zástupné znaky.

### <a name="examples"></a>Příklady

Vždy zadejte verzi nebo rozsahu verze závislosti balíčku v souborech projektu `packages.config` soubory, a `.nuspec` soubory. Bez verze nebo verze rozsah, NuGet 2.8.x a dříve vybere nejnovější verze balíčku k dispozici při rozpoznávání závislost, zatímco NuGet 3.x a později rozhodne nejnižší verze balíčku. Určení verze nebo verze, rozsah zabraňuje tato nejistoty.

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Odkazy na v `packages.config`:**

V `packages.config`, každý závislostí je označené přesného `version` atribut, který se používá při obnovení balíčků. `allowedVersions` Atribut se používá pouze během operace aktualizace omezit verze, do kterých může aktualizovat balíček.

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

**Odkazy na v `.nuspec` soubory**

`version` Atribut `<dependency>` element popisuje rozsah verze, které jsou přijatelné pro závislost.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a>Čísla verzí normalizovaný

> [!Note]
> Toto je narušující změně pro NuGet 3.4 a novější.

Při získávání balíčky z úložiště během instalace, znovu nainstalovat, nebo obnovit operace, považuje NuGet 3.4 + čísla verzí následujícím způsobem:

- Úvodní nuly jsou odebrány z čísla verzí:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Nula v čtvrtá součást číslo verze bude vynechán.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Tato hodnota normalization nemá vliv na čísla verze v balíčcích sami; ovlivňuje způsob NuGet odpovídá jen verze při řešení závislostí.

Úložiště balíčku NuGet však musí považovat tyto hodnoty stejným způsobem jako NuGet aby duplikace verze balíčku. Proto úložiště, který obsahuje verzi *1.0* balíčku neměly hostovat taky verze *1.0.0* jako samostatné a jiný balíček.
