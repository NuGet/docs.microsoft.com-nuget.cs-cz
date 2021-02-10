---
title: Rezervace předpony ID
description: Popis funkce rezervace předpony ID balíčku a průvodce vytvářením
author: JonDouglas
ms.author: jodou
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: 428fd3d7b324f6eb825b17e4a87a662fbd84a2f0
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990098"
---
# <a name="package-id-prefix-reservation"></a>Rezervace předpony ID balíčku

Vlastníci balíčku si můžou vyhradit a chránit svoji identitu tím, že si zachovají předpony ID. Příjemci balíčku jsou k dispozici další informace, pokud jsou nenáročné na balíčky, které jsou náročné, v jejich identifikačních vlastnostech. 

[NuGet.org](https://www.nuget.org/) a visual Studio 2017 verze 15,4 nebo novější zobrazí vizuální indikátor pro balíčky, které jsou odesílány vlastníky s vyhrazenou předponou ID balíčku, pokud balíček odpovídá vzoru pro pojmenování předpony vyhrazeného ID. Níže uvedený odkaz vysvětluje, co znamená rezervace předpony ID a jak může vlastník použít pro předponu ID.

## <a name="id-prefix-reservation-details"></a>Podrobnosti rezervace předpony ID

Když je vyhrazená předpona ID balíčku, v galerii [NuGet.org](https://www.nuget.org/) a také v aplikaci Visual Studio dojde k několika akcím. Kromě toho existují pokročilé scénáře, které jsou podporovány rezervací předpony ID, jako je například nastavení předpony jako Public, delegování podmnožin předpony více vlastníkům.

### <a name="id-prefix-reservation-on-nugetorg"></a>Rezervace předpony ID v nuget.org

Pokud je předpona vyhrazena pro [NuGet.org](https://www.nuget.org/), dojde k následujícímu:

1. Rezervace předpony je přidružená k vlastníkovi nebo sadě vlastníků v [NuGet.org](https://www.nuget.org/).

1. Pokaždé, když se odešle balíček do [NuGet.org](https://www.nuget.org/) s ID, které se shoduje s předponou rezervovaného ID, balíček se zamítne, pokud nepochází od vlastníků, které rezervovaly předponu ID.

1. Každý balíček, který odpovídá předponě rezervovaného ID a pochází od vlastníků, které rezervovaly předponu ID, bude mít vizuální indikátor v aplikaci Visual Studio 2017 verze 15,4 nebo novější a na [NuGet.org](https://www.nuget.org/) , který označuje, že balíček je pod rezervovanou předponou ID. To platí pro nové odesílání balíčků i pro existující balíčky v rámci vlastníků. **Poznámka:** Indikátor v aplikaci Visual Studio se zobrazí pouze v případě, že je jako zdroj balíčku vybrán jeden informační kanál.

1. Všechny dříve existující balíčky, které odpovídají předponě rezervovaného ID, ale *nejsou vlastněny vlastníkem rezervované* předpony, zůstanou beze změny (nebudou v seznamu uvedeny), ale nebudou mít indikátor vizuálu. Kromě toho budou moci vlastníci těchto balíčků i nadále odesílat nové verze do balíčku.

Tyto změny jsou založeny na následujících podmínkách a ukládají několik dalších omezení:

- Pouze jeden vlastník balíčku musí mít vyhrazenou předponu pro zobrazení vizuálního indikátoru (pro balíčky s více vlastníky).

- Pokud je k dispozici více než jeden vlastník balíčku, kde má jeden nebo více vlastníků vyhrazenou předponu a jeden nebo více vlastníků nemá rezervovanou předponu, mohou jiní vlastníky s rezervovanou předponou odebrat pouze vlastníci. Vlastníci, kteří nemají vyhrazenou předponu, nemohou odebrat vlastníky s vyhrazenou předponou. Můžou pořád odebrat i další vlastníky, které nemají rezervovanou předponu.

- Jakmile má balíček vizuální indikátor, měl by mít *vždy* vizuální indikátor (Zaručujeme, že nejméně jeden vlastník s rezervovanou předponou zůstane vždy vlastníkem).

### <a name="advanced-prefix-reservation-scenarios"></a>Pokročilé scénáře rezervace předpon

K dispozici je několik pokročilejších scénářů rezervace prefixů, včetně delegování s předponou a označení předpon jako veřejných. Níže jsou uvedeny pokročilejší rezervace předpon, které je možné provést. 

- Během rezervace předpony může vlastník požádat o delegování podmnožiny předpon (nebo předpony) na jiné vlastníky. Například pokud "[Microsoft](https://www.nuget.org/profiles/microsoft)" vlastní "Microsoft. \* ", ale "[ASPNET](https://www.nuget.org/profiles/aspnet)" chce rezervovat "Microsoft. ASPNET. \* ", "[Microsoft](https://www.nuget.org/profiles/microsoft)" se může rozhodnout delegovat "Microsoft. ASPNET. \* " na účet [ASPNET](https://www.nuget.org/profiles/aspnet) .

- V rámci rezervované předpony se vlastník může rozhodnout, že má předponu veřejnou. Tím se jim budou zobrazovat indikátory, které ukazují, že balíček pochází z rezervované předpony, ale **neblokuje** budoucí odesílání balíčků na předponu pro libovolného vlastníka. To je užitečné pro open source projekty s mnoha přispěvateli – přispěvatelé Top nebo Core můžou mít vyhrazenou předponu, ale může být pořád otevřená pro všechny přispěvatele. 

### <a name="prefix-reservation-visual-indicator"></a>Vizuální indikátor rezervace předpony

Když balíček pochází z rezervované předpony, zobrazí se v galerii [NuGet.org](https://www.nuget.org/) a v aplikaci visual Studio 2017 verze 15,4 nebo novější následující vizuální indikátory:

**galerie NuGet.org** 
 ![ Galerie nuget.org](media/nuget-gallery-reserved-prefix.png)

**Visual Studio** 
 ![ Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proces aplikace rezervace předpony ID

1. Zkontrolujte kritéria přijetí [pro rezervaci ID předpony](#id-prefix-reservation-criteria).

2. Určete předpony, které chcete vyhradit, kromě všech [pokročilých scénářů vyhrazených předpon](#advanced-prefix-reservation-scenarios) , které můžete potřebovat.

3. Odešlete e-mail na [account@nuget.org](mailto:account@nuget.org) zobrazované jméno vlastníka na [NuGet.org](https://www.nuget.org/)a všechny rezervované předpony, které požadujete. Pokud delegujete podmnožiny předpon více vlastníkům, ujistěte se, že jste uváděli všechny zobrazované názvy a podmnožiny předpon všech vlastníků.

Po odeslání aplikace se zobrazí oznámení o přijetí nebo zamítnutí (s kritérii, která způsobila zamítnutí). Pro potvrzení identity vlastníka možná budete muset požádat o další identifikační otázky.

### <a name="id-prefix-reservation-criteria"></a>Kritéria rezervace předpony ID

Při kontrole libovolné aplikace pro rezervaci předpony ID tým [NuGet.org](https://www.nuget.org) vyhodnotí aplikaci proti níže uvedeným kritériím. Počítejte s tím, že není nutné splnit všechna kritéria, aby bylo možné zarezervovat předponu, ale aplikace může být odepřena, pokud není k dispozici podstatný důkaz kritérií, která jsou splněna (s vysvětlením uvedeným):

1. Je správně předpona ID balíčku a jednoznačně identifikován vlastník rezervace?

1. Má vlastník [povolen 2FA pro svůj účet NuGet.org](individual-accounts.md#enable-two-factor-authentication-2fa)?

1. Je prefix ID balíčku něco společného, který by neměl patřit žádnému individuálnímu vlastníkovi nebo organizaci?

1. *Nepovedlo* se mu zachovávat předponu ID balíčku, která by způsobila nejednoznačnost, nejasnost nebo jiné poškození komunity?

Při publikování balíčků do NuGet.org v rámci rezervované předpony ID je potřeba vzít v úvahu následující osvědčené postupy:

1. Jsou identifikující vlastnosti balíčků, které odpovídají předponě ID balíčku, jasné a konzistentní (zejména autor balíčku)?

1. Mají balíčky licenci (pomocí elementu metadata [licence](../reference/nuspec.md#license) a licenseUrl, který se už nepoužívá)?

1. Pokud mají balíčky ikonu (pomocí elementu metadat iconUrl), jsou také použity prvkem metadat [ikony](../reference/nuspec.md#icon) ? Nejde odebrat iconUrl, ale musí se použít vložené ikony.
 
Kromě výše uvedených bodů zvažte možnost projít si kompletní [Průvodce vytvářením osvědčených postupů pro vytváření balíčků](../create-packages/package-authoring-best-practices.md) .

## <a name="third-party-feed-provider-scenarios"></a>Scénáře poskytovatele kanálu třetích stran

Pokud se poskytovatel kanálu třetí strany zajímá o implementaci vlastní služby pro poskytování rezervací předpon, může to udělat úpravou vyhledávací služby v poskytovatelích kanálu NuGet v3. Změnou ve službě vyhledávání informačních kanálů je přidání `verified` Vlastnosti. Klient NuGet nebude podporovat přidané vlastnosti v kanálu v2.

Další informace najdete v dokumentaci k [vyhledávací službě rozhraní API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Zásady sporu pro rezervaci předpony ID balíčku
Pokud se domníváte, že vlastník na [NuGet.org](https://www.nuget.org) byl přiřazen k rezervaci předpony ID balíčku, která se nachází na výše uvedených kritériích, nebo v jakýchkoli ochranných známkách nebo copyrightech, pošlete prosím e-mail [support@nuget.org](mailto:support@nuget.org) s touto předponou ID, vlastníkem předpony ID a důvodem, proč se přiřadí rezervované předpony.

