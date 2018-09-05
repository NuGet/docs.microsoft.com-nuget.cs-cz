---
title: NuGet 1.2 poznámky
description: Zpráva k vydání verze pro NuGet 1.2, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b47f73c1c225540226d3780e17053427b8ea4a8a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545684"
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 poznámky

[Zpráva k vydání verze NuGet 1.0 a 1.1](../release-notes/nuget-1.1.md) | [zpráva k vydání verze NuGet 1.3](../release-notes/nuget-1.3.md)

NuGet 1.2 vydané 30. března 2011.

## <a name="new-features"></a>Nové funkce

### <a name="framework-profile-support"></a>Podpora profilů rozhraní Framework

Od samého začátku NuGet nepodporuje, s knihovnami cílit na různá rozhraní. Ale nyní balíčky můžou obsahovat sestavení, které se zaměřují na konkrétní profily, třeba profilu Windows Phone. Chcete-li cílit na konkrétní profil rozhraní, přidejte dash, za nímž následuje profilu – zkratka. Třeba zaměřit na programu SilverLight na Windows Phone (označuje se také jako Windows Phone 7), můžete vložit sestavení ve složce sl3 wp, jak je ukázáno na následujícím snímku obrazovky.

![Rozložení složky Framework profilu](./media/framework-profile-support.png)

Můžete pokládat proč jsme neměli používat "wp7" jako zástupný název prostě vybrat. V části jsme se předvídání, Windows Phone 7 může spustit v budoucnu novější verzi programu Silverlight, v takovém případě bude muset být konkrétnější informace, o které rozhraní profilování vám se budou zaměřovat.

### <a name="automatically-add-binding-redirects"></a>Automaticky přidat přesměrování vazby

Při instalaci balíčku s sestaveních se silným názvem, NuGet nyní může zjišťovat případy, kdy projekt vyžaduje, aby přidávané do konfiguračního souboru, aby se projekt ke kompilaci a automaticky přidat přesměrování vazby. Část 3 David Ebbo blogový příspěvek řady týkající se správy verzí NuGet s názvem "[sjednocení prostřednictvím vazby přesměruje](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" popisuje účel tuto funkci podrobněji.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Určení Framework odkazy na sestavení (GAC)

V některých případech může balíček závisí na sestavení, který je v rozhraní .NET Framework. Přesněji řečeno není vždy nutné, že příjemce balíčku odkazují na sestavení rozhraní framework. Ale v některých případech je důležité, například když vývojář potřebuje Chcete-li použít váš balíček psát kód s využitím typy v tomto sestavení. Nové `frameworkAssemblies` elementu, podřízený element elementu metadat umožňuje zadat sadu `frameworkAssembly` prvky odkazující na sestavení rozhraní Framework v mezipaměti GAC. Všimněte si důraz na sestavení rozhraní Framework.
Tato sestavení nejsou součástí vašeho balíčku, jak se budou považovat za na každém počítači, jako součást rozhraní .NET Framework. V následující tabulce jsou uvedeny atributy `frameworkAssembly` elementu.


|Atribut |Popis|
|----------------|-----------|
|**assemblyName**|*Vyžaduje*. Název sestavení, jako například `System.Net`.|
|**targetFramework**|*Volitelné*. Umožňuje zadat název rozhraní framework a profil (nebo alias), která se toto rozhraní framework sestavení použije jako je například "net40" nebo "sl4". Používá stejný formát je popsáno v [podpora více cílových platforem](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe je nyní schopen ukládání přihlašovacích údajů, klíč rozhraní API

Při použití nástroje příkazového řádku nuget.exe, můžete nyní použít příkaz SetApiKey ukládat svůj klíč rozhraní API. Díky tomu nebudete muset pokaždé, když nasdílíš změny balíčku je zadat. Podrobné informace o ukládání svůj klíč rozhraní API s nuget.exe [, přečtěte si dokumentaci o publikování balíčku](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Průzkumník balíčků
Aktualizovali jsme Průzkumníku balíčků do podpory NuGet 1.2. Další informace, podívejte se [zpráva k vydání verze Průzkumníku balíčků](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Další funkce a opravy

Předchozím seznamu se nejvíce patrné mnoho funkcí, které jsme implementovali a chyb, které jsme opravili. Můžeme implementovat/fixed [59 pracovní položky](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) v této verzi.

## <a name="known-issues"></a>Známé problémy

* **1.2 balíček nekompatibility**: balíčky sestavené pomocí nejnovější verze nástroje příkazového řádku, nuget.exe (> 1.2) nebude fungovat se staršími verzemi doplněk NuGet VS (například 1.1). Pokud narazíte na chybovou zprávu s informacemi o tom něco o nekompatibilní schématu, používáte k této chybě. Aktualizujte NuGet na nejnovější verzi.
* **Nekompatibilita NuGet.Server**: hostuješ interní NuGet informačního kanálu pomocí aplikace NuGet.Server project, budete muset aktualizovat na nejnovější verzi NuGet.Server tohoto projektu.
* **Chyba Neshoda podpisu**: Pokud narazíte na chybu během upgradu a zobrazí se zpráva o podpis neshoda, musíte nejprve odinstalovat NuGet a nainstalujte ji. Je uvedena v našich [známé problémy v sadě stránky](../release-notes/known-issues.md) který poskytuje další podrobnosti. Problém pouze ovlivňuje spuštěné Visual Studio 2010 SP1 a verze NuGet 1.0 nainstalované, který byl nesprávně podepsané. Tato verze byla pouze k dispozici z webu CodePlex během krátké doby tak tento problém by neměla mít vliv na příliš mnoho lidí.