---
title: Zásady správného řízení projektu NuGet
description: Model zásad správného řízení pro NuGet, včetně rolí a odpovědností pro vývojáře, přispěvatele a uživatele.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2aaaf41b3fc4ef3621333e5099780b5d7ef393bc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64500399"
---
# <a name="nuget-governance"></a>NuGet zásady správného řízení

> Tento dokument je založen na [benevolentní diktátorský model řízení na](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) Univerzitě v Oxfordu. Je licencován pod [Creative Commons Attribution-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Projekt NuGet je veden benevolentním diktátorem a řízen komunitou. To znamená, že komunita aktivně přispívá k každodenní údržbě projektu, ale obecnou strategickou linii je nakreslena benevolentním diktátorem. V případě neshody má benevolentní diktátor poslední slovo.

Úkolem benevolentního diktátora je řešit spory v rámci komunity a zajistit, aby projekt mohl postupovat koordinovaným způsobem. Na druhé straně je úkolem komunity řídit rozhodnutí benevolentního diktátora prostřednictvím aktivníangažovanosti a příspěvku.

## <a name="roles-and-responsibilities"></a>Role a odpovědnosti

Jsou zde popsány čtyři role: Benevolentní diktátor, vývojáři, přispěvatelé a uživatelé.

### <a name="benevolent-dictator"></a>Benevolentní diktátor

Základní tým NuGet je samozvaný benevolentní diktátor nebo vedoucí projektu. Nicméně, protože komunita má vždy schopnost viditelně, tým je plně odpovědný komunitě. Očekává se, že vedoucí projektu pochopí komunitu jako celek a bude se snažit uspokojit co nejvíce protichůdných potřeb a zároveň zajistí, aby projekt dlouhodobě přežil.

V mnoha ohledech je úloha benevolentního diktátora méně o diktatuře, jako spíše o diplomacii. Klíčem je zajistit, aby, jak se projekt rozšiřuje, právo lidé jsou uvedeny vliv na to a společenství shromáždění za vizi projektu vést. Úkolem zájemce je pak zajistit, aby vývojáři (viz níže) učinili správná rozhodnutí jménem projektu. Obecně řečeno, pokud jsou vývojáři v souladu se strategií projektu, vedoucí projektu jim umožní pokračovat, jak chtějí.

Kromě toho pracovníci .NET Foundation zvážit vedoucí projektu primární nebo první kontaktní místo pro NuGet pro účely obchodních operací, včetně registrace domén a technické služby (např. podepisování kódu).

### <a name="committers"></a>Vývojáři

Vývojáři jsou přispěvatelé, kteří trvale cenné příspěvky nuget a jsou jmenováni benevolentní diktátor. Jakmile jsou vývojáři jmenováni, spoléhají se na to, že budou psát kód přímo do úložiště a prověřovat příspěvky ostatních. Vývojáři jsou často vývojáři, ale mohou přispět jinými způsoby.

Obvykle se vývojář zaměřuje na konkrétní aspekt projektu a přináší úroveň odborných znalostí a porozumění, která jim získává respekt komunity a vedoucího projektu. Role vývojáře není oficiální, je to prostě pozice, kterou vlivní členové komunity přebírají, protože vedoucí projektu se na ně dívá jako na vedení a podporu.

Vývojáři nemají žádnou autoritu, pokud jde o celkový směr NuGet. Nicméně, oni mají ucho vedoucího projektu. Úkolem vývojáře je zajistit, aby si vedoucí byl vědom potřeb a kolektivních cílů komunity, a pomáhat rozvíjet nebo přinášet odpovídající příspěvky k projektu. Často jsou committers neformální kontrolu nad svými konkrétními oblastmi odpovědnosti a jsou jim přidělena práva přímo modifikovat určité oblasti zdrojového kódu. To znamená, že i když vývojáři nemají explicitní rozhodovací pravomoc, často zjistí, že jejich činy jsou synonymem pro rozhodnutí vedoucího.

### <a name="contributors"></a>Přispěvatelé

Přispěvatelé jsou členové komunity, kteří odesílají opravy nuget. Tyto záplaty mohou být jednorázový výskyt nebo se vyskytují v průběhu času. Očekává se, že přispěvatelé předkládají opravy, které jsou zpočátku malé a zvětšují se, když přispěvatel, vývojáři a vedoucí projektu vybudovali důvěru v kvalitu oprav přispěvatele. Přispěvatelé jsou rozpoznáni v přidruženém dokumentu poznámky k verzi produktu.

Před odesláním první opravy přispěvatele do úložiště musí podepsat [licenční smlouvu přispěvatele](http://en.wikipedia.org/wiki/Contributor_License_Agreement) nebo smlouvu o přiřazení k nadaci .NET Foundation. Oprava může být předložena a projednána, ale nemůže být skutečně potvrzena do úložiště bez příslušného papírování. Chcete-li získat licenční smlouvu s přispěvatelem, zašlete žádost e-mailem na adresu [contributions@nuget.org](mailto:contributions@nuget.org).

Chcete-li se stát přispěvatelem, odešlete žádost o přijetí vyžádat do jednoho z následujících úložišť:

- [Klient NuGet](https://github.com/NuGet/NuGet.Client)
- [Galerie NuGet](https://github.com/nuget/nugetgallery)
- [Dokumenty NuGet](https://github.com/nuget/nugetdocs)

Podrobný proces odeslání žádosti o přijetí vyžádat se liší podle úložiště:

- [Pokyny k příspěvku pro klienta NuGet a galerii NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Pokyny k příspěvkům pro NuGet Docs](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Uživatelé

Uživatelé jsou členové komunity, kteří potřebují a používají NuGet jako příjemci balíčků a/nebo autoři. Uživatelé jsou nejdůležitějšími členy komunity: bez nich by projekt neměl žádný účel. Uživatel může být kdokoli; neexistují žádné zvláštní požadavky.

Uživatelé by měli být povzbuzováni k účasti v životě NuGet a komunity co nejvíce. Příspěvky uživatelů umožňují projektovému týmu zajistit, že uspokojují potřeby těchto uživatelů. Běžné aktivity uživatelů zahrnují mimo jiné následující:

- Obhajování využití projektu
- Informování vývojářů o silných a slabých stránkách projektu z pohledu nového uživatele
- Poskytování morální podpory (poděkování ujde dlouhou cestu)
- Psaní dokumentace a výukových programů
- Podávání hlášení chyb a žádostí o funkce
- Účast na komunitních akcích, jako jsou například chyby
- Účast na diskusních fórech nebo fórech

Uživatelé, kteří se na projektu a jeho komunitě nadále zapojují, se často stále více zapojují. Tito uživatelé se pak mohou stát přispěvateli, jak je popsáno výše.

## <a name="package-succession-under-special-circumstances"></a>Dědění souborných služeb za zvláštních okolností

V nešťastné situaci, kdy je držitel účtu NuGet nezpůsobilý nebo zesnulý, budeme spolupracovat s komunitou na přidání vhodného vlastníka / s do balíčku, kde uvedený účet má výhradní vlastnictví a balíček je zveřejněn pod [licencí schválenou OSI](https://opensource.org/licenses/alphabetical). Chcete-li požádat o vlastnictví, musíte nám zaslat následující dokumenty:

1. Fotokopie vašeho vládního průkazu totožnosti s fotografií.
1. Jeden z následujících dokladů prokazujících stav předchozího majitele účtu: 
    - Úřední úmrtní list vydaný vládou, pokud předchozí držitel účtu zemřel, nebo
    - Ověřený doklad, jako je potvrzení podepsané zdravotnickým pracovníkem odpovědným za péči o nezpůsobilého držitele účtu.
1. Jeden z následujících dokladů prokazujících vaše vlastnické právo: 
    - Oddací list prokazující, že jste pozůstalým manželem nebo manželkou majitele účtu,
    - Podepsaná plnou moc,
    - Kopie závěti nebo důvěryhodného dokumentu, který vás jmenuje vykonavatelem nebo příjemcem,
    - Rodný list pro majitele účtu, pokud jste jejich rodiče, nebo
    - Opatrovnictví papírování, pokud jste zákonným zástupcem majitele účtu.

Pokud se ocitnete v nouzi s odkazem na [support@nuget.org](mailto:support@nuget.org) tyto zásady, zašlete nám e-mail na adresu s ID a verzí balíčku.

## <a name="transparency"></a>Průhlednost

Pro jeho úspěch je zásadní budování důvěry komunity ve správu projektu s otevřeným zdrojovým kódem. Za tímto účelem musí být rozhodování prováděno transparentním a otevřeným způsobem. Diskuse o směřování projektu musí být provedena veřejně. Komunita by nikdy neměla být zaskočena rozhodnutím benevolentního diktátora. Kromě toho musí být archivována diskuse o rozhodnutích projektu, aby členové komunity mohli pochopit celou historii rozhodnutí a jeho kontext.
