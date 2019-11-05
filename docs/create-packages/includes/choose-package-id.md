---
ms.openlocfilehash: c92f6e0c34347ee8555d416140d95ea2df5a3fbb
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610557"
---
Identifikátor balíčku a číslo verze jsou dvě nejdůležitější hodnoty v projektu, protože jednoznačně identifikují přesný kód obsažený v balíčku.

**Osvědčené postupy pro identifikátor balíčku:**

- **Jedinečnost**: identifikátor musí být jedinečný v rámci NuGet.org nebo bez ohledu na to, jakou galerii hostují balíček. Než se rozhodnete pro identifikátor, vyhledejte příslušnou galerii a ověřte, jestli se tento název už používá. Aby nedocházelo ke konfliktům, dobrým vzorem je použít název vaší společnosti jako první část identifikátoru, například `Contoso.`.
- **Obor názvů jako názvy**: Sledujte vzor podobný oborům názvů v rozhraní .NET pomocí notace tečky namísto spojovníků. Použijte například `Contoso.Utility.UsefulStuff` místo `Contoso-Utility-UsefulStuff` nebo `Contoso_Utility_UsefulStuff`. Příjemci také naleznou užitečné, pokud se identifikátor balíčku shoduje s obory názvů použitými v kódu.
- **Ukázkové balíčky**: Pokud vytváříte balíček ukázkového kódu, který ukazuje, jak použít jiný balíček, připojte `.Sample` jako příponu k identifikátoru, jako v `Contoso.Utility.UsefulStuff.Sample`. (Vzorový balíček samozřejmě má závislost na druhém balíčku.) Při vytváření ukázkového balíčku použijte hodnotu `contentFiles` v `<IncludeAssets>`. Ve složce `content` uspořádejte vzorový kód do složky s názvem `\Samples\<identifier>` jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Osvědčené postupy pro verzi balíčku:**

- Obecně platí, že nastavte verzi balíčku tak, aby odpovídala projektu (nebo sestavení), i když to není bezpodmínečně nutné. Toto je jednoduchá skutečnost při omezení balíčku na jediné sestavení. Celkově mějte na paměti, že aplikace NuGet pracuje s verzemi balíčku při řešení závislostí, nikoli ve verzích sestavení.
- Při použití nestandardního schématu verzí nezapomeňte zvážit pravidla správy verzí NuGet, jak je vysvětleno v tématu [Správa verzí balíčků](../../concepts/package-versioning.md). NuGet je většinou [kompatibilní s semver 2](../../concepts/package-versioning.md#semantic-versioning-200).

> Informace o řešení závislostí najdete v tématu věnovaném [řešení závislostí s PackageReference](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference). Starší informace, které mohou být užitečné také pro lepší pochopení správy verzí, najdete v této sérii příspěvků na blogu.
>
> - [Část 1: pořízení Hell knihovny DLL](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Část 2: základní algoritmus](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Část 3: sjednocení pomocí přesměrování vazeb](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)
