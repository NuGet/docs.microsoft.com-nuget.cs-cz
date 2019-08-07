---
ms.openlocfilehash: e8949e9964ed19d342df53f08f59bb0f89e5feb0
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817477"
---
Identifikátor balíčku a číslo verze jsou dvě nejdůležitější hodnoty v projektu, protože jednoznačně identifikují přesný kód obsažený v balíčku.

**Osvědčené postupy pro identifikátor balíčku:**

- **Jedinečnost**: Identifikátor musí být jedinečný v rámci nuget.org nebo bez ohledu na to, jakou galerii hostují balíček. Než se rozhodnete pro identifikátor, vyhledejte příslušnou galerii a ověřte, jestli se tento název už používá. Aby nedocházelo ke konfliktům, dobrým vzorem je použít název vaší společnosti jako první část identifikátoru, například `Contoso.`.
- **Názvy podobných oborům názvů**: Sledujte vzor podobný oborům názvů v rozhraní .NET pomocí notace tečky namísto spojovníků. Použijte `Contoso.Utility.UsefulStuff` například `Contoso-Utility-UsefulStuff` místo nebo`Contoso_Utility_UsefulStuff`. Příjemci také naleznou užitečné, pokud se identifikátor balíčku shoduje s obory názvů použitými v kódu.
- **Ukázkové balíčky**: Pokud vytváříte balíček ukázkového kódu, který ukazuje, jak použít jiný balíček, připojte `.Sample` se jako přípona k identifikátoru, jako `Contoso.Utility.UsefulStuff.Sample`v. (Vzorový balíček samozřejmě má závislost na druhém balíčku.) Při vytváření ukázkového balíčku použijte `contentFiles` hodnotu v. `<IncludeAssets>` Ve složce uspořádejte vzorový kód do složky s názvem `\Samples\<identifier>` jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`. `content`

**Osvědčené postupy pro verzi balíčku:**

- Obecně platí, že nastavte verzi balíčku tak, aby odpovídala projektu (nebo sestavení), i když to není bezpodmínečně nutné. Toto je jednoduchá skutečnost při omezení balíčku na jediné sestavení. Celkově mějte na paměti, že aplikace NuGet pracuje s verzemi balíčku při řešení závislostí, nikoli ve verzích sestavení.
- Při použití nestandardního schématu verzí nezapomeňte zvážit pravidla správy verzí NuGet, jak je vysvětleno v tématu [Správa verzí balíčků](../../reference/package-versioning.md). NuGet je většinou [kompatibilní s semver 2](../../reference/package-versioning.md#semantic-versioning-200).

> Informace o řešení závislostí najdete v tématu věnovaném [řešení závislostí s PackageReference](../../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Starší informace, které mohou být užitečné také pro lepší pochopení správy verzí, najdete v této sérii příspěvků na blogu.
>
> - [Část 1: Přijetí na Hell knihovny DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Část 2: Základní algoritmus](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Část 3: Sjednocení pomocí přesměrování vazeb](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)