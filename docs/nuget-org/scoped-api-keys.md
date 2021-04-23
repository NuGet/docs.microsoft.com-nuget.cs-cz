---
title: Obory klíčů rozhraní API
description: Převzetí řízení klíčů rozhraní API, které použijete k nabízení balíčků
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: a3d2504528249f3545e2eb5d9bce7713029638db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901587"
---
# <a name="scoped-api-keys"></a>Obory klíčů rozhraní API

Pro zajištění bezpečnějšího prostředí pro distribuci balíčků můžete převzít řízení klíčů rozhraní API přidáním oborů.

Možnost poskytovat rozsah klíčů rozhraní API vám poskytne lepší kontrolu nad rozhraními API. Další možnosti:

- Vytvořte několik klíčů rozhraní API s vymezeným oborem, které lze použít pro různé balíčky s různými časovými obdobími vypršení platnosti.
- Získejte zabezpečený klíč rozhraní API.
- Úpravou existujících klíčů rozhraní API změňte použitelnost balíčku.
- Aktualizujte nebo odstraňte existující klíče rozhraní API, aniž by došlo k překážkám operací pomocí jiných klíčů.

## <a name="why-do-we-support-scoped-api-keys"></a>Proč podporujeme vymezené klíče rozhraní API?

Pro klíče rozhraní API podporujeme obory, které vám umožní mít přesnější oprávnění. V minulosti nabídl NuGet pro účet jeden klíč rozhraní API a tento přístup měl několik nevýhod:

- **Jeden klíč rozhraní API pro řízení všech balíčků**. Pomocí jediného klíče rozhraní API, který se používá ke správě všech balíčků, je obtížné tento klíč bezpečně sdílet, pokud se k různým balíčkům účastní více vývojářů a když sdílí účet vydavatele.
- **Všechna oprávnění nebo žádná**. Každý, kdo má přístup k klíči rozhraní API, má všechna oprávnění (Publish, push a unlist) v balíčcích. To není často žádoucí v prostředí s více týmy.
- **Jediný bod selhání**. Jeden klíč rozhraní API označuje také jediný bod selhání. Pokud dojde k ohrožení bezpečnosti klíče, můžou být všechny balíčky přidružené k tomuto účtu potenciálně ohrožené. Obnovení klíče rozhraní API je jediný způsob, jak zamezit úniku a vyhnout se přerušení pracovního postupu CI/CD. Kromě toho můžou nastat případy, kdy budete chtít odvolat přístup k klíči rozhraní API pro jednotlivce (například když zaměstnanec odejde z organizace). Neexistuje žádný čistý způsob, jak to zvládnout dnes.

Pomocí vymezených klíčů rozhraní API se snažíme tyto problémy vyřešit a přitom se ujistit, že žádná z existujících pracovních postupů není přerušená.

## <a name="acquire-an-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Vytvoření klíčů rozhraní API s vymezeným oborem

Můžete vytvořit více klíčů rozhraní API na základě vašich požadavků. Klíč rozhraní API se může vztahovat na jeden nebo více balíčků, má různé obory, které udělují specifická oprávnění, a má k ní přidružené datum vypršení platnosti.

V následujícím příkladu máte klíč rozhraní API s názvem `Contoso service CI` , který se dá použít k nabízení balíčků pro konkrétní `Contoso.Service` balíčky, a je platný po dobu 365 dnů. Jedná se o typický scénář, kdy různé týmy v rámci stejné organizace pracují na různých balíčcích a členové týmu poskytují klíč, který uděluje oprávnění pouze pro balíček, na kterém pracují. Vypršení platnosti slouží jako mechanismus, který brání zastaralým nebo zapomenutým klíčům.

