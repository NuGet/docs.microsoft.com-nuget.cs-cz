---
title: Postup vytvoření lokalizovaného balíčku NuGet
description: Podrobnosti o dvou způsobech vytvoření lokalizovaných balíčků NuGet, a to buď zahrnutím všech sestavení do jednoho balíčku, nebo publikováním samostatných sestavení.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: cb3f8a9df66f259b130996822f102c27636d5d2c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774760"
---
# <a name="creating-localized-nuget-packages"></a>Vytváření lokalizovaných balíčků NuGet

Existují dva způsoby, jak vytvořit lokalizované verze knihovny:

1. Zahrňte všechna lokalizovaná sestavení prostředků do jednoho balíčku.
1. Pomocí striktní sady konvencí vytvořte samostatné lokalizované satelitní balíčky.

Obě metody mají své výhody a nevýhody, jak je popsáno v následujících částech.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Lokalizovaná sestavení prostředků v jednom balíčku

Zahrnutí lokalizovaných sestavení prostředků do jednoho balíčku je obvykle nejjednodušší přístup. To uděláte tak, že vytvoříte složky v rámci `lib` pro jiný podporovaný jazyk, než je výchozí verze balíčku (předpokládá se en-us). V těchto složkách můžete umístit sestavení prostředků a lokalizované soubory XML technologie IntelliSense.

Například následující struktura složek podporuje, němčina (de), italština (IT), japonština (Japonsko), ruština (ru), čínština (zjednodušená) (zh-Hans) a čínština (tradiční) (zh-Hant):

```
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
```

Můžete vidět, že jsou všechny jazyky uvedené pod `net40` cílovou složkou rámce. Pokud [podporujete více platforem](../create-packages/supporting-multiple-target-frameworks.md), pak máte složku `lib` pro každou variantu.

V případě, že tyto složky jsou na místě, budete odkazovat na všechny soubory v `.nuspec` :

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

