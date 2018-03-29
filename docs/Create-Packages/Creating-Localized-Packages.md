---
title: Vytvoření lokalizovaných balíčků NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Podrobnosti o dva způsoby vytvoření lokalizované balíčky NuGet, včetně všech sestaveních ve jeden balíček nebo publikování samostatné sestavení.
keywords: Lokalizace balíčku NuGet, NuGet satelitní sestavení, vytvoření lokalizovaných balíčků NuGet lokalizace konvence
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 39ff6d300ec1a1f7941cad5953599f25f55117f4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="creating-localized-nuget-packages"></a>Vytvoření lokalizovaných balíčků NuGet

Existují dva způsoby vytvoření lokalizované verze knihovny:

1. Zahrňte všechna sestavení lokalizované prostředky jeden balíček.
1. Vytvořte balíčky samostatném lokalizovaná satelitní o striktní sadu pravidel.

Obě metody mít jejich výhody a nevýhody, jak je popsáno v následujících částech.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Lokalizovaný prostředek sestavení v jeden balíček

Včetně lokalizovaný prostředek sestavení v jednom balíčku je obvykle nejjednodušší přístup. K tomuto účelu vytváření složek v rámci `lib` pro podporovaný jazyk jiné než výchozí balíček (předpokládá, že en-us). V uvedených složkách můžete umístit prostředek sestavení a lokalizované soubory IntelliSense XML.

Například následující strukturu složek podporuje, němčina (de), italština (it), japonština (ja), ruština (ru), čínština (zjednodušená) (zh-Hans) a čínština (tradiční) (zh-Hant):

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

Uvidíte, že jazyky jsou všechny uvedené pod `net40` cílové složce framework. Pokud jste [podpora více rozhraní](../create-packages/supporting-multiple-target-frameworks.md), pak máte složku ve složce `lib` pro každý typ variant.

Pomocí těchto složek na místě, pak odkazovat všechny soubory ve vašem `.nuspec`:

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

Jeden balíček příklad, který používá tento přístup je [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Výhody a nevýhody (lokalizovaný prostředek sestavení)

Sdružování všechny jazyky do jednoho balíčku má několik nevýhody:

1. **Sdílené metadata**: vzhledem k tomu, že balíček NuGet může obsahovat pouze jeden `.nuspec` souboru, můžete zadat metadata pouze jeden jazyk. To znamená NuGet nemá k dispozici podpora lokalizované metadat.
1. **Velikost balíčku**: v závislosti na počet jazyků, které podporujete, knihovně, může být výrazně velký, což zpomalí instalace a obnovení balíčku.
1. **Souběžné verze**: sdružování lokalizované soubory do jednoho balíčku vyžaduje verzi všechny prostředky v tomto balíčku současně, místo bude možné verze jednotlivých lokalizace samostatně. Kromě toho jakékoliv aktualizace jakékoli jeden lokalizace vyžaduje novou verzi celý balíček.

Však také má několik výhod:

1. **Jednoduchost**: příjemci balíčku získat všechny podporované jazyky v jedné instalaci, namísto nutnosti instalovat samostatně jednotlivé jazyky. Snazší najít v nuget.org je také jeden balíček.
1. **Doplněná verze**: vzhledem k tomu, že jsou všechny sestavení prostředků ve stejném balíčku jako primární sestavení, všechny sdílet stejné číslo verze a nespouštět riziko získávání chybnou informací odpojené.

## <a name="localized-satellite-packages"></a>Lokalizovaná satelitní balíčky

Podobně jako na tom, jak rozhraní .NET Framework podporuje satelitní sestavení, tato metoda odděluje lokalizované prostředky a soubory IntelliSense XML do balíčků satelit.

Do tohoto, váš primární balíček použije zásady vytváření názvů `{identifier}.{version}.nupkg` a obsahuje sestavení pro výchozí jazyk (například en US). Například `ContosoUtilities.1.0.0.nupkg` by obsahovat následující strukturou:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Satelitní sestavení pak používá zásady vytváření názvů `{identifier}.{language}.{version}.nupkg`, jako například `ContosoUtilities.de.1.0.0.nupkg`. Identifikátor **musí** přesně shodovat s primární balíčku.

Vzhledem k tomu je samostatný balíček, má svou vlastní `.nuspec` soubor, který obsahuje lokalizované metadat. Mějte na paměti, jazyk v `.nuspec` **musí** odpovídat používaný v názvu souboru.

Satelitní sestavení **musí** zároveň deklarovat přesnou verzi primární balíčku jako závislost, pomocí zápisu verze [] \(viz [verze balíčku](../reference/package-versioning.md)). Například `ContosoUtilities.de.1.0.0.nupkg` závislost na musí deklarovat `ContosoUtilities.1.0.0.nupkg` pomocí `[1.0.0]` zápis. Balíček satelitní můžou mít samozřejmě číslo jinou verzi než primární balíček.

Struktura satelitní balíček pak zahrnout sestavení prostředků a soubor XML IntelliSense podsložky, která odpovídá `{language}` v názvu souboru balíčku:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Poznámka:**: Pokud konkrétní subkultury jako `ja-JP` nezbytné, vždy použijte identifikátor vyšší úrovně jazyka, jako je třeba `ja`.

V satelitní sestavení, NuGet rozpozná **pouze** tyto soubory ve složce, která odpovídá `{language}` v názvu souboru. Všechny další se ignorují.

Pokud jsou splněny všechny tyto konvence, NuGet rozpozná balíček jako balíček satelitní a instalace lokalizované soubory do primární balíčku `lib` složky, jako kdyby měl byla původně sdružit do sady. Odinstalace balíčku satelitní odebere jeho soubory ze stejné složce.

Měli byste vytvořit další satelitní sestavení stejným způsobem pro každý podporovaný jazyk. Příklad zkontrolujte sadu rozhraní ASP.NET MVC balíčků:

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (anglické primární)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))
- [Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))

