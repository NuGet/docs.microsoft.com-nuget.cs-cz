---
title: Jak vytvořit lokalizovaný balíček NuGet
description: Podrobnosti o dvou způsobech vytvoření lokalizovaných balíčků NuGet, buď zahrnutím všech sestavení do jednoho balíčku nebo publikováním samostatných sestavení.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610943"
---
# <a name="creating-localized-nuget-packages"></a>Vytváření lokalizovaných balíčků NuGet

Existují dva způsoby, jak vytvořit lokalizované verze knihovny:

1. Zahrnout všechna sestavení lokalizovaných prostředků do jednoho balíčku.
1. Vytvořte samostatné lokalizované satelitní balíčky podle přísné sady konvencí.

Obě metody mají své výhody a nevýhody, jak je popsáno v následujících částech.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Lokalizovaná sestavení prostředků v jednom balíčku

Zahrnutí lokalizovaných sestavení prostředků do jednoho balíčku je obvykle nejjednodušší přístup. Chcete-li to provést, vytvořte složky v rámci `lib` podporovaného jazyka než výchozího balíčku (předpokládá se en-us). V těchto složkách můžete umístit sestavení prostředků a lokalizované soubory XML Technologie IntelliSense.

Například následující struktura složek podporuje, němčina (de), italština (it), japonština (ja), ru), čínština (zjednodušená) (zh-Hans) a čínština (tradiční) (zh-Hant):

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

Můžete vidět, že všechny jazyky `net40` jsou uvedeny pod složky cílové architektury. Pokud [podporujete více architektur](../create-packages/supporting-multiple-target-frameworks.md), pak máte složku `lib` pod pro každou variantu.

S těmito složkami na místě, pak `.nuspec`odkazovat na všechny soubory v :

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

