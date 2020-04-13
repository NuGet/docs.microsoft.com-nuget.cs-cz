---
title: NuGet 4.8 RTM Poznámky k verzi
description: Poznámky k verzi pro NuGet 4.8.1 včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813764"
---
# <a name="nuget-48-release-notes"></a>NuGet 4.8 Poznámky k verzi

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) je dodáván s funkcí NuGet 4.8.


K dispozici jsou také verze příkazového řádku se stejnými funkcemi:
* NuGet.exe 4,8 - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>Shrnutí: Co je nového v 4.8.0
* NuGet.exe nyní podporuje longfilenames v systému Windows 10 - [#6937](https://github.com/NuGet/Home/issues/6937)
* Ověřovací moduly teď fungují napříč msbuild, DotNet.exe, NuGet.exe a Visual Studio, včetně multiplatformního. První generace ověřovacích modulů nebyly v souboru MsBuild, DotNet.exe podporovány. Poznámka: Sestavení VS 2017 15.9 Preview mají včetně modulu plug-in pro ověřování VSTS. [#6486](https://github.com/NuGet/Home/issues/6486)
* MsBuild Je SDK Resolver nyní staví jako součást NuGet a nainstaluje s nástroji NuGet pro VS. Tím se zabrání tomu, aby se verze dostaly ven z synchronizace. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference nyní podporuje metadata DevelopmentDependency - [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>Shrnutí: Co je nového v 4.8.2

* Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="known-issues"></a>Známé problémy
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Instalace podepsaných balíčků na počítači CI nebo v offline prostředí trvá déle než obvykle

#### <a name="issue"></a>Problém
Pokud má počítač omezený přístup k internetu (například sestavení počítače ve scénáři CI/CD), instalace nebo obnovení podepsaného balíčku nuget bude mít za následek upozornění ([NU3028](../reference/errors-and-warnings/nu3028.md)), protože servery pro odvolání nejsou dostupné. To se očekává. V některých případech to však může mít nezamýšlené concequences, jako je například instalace nebo obnovení balíčku trvá déle než obvykle.

#### <a name="workaround"></a>Alternativní řešení
Aktualizace Visual Studio 15.8.4 a NuGet.exe 4.8.1 kde jsme zavedli proměnnou prostředí přepnout režim kontroly odvolání.
Nastavení `NUGET_CERT_REVOCATION_MODE` proměnné prostředí `offline` vynutí NuGet zkontrolovat stav odvolání certifikátu pouze proti seznamu odvolaných certifikátů uložených v mezipaměti a NuGet se nepokusí dosáhnout odvolání serverů. Pokud je režim kontroly `offline`odvolání nastaven na , bude upozornění sníženo na informace.

> [!Warning]
> Nedoporučuje se přepínat režim kontroly odvolání do režimu offline za normálních podmínek. To způsobí, že NuGet přeskočit kontrolu odvolání online a provést pouze kontrolu odvolání offline proti seznamu odvolání certifikátu uloženého v mezipaměti, který může být zastaralý. To znamená, že balíčky, u kterých mohl být podpisový certifikát odvolán, budou nadále nainstalovány nebo obnoveny, což by jinak selhalo v kontrole odvolání a nebyly by nainstalovány.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Tato `Migrate packages.config to PackageReference...` možnost není k dispozici v kontextové nabídce po kliknutí pravým tlačítkem myši.

#### <a name="issue"></a>Problém

Při prvním otevření projektu NuGet nemusí mít inicializována, dokud není provedena operace NuGet. To způsobí, že možnost migrace se nezobrazí v `packages.config` `References`místní nabídce pravým tlačítkem myši na nebo .

#### <a name="workaround"></a>Alternativní řešení

Proveďte některou z následujících akcí NuGet:
* Otevřete ui Správce balíčků – `References` klikněte pravým tlačítkem myši a vyberte`Manage NuGet Packages...`
* Otevřete konzolu Správce `Tools > NuGet Package Manager`balíčků – od , vyberte`Package Manager Console`
* Spuštění obnovení NuGet – klikněte pravým tlačítkem myši na uzel řešení v Průzkumníku řešení a vyberte`Restore NuGet Packages`
* Sestavení projektu, který také aktivuje obnovení NuGet

Nyní byste měli mít možnost zobrazit možnost migrace. Všimněte si, že tato možnost není podporována a nezobrazí se pro typy projektů ASP.NET a C++.
Poznámka: Toto bylo opraveno ve VS 2017 15.9 Náhled 3

## <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

### <a name="bugs"></a>Chyby
#### <a name="signing"></a>certifikát
* Podepisování: Instalace podepsaného balíčku v offline prostředí [#7008](https://github.com/NuGet/Home/issues/7008) -- Opraveno v 4.8.1
* Podepisování: nesprávná kontrola adresy URL - [#7174](https://github.com/NuGet/Home/issues/7174)
* Podepisování: zkontrolujte integritu balíčku v úložištiSignatureVerifier, když je balíček spolupodepsaný - [#6926](https://github.com/NuGet/Home/issues/6926)
* "Kontrola integrity balíčku se nezdařila." by měl mít ID balíčku ve zprávě (a kód chyby) - [#6944](https://github.com/NuGet/Home/issues/6944)
* Ověření podepsaného balíčku úložiště umožňuje balíčky podepsané jiným certifikátem - [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet - Podepisování - Adresa URL časového razítka nemůže být https:// ? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Nenullref v NuSpec balení scénář, také zlepšit možnosti - [#6866](https://github.com/NuGet/Home/issues/6866)
* Paměť je neplatná při aktualizaci informací o autorovi podpisu při přidávání časového razítka k protipodpisu - [#6840](https://github.com/NuGet/Home/issues/6840)
* Podepisování: odebrání výjimek ctl - [#6794](https://github.com/NuGet/Home/issues/6794)
* Podepisování: contentUrl MUSÍ být HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)
* Podepisování: SignedPackageVerifierSettings.VSClientDefaultPolicy není použito - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Pack
* obnovení a sestavení by nemělo být potřeba při použití dotnet.exe zabalit nuspec - [#6866](https://github.com/NuGet/Home/issues/6866)
* Povolit prázdné náhradní tokeny v NuspecProperties - [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask vyvolá NullReferenceException, když je zadána vlastnost NuspecProperties - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Usnadnění
* [Přístupnost] Řetězec 'Předběžná verze' pod tlačítkem balíčku je pokryt popisem balíčku v pm ui - [#4504](https://github.com/NuGet/Home/issues/4504)
* [Přístupnost] Rozbalovací nabídka a nastavení zdroje balíčků se zkrátí při výběru offline balíčků Microsoft Visual Studio v uzlovém rozhraní PM – [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Konzola pro správu prostředí Powershell (PMC)
* `Update-Package`ignoruje rozsah verzí PackageReference - [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall`řešení široký problém - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall`přeinstaluje všechny balíčky namísto pouze pojmenované - [#737](https://github.com/NuGet/Home/issues/737)
* Může aktualizovat na neuvedený balíček NuGet z konzoly Správce balíčků - [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Různé
* Chcete-li opravit `NuGet update self` NGet.Commandline nupkg by neměl amed 2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)
* Zlepšete zkušenosti s chybami instalace NU1107 - [#7107](https://github.com/NuGet/Home/issues/7107)
* Serializace GetAuthenticationCredentialRequest je nesprávná - [#6983](https://github.com/NuGet/Home/issues/6983)
* NuGet Visual Studio AsyncPackage se nezdaří načíst při inicializování z vlákna uživatelského rozhraní - [#6976](https://github.com/NuGet/Home/issues/6976)
* Obnovení hlásí zavádějící chyby s uvedením project.json je potřeba - [#6959](https://github.com/NuGet/Home/issues/6959)
* Správce balíčků UI: náhled změn, ok tlačítko není automaticky použitelné pomocí klávesnice - [#6893](https://github.com/NuGet/Home/issues/6893)
* RestoreSources jsou ignorovány pro projekt s p2p odkazy - [#6776](https://github.com/NuGet/Home/issues/6776)
* Vytvoření projektu testování částí pomocí šablony rozhraní .NET Framework otevře starší model projektu s packages.config - [#6736](https://github.com/NuGet/Home/issues/6736)
* povolit odkaz projektu k přepsání závislosti balíčku - [#6536](https://github.com/NuGet/Home/issues/6536)
* Vystavit NoDefaultExcludes v úkolu MSBuild - [#6450](https://github.com/NuGet/Home/issues/6450)
* Stavová zpráva pro "Vymazat všechny mezipaměti NuGet" může být skryta v okně změnit velikost - [#5938](https://github.com/NuGet/Home/issues/5938)


[Seznam všech problémů opravených v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
