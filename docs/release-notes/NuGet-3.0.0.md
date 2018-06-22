---
title: Poznámky k verzi 3.0 NuGet
description: Poznámky k verzi pro včetně NuGet 3.0.0 – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 26236c2db0e1a6be9c660905db567d9ebbbbe377
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820287"
---
# <a name="nuget-30-release-notes"></a>Poznámky k verzi 3.0 NuGet

[Poznámky k verzi RC2 NuGet 3.0](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 poznámky k verzi](../release-notes/nuget-3.1.md)

NuGet 3.0 byla vydána 20. července 2015 jako sada rozšíření pro Visual Studio 2015. Jsme nabídnutých k poskytování této verze pomocí sady Visual Studio, takže dokončení aktualizované NuGet 3.0 prostředí budou k dispozici pro nové uživatele v sadě Visual Studio. Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.

Doporučujeme, abyste tyto vývojáři, kteří mají přístup k sadě Visual Studio Galerie aktualizaci na nejnovější verzi, která je k dispozici, protože jsme publikují aktualizace krátce po vydání sady Visual Studio 2015, který obsahuje podporu pro vývoj pro Windows 10.

Celkem, jsme uzavřený 240 problémy ve verzi 3.0 a vy můžete zkontrolovat [úplný seznam problémů na Githubu](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Známé problémy

Došlo k několika známých problémů doručit v této verzi a všechny tyto položky jsou pevné v našem naplánované 3.1 verzi se shoduje s verzí Windows 10 na července 29.  Budete moci aktualizovat vaše rozšíření sady Visual Studio z galerie stejné nebo pozdější datum o vyřešení těchto známých problémů.

*  Překlad není k dispozici pro popisek "Nezobrazovat tuto" na okno náhledu a popisku "Autoři" v okně Popis balíčku.
*  Pokud jste práci na projektu pomocí sady TFS ovládací prvek zdroje, NuGet nelze prezentovat Správce balíčků uživatelské rozhraní Pokud souboru Nuget.Config je označena jako jen pro čtení.
   * **Alternativní řešení** rezervovat soubor ze sady TFS.
*  Text v žlutý "restartování pruh" v okně NuGet Powershell není viditelný, při použití tmavý motiv sady Visual Studio.
   * **Alternativní řešení** použít motiv světlý Visual Studio.


## <a name="summary-of-top-issues-resolved"></a>Souhrn nejvyšší vyřešení problémů

* [Aktualizace časté sítě volá při aktualizuje okno Správce balíčků](https://github.com/NuGet/Home/issues/515)
* [Odložené scroll při zobrazení změna na instalaci v Správce balíčků](https://github.com/NuGet/Home/issues/519)
* [Volání sítě by měl být spouštěn na vlákna na pozadí](https://github.com/NuGet/Home/issues/516)
* [Přidat zaškrtávací políčko "Nezobrazovat okno náhledu.](https://github.com/NuGet/Home/issues/566)
* [Omezení ke snížení využití procesoru přidané procesů](https://github.com/NuGet/Home/issues/356)
* Vylepšené zpracování reference knihovny tříd portable
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Služba pro automatické dokončování se malá a velká písmena](https://github.com/NuGet/Home/issues/198)
* [Aktualizace znovu zavést pověření základního ověřování](https://github.com/NuGet/Home/issues/456)
* [Chyba vylepšené protokolování](https://github.com/NuGet/Home/issues/407)
* [Vylepšené prostředí powershell chybové zprávy při volání metody balíčku aktualizace](https://github.com/NuGet/Home/issues/5)
* [Pevný odkaz "Další informace o možnostech, aby se zabránilo chybám ve Windows 10](https://github.com/NuGet/Home/issues/822)
* [Mějte na paměti, nastavení předběžné verze zaškrtávací políčko](https://github.com/NuGet/Home/issues/732)
* [Vylepšené shromáždění výkonu pomocí ukládání do mezipaměti výsledky napříč projekty v řešení](https://github.com/NuGet/Home/issues/721)
* [Paralelní se dají shromáždit více balíčků.](https://github.com/NuGet/Home/issues/713)
* [Odebrat install-package-force příkaz](https://github.com/NuGet/Home/issues/697)

Prosím dohlížet na [náš blog](http://blog.nuget.org) další průběh a oznámení jako jsme Příprava poskytovat podporu pro vývoj pro Windows 10.