### <a name="summary-of-required-conventions"></a>Souhrn požadované konvence

- Primární balíček musí mít název. `{identifier}.{version}.nupkg`
- Satelitní balíček musí mít název. `{identifier}.{language}.{version}.nupkg`
- Satelitní balíček `.nuspec` musíte zadat jeho jazyk odpovídající název souboru.
- Satelitní balíčku musí deklarovat závislost na přesnou verzi systému primární notaci [] v jeho `.nuspec` souboru. Rozsahy nejsou podporovány.
- Satelitní balíčku musíte umístit soubory v `lib\[{framework}\]{language}` složky, který přesně odpovídá `{language}` v názvu souboru.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Výhody a nevýhody (satelitní balíčky)

Použití balíčků satelitní má několik výhod:

1. **Velikost balíčku**: celkové nároky na primární balíčku je minimalizován, a spotřebitelé pouze vynakládá jednotlivé jazyky, které chtějí používat.
1. **Samostatné metadata**: každý balíček satelitní má svou vlastní `.nuspec` soubor a proto jeho vlastní lokalizované metadata protože. To umožňuje snadno najít balíčků tak, že nuget.org s podmínkami lokalizované některé příjemcům.
1. **Odpojené verze**: satelitní sestavení, se uvolní v čase, nikoli všechny najednou, umožňuje šíření vaše snahy o lokalizaci.

Satelitní balíčky však mít vlastní sadu nevýhody:

1. **Zbytečné soubory**: místo jeden balíček, máte velký počet balíčků, které může vést k nepřehlednost výsledků na nuget.org a dlouhý seznam odkazů v projektu sady Visual Studio.
1. **Striktní konvence**. Satelitní balíčky musí přesně odpovídat daným nebo lokalizované verze nesmí být zachyceny správně.
1. **Správa verzí**: každý balíček satelitní musí mít přesnou verzi závislostí na primární balíčku. To znamená, že primární balíček aktualizace může vyžadovat aktualizaci všech balíčků satelitní taky i v případě, že prostředky nezměnil.
