---
title: Předběžné verze v balíčcích NuGet
description: Pokyny pro vytváření předprodejních balíčků
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610717"
---
# <a name="building-pre-release-packages"></a>Vytváření předprodejních balíčků

Při každém vydání aktualizovaného balíčku s novým číslem verze, NuGet považuje tento jeden jako "nejnovější stabilní verze", jak je znázorněno, například v ui Správce balíčků v rámci sady Visual Studio:

![UI Správce balíčků zobrazující nejnovější stabilní verzi](media/Prerelease_01-LatestStable.png)

Stabilní verze je taková, která je považována za dostatečně spolehlivou pro použití ve výrobě. Nejnovější stabilní verze je také ten, který bude nainstalován jako balíček aktualizace nebo během obnovení balíčku (s výhradou omezení, jak je popsáno v [přeinstalaci a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md)).

Pro podporu životního cyklu vydání softwaru umožňuje aplikace NuGet 1.6 a novější distribuci předběžných balíčků, kde číslo verze `-alpha`obsahuje `-beta`sémantickou příponu správy verzí, například , , nebo `-rc`. Další informace naleznete [v tématu Package versioning](../concepts/package-versioning.md#pre-release-versions).

Tyto verze můžete zadat jedním z následujících způsobů:

- **Pokud váš [`PackageReference`](../consume-packages/package-references-in-project-files.md)projekt používá **: zahrnout sémantické `.csproj` verze [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) přípony v prvku souboru:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Pokud má váš [`packages.config`](../reference/packages-config.md) projekt soubor:** zahrňte do [`.nuspec`](../reference/nuspec.md) [`version`](../reference/nuspec.md#version) prvku souboru příponu sémantické verze:

    ```xml
    <version>1.0.1-alpha</version>
    ```

Až budete připraveni vydat stabilní verzi, stačí odebrat příponu a balíček má přednost před všemi předběžnými verzemi. Znovu naleznete [v tématu Package versioning](../concepts/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Instalace a aktualizace předběžných verzí balíčků

Ve výchozím nastavení NuGet neobsahuje předběžné verze při práci s balíčky, ale můžete změnit toto chování následujícím způsobem:

- **UI Správce balíčků v sadě Visual Studio**: V **umělou spravovat nugetové balíčky** zaškrtněte políčko **Zahrnout předběžnou verzi:**

    ![Zaškrtávací políčko Zahrnout předběžnou verzi v sadě Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Nastavením nebo zrušením zaškrtnutí tohoto pole se aktualizuje ui Správce balíčků a seznam dostupných verzí, které můžete nainstalovat.

- **Konzola Správce**balíčků `-IncludePrerelease` : `Find-Package`Použijte `Get-Package` `Install-Package`přepínač `Sync-Package`s `Update-Package` příkazy , , , a příkazy. Odkazovat na [odkaz prostředí PowerShell](../reference/powershell-reference.md).

- **NuGet CLI**: `-prerelease` Použijte `install`přepínač `update` `delete`s `mirror` příkazy , , a. Odkazovat na [odkaz NuGet CLI](../reference/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Sémantická správa verzí

[Sémantické Versioning nebo SemVer konvence](https://semver.org/spec/v1.0.0.html) popisuje, jak využít řetězce v číslech verzí sdělit význam základního kódu.

V této úmluvě má každá `Major.Minor.Patch`verze tři části , s následujícím významem:

- `Major`: Nejnovější změny
- `Minor`: Nové funkce, ale zpětně kompatibilní
- `Patch`: Pouze opravy zpětně kompatibilních chyb

Předběžné verze jsou pak označeny připojením pomlčky a řetězce za číslo opravy. Technicky vzato můžete použít *libovolný* řetězec po pomlčka a NuGet bude považovat balíček jako předběžnou verzi. NuGet pak zobrazí číslo plné verze v příslušném ui, takže spotřebitelé interpretovat význam pro sebe.

S ohledem na to je obecně dobré dodržovat uznávané konvence pojmenování, například následující:

- `-alpha`: Alfa verze, obvykle používaná pro nedokončenou práci a experimentování
- `-beta`: Beta verze, obvykle taková, která je dokončena pro další plánovanou verzi, ale může obsahovat známé chyby.
- `-rc`: Release candidate, obvykle vydání, které je potenciálně konečné (stabilní), pokud se neobjeví významné chyby.

> [!Note]
> NuGet 4.3.0+ podporuje [sémantické versioning v2.0.0](https://semver.org/spec/v2.0.0.html), který podporuje pre-release čísla s tečkou zápisu, jako v `1.0.1-build.23`. Dot notace není podporována s Verzemi NuGet před 4.3.0. V dřívějších verzích NuGet můžete použít `1.0.1-build23` formulář, jako je, ale to bylo vždy považováno za předběžnou verzi.

Bez ohledu na přípony, které používáte, však NuGet jim dá přednost v obráceném abecedním pořadí:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

Jak je znázorněno, verze bez přípony bude mít vždy přednost před předběžnými verzemi.

Úvodní 0s nejsou potřeba s semver2, ale jsou se schématem staré verze. Pokud používáte číselné přípony s předprodejními značkami, které mohou používat dvouciferná čísla (nebo více), použijte úvodní nuly jako v beta.01 a beta.05, abyste zajistili, že se správně seřadí, když se čísla zvětší. Toto doporučení platí pouze pro schéma staré verze.
