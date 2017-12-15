---
title: "Poznámky k verzi NuGet 3.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 70316f35-f046-4f72-98e0-736de172e918
description: "Poznámky k verzi pro NuGet 3.2 včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.2 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 364a1ac62af25351e78df0b9a506f0919fc8fb61
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-32-release-notes"></a>Poznámky k verzi 3.2 NuGet

[Poznámky k verzi 3.2 RC NuGet](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 poznámky k verzi](../release-notes/nuget-3.2.1.md)

NuGet 3.2 byla vydaná verze 16 září 2015 jako kolekce vylepšení a opravy pro 3.1.1 a je dostupný z obou [dist.nuget.org](http://dist.nuget.org/index.html) a [Galerie sady Visual Studio](https://visualstudiogallery.msdn.microsoft.com/5d345edc-2e2d-4a9c-b73b-d53956dc458d?SRC=Home).

## <a name="new-features"></a>Nové funkce

* Projekty, které za provozu ve stejné složce, teď může mít různé `project.json` soubory v této složce, které jsou specifické pro každý projekt.  Pro každý projekt, název `project.json` soubor `{ProjectName}.project.json` a NuGet získáte preference tato konfigurace pro každý projekt, odpovídajícím způsobem.  Je podporováno pouze pomocí nástrojů pro Windows 10 verze 1.1 nainstalovaný - [1102](https://github.com/NuGet/Home/issues/1102)
* Klienti NuGet podporují zadání globální proměnné prostředí NUGET_PACKAGES k určení umístění složky sdíleného globální balíčky použít v `project.json` spravované projekty s v1.1 nástroje Windows 10.

## <a name="command-line-updates"></a>Aktualizace příkazového řádku

Toto je první verze součásti nuget.exe klienta, který podporuje servery NuGet v3 a obnovují se balíčky pro projekty spravované pomocí `project.json` souboru.

Došlo k několika ověřené informačního kanálu problémy, které byla provedena v této verzi ke zlepšení interakce s klientem.

* Instalace / obnovení interakce odeslat pouze přihlašovací údaje pro počáteční požadavek na ověřeného informačního kanálu - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Příkaz nabízené nevyřeší pověření z konfigurace – [1248](https://github.com/NuGet/Home/issues/1248)
* Uživatelský agent a hlavičky se teď odešlou do úložiště NuGet, které pomáhají při sledování statistiky - [929](https://github.com/NuGet/Home/issues/929)

Jsme provedli několik vylepšení lépe řešit selhání sítě při pokusu o práci s vzdáleného úložiště NuGet:

* Vylepšené chybové zprávy, když nelze se připojit ke vzdálené kanály - [. 1238](https://github.com/NuGet/Home/issues/1238)
* Opravě příkazu restore NuGet správně vrátit 1, když dojde k chybě - [1186](https://github.com/NuGet/Home/issues/1186)
* Nyní opakování pokusu o připojení k síti každých 200 MS maximálně 5 pokusů v případě chyby HTTP 5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* Vylepšené zpracování přesměrování odpovědí serveru během nabízené command - [. 1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source`Teď podporuje název adresy URL nebo úložiště ze souboru Nuget.Config jako argument - [1046](https://github.com/NuGet/Home/issues/1046)
* Chybějící balíčky, které nebyly umístěny v úložiště během obnovení jsou nyní oznamovány klientu jako chyby místo upozornění [1038](https://github.com/NuGet/Home/issues/1038)
* Opraveny multipartwebrequest zpracování \r\n pro scénáře, platformy Unix/Linux - [. 776](https://github.com/NuGet/Home/issues/776)

Existuje několik problémů, které na problémy s různými příkazy:

* Příkaz nabízené již nemá GET před PUT proti zdroji balíčku - [. 1237](https://github.com/NuGet/Home/issues/1237)
* Příkaz seznamu už opakuje čísla verze – [1185](https://github.com/NuGet/Home/issues/1185)
* Pack s argumentem - sestavení nyní správně podporuje C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Opravené problémy při pokusu o pack projektu F # vytvořené s nástroji Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* V případě balíčků již existuje - obnovit teď ne ops [1040](https://github.com/NuGet/Home/issues/1040)
* Vylepšené chybové zprávy, když `packages.config` soubor je poškozený. - [1034](https://github.com/NuGet/Home/issues/1034)
* Opravě příkazu restore s přepínačem - SolutionDirectory pro práci s relativní cesty - [992](https://github.com/NuGet/Home/issues/992)
* Vylepšené aktualizované příkaz pro podporu celé řešení aktualizace – [924](https://github.com/NuGet/Home/issues/924)

Úplný seznam problémů popsaných v této verzi najdete v Githubu NuGet [příkazového řádku milník](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Aktualizace rozšíření Visual Studio

### <a name="new-features-in-visual-studio"></a>Nové funkce v sadě Visual Studio

* Nové položky kontextové nabídky byl přidán do Průzkumníka řešení na uzlu řešení, který umožňuje balíčky obnovit bez vytváření řešení ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nové, obnovení balíčků' položky kontextové nabídky](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Aktualizace a opravy v sadě Visual Studio

Opravy pro ověřený kanály byly zahrnuté a aplikace také rozšíření.  Následující položky ověřování byla provedena také v rozšíření:

* Nyní správně považuje NuGet v3 ověřený informační kanály správně, místo jako v2 ověřená informační kanály - [1216](https://github.com/NuGet/Home/issues/1216)
* Opravené žádost o pověření pro ověření v projektech pomocí `project.json` a komunikaci s v2 kanály - [1082](https://github.com/NuGet/Home/issues/1082)

Připojení k síti měla vliv na uživatelské rozhraní v sadě Visual Studio a jsme to řešit pomocí následující opravy:

* Vylepšení údržby místní mezipaměti verze balíčku - [1096](https://github.com/NuGet/Home/issues/1096)
* Změnit chování selhání při připojování k v3, informační kanál už pokus o považovat za informačního kanálu v2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Nyní brání instalaci selhání při instalaci balíčku pro více zdrojů balíčku - [1183](https://github.com/NuGet/Home/issues/1183)

Vylepšili zpracování interakce s operacemi sestavení:

* Nyní budete pokračovat k vytvoření projektů, pokud probíhá obnovení balíčků pro projekt selže - [1169](https://github.com/NuGet/Home/issues/1169)
* Instalaci balíčku do projektu, který závisí na jiném projektu v řešení vynutí opětovném sestavení řešení - [981](https://github.com/NuGet/Home/issues/981)
* Opravě nainstaluje balíček, který selhal provedené správně změny vrátit do projektu - [. 1265](https://github.com/NuGet/Home/issues/1265)
* Opravě neúmyslného odstranění `developmentDependency` atribut na balíček v `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Volání `install.ps1` Teď máte správný `$package.AssemblyReferences` objekt předaný - [1245](https://github.com/NuGet/Home/issues/1245)
* Již nadále nebrání odinstaluje balíčků v projekty UWP při projekt je ve špatném stavu - [. 1128](https://github.com/NuGet/Home/issues/1128)
* Řešení obsahující směs `packages.config` a `project.json` projekty jsou nyní správně vytvořen bez nutnosti druhý sestavení operace – [1122](https://github.com/NuGet/Home/issues/1122)
* Soubory app.config správně hledání, pokud jsou propojené nebo nachází v jiné složce - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Projekty UWP nyní mohou instalovat balíčky neuvedené - [1109](https://github.com/NuGet/Home/issues/1109)
* Obnovení balíčků je nyní povoleno při řešení není v uloženém stavu - [. 1081](https://github.com/NuGet/Home/issues/1081)

Zpracování aktualizace konfigurace, které byly opraveny soubory:

* Odebrání už soubor cíle doručit z balíčku na následné buildů `project.json` spravovaný projekt - [1288](https://github.com/NuGet/Home/issues/1288)
* Už během vytváření sestavení řešení ASP.NET 5 - Změna Nuget.Config souborů [1201](https://github.com/NuGet/Home/issues/1201)
* Během aktualizace balíčku - už změna povoleno omezení verze [1130](https://github.com/NuGet/Home/issues/1130)
* Soubory zámku teď zůstanou po sestavení - [1127](https://github.com/NuGet/Home/issues/1127)
* Provádí úpravu `packages.config` a není je přepisování během aktualizace – [585](https://github.com/NuGet/Home/issues/585)

Interakce s TFS zdrojového kódu se zlepší:

* Už selhání instalace pro balíčky, které jsou vázány na TFS - [. 1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Opravené NuGet uživatelské rozhraní pro integraci sady TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Opravě odkazy na balíčky obnovit správně pocházet ze složky balíčků - [1004](https://github.com/NuGet/Home/issues/1004)

Nakonec vylepšili také tyto položky:

* Podrobnosti zprávy protokolu omezení pro `project.json` spravované projekty - [1163](https://github.com/NuGet/Home/issues/1163)
* Nyní správně zobrazení nainstalovaná verze balíčku v uživatelském rozhraní - [1061](https://github.com/NuGet/Home/issues/1061)
* Balíčky s závislostí rozsahů určených v jejich nuspec teď obsahují předprodejní verze těchto závislostí pro balíček stabilní verze - nainstalována [1304](https://github.com/NuGet/Home/issues/1304)

Úplný seznam problémů řešit pro rozšíření sady Visual Studio naleznete na webu NuGet GitHub [3.2 milník](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Známé problémy

Abychom mohli pokračovat ke sledování problémů na našich seznamu problémy Githubu, které naleznete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)