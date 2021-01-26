---
title: Zásady správného řízení projektu NuGet
description: Model zásad správného řízení pro NuGet, včetně rolí a zodpovědností pro svěření, přispěvatele a uživatele.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2edaac0218dc936ea6bfe1814c0aab963028ea87
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775603"
---
# <a name="nuget-governance"></a>Zásady správného řízení NuGet

> Tento dokument je založený na [modelu zásad správného řízení Benevolent Dictator](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) na University of Oxford. Licence na produkt Creative- [2,0 Attribution-ShareAlike UK: anglie & Wales](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Projekt NuGet vychází z Benevolent Dictator a je spravovaný komunitou. To znamená, že komunita aktivně přispívá k každodenní údržbě projektu, ale obecný strategický řádek je vykreslen Benevolent Dictator. V případě odsouhlasení má Benevolent Dictator poslední slovo.

Jedná se o úlohu Benevolent Dictator k řešení sporů v rámci komunity a k zajištění toho, aby projekt byl schopný sestavovat koordinovaným způsobem. V takovém případě se jedná o úlohu komunity, která bude řídit rozhodnutí Benevolent Dictator prostřednictvím aktivní zapojení a příspěvku.

## <a name="roles-and-responsibilities"></a>Role a povinnosti

Tady jsou popsané čtyři role: Benevolent Dictator, potvrzování, přispěvatelé a uživatelé.

### <a name="benevolent-dictator"></a>Benevolent dictator

Jádro NuGet Core je samoně určené jako Benevolent Dictator nebo vedoucí projektu. Protože ale komunita má vždycky možnost rozvětvení, tým je plně zodpovězený na komunitu. Očekává se, že vedoucí projektu porozumí komunitě jako celek a snaží se co nejlépe naplnit tolik konfliktních potřeb a zároveň zajistit, aby byl projekt v dlouhodobém horizontu.

V mnoha ohledech je role Benevolent dictator méně o dictatorship a další informace o Diplomacy. Klíčem je zajistit, že se po rozšíření projektu nastanou jejich vliv na pravé lidi a na komunitu, které Rallies za vizi vedoucího projektu. Úkolem vedoucího je, aby se zajistilo, že odesílatelé (viz níže) učiní správná rozhodnutí jménem projektu. Obecně řečeno, pokud jsou odesílatelé zarovnané na strategii projektu, vedoucí projektu jim umožní pokračovat v tom, jak chtějí.

Navíc zaměstnanci .NET Foundation považují projekt za primární nebo první kontaktní bod pro NuGet pro účely obchodních operací, včetně registrací domény a technických služeb (např. podepisování kódu).

### <a name="committers"></a>37 přispěvatelů

Odesílatelé jsou přispěvatelé, kteří udělali cenné příspěvky do NuGet a jsou určené Benevolent Dictator. Po jmenování se spoléhají na to, že zapisují kód přímo do úložiště a zobrazí další příspěvky. Přídávajících jsou často vývojáři, ale můžou přispívat jiným způsobem.

Obvykle se přípravek zaměřuje na konkrétní aspekt projektu a přináší úroveň odbornosti a porozumění, který jim získá ohled na komunitu a vedoucího projektu. Role žadatele není oficiální, je to jednoduše pozice, kterou neberou členové komunity jako vedoucí k tomu, aby měli pokyny a podporu.

Potvrzování nemají žádnou autoritu, kde je celkový směr NuGet. Nicméně mají v vedoucím projektu ušní zájem. Je to úloha odesílatele, která zajistí, že si potenciální zákazník klade informace o potřebách komunity a jejich kolektivních cílech a pomohli nám s vývojem a příjímat vhodné příspěvky k projektu. Příslušnci mají často neformální kontrolu nad jejich konkrétní oblastí zodpovědnosti a jsou jim přiřazena práva k přímé úpravě určitých oblastí zdrojového kódu. To znamená, že i když přípravci nemají explicitní rozhodovací autoritu, často zjistí, že jejich akce jsou synonymem rozhodnutí učiněných zájemcem.

### <a name="contributors"></a>Přispěvatelé

Přispěvatelé jsou členové komunity, kteří odesílají opravy do NuGet. Tyto opravy můžou být jednorázové výskyty nebo dojde v průběhu času. Předpokladem je, že přispěvatelé odesílají opravy, které jsou malé a větší, když přispěvatel, žadatelé a vedoucí projektu sestavili důvěru ve kvalitě oprav v přispěvateli. Přispěvatelé jsou rozpoznáni v dokumentu poznámky k verzi přidruženého produktu.

Před vložením do úložiště se první oprava přispěvatele musí podepsat [licenční smlouvu přispěvatele](http://en.wikipedia.org/wiki/Contributor_License_Agreement) nebo smlouvu o přiřazení k rozhraní .NET Foundation. Opravu je možné odeslat a probrat, ale nemůžete ji ve skutečnosti zaslat do úložiště, aniž by to mělo odpovídající paperwork. Pokud chcete získat licenční smlouvu přispěvatele, odešlete prosím žádost e-mailem na adresu [contributions@nuget.org](mailto:contributions@nuget.org) .

Pokud se chcete stát přispěvatelem, odešlete žádost o přijetí změn do jednoho z následujících úložišť:

- [Klient NuGet](https://github.com/NuGet/NuGet.Client)
- [Galerie NuGet](https://github.com/nuget/nugetgallery)
- [Dokumentace k NuGet](https://github.com/nuget/nugetdocs)

Podrobný proces odeslání žádosti o získání dat se liší podle úložiště:

- [Pokyny k příspěvku pro klienta NuGet a galerii NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Pokyny k příspěvkům pro dokumenty NuGet](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Uživatelé

Uživatelé jsou členy komunity, kteří potřebují a používají NuGet, jako spotřebitelé balíčku nebo autoři. Uživatelé jsou nejdůležitějšími členy komunity: bez nich by projekt neměl mít žádný účel. Kdokoli může být uživatel; neexistují žádné zvláštní požadavky.

Uživatelé by měli být povzbuzeni, aby se účastnili životnosti NuGet a komunity co nejvíce. Příspěvky uživatelů umožňují týmu projektu zajistit, že vyhovují potřebám těchto uživatelů. Mezi běžné aktivity uživatelů patří mimo jiné tyto:

- Poradce pro použití projektu
- Informování vývojářů a slabých stránek projektů z perspektivy nového uživatele
- Poskytování podpory morální (Děkujeme, že se jedná o dlouhou možnost)
- Psaní dokumentace a výukových kurzů
- Vytváření sestav o chybách a žádostí o funkce
- Účast na událostech komunity, jako je například Chyba bashes
- Účast na diskuzních vývěskách nebo fórech

Uživatelé, kteří pokračují v zapojení do projektu a jeho komunity, často zjistí, že se tím stanou ještě více a s dalšími účastníky. Tito uživatelé pak mohou začít, aby se stali přispěvateli, jak je popsáno výše.

## <a name="package-succession-under-special-circumstances"></a>Úspěch balíčku za zvláštních okolností

Ve unfortunate situaci, kdy je držitel účtu NuGet incapacitated nebo zemřelý, budeme spolupracovat s komunitou, aby do balíčku přidal příslušné vlastníky/s, kde má daný účet výhradní vlastnictví a balíček je publikovaný v rámci [licence OSI schválené](https://opensource.org/licenses/alphabetical). Pokud chcete požádat o vlastnictví, musíte nám poslat následující dokumenty:

1. Fotokopie vašeho ID fotografie vydané vládou
1. Jeden z následujících dokumentů prokazující stav předchozího držitele účtu: 
    - Oficiální certifikát smrti státní správy, pokud se předchozí držitel účtu přestane nastavovat, nebo
    - Certifikovaný dokument, jako je certifikát podepsaný lékařským odborníkem, který se stará o péči držitele účtu incapacitated.
1. Jeden z následujících dokumentů potvrzujících právo na vlastnictví: 
    - Certifikát sňatku ukazující, že jste držitelem držitele účtu, který jste si pozůstali.
    - Podepsaná mocnina právního zástupce,
    - Kopie nebo vztahu důvěryhodnosti dokumentu, který můžete pojmenovat jako vykonavatel nebo příjemce,
    - Certifikát pro narození držitele účtu, pokud jste jeho rodiče, nebo
    - Strážce paperwork, pokud jste právní opatrovník držitele účtu.

Pokud zjistíte, že tuto zásadu potřebujete vyvoláni, pošlete nám e-mail [support@nuget.org](mailto:support@nuget.org) s ID a verzí balíčku.

## <a name="transparency"></a>Transparentnost

Sestavování důvěry komunity v rámci zásad správného řízení pro open source projekt je zásadní pro jeho úspěch. K tomuto účelu se rozhodování musí provádět transparentním a otevřeným způsobem. Diskuze o směru projektu se musí provádět veřejně. Komunita by nikdy neměla být bez ochrany odlovena rozhodnutím Benevolent Dictator. Kromě toho musí být diskuze o rozhodnutích projektu archivována, aby členové komunity mohli porozumět celé historii rozhodnutí a jeho kontextu.
