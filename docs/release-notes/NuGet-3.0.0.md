---
title: Zpráva k vydání verze NuGet 3,0
description: Poznámky k verzi pro NuGet 3.0.0, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776548"
---
# <a name="nuget-30-release-notes"></a>Zpráva k vydání verze NuGet 3,0

Poznámky k verzi [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  Zpráva k [vydání verze NuGet 3,1](../release-notes/nuget-3.1.md)

Sada NuGet 3,0 byla vydána 20. července 2015 jako rozšíření sady Visual Studio 2015. Vložili jsme tuto verzi do sady Visual Studio, aby byly k dispozici kompletní aktualizované prostředí NuGet 3,0 pro nové uživatele sady Visual Studio. Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.

Doporučujeme vývojářům, kteří mají přístup k aktualizaci galerie sady Visual Studio, k nejnovější verzi, která je k dispozici, protože publikujeme krátce po vydání sady Visual Studio 2015, které obsahuje podporu pro vývoj pro Windows 10.

V Total jsme uzavřeli 240 problémů ve verzi 3,0 a můžete si prohlédnout [úplný seznam problémů na GitHubu](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Známé problémy

V této verzi se dostalo několik známých problémů. všechny tyto položky jsou opravené v naší plánované verzi 3,1, aby se shodovaly s vydáním Windows 10 v červenci vysílání 29..  Můžete aktualizovat rozšíření aplikace Visual Studio z Galerie od tohoto data a opravit tyto známé problémy.

*  Pro popisek "Nezobrazovat znovu" v okně náhledu a v popisku "autoři" v okně Popis balíčku není překlad k dispozici.
*  Při práci na projektu pomocí správy zdrojového kódu TFS nemůže NuGet prezentovat uživatelské rozhraní Správce balíčků, pokud je soubor Nuget.Config označený jen pro čtení.
   * **Alternativní řešení** Rezervujte soubor z TFS.
*  Když použijete tmavý motiv sady Visual Studio, text ve žlutém "pravém panelu" v okně PowerShellu NuGet se nezobrazí.
   * **Alternativní řešení** Použijte světlý motiv sady Visual Studio.


## <a name="summary-of-top-issues-resolved"></a>Shrnutí nejdůležitějších vyřešených problémů

* [Častá volání síťové aktualizace po aktualizaci okna Správce balíčků](https://github.com/NuGet/Home/issues/515)
* [Zpožděný posun při změně na nainstalované zobrazení ve Správci balíčků](https://github.com/NuGet/Home/issues/519)
* [Síťová volání by se měla spustit ve vlákně na pozadí.](https://github.com/NuGet/Home/issues/516)
* [Přidáno zaškrtávací políčko nezobrazit Náhled okna](https://github.com/NuGet/Home/issues/566)
* [Přidání omezení procesů pro snížení využití procesoru](https://github.com/NuGet/Home/issues/356)
* Vylepšené zpracování odkazů na přenositelné knihovny tříd
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Služba automatického dokončování rozlišuje velká a malá písmena.](https://github.com/NuGet/Home/issues/198)
* [Aktualizace pro znovu zavedení přihlašovacích údajů základního ověřování](https://github.com/NuGet/Home/issues/456)
* [Vylepšené protokolování chyb](https://github.com/NuGet/Home/issues/407)
* [Vylepšené chybové zprávy PowerShellu při volání rutiny Update-Package](https://github.com/NuGet/Home/issues/5)
* [Opravte odkaz "informace o možnostech", aby se zabránilo chybám ve Windows 10](https://github.com/NuGet/Home/issues/822)
* [Zapamatovat si nastavení zaškrtávacího políčka předběžného vydání](https://github.com/NuGet/Home/issues/732)
* [Lepší výkon při shromažďování díky ukládání výsledků do mezipaměti napříč projekty v řešení](https://github.com/NuGet/Home/issues/721)
* [Paralelní shromažďování více balíčků](https://github.com/NuGet/Home/issues/713)
* [Odebraný příkaz Install-Package-Force](https://github.com/NuGet/Home/issues/697)

Pořiďte si prosím svůj [blog na našem blogu](http://blog.nuget.org) a získejte další informace o průběhu a oznámeních, jak jsme připraveni doručovat podporu pro vývoj pro Windows 10.