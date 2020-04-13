---
title: Rezervace předpony ID
description: Popis funkce rezervace ID balíčku a průvodce autorem.
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: da464cc44d8c874e13c0cdfab871f31e643b577f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610498"
---
# <a name="package-id-prefix-reservation"></a>Rezervace předpony ID balíčku

Vlastníci balíčků mohou rezervovat a chránit svou identitu rezervací předponek ID. Příjemci balíčků jsou opatřeny další informace, pokud balíčky, které spotřebovávají nejsou klamavé v jejich identifikační vlastnosti. 

[nuget.org](https://www.nuget.org/) a Visual Studio 2017 verze 15.4 nebo novější zobrazit vizuální indikátor pro balíčky, které jsou odeslány vlastníky s předponou id rezervované ho balíku, tak dlouho, dokud balíček odpovídá vyhrazené ID předpony pojmenování vzor. Níže uvedený odkaz vysvětluje, co rezervace předpony ID znamená a jak může vlastník požádat o předponu ID.

## <a name="id-prefix-reservation-details"></a>Podrobnosti rezervace předpony ID

Když je předpona ID balíčku vyhrazena, několik věcí se stane v [galerii nuget.org,](https://www.nuget.org/) stejně jako v sadě Visual Studio. Kromě toho existují pokročilé scénáře, které jsou podporovány rezervace mise předpony ID, jako je například nastavení předpony jako "veřejné", delegování podskupin předpony na více vlastníků.

### <a name="id-prefix-reservation-on-nugetorg"></a>ID rezervace předpony na nuget.org

Pokud je předpona rezervována v [nuget.org](https://www.nuget.org/), dojde k následujícímu:

1. Rezervace předpony je přidružena k vlastníkovi nebo sadě vlastníků na [nuget.org](https://www.nuget.org/).

1. Vždy, když je balíček odeslán [nuget.org](https://www.nuget.org/) s ID, které odpovídá předponě rezervovaného ID, je balíček odmítnut, pokud nepochází od vlastníka, který si předponu ID rezervoval.

1. Každý balíček, který odpovídá předponě rezervovaného ID a pochází od vlastníka, který si rezervoval předponu ID, bude mít vizuální indikátor ve Visual Studiu 2017 verze 15.4 nebo novější a [na nuget.org](https://www.nuget.org/) označující, že balíček je pod předponou vyhrazeného ID. To platí jak pro nové odeslání balíčku, tak pro stávající balíčky pod vlastníkem (vlastníky). **Poznámka:** Indikátor v sadě Visual Studio se zobrazí pouze v případě, že je jako zdroj balíčku vybrán jeden zdroj.

1. Všechny dříve existující balíčky, které odpovídají předponě rezervovaného ID, ale *nejsou* vlastněny vlastníkem vyhrazené předpony, zůstanou nezměněny (nebudou neuvedeny, ale také nebudou mít vizuální indikátor). Kromě toho budou vlastníci těchto balíčků stále moci odeslat nové verze do balíčku.

Tyto změny jsou založeny na následujících podmínkách a ukládají několik dalších omezení:

- Pouze jeden vlastník balíčku musí mít vyhrazenou předponu pro vizuální indikátor zobrazí (pro balíčky s více vlastníky).

- Pokud existuje více než jeden vlastník balíčku, kde jeden nebo více vlastníků má vyhrazenou předponu a jeden nebo více vlastníků nemá vyhrazenou předponu, pak pouze vlastníci s vyhrazenou předponou mohou odebrat jinévlastníky s vyhrazenou předponou. Vlastníci, kteří nemají rezervovanou předponu, nemohou odebrat vlastníky s rezervovanou předponou. Stále mohou odebrat ostatní vlastníky, kteří také nemají rezervovanou předponu.

- Jakmile má balíček vizuální indikátor, měl by mít *vždy* vizuální indikátor (zaručující, že alespoň jeden vlastník s vyhrazenou předponou zůstane vždy vlastníkem)

### <a name="advanced-prefix-reservation-scenarios"></a>Scénáře rozšířené rezervace předpony

Existuje několik pokročilejších scénářů rezervace předpony popsaných níže, včetně delegování podpony a označení předpony jako veřejné. Níže jsou pokročilejší rezervace předpony, které lze provést. 

- Během rezervace předpony může vlastník požádat o delegování podmnoží předpony (nebo předpony) jiným vlastníkům. Například pokud '[Microsoft](https://www.nuget.org/profiles/microsoft)' vlastní 'Microsoft. \*', ale '[aspnet](https://www.nuget.org/profiles/aspnet)' chce rezervovat 'Microsoft.AspNet. \*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' může zvolit delegovat 'Microsoft.AspNet. \*' na účet [aspnet.](https://www.nuget.org/profiles/aspnet)

- Během rezervace předpony může vlastník zvolit, zda předponu zveřejní. To jim stále poskytne vizuální indikátor, který ukazuje, že balíček pochází z vyhrazené předpony, ale **nebude** blokovat budoucí odeslání balíčku na předponu pro žádného vlastníka. To je užitečné pro open source projekty s mnoha přispěvateli – horní nebo základní přispěvatelé mohou mít předponu vyhrazenou, ale stále může být otevřena všem přispěvatelům. 

### <a name="prefix-reservation-visual-indicator"></a>Vizuální indikátor rezervace předpony

Když balíček pochází z rezervované předpony, zobrazí se níže uvedené vizuální indikátory na [galerii nuget.org](https://www.nuget.org/) a ve Visual Studiu 2017 verze 15.4 nebo novější:

**nuget.org Gallery**galerie nuget.org nuget.org
![](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proces žádosti o žádost o rezervaci předpony ID

1. Zkontrolujte [kritéria přijetí rezervace ID předpony](#id-prefix-reservation-criteria).

2. Určete předpony, které chcete rezervovat, kromě všech [pokročilých scénářů rezervace předpony,](#advanced-prefix-reservation-scenarios) které můžete potřebovat.

3. Odešlete [account@nuget.org](mailto:account@nuget.org) poštu se zobrazovaným jménem vlastníka na [nuget.org](https://www.nuget.org/)a také všechny vyhrazené předpony, které požadujete. Pokud delegujete podmnožiny předpony na více vlastníků, nezapomeňte uvést všechny názvy zobrazení vlastníka a podmnožiny předponu.

Po podání žádosti budete upozorněni na přijetí nebo zamítnutí (s kritérii, která způsobila zamítnutí). Možná budeme muset položit další identifikační otázky, abychom potvrdili identitu vlastníka.

### <a name="id-prefix-reservation-criteria"></a>Kritéria rezervace předpony ID

Při kontrole jakékoli žádosti o rezervaci předpony ID vyhodnotí [nuget.org](https://www.nuget.org/) tým aplikaci podle níže uvedených kritérií. Aby byla předpona rezervována, musí být splněna všechna kritéria, ale žádost může být zamítnuta, pokud neexistují podstatné důkazy o splnění kritérií (s vysvětlením):

1. Má předpona ID balíčku správně a jasně identifikovat vlastníka balíčku?

1. Povolil vlastník balíčku [2FA pro svůj NuGet.org účet](individual-accounts.md#enable-two-factor-authentication-2fa)?

1. Je významný počet balíčků, které již byly odeslány vlastníkem pod předponou ID balíčku?

1. Je předpona ID balíčku předpona něco společného, co by nemělo patřit žádnému jednotlivému vlastníkovi nebo organizaci?

1. *Nezpůsobilo* by vyhrazení předpony ID balíčku nejednoznačnost a zmatek pro komunitu?

1. Jsou identifikační vlastnosti balíčků, které odpovídají předponě ID balíčku, jasné a konzistentní (zejména autor balíčku)?

1. Mají balíčky licenci (pomocí prvku metadat [licence](../reference/nuspec.md#license) a NOT licenseUrl, který je zastaralá)?

1. Pokud balíčky mají ikonu (pomocí iconUrl metadata element), jsou také pomocí prvku metadat [ikony](../reference/nuspec.md#icon) (to není požadavek na odstranění iconUrl)?

## <a name="third-party-feed-provider-scenarios"></a>Scénáře poskytovatelů informačních kanálů třetích stran

Pokud poskytovatel informačního kanálu třetí strany má zájem o implementaci své vlastní služby k poskytování rezervací předpony, může tak učinit úpravou vyhledávací služby v zprostředkovateli informačního kanálu NuGet V3. Změna ve službě vyhledávání zdrojů je `verified` přidání vlastnosti. Klient NuGet nebude podporovat přidané vlastnosti v kanálu V2.

Další informace naleznete v [dokumentaci k vyhledávací službě rozhraní API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Zásady pro spor o rezervaci předpony ID balíčku
Pokud se domníváte, že majiteli na [NuGet.org](https://www.nuget.org) byla přidělena rezervace předpony id balíčku, která je v [support@nuget.org](mailto:support@nuget.org) rozporu s výše uvedenými kritérii nebo porušuje ochranná práva nebo autorská práva, zašlete prosím e-mail s dotyčnou předponou ID, vlastníka předpony ID a důvodem zpochybnění přiřazené rezervace předpony.

