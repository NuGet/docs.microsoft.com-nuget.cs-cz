---
title: Předběžné verze verzí v balíčcích NuGet
description: Doprovodné materiály k sestavování balíčků předběžných verzí
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 5dda56ccd4c959bcbcbd12b7a4771ddff1fe7530
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623003"
---
# <a name="building-pre-release-packages"></a>Sestavování balíčků předběžných verzí

Kdykoliv vydáte aktualizovaný balíček s novým číslem verze, NuGet ho považuje za "nejnovější stabilní verzi", jak je znázorněno v uživatelském rozhraní Správce balíčků v sadě Visual Studio:

![Uživatelské rozhraní Správce balíčků zobrazující nejnovější stabilní verzi](media/Prerelease_01-LatestStable.png)

Stabilní verze je ta, která je dostatečně spolehlivá, aby se mohla používat v produkčním prostředí. Nejnovější stabilní verze je zároveň ta, která se nainstaluje jako aktualizace balíčku nebo během obnovování balíčku (v závislosti na tom, jak je popsáno v tématu [Přeinstalace a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md)).

Aby bylo možné podporovat životní cyklus vydání softwaru, NuGet 1,6 a novější umožňuje distribuci předběžných balíčků, kde číslo verze zahrnuje příponu sémantické verze, například `-alpha` , `-beta` nebo `-rc` . Další informace najdete v tématu [Správa verzí balíčků](../concepts/package-versioning.md#pre-release-versions).

Tyto verze můžete zadat jedním z následujících způsobů:

- **Pokud projekt používá [`PackageReference`](../consume-packages/package-references-in-project-files.md) **: v prvku souboru uveďte příponu sémantické verze `.csproj` [`PackageVersion`](/dotnet/core/tools/csproj#packageversion) :

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Pokud projekt obsahuje [`packages.config`](../reference/packages-config.md) soubor**: v prvku souboru uveďte příponu sémantické verze [`.nuspec`](../reference/nuspec.md) [`version`](../reference/nuspec.md#version) :

    ```xml
    <version>1.0.1-alpha</version>
    ```

Až budete připraveni uvolnit stabilní verzi, stačí odebrat příponu a balíček má přednost před všemi předběžnými verzemi. Přečtěte si další informace v tématu [Správa verzí balíčků](../concepts/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Instalace a aktualizace balíčků předběžné verze

Ve výchozím nastavení NuGet nezahrnuje předběžné verze verzí při práci s balíčky, ale toto chování můžete změnit následujícím způsobem:

- **Uživatelské rozhraní Správce balíčků v aplikaci Visual Studio**: v uživatelském rozhraní **Spravovat balíčky NuGet** zaškrtněte políčko **zahrnout předběžné verze** :

    ![Zaškrtávací políčko zahrnout předběžné verze v aplikaci Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Nastavením nebo zrušením zaškrtnutí tohoto políčka se obnoví uživatelské rozhraní Správce balíčků a seznam dostupných verzí, které můžete nainstalovat.

- **Konzola správce balíčků**: použijte `-IncludePrerelease` přepínač s `Find-Package` `Get-Package` příkazy,, `Install-Package` , `Sync-Package` a `Update-Package` . Podívejte se na [referenční informace k prostředí PowerShell](../reference/powershell-reference.md).

- Rozhraní příkazového **řádku NuGet**: použijte `-prerelease` přepínač `install` s `update` příkazy,, `delete` a `mirror` . Přečtěte si [referenční informace k NUGET CLI](../reference/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Sémantická správa verzí

[Sémantická verze nebo konvence SemVer](https://semver.org/spec/v1.0.0.html) popisuje, jak používat řetězce v číslech verzí k vyjádření významu základního kódu.

Každá verze v této konvenci má tři části, `Major.Minor.Patch` a to s následujícím významem:

- `Major`: Přerušující se změny
- `Minor`: Nové funkce, ale zpětně kompatibilní
- `Patch`: Jenom zpětně kompatibilní opravy chyb

Předprodejní verze jsou potom označeny připojením pomlčky a řetězcem po čísle opravy. Technicky řečeno, můžete použít *libovolný* řetězec po spojovníku a NuGet bude balíček zakládat jako předběžnou verzi. NuGet pak zobrazí plné číslo verze v příslušném uživatelském rozhraní a ponechává spotřebitelům interpretovat význam pro sebe samé.

V takovém případě je obecně vhodné postupovat podle rozpoznaných konvencí pojmenování, jako jsou následující:

- `-alpha`: Verze alfa, obvykle se používá pro práci v průběhu a experimentování
- `-beta`: Beta verze, obvykle ta, která je dokončena pro další plánované vydání, ale může obsahovat známé chyby.
- `-rc`: Verze Release Candidate, obvykle verze, která je potenciálně finální (stabilní), pokud se neobjeví významné chyby.

> [!Note]
> NuGet 4.3.0 + podporuje [sémantickou správu verzí v 2.0.0](https://semver.org/spec/v2.0.0.html), která podporuje předběžné verze čísel s tečkami Notation, jako v `1.0.1-build.23` . Zápis tečky není u verzí NuGet před 4.3.0 podporován. V dřívějších verzích nástroje NuGet byste mohli použít tvar, jako by `1.0.1-build23` byl ale vždy považován za předběžnou verzi.

Bez ohledu na přípony, které použijete, ale NuGet jim dáte přednost v obráceném abecedním pořadí:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

Jak je znázorněno, verze bez přípony vždy bude mít přednost před předběžnou verzí.

Úvodní 0s nejsou pro semver2 nutné, ale jsou ve starém schématu verze. Použijete-li číselné přípony s předběžnými značkami, které mohou používat čísla s dvojitými číslicemi (nebo více), použijte úvodní nuly jako ve verzích beta. 01 a beta. 05, aby se zajistilo, že budou správně řazeny, když čísla získají větší hodnotu. Toto doporučení platí pouze pro původní schéma verze.
