---
ms.openlocfilehash: c92f6e0c34347ee8555d416140d95ea2df5a3fbb
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610557"
---
Identifikátor balíčku a číslo verze jsou dvě nejdůležitější hodnoty v projektu, protože jednoznačně identifikují přesný kód, který je obsažen v balíčku.

**Doporučené postupy pro identifikátor balíčku:**

- **Jedinečnost**: Identifikátor musí být jedinečný v celé nuget.org nebo v jakékoli galerii, která balíček hostuje. Než se rozhodnete pro identifikátor, vyhledejte v příslušné galerii, zda je název již používán. Chcete-li se vyhnout konfliktům, je dobrým vzorem použití názvu společnosti `Contoso.`jako první části identifikátoru, například .
- **Názvy podobné oboru názvů**: Postupujte podle vzoru podobného oborům názvů v rozhraní .NET pomocí tečkového zápisu místo spojovníků. Například použijte `Contoso.Utility.UsefulStuff` spíše `Contoso-Utility-UsefulStuff` `Contoso_Utility_UsefulStuff`než nebo . Spotřebitelé také najít užitečné, když identifikátor balíčku odpovídá obory názvů používané v kódu.
- **Ukázkové balíčky**: Pokud vytvoříte balíček ukázkový kód, `.Sample` který ukazuje, jak používat jiný `Contoso.Utility.UsefulStuff.Sample`balíček, připojte jako příponu k identifikátoru, jako v . (Ukázkový balíček by samozřejmě měl závislost na druhém balíčku.) Při vytváření ukázkového balíčku `contentFiles` použijte `<IncludeAssets>`hodnotu v . Ve `content` složce uspořádejte ukázkový `\Samples\<identifier>` kód `\Samples\Contoso.Utility.UsefulStuff.Sample`do složky volané jako v .

**Doporučené postupy pro verzi balíčku:**

- Obecně nastavte verzi balíčku tak, aby odpovídala projektu (nebo sestavení), i když to není nezbytně nutné. Jedná se o jednoduchou záležitost, když omezíte balíček na jedno sestavení. Celkově nezapomeňte, že NuGet sám se zabývá verze balíčků při řešení závislostí, nikoli verze sestavení.
- Při použití nestandardní verze schématu, nezapomeňte zvážit NuGet pravidla správy verzí, jak je vysvětleno v [package versioning](../../concepts/package-versioning.md). NuGet je většinou [semver 2 kompatibilní](../../concepts/package-versioning.md#semantic-versioning-200).

> Informace o rozlišení závislostí naleznete v [tématu Řešení závislostí s PackageReference](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference). Pro starší informace, které mohou být také užitečné pro lepší pochopení správy verzí, naleznete v této sérii blogových příspěvků.
>
> - [Část 1: Převzetí DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Část 2: Základní algoritmus](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Část 3: Sjednocení prostřednictvím závazných přesměrování](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)
