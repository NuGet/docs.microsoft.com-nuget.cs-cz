---
title: Klíče rozhraní API s vymezenou s rozsahem
description: Převzetí kontroly nad klíči rozhraní API, které používáte k nabízení balíčků
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427500"
---
# <a name="scoped-api-keys"></a>Klíče rozhraní API s vymezenou s rozsahem

Chcete-li NuGet bezpečnější prostředí pro distribuci balíčků, můžete převzít kontrolu klíčů rozhraní API přidáním oborů.

Možnost poskytnout rozsah klíčů rozhraní API vám lepší kontrolu nad rozhraníapi. Můžete:

- Vytvořte více klíčů rozhraní API s vymezeným oborem, které lze použít pro různé balíčky s různými časovými rámci vypršení platnosti.
- Získejte klíče rozhraní API bezpečně.
- Upravte existující klíče rozhraní API a změňte použitelnost balíčku.
- Aktualizujte nebo odstraňte existující klíče rozhraní API bez omezení operací pomocí jiných klíčů.

## <a name="why-do-we-support-scoped-api-keys"></a>Proč podporujeme klíče rozhraní API s rozsahem?

Podporujeme obory pro klíče rozhraní API, které vám umožní mít podrobnější oprávnění. Dříve NuGet nabídl jeden klíč rozhraní API pro účet a tento přístup měl několik nevýhod:

- **Jeden klíč rozhraní API pro řízení všech balíčků**. S jedním klíčem rozhraní API, který se používá ke správě všech balíčků, je obtížné bezpečně sdílet klíč, když více vývojářů jsou zapojeny s různými balíčky a když sdílejí účet vydavatele.
- **Všechna oprávnění nebo žádná**. Každý, kdo má přístup ke klíči rozhraní API, má všechna oprávnění (publikovat, tlačit a zrušit seznam) v balíčcích. To často není žádoucí v prostředí s více týmy.
- **Jediný bod selhání**. Jeden klíč rozhraní API také znamená jeden bod selhání. Pokud je klíč ohrožen, všechny balíčky přidružené k účtu může být potenciálně ohrožena. Aktualizace klíče rozhraní API je jediný způsob, jak připojit nevracení a zabránit přerušení pracovního postupu CI/CD. Kromě toho mohou existovat případy, kdy chcete odvolat přístup ke klíči rozhraní API pro jednotlivce (například když zaměstnanec opustí organizaci). Dnes neexistuje žádný čistý způsob, jak to zvládnout.

S rozsahem klíče rozhraní API, snažíme se řešit tyto problémy a zároveň se ujistěte, že žádný z existujících pracovních postupů přerušit.

## <a name="acquire-an-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Vytvoření klíčů rozhraní API s vymezenou montou s vymezenou monto

Můžete vytvořit více klíčů rozhraní API na základě vašich požadavků. Klíč rozhraní API lze použít pro jeden nebo více balíčků, mají různé obory, které udělují určitá oprávnění a mají datum vypršení platnosti s ním spojené.

V následujícím příkladu máte klíč `Contoso service CI` rozhraní API s názvem, `Contoso.Service` který lze použít k nabízení balíčků pro konkrétní balíčky a je platný po dobu 365 dnů. Toto je typický scénář, kde různé týmy v rámci stejné organizace pracují na různých balíčcích a členové týmu jsou k dispozici klíč, který uděluje jim oprávnění pouze pro balíček, na kterém pracují. Vypršení platnosti slouží jako mechanismus, aby se zabránilo zastaralé nebo zapomenuté klíče.

