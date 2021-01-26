---
title: Zpráva k vydání verze NuGet 1,2
description: Poznámky k verzi pro NuGet 1,2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: af2248a41800f7641be9b77d7bb72e2a94d4ce47
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777198"
---
# <a name="nuget-12-release-notes"></a>Zpráva k vydání verze NuGet 1,2

Poznámky k verzi [NuGet 1,0 a 1,1](../release-notes/nuget-1.1.md)  |  Zpráva k [vydání verze NuGet 1,3](../release-notes/nuget-1.3.md)

NuGet 1,2 byl vydán 30. března 2011.

## <a name="new-features"></a>Nové funkce

### <a name="framework-profile-support"></a>Podpora profilů architektury

Od začátku podporuje NuGet knihovny, které cílí na různé architektury. Balíčky teď ale můžou obsahovat sestavení, která cílí na konkrétní profily, jako je Windows Phone profil. Chcete-li cílit na konkrétní profil rozhraní, přidejte pomlčku následovaný zkratkou profilu. Chcete-li například cílit na SilverLight běžící na Windows Phone (označuje se také jako Windows Phone 7), můžete vložit sestavení do složky SL3-WP, jak je znázorněno na následujícím snímku obrazovky.

![Rozložení složky profilu architektury](./media/framework-profile-support.png)

Můžete se zeptat, proč jsme nechtěli použít jako moniker možnost "WP7". V některých případech předpokládáme, že Windows Phone 7 může v budoucnu běžet novější verze Silverlightu. v takovém případě může být nutné mít konkrétnější informace o tom, který profil rozhraní si určený.

### <a name="automatically-add-binding-redirects"></a>Automaticky přidat přesměrování vazby

Při instalaci balíčku se silnými pojmenovanými sestaveními teď může NuGet detekovat případy, kdy projekt vyžaduje, aby se do konfiguračního souboru přidaly přesměrování vazby, aby se projekt mohl kompilovat a přidat automaticky. 3. část davidch příspěvků na blogu Ebbo ve verzi NuGet s názvem "[sjednocení prostřednictvím přesměrování vazby](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" pokrývá účel této funkce ve více podrobnostech.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Zadání odkazů na sestavení rozhraní .NET Framework (GAC)

V některých případech může balíček záviset na sestavení, které je v .NET Framework. Výhradně řečeno, není vždy nutné, aby příjemce balíčku odkazoval na sestavení rozhraní. V některých případech je však důležité, například pokud vývojář potřebuje k psaní kódu v tomto sestavení kód, aby mohl váš balíček použít. Nový `frameworkAssemblies` prvek, podřízený element elementu metadata, umožňuje zadat sadu prvků, které `frameworkAssembly` odkazují na sestavení rozhraní v globální mezipaměti sestavení (GAC). Poznamenejte si zdůraznění sestavení rozhraní.
Tato sestavení nejsou součástí balíčku, protože se předpokládá, že jsou na každém počítači v rámci .NET Framework. V následující tabulce jsou uvedeny atributy `frameworkAssembly` prvku.


|Atribut |Popis|
|----------------|-----------|
|**Doplňk**|*Požadováno*. Název sestavení, například `System.Net` .|
|**targetFramework**|*Volitelné*. Povoluje zadání architektury a názvu profilu (nebo alias), který toto sestavení rozhraní používá, například "net40" nebo "sl4". Používá stejný formát popsaný v tématu [Podpora více cílových rozhraní](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe teď můžou ukládat přihlašovací údaje klíče rozhraní API.

Když použijete nástroj nuget.exe příkazového řádku, můžete teď použít příkaz SetApiKey k uložení klíče rozhraní API. Tímto způsobem je nebudete muset zadávat při každém vložení balíčku. Další podrobnosti o uložení klíče rozhraní API pomocí nuget.exe najdete [v dokumentaci k publikování balíčku](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Průzkumník balíčků
Průzkumník balíčků byl aktualizován tak, aby podporoval NuGet 1,2. Další informace najdete v [poznámkách k verzi Průzkumníka balíčků](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Další funkce/opravy

Předchozí seznam byl nejvýraznější z mnoha implementovaných funkcí a chyb, které jsme opravili. Vše všem jsme implementovali nebo opravili [59 pracovních položek](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) v této verzi.

## <a name="known-issues"></a>Známé problémy

* **1,2 nekompatibilita balíčku**: balíčky sestavené s nejnovější verzí nástroje příkazového řádku, nuget.exe (> 1,2), nebudou fungovat se staršími verzemi doplňku NuGet vs (například 1,1). Pokud narazíte na chybovou zprávu s oznámením o nekompatibilním schématu, zobrazí se tato chyba. Aktualizujte prosím NuGet na nejnovější verzi.
* **NuGet. nekompatibilita serveru**: Pokud Hostujte interní kanál NuGet pomocí projektu NuGet. Server, budete muset tento projekt aktualizovat na nejnovější verzi NuGet. Server.
* **Chyba neshody signatury**: Pokud při upgradu dojde k chybě se zprávou o neshodě signatur, musíte nejdřív odinstalovat NuGet a pak ho nainstalovat. Tato stránka je uvedena na [stránce známé problémy](../release-notes/known-issues.md) , která poskytuje další podrobnosti. Problém se týká pouze těch, na kterých běží aplikace Visual Studio 2010 SP1 a má nainstalovanou verzi NuGet 1,0, která byla nesprávně podepsaná. Tato verze byla k dispozici pouze na webu CodePlex po krátké době, takže tento problém by neměl mít vliv na příliš mnoho lidí.