---
title: Poznámky k verzi 1.5 NuGet
description: Zpráva k vydání verze pro NuGet 1.5, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548722"
---
# <a name="nuget-15-release-notes"></a>Poznámky k verzi 1.5 NuGet

[Zpráva k vydání verze NuGet 1.4](../release-notes/nuget-1.4.md) | [zpráva k vydání verze NuGet 1.6](../release-notes/nuget-1.6.md)

NuGet 1.5 vydané 30. srpna 2011.

## <a name="features"></a>Funkce

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Šablony projektů s předinstalovanou NuGet balíčky
Při vytváření nové šablony projektu ASP.NET MVC 3, knihovny skriptů jQuery zahrnutý v projektu jsou ve skutečnosti tam umístili instalace balíčků NuGet.

Šablona projektu ASP.NET MVC 3 zahrnuje sadu balíčků NuGet, které se nainstalují při vyvolání šablony projektu. Tato možnost zahrnout balíčky NuGet pomocí šablony projektu je teď součástí balíčku nuget, který _jakékoli_ šablony projektu můžete nově využít výhod.

Další podrobnosti o této funkci najdete v tomto [příspěvek na blogu od vývojářů funkci](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Odkazy na explicitní sestavení

Přidat nový `<references />` použít k explicitnímu zadání sestavení, v rámci elementu balíček by se měla odkazovat.

Například přidejte následující:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Pak jenom `xunit.dll` a `xunit.extensions.dll` bude odkazovat z příslušné [framework nebo profil podsložky](../reference/nuspec.md#explicit-assembly-references) z `lib` složky, i když existují jiné sestavení ve složce.

Pokud tento prvek je vynechán, pak platí obvyklé chování, která má odkazovat na všechna sestavení v `lib` složky.

__Co tato funkce slouží?__

Tato funkce podporuje jenom sestavení doby návrhu. Například při použití kontrakty kódu, sestavení kontraktu musí být vedle sestavení modulu runtime, které se rozšiřují, aby sada Visual Studio můžete najít je, ale sestavení kontraktu nesmí odkazovat ve skutečnosti projekt a by neměl být zkopírována do `bin` složky.

Podobně tato funkce umožňuje pro rozhraní pro testování částí jako jsou XUnit, které potřebují jeho nástroje pro sestavení vedle sestavení modulu runtime, ale vyloučit z projektových odkazů.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Přidání možnosti vyloučit soubory souboru .nuspec
`<file>` v elementu `.nuspec` souboru je možné zahrnout určitý soubor nebo sady souborů pomocí zástupného znaku. Při použití zástupného znaku, neexistuje žádný způsob, jak vyloučit určitou podmnožinu zahrnuté soubory. Předpokládejme například, že chcete všechny textové soubory ve složce s výjimkou konkrétní skupinu.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Chcete-li zadat více souborů použijte středníky.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Nebo použijte zástupný znak pro vyloučení sadu souborů, jako jsou všechny záložní soubory

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Odebrání balíčků v dialogovém okně zobrazí výzvu k odebrání závislostí
Při odinstalaci balíčku se závislostmi, vyzve NuGet umožňuje odebrání závislosti balíčku společně s balíček.

![Odebrání závislé balíčky](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` zlepšení příkazu
`Get-Package` Příkaz nyní podporuje `-ProjectName` parametru. Takže příkaz

    Get-Package –ProjectName A

Zobrazí seznam všech balíčků nainstalovaných ve projekt A.

### <a name="support-for-proxies-that-require-authentication"></a>Podpora pro proxy servery, které vyžadují ověřování
Pokud používáte NuGet za proxy serverem, který vyžaduje ověření, NuGet teď zadání přihlašovacích údajů proxy serveru. Zadání přihlašovacích údajů umožňuje NuGet pro připojení k Vzdálené úložiště.

### <a name="support-for-repositories-that-require-authentication"></a>Podpora pro úložiště, které vyžadují ověřování
NuGet teď podporuje připojení k [soukromých úložišť](../hosting-packages/local-feeds.md) , které vyžadují základní ověřování nebo ověřování NTLM.

Podpora pro ověřování algoritmem Digest bude přidána v budoucí verzi.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Vylepšení výkonu pro úložiště nuget.org
Provedli jsme několik vylepšení výkonu v galerii nuget.org na balíček výpis a rychlejší hledání.

### <a name="solution-dialog-project-filtering"></a>Filtrování řešení dialogové okno projektu
V okně úrovni řešení při zobrazení výzvy ke jaké projekty k instalaci ukážeme pouze projekty, které jsou kompatibilní s vybraným balíčkem.

### <a name="package-release-notes"></a>Zpráva k vydání verze balíčku
Balíčky NuGet nyní zahrnují podporu pro zprávu k vydání verze. Poznámky k verzi zobrazit pouze až při zobrazení _aktualizace_ balíčku, proto nemá smysl přidat do vaší první verze.

![Zpráva k vydání verze v rámci kartu aktualizace](./media/manage-nuget-packages-release-notes.png)

Chcete-li přidat poznámky k verzi balíčku, použijte nové `<releaseNotes />` prvek metadat v souboru NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>souboru .nuspec & ltfiles /&gt; zlepšení
`.nuspec` Souboru teď umožňuje prázdný `<files />` element, který informuje nuget.exe nechcete zahrnout všechny soubory v balíčku.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.5 bylo celkem 107 pracovní položky opraveno. 103 z nich byly označeny jako chyby.

Úplný seznam pracovních položek opravených NuGet 1.5 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Opravy chyb za zmínku:

* [Problém 1273](http://nuget.codeplex.com/workitem/1273): provedené `packages.config` více verzí popisný řazení balíčky podle abecedy a odebráním prázdné znaky.
* [Problém 844](http://nuget.codeplex.com/workitem/844): čísla verzí se nyní normalizují tak, aby `Install-Package 1.0` funguje na balíček s verzí `1.0.0`.
* [Problém 1060](http://nuget.codeplex.com/workitem/1060): při vytváření balíčku pomocí nuget.exe, `-Version` příznak přepsání `<version />` elementu.