![Vytvořit klíče rozhraní API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Použití glob vzory

Pokud pracujete na více balíčcích a máte velký seznam balíčků ke správě, můžete použít globbing vzory vybrat více balíčků dohromady. Chcete-li například udělit určité obory klíči pro všechny `Fabrikam.Service`balíčky, jejichž ID `fabrikam.service.*` začíná , můžete to provést zadáním do textového pole **Vzor Glob.**

![Vytvořit klíče rozhraní API](media/scoped-api-keys-glob-pattern.png)

Použití glob vzory k určení oprávnění klíče rozhraní API platí také pro nové balíčky odpovídající glob vzor. Například pokud se pokusíte push `Fabrikam.Service.Framework`nový balíček s názvem , můžete to udělat s `fabrikam.service.*`klíčem vytvořeným dříve, protože balíček odpovídá glob vzor .

## <a name="obtain-api-keys-securely"></a>Bezpečné získání klíčů rozhraní API

Z bezpečnostních důvodů se nově vytvořený klíč nikdy nezobrazí na obrazovce a je k dispozici pouze pomocí tlačítka **Kopírovat.** Podobně klíč není přístupný po aktualizaci stránky.

![Vytvořit klíče rozhraní API](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Úprava existujících klíčů rozhraní API

Můžete také aktualizovat klíčová oprávnění a obory bez změny samotného klíče. Pokud máte klíč s určitým oborem (y) pro jeden balíček, můžete použít stejný obor (y) na jeden nebo mnoho dalších balíčků.

![Vytvořit klíče rozhraní API](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Aktualizace nebo odstranění existujících klíčů rozhraní API

Vlastník účtu může aktualizovat klíč, v takovém případě oprávnění (na balíčky), obor a vypršení platnosti zůstávají stejné, ale je vydán nový klíč, takže starý klíč je nepoužitelný. To je užitečné při správě zastaralých klíčů nebo tam, kde existuje potenciál pro únik klíče rozhraní API.

![Vytvořit klíče rozhraní API](media/scoped-api-keys-refresh.png)

Můžete také odstranit tyto klíče, pokud již nejsou potřeba. Odstraněním klíče odeberete klíč a způsobí, že bude nepoužitelný.

## <a name="faqs"></a>Nejčastější dotazy

### <a name="what-happens-to-my-old-legacy-api-key"></a>Co se stane s mým starým (starším) klíčem rozhraní API?

Váš starý klíč rozhraní API (starší verze) pokračuje v práci a může fungovat tak dlouho, jak chcete, aby fungoval. Tyto klíče však budou vyřazeny, pokud nebyly použity více než 365 dní k vysunutí balíčku. Další podrobnosti najdete v příspěvku blogu [Změny vypršení platnosti klíčů rozhraní API](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Tento klíč již nelze aktualizovat. Je třeba odstranit starší klíč a místo toho vytvořit nový klíč s vymezeným oborem.

> [!NOTE]
> Tento klíč má všechna oprávnění pro všechny balíčky a jeho platnost nikdy nevyprší. Měli byste zvážit odstranění tohoto klíče a vytvoření nových klíčů s vymezenými oprávněními a definitivní platností.

### <a name="how-many-api-keys-can-i-create"></a>Kolik klíčů rozhraní API mohu vytvořit?

Počet klíčů rozhraní API, které můžete vytvořit, není nijak omezen. Doporučujeme vám však, abyste ji udrželi na zvládnutelném počtu, abyste neskončili s mnoha zastaralými klíči bez znalosti, kde a kdo je používá.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Můžu odstranit starší klíč rozhraní API nebo přestat používat?

Ano. Můžete -- a pravděpodobně byste měli -- odstranit váš starší klíč rozhraní API.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Mohu získat zpět klíč rozhraní API, který jsem omylem vymazal(a)?

Ne. Po odstranění můžete vytvořit pouze nové klíče. Pro omylem odstraněné klíče není možné obnovit.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Má starý klíč rozhraní API nadále fungovat při aktualizaci klíče rozhraní API?

Ne. Po aktualizaci klíče se vygeneruje nový klíč, který má stejný obor, oprávnění a vypršení platnosti jako ten starý. Starý klíč přestává existovat.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Můžu dát více oprávnění existujícímu klíči rozhraní API?

Obor nelze upravit, ale můžete upravit seznam balíčků, pro který se vztahuje.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Jak poznám, že platnost některého z mých klíčů vypršela nebo vypršela?

Pokud platnost některého klíče vyprší, dáme vám vědět prostřednictvím varovné zprávy v horní části stránky. Varovný e-mail také zašleme držiteli účtu deset dní před vypršením platnosti klíče, abyste podle něj mohli jednat s velkým předstihem.