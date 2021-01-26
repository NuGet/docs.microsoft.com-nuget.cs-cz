---
title: Zpráva k vydání verze NuGet 3,2
description: Poznámky k verzi pro NuGet 3,2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 38a56b1572770b02ff09135a3b0290742ca80f41
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780303"
---
# <a name="nuget-32-release-notes"></a>Zpráva k vydání verze NuGet 3,2

Poznámky k verzi [pro NuGet 3,2 – RC](../release-notes/nuget-3.2-RC.md)  |  [Poznámky k verzi NuGet 3.2.1](../release-notes/nuget-3.2.1.md)

NuGet 3,2 byl vydán 16. září 2015 jako kolekce vylepšení a oprav pro vydání verze 3.1.1 a je k dispozici jak z [DIST.NuGet.org](http://dist.nuget.org/index.html) , tak i z [Galerie sady Visual Studio](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).

## <a name="new-features"></a>Nové funkce

* Projekty, které jsou ve stejné složce v reálném čase, teď mohou mít různé `project.json` soubory v dané složce specifické pro každý projekt.  Pro každý projekt `project.json` Zadejte název souboru `{ProjectName}.project.json` a NuGet pro každý projekt patřičně přizpůsobíte tuto konfiguraci.  Tato podpora se podporuje jenom u nainstalovaných nástrojů Windows 10 v 1.1 – [1102](https://github.com/NuGet/Home/issues/1102) .
* Klienti NuGet podporují zadání globální proměnné prostředí NUGET_PACKAGES k určení umístění sdílené globální složky balíčků používané ve `project.json` spravovaných projektech pomocí nástrojů Windows 10 v 1.1.

## <a name="command-line-updates"></a>Aktualizace příkazového řádku

Toto je první verze klienta nuget.exe, která podporuje servery NuGet v3 a obnovuje balíčky pro projekty spravované se `project.json` souborem.

V této verzi bylo k dispozici několik problémů s informačním kanálem, které byly vyřešeny pro zlepšení interakcí s klientem.

* Přihlašovací údaje pro instalaci/obnovení pouze odesílají pověření pro počáteční požadavek do ověřeného informačního kanálu – [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Příkaz push neřeší přihlašovací údaje z konfigurace- [1248](https://github.com/NuGet/Home/issues/1248)
* Uživatelský agent a hlavičky se teď odesílají do úložišť NuGet, které vám pomůžou sledovat statistiky – [929](https://github.com/NuGet/Home/issues/929) .

Provedli jsme řadu vylepšení pro lepší zpracování selhání sítě při pokusu o práci se vzdáleným úložištěm NuGet:

* Vylepšené chybové zprávy, když se nemůže připojit ke vzdáleným kanálům – [1238](https://github.com/NuGet/Home/issues/1238)
* Opravený příkaz pro obnovení NuGet pro správné vrácení 1, pokud dojde k chybě – [1186](https://github.com/NuGet/Home/issues/1186)
* Opakování pokusu o připojení k síti každých 200ms po dobu maximálně 5 pokusů v případě chyby HTTP 5xx – [1120](https://github.com/NuGet/Home/issues/1120)
* Vylepšené zpracování odpovědí přesměrování serveru během příkazu push- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` teď podporuje buď adresu URL, nebo název úložiště z Nuget.Config jako argument- [1046](https://github.com/NuGet/Home/issues/1046)
* Chybějící balíčky, které nebyly umístěny v úložišti během obnovy, jsou nyní hlášeny jako chyby namísto upozornění [1038](https://github.com/NuGet/Home/issues/1038)
* Opravené zpracování multipartwebrequest ve scénářích \r\n pro systémy UNIX a Linux – [776](https://github.com/NuGet/Home/issues/776)

K dispozici je několik oprav pro problémy s různými příkazy:

* Příkaz push už nefunguje před VLOŽENÍm na zdroj balíčku- [1237](https://github.com/NuGet/Home/issues/1237) .
* Příkaz list už neopakuje čísla verzí – [1185](https://github.com/NuGet/Home/issues/1185)
* Sada s argumentem-Build teď správně podporuje C# 6,0 – [1107](https://github.com/NuGet/Home/issues/1107) .
* Opravené problémy při pokusu o zabalení projektu F # sestaveného se sadou Visual Studio 2015 – [1048](https://github.com/NuGet/Home/issues/1048)
* Obnovit nyní No-OPS, když už existují balíčky – [1040](https://github.com/NuGet/Home/issues/1040)
* Vylepšené chybové zprávy, když `packages.config` je soubor poškozený- [1034](https://github.com/NuGet/Home/issues/1034)
* Oprava příkazu RESTORE s parametrem-SolutionDirectory pro práci s relativními cestami – [992](https://github.com/NuGet/Home/issues/992)
* Vylepšení aktualizovaného příkazu pro podporu aktualizace pro všechny řešení – [924](https://github.com/NuGet/Home/issues/924)

Úplný seznam problémů řešených v této verzi najdete v [milníku příkazového řádku](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)pro GitHub NuGet.

## <a name="visual-studio-extension-updates"></a>Aktualizace rozšíření sady Visual Studio

### <a name="new-features-in-visual-studio"></a>Nové funkce v aplikaci Visual Studio

* Do Průzkumník řešení v uzlu řešení byla přidána nová položka kontextové nabídky, která umožňuje obnovení balíčků bez sestavení řešení ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nová položka kontextové nabídky obnovit balíčky](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Aktualizace a opravy v aplikaci Visual Studio

Opravy pro ověřené informační kanály byly zahrnuty a řešeny také v rozšíření.  Následující ověřovací položky byly také adresovány v rozšíření:

* Nyní správně zpracovává správně ověřené informační kanály NuGet V3 místo verze V2 ověřované informační kanály – [1216](https://github.com/NuGet/Home/issues/1216)
* Opravený požadavek na přihlašovací údaje pro ověřování v projektech `project.json` , které používají a komunikují s kanály v2 – [1082](https://github.com/NuGet/Home/issues/1082)

Síťové připojení ovlivnilo uživatelské rozhraní v aplikaci Visual Studio a vyřešili jsme to s následujícími opravami:

* Vylepšená údržba místní mezipaměti verzí balíčků – [1096](https://github.com/NuGet/Home/issues/1096)
* Při připojování k informačnímu kanálu V3 došlo ke změně chování při selhání, aby se už nepokoušelo považovat za kanál v2 – [1253](https://github.com/NuGet/Home/issues/1253) .
* Nyní brání selhání instalace při instalaci balíčku s více zdroji balíčků – [1183](https://github.com/NuGet/Home/issues/1183)

Vylepšili jsme zpracování interakcí s operacemi sestavení:

* Nyní pokračuje v sestavování projektů, pokud se obnovení balíčků pro jeden projekt nezdařilo- [1169](https://github.com/NuGet/Home/issues/1169)
* Instalace balíčku do projektu, který je závislý na jiném projektu v řešení, vynutí opětovné sestavení řešení- [981](https://github.com/NuGet/Home/issues/981)
* Opravily se neúspěšné instalace balíčků pro správné vrácení změn projektu – [1265](https://github.com/NuGet/Home/issues/1265)
* Opravené nechtěné odebrání `developmentDependency` atributu v balíčku v `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Volání `install.ps1` nyní mají `$package.AssemblyReferences` předaný správný objekt- [1245](https://github.com/NuGet/Home/issues/1245)
* Už nebrání odinstalaci balíčků v projektech UWP, pokud je projekt ve špatném stavu – [1128](https://github.com/NuGet/Home/issues/1128) .
* Řešení obsahující kombinaci `packages.config` `project.json` projektů a jsou nyní správně sestavena bez nutnosti druhé operace sestavení- [1122](https://github.com/NuGet/Home/issues/1122)
* Správné umístění souborů app.config, pokud jsou propojené nebo umístěné v jiné složce – [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Projekty UWP teď můžou instalovat neuvedené balíčky – [1109](https://github.com/NuGet/Home/issues/1109)
* Obnovení balíčku je teď povolené, zatímco řešení není v uloženém stavu – [1081](https://github.com/NuGet/Home/issues/1081) .

Zpracování aktualizací konfiguračních souborů bylo opraveno:

* Už neodebíráte soubor cílů doručený z balíčku na následných sestaveních `project.json` spravovaného projektu – [1288](https://github.com/NuGet/Home/issues/1288)
* Už se nemění Nuget.Config soubory během buildu řešení ASP.NET 5 – [1201](https://github.com/NuGet/Home/issues/1201) .
* Již nemění se omezení povolených verzí během aktualizace balíčku- [1130](https://github.com/NuGet/Home/issues/1130)
* Zámek soubory nyní zůstane uzamčen během sestavování- [1127](https://github.com/NuGet/Home/issues/1127)
* Změny se teď upravují `packages.config` a nepřepisují během aktualizací – [585](https://github.com/NuGet/Home/issues/585)

Vylepšení interakcí se správou zdrojových kódů TFS:

* Neúspěšná instalace pro balíčky, které jsou svázané s TFS- [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Opravené uživatelské rozhraní NuGet pro povolení integrace TFS 2013- [1071](https://github.com/NuGet/Home/issues/1071)
* Opravené odkazy na balíčky obnovené tak, aby se správně pocházely ze složky balíčků – [1004](https://github.com/NuGet/Home/issues/1004)

Nakonec jsme vylepšili také tyto položky:

* Podrobnost protokolování zpráv protokolu pro `project.json` spravované projekty – [1163](https://github.com/NuGet/Home/issues/1163)
* V uživatelském rozhraní se teď správně zobrazuje nainstalovaná verze balíčku – [1061](https://github.com/NuGet/Home/issues/1061) .
* Balíčky s rozsahy závislosti zadanými ve svých nuspec nyní mají předprodejní verze těchto závislostí nainstalované pro stabilní verzi balíčku- [1304](https://github.com/NuGet/Home/issues/1304) .

Úplný seznam problémů řešených pro rozšíření sady Visual Studio najdete v [milníku NuGet 3,2](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2) .

## <a name="known-issues"></a>Známé problémy

Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)