Jedním z ukázkových balíčků, které používají tento přístup, je [Microsoft. data. OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Výhody a nevýhody (lokalizovaná sestavení prostředků)

Sdružování všech jazyků v jednom balíčku má několik nevýhody:

1. **Sdílená metadata**: vzhledem k tomu, že balíček NuGet může obsahovat jenom jeden `.nuspec` soubor, můžete zadat metadata jenom pro jeden jazyk. To znamená, že NuGet nepodporuje lokalizovaná metadata.
1. **Velikost balíčku**: v závislosti na počtu jazyků, které podporujete, může být knihovna výrazně velká, což zpomaluje instalaci a obnovení balíčku.
1. **Současná vydání**: sdružování lokalizovaných souborů do jednoho balíčku vyžaduje, abyste všechny prostředky v tomto balíčku uvolnili současně, ale nedokázali uvolnit každou lokalizaci samostatně. Kromě toho jakákoli aktualizace na jednu lokalizaci vyžaduje novou verzi celého balíčku.

Má ale také několik výhod:

1. **Jednoduchost**: spotřebitelé balíčku získají všechny podporované jazyky v jediné instalaci, ale nemusíte instalovat jednotlivé jazyky samostatně. Jeden balíček je také snazší najít na nuget.org.
1. Spárované **verze**: vzhledem k tomu, že všechna sestavení prostředků jsou ve stejném balíčku jako primární sestavení, všichni sdílejí stejné číslo verze a nespouštějí riziko chybného odložení.

## <a name="localized-satellite-packages"></a>Lokalizované satelitní balíčky

Podobně jako .NET Framework podporuje satelitní sestavení, tato metoda odděluje lokalizované prostředky a soubory XML technologie IntelliSense do satelitních balíčků.

V takovém případě váš primární balíček používá zásady vytváření názvů `{identifier}.{version}.nupkg` a obsahuje sestavení pro výchozí jazyk (například en-us). Například `ContosoUtilities.1.0.0.nupkg` by obsahoval následující strukturu:

```
lib
└───net40
        ContosoUtilities.dll
        ContosoUtilities.xml
```

Satelitní sestavení potom používá konvence pojmenování, jako je například `{identifier}.{language}.{version}.nupkg` `ContosoUtilities.de.1.0.0.nupkg` . Identifikátor **musí** přesně odpovídat primárnímu balíčku.

Vzhledem k tomu, že se jedná o samostatný balíček, má vlastní `.nuspec` soubor, který obsahuje lokalizovaná metadata. Je třeba mít na vědomí, že jazyk v rozhraní `.nuspec` **musí** odpovídat názvu použitému v souboru filename.

Satelitní sestavení **musí** také deklarovat přesnou verzi primárního balíčku jako závislost pomocí zápisu verze [] (viz [Správa verzí balíčku](../concepts/package-versioning.md)). Například `ContosoUtilities.de.1.0.0.nupkg` musí deklarovat závislost na `ContosoUtilities.1.0.0.nupkg` používání `[1.0.0]` zápisu. Satelitní balíček může samozřejmě mít jiné číslo verze než primární balíček.

Struktura satelitního balíčku musí poté zahrnovat sestavení prostředků a soubor XML IntelliSense do podsložky, která odpovídá `{language}` názvu souboru balíčku:

```
lib
└───net40
    └───de
            ContosoUtilities.resources.dll
            ContosoUtilities.xml
```

**Poznámka**: Pokud konkrétní subjazykové verze, jako `ja-JP` jsou třeba, jsou nutné, vždy používejte identifikátor jazyka vyšší úrovně, například `ja` .

V satelitním sestavení NuGet rozpozná **pouze** soubory ve složce, které odpovídají `{language}` názvu souboru. Všechny ostatní jsou ignorovány.

Když jsou splněné všechny tyto konvence, NuGet rozpozná balíček jako satelitní balíček a nainstaluje lokalizované soubory do složky primárního balíčku `lib` , jako kdyby byly původně zabalené. Odinstalováním satelitního balíčku dojde k odebrání souborů ze stejné složky.

Vytvořili byste Další satelitní sestavení stejným způsobem pro každý podporovaný jazyk. Podívejte se například na sadu balíčků ASP.NET MVC:

- [Microsoft. ASPNET. Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (angličtina – primární)
- [Microsoft.ASPNET.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (němčina)
- [Microsoft. ASPNET. Mvc. ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonština)
- [Microsoft. ASPNET. Mvc. zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (čínština (zjednodušená))
- [Microsoft. ASPNET. Mvc. zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (čínština (tradiční))

### <a name="summary-of-required-conventions"></a>Shrnutí požadovaných konvencí

- Primární balíček musí mít název. `{identifier}.{version}.nupkg`
- Satelitní balíček musí mít název. `{identifier}.{language}.{version}.nupkg`
- Satelitní balíček `.nuspec` musí určovat svůj jazyk tak, aby odpovídal názvu souboru.
- Satelitní balíček musí deklarovat závislost na přesnou verzi primárního objektu pomocí zápisu [] v jeho `.nuspec` souboru. Rozsahy nejsou podporovány.
- Satelitní balíček musí umístit soubory do `lib\[{framework}\]{language}` složky, která přesně odpovídá `{language}` názvu souboru.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Výhody a nevýhody (satelitní balíčky)

Použití satelitních balíčků má několik výhod:

1. **Velikost balíčku**: celkové nároky na primární balíček se minimalizují a spotřebitelé účtují jenom náklady na jednotlivé jazyky, které chtějí používat.
1. **Samostatná metadata**: každý satelitní balíček má vlastní `.nuspec` soubor, a proto jeho vlastní lokalizovaná metadata, protože. To může některým spotřebitelům dovolit snazší hledání balíčků tím, že prohledají nuget.org s lokalizovanými podmínkami.
1. **Oddělitelné verze**: satelitní sestavení lze uvolnit v průběhu času, nikoli všechny najednou, což vám umožní rozložit vaše lokalizace.

Nicméně satelitní balíčky mají svou vlastní sadu nevýhod:

1. **Zbytečných**: místo jednoho balíčku máte mnoho balíčků, které mohou vést k zbytečnému vyhledávání výsledků hledání v NuGet.org a dlouhému seznamu odkazů v projektu sady Visual Studio.
1. **Striktní konvence**. Satelitní balíčky musí přesně splňovat konvence nebo lokalizované verze nebudou správně vyzvednuty.
1. **Správa verzí**: každý satelitní balíček musí mít přesnou závislost verze v primárním balíčku. To znamená, že aktualizace primárního balíčku může vyžadovat aktualizaci všech satelitních balíčků i v případě, že se prostředky nezměnily.
