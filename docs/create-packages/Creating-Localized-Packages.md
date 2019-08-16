---
title: Postup vytvoření lokalizovaného balíčku NuGet
description: Podrobnosti o dvou způsobech vytvoření lokalizovaných balíčků NuGet, a to buď zahrnutím všech sestavení do jednoho balíčku, nebo publikováním samostatných sestavení.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: dbc3781bd17f815c6b32fc70b275469337148f41
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488838"
---
# <a name="creating-localized-nuget-packages"></a>Vytváření lokalizovaných balíčků NuGet

Existují dva způsoby, jak vytvořit lokalizované verze knihovny:

1. Zahrňte všechna lokalizovaná sestavení prostředků do jednoho balíčku.
1. Pomocí striktní sady konvencí vytvořte samostatné lokalizované satelitní balíčky.

Obě metody mají své výhody a nevýhody, jak je popsáno v následujících částech.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Lokalizovaná sestavení prostředků v jednom balíčku

Zahrnutí lokalizovaných sestavení prostředků do jednoho balíčku je obvykle nejjednodušší přístup. To uděláte tak, že vytvoříte složky `lib` v rámci pro jiný podporovaný jazyk, než je výchozí verze balíčku (předpokládá se en-us). V těchto složkách můžete umístit sestavení prostředků a lokalizované soubory XML technologie IntelliSense.

Například následující struktura složek podporuje, němčina (de), italština (IT), japonština (Japonsko), ruština (ru), čínština (zjednodušená) (zh-Hans) a čínština (tradiční) (zh-Hant):

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

Můžete vidět, že jsou všechny jazyky uvedené pod `net40` cílovou složkou rámce. Pokud podporujete [více platforem](../create-packages/supporting-multiple-target-frameworks.md), pak máte složku `lib` pro každou variantu.

V případě, že tyto složky jsou na místě, budete odkazovat na všechny `.nuspec`soubory v:

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

