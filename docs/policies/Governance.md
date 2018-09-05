---
title: Zásady správného řízení projektu NuGet
description: Model zásady správného řízení pro NuGet, včetně role a zodpovědnosti pro přispěvatelů, přispěvatelů a uživatelů.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2aaaf41b3fc4ef3621333e5099780b5d7ef393bc
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549447"
---
# <a name="nuget-governance"></a>Zásady správného řízení NuGet

> Tento dokument je založen na [dobrovolnické modelu zásad správného řízení Dictator](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) podle University Oxford. Je licencován [Creative Commons Attribution-ShareAlike 2.0 VB: Anglie & licenci Wales](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Projekt NuGet je vedené dobrovolnické Dictator a spravuje komunity. To znamená komunity aktivně přispívá ke každodenní údržbu projektu, ale obecné strategické linie vychází podle dobrovolnické dictator. V případě neshody má dobrovolnické dictator poslednímu slovu.

Je úloha dobrovolnické dictator řešení sporů v rámci komunity a ujistěte se, že se projekt průběh koordinovaným způsobem. Pak se úlohy od komunity a provede rozhodnutí dobrovolnické dictator prostřednictvím aktivního zapojení a příspěvek.

## <a name="roles-and-responsibilities"></a>Role a zodpovědnosti

Existují čtyři role je zde popsáno: dobrovolnické Dictator, přispěvatelů, přispěvatelů a uživatelů.

### <a name="benevolent-dictator"></a>Dobrovolnické dictator

Tým core NuGet je držitelem určené jako vedoucí projektu nebo dobrovolnické Dictator. Protože však komunity vždy má schopnost forku, tým je plně zodpovědět v komunitě. Vedoucí projektu se očekává komunity jako celek porozuměním snažit splnit jako řada konfliktní musí nejdříve, přitom zajistit, že projekt odolává v dlouhodobém horizontu.

V mnoha směrech je role dobrovolnické dictator menší o dictatorship a další informace o diplomacii. Klíč je zajistit, že jako projekt rozšíří, lidé mít vliv a komunity rallies za vizí toho, vedoucí projektu. Úloha zájemce je pak k zajištění, že přispěvatelů (viz níže) dělat správná rozhodnutí jménem projektu. Obecně řečeno za předpokladu, přispěvatelů jsou v souladu s projektu strategie, vedoucí projektu jim umožní pokračovat, protože přejí.

Kromě toho .NET Foundation pracovníky zvažte vedoucí projektu primární nebo první bod kontaktu pro NuGet pro účely obchodních operací včetně registrace domény a technické služby (například podepisování kódu).

### <a name="committers"></a>Přispěvatelů

Přispěvatelů jsou přispěvatelé, kteří provedli zachovaného cenné příspěvky NuGet a jmenuje dobrovolnické Dictator. Jakmile jmenován, spoléhat přispěvatelů k psaní kódu přímo do úložiště i příspěvky z jiné obrazovky. Přispěvatelů jsou často vývojáři, ale může přispívat jinými způsoby.

Obvykle potvrzovatelem se zaměřuje na specifický aspekt projektu a přináší úrovně odborných znalostí a tím, že je nepřesahuje dodržování komunity a vedoucí projektu. Role potvrzovatelem není oficiální jeden, je jednoduše pozici, která se vlivní členové komunity předpokládají jako vyhledá vedoucí projektu jim pokyny a podporu.

Přispěvatelů mít žádná autorita, pokud jde o celkovou směr NuGet. Avšak musí mazat vedoucí projektu. Jde potvrzovatelem úlohu tak, aby byl zájemce vědět potřebám a cílům kolektivní od komunity a usnadňují vývoj nebo vyvolat odpovídající příspěvků do projektu. Často přispěvatelů disponují neformální kontrolu nad jejich konkrétní oblasti zodpovědnosti a jsou přiřazeny práva pro modifikaci přímo určité oblasti zdrojového kódu. To znamená i když přispěvatelů mají explicitní oprávnění rozhodování, často najdou, že jsou jejich akce synonymní s použitím rozhodnutí provedených zájemce.

### <a name="contributors"></a>Contributors

Přispěvatelé jsou členové komunity, kteří odesílají opravy NuGet. Tyto opravy mohou být jednorázová akce nebo nastanou v průběhu času. Očekávání se, že přispěvatelé odeslání opravy, které jsou malé zpočátku i při pozdějším růstu větší při Přispěvatel, přispěvatelů a vedoucí projektu sestavili důvěra v kvalitní přispěvatele opravy. Přispěvatelé jsou rozpoznány v dokumentu poznámky k verzi produktu přidružené.

Před první oprava přispěvatele do úložiště, se musí přihlásit [Přispěvatel licenční smlouvy](http://en.wikipedia.org/wiki/Contributor_License_Agreement) nebo smlouvy, přiřazení a .NET Foundation. Oprava může odeslání a popsaných ale nesmí mít ve skutečnosti zaměřuje na úložiště bez odpovídající doklady na místě. Získat přispěvatele licenční smlouvy, pošlete žádost v e-mailu [ contributions@nuget.org ](mailto:contributions@nuget.org).

Chcete-li Staňte přispěvatelem a odešlete žádost o přijetí změn do jedné z následujících databází:

- [Pro klienta NuGet](https://github.com/NuGet/NuGet.Client)
- [Galerie NuGet](https://github.com/nuget/nugetgallery)
- [Dokumentace pro NuGet](https://github.com/nuget/nugetdocs)

Podrobný postup pro odeslání žádosti o přijetí změn se liší podle úložiště:

- [Pokyny příspěvek pro klienta NuGet a Galerie NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Příspěvek pokyny, jak NuGet Docs](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Uživatelé

Uživatelé jsou členové komunity, kteří je potřeba a použít NuGet, jako balíček uživatele a/nebo autoři. Uživatelé jsou nejdůležitější členové komunity: bez nich projektu by mít žádné účel. Kdokoli může být uživatele. neexistují žádné zvláštní požadavky.

Uživatelé by měly k účasti v životě NuGet a co nejvíc komunity. Příspěvky uživatele povolit projektovým týmem, abyste Ujistěte se, že jejich jsou vyhovující potřebám uživatelů. Běžné činnosti uživatele patří, ale nejsou omezeny na následující:

- Které podporuje pro použití projektu
- Informuje vývojáře projektu silné a slabé stránky z hlediska nového uživatele
- Zajištění morální podpory (děkovného přejde dlouhou cestu)
- Zápis dokumentace a kurzy
- Vyplňte zpráv o chybách a žádosti o funkce
- Účastní komunitní akce, jako je například bashes chyb
- Účast na diskuse tabulí nebo fóra

Uživatelé, kteří dál pokračovat s projektu a její komunita se často naleznou sami sebe stává čím dál tím víc součástí. Tyto uživatele může poté přejděte k stát přispěvatele, jak je popsáno výše.

## <a name="package-succession-under-special-circumstances"></a>Balíček po sobě za zvláštních okolností

V unfortunate situaci, kdy držitel účtu NuGet je jejich vyřazení z funkce nebo zemřel, budete spolupracujeme s komunitou do balíčku, kde uvedeného účtu je jediným vlastníkem a balíček je publikovaný pod přidat odpovídající vlastníka/s [OSI schválené licence](https://opensource.org/licenses/alphabetical). Požádat o vlastnictví musí nám pošlete následující dokumenty:

1. Kopírovacích vaše ID vláda vydala fotografii.
1. Jeden z následujících dokumentech prokázání stav předchozího vlastníka účtu: 
    - Certifikát oficiální, vláda vydala smrti, pokud je předchozí držitel účtu zemřel, nebo,
    - Certifikované dokument jako je například certifikát podepsaný službou lékařské professional starosti péči držitel nezpůsobilý účtu.
1. Jeden z následujících dokumentech prokázání vaše právo na vlastnictví: 
    - Manželství certificate znázorňující, že jste zbývající manželem vlastníka účtu
    - Podepsané moci napájení
    - Kopie pojmenování jako prováděcí modul nebo příjemce, dokument se nebo vztah důvěryhodnosti
    - Certifikát narození pro držitele účtu, pokud jste své nadřazené položky, nebo,
    - Pokud jste zákonný vlastníka účtu opatrovníka doklady.

Pokud zjistíte, které je nutné vyvolání této zásady, odešlete nám e-mail na [ support@nuget.org ](mailto:support@nuget.org) s ID a verzi balíčku.

## <a name="transparency"></a>Transparentnost

Vytváření komunity důvěryhodnost zásad správného řízení projektu open source je zásadní pro její úspěch. K tomuto účelu musí provést způsobem transparentní, otevřete rozhodování. Diskuze o směr projektu je třeba provést veřejně. Měl by ji zachytit nikdy komunity zastihnout nepřipravené podle rozhodnutí dobrovolnické Dictator. Kromě toho musí diskuze o rozhodnutích projektu archivovat tak, aby členové komunity by rozuměla celou historii rozhodnutí a jeho kontextu.
