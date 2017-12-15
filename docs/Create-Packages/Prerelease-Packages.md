---
title: "Předběžné verze verze v balíčky NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df6a366a-22c1-47bb-8017-18231311ce88
description: "Pokyny pro vytváření předběžné verze balíčků"
keywords: "Správa verzí, verze balíčku NuGet, předprodejní verze NuGet, předběžné verze balíčků NuGet, verze balíčku preview, verze RC balíčku, Beta verze balíčku, sémantické verze NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 07cb9b9bdeeea6f283e95a11a06d7f2043c9b17c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="building-pre-release-packages"></a>Vytváření předběžné verze balíčků

Vždy, když uvolnění aktualizovaný balíček s nové číslo verze se považuje za NuGet než jako "nejnovější stabilní verze" jak je vidět, třeba v uživatelském rozhraní Správce balíčků ve Visual Studiu:

![Uživatelského rozhraní Správce balíčků zobrazující nejnovější stabilní verze](media/Prerelease_01-LatestStable.png)

Stabilní verze je ten, který je považován za dostatečně spolehlivé, který se má použít v produkčním prostředí. Nejnovější stabilní verze je také ten, který se nainstaluje jako aktualizace balíčku nebo při obnovování balíčků (vztahují omezení, jak je popsáno v [Reinstalling a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md)).

Pro podporu životního cyklu verze softwaru, NuGet 1.6 nebo novější umožňuje distribuci předběžné verze balíčků, kde se číslo verze obsahuje příponu sémantické verze, jako `-alpha`, `-beta`, nebo `-rc`. Další informace najdete v tématu [Správa verzí balíčku](../reference/package-versioning.md#pre-release-versions).

Tyto verze můžete určit dvěma způsoby:

- `.nuspec`soubor: zahrnují příponou sémantickou verzi v `version` element:

    ```xml
    <version>1.0.1-alpha</version>
    ```

- Atributů sestavení: při vytváření balíčků z projektu sady Visual Studio (`.csproj` nebo `.vbproj`), použijte `AssemblyInformationalVersionAttribute` k určení verze:

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    NuGet převezme tuto hodnotu namísto verze zadaná v `AssemblyVersion` atribut, který nepodporuje sémantické verze.

Až budete připraveni k uvolnění stabilní verze, právě odeberte příponu a balíček má přednost před všechny předprodejní verze. Znovu, najdete v části [Správa verzí balíčku](../reference/package-versioning.md#pre-release-versions).


## <a name="installing-and-updating-pre-release-packages"></a>Instalace a aktualizace předběžné verze balíčků

Ve výchozím nastavení NuGet nezahrnuje předprodejní verze při práci s balíčky, ale toto chování lze změnit takto:

- **Správce balíčků uživatelského rozhraní v sadě Visual Studio**: V **spravovat balíčky NuGet** uživatelského rozhraní, zkontrolujte **zahrnout předběžné verze** pole:

    ![Políčko zahrnout předběžné verze v sadě Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Nastavení nebo zrušíte zaškrtnutí tohoto políčka se aktualizuje uživatelské rozhraní Správce balíčků a seznam dostupných verzí, které můžete instalovat.

- **Konzola správce balíčků**: použití `-IncludePrerelease` přepínač s `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, a `Update-Package` příkazy. Odkazovat [referenční informace prostředí PowerShell](../tools/powershell-reference.md).

- **Rozhraní příkazového řádku NuGet**: použití `-prerelease` přepínač s `install`, `update`, `delete`, a `mirror` příkazy. Odkazovat [odkaz NuGet rozhraní příkazového řádku](../tools/nuget-exe-cli-reference.md)


## <a name="semantic-versioning"></a>Sémantické verze

[Sémantické verze nebo SemVer konvence](http://semver.org/spec/v1.0.0.html) popisuje, jak využívat řetězců v čísla verzí pro vyjádření jejich význam kódu.

V touto konvencí, každá verze má tři části `Major.Minor.Patch`, s následující význam:

- `Major`: Nejnovější změny
- `Minor`: Nové funkce, ale zpětně kompatibilní
- `Patch`: Zpětné opravy pouze kompatibilní chyb

Předběžné verze jsou pak odlišené připojování řetězec a pomlčka po číslo opravy. Technicky platí, že můžete použít * žádné * řetězec po pomlčku a NuGet bude považovat za balíček předběžné verze. Číslo plnou verzi NuGet pak zobrazí v uživatelském rozhraní použít, a spotřebitelé interpretovat význam sami.

Myslete na to je obvykle dobrou sledovat rozpoznaný zásady vytváření názvů jako je například následující:

- `-alpha`: Alfa verze, obvykle se používá pro práce v průběhu a experimentování
- `-beta`: Beta verze, obvykle ten, který je funkce dokončení další plánované verze, ale může obsahovat známé chyby.
- `-rc`: Release candidate, obvykle verzi, která je potenciálně konečné (stable), pokud vznikat významné chyby.

> [!Note]
> NuGet nepodporuje [SemVer kompatibilní (v2.0.0)](http://semver.org/spec/v2.0.0.html) předběžné verze čísla pomocí zápisu s tečkou, jako v `1.0.1-build.23`. Můžete použít formuláře jako `1.0.1-build23` , ale je vždy to předběžné verze.

Ať přípony, které používáte, ale NuGet získáte jejich prioritu ve vzestupném abecedním pořadí:

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta12
1.0.1-beta05
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
```

Jak je znázorněno, verze bez žádné přípony bude vždy přednost předběžné verze. Všimněte si také, že pokud používáte číselné přípony s předběžné verze značky, které můžou používat dvoumístných čísel (nebo více), použít úvodní nuly jako beta01 a beta05 zajistit, že budou řadit správně při získání větší čísla.