Jedním z ukázkových balíčků, které používají tento přístup, je [Microsoft. data. OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Výhody a nevýhody (lokalizovaná sestavení prostředků)

Sdružování všech jazyků v jednom balíčku má několik nevýhody:

1. **Sdílená metadata**: Vzhledem k tomu, že balíček NuGet může obsahovat `.nuspec` jenom jeden soubor, můžete zadat metadata jenom pro jeden jazyk. To znamená, že NuGet nepodporuje lokalizovaná metadata.
1. **Velikost balíčku**: V závislosti na počtu jazyků, které podporujete, může být knihovna značně velká, což zpomaluje instalaci a obnovení balíčku.
1. **Současná vydání**: Sdružování lokalizovaných souborů do jednoho balíčku vyžaduje, abyste všechny prostředky v tomto balíčku uvolnili současně, ale nedokázali uvolnit každou lokalizaci samostatně. Kromě toho jakákoli aktualizace na jednu lokalizaci vyžaduje novou verzi celého balíčku.

Má ale také několik výhod:

1. **Jednoduchost**: Příjemci balíčku získají všechny podporované jazyky v jediné instalaci, ale nemusíte instalovat jednotlivé jazyky samostatně. Jeden balíček je také snazší najít na nuget.org.
1. **Společně**navázané verze: Vzhledem k tomu, že všechna sestavení prostředků jsou ve stejném balíčku jako primární sestavení, všichni sdílejí stejné číslo verze a nespouštějí riziko chybného odložení.

## <a name="localized-satellite-packages"></a>Lokalizované satelitní balíčky

Podobně jako .NET Framework podporuje satelitní sestavení, tato metoda odděluje lokalizované prostředky a soubory XML technologie IntelliSense do satelitních balíčků.

V takovém případě váš primární balíček používá zásady vytváření názvů `{identifier}.{version}.nupkg` a obsahuje sestavení pro výchozí jazyk (například en-us). Například `ContosoUtilities.1.0.0.nupkg` by obsahoval následující strukturu:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Satelitní sestavení potom používá konvence `{identifier}.{language}.{version}.nupkg`pojmenování, `ContosoUtilities.de.1.0.0.nupkg`jako je například. Identifikátor **musí** přesně odpovídat primárnímu balíčku.

Vzhledem k tomu, že se jedná o samostatný balíček, `.nuspec` má vlastní soubor, který obsahuje lokalizovaná metadata. Je třeba mít na vědomí, že `.nuspec` jazyk v rozhraní **musí** odpovídat názvu použitému v souboru filename.

Satelitní sestavení **musí** zároveň deklarovat přesnou verzi primární balíčku jako závislost, pomocí zápisu verze [] \(viz [verze balíčku](../concepts/package-versioning.md)). Například `ContosoUtilities.de.1.0.0.nupkg` musí deklarovat závislost na `ContosoUtilities.1.0.0.nupkg` používání `[1.0.0]` zápisu. Satelitní balíček může samozřejmě mít jiné číslo verze než primární balíček.

Struktura satelitního balíčku musí poté zahrnovat sestavení prostředků a soubor XML IntelliSense do podsložky, která odpovídá `{language}` názvu souboru balíčku:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Poznámka**: Pokud konkrétní subjazykové verze `ja-JP` , jako jsou třeba, jsou nutné, vždy používejte identifikátor `ja`jazyka vyšší úrovně, například.

V satelitním sestavení NuGet rozpozná **pouze** soubory ve složce, které odpovídají `{language}` názvu souboru. Všechny ostatní jsou ignorovány.

Když jsou splněné všechny tyto konvence, NuGet rozpozná balíček jako satelitní balíček a nainstaluje lokalizované soubory do `lib` složky primárního balíčku, jako kdyby byly původně zabalené. Odinstalováním satelitního balíčku dojde k odebrání souborů ze stejné složky.

Vytvořili byste Další satelitní sestavení stejným způsobem pro každý podporovaný jazyk. Podívejte se například na sadu balíčků ASP.NET MVC:

- [Microsoft. ASPNET. Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (angličtina – primární)
- [Microsoft.ASPNET.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (němčina)
- [Microsoft. ASPNET. Mvc. ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonština)
- [Microsoft. ASPNET. Mvc. zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (čínština (zjednodušená))
- [Microsoft. ASPNET. Mvc. zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (čínština (tradiční))

### <a name="summary-of-required-conventions"></a>Shrnutí požadovaných konvencí

- Primární balíček musí mít název.`{identifier}.{version}.nupkg`
- Satelitní balíček musí mít název.`{identifier}.{language}.{version}.nupkg`
- Satelitní balíček `.nuspec` musí určovat svůj jazyk tak, aby odpovídal názvu souboru.
- Satelitní balíček musí deklarovat závislost na přesnou verzi primárního objektu pomocí zápisu [] v jeho `.nuspec` souboru. Rozsahy nejsou podporovány.
- Satelitní balíček musí umístit soubory do `lib\[{framework}\]{language}` složky, která přesně odpovídá `{language}` názvu souboru.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Výhody a nevýhody (satelitní balíčky)

Použití satelitních balíčků má několik výhod:

1. **Velikost balíčku**: Celkové nároky na primární balíček se minimalizují a spotřebitelé účtují jenom náklady na jednotlivé jazyky, které chtějí použít.
1. **Samostatná metadata**: Každý satelitní balíček má vlastní `.nuspec` soubor, a proto jeho vlastní lokalizovaná metadata, protože. To může některým spotřebitelům dovolit snazší hledání balíčků tím, že prohledají nuget.org s lokalizovanými podmínkami.
1. **Oddělitelné verze**: Satelitní sestavení může být uvolněna v průběhu času, nikoli vše najednou, což vám umožní rozložit vaše lokalizace.

Nicméně satelitní balíčky mají svou vlastní sadu nevýhod:

1. **Nepotřebné**: Místo jednoho balíčku máte mnoho balíčků, které mohou vést k zbytečným výsledkům hledání v nuget.org a dlouhému seznamu odkazů v projektu sady Visual Studio.
1. **Striktní konvence**. Satelitní balíčky musí přesně splňovat konvence nebo lokalizované verze nebudou správně vyzvednuty.
1. **Správa verzí**: Každý satelitní balíček musí mít přesnou závislost verze v primárním balíčku. To znamená, že aktualizace primárního balíčku může vyžadovat aktualizaci všech satelitních balíčků i v případě, že se prostředky nezměnily.
