---
title: Poznámky k verzi 3.0 NuGet
description: Zpráva k vydání verze pro NuGet 3.0.0 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551860"
---
# <a name="nuget-30-release-notes"></a>Poznámky k verzi 3.0 NuGet

[Zpráva k vydání verze NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [zpráva k vydání verze NuGet 3.1](../release-notes/nuget-3.1.md)

20. července 2015 byla vydána NuGet 3.0 jako rozšíření sady Visual Studio 2015. Můžeme nabídnout poskytovat této vydané verzi sady Visual Studio tak, aby kompletní aktualizované prostředí NuGet 3.0 by být k dispozici pro nové uživatele služby Visual Studio. Tato verze rozšíření NuGet dostupná jenom pro Visual Studio 2015.

Doporučujeme, abyste tyto vývojáře, kteří mají přístup ke službě update Galerie sady Visual Studio na nejnovější verzi, která je k dispozici, protože aktualizace publikujeme krátce po vydání sady Visual Studio 2015, která obsahuje podporu pro vývoj pro Windows 10.

Celkem, jsme uzavřeli 240 problémech ve verzi 3.0 a můžete zkontrolovat [úplný seznam všech problémů na Githubu](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Známé problémy

Došlo k několika problémech doručit v této vydané verzi a všechny tyto položky jsou opravené v našich plánovaných verzi 3.1 se shoduje s verzí Windows 10 na 29. července.  Budete moct aktualizovat vaše rozšíření sady Visual Studio z Galerie nebo po tomto datu k řešení těchto známých problémů.

*  Překlad není k dispozici pro "není tuto zprávu nezobrazovat" popisek v okně verze preview a "Autoři" popisek v okně Popis balíčku.
*  Když pracujete na projektu pomocí TFS ovládací prvek zdroje, NuGet nelze prezentovat Správce balíčků uživatelské rozhraní je-li soubor Nuget.Config je označena jako jen pro čtení.
   * **Alternativní řešení** rezervovat soubor ze serveru TFS.
*  Text žlutě "restartování bar", v okně Powershellu NuGet není viditelný, při použití tmavého motivu sady Visual Studio.
   * **Alternativní řešení** pomocí sady Visual Studio světlý motiv.


## <a name="summary-of-top-issues-resolved"></a>Přehled hlavních problémů vyřešit

* [Sítě časté aktualizace se volá, když se aktualizuje okno Správce balíčků](https://github.com/NuGet/Home/issues/515)
* [Zpožděné posuvníku při změně na instalaci zobrazení ve správci balíčků](https://github.com/NuGet/Home/issues/519)
* [Volání sítě by měl běžet na vlákně na pozadí](https://github.com/NuGet/Home/issues/516)
* [Přidá zaškrtávací políčko "Nezobrazovat okno náhledu.](https://github.com/NuGet/Home/issues/566)
* [Přidání procesu omezování ke snížení využití procesoru](https://github.com/NuGet/Home/issues/356)
* Vylepšené zpracování odkaz na přenosné knihovny tříd
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Automatické dokončování službě se malá a velká písmena](https://github.com/NuGet/Home/issues/198)
* [Aktualizace znovu zavést pověření základního ověřování](https://github.com/NuGet/Home/issues/456)
* [Vylepšené chybové protokolování](https://github.com/NuGet/Home/issues/407)
* [Vylepšené prostředí powershell chybových zpráv při volání metody Update-Package](https://github.com/NuGet/Home/issues/5)
* [Oprava propojení, kde se dozvíte o možnostech' aby se zabránilo selhání ve Windows 10](https://github.com/NuGet/Home/issues/822)
* [Mějte na paměti nastavení zaškrtávacího políčka předběžné verze](https://github.com/NuGet/Home/issues/732)
* [Vylepšené shromažďování výkonu díky ukládání do mezipaměti výsledky ve všech projektech v řešení](https://github.com/NuGet/Home/issues/721)
* [Současně se dají shromáždit víc balíčků.](https://github.com/NuGet/Home/issues/713)
* [Odebrat install-package-force příkaz](https://github.com/NuGet/Home/issues/697)

Prosím dohlížet na [náš blog o](http://blog.nuget.org) další průběh a oznámení podle Připravíme k poskytování podpory pro vývoj pro Windows 10.