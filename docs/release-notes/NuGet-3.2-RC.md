---
title: Zpráva k vydání verze NuGet 3.2 RC
description: Zpráva k vydání verze pro NuGet 3.2 RC, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eafdedc3ad022a6794dbeb390de87d7f317e28f1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551495"
---
# <a name="nuget-32-rc-release-notes"></a>Zpráva k vydání verze NuGet 3.2 RC

[Zpráva k vydání verze NuGet 3.1.1](../release-notes/nuget-3.1.1.md) | [zpráva k vydání verze NuGet 3.2](../release-notes/nuget-3.2.md)

Verze Release candidate NuGet 3.2 byla vydána verze 2. září 2015 jako kolekce vylepšení a oprav pro 3.1.1.  Navíc jsou první verze, které jsou publikovány nejprve nové dist.nuget.org úložiště.

## <a name="new-features"></a>Nové funkce

* Projekty, které živé ve stejné složce, teď můžou mít různé `project.json` soubory v této složce, které jsou specifické pro každý projekt.  Pro každý projekt pojmenujte `project.json` souboru `{ProjectName}.project.json` a NuGet se správně odkazovat a využívat obsah pro každý projekt odpovídajícím způsobem.  Tento atribut podporuje novou funkci [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` Teď podporuje globalPackagesFolder jako relativní cesta - [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Aktualizace příkazového řádku

Toto je první verze nuget.exe klienta, který podporuje v3 servery NuGet a obnovují se balíčky pro projekty spravovaných pomocí `project.json` souboru.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Došlo k několika ověřené informační kanály problémy, které se zákazníky a vyřešené v této verzi ke zlepšení interakce s klientem.

* Instalace / obnovení interakce jenom odeslání přihlašovacích údajů pro počáteční požadavek na ověřeného kanál – [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Příkazu push nelze vyřešit pomocí přihlašovacích údajů z konfigurace – [1248](https://github.com/NuGet/Home/issues/1248)
* Uživatelský agent a záhlaví jsou nyní předány úložiště NuGet, které vám pomůžou s statistiky sledování – [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Provedli jsme několik vylepšení líp řešit selhání sítě při pokusu o práci s jako vzdálené úložiště NuGet:

* Vylepšené chybové zprávy, když nelze se připojit k informačním kanálům vzdálené – [. 1238](https://github.com/NuGet/Home/issues/1238)
* Oprava příkazu NuGet restore správně vrácené 1 v případě, že dojde k chybě - [1186](https://github.com/NuGet/Home/issues/1186)
* Nyní opakování pokusu o připojení k síti každý 200 MS maximálně 5 pokusů v případě chyby HTTP 5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* Vylepšené zpracování přesměrování odpovědi serveru během příkazu push - [. 1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` Teď podporuje název adresy URL nebo úložiště ze souboru Nuget.Config jako argument - [1046](https://github.com/NuGet/Home/issues/1046)
* Chybějící balíčky, které nebyly umístěny v úložišti během obnovení jsou nyní hlášeny jako chyby místo upozornění [1038](https://github.com/NuGet/Home/issues/1038)
* Opravit multipartwebrequest zpracování \r\n pro scénáře, platformy Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Existuje několik oprav na problémy s různými příkazy:

* Příkazu push už nemá GET před PUT zdroji balíčku - [1237](https://github.com/NuGet/Home/issues/1237)
* Příkaz listovat už opakuje čísla verze – [1185](https://github.com/NuGet/Home/issues/1185)
* Pack s argumentem - sestavení nyní správně podporuje C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Opravené problémy s pokusem o pack projektu F # sestavené pomocí sady Visual Studio 2015 – [1048](https://github.com/NuGet/Home/issues/1048)
* Obnovení teď operace, pokud balíčky již existuje - [1040](https://github.com/NuGet/Home/issues/1040)
* Vylepšené chybové zprávy, když `packages.config` soubor je poškozený - [1034](https://github.com/NuGet/Home/issues/1034)
* Oprava příkazu restore s `-SolutionDirectory` přepínač pro práci s relativními cestami - [992](https://github.com/NuGet/Home/issues/992)
* Vylepšené aktualizované příkaz k podpoře celého řešení pro sadu vs11 – [924](https://github.com/NuGet/Home/issues/924)

Úplný seznam problémy vyřešené v této verzi najdete v Githubu NuGet [příkazového řádku milník](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Aktualizace rozšíření sady Visual Studio

### <a name="new-features-in-visual-studio"></a>Nové funkce v sadě Visual Studio

* Do okna Průzkumník řešení na uzel řešení, která umožňuje balíčky obnovit bez sestavování řešení se přidá nová položka nabídky kontextu ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nové balíčky obnovit položky kontextové nabídky](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Aktualizace a opravy v sadě Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Opravy pro ověřené informační kanály byly zahrnuty a zákazníky a vyřešené v rozšíření také.  Následující položky ověřování také se zákazníky a vyřešené v rozšíření:

* Nyní správně považuje NuGet v3 ověřené informační kanály správně, nikoli jako v2 ověřené informační kanály - [1216](https://github.com/NuGet/Home/issues/1216)
* Opravené žádost o ověření přihlašovacích údajů v projektech pomocí `project.json` a komunikaci s informačními kanály v2 - [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Připojení k síti měla vliv na uživatelské rozhraní v sadě Visual Studio a My to řešit pomocí následujících oprav:

* Lepší Údržba místní mezipaměť balíčků verze – [1096](https://github.com/NuGet/Home/issues/1096)
* Změnit chování selhání při připojování k v3 informačního kanálu již došlo k pokusu o ji považovat za kanál v2 – [1253](https://github.com/NuGet/Home/issues/1253)
* Teď nemůžeme instalovat chyby při instalaci balíčku s více zdroji balíčku - [1183](https://github.com/NuGet/Home/issues/1183)

Vylepšili jsme zpracování interakce s následující operace:

* Teď budete pokračovat k sestavení projektů, pokud se obnovují se balíčky pro jednoho projektu selhalo – [1169](https://github.com/NuGet/Home/issues/1169)
* Instalace balíčku do projektu, na kterém závisí jiný projekt v řešení vynutí opětovné sestavení řešení - [981](https://github.com/NuGet/Home/issues/981)
* Oprava instalace balíčku se nezdařilo správně vrátit zpět změny projektu – [. 1265](https://github.com/NuGet/Home/issues/1265)
* Opravit nechtěnému odstranění `developmentDependency` atribut na balíčku v `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Volání `install.ps1` teď mají správnou `$package.AssemblyReferences` objekt předaný - [1245](https://github.com/NuGet/Home/issues/1245)
* Již nadále nebrání odinstaluje balíčků v projektech UPW, zatímco projekt je ve špatném stavu - [1128](https://github.com/NuGet/Home/issues/1128)
* Řešení obsahující kombinaci `packages.config` a `project.json` projekty jsou nyní správně sestavena bez nutnosti sekundy sestavení operace - [1122](https://github.com/NuGet/Home/issues/1122)
* Pokud jsou propojené nebo nachází v jiné složce - správně vyhledání soubory app.config [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Projekty UWP nyní mohou instalovat balíčky neuvedené - [1109](https://github.com/NuGet/Home/issues/1109)
* Obnovení balíčku je teď povolené, zatímco řešení není v uloženém stavu - [. 1081](https://github.com/NuGet/Home/issues/1081)


Zpracování aktualizací konfigurace, které byly opraveny soubory:

* Odebrání už soubor cílů doručovaný balíček na následující sestavení `project.json` spravovaný projekt - [1288](https://github.com/NuGet/Home/issues/1288)
* Už změna souboru Nuget.Config souborů během sestavování řešení ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Při aktualizaci balíčku - už změna nepovoluje omezení verze [1130](https://github.com/NuGet/Home/issues/1130)
* Uzamknout soubory teď zůstanou během sestavování - [1127](https://github.com/NuGet/Home/issues/1127)
* Úpravu `packages.config` a není přepisování během aktualizací - [585](https://github.com/NuGet/Home/issues/585)


Zlepšení interakce s TFS správy zdrojového kódu:

* Už selhání instalace pro balíčky, které jsou vázány na TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Opravené NuGet uživatelského rozhraní pro integraci sady TFS 2013 – [1071](https://github.com/NuGet/Home/issues/1071)
* Opravit odkazy na balíčky se obnovily správně pocházet ze složky packages - [1004](https://github.com/NuGet/Home/issues/1004)

A konečně vylepšili jsme také tyto položky:

* Snížit úroveň podrobností protokolu zpráv pro `project.json` spravované projekty – [1163](https://github.com/NuGet/Home/issues/1163)
* Nyní správně zobrazuje v uživatelském rozhraní – nainstalovaná verze balíčku [1061](https://github.com/NuGet/Home/issues/1061)


Úplný seznam všech problémech, které řeší pro rozšíření sady Visual Studio najdete na webu NuGet GitHub [3.2 milník](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Známé problémy

Pokračujeme v sledování problémů v našem seznamu problémů na Githubu najdete je na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)