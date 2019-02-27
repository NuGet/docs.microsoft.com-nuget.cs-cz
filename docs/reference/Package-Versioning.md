---
title: Odkaz na balíček NuGet verze
description: Přesné údaje o zadání čísel verzí a rozsahy adres pro další balíčky, na které závisí balíčku NuGet, a jak jsou závislosti nainstalované.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6407cd2ea5e5e7a9c9e2be679764a8a0d5dd9260
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852465"
---
# <a name="package-versioning"></a>Správa verzí balíčků

Konkrétní balíček je vždy rozumělo použití jeho identifikátor balíčku a číslem přesnou verzi. Například [Entity Framework](https://www.nuget.org/packages/EntityFramework/) na nuget.org má několik desítek konkrétní balíčky k dispozici od verze *4.1.10311* verzi *6.1.3* (nejnovější stabilní verze vydání) a širokou škálu předběžných verzí, jako jsou *6.2.0-beta1*.

Při vytváření balíčku, přiřaďte číslo konkrétní verze s příponou volitelný text, který předběžné verze. Při využívání balíčků, na druhé straně může zadáte číslo přesnou verzi nebo rozsah verzí přijatelné.

V tomto tématu:

- [Základní informace o verzi](#version-basics) včetně přípony předběžné verze.
- [Rozsahů verzí a zástupných znacích](#version-ranges-and-wildcards)
- [Čísla verzí normalizované](#normalized-version-numbers)

## <a name="version-basics"></a>Základní informace o verzi

Číslo konkrétní verze má formát *Hlavníverze.podverze.oprava [-přípona]*, kde komponenty mají následující význam:

- *Hlavní*: Změny způsobující chyby
- *Vedlejší*: Nové funkce, ale zpětně kompatibilní
- *Oprava*: Zpětně kompatibilní chyby opravuje pouze
- *-Přípony* (volitelné): spojovník následovaný řetězec označující Předběžná verze (následující [Semantic Versioning nebo SemVer 1.0 konvence](http://semver.org/spec/v1.0.0.html)).

**Příklady:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org odmítne všechny nahrávání balíčku, který nemá číslem přesnou verzi. Verze musí být zadán v `.nuspec` nebo soubor projektu používá k vytvoření balíčku.

### <a name="pre-release-versions"></a>Předběžné verze

Technicky vzato Tvůrce balíčku můžete použít libovolný řetězec jako příponu k označení předprodejní verze NuGet považuje předběžné verze těchto verzí a díky žádná interpretace. To znamená je zahrnuta NuGet zobrazí řetězec na plnou verzi v jakékoli uživatelské rozhraní, byste museli opustit jakékoli výklad tuto příponu význam příjemci.

Ale nutné dodat, balíček vývojáři obvykle postupují podle rozpoznaný zásady vytváření názvů:

- `-alpha`: Alfa verze, obvykle se používá pro nedokončenou prací a experimentování.
- `-beta`: Betaverze, obvykle ten, který je funkce pro další plánované vydání, ale může obsahovat známé chyby.
- `-rc`: Verze Release candidate, obvykle, která je potenciálně konečné vydání (stabilní), není-li významný chyby se objeví.

> [!Note]
> Podporuje NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), která podporuje předběžné verze čísla pomocí zápisu s tečkou, stejně jako v *1.0.1-build.23*. Verze NuGet starší než 4.3.0 nepodporuje zápisu s tečkou. Můžete použít formuláře jako *1.0.1-build23*.

Při řešení a odkazy na balíček více verzí balíčku se liší pouze podle přípony, NuGet nejprve zvolí verze bez přípony a potom použije prioritu předběžných verzí ve vzestupném abecedním pořadí. Například následující verze vybere v uvedeném pořadí:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantic Versioning 2.0.0

Díky NuGet 4.3.0+ a sady Visual Studio 2017 verze 15.3 + podporuje NuGet [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).

Některé sémantiku SemVer v2.0.0 nepodporují starší klienti. NuGet bere v úvahu verze balíčku bude SemVer v2.0.0 konkrétní, pokud je splněna jedna z následujících příkazů:

- Předběžné verze je popisek oddělené tečkou, třeba *1.0.0-alpha.1*
- Verze má metadat sestavení, například *1.0.0+githash*

Pro nuget.org balíček definován jako balíček v2.0.0 SemVer, pokud je splněna jedna z následujících příkazů:

- Verze balíčku vlastní je SemVer v2.0.0 předpisům, ale není SemVer v1.0.0 předpisy, podle výše.
- Některé z rozsahů verzí závislost balíčku má minimální nebo maximální verzi, která je SemVer v2.0.0 předpisům, ale není SemVer v1.0.0 předpisy, výše; například *[1.0.0-alpha.1,)*.

Pokud odešlete balíček v2.0.0 konkrétní SemVer na nuget.org, balíček je viditelný pro starší klienty a k dispozici pro následující klienty NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 verze 15.3 +
- Visual Studio 2015 se sadou [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- DotNet
  - dotnetcore.exe (2.0.0+ sady .NET SDK)

Klienti třetích stran:

- JetBrains Rider
- Stáhnout verzi 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Rozsahů verzí a zástupných znacích

Při odkazování na závislosti balíčků, podporuje NuGet, pomocí notace interval pro zadání rozsahu verzí shrnout takto:

| Zápis | Použité pravidlo | Popis |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Minimální verze (včetně) |
| (1.0,) | x > 1.0 | Minimální verze exkluzivní |
| [1.0] | x == 1.0 | Shoda přesnou verzi |
| (,1.0] | x ≤ 1.0 | Maximální verze, včetně |
| (,1.0) | x < 1.0 | Maximální verze exkluzivní |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Přesné rozsahu, včetně |
| (1.0,2.0) | 1.0 < x < 2.0 | Přesný rozsah exkluzivní |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Smíšené včetně minimální a výhradní maximální verze |
| (1.0)    | neplatné | neplatné |

Při použití formátu PackageReference NuGet podporuje také pomocí zástupných znaků zápisu, \*pro hlavní, vedlejší, opravy a příponu předběžné verze část čísla. Zástupné znaky se nepodporují `packages.config` formátu.

> [!Note]
> Předběžné verze nejsou zahrnuty při rozpoznávání rozsahů verzí. Předběžné verze *jsou* zahrnuty při použití zástupného znaku (\*). Rozsah verzí *[1.0,2.0]*, například nezahrnuje 2.0 beta, ale zástupné zápis _2.0-*_ nepodporuje. Zobrazit [vydat 912](https://github.com/NuGet/Home/issues/912) pro další informace o zástupných znacích předběžné verze.

### <a name="examples"></a>Příklady

Vždy v souborech projektu, zadejte verzi nebo rozsah verzí pro závislosti balíčků `packages.config` soubory, a `.nuspec` soubory. Bez verzi nebo rozsah verzí, NuGet 2.8.x a dříve zvolí nejnovější verze balíčku k dispozici při překladu závislost, zatímco NuGet 3.x a později zvolí nejnižší verze balíčku. Určení verze nebo verze rozsah předchází tento nejistoty.

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

V `packages.config`, všech závislostí je uvedený s přesná `version` atribut, který se používá při obnovování balíčků. `allowedVersions` Atribut se používá pouze během operace aktualizace, chcete-li omezit verze, ke kterým může aktualizovat balíček.

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

**Odkazy v `.nuspec` soubory**

`version` Atribut `<dependency>` element popisuje rozsah verzí, které jsou přijatelné pro závislost.

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

## <a name="normalized-version-numbers"></a>Čísla verzí normalizované

> [!Note]
> Toto je zásadní změny pro NuGet 3.4 a vyšší.

Získání balíčků z úložiště během instalace, přeinstalujte nebo obnovení operací, zpracovává NuGet 3.4 + čísla verzí následujícím způsobem:

- Počáteční nuly jsou odebrány z čísel verzí:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Nula v čtvrtá součást čísla verze budou vypuštěny.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Tato normalizace nemá vliv na čísla verzí v balíčcích. ovlivňuje pouze jak odpovídá NuGet verze, pokud řešení závislostí.

Úložiště balíčků NuGet však musí zpracovat tyto hodnoty stejným způsobem jako NuGet, aby se zabránilo duplikování verze balíčku. Proto úložiště, který obsahuje verzi *1.0* balíčku nemělo by hostovat také verze *1.0.0* jako samostatné a odlišné balíček.
