---
title: Odkaz na rezervace předpony ID
description: Průvodce Autor a popis funkce rezervace předpony ID balíčku.
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e8b902c89427333afb7a27ee9de0eeb99a92f391
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225872"
---
# <a name="package-id-prefix-reservation"></a>Rezervace předpony ID balíčku

Vlastníky balíčku můžete rezervovat a rezervace předpony ID chránit svoji identitu. Příjemci balíček jsou k dispozici společně s dalšími informacemi v případě využívání balíčky, které balíček, který se využívání nejsou podvodný v jejich identifikující vlastnosti. 

[nuget.org](https://www.nuget.org/) a Visual Studio 2017 verze 15.4 nebo novější zobrazit vizuální indikátor pro balíčky, které jsou předložené vlastníky, kteří mají předponu ID vyhrazené balíčku tak dlouho, dokud balíček odpovídá rezervované ID předpony vzor pro pojmenování. Následující odkaz vysvětluje co znamená rezervace předpony ID, a jak předponu ID požádat vlastníka.

## <a name="id-prefix-reservation-details"></a>Podrobnosti rezervace předpony ID

Pokud je vyhrazena předpona ID balíčku, stane se několik věcí na [nuget.org](https://www.nuget.org/) galerie, stejně jako v sadě Visual Studio. Kromě toho jsou pokročilé scénáře, které jsou podporovány rezervace předpony ID, jako je nastavení předpony jako "public" delegování předponu podmnožiny více vlastníkům.

### <a name="id-prefix-reservation-on-nugetorg"></a>Rezervace předpony ID na nuget.org

Když je vyhrazeno předponu [nuget.org](https://www.nuget.org/), stane se následující:

1. Rezervace předpony je přidružené k roli vlastníka nebo sadu vlastníků na [nuget.org](https://www.nuget.org/).

1. Vždy, když se balíček odešle na [nuget.org](https://www.nuget.org/) s ID, který odpovídá rezervované předpona ID, je balíček zamítnuty, pokud pochází z počet vlastníků, která je vyhrazena předpona ID.

1. Libovolný balíček, který odpovídá rezervované předpona ID a mohou být počet vlastníků, která je vyhrazena předpona ID bude mít vizuální označení, v sadě Visual Studio 2017 verze 15.4 nebo novější a na [nuget.org](https://www.nuget.org/) označující, že balíček je v části vyhrazenou předponu ID. To platí pro nový balíček odesílání i existující balíčky v části počet vlastníků. **Poznámka:** Indikátor v sadě Visual Studio se zobrazí jenom v případě, že jako zdroj balíčku byl vybrán jeden kanál.

1. Všechna dříve existující balíčky, které odpovídají vyhrazenou předponou ID, ale jsou *není* vlastněné vlastníka vyhrazený předponu zůstane beze změny (nebudou neuvedené v seznamu, ale nebudou mít také vizuální označení). Kromě toho vlastníků těchto balíčků bude ji možné odeslat nové verze balíčku.

Tyto změny jsou založené na těchto podmínkách a několika další omezení:

- Pouze jednoho vlastníka balíčku musí mít vyhrazenou předponou pro vizuální indikátor zobrazit (pro balíčky s několika vlastníků).

- Pokud existuje více než jednoho vlastníka balíčku, kde má vyhrazenou předponou jednoho nebo několika vlastníka a jednoho nebo několika vlastníka nemá vyhrazenou předponou, lze odebrat pouze počet vlastníků s vyhrazenou předponou počet dalších vlastníků s vyhrazenou předponou. Vlastníci, kteří nemají rezervované předpony nelze odebrat vlastníky s rezervovanou předponou. Mohou stále odebírat další vlastníky, které nemají také rezervované předpony.

- Jakmile balíček obsahuje vizuální označení, by měl *vždy* mají vizuální označení (zaručující, že alespoň jednoho vlastníka s vyhrazenou předponou vždy zůstane vlastníka)

### <a name="advanced-prefix-reservation-scenarios"></a>Rozšířené předpony rezervace scénáře

Existuje několik pokročilejší scénáře vyhrazení předpony je popsáno níže, včetně delegování subprefix a označení předpony jako public. Níže jsou pokročilejší rezervace předpony, které mohou být provedeny. 

- Během rezervace předpony vlastníka požádat o delegování podmnožiny předpony (nebo předponu) další vlastníky. Například pokud "[Microsoft](https://www.nuget.org/profiles/microsoft)" vlastní "Microsoft.\*", ale "[aspnet](https://www.nuget.org/profiles/aspnet)" chce rezervovat "Microsoft.AspNet.\*","[Microsoft](https://www.nuget.org/profiles/microsoft)" může Zvolte pro delegování "Microsoft.AspNet. \*' chcete [aspnet](https://www.nuget.org/profiles/aspnet) účtu.

- Během rezervace předpony vlastníka můžete zvolit, jestli veřejné předpony. Stále získáte tak jejich vizuální indikátor zobrazuje, že balíček pochází z vyhrazenou předponu, ale bude **není** blokovat budoucí balíček příspěvky na této předponě pro jakékoli vlastníka. To je užitečné pro open source projekty s mnoha přispěvateli – přispěvatelé top nebo core může mít předponu vyhrazené, ale stále může být otevřený, aby všichni přispěvatelé. 

### <a name="prefix-reservation-visual-indicator"></a>Předpona rezervace vizuální označení

Když balíček pochází z vyhrazenou předponou, zobrazí pod visual ukazatele na [nuget.org](https://www.nuget.org/) galerie a v sadě Visual Studio 2017 verze 15.4 nebo novější:

**Galerie nuget.org**
![nuget.org Galerie](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proces aplikace rezervace předpony ID

1. Projděte si přijetí [kritéria pro rezervace předpony ID](#id-prefix-reservation-criteria).

2. Určení předpon, které chcete rezervovat, spolu s některou [pokročilé scénáře vyhrazení předpony](#advanced-prefix-reservation-scenarios) může vyžadovat.

3. Odeslat e-mail na adresu [ account@nuget.org ](mailto:account@nuget.org) s vlastníkem zobrazovaný název na [nuget.org](https://www.nuget.org/), stejně jako všechny rezervované předpony, které jste požádali. Pokud předponu podmnožiny jsou delegování více vlastníkům, ujistěte se, že zmiňovat všechny vlastníka zobrazovaných názvů a předpony podmnožin.

Po odeslání žádosti budete upozorněni, přijetí nebo zamítnutí (s kritéria, která způsobila odmítnutí). Musíme mohou se ptát další identifikační potvrdit identitu vlastníka.

### <a name="id-prefix-reservation-criteria"></a>Kritéria rezervace předpony ID

Když zkontrolujete všechny žádosti o rezervace předpony ID [nuget.org](https://www.nuget.org/) týmu se vyhodnotí jako aplikace proti následující kritéria. Ne všechna kritéria je potřeba splnit u předpony, které budou rezervovány, ale aplikace může být odepřen, pokud není podstatné doklad o kritéria neplní (s vysvětlením zadaný):

1. Předponu ID balíčku správně a jasně určit vlastníka balíčku?

1. Vlastník pod předpona ID balíčku se velký počet balíčků, které již byly odeslány?

1. Je předpona ID balíčku běžné něco, co by neměl patřit do jakékoli jednotlivých vlastník nebo organizace?

1. By *není* rezervace předpony ID balíčku způsobit nejednoznačnost a záměny pro komunitu?

1. Jsou identifikující vlastnosti balíčků, které odpovídají jasné a konzistentní předpona ID balíčku (zejména autora balíčku)?

1. Mají balíčky licenci (pomocí [licence](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license) metadat elementu a není licenseUrl, který již není používán)?

## <a name="third-party-feed-provider-scenarios"></a>Informační kanál zprostředkovatele scénáře třetích stran

Pokud zprostředkovatel kanálů od jiných dodavatelů má zájem o implementaci vlastní služby k poskytování rezervace předpony, můžete toho dosáhnout úpravou vyhledávací služba ve verzi 3 NuGet kanálu poskytovatelů. Přidání do informačního kanálu vyhledávací službu, je přidat *ověřit* vlastnost, s příklady pro informační kanály V3 níže. Klienta NuGet nebudou podporovat přidání vlastnosti v kanálu V2.

Další informace najdete v tématu [dokumentaci k rozhraní API služby search](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Balíček předpona ID rezervace sporu zásad
Pokud si myslíte, že vlastník na [NuGet.org](https://www.nuget.org) byla přiřazena rezervace předpony ID balíčku, přejde na výše uvedená kritéria, nebo porušuje na ochranné známky nebo autorských práv, prosím e-mailu [ support@nuget.org ](mailto:support@nuget.org)dotyčný předpona ID, vlastník předpona ID a důvod sporných rezervace přiřazené předpony.

