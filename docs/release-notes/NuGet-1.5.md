---
title: Zpráva k vydání verze NuGet 1,5
description: Poznámky k verzi pro NuGet 1,5, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383346"
---
# <a name="nuget-15-release-notes"></a>Zpráva k vydání verze NuGet 1,5

[Poznámky k verzi nuget 1,4](../release-notes/nuget-1.4.md) | zpráva k [vydání verze NuGet 1,6](../release-notes/nuget-1.6.md)

NuGet 1,5 byl vydán 30. srpna 2011.

## <a name="features"></a>Funkce

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Šablony projektů s předinstalovanými balíčky NuGet
Při vytváření nové šablony projektu ASP.NET MVC 3 se ve vlastně umístění knihoven skriptů jQuery obsažených v projektu nainstalují balíčky NuGet.

Šablona projektu ASP.NET MVC 3 obsahuje sadu balíčků NuGet, které se instalují při vyvolání šablony projektu. Tato možnost zahrnout balíčky NuGet se šablonou projektu je teď funkcí NuGet, kterou může mít _každá_ šablona projektu teď možnost využít.

Další podrobnosti o této funkci najdete [v tomto blogovém příspěvku vývojářem této funkce](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Explicitní odkazy na sestavení

Přidání nového prvku `<references />`, který slouží k explicitnímu určení, která sestavení v rámci balíčku by měla být odkazována.

Například pokud přidáte následující:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Pak budou odkazy na `xunit.dll` a `xunit.extensions.dll` odkazovány z příslušné [podsložky Framework/profil](../reference/nuspec.md#explicit-assembly-references) složky `lib`, i když jsou ve složce jiná sestavení.

Pokud je tento element vynechán, použije se obvyklé chování, které má odkazovat na každé sestavení ve složce `lib`.

__K čemu se tato funkce používá?__

Tato funkce podporuje sestavení pouze pro dobu návrhu. Například při použití kontraktů kódu musí být sestavení kontraktu vedle sestavení modulu runtime, která se rozšiřují, aby je Visual Studio mohl najít, ale sestavení kontraktu by na ně neměla být odkazováno v projektu a neměla by být kopírována do složky `bin`.

Podobně lze funkci použít pro rozhraní testování částí, jako je například XUnit, které vyžadují, aby jejich nástroje byly umístěny vedle sestavení modulu runtime, ale vyloučeny z odkazů na projekt.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Přidání možnosti pro vyloučení souborů v souboru. nuspec
Element `<file>` v rámci `.nuspec` souboru lze použít k zahrnutí konkrétního souboru nebo sady souborů pomocí zástupného znaku. Pokud používáte zástupný znak, neexistuje žádný způsob, jak vyloučit určitou podmnožinu zahrnutých souborů. Předpokládejme například, že chcete všechny textové soubory ve složce s výjimkou konkrétního.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

K určení více souborů použijte středníky.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Případně můžete použít zástupnou kartu k vyloučení sady souborů, například všech záložních souborů.

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Odebrání balíčků pomocí dialogových oken pro odebrání závislostí
Při odinstalaci balíčku se závislostmi se zobrazí výzva NuGet umožňující odebrání závislostí balíčku spolu s balíčkem.

![Odebírají se závislé balíčky.](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>vylepšení příkazu `Get-Package`
Příkaz `Get-Package` nyní podporuje parametr `-ProjectName`. Příkaz

    Get-Package –ProjectName A

Zobrazí seznam všech balíčků nainstalovaných v projektu A.

### <a name="support-for-proxies-that-require-authentication"></a>Podpora proxy serverů, které vyžadují ověření
Při používání NuGet za proxy serverem, který vyžaduje ověření, NuGet se teď vyzve k zadání přihlašovacích údajů proxy serveru. Zadání přihlašovacích údajů umožňuje NuGet připojit se ke vzdálenému úložišti.

### <a name="support-for-repositories-that-require-authentication"></a>Podpora úložišť, která vyžadují ověření
NuGet teď podporuje připojení k [soukromým úložištím](../hosting-packages/local-feeds.md) , která vyžadují základní ověřování nebo ověřování NTLM.

V budoucí verzi se přidá podpora pro ověřování algoritmem Digest.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Vylepšení výkonu úložiště nuget.org
V galerii nuget.org jsme provedli několik vylepšení výkonu, aby se vytvářely výpisy balíčků a hledání rychleji.

### <a name="solution-dialog-project-filtering"></a>Filtrování projektu dialogu řešení
V dialogovém okně na úrovni řešení se po zobrazení výzvy k instalaci projektů zobrazí pouze projekty, které jsou kompatibilní s vybraným balíčkem.

### <a name="package-release-notes"></a>Poznámky k verzi balíčku
Balíčky NuGet teď zahrnují podporu pro poznámky k verzi. Poznámky k verzi se zobrazují jenom při prohlížení _aktualizací_ balíčku, takže nedávají smysl přidat ho do vaší první verze.

![Poznámky k verzi na kartě aktualizace](./media/manage-nuget-packages-release-notes.png)

Chcete-li přidat do balíčku poznámky k verzi, použijte nový prvek `<releaseNotes />` metadat v souboru NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>nuspec & ltfiles/vylepšení&gt;
Soubor `.nuspec` nyní umožňuje prázdný `<files />` prvek, který instruuje NuGet. exe, že neobsahuje žádný soubor v balíčku.

## <a name="bug-fixes"></a>Opravy chyb
Aktualizace NuGet 1,5 obsahovala celkem 107 pracovních položek. 103 z nich bylo označeno jako chyby.

Úplný seznam pracovních položek opravených v NuGet 1,5 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Opravy chyb zaznamenaly:

* [Problém 1273](http://nuget.codeplex.com/workitem/1273): provedli jsme `packages.config`ější správu verzí pomocí řazení balíčků abecedně a odebráním nadbytečného prázdného znaku.
* [Problém 844](http://nuget.codeplex.com/workitem/844): čísla verzí jsou nyní normalizována, aby `Install-Package 1.0` fungovala na balíčku s verzí `1.0.0`.
* [Problém 1060](http://nuget.codeplex.com/workitem/1060): při vytváření balíčku pomocí NuGet. exe příznak `-Version` Přepisuje `<version />` element.
