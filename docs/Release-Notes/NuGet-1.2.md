---
title: NuGet 1.2 poznámky
description: Poznámky k verzi pro NuGet 1.2 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9267374775887889b063c844063988504a541a38
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 poznámky

[Poznámky k verzi NuGet 1.0 a 1.1](../release-notes/nuget-1.1.md) | [NuGet 1.3 poznámky k verzi](../release-notes/nuget-1.3.md)

Verze NuGet 1.2 byla vydána 30. března 2011.

## <a name="new-features"></a>Nové funkce

### <a name="framework-profile-support"></a>Podpora profilů Framework

Od začátku, NuGet podporována s knihovny cíle různé architektury. Ale nyní balíčky můžou obsahovat sestavení, která cílí na konkrétní profily, třeba profilu Windows Phone. Pokud chcete zacílit na konkrétní profil prostředí, připojte pomlčkou následuje zkratka profilu. Například pokud chcete zacílit SilverLight systémem Windows Phone (neboli Windows Phone 7), můžete umístit sestavení ve složce sl3 wp, jak ukazuje následující snímek obrazovky.

![Rozložení složky Framework profilu](./media/framework-profile-support.png)

Může požádat, proč jsme právě nevybral použít "wp7" jako moniker. V části jsme se očekává, že Windows Phone 7 může v budoucnu spustit na novější verzi programu Silverlight, které se budou zaměřovat v takovém případě budete muset být konkrétnější, o které framework profilu, můžete se.

### <a name="automatically-add-binding-redirects"></a>Automaticky přidána přesměrování vazby

Při instalaci balíčku s sestavení se silným názvem, NuGet nyní může zjišťovat případech, kde projekt vyžaduje vazby přesměrování, které mají být přidány do konfiguračního souboru aplikace project pro kompilaci a je přidá automaticky. Část 3 řady příspěvek blogu David Ebbo na verze NuGet s názvem "[sjednocení prostřednictvím vazby přesměruje](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" popisuje účel tuto funkci v další podrobnosti.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Určení Framework odkazy na sestavení (GAC)

V některých případech může balíček závisí na sestavení, které je v rozhraní .NET Framework. Přesněji řečeno není vždy nutné, aby příjemci vašeho balíčku referenční sestavení rozhraní. V některých případech je ale důležité, například když vývojář potřebuje kódu s typy v toto sestavení. Chcete-li použít vašeho balíčku. Nové `frameworkAssemblies` elementu, podřízený element elementu metadat, můžete zadat sadu `frameworkAssembly` elementy ukazující na sestavení rozhraní v mezipaměti GAC. Všimněte si důraz na sestavení rozhraní.
Tyto sestavení nejsou součástí vašeho balíčku, protože se předpokládá, že se na každý počítač v rámci rozhraní .NET Framework. V následující tabulce jsou uvedené atributy `frameworkAssembly` elementu.


|Atribut |Popis|
|----------------|-----------|
|**assemblyName**|*Požadované*. Název sestavení, například `System.Net`.|
|**targetFramework**|*Volitelné*. Umožňuje zadat název framework a profilu (nebo alias) toto sestavení rozhraní vztahující se k například "net40" nebo "sl4". Používá stejný formát popsané v [podpora více cílové rozhraní](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe je nyní možné ukládat přihlašovací údaje klíč rozhraní API

Při použití nástroje příkazového řádku nuget.exe, teď můžete SetApiKey příkaz pro uložení klíče rozhraní API. Tímto způsobem, nebude muset pokaždé, když push balíček je zadat. Další informace o ukládání klíče rozhraní API s nuget.exe [přečtěte si dokumentaci o publikování balíčku](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Balíček Průzkumníka
Balíček Průzkumníka aktualizoval na podporu NuGet 1.2. Další informace, podívejte se [poznámky k verzi balíčku Explorer](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Ostatní funkce opravy

V předchozím seznamu byly nejvíce patrné mnoho funkcí, které implementovali jsme a chyb, které vyřešili. Všechny ve všech implementována/vyřešili [59 pracovní položky](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) v této verzi.

## <a name="known-issues"></a>Známé problémy

* **1.2 balíček nekompatibilita**: vytvořené balíčky s nejnovější verzi nástroje příkazového řádku, nuget.exe (> 1.2) nebude fungovat se staršími verzemi doplněk NuGet VS (například 1.1). Pokud spustíte do chybovou zprávu oznamující něco o nekompatibilní schématu, používáte k této chybě. Aktualizujte prosím NuGet na nejnovější verzi.
* **Nekompatibilita NuGet.Server**: Pokud máte k interní NuGet kanálu pomocí projektu NuGet.Server, budete muset aktualizovat na nejnovější verzi NuGet.Server daného projektu.
* **Došlo k neshodě chyba podpis**: Pokud spustíte došlo k chybě během upgradu se zobrazí zpráva o podpis neshoda, musíte nejprve odinstalovat NuGet a nainstalujte ji. Položka je uvedena v našich [známé problémy stránky](../release-notes/known-issues.md) který obsahuje další podrobnosti. Problém pouze ovlivní spuštěné Visual Studio 2010 SP1 a verze NuGet 1.0 nainstalovaný, která je nesprávně podepsaná. Tato verze se pouze k dispozici, z webu CodePlex po krátkou dobu abyste tento problém by neměla mít vliv na příliš mnoho uživatelů.