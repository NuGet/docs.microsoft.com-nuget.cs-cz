---
title: Vytvoření lokalizovaných balíčků NuGet
description: Podrobnosti o dva způsoby vytvoření lokalizovaných balíčků NuGet, včetně všechna sestavení v jediném balíčku nebo publikování samostatné sestavení.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: b1c2511c1fbafc7f52029c23521fa55671b0b5c5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546892"
---
# <a name="creating-localized-nuget-packages"></a>Vytvoření lokalizovaných balíčků NuGet

Existují dva způsoby vytvoření lokalizované verze knihovny:

1. Zahrňte všechna sestavení lokalizovaných prostředků v jediném balíčku.
1. Vytváření balíčků samostatné lokalizované satelitní podle striktní sadu pravidel.

Obě metody mají své výhody a nevýhody, jak je popsáno v následujících částech.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Sestavení lokalizovaných prostředků v jediném balíčku

Včetně sestavení lokalizovaných prostředků v jediném balíčku je obvykle nejjednodušším přístupem. K tomuto účelu vytváření složek v rámci `lib` pro podporovaný jazyk jiné než výchozí balíček (předpokládá, že en-us). V těchto složkách můžete umístit sestavení prostředků a lokalizované soubory XML technologie IntelliSense.

Například následující strukturu složek podporuje, němčina (de), italština (it), japonština (Japonsko), ruština (ru), čínština (zjednodušená) (zh-Hans) a čínština (tradiční) (zh-Hant):

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

Uvidíte, že jazyky jsou všechny uvedené pod `net40` cílové rozhraní framework složky. Pokud jste [podporuje více platforem](../create-packages/supporting-multiple-target-frameworks.md), pak máte složku ve složce `lib` pro každý typ variant.

Pomocí těchto složek na místě můžete odkázat na všechny soubory ve vašich `.nuspec`:

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

