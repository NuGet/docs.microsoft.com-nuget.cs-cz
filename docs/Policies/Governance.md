---
title: Zásady správného řízení projektů NuGet
description: Model zásad správného řízení pro NuGet, včetně role a zodpovědnosti committers, přispěvatelé a uživatelů.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 37bfd146eefd52fd0332f3b99fa36651fc5c93d4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-governance"></a>Zásady správného řízení NuGet

> Tento dokument je založen na [Benevolent Model řízení Dictator](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) podle univerzity Oxford. Je licencován [Creative Commons uvedení ShareAlike 2.0 UK: Anglii & Walesu licence](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Projekt NuGet je vedla podle Benevolent Dictator a spravuje komunitou. To znamená komunita aktivně přispívá ke každodenní správě projektu, ale obecné strategické řádku vykreslením podle benevolent dictator. V případě neshody má benevolent dictator poslední slovo.

Je úloha benevolent dictator řešení sporů v rámci komunity a zajistěte, aby byl projekt moct průběhu koordinovaným způsobem. Pak je na Průvodce rozhodnutí, která benevolent dictator prostřednictvím active engagement a příspěvek Společenství úlohy.

## <a name="roles-and-responsibilities"></a>Role a zodpovědnosti

Existují čtyři role postupu popsaného tady: Benevolent Dictator, Committers, přispěvatelé a uživatelů.

### <a name="benevolent-dictator"></a>Benevolent dictator

Tým core NuGet je samoobslužné určené jako realizace Benevolent Dictator nebo projektu. Ale protože komunity vždy má schopnost rozvětvení, týmem je plně zodpovědět komunitě. Realizace projektu se očekává pochopit komunity jako celek a snažit splnit mnoho konfliktní stačit nejdříve, a zajistit, že projekt odolává z dlouhodobého hlediska.

V mnoha směrech je role benevolent dictator menší o dictatorship a informace o diplomacii. Klíč je potřeba zajistit, že jako projekt rozšíří, příslušní lidé mají vliv a komunitou rallies za vizi realizace projektu. Úloha zájemce je pak zajistit, aby bylo rozhodnutí správné jménem projektu committers (viz níže). Obecně řečeno, dokud committers jsou v souladu s projektu strategie, realizace projektu mu umožní pokračovat, protože chtějí mít.

Kromě toho .NET Foundation pracovníci zvažte realizace projektu primární nebo první bod kontaktu pro NuGet pro účely podnikové operace, včetně registrací domény a technické služby (například podepisování kódu).

### <a name="committers"></a>Committers

Committers jsou přispěvatelé, kteří provedli dlouhodobě cenné příspěvky NuGet a jmenuje Benevolent Dictator. Jakmile jmenováno, spoléhat committers k zápisu kódu přímo do úložiště a obrazovky příspěvky jiných. Committers jsou často vývojáři ale můžete přispívat jinými způsoby.

Obvykle committer se zaměřuje na konkrétních aspektů projektu a přináší úroveň znalosti a pochopení, která je mírou dodržování komunity a realizace projektu. Role committer není oficiální jeden, je jednoduše pozici, která předpokládá vliv členové komunity služby jako vypadá realizace projektu jim pokyny a podporu.

Committers mají žádná oprávnění, kde se týká celkové směr NuGet. Ale mají vymazat zájemce projektu. Je úlohy committer zajistit, že zájemce známa potřeb a souhrnný cíle Společenství a usnadňují vývoj nebo vyvolat odpovídající příspěvky k projektu. Často committers mají neformální kontrolu nad jejich konkrétní oblasti zodpovědnosti a jsou přiřazeny přímo měnit určitých oblastí ve zdrojovém kódu. To znamená i když committers nemusí explicitní rozhodovacích autority, budou často najdou, jejich akce jsou totožná s rozhodnutí, která provedené zájemce.

### <a name="contributors"></a>Contributors

Přispěvatelé jsou členy komunity, kteří odesílají opravy na NuGet. Tyto opravy mohou být jednorázová akce nebo vyskytnout v čase. Očekávání se, že přispěvatelé odeslání opravy, které jsou malé nejprve a zvýší větší při Přispěvatel, committers a realizace projektu jste vytvořili důvěru kvality Přispěvatel opravy. Přispěvatelé rozpoznávají v dokumentu poznámky k verzi produktu přidružené.

Před jeho přispěvatelem první oprava do úložiště, musí se přihlásit [Přispěvatel licenční smlouvy](http://en.wikipedia.org/wiki/Contributor_License_Agreement) nebo přiřazení smlouvu základ .NET. Oprava může být odeslána a popsané ale nemůže být ve skutečnosti potvrdit do úložiště bez odpovídající doklady na místě. Pokud chcete získat Přispěvatel licenční smlouvy, prosím poslat žádost o v e-mailu [ contributions@nuget.org ](mailto:contributions@nuget.org).

K Přispěvatel, odešlete žádost o přijetí změn na jednu z následujících úložiště:

- [Klienta NuGet](https://github.com/NuGet/NuGet.Client)
- [Galerie NuGet](https://github.com/nuget/nugetgallery)
- [Dokumentace NuGet](https://github.com/nuget/nugetdocs)

Podrobný proces odesílání žádosti o přijetí změn se liší podle úložiště:

- [Příspěvek pokyny pro klienty NuGet a Galerie NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Příspěvek pokyny pro dokumenty NuGet](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Uživatelé

Uživatelé jsou členy komunity, kteří mají potřeba a použít NuGet, jako balíček příjemci nebo autoři. Uživatelé jsou nejdůležitější členové komunity: bez, projekt by mít žádný účel. Každý, kdo může být uživatel; nejsou žádné zvláštní požadavky.

Uživatelé by měly při účastnit dobu životnosti NuGet a co nejvíce komunity. Povolit uživatele příspěvky projektový tým zajistit, že jejich jsou splňující potřeby těchto uživatelů. Běžné činnosti uživatele patří, ale nejsou omezeny na následující:

- Zasazovat o pro použití projektu
- Informuje o vývojáři síly projektu a slabá místa z hlediska nového uživatele
- Zajištění právnická podpory (Děkujeme vám bude způsob, jak dlouho)
- Zápis dokumentace a cvičení
- Vyplnění sestavy chyb a žádosti o funkce
- Účastní komunity událostmi, například bashes chyb
- Účastí v diskusní vývěsky nebo fóra

Uživatelé, kteří se spojte s projekt a její komunitě i nadále často najít sami stal více zahrnuta. Tyto uživatele může potom přejděte se přispěvatele, jak je popsáno výše.

## <a name="package-succession-under-special-circumstances"></a>Balíček po sobě zvláštní okolnosti

V velice nepříjemná situaci kterých držitel účtu NuGet je jejich vyřazení z funkce nebo zemřelý jsme budete pracovat s komunitou přidání odpovídající vlastníka nebo s do balíčku, kde uvedené účet má jedinou vlastnictví a balíček je publikována v části [OSI schválení licence](https://opensource.org/licenses/alphabetical). Požádat o vlastnictví, je potřeba poslat nám v následujících dokumentech:

1. Fotokopie ID vašeho vydané vládou fotografii.
1. Jedna z následujících dokumentech prokázání stav předchozí držitel účtu: 
    - Certifikát oficiální, vydané vládou smrti Pokud předchozí držitel účtu zemřelý, nebo,
    - Dokument, certifikovaným třeba certifikát podepsaný službou lékařské professional starosti péče o držitel nezpůsobilých účtu.
1. Jedna z následujících dokumentech prokázání vaše právo na vlastnictví: 
    - Certifikát manželství zobrazující, že jste hostujícího manžela vlastníka účtu
    - Podepsaný moci power
    - Kopie budou nebo vztahu důvěryhodnosti dokumentu pojmenování můžete jako vykonavatele nebo oprávněná osoba,
    - Certifikát narození pro vlastníka účtu, pokud je jeho nadřazeným prvkem, nebo,
    - Pokud jste právní ochrany vlastníka účtu opatrovníka doklady.

Pokud se přistihnete potřeba zkontrolovat vyvolání tuto zásadu, nám prosím pošlete e-mail na [ support@nuget.org ](mailto:support@nuget.org) s ID a verzi balíčku.

## <a name="transparency"></a>Průhlednost

Vytvoření vztahu důvěryhodnosti komunity v zásad správného řízení open source projektu je potřeba jeho úspěch. Za tímto účelem je třeba provést rozhodování transparentní, otevřete způsobem. Diskuze o projektu směru, je třeba provést veřejně. Komunita by měl být nikdy zachycena rozhodnutím podle Benevolent Dictator nepřipravené. Kromě toho musí diskuzi o projektu rozhodnutí archivovat tak, aby členové komunity můžete porozumět celou historii rozhodnutí a jeho kontextu.