Jeden příklad balíček, který používá tento přístup je [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Výhody a nevýhody (lokalizovaná sestavení prostředků)

Sdružování všech jazyků do jednoho balíčku má několik nevýhod:

1. **Sdílená metadata**: Vzhledem k tomu, že balíček NuGet může obsahovat pouze jeden `.nuspec` soubor, můžete poskytnout metadata pouze pro jeden jazyk. To znamená NuGet nepředstavuje podporu lokalizovaných metadat.
1. **Velikost balíčku**: V závislosti na počtu jazyků, které podporujete, může být knihovna značně velká, což zpomaluje instalaci a obnovení balíčku.
1. **Simultánní verze**: Sdružování lokalizovaných souborů do jednoho balíčku vyžaduje, abyste uvolnili všechny datové zdroje v tomto balíčku současně, místo toho, abyste mohli uvolnit každou lokalizaci samostatně. Kromě toho každá aktualizace jedné lokalizace vyžaduje novou verzi celého balíčku.

Má však také několik výhod:

1. **Jednoduchost**: Spotřebitelé balíčku získat všechny podporované jazyky v jedné instalaci, spíše než nutnost instalovat každý jazyk samostatně. Jeden balíček je také snazší najít na nuget.org.
1. **Vázané verze**: Vzhledem k tomu, že všechna sestavení prostředků jsou ve stejném balíčku jako primární sestavení, všechny sdílejí stejné číslo verze a nepředstavují riziko chybného oddělení.

## <a name="localized-satellite-packages"></a>Lokalizované satelitní balíčky

Podobně jako rozhraní .NET Framework podporuje satelitní sestavení, tato metoda odděluje lokalizované prostředky a soubory IntelliSense XML do satelitních balíčků.

Proveďte to, primární balíček `{identifier}.{version}.nupkg` používá konvence pojmenování a obsahuje sestavení pro výchozí jazyk (například en US). Například `ContosoUtilities.1.0.0.nupkg` by obsahovat následující strukturu:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Satelitní sestavení pak používá `{identifier}.{language}.{version}.nupkg`konvence pojmenování , například `ContosoUtilities.de.1.0.0.nupkg`. Identifikátor **se musí** přesně shodovat s primárním balíčkem.

Protože se jedná o samostatný balíček, má vlastní `.nuspec` soubor, který obsahuje lokalizovaná metadata. Mějte na paměti, `.nuspec` že jazyk v **musí** odpovídat jazyk u použitého v názvu souboru.

Satelitní sestavení **musí** také deklarovat přesnou verzi primárního balíčku jako závislost pomocí zápisu verze [] (viz [Správa verzí balíčku).](../concepts/package-versioning.md) Například `ContosoUtilities.de.1.0.0.nupkg` musí deklarovat `ContosoUtilities.1.0.0.nupkg` závislost `[1.0.0]` na použití zápisu. Satelitní balíček může mít samozřejmě jiné číslo verze než primární balíček.

Struktura satelitního balíčku pak musí obsahovat sestavení prostředků a soubor Xml IntelliSense v podsložce, která odpovídá `{language}` názvu souboru balíčku:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Poznámka**: Pokud `ja-JP` jsou nezbytné určité subkultury, vždy používejte `ja`identifikátor jazyka vyšší úrovně, například .

V satelitním sestavení NuGet rozpozná **pouze** ty soubory `{language}` ve složce, která odpovídá v názvu souboru. Všechny ostatní jsou ignorovány.

Při splnění všech těchto konvencí, NuGet rozpozná balíček jako satelitní balíček a `lib` nainstaluje lokalizované soubory do složky primárního balíčku, jako by byly původně svázaný. Odinstalováním satelitního balíčku odeberete jeho soubory ze stejné složky.

Pro každý podporovaný jazyk byste vytvořili další satelitní sestavení stejným způsobem. Například zkontrolujte sadu ASP.NET balíčků MVC:

- [Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (angličtina primární)
- [Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (něm.)
- [Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonština)
- [Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (zjednodušená čínština))
- [Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (čínština (tradiční))

### <a name="summary-of-required-conventions"></a>Shrnutí požadovaných konvencí

- Primární balíček musí být pojmenován.`{identifier}.{version}.nupkg`
- Satelitní balíček musí být pojmenován`{identifier}.{language}.{version}.nupkg`
- Satelitní balíček `.nuspec` musí zadat svůj jazyk tak, aby odpovídal názvu souboru.
- Satelitní balíček musí deklarovat závislost na přesné verzi primární pomocí `.nuspec` [] zápisu v jeho souboru. Rozsahy nejsou podporovány.
- Satelitní balíček musí umístit `lib\[{framework}\]{language}` soubory do `{language}` složky, která přesně odpovídá názvu souboru.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Výhody a nevýhody (satelitní balíčky)

Použití satelitních balíčků má několik výhod:

1. **Velikost balíčku**: Celková stopa primárního balíčku je minimalizována a spotřebitelům vznikají pouze náklady na každý jazyk, který chtějí používat.
1. **Samostatná metadata**: Každý `.nuspec` satelitní balíček má svůj vlastní soubor a tím i vlastní lokalizovaná metadata, protože. To může umožnit některým spotřebitelům snadněji najít balíčky vyhledáním nuget.org s lokalizovanými termíny.
1. **Oddělené verze**: Satelitní sestavení mohou být uvolněna v průběhu času, nikoli všechny najednou, což vám umožní rozložit vaše lokalizační úsilí.

Nicméně, satelitní balíčky mají své vlastní sady nevýhod:

1. **Nepořádek**: Namísto jednoho balíčku máte mnoho balíčků, které mohou vést k přeplněným výsledkům hledání na nuget.org a dlouhý seznam odkazů v projektu sady Visual Studio.
1. **Přísné konvence**. Satelitní balíčky musí přesně dodržovat konvence, jinak lokalizované verze nebudou správně vyzvednuty.
1. **Správa verzí**: Každý satelitní balíček musí mít přesnou závislost verze na primárním balíčku. To znamená, že aktualizace primárního balíčku může vyžadovat také aktualizaci všech satelitních balíčků, a to i v případě, že se prostředky nezměnily.