Jeden příklad balíčku, který používá tento přístup je [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Výhody a nevýhody (lokalizovaný prostředek sestavení)

Sdružování všechny jazyky v jediném balíčku má několik nevýhody:

1. **Sdílet metadata**: protože balíčku NuGet může obsahovat jenom jeden `.nuspec` soubor, můžete zadat metadata pouze jeden jazyk. To znamená NuGet není k dispozici podpora lokalizované metadat.
1. **Balíček velikost**: v závislosti na počtu podporovaných jazyků, knihovny, může být značně velké, což zpomalí instalace a obnovení balíčku.
1. **Souběžných verzí**: sdružování lokalizované soubory do jediného balíčku vyžaduje uvolnit všechny prostředky v tomto balíčku současně, namísto samostatně uvolnit každý lokalizace. Kromě toho kterákoli aktualizace jakékoli jeden lokalizaci vyžaduje novou verzi celý balíček.

Také má však několik výhod:

1. **Zjednodušení**: spotřebitele balíčku získat všechny podporované jazyky v jedna instalace, a nemusíte instalovat každý jazyk samostatně. Jeden balíček je také snazší najít na nuget.org.
1. **Verze s velkou provázaností**: vzhledem k tomu, že všechna sestavení prostředků jsou ve stejném balíčku jako primární sestavení, sdílejí stejné číslo verze a při spuštění riziko získávání chybně oddělení.

## <a name="localized-satellite-packages"></a>Lokalizovaná satelitní balíčky

Podobně jako způsob, jakým rozhraní .NET Framework podporuje satelitní sestavení, tato metoda odděluje lokalizované prostředky a soubory IntelliSense XML do satelitních balíčků.

To, jak, váš primární balíček používá konvence `{identifier}.{version}.nupkg` a obsahuje sestavení pro výchozí jazyk (třeba cs cz). Například `ContosoUtilities.1.0.0.nupkg` by obsahovala následující strukturu:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Satelitní sestavení pak používá konvence `{identifier}.{language}.{version}.nupkg`, jako například `ContosoUtilities.de.1.0.0.nupkg`. Identifikátor **musí** přesně odpovídat primární balíček.

Protože jde o samostatný balíček, má své vlastní `.nuspec` soubor, který obsahuje lokalizované metadat. Mějte na paměti, který jazyk `.nuspec` **musí** odpovídat tomu použitému v názvu souboru.

Satelitní sestavení **musí** zároveň deklarovat přesnou verzi primární balíčku jako závislost, pomocí zápisu verze [] \(viz [verze balíčku](../reference/package-versioning.md)). Například `ContosoUtilities.de.1.0.0.nupkg` musí deklarovat závislost na `ContosoUtilities.1.0.0.nupkg` pomocí `[1.0.0]` zápis. Balíček satelitní může samozřejmě mít jinou verzi číslo než primární balíček.

Struktura balíčku satelitní pak zahrnout sestavení prostředků a soubor XML IntelliSense do podsložky, která odpovídá `{language}` v názvu souboru balíčku:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Poznámka:**: není-li konkrétní subkultury jako `ja-JP` jsou nezbytné, vždy používejte identifikátor vyšší úrovně jazyka, jako je třeba `ja`.

Do satelitního sestavení NuGet rozpozná **pouze** tyto soubory ve složce, která odpovídá `{language}` v názvu souboru. Případné další se ignorují.

Pokud se splní všechny tyto konvence, NuGet rozpozná balíčku jako balíček satelitní a lokalizované soubory nainstalovat do primární balíček `lib` složky, jako by se měl byly spojeny původně. Odinstalovává se balíček satelitní odebere jeho souborů ze stejné složce.

Vytvoříte další satelitní sestavení stejným způsobem pro každý podporovaný jazyk. Příklad prozkoumejte sadu balíčků ASP.NET MVC:

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (anglické primární)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (němčina)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonština)
- [Microsoft.AspNet.Mvc.zh Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (čínština (zjednodušená))
- [Microsoft.AspNet.Mvc.zh Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (čínština (tradiční))

### <a name="summary-of-required-conventions"></a>Souhrnné informace o požadované konvence

- Primární balíček musí mít název. `{identifier}.{version}.nupkg`
- Satelitní balíčku musí mít název. `{identifier}.{language}.{version}.nupkg`
- Satelitní balíček `.nuspec` musíte zadat jeho jazyk tak, aby odpovídaly názvu souboru.
- Satelitní balíčku musí deklarovat závislost na přesnou verzi primární pomocí zápisu []. v jeho `.nuspec` souboru. Rozsahy nejsou podporovány.
- Satelitní balíčku musíte umístit soubory `lib\[{framework}\]{language}` složky, který přesně odpovídá `{language}` v názvu souboru.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Výhody a nevýhody (satelitní balíčky)

Použití balíčků satelitní má několik výhod:

1. **Balíček velikost**: je minimalizován celkový objem primární balíček a spotřebitelé pouze vám být naúčtovány náklady na jednotlivé jazyky, které chtějí používat.
1. **Samostatné metadat**: každý balíček satelitní má vlastní `.nuspec` soubor a proto lokalizované metadat protože. To umožňuje některé příjemce snadněji najít balíčků tak, že nuget.org lokalizované podmínek.
1. **Oddělené verze**: satelitní sestavení mohou být vydány v čase, nikoli všechny najednou, umožňuje rozprostřete vaše úsilí lokalizace.

Satelitní balíčků však mají své vlastní sadu nevýhody:

1. **Nepořádku**: místo jeden balíček, budete mít mnoho balíčků, které můžou vést k výsledkům nevypadala hledání na webech nuget.org a dlouhý seznam odkazů v projektu sady Visual Studio.
1. **Striktní konvence**. Satelitní balíčky musí konvence přesně nebo lokalizované verze nesmí být nenačítají správně.
1. **Správa verzí**: každý balíček satelitní musí mít závislost přesnou verzi na primární balíčku. To znamená, že aktualizace primární balíčku může vyžadovat aktualizaci všechny satelitní balíčky, i v případě, že prostředky nezměnila.
