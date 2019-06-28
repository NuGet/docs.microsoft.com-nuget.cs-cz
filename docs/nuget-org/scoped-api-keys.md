---
title: S vymezeným oborem klíče rozhraní API
description: Převzetí kontroly nad klíče rozhraní API, které používají tak, aby nabízel balíčky
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427500"
---
# <a name="scoped-api-keys"></a>S vymezeným oborem klíče rozhraní API

Chcete-li lépe zabezpečené prostředí pro distribuci balíčku NuGet, může převzít kontrolu nad klíči rozhraní API přidáním oborů.

Schopnost poskytovat nastavit obor na klíči rozhraní API poskytují lepší kontrolu rozhraní API. Můžete:

- Vytvoření více vymezených klíče rozhraní API, které lze použít pro jiné balíčky s různou časových rámců při vypršení platnosti.
- Získání klíčů rozhraní API zabezpečené.
- Upravte existující klíče rozhraní API, chcete-li změnit balíček použitelnosti.
- Aktualizovat nebo odstranit existující klíče rozhraní API bez bránících operací pomocí dalších klíčů.

## <a name="why-do-we-support-scoped-api-keys"></a>Proč podporujeme s vymezeným oborem klíče rozhraní API?

Podporujeme obory klíče rozhraní API vám umožní mít udělená oprávnění dál odstupňovat. Dříve NuGet nabízí jeden klíč rozhraní API pro účet a tento přístup má několik nevýhody:

- **Jeden klíč rozhraní API k řízení všech balíčků**. Pomocí jednoho klíče rozhraní API, který se používá ke správě všech balíčků je obtížné bezpečně sdílet klíč při více vývojářů, které jsou spojené s různými balíčky a při sdílení vydavatelského účtu.
- **Všechna oprávnění, nebo žádný**. Každý, kdo má přístup ke klíči rozhraní API má všechna oprávnění (publikovat, nabízených oznámení a zrušení seznamu) na balíčky. To je často žádoucí v prostředí s více týmy.
- **Jeden bod selhání**. Jeden klíč rozhraní API také znamená, že jediný bod selhání. Pokud klíče je ohrožena všech balíčků přidružených k účtu může potenciálně dojít k ohrožení. Aktualizovat klíč rozhraní API je jediný způsob, jak připojit nevracení paměti a předešlo výpadkům při pracovního postupu CI/CD. Kromě toho můžou nastat případy Pokud chcete odvolat přístup ke klíči rozhraní API pro jednotlivce (například když zaměstnanec odejde z organizace). Není čistý způsob, jak toto zpracování ještě dnes.

S klíči rozhraní API s vymezeným oborem Snažíme se vyřešit tyto problémy při a ujistěte se, že žádná z stávajících pracovních postupů přerušit.

## <a name="acquire-an-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Vytvoření s vymezeným oborem klíče rozhraní API

Můžete vytvořit víc klíčů rozhraní API na základě vašich požadavků. Klíč rozhraní API můžete použít jeden nebo více balíčků, mají různé obory, které udělují oprávnění a mají datum vypršení platnosti s ním spojená.

V následujícím příkladu máte klíč rozhraní API s názvem `Contoso service CI` , který můžete použít k balíčky pro konkrétní `Contoso.Service` balíčky a je platný 365 dní. Toto je typický scénář, kde jsou různé týmy v rámci stejné organizace prací na různých balíčcích a členy týmu k dispozici klíč, který uděluje oprávnění jen pro balíček, na kterém pracují. Vypršení platnosti slouží jako mechanismus, aby se zabránilo zastaralé či zapomenutí klíče.