![Vytvoření klíčů rozhraní API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Použití vzorů glob

Pokud pracujete na více balíčcích a máte velký seznam balíčků, které se mají spravovat, můžete pomocí vzorů expanze názvů vybrat více balíčků dohromady. Například pokud chcete udělit určité obory klíči pro všechny balíčky, jejichž ID začíná na `Fabrikam.Service` , můžete to provést tak, že zadáte `fabrikam.service.*` do textového pole **glob Pattern** .

![Vytvoření klíčů rozhraní API – 2](media/scoped-api-keys-glob-pattern.png)

Použití vzorů glob k určení oprávnění klíče rozhraní API platí i pro nové balíčky, které odpovídají vzoru glob. Pokud se například pokusíte odeslat nový balíček s názvem `Fabrikam.Service.Framework` , můžete to provést pomocí dříve vytvořeného klíče, protože balíček odpovídá glob vzoru `fabrikam.service.*` .

## <a name="obtain-api-keys-securely"></a>Zabezpečený získávání klíčů rozhraní API

Z důvodu zabezpečení se nově vytvořený klíč nikdy nezobrazuje na obrazovce a je k dispozici pouze pomocí tlačítka **Kopírovat** . Podobně klíč není přístupný po obnovení stránky.

![Vytvoření klíčů rozhraní API – 3](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Upravit existující klíče rozhraní API

Je také možné, že budete chtít aktualizovat klíčová oprávnění a obory beze změny samotného klíče. Pokud máte klíč s konkrétními obory pro jeden balíček, můžete použít stejný obor (y) na jednom nebo mnoha dalších balíčcích.

![Vytvoření klíčů rozhraní API – 4](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Aktualizovat nebo odstranit existující klíče rozhraní API

Vlastník účtu se může rozhodnout aktualizovat klíč. v takovém případě se oprávnění (v balíčcích), rozsah a vypršení platnosti zůstane stejné, ale nový klíč se vydá, protože starý klíč je vydaný jako nepoužitelný. To je užitečné při správě zastaralých klíčů nebo v případě úniku klíčů rozhraní API.

![Vytvoření klíčů rozhraní API-5](media/scoped-api-keys-refresh.png)

Tyto klíče můžete odstranit i v případě, že už je nepotřebujete. Odstranění klíče odebere klíč a stane se nepoužitelným.

## <a name="faqs"></a>Nejčastější dotazy

### <a name="what-happens-to-my-old-legacy-api-key"></a>Co se stane se starým (starším) klíčem rozhraní API?

Starý klíč rozhraní API (starší verze) bude i nadále fungovat a může fungovat tak dlouho, dokud budete chtít pracovat. Tyto klíče se ale vyřadí, pokud se nepoužily po dobu delší než 365 dní k odeslání balíčku. Další podrobnosti najdete v blogovém příspěvku [o změnách platnosti klíčů rozhraní API](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Tento klíč už nemůžete aktualizovat. Je nutné odstranit starší klíč a místo toho vytvořit nový klíč s oborem.

> [!NOTE]
> Tento klíč má všechna oprávnění pro všechny balíčky a nikdy nekončí jeho platnost. Měli byste zvážit odstranění tohoto klíče a vytváření nových klíčů s rozsahem oprávnění a s určením platnosti.

### <a name="how-many-api-keys-can-i-create"></a>Kolik klíčů rozhraní API můžu vytvořit?

Počet klíčů rozhraní API, které můžete vytvořit, není nijak omezený. Doporučujeme však, abyste zachovali spravovatelný počet, takže nebudete mít spoustu zastaralých klíčů bez znalosti toho, kde a kdo je používá.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Můžu odstranit zastaralý klíč rozhraní API nebo ho teď přestat používat?

Ano. Můžete--a pravděpodobně byste měli odstranit starší klíč rozhraní API.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Můžu získat zpátky svůj klíč rozhraní API, který jsem odstranil omylem?

No. Po odstranění můžete vytvořit pouze nové klíče. Nechtěně odstraněné klíče není možné obnovit.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Funguje starý klíč rozhraní API i nadále při aktualizaci klíče rozhraní API?

No. Když aktualizujete klíč, vygeneruje se nový klíč, který má stejný obor, oprávnění a vypršení platnosti jako starý. Starý klíč přestane existovat.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Můžu pro existující klíč rozhraní API přidělit další oprávnění?

Obor nemůžete změnit, ale můžete upravit seznam balíčků, na který se vztahuje.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Návody zjistit, jestli vypršela platnost nějakého z mých klíčů nebo že vypršela platnost?

Pokud vyprší platnost nějakého klíče, dáme vám v horní části stránky informovat zprávu s upozorněním. E-mailovou zprávu pro držitele účtu pošleme také deset dnů před vypršením platnosti klíče, abyste mohli i nadále fungovat předem.