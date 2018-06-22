---
title: Poznámky k verzi 1.5 verzi NuGet
description: Poznámky k verzi pro NuGet 1.5 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f2f7ebe718ce943faa31b7e19395eead8726648
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821340"
---
# <a name="nuget-15-release-notes"></a>Poznámky k verzi 1.5 verzi NuGet

[Poznámky k verzi NuGet 1.4](../release-notes/nuget-1.4.md) | [NuGet 1.6 poznámky k verzi](../release-notes/nuget-1.6.md)

NuGet 1.5 byla vydána 30 Srpen 2011.

## <a name="features"></a>Funkce

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Šablony projektů s předinstalovanými NuGet balíčky
Při vytváření nové šablony projektu ASP.NET MVC 3, knihovny skriptů jQuery zahrnutý v projektu ve skutečnosti tam umístili instalace balíčků NuGet.

Šablona projektu ASP.NET MVC 3 zahrnuje sadu balíčky NuGet, které budou instalovány při vyvolání šablona projektu. Tato schopnost mezi ně patřit balíčky NuGet pomocí šablony projektu je nyní funkce NuGet, _žádné_ šablona projektu teď můžete využít výhod.

Další podrobnosti o této funkci najdete v tématu to [příspěvku na blogu vývojáře funkce](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Odkazy na explicitní sestavení

Přidat novou `<references />` elementu použitého k explicitnímu zadání sestavení, v rámci na balíček by měl odkazovat.

Například přidejte následující:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Pak pouze `xunit.dll` a `xunit.extensions.dll` se bude odkazovat z příslušné [framework nebo profilu podsložky](../reference/nuspec.md#explicit-assembly-references) z `lib` složky, i když existují další sestavení ve složce.

Pokud tento element je tento parametr vynechán, pak platí obvyklé chování, která má odkazovat na všechna sestavení v `lib` složky.

__Co se tato funkce používá?__

Tato funkce podporuje pouze sestavení v době návrhu. Například při použití kontrakty kódu, kontrakt sestavení musí být vedle sestavení modulu runtime, která budou posílení, aby Visual Studio můžete je vyhledat, ale sestavení smlouvy nesmí odkazovat ve skutečnosti projektu a nesmí být zkopírován do `bin` složky.

Podobně tato funkce slouží k pro systémů testů jednotek, jako je například XUnit, které musí jeho nástroje pro sestavení vedle sestavení za běhu, ale vyloučené z odkazů projektu.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Přidání možnosti vyloučit soubory ve příponou .nuspec
`<file>` v rámci `.nuspec` soubor lze použít k zahrnutí konkrétní soubor nebo sadu souborů pomocí zástupného znaku. Pokud používáte zástupný znak, neexistuje žádný způsob, jak vyloučit určitou podmnožinu zahrnuté soubory. Předpokládejme například, že chcete všechny textových souborů ve složce s výjimkou některou.

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

Nebo vyloučit určitou sadu souborů, jako je například všechny záložní soubory použít zástupný znak

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Odebrání balíčků v dialogovém okně zobrazí výzvu k odebrání závislostí
Při odinstalaci balíčku se závislostmi, NuGet vyzve, povolení odebrání závislostí balíčků balíčku společně s.

![Odebrání závislých balíčků](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` příkaz zlepšování
`Get-Package` Příkaz teď podporuje `-ProjectName` parametr. Takže příkaz

    Get-Package –ProjectName A

Zobrazí seznam všech balíčky nainstalované v projektu A.

### <a name="support-for-proxies-that-require-authentication"></a>Podpora pro proxy servery, které vyžadují ověřování
Při použití NuGet za proxy server, který vyžaduje ověření, výzvou k zadání přihlašovacích údajů proxy teď NuGet. Zadání přihlašovacích údajů umožňuje NuGet pro připojení k Vzdálené úložiště.

### <a name="support-for-repositories-that-require-authentication"></a>Podpora pro úložiště, které vyžadují ověřování
NuGet teď podporuje připojení k [privátní úložiště](../hosting-packages/local-feeds.md) základní ověřování nebo ověřování NTLM, které vyžadují.

Podpora pro ověřování hodnotou hash bude přidán v budoucí verzi.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Vylepšení výkonu do úložiště nuget.org
Provedli jsme několik vylepšení výkonu do Galerie nuget.org do balíček výpis a rychlejší hledání.

### <a name="solution-dialog-project-filtering"></a>Řešení dialogovém okně projekt filtrování
V dialogu úrovni řešení při zobrazení výzvy ke jaké projekty k instalaci ukážeme pouze projekty, které jsou kompatibilní s vybraným balíčkem.

### <a name="package-release-notes"></a>Poznámky k verzi balíčku
Balíčky NuGet nyní zahrnují podporu pro poznámky k verzi. Poznámky k verzi jenom zobrazit si při prohlížení _aktualizace_ pro balíček, takže nemá smysl chcete přidat do první verzi.

![Poznámky k verzi v rámci kartu aktualizace](./media/manage-nuget-packages-release-notes.png)

Chcete-li přidat poznámky k verzi balíčku, použijte nové `<releaseNotes />` element metadata v souboru NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>příponou .nuspec & ltfiles /&gt; zlepšování
`.nuspec` Souboru teď umožňuje prázdný `<files />` element, který sděluje nuget.exe nechcete zahrnout všechny soubory v balíčku.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.5 měl celkem 107 pracovní položky, které jsou pevné. 103 těchto byly označeny jako chyby.

Úplný seznam pracovní položky pevná ve NuGet 1.5 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Opravy chyb vhodné poznamenat:

* [Problém 1273](http://nuget.codeplex.com/workitem/1273): provedené `packages.config` více verzí popisný abecedně řazení balíčky a odebrání navíc mezer.
* [Problém 844](http://nuget.codeplex.com/workitem/844): čísla verzí jsou nyní normalized tak, aby `Install-Package 1.0` funguje na balíček s verzí `1.0.0`.
* [Problém 1060](http://nuget.codeplex.com/workitem/1060): při vytváření balíčku pomocí nuget.exe, `-Version` příznak přepsání `<version />` elementu.