![Vytvoření klíče rozhraní API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Použití glob vzory

Pokud pracujete ve více balíčků a máte dlouhý seznam balíčků pro správu, můžete pomocí vzorů podpory zástupných znaků vybrat více balíčků najednou. Například pokud budete chtít udělit konkrétní obory pro klíč pro všechny balíčky, jejichž ID začíná `Fabrikam.Service`, můžete to udělat tak, že zadáte `fabrikam.service.*` v **Glob vzor** textového pole.

![Vytvoření klíče rozhraní API](media/scoped-api-keys-glob-pattern.png)

Určit oprávnění klíče rozhraní API pomocí vzorů glob platí také pro nové balíčky pro odpovídající vzoru glob. Například, pokud se pokusíte vložit nový balíček s názvem `Fabrikam.Service.Framework`, můžete to udělat pomocí klíče vytvořili dříve, protože balíček shoduje se vzorem glob `fabrikam.service.*`.

## <a name="obtain-api-keys-securely"></a>Získání klíčů rozhraní API zabezpečené

Pro zabezpečení, nově vytvořený klíč se nikdy zobrazí na obrazovce a je k dispozici používání jenom **kopírování** tlačítko. Podobně klíč není přístupný, po aktualizaci stránky.

![Vytvoření klíče rozhraní API](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Upravit existující klíče rozhraní API

Můžete také aktualizovat oprávnění ke klíči a obory beze změny vlastního klíče. Pokud máte klíč s konkrétní rozsahy pro jeden balíček, můžete použít stejné rozsahy na jeden nebo více balíčků.

![Vytvoření klíče rozhraní API](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Aktualizovat nebo odstranit existující klíče rozhraní API

Vlastník účtu můžete klíč aktualizovat, v takovém případě oprávnění (balíčky), oboru a vypršení platnosti zůstanou stejné, ale nový klíč vystaven, provádění nepoužitelné starý klíč. To je užitečné při správě zastaralé klíče, nebo pokud neexistuje žádné riziko úniku klíče rozhraní API.

![Vytvoření klíče rozhraní API](media/scoped-api-keys-refresh.png)

Můžete také odstranit tyto klíče, pokud už nejsou potřeba. Odstraňuje se klíč odebere klíč a zpřístupňuje je nepoužitelné.

## <a name="faqs"></a>Nejčastější dotazy

### <a name="what-happens-to-my-old-legacy-api-key"></a>Co se stane staré (starší verze) klíč rozhraní API?

Váš klíč rozhraní API (starší verze) i nadále fungovat a může fungovat, dokud jej chcete pracovat. Ale tyto klíče budou dostupné jenom Pokud nebyly byly použity na více než 365 dnů tak, aby nabízel balíčku. Další podrobnosti najdete v blogovém příspěvku [změny u nichž vyprší platnost klíče rozhraní API](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Jste již nemůže aktualizovat tento klíč. Budete muset odstranit starší verze klíče a místo toho vytvořte nový klíč s vymezeným oborem.

> [!NOTE]
> Tento klíč má všechna oprávnění pro všechny balíčky a nikdy nevyprší. Měli byste zvážit odstranění tohoto klíče a vytvoření nových klíčů s s vymezeným oborem oprávnění a jednoznačného vypršení platnosti.

### <a name="how-many-api-keys-can-i-create"></a>Kolik klíčů rozhraní API můžete vytvořit?

Neexistuje žádné omezení počtu klíčů rozhraní API, které lze vytvořit. Ale doporučujeme vám zajistit jeho na spravovat počet tak, že není tím, že mají mnoho zastaralé klíče s žádné informace o umístění a kdo je používá.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Můžete odstranit Moje starší verze klíč rozhraní API nebo můžete přestat používat nyní?

Ano. Je možné – a pravděpodobně by měl – odstranit klíč rozhraní API starší verze.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Získat zpět Můj klíč rozhraní API, který byl odstraněn omylem?

Ne. Po odstranění můžete pouze vytvářet nové klíče. Je možné omylem odstraněné klíče bez obnovení.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Dál starý klíč rozhraní API pro práci po aktualizaci klíče rozhraní API?

Ne. Po aktualizaci klíč se získá generovat nový klíč, který má stejný obor, oprávnění a vypršení platnosti jako měl ten starý. Starý klíč přestane existovat.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Můžete udělit další oprávnění k existující klíč rozhraní API?

Nelze měnit obor, ale můžete upravit seznam balíčků, které se vztahuje na.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Jak poznám, že pokud některé zkratky vypršela nebo získávání buď vypršela platnost?

Pokud vyprší platnost libovolné klávesy, můžeme vám dá vědět prostřednictvím zprávu s upozorněním v horní části stránky. Jsme také odeslat e-mailové upozornění pro vlastníka účtu deseti dnů před vypršením platnosti klíče tak, aby na něm může fungovat dobře předem.