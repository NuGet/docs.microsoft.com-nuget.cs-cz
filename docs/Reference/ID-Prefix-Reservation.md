---
title: "Předpona ID rezervace odkaz | Microsoft Docs"
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 76c0bb7f-9aaf-4c09-b3fd-f6802f9dd602
description: "Popis funkce rezervace předponu ID balíčku a Průvodce obsahu."
keywords: "ID balíčku NuGet, předpony, rezervace"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: e94d1431667ec17347165ac0a3993c0b552e6a60
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="package-id-prefix-reservation"></a>Rezervace předpona ID balíčku
[nuget.org](https://www.nuget.org/) a Visual Studio 2017 verze 15,4 nebo novější zobrazit vizuální indikátor pro balíčky, které jsou odeslaná vlastníky předponu ID balíčku vyhrazené, tak dlouho, dokud balíček odpovídá rezervované ID předpony vzoru pro pojmenovávání. Následující odkaz vysvětluje, co znamená rezervace předpona ID a jak můžete použít vlastníka pro předponu ID.

## <a name="what-is-package-id-prefix-reservation"></a>Co je rezervace předpona ID balíčku?
Vlastníci balíčku je moct vyhradit a chránit svou identitu vyhrazením ID předpony. Příjemci balíček jsou k dispozici společně s dalšími informacemi v případě využívání balíčky, které balíčku, který se spotřebovávají nejsou podvodný v jejich identifikující vlastnosti. Přečtěte si k fungování rezervace předpona ID v podrobnosti najdete v tématu.

## <a name="id-prefix-reservation-details"></a>Podrobnosti o rezervaci předpona ID 
Když je vyhrazena předpona ID balíčku, dojde k několika změnám na [nuget.org](https://www.nuget.org/) galerie, stejně jako v sadě Visual Studio. Kromě toho jsou pokročilé scénáře, které jsou podporovány rezervace předpona ID, jako je třeba nastavení předponu jako 'veřejné' delegování předponu podmnožin na více vlastníky.

Následující část popisuje funkci v podrobnosti a také pokročilejší funkce.

### <a name="id-prefix-reservation-on-nugetorg"></a>Rezervace předpona ID v nuget.org
Když je vyhrazena předpona na [nuget.org](https://www.nuget.org/), proběhne následující:
1. Předpona rezervace je přidružená ke vlastníka nebo sadu vlastníky na [nuget.org](https://www.nuget.org/). 
2. Vždy, když je balíček odeslána [nuget.org](https://www.nuget.org/) s ID, který odpovídá rezervované předpony ID balíčku byl odmítnut pokud pochází z vlastníka/vlastníků, která vyhrazena předpona ID.
3. Všechny balíček, který odpovídá rezervované předpony ID a pochází z vlastníka/vlastníků, která vyhrazena předpona ID bude mít vizuální indikátor ve verzi Visual Studio 2017 15,4 nebo novější a na [nuget.org](https://www.nuget.org/) označující, že balíček je v části vyhrazenou předponu ID. To platí pro nový balíček odesílání jak existující balíčky pod vlastníka/vlastníků. **Poznámka:** indikátoru v sadě Visual Studio se zobrazí pouze pokud je vybraný jeden informačního kanálu jako zdroj balíčku. 
4. Všechny dříve existující balíčky, které odpovídají vyhrazena předpona ID, ale jsou *není* Vlastněno vlastníkem z vyhrazených předponu zůstane beze změny (nebudou, ale také nebude mít visual indikátoru). Kromě toho vlastníci tyto balíčky budou mít pořád povolený k odeslání nové verze balíčku.

Tyto změny jsou založené na těchto podmínkách a zavádí několik další omezení:
* Pouze jednoho vlastníka balíčku musí mít předponu vyhrazené pro visual ukazatel zobrazí (pro balíčků s několika vlastníky).
* Pokud existuje více než jednoho vlastníka balíčku, kde má jeden nebo více vlastníky rezervované předpony a jednoho nebo více vlastníků nemá rezervované předpony, můžete odebrat pouze vlastníka/vlastníků s rezervované předpony jiných majitele(ů) s vyhrazenou předponu. Vlastníci, kteří nemají vyhrazenou předponu nelze odebrat vlastníky s vyhrazenou předponu. Stále může odebrat další vlastníky, která také nemají vyhrazenou předponu.
  * Jakmile balíček visual indikátoru, by měl *vždy* mít visual ukazatele (záruky toho, že alespoň jednoho vlastníka s rezervované předpony vždy zůstanou vlastníka)

### <a name="advanced-prefix-reservation-scenarios"></a>Pokročilé předponu rezervace scénáře
Existuje několik pokročilejší scénáře rezervace předponu popsané dál, včetně delegování subprefix a označování předpony jako veřejné. Níže jsou pokročilejší rezervace předpony, které lze provést. 

* Během předponu rezervace vlastník může požádat o delegování podmnožin předpony (nebo předponu) na jiné vlastníky. Například pokud se[Microsoft](https://www.nuget.org/profiles/microsoft)' vlastní ' společnosti Microsoft.\*', ale '[aspnet](https://www.nuget.org/profiles/aspnet)' chce rezervovat ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)se může Zvolte pro delegování "Microsoft.AspNet. \*' na [aspnet](https://www.nuget.org/profiles/aspnet) účtu.
*  Během předponu rezervace můžete vybrat vlastník zveřejnit předponu. To bude stále jim poskytnout visual indikátoru zobrazující balíček pochází z vyhrazenou předponu, že se bude **není** blokovat budoucí balíček odesílání na předponě pro všechny vlastníka. To je užitečné pro projekty s otevřeným zdrojem s mnoha přispěvateli – přispěvatele top nebo základní může mít předponu vyhrazené, ale stále může být otevřené pro všechny přispěvatele. 

### <a name="prefix-reservation-visual-indicator"></a>Předpona rezervace visual indikátoru
Pokud balíček pochází z vyhrazenou předponu, zobrazí se níže visual ukazatele na [nuget.org](https://www.nuget.org/) galerie a Visual Studio 2017 verze 15,4 nebo novější:

**Galerie nuget.org**
![nuget.org Galerie](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![sady Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proces aplikace rezervace předpona ID
Chcete-li použít pro předponu rezervace, postupujte níže uvedených pokynů. 
1. Zkontrolujte přijetí [kritéria pro předponu ID rezervace](#id-prefix-reservation-criteria).
2. Určit obory názvů, které chcete rezervovat, kromě žádné [pokročilé scénáře rezervace předponu](#advanced-prefix-reservation-scenarios) může vyžadovat.
3. Odesílat e-maily na [ account@nuget.org ](mailto:account@nuget.org) se na vlastníka zobrazovaný název na [nuget.org](https://www.nuget.org/), a také všechny rezervované předpony, které jste požádali. Pokud na více vlastníky jsou delegování předponu podmnožiny, ujistěte se, zmínili všechny vlastníka zobrazovaných názvů a předpony podmnožin.

Po odeslání aplikace, budete upozorněni přijetí nebo odmítnutí (s kritéria, která způsobila odmítání). Musíme ptají další identifikační potvrdit identitu vlastníka. 

### <a name="id-prefix-reservation-criteria"></a>Kritéria rezervace předpona ID
Při revizi všechny aplikace pro rezervaci předpona ID, [nuget.org](https://www.nuget.org/) tým bude evalaute aplikace před níže kritéria. Ne všechna kritéria musí být splněné, předpony, které budou rezervovány, ale aplikace může být odepřena, pokud není k dispozici významné důkaz kritéria plněny (s vysvětlením zadané):
1. Předpona ID balíčku správně a jednoznačně identifikovat vlastníka balíčku?
2. Jsou velký počet balíčků, které již byly vlastníkem pod předpona ID balíčku?
3. Je předpona ID balíčku běžné něčeho, co by neměl patří do všech jednotlivých vlastník nebo organizace?
4. By *není* rezervování předpona ID balíčku způsobit nejednoznačnosti a přehlednosti pro komunity?
5. Jsou identifikující vlastnosti balíčky, které odpovídají jasné a konzistentní předpona ID balíčku (zejména autora balíčku)?

## <a name="3rd-party-feed-provider-scenarios"></a>3. stran kanálu zprostředkovatele scénáře
Pokud 3. stran kanálu zprostředkovatele zájem o implementaci vlastní služba poskytnout předponu rezervace, můžete toho dosáhnout úpravou službu vyhledávání ve NuGet V3 kanálu zprostředkovatele. Přidání ve službě informačního kanálu vyhledávání je přidání *ověřit* vlastnost s příklady pro informační kanály V3 níže. Klient NuGet nebude podporovat přidané vlastnosti v V2 informačního kanálu.

Další informace najdete v tématu [dokumentaci k rozhraní API služby vyhledávání](../api/search-query-service-resource.md